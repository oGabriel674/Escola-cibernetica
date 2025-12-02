# CTF - Natas (OverTheWire)
### solução de 0 → 15
###### solved by @oGabriel674

> Esta é uma série de desafios voltados para a exploração de vulnerabilidades e fundamentos de segurança web.

## O que é o Natas?
- Parte da plataforma OverTheWire, que oferece diversos wargames para aprendizado em segurança da informação.
- Focado em segurança web server-side, ou seja, vulnerabilidades que ocorrem no servidor de um site.

- [Página do desafio](https://overthewire.org/wargames/natas/)
  
#### Descrição

O desafio tem início no nível 0. Cada fase apresenta uma página web vulnerável, projetada para expor falhas comuns em aplicações web. O objetivo principal é identificar e explorar essas vulnerabilidades para descobrir a senha que desbloqueia o próximo nível.

#### nível 0

acessível através das credenciais padrão (natas0 / natas0).

#### nível 0 → 1

No início, nos deparamos com a seguinte página, que exibe a seguinte mensagem:

<img width="747" height="146" alt="Captura de tela 2025-11-11 161446" src="https://github.com/user-attachments/assets/cd31dde5-c5c0-48d0-8909-9612503d0482" />

A solução para este nível é bastante simples: ao inspecionar o código-fonte da página, é possível localizar a chave de acesso para o próximo desafio.

<img width="689" height="442" alt="Captura de tela 2025-11-11 161430" src="https://github.com/user-attachments/assets/35c2661b-66c8-4b15-a24e-c8076f825aa0" />

> chave: 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq

#### nível 1 → 2

> credenciais: natas1 / 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq

No nível seguinte, nos deparamos com uma restrição adicional: o clique com o botão direito do mouse está desabilitado, o que dificulta o acesso direto ao código-fonte da página.

<img width="750" height="172" alt="Captura de tela 2025-11-20 204055" src="https://github.com/user-attachments/assets/bf174390-971b-420d-87ec-99dd2e8c3997" />

<img width="547" height="147" alt="Captura de tela 2025-11-20 204818" src="https://github.com/user-attachments/assets/0362371a-4e83-4b0a-803c-54aae97fb3c2" />

Para contornar este bloqueio, é possível utilizar o atalho do teclado `Ctrl + U`, que permite visualizar o código-fonte da página diretamente, mesmo com o clique direito desabilitado.

Após acessar o código-fonte da página, rapidamente identificamos a chave necessária para avançar ao próximo nível do desafio.

<img width="1334" height="404" alt="Captura de tela 2025-11-20 205909" src="https://github.com/user-attachments/assets/9f285847-6649-448f-8179-cd820f40f561" />

> chave: TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI

#### nível 2 → 3

> credenciais: natas2 / TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI

Neste nível, é exibida a mensagem:

<img width="747" height="143" alt="Captura de tela 2025-11-20 210520" src="https://github.com/user-attachments/assets/5c0c66b9-6690-4c7c-b9aa-1c3537798602" />

Analizando o código-fonte da página, identificamos um link suspeito, que possivelmente està relacionado à progressão do desafio.

<img width="1346" height="332" alt="Captura de tela 2025-11-20 211600" src="https://github.com/user-attachments/assets/84fd8965-d602-4e68-bf63-0e76faa97dc1" />

Ao acessarmos o link, somos redirecionados para uma nova página que, aparentemente, não fornece nenhuma informação visível de imediato, exibindo apenas um pequeno pixel.

<img width="535" height="360" alt="Captura de tela 2025-11-20 212106" src="https://github.com/user-attachments/assets/a40fbe6c-afe0-45bc-b9f0-8c4ad6903543" />

Ao observar com um pouco mais de atenção o link identificado, notamos que ele contém um caminho adicional na [URL](https://tecnoblog.net/responde/o-que-e-url/) , especificamente um diretório denominado `/files/` antes do arquivo pixel.png, podendo indicar a existência de outros recursos acessíveis nesse mesmo diretório.

Acessando o diretório /files/, encontramos um arquivo denominado user.txt.

<img width="671" height="332" alt="Captura de tela 2025-11-20 213507" src="https://github.com/user-attachments/assets/517d3439-d44f-467f-af1c-41118d1074eb" />

Ao acessá-lo, encontramos a chave necessária para avançar ao próximo nível do desafio.

<img width="385" height="154" alt="Captura de tela 2025-11-20 213443" src="https://github.com/user-attachments/assets/60f897e4-5e29-42ae-b068-5681f95e3048" />

> chave: 3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH

#### nível 3 → 4

> credenciais: natas3 / 3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH

Novamente, é exibida a mensagem:

<img width="747" height="143" alt="Captura de tela 2025-11-20 210520" src="https://github.com/user-attachments/assets/4586121b-a7ec-44a2-9f97-cdfd9bbca060" />

A análise do código-fonte revela uma dica sutil, indicando que o conteúdo não está indexado por mecanismos de busca.

<img width="1366" height="328" alt="Captura de tela 2025-11-20 214604" src="https://github.com/user-attachments/assets/601b64bf-d8c6-4cca-99da-cbcbe470d2bd" />

Ao analisarmos o arquivo `/robots.txt` — que contém instruções para robôs de mecanismos de busca, como o Googlebot, sobre quais páginas ou seções do site devem ser rastreadas ou ignoradas — identificamos um novo diretório `/s3cr3t/`. Ao acessá-lo, encontramos novamente uma página com um arquivo denominado user.txt.

<img width="677" height="332" alt="Captura de tela 2025-11-20 215114" src="https://github.com/user-attachments/assets/0cf3981c-b57d-494f-a765-5224668db988" />

Ao abrir o arquivo, encontramos a chave necessária para avançar para o próximo nível.

<img width="366" height="42" alt="Captura de tela 2025-11-20 215131" src="https://github.com/user-attachments/assets/4271e0bd-21b5-419f-ba1e-b4e68fb2569f" /> 

> chave: QryZXc2e0zahULdHrtHxzyYkj59kUxLQ

#### nível 4 → 5

> credenciais: natas4 / QryZXc2e0zahULdHrtHxzyYkj59kUxLQ

Neste novo nível, somos apresentados à seguinte frase:

<img width="745" height="191" alt="Captura de tela 2025-11-26 213253" src="https://github.com/user-attachments/assets/43724b43-32ae-4c4a-8bda-752cb5662c94" />

Ao recarregar a página, uma nova frase é exibida:

<img width="749" height="210" alt="Captura de tela 2025-11-26 213526" src="https://github.com/user-attachments/assets/62314d18-9706-4dcd-a8ab-679b0de3a34a" />

Indicando que a chave só poderá ser acessada por um usuário autorizado; nesse caso, o acesso deve ocorrer a partir de `http://natas5.natas.labs.overthewire.org/`

Para contornar isso, utilizamos o Burp Suite, que funciona como um proxy capaz de interceptar e manipular o tráfego entre o navegador e o servidor.

Com o Burp Suite aberto e o navegador configurado para utilizar o proxy, acesse `http://natas4.natas.labs.overthewire.org/`para que a requisição seja capturada em __Proxy → Intercept__. Na mensagem interceptada, localizamos o cabeçalho __Referer__, que aparece como `Referer: http://natas4.natas.labs.overthewire.org/`, e o substituimos por `Referer: http://natas5.natas.labs.overthewire.org/`. 

<img width="1905" height="786" alt="Screenshot_2025-11-26_18_48_10" src="https://github.com/user-attachments/assets/05027ee4-5acf-49c9-8dde-798fbd663fb4" />

Em seguida, encaminhamos a requisição com __Forward__ para que o servidor a aceite como proveniente do domínio autorizado. Com essa alteração, a página correta será retornada e a resposta exibirá a senha necessária para acessar o próximo nível (Natas5).

<img width="598" height="157" alt="Screenshot_2025-11-26_18_52_16" src="https://github.com/user-attachments/assets/da7181ca-c38d-4d86-b38d-14a97f2856ed" />

> chave: 0n35PkgqAPm2zbEpOU802c0x0Msn1ToK

#### nível 5 → 6

> credenciais: natas5 / 0n35PkgqAPm2zbEpOU802c0x0Msn1ToK

Enunciado do nível:
 
<img width="749" height="144" alt="Captura de tela 2025-11-26 220402" src="https://github.com/user-attachments/assets/01259568-979f-4daf-ac02-dbd784cd8a89" />

De acordo com o enunciado, o desafio verifica se o usuário está autenticado ou não. É provável que o site utilize [cookies de sessão](https://www.cookieyes.com/blog/session-cookies/) para controlar o estado de login. Com base nisso, o objetivo passa a ser identificar o cookie responsável pela autenticação e manipular seu valor de forma a simular um usuário autorizado.

Para realizar essa manipulação, é necessário acessar o [__DevTools__](https://learn.microsoft.com/pt-br/microsoft-edge/devtools/overview) do navegador e abrir a aba de Cookies. Em seguida, deve-se localizar o cookie associado ao domínio `natas5.natas.labs.overthewire.or`. Após identificar o cookie responsável pela autenticação, basta alterar seu valor — que provavelmente estará definido como __0__ — para __1__, simulando assim um estado de usuário autenticado.

<img width="1920" height="251" alt="Screenshot_2025-11-26_20_40_37" src="https://github.com/user-attachments/assets/2fe437d5-0f0b-4170-bf2c-452e320c518a" />

Essa modificação permite contornar a verificação de autenticação e acessar a chave necessária para avançar ao próximo nível do desafio

<img width="599" height="134" alt="Screenshot_2025-11-26_20_40_54" src="https://github.com/user-attachments/assets/00cd14b9-c4a4-4977-9d6a-ff85c2607d8a" />

> chave: 0RoJwHdSKWFTYR5WuiAewauSuNaBXned

#### nível 6 → 7

> credenciais: natas6 / 0RoJwHdSKWFTYR5WuiAewauSuNaBXned

Enunciado do nível:

<img width="752" height="212" alt="Captura de tela 2025-11-27 202754" src="https://github.com/user-attachments/assets/709cd444-9a4f-48e7-8260-57ad9a03accf" />

A página solicita uma __“entrada secreta”__ como condição para revelar a chave de acesso ao próximo nível do desafio.

Além disso, a página disponibiliza um link que permite acessar diretamente o código-fonte da aplicação. Ao abrir esse recurso, nos deparamos com o seguinte trecho de código, que revela a lógica utilizada pelo servidor para validar a “entrada secreta” e controlar o acesso à chave do próximo nível.

<img width="1428" height="691" alt="Captura de tela 2025-11-27 201823" src="https://github.com/user-attachments/assets/79151f9e-3063-4433-8900-38056e3968d7" />

Ao analisar o código, identificamos uma linha com a seguinte estrutura:

`include "includes/secret.inc";`

Esse trecho revela que o sistema está importando um arquivo externo, localizado em __includes/secret.inc__. Isso indica que a chave necessária para avançar no desafio está acessível diretamente por meio dessa URL. Assim, ao acessar o caminho correspondente no navegador, conseguimos visualizar o conteúdo do arquivo e obter a entrada sevreta.

<img width="331" height="74" alt="Captura de tela 2025-11-27 202548" src="https://github.com/user-attachments/assets/01855284-7112-4f0d-9955-19c43277cf60" />

Ao fornecer a entrada secreta, a aplicação valida o acesso e retorna a chave necessária para avançar ao próximo nível do desafio.

<img width="747" height="265" alt="Captura de tela 2025-11-27 202842" src="https://github.com/user-attachments/assets/81b0ca8d-9e4a-42bc-a43f-a84cb828067e" />

> chave: bmg8SvU1LizuWjx3y7xkNERkHxGre0GS

#### nível 7 → 8

> credenciais: natas7 / bmg8SvU1LizuWjx3y7xkNERkHxGre0GS

A página disponibiliza os seguintes links:

<img width="743" height="174" alt="Captura de tela 2025-11-27 211624" src="https://github.com/user-attachments/assets/d496ba13-e3b5-4bc2-8a3b-10da587997f6" />

Ao acessar um dos links fornecidos, é possível observar que a página utiliza o parâmetro `page` para decidir qual arquivo será incluído e exibido.

<img width="465" height="40" alt="Captura de tela 2025-11-27 214529" src="https://github.com/user-attachments/assets/a082a7f2-fc8b-4778-a68b-1a9b1128a787" />

Se o código da aplicação permite incluir qualquer arquivo por meio do parâmetro page, podemos explorar essa funcionalidade para “forçar” o site a carregar o arquivo secreto. Os níveis do Natas seguem um padrão em que a senha para o próximo nível fica armazenada em um arquivo dentro da pasta `/etc/natas_webpass/`. Assim, ao manipular a URL e definir o parâmetro page para apontar diretamente para esse arquivo, conseguimos que o servidor o inclua e exiba seu conteúdo. 

<img width="624" height="32" alt="Captura de tela 2025-11-27 215343" src="https://github.com/user-attachments/assets/c1a182b6-624c-4858-8fbb-eeb94b113d25" />

Dessa forma, obtemos a chave necessária para avançar ao próximo desafio.

<img width="745" height="186" alt="Captura de tela 2025-11-27 213554" src="https://github.com/user-attachments/assets/218cb7f6-81d6-4785-8ec7-c8f295370db0" />

> chave: xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q

#### nível 8 → 9

> credenciais: natas8 / xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q

Assim como em níveis anteriores, a página novamente solicita uma __“entrada secreta”__ como condição para liberar a chave de acesso ao próximo desafio.

<img width="747" height="219" alt="Captura de tela 2025-11-27 223727" src="https://github.com/user-attachments/assets/c858c0d0-a7c3-4d1b-bf5e-68048dd5e4b7" />

Além disso, é disponibilizado um link para o código-fonte.

<img width="1335" height="809" alt="Captura de tela 2025-11-27 223956" src="https://github.com/user-attachments/assets/15c7300c-fce0-455b-9058-e06b501f42dd" />

Ao analisar o código-fonte, percebemos que a aplicação espera uma entrada igual a __3d3d516343746d4d6d6c315669563362__. No entanto, essa entrada não é utilizada diretamente, pois passa por uma transformação realizada pela função `encodeSecret()`. 

Utilizando o seguinte script em [Python](https://aws.amazon.com/pt/what-is/python/), conseguimos inverter o processo aplicado pela função e recuperar o valor original da entrada secreta.

```
import base64

secret = "3d3d516343746d4d6d6c315669563362"
secret = bytes.fromhex(secret)
secret = secret[::-1]
secret = base64.decodebytes(secret)

print(secret)

```
> resposta: oubWYf2kBq

Ao inserir a entrada correta, a aplicação valida o valor fornecido e libera o acesso à chave do próximo nível.

<img width="744" height="262" alt="Captura de tela 2025-11-27 223204" src="https://github.com/user-attachments/assets/dfed4ea4-7fa1-438f-bf64-870486c53b54" />

> chave: ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t

#### nível 9 → 10

> credenciais: natas9 / ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t

O nível possuiu o seguinte enunciado:

<img width="748" height="254" alt="Captura de tela 2025-11-27 230756" src="https://github.com/user-attachments/assets/27f621ea-29c4-450c-8d65-e087955fdb8b" />

E novamente um link para acessar o código-fonte.

<img width="1374" height="731" alt="Captura de tela 2025-11-27 231116" src="https://github.com/user-attachments/assets/faf6e047-01fc-4cef-b779-45f923130226" />


Ao analisar o código, podemos perceber a possibilidade de injeção de comandos.

Portanto, ao inserir o comando `; cat /etc/natas_webpass/natas10` no campo de busca, a aplicação executa esse trecho adicional no [shell](https://www.datacamp.com/pt/blog/what-is-shell). Isso acontece porque o caractere `;` atua como um separador de comandos, permitindo que instruções diferentes sejam encadeadas. Dessa forma, conseguimos forçar o sistema a exibir diretamente o conteúdo do arquivo que contém a senha do próximo nível

<img width="746" height="207" alt="Captura de tela 2025-11-27 232644" src="https://github.com/user-attachments/assets/30926a2f-5709-4462-99e1-8ea24d7dde47" />

> chave: t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu

#### nível 10 → 11


> credenciais: natas10 / t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu

O nível possuiu o seguinte enunciado:

<img width="751" height="305" alt="Captura de tela 2025-11-28 183014" src="https://github.com/user-attachments/assets/7c682c8c-8ea2-49c2-9479-05c4f7cebb4d" />

Assim como no nível anterior, novamente nos é fornecido um link para o código-fonte da aplicação.

<img width="1405" height="851" alt="Captura de tela 2025-11-28 183727" src="https://github.com/user-attachments/assets/d8d43c02-4648-4eb3-b2b0-2e5220af7622" />

Ao analisar o código-fonte, percebemos que sua estrutura é bastante semelhante à do nível anterior. No entanto, há uma diferença importante, foram adicionadas restrições quanto aos caracteres permitidos na entrada.

Utilizando a expressão `.* /etc/natas_webpass/natas11` como entrada, conseguimos explorar a forma como a aplicação trata os parâmetros e, com isso, forçar a leitura de arquivos específicos dentro de um diretório.

O uso de `.*` funciona como um coringa, permitindo que o sistema interprete a entrada de maneira mais ampla e aceite caminhos adicionais. Dessa forma, é possível direcionar a aplicação para incluir o arquivo que contém a senha do próximo nível, mesmo diante das restrições impostas pelo código.

<img width="747" height="333" alt="Captura de tela 2025-11-28 184015" src="https://github.com/user-attachments/assets/47b92a63-b178-4b85-a87c-b81bee662206" />

> chave: UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk

#### nível 11 → 12

> credenciais: natas11 / UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk

O enunciado informa que os cookies estão protegidos por uma criptografia [XOR](https://pt.khanacademy.org/computing/computer-science/cryptography/ciphers/a/xor-bitwise-operation). Isso significa que o valor armazenado no cookie não é salvo em texto "claro", mas sim após passar por uma operação de XOR com uma chave definida pelo sistema. Esse tipo de criptografia é relativamente simples: cada byte do texto original é combinado com um byte da chave por meio da operação lógica XOR, resultando em um valor aparentemente aleatório. 

<img width="672" height="215" alt="Captura de tela 2025-11-28 184645" src="https://github.com/user-attachments/assets/883a6977-9e77-4f9d-80c1-96583cb98625" />

A aplicação oferece a possibilidade de selecionar a cor do background do site. Esse recurso, embora pareça apenas estético, está diretamente ligado ao funcionamento dos cookies e à forma como eles são manipulados.

Além disso, o cookie contém o campo `showpassword`, inicialmente definido como `no`. A lógica do sistema indica que, se esse valor for alterado para `yes`, a aplicação revelará a senha do próximo nível. O problema é que o cookie não está armazenado em texto puro: ele passa por uma função chamada `xor_encrypt()`, que aplica uma criptografia simples baseada em XOR.
Como não temos acesso direto à chave utilizada por essa função, não é possível modificar o cookie manualmente de forma imediata. O desafio, portanto, consiste em descobrir ou deduzir a chave XOR para que possamos decifrar o cookie atual, alterar o campo `showpassword` para `yes`, e então recriptografar o valor corretamente. Só assim o sistema aceitará o cookie modificado e exibirá a senha.

Para validar o funcionamento da criptografia XOR e gerar o novo cookie, podemos utilizar um [compilador PHP online](https://www.programiz.com/php/online-compiler/) junto com o seguinte código:

 ```
function  xor_encrypt_2 ( $in ) {                   
      $key = base64_decode ( "HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyJvTRg%3D" );                   
      $text = $in ;                   
      $outText = '' ;             
                        
      for ( $i = 0 ; $i < strlen ( $text ); $i ++) {            
  $outText .= $text [ $i ] ^ $key [ $i % strlen ( $key )];                   
      }                   
      return  $outText ;                       
          }                        

          $mydata = array ( "showpassword" => "no" , "bgcolor" => "#ffffff" );                       
          $mydata_json = json_encode ( $mydata );                       
          $mydata_enc = xor_encrypt_2 ( $mydata_json );                       
          echo  $mydata_enc ;  
 ```

<img width="1433" height="494" alt="Captura de tela 2025-11-29 154921" src="https://github.com/user-attachments/assets/5302466a-afe3-495a-a60f-a18a79c21162" />

> respsta: eDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeDWoeD	

Após isso, precisamos codificar o novo cookie para "yes" como valor para "showpassword", utilizando o seguinte script:

```
  function  xor_encrypt_2 ( $in ) {                   
    $key = "eDWo" ;                   
    $text = $in ;                   
    $outText = '' ; 
                                    
    for ( $i = 0 ; $i < strlen ( $text ); $i ++) {            
  $outText .= $text [ $i ] ^ $key [ $i % strlen ( $key )];                   
      }                   
      return  $outText ;                       
          }                        
          $mydata = array ( "showpassword" => "yes" , "bgcolor" => "#ffffff" ); 
          $mydata_json = json_encode ( $mydata );                       
          $mydata_enc = xor_encrypt_2 ( $mydata_json );                       
          $mydata_b64 = base64_encode ( $mydata_enc );                       
          echo  $mydata_b64 ;

```

<img width="1419" height="443" alt="Captura de tela 2025-11-29 155204" src="https://github.com/user-attachments/assets/b28f0c29-2729-4f9f-ad5d-47be10b0bd15" />

> valor do novo cookie: HmYkBwozJw4WNyAAFyB1VUc9MhxHaHUNAic4Awo2dVVHZzEJAyIxCUc5

Com o novo valor do cookie, o passo final é editar o cookie - com o nome de "data" - diretamente no navegador. Para isso, podemos utilizar as ferramentas de desenvolvedor (DevTools) disponível no navegador.

<img width="749" height="658" alt="Captura de tela 2025-11-29 155914" src="https://github.com/user-attachments/assets/ecce2691-e6e5-4f85-8b07-4704cd0de28e" />

E assim, basta recarregar a página para obtermos a chave para o proximo nível.

<img width="675" height="235" alt="Captura de tela 2025-11-29 151738" src="https://github.com/user-attachments/assets/909aa85f-a755-46bc-90f5-8994665da52b" />

> chave: yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB

#### nível 12 → 13

> credenciais: natas12 / yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB

Neste nível, a aplicação nos pede para enviar um arquivo [JPEG](https://www.adobe.com/br/creativecloud/file-types/image/raster/jpeg-file.html) com tamanho máximo de 1KB. Essa restrição de tamanho é proposital: ela impede que façamos upload de imagens comuns, que geralmente ultrapassam facilmente esse limite. 

<img width="675" height="219" alt="Captura de tela 2025-11-29 163500" src="https://github.com/user-attachments/assets/bce96671-aaff-4e21-a05c-5623aeffdebc" />

Assim como nos níveis anteriores, este desafio disponibiliza o código-fonte da aplicação.

```

<html>
<head>
<!-- This stuff in the header has nothing to do with the level -->
<link rel="stylesheet" type="text/css" href="http://natas.labs.overthewire.org/css/level.css">
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/jquery-ui.css" />
<link rel="stylesheet" href="http://natas.labs.overthewire.org/css/wechall.css" />
<script src="http://natas.labs.overthewire.org/js/jquery-1.9.1.js"></script>
<script src="http://natas.labs.overthewire.org/js/jquery-ui.js"></script>
<script src=http://natas.labs.overthewire.org/js/wechall-data.js></script><script src="http://natas.labs.overthewire.org/js/wechall.js"></script>
<script>var wechallinfo = { "level": "natas12", "pass": "<censored>" };</script></head>
<body>
<h1>natas12</h1>
<div id="content">
<?php

function genRandomString() {
    $length = 10;
    $characters = "0123456789abcdefghijklmnopqrstuvwxyz";
    $string = "";

    for ($p = 0; $p < $length; $p++) {
        $string .= $characters[mt_rand(0, strlen($characters)-1)];
    }

    return $string;
}

function makeRandomPath($dir, $ext) {
    do {
    $path = $dir."/".genRandomString().".".$ext;
    } while(file_exists($path));
    return $path;
}

function makeRandomPathFromFilename($dir, $fn) {
    $ext = pathinfo($fn, PATHINFO_EXTENSION);
    return makeRandomPath($dir, $ext);
}

if(array_key_exists("filename", $_POST)) {
    $target_path = makeRandomPathFromFilename("upload", $_POST["filename"]);


        if(filesize($_FILES['uploadedfile']['tmp_name']) > 1000) {
        echo "File is too big";
    } else {
        if(move_uploaded_file($_FILES['uploadedfile']['tmp_name'], $target_path)) {
            echo "The file <a href=\"$target_path\">$target_path</a> has been uploaded";
        } else{
            echo "There was an error uploading the file, please try again!";
        }
    }
} else {
?>

<form enctype="multipart/form-data" action="index.php" method="POST">
<input type="hidden" name="MAX_FILE_SIZE" value="1000" />
<input type="hidden" name="filename" value="<?php print genRandomString(); ?>.jpg" />
Choose a JPEG to upload (max 1KB):<br/>
<input name="uploadedfile" type="file" /><br />
<input type="submit" value="Upload File" />
</form>
<?php } ?>
<div id="viewsource"><a href="index-source.html">View sourcecode</a></div>
</div>
</body>
</html>

```

Observando o código-fonte, é possivel notar que o servidor verifica a extensão do arquivo, mas não o conteúdo do arquivo.

<img width="949" height="166" alt="Captura de tela 2025-11-29 165932" src="https://github.com/user-attachments/assets/95223f58-8bb6-423b-8d73-bc8d16437545" />

Também é possível notar que a extensão `.jpg` está sendo adicionada diretamente ao formulário HTML, tornando-o editável nas Ferramentas de DevTools. 

Podemos explorar isso criando um script PHP no terminal do [linux](https://www.ibm.com/br-pt/think/topics/linux):

`nano shell.php`

Após isso, abrimos as ferramentas de DevTools e alteramos o elemento do formulário HTML (provavelmente será algo similar a `<input type="hidden" name="filename" value="abc123.jpg">`) para `<input type="hidden" name="filename" value="abc123.php">`.

<img width="1277" height="461" alt="Captura de tela 2025-11-29 191135" src="https://github.com/user-attachments/assets/2c24a2ea-ceb3-4501-91e9-e7e9f20e54a8" />

Após editar o formulário e alterar a extensão para `.php`, realizamos o upload do arquivo para o servidor. O servidor salva o arquivo com o nome: 

`upload/abc123.php`

 Em seguida, basta acessar o link gerado após o upload. Como o arquivo contém código PHP válido, ao ser acessado ele será executado pelo servidor e o resultado será a chave para o próximo nível.

<img width="383" height="43" alt="Captura de tela 2025-11-29 192128" src="https://github.com/user-attachments/assets/7792aeeb-adeb-4ffe-acde-902a3a0a48a7" />

> chave: trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC

#### nível 13 → 14

> credenciais: natas13 / trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC

