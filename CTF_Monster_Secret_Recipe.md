#  CTF Cookie Monster Secret Recipe (Web Exploitation)
###### solved by @oGabriel674

> this is a CTF about Web Exploitation

## Desafio:  Cookie Monster Secret Recipe (Web Exploitation)
#### Intrudução

Este é um desafio de [CTF](https://hackersec.com/desafios-hacker-o-que-sao-os-ctf/) (Capture The Flag), apresentado em 2025 pela plataforma [picoCTF](https://picoctf.org/). Trata-se de uma proposta introdutória voltada para ["Web Exploitation"](https://pt.wikipedia.org/wiki/Exploit_(seguran%C3%A7a_de_computadores)), onde o objetivo é explorar um site em busca da receita secreta de cookies, escondida em algum lugar.

- [Página do desafio](https://play.picoctf.org/practice/challenge/469)
  
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

A mensagem, mais uma vez, sugere que os cookies são relevantes. 

Analizando os dados no navegador, identificamos um cookie chamado "secret_recip", cujo valor está codificado.

<img width="896" height="85" alt="Captura de tela 2025-09-06 130855" src="https://github.com/user-attachments/assets/407ec2b5-5bf5-43d7-96db-273efd876506" />

Ao observar o conteúdo, nota-se que se trata de uma [codificação URL](https://en.wikipedia.org/wiki/Percent-encoding)(oficialmente conhecida como codificação percentual). 

Para realizar a decodificação, utilizei o site [URLenconder.org](https://www.urlencoder.org/pt/), que oferece ferramentas uteis e práticas para auxiliar nesse processo.

Então, inserindo a string diretamente na caixa de texto principal, realizamos a decodificação - que pode ser feita simplismente clicando em "Decodificar".

<img width="1201" height="568" alt="cópiaCaptura de tela 2025-09-06 131707" src="https://github.com/user-attachments/assets/721ea280-7372-43e0-a7f8-7a0610b6b0b6" />

Após a decodificação, é revelada outra string codificada - desta vez, no formato [Base64](https://en.wikipedia.org/wiki/Base64).

<img width="635" height="68" alt="Captura de tela 2025-09-06 131707" src="https://github.com/user-attachments/assets/4dac28b9-0042-4226-859c-43964e984eba" />

Utilizando a ferramenta Base64 do site [DokeHost](https://dokehost.com.br/ferramenta/codificar-decodificar-base64), é possível decodificar a mensagem. Pra isto, basta selecionar a opção de descriptografia, inserir a string e clicar em "decodificar".

<img width="1031" height="368" alt="Captura2 de tela 2025-09-06 132502" src="https://github.com/user-attachments/assets/de486c7a-eb5b-4ca2-9503-681b7f32b58b" />

Consseguimos, assim, encontrar a nossa flag.

<img width="810" height="231" alt="Captura de tela 2025-09-06 142016" src="https://github.com/user-attachments/assets/e59bdc68-7f9f-4c72-83de-582854731309" />

#### conclusão

Flag:

> picoCTF{c00k1e_m0nster_l0ves_c00kies_73110ED1}

Este desafio foi uma excelente aplicação dos conceitos básicos de Web Exploitation e criptografia, mostrando que a resposta pode estar sempre á vista - basta saber como procurar.
