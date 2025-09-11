# CTF Flag Hunter (Reverse Engineering)
###### solved by @oGabriel674

> this is a CTF about Reverse Engineering

## Desafio: Flag Hunter (Reverse Engineering)
#### Intrudução
 
 Este é um desafio de [CTF](https://hackersec.com/desafios-hacker-o-que-sao-os-ctf/) (Capture The Flag), apresentado em 2025 pela plataforma [picoCTF](https://picoctf.org/). Trata-se de uma proposta introdutória voltada para ["Reverse Engineering"](https://en.wikipedia.org/wiki/Reverse_engineering). 
 
O desafio é analisar um binário que contém uma função de verificação de flag, compreender sua lógica interna e, a partir disso, descobrir a flag.

- [Página do desafio](https://play.picoctf.org/practice/challenge/472).

#### Descrição

O desafio possui o seguinte enunciado:

> Lyrics jump from verses to the refrain kind of like a subroutine call. There's a hidden refrain this program doesn't print by default. Can you get it to print it? There might be something in it for you.
> (As letras saltam dos versos para o refrão, como uma chamada de subrotina. Há um refrão oculto que este programa não imprime por padrão. Você consegue fazer com que ele o imprima? Pode haver algo nele para você.)

Além disso, possui três dicas:

> - This program can easily get into undefined states. Don't be shy about Ctrl-C.(Este programa pode facilmente entrar em estados indefinidos. Não tenha vergonha de usar Ctrl-C.)
> - Unsanitized user input is always good, right?(A entrada de dados do usuário não higienizada é sempre boa, certo?)
> - Is there any syntax that is ripe for subversion?(Existe alguma sintaxe que seja propícia à subversão?)

#### Solução

Utilizarei o terminal do [Kali Linux](https://en.wikipedia.org/wiki/Kali_Linux) para resolver este desafio.

O desafio solicita que estabeleçamos uma conexão com o serviço remoto utilizando o comando [NetCat](https://en.wikipedia.org/wiki/Netcat) ($ nc verbal-sleep.picoctf.net 53369). Além disso, o código-fonte do programa é disponibilizado para download, permitindo uma melhor análise de sua lógica. 

Ao executarmos o comando, somos conectados a um programa que aparentemente nos apresenta o início de um poema, seguindo por um campo de entrada onde podemos digitar.

<img width="640" height="251" alt="Screenshot_2025-09-06_14_14_49" src="https://github.com/user-attachments/assets/e2fc45e3-f430-4be2-b2ce-c4374d1ac694" />

Ao tentarmos digitar algo, o programa apenas retorna mais algumas linhas de texto que completam o poema, No entanto, ao analisarmos mais profundamente, é possível notar que uma parte do texto se repete, juntamente com o que foi digitado e o prefixo  "Crowd:".

<img width="604" height="308" alt="Screenshot_2025-09-06_17_10_14" src="https://github.com/user-attachments/assets/d23fc76b-8a35-4ee8-8445-d157b71a11d3" />

Após essa etapa, o programa encerra a exibição e perminte digitar novamente em seu campo de entrada.

Analizando o código-fonte, é possivel identificar rapidamente onde a flag está inserida. Logo no início do script podemos notar que a flag está armazenada em um arquivo de texto, que só será executado quando a introdução secreta é impressa.

<img width="402" height="236" alt="Captura de tela 2025-09-06 192217" src="https://github.com/user-attachments/assets/04185084-aff6-412a-ae1c-eeca360fb6e6" />

Na estrutura principal do script, observamos que a excução se inicia com um loop [while](https://linguagemc.com.br/o-comando-while-em-c/), que permanece ativo até que o poema termine ou número máximo de linhas seja atingido. Dentro desse loop, há um [for](https://linguagemc.com.br/a-estrutura-de-repeticao-for-em-c/) que percorre cada linha da letra e a divide por ponto e vírgula(":"), caso existem múltiplos comandos na mesma linha. A lógica central do script consiste em verificar o conteúdo de cada linha por meio de instruções [if](https://www.inf.pucrs.br/flash/cbp/selecao_if.html). Dependendo do comando encontrado, o programa decide qual trecho da letra será exibido a seguir. A última condição - e talvez a mais reveladora - verifica se a linha começa com o comando "RETURN" seguido de um número, Esse número representa o índice da linha para onde o script deve retornar. Ao analisar esse comportamento, percebemos que o retorno pode levar diretamente ao início da execução, onde está localizada a introdução secreta que contém a flag. Portanto, a escolha lógica do número a ser usado após o comando "RETURN" é aquela que aponta para o índice da linha onde essa introdução está presente (linha 0). 


<img width="624" height="882" alt="Captura de tela 2025-09-06 165736" src="https://github.com/user-attachments/assets/f80dc713-420e-43be-9185-b459a6a7b833" />


Ao inserir um ponto e vírgula antes do comando "RETURN", conseguimos dividir a entrada em duas partes. Isso permite ignorar o prefixo "Crowd: " que é automaticamente adicionado, e executar diretamente o comando "RETURN". Com isso, redirecionamos o fluxo do script e revelamos a flag sem seguir o caminho padrão.

<img width="640" height="370" alt="Screenshot_2025-09-06_15_29_15" src="https://github.com/user-attachments/assets/37c2abe1-6ce4-475f-8ffb-17d7e8742d40" />

#### conclusão 

Flag:

> picoCTF{70637h3r_f0r3v3r_0ed60683}

Este desafio foi uma excelente aplicação dos conceitos básicos de Reverse Engineering, mostrando como como pequenas alterações na entrada - como o uso de ponto e vírgula - podem alterar completamente o fluxo de execução.
