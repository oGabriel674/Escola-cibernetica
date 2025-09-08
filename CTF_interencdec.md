# CTF Interencdec (Cryptography)
###### solved by @oGabriel674

> this is a CTF about Cryptography

## Desafio: Interencdec (Cryptography)
#### Intrudução
 
 Este é um desafio de [CTF](https://hackersec.com/desafios-hacker-o-que-sao-os-ctf/) (Capture The Flag), apresentado em 2024 pela plataforma [picoCTF](https://picoctf.org/). Trata-se de uma proposta introdutória voltada para ["Cryptography"](https://en.wikipedia.org/wiki/Cryptography). 
 
 O desafio trata-se de decodificar uma string em diferentes processos para encontrar a flag.

- [Página do desafio](https://play.picoctf.org/practice/challenge/418).

#### Descrição

O desafio possui um simples enunciado, contendo apenas a frase:

> Can you get the real meaning from this file.(Você consegue entender o significado real deste arquivo?)

Além diiso, há uma dica:

> Engaging in various decoding processes is of utmost importance.(O envolvimento em vários processos de decodificação é de extrema importância.)

E o seguinte arquivo codificado para download:

> YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgyeG9OakJzTURCcGZRPT0nCg==

Servindo como ponto de partida para a análise.

#### Interpretando a dica

Segundo a dica, o processo de decodificação do arquivo deve ser realizado em múltiplas fases.

#### solução

Após a análise do conteúdo codificado, foi possível identificar que se trata de uma codificação em [Base64](https://en.wikipedia.org/wiki/Base64). Utilizando a ferramenta Base64 disponível no site [DokeHost](https://dokehost.com.br/ferramenta/codificar-decodificar-base64), é possível decodificar a mensagem. Para isso, basta selecionar a opção de "descriptografar", inserir a string desejada e clicar em "decodificar".

<img width="925" height="285" alt="Captura de tela 2025-09-07 121525" src="https://github.com/user-attachments/assets/7d94232d-7bd2-424e-9dc6-59685121e88b" />

Após a primeira decodificação, nos deparamos com uma nova string também codificada. Mais uma vez, identificamos que se trata de uma codificação Base64.

<img width="921" height="193" alt="Captura de tela 2025-09-07 121541" src="https://github.com/user-attachments/assets/6fae6d40-7df2-4791-96da-d00cc5bd8b76" />

Sendo assim, basta repetir o processo de decodificação utilizado anteriormente para obter o novo conteúdo. 

O texto resultante das duas decodificações em Base64 ainda apresenta características de criptografia.

<img width="910" height="194" alt="Captura de tela 2025-09-07 122039" src="https://github.com/user-attachments/assets/8aebf6e5-1ece-4d35-8219-94544fc06646" />

Provavelmente trata-se de uma cifra de rotação. Para decifrá-la, podemos utilizar a ferramenta disponível no site [dcode.fr](https://www.dcode.fr/). Basta acessar o campo de busca “Recherche sur dCode”, digitar "ROT13" - refere-se a uma técnica simples de criptografia chamada "Rotate by 13", ou rotação de 13 posições no alfabeto, uma variação da [Cifra de César](https://pt.wikipedia.org/wiki/Cifra_de_C%C3%A9sar) - e selecionar a opção “Code César (ROT13, ROT)”.

<img width="421" height="459" alt="Captura de tela 2025-09-07 151840" src="https://github.com/user-attachments/assets/6be022ee-e566-44a2-ac27-f76a08c4e44e" />


Em seguida, inserimos o texto cifrada e aplicamos a decodificação para revelar a flag.

<img width="528" height="217" alt="Captura de tela 2025-09-07 130942" src="https://github.com/user-attachments/assets/ee113e50-0fc5-4687-8c9a-e5cf1fe16267" />

Após isso a flag é revelada.

<img width="412" height="323" alt="Captura de tela 2025-09-07 131006" src="https://github.com/user-attachments/assets/a4030b55-6e00-4fff-a6a3-0a1f6631e556" />

#### conclusão

Flag:

> picoCTF{caesar_d3cr9pt3d_ea60e00b}

Este desafio foi uma excelente aplicação dos conceitos básicos de criptografia, mostrando como múltiplas camadas de codificação podem ser utilizadas para ocultar informações. A identificação da codificação Base64 seguida da aplicação da cifra de rotação ROT13 permitiu a recuperação da flag com sucesso
