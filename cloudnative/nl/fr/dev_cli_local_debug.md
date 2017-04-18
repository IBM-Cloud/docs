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

# Débogage d'une application locale
{: #local-debug}

Les instructions de débogage d'une application locale sont fournies ci-après pour les langages suivants : 

* [Java](#java) 
* [Node.js](#node)

**Remarque** : le débogage des applications Swift n'est pas actuellement pris en charge.

## Débogage d'une application Java
{: #java}

Procédez comme suit pour activer le débogage pour une application Java :

1. Depuis le répertoire racine de votre projet d'application, exécutez la commande suivante :

 `bx dev debug
`

2. Connectez le débogueur à votre application :

 * [Eclipse ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm)
 * [IntelliJ ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html)
 * [VSCode ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugge)
 * Ligne de commande JDK : `jdb -attach <hôte:port>`

## Débogage d'une application Node.js
 
{: #node}

Procédez comme suit pour activer le débogage pour une application Node.js :

1. Depuis le répertoire racine de votre projet d'application, exécutez la commande suivante :

 `bx dev debug
`

2. Connectez le débogueur à votre application :
 * [VSCode ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://blog.docker.com/2016/07/live-debugging-docker/).
 * [WebStorm ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/)


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


