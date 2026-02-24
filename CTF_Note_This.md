# CTF Note This (SSTI)
###### solved by @oGabriel674

> this is a CTF about SSTI (Server-Side Template Injection)

## Desafio: Note This (SSTI)

#### Solução

O desafio tem início na tela de login, onde devemos inserir credenciais para acessar o sistema.

<img width="502" height="285" alt="Captura de tela 2026-02-22 221343" src="https://github.com/user-attachments/assets/c05dae2d-4fd2-4cfd-9c99-b2eeeea02686" />

Na fase de reconhecimento, utilizado um teste simples para verificar o comportamento do sistema frente a entradas dinâmicas. Ao inserir a expressão __``{{7*7}}``__ no campo de entrada, o servidor retornou o resultado da operação matemática, que foi __49__.
Esse comportamento evidenciou a presença de uma vulnerabilidade do tipo [SSTI (Server-Side Template Injection)](https://www.imperva.com/learn/application-security/server-side-template-injection-ssti/).

<img width="498" height="314" alt="Captura de tela 2026-02-22 221416" src="https://github.com/user-attachments/assets/fa1945e3-9bfd-483f-95ed-e12803cfd888" />

Após confirmar a vulnerabilidade de __SSTI (Server-Side Template Injection)__ por meio do teste com ``{{7*7}}``, foi possível observar que o motor de template em uso se trata do [Jinja2](https://www.treinaweb.com.br/blog/o-que-e-o-jinja2), Ja que a sintaxe __``{{ }}__`` é característica  desse template.

