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
