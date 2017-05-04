---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Depuração do aplicativo local
{: #local-debug}

As instruções de depuração de aplicativo local são fornecidas para os idiomas a seguir:

* [Java](#java)
* [Node.js](#node)

**Nota**: a depuração do aplicativo Swift não é suportada.

## Depuração do aplicativo Java
{: #java}

Etapas para ativar a depuração de um aplicativo Java:

1. No diretório raiz do projeto do aplicativo, execute o comando a seguir:

	`bx dev debug`

2. Conectando o depurador a seu aplicativo:

	* Eclipse
      1. Importe o projeto “Projeto maven existente” no Eclipse.
      2. Crie uma configuração de depuração de [Aplicativo remoto Java![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm)”.
      		1. Insira o endereço IP ou `localhost:<port>`  
      		2. Insira `7777` para o número da porta.
      		3. Especifique o nome do projeto Java que você importou.
      6. Configure um ponto de interrupção no IDE.
      7. Execute a configuração de depuração.
      8. Acesse o terminal com um navegador para recriar o problema.  
	   **Nota**: a porta padrão é 9080 para o terminal Java basic Microservices.
	* [IntelliJ ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html)
	* [VSCode ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugge)
	* Linha de comandos JDK: `jdb -attach <host:port>`

## Depuração do aplicativo Node.js

{: #node}

Etapas para ativar a depuração de um aplicativo Node.js:

1. No diretório raiz do projeto do aplicativo, execute o comando a seguir:

	`bx dev debug`

2. Conectando o depurador a seu aplicativo:
	* [VSCode ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://blog.docker.com/2016/07/live-debugging-docker/)
	* [WebStorm ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/)


<!--
## Swift application debugging - content from mike tunnicliffe
{: #swift}

Steps to enable debug for a Swift application:  

1. On the App server (or system where the Swift application will execute), you should start the 'lldb server':
 - `lldb-server platform -->
<!-- listen <port number>`
2. On the App server, build the Kitura-based server application using the debug configuration:
 - `swift build debug`
3. On the App server, start the Kitura-based server application:
 - `./build/debug/Kitura-Starter`
4. On the client system (also known as the host system), start the 'lldb client':
 - `lldb`
5. Configure lldb client to connect to lldb-server:
 - `(lldb) platform select remote-linux`
 - `(lldb) platform connect connect://<ip address server>:<port number server>`
6. Execute commands to debug remote program:
 - `(lldb) process attach -->
<!--pid 3626`
-->
