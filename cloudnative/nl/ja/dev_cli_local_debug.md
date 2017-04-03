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

# ローカル・アプリケーション・デバッグ
{: #local-debug}

次の言語について、ローカル・アプリケーション・デバッグ手順が下に示されています。 

* [Java](#java) 
* [Node.js](#node)

**注**: Swift アプリケーションのデバッグは現在サポートされていません。

## Java アプリケーションのデバッグ
{: #java}

Java アプリケーションのデバッグを有効にするステップ

1. アプリケーション・プロジェクトのルート・ディレクトリーから、以下のコマンドを実行します。

 `bx dev debug`

2. デバッガーをアプリケーションに接続します。

 * [Eclipse ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm)
 * [IntelliJ ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.jetbrains.com/help/idea/2016.3/run-debug-configuration-remote.html)
 * [VSCode ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://marketplace.visualstudio.com/items?itemName=donjayamanne.javadebugge)
 * JDK コマンド・ライン: `jdb -attach <host:port>`

## Node.js アプリケーションのデバッグ
 
{: #node}

Node.js アプリケーションのデバッグを有効にするステップ

1. アプリケーション・プロジェクトのルート・ディレクトリーから、以下のコマンドを実行します。

 `bx dev debug`

2. デバッガーをアプリケーションに接続します。
 * [VSCode ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://blog.docker.com/2016/07/live-debugging-docker/)
 * [WebStorm ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://blog.alexseifert.com/2016/10/25/debugging-node-js-in-a-docker-container-with-webstorm/)


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


