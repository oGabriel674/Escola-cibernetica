#  CTF RED (Forensics)
###### solved by @oGabriel674

> this is a CTF about Forensics

## Desafio: RED (Forensics)
#### Intrudução

Este é um desafio de [CTF](https://hackersec.com/desafios-hacker-o-que-sao-os-ctf/) (Capture The Flag), apresentado em 2025 pela plataforma [picoCTF](https://picoctf.org/). Trata-se de uma proposta introdutória voltada para categoria de ["Forensics"](https://trailofbits.github.io/ctf/forensics/), com o objetivo de investigar um arquivo suspeito.

- [Página do desafio](https://play.picoctf.org/practice/challenge/460)
  
#### Análise Inicial

O desafio apresenta um enunciado simples, contendo apenas a repetição da palavra "red" diversas vezes. 

Print do enunciado:

<img width="324" height="78" alt="Captura de tela 2025-09-07 150419" src="https://github.com/user-attachments/assets/aa51b513-b44a-4f7b-91ed-d15b2be956df" />

Além disso, possui três dicas:

> - The picture seems pure, but is it though?(A imagem parece pura, mas será mesmo?)
>
> - Red?Ged?Bed?Aed?(Vermelho?Ged?Cama?Aed?)
>
> - Check whatever Facebook is called now.(Confira o nome atual do Facebook.)

E uma imagem no formato PNG disponibilizada para download, que será utilizada como base para nossas análises.

#### solução

O arquivo PNG apresenta exclusivamente um quadrado vermelho, sem elementos adicionais que possibilitam uma análise detalhada.

<img width="232" height="226" alt="Captura de tela 2025-09-07 222603" src="https://github.com/user-attachments/assets/f0c00be6-c90c-4bf0-a282-4706c598921a" />

Ao tentarmos extrair uma sequência de texto do arquivo, encontramos um pequeno poema que, ao observarmos as letras iniciais de cada linha, revela a mensagem oculta 'CHECK [LSB](https://en.wikipedia.org/wiki/Bit_numbering#:~:text=Bit%20menos%20significativo%20na%20esteganografia%20digital)', sugerindo a presença de dados escondidos nos bits menos significativos.

<img width="611" height="393" alt="Screenshot_2025-09-07_21_05_55" src="https://github.com/user-attachments/assets/95b08e12-1fbc-4d09-bb4f-ec4749d69ebb" />

Para dar continuidade para o desafio, foi utilizado o site [CyberChef](https://gchq.github.io/CyberChef/), que oferece uma variedade de ferramentas práticas e eficientes para análise de dados.

No site, basta selecionar a opção "Extract LSB", acessível ao pesquisar por "Extract" na barra de pesquisa. Essa funcionalidade permite extrair os bits menos significativos (LSB) de uma imagem ou arquivo.

<img width="367" height="465" alt="Captura de tela 2025-09-07 221144" src="https://github.com/user-attachments/assets/bf8812a4-5baa-4ed4-9615-f53ab75404e2" />

No canto superior esquerdo da interface do CyberChef, selecionamos a opção "Open file as input", que permite carregar o arquivo a ser analisado. Com o arquivo devidamente inserido, é possível aplicar a operação "Extract LSB" para extrair os bits menos significativos.

Nos campos de texto identificados como "Colour Pattern" (1, 2, 3 e 4), inserimos as letras [RGBA](https://www.w3schools.com/css/css_colors_rgb.asp#:~:text=AN%C3%9ANCIO-,Valor%20RGBA,-Os%20valores%20de), que representam os canais de cor Red, Green, Blue e Alpha. Essa configuração é comumente utilizada em imagens no formato PNG, permitindo a extração da intensidade de cada componente de cor, incluindo a transparência (Alpha), essencial para a análise detalhada dos dados ocultos.

<img width="570" height="258" alt="Captura de tela 2025-09-07 221829" src="https://github.com/user-attachments/assets/43be161e-0692-4134-9b63-52a1152c3c21" />

A aplicação da extração dos bits menos significativos resulta em uma sequência de texto codificada, que se repete diversas vezes ao longo da saída, sugerindo um padrão ou estrutura oculta.

<img width="939" height="317" alt="Captura de tela 2025-09-07 221900" src="https://github.com/user-attachments/assets/e3664138-209f-48d4-be79-e2b2ffc45c89" />

Ao analisar o segmento, é possível identificar que se trata de uma codificação em [Base64](https://en.wikipedia.org/wiki/B). Utilizando a ferramenta do CyberChef, aplicamos a função de decodificação correspondente — acessível ao buscar por “From Base64” na barra de pesquisa — para converter o conteúdo codificado em texto legível.

Apõs aplicar a função, o conteúdo codificado foi convertido com sucesso, revelando a flag oculta no texto decodificado.

#### conclusão

Flag:

> picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}

Este desafio foi uma excelente aplicação dos conceitos básicos de análise forense, evidenciando como uma imagem aparentemente comum pode ocultar informações.
