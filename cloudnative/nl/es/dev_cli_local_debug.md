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

# Depuración de aplicaciones locales
{: #local-debug}

Las instrucciones para la depuración de aplicaciones locales se proporcionan a continuación para los siguientes lenguajes: 

* [Java](#java) 
* [Node.js](#node)

**Nota**: actualmente no se soporta la depuración de aplicaciones Swift.

## Depuración de aplicaciones Java
{: #java}

Pasos para habilitar la depuración para una aplicación Java:

1. Desde el directorio raíz del proyecto de aplicación ejecute el siguiente mandato:

 `bx dev debug`

2. Conexión del depurador a su aplicación:

 * [Eclipse ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm)
 * [IntelliJ ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html)
 * [VSCode ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugge)
 * Línea de mandatos JDK: `jdb -attach <host:port>`

## Depuración de aplicaciones Node.js 
 
{: #node}

Pasos para habilitar la depuración para una aplicación Node.js:

1. Desde el directorio raíz del proyecto de aplicación ejecute el siguiente mandato:

 `bx dev debug`

2. Conexión del depurador a su aplicación:
 * [VSCode ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://blog.docker.com/2016/07/live-debugging-docker/).
 * [WebStorm ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/)


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


