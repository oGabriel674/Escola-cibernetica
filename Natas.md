# CTF - Natas (OverTheWire)
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

Ao observar com um pouco mais de atenção o link identificado, notamos que ele contém um caminho adicional na [URL](https://tecnoblog.net/responde/o-que-e-url/) , especificamente um diretório denominado /files/ antes do arquivo pixel.png, podendo indicar a existência de outros recursos acessíveis nesse mesmo diretório.

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
