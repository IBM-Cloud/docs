---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Debug dell'applicazione locale 
{: #local-debug}

Le istruzioni per il debug dell'applicazione locale sono fornite di seguito per i seguenti linguaggi: 

* [Java](#java) 
* [Node.js](#node)

**Nota**: il debug dell'applicazione Swift al momento non è supportato.

## Debug dell'applicazione Java
{: #java}

Passi per abilitare il debug per un'applicazione Java: 

1. Dalla tua directry root del progetto dell'applicazione esegui il seguente comando:

 `bx dev debug`

2. Collegamento del programma di debug alla tua applicazione:

 * [Eclipse ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm)
 * [IntelliJ ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html)
 * [VSCode ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugge)
 * Riga di comando JDK: `jdb -attach <host:port>`

## Debug dell'applicazione Node.js
 
{: #node}

Passi per abilitare il debug per un'applicazione Node.js: 

1. Dalla tua directry root del progetto dell'applicazione esegui il seguente comando:

 `bx dev debug`

2. Collegamento del programma di debug alla tua applicazione:
 * [VSCode ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://blog.docker.com/2016/07/live-debugging-docker/).
 * [WebStorm ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/)


<!-- 
## Swift application debugging - content from mike tunnicliffe
{: #swift}

Steps to enable debug for a Swift application:  

1. On the App server (or system where the Swift application will execute), you should start the 'lldb server':
 - `lldb-server platform --><!--listen <port number>`
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
 - `(lldb) process attach --><!--pid 3626`
--> 


