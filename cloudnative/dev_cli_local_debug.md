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

# Local application debugging
{: #local-debug}

Local application debugging instructions are provided for the following languages:

* [Java](#java)
* [Node.js](#node)

**Note**: Swift application debugging is not supported.

## Java application debugging
{: #java}

Steps to enable debug for a Java application:

1. From your application project's root directory run the following command:

	`bx dev debug`

2. Connecting the debugger to your application:

	* Eclipse
      1. Import the “Existing maven project” project into Eclipse.
      2. Create a [Java remote application ![External link icon](../icons/launch-glyph.svg "External link icon")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm)” debug configuration.
      		1. Enter the IP address or `localhost:<port>`  
      		2. Enter `7777` for port number.
      		3. Specify the name of the java project that you imported.
      6. Set a breakpoint in the IDE.
      7. Run the debug configuration.
      8. Access the endpoint with a browser to recreate the issue.  
	   **Note**: The default port is 9080 for the Java basic Microservices endpoint.
	* [IntelliJ ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html)
	* [VSCode ![External link icon](../icons/launch-glyph.svg "External link icon")](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugge)
	* JDK command line: `jdb -attach <host:port>`

## Node.js application debugging

{: #node}

Steps to enable debug for a Node.js application:

1. From your application project's root directory run the following command:

	`bx dev debug`

2. Connecting the debugger to your application:
	* [VSCode ![External link icon](../icons/launch-glyph.svg "External link icon")](https://blog.docker.com/2016/07/live-debugging-docker/)
	* [WebStorm ![External link icon](../icons/launch-glyph.svg "External link icon")](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/)


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
