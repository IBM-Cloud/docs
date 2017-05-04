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

# 本地应用程序调试
{: #local-debug}

提供了下列语言的本地应用程序调试指示信息：

* [Java](#java)
* [Node.js](#node)

**注**：不支持 Swift 应用程序调试。

## Java 应用程序调试
{: #java}

启用 Java 应用程序调试的步骤：

1. 从应用程序项目的根目录运行以下命令：

	`bx dev debug`

2. 将调试器连接到应用程序：

	* Eclipse
      1. 将“现有 Maven 项目”项目导入到 Eclipse。
      2. 创建 [Java 远程应用程序 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm) 调试配置。
      		1. 输入 IP 地址或 `localhost:<port>`  
      		2. 输入 `7777` 作为端口号。
      		3. 指定所导入 Java 项目的名称。
      6. 在 IDE 中设置断点。
      7. 运行调试配置。
      8. 使用浏览器访问端点，以重现问题。  
	   **注**：Java 基本微服务端点的缺省端口是 9080。
	* [IntelliJ ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html)
	* [VSCode ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugge)
	* JDK 命令行：`jdb -attach <host:port>`

## Node.js 应用程序调试

{: #node}

启用 Node.js 应用程序调试的步骤：

1. 从应用程序项目的根目录运行以下命令：

	`bx dev debug`

2. 将调试器连接到应用程序：
	* [VSCode ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://blog.docker.com/2016/07/live-debugging-docker/)
	* [WebStorm ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/)


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
