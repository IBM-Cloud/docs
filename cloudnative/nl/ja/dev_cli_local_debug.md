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

# ローカル・アプリケーション・デバッグ
{: #local-debug}

次の言語について、ローカル・アプリケーション・デバッグ手順が示されています。

* [Java](#java)
* [Node.js](#node)

**注**: Swift アプリケーションのデバッグはサポートされていません。

## Java アプリケーションのデバッグ
{: #java}

Java アプリケーションのデバッグを有効にするステップ

1. アプリケーション・プロジェクトのルート・ディレクトリーから、以下のコマンドを実行します。

	`bx dev debug`

2. デバッガーをアプリケーションに接続します。

	* Eclipse
      1. 「Existing maven project」プロジェクトを Eclipse にインポートします。
      2. [Java リモート・アプリケーション ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Ftasks%2Ftask-remotejava_launch_config.htm) のデバッグ構成を作成します。
      		1. IP アドレスまたは `localhost:<port>` を入力します。  
      		2. ポート番号として `7777` を入力します。
      		3. インポートした java プロジェクトの名前を指定します。
      6. IDE にブレークポイントを設定します。
      7. デバッグ構成を実行します。
      8. ブラウザーでエンドポイントにアクセスして、問題を再現します。  
	   **注**: Java の基本的なマイクロサービス・エンドポイントのデフォルト・ポートは 9080 です。
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
