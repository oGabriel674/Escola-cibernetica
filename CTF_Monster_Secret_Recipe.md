#  CTF Cookie Monster Secret Recipe (Web Exploitation)
###### solved by @oGabriel674

> this is a CTF about Web Exploitation

## Desafio:  Cookie Monster Secret Recipe (Web Exploitation)
#### Intrudução

Este é um desafio de CTF (Capture The Flag), apresentado em 2025 pela plataforma [picoCTF](https://picoctf.org/). Trata-se de uma proposta introdutório voltada para ["Web Exploitation"](https://pt.wikipedia.org/wiki/Exploit_(seguran%C3%A7a_de_computadores)), onde o objetivo é explorar um site em busca da receita secreta de cookies, escondida em algum lugar.

#### Análise Inicial

O desafio possui a seguinte descrição:

> Cookie Monster has hidden his top-secret cookie recipe somewhere on his website. As an aspiring cookie detective, your mission is to uncover this delectable secret. Can you outsmart Cookie Monster and find the hidden recipe?
>(O Monstro dos Come-Come escondeu sua receita secreta de biscoitos em algum lugar do seu site. Como um aspirante a detetive de biscoitos, sua missão é desvendar esse segredo delicioso. Você consegue enganar o Monstro dos Come-Come e encontrar a receita escondida?)

Além disso, há três dicas:

>- Sometimes, the most important information is hidden in plain sight. Have you checked all parts of the webpage?(Às vezes, as informações mais importantes estão escondidas à vista de todos. Você verificou todas as partes da página?)
>- Cookies aren't just for eating - they're also used in web technologies!(Os cookies não servem apenas para comer: eles também são usados ​​em tecnologias da web!)
>- Web browsers often have tools that can help you inspect various aspects of a webpage, including things you can't see directly.(Web browsers often have tools that can help you inspect various aspects of a webpage, including things you can't see directly.)

#### Interpretando as dicas

As dicas fornecidas indicam que a flag esta visível, porém codificada, e que devemos inspecionar os [cookies HTTP](https://developer.mozilla.org/pt-BR/docs/Web/HTTP/Guides/Cookies) armazenados no site pelo navegador.

#### solução 

Assim que acessamos o link do desafio, somos redirecionados para a seguinte página de login:

<img width="864" height="391" alt="Captura de tela 2025-09-05 222812" src="https://github.com/user-attachments/assets/b81da2a2-0080-4e11-a8a5-9dff79231f16" />

Ao tentar realizar o login, nos deparamos com a seguinte mensagem de erro:

<img width="578" height="203" alt="Captura de tela 2025-09-06 001214" src="https://github.com/user-attachments/assets/85781301-970e-463b-b6f6-cb4e067d7acb" />

A mensagem, mais uma vez, sugere que os cookies são relevantes. Ao analizar os dados no navegador, identificamos um cookie chamado "secret_recip", cujo valor está codificado.

> cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzXzczMTEwRUQxfQ%3D%3D


