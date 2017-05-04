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

# Depuración de aplicaciones locales
{: #local-debug}

Se proporcionan instrucciones para la depuración de aplicaciones locales para los siguientes lenguajes:

* [Java](#java)
* [Node.js](#node)

**Nota**: no se admite la depuración de aplicaciones Swift.

## Depuración de aplicaciones Java
{: #java}

Pasos para habilitar la depuración para una aplicación Java:

1. Desde el directorio raíz del proyecto de aplicación ejecute el siguiente mandato:

	`bx dev debug`

2. Conexión del depurador a su aplicación:

	* Eclipse
      1. Importe el proyecto “Proyecto maven existente” en Eclipse.
      2. Cree una configuración de depuración de [aplicación remota Java ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm)”. 
      		1. Escriba la dirección IP o `localhost:<port>`  
      		2. Escriba `7777` para el número de puerto. 
      		3. Especifique el nombre del proyecto java que ha importado.
      6. Defina un punto de interrupción en el IDE.
      7. Ejecute la configuración de depuración. 
      8. Acceda al punto final con un navegador para reproducir el problema.   
	   **Nota**: el puerto predeterminado es 9080 para el punto final de Java Basic Microservices.
	* [IntelliJ ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html)
	* [VSCode ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugge)
	* Línea de mandatos JDK: `jdb -attach <host:port>`

## Depuración de aplicaciones Node.js

{: #node}

Pasos para habilitar la depuración para una aplicación Node.js:

1. Desde el directorio raíz del proyecto de aplicación ejecute el siguiente mandato:

	`bx dev debug`

2. Conexión del depurador a su aplicación:
	* [VSCode ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://blog.docker.com/2016/07/live-debugging-docker/)
	* [WebStorm ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/)


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
