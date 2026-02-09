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
 
O sufixo __`.phps`__ se refere a um arquivo de código-fonte PHP formatado ([__PHP Source__](https://lbodev.com.br/glossario/o-que-e-php-source-code-management/#google_vignette)). Diferentemente de um arquivo .php comum, que é interpretado e executado pelo servidor para gerar uma página funcional, o arquivo .phps é configurado para exibir o código-fonte de forma legível, geralmente com realce de sintaxe (syntax highlighting). Essa característica permite visualizar diretamente a lógica implementada, sem que o servidor execute o script."
