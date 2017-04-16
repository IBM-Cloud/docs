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

# Debuggen einer lokalen Anwendung
{: #local-debug}

Nachfolgend werden die Anweisungen zum Debuggen einer lokalen Anwendung für die folgenden Sprachen aufgeführt:  

* [Java](#java) 
* [Node.js](#node)

**Hinweis:** Das Debugging von Swift-Anwendungen wird derzeit nicht unterstützt. 

## Debuggen einer Java-Anwendung
{: #java}

Schritte zur Aktivierung eines Debuggings für eine Java-Anwendung: 

1. Führen Sie im Stammverzeichnis des Anwendungsprojekts den folgenden Befehl aus: 

 `bx dev debug`

2. Verbinden Sie den Debugger mit der Anwendung: 

 * [Eclipse ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm)
 * [IntelliJ ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html)
 * [VSCode ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugge)
 * JDK-Befehlszeile: `jdb -attach <host:port>`

## Debuggen einer Node.js-Anwendung
 
{: #node}

Schritte zur Aktivierung eines Debuggings für eine Node.js-Anwendung: 

1. Führen Sie im Stammverzeichnis des Anwendungsprojekts den folgenden Befehl aus: 

 `bx dev debug`

2. Verbinden Sie den Debugger mit der Anwendung: 
 * [VSCode ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://blog.docker.com/2016/07/live-debugging-docker/).
 * [WebStorm ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/)


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


