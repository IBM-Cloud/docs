---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Liberty アプリおよび Node.js アプリの管理
{: #app_management}


アプリ管理は、開発用およびデバッグ用のユーティリティーの一式であり、{{site.data.keyword.Bluemix}} 上の Liberty および Node.js アプリケーション用に使用可能にすることができます。
{:shortdesc}

## アプリ管理ユーティリティー
{: #Utilities}

### これらのユーティリティーでは、Liberty と Node.js の両方がサポートされます
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

*proxy* では、アプリケーションと {{site.data.keyword.Bluemix_notm}} 間の最低限のアプリケーション管理が行われます。

有効にすると、ビルドパックは、アプリケーションのランタイムとコンテナーの間に配置されたプロキシー・エージェントを開始します。*proxy* ユーティリティーは、アプリケーションが受信したすべての要求を処理します。要求のタイプに基づいて、アプリ管理アクションを実行するか、要求をアプリケーションに転送します。*proxy* により、他のほとんどのアプリ管理ユーティリティーを有効化できます。*proxy* を有効にすることで、アプリケーション・コンテナーは、アプリケーションが異常終了した場合でも存続します。また、プロキシー・エージェントでは、増分ファイル更新も可能です。これにより、Node.js アプリケーションの「Live Edit」モードが使用可能になります。

#### devconsole
{: #devconsole}

(*devconsole*) 開発コンソール・ユーティリティーは、以下の URL でアクセス可能です。
```
http://<yourappname>.mybluemix.net/bluemix-debug/manage
    ```

開発コンソールを使用することで、ユーザーは、アプリケーションを再始動、停止、または一時停止できます。また、ユーザーは、shell および inspector ユーティリティーを使用可能にしたり、それらにアクセスしたりすることもできます。

Node バージョン 6.3.0 以上では、開発コンソールで、アプリケーションの再始動ボタンが用意されており、また shell ユーティリティーにアクセスできます。詳しくは、*inspector* の説明を参照してください。

devconsole ユーティリティーは *proxy* も開始します。

#### hc
{: #hc}

(*hc*) ヘルス・センター・エージェントにより、アプリケーションをヘルス・センター・クライアントでモニターできます。

ヘルス・センターでは、IBM Monitoring and Diagnostic Tools を使用した Liberty アプリケーションおよび Node.js アプリケーションのパフォーマンスの分析がサポートされます。詳しくは、『[How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}』を参照してください。</p></li>

#### shell
{: #shell}

*shell* ユーティリティーは、Web ベースのシェルを使用可能にします。これには、*devconsole* ユーティリティーから、または以下の URL によりアクセスできます。

```
http://<yourappname>.mybluemix.net/bluemix-debug/shell
    ```

*shell* ユーティリティーにアクセスすると、アプリケーションにシェルでアクセスできる端末ウィンドウが表示されます。ファイルの編集、メモリー使用量の確認、診断コマンドの実行など、通常のシェルでサポートされる任意の操作を実行できます。

*shell* ユーティリティーは *proxy* も開始します。

### 以下のユーティリティーでは、Liberty のみがサポートされます
{: #liberty_utilities}

#### debug
{: #debug}

*debug* ユーティリティーは、Liberty アプリケーションをデバッグ・モードにし、IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} などのクライアントがアプリケーションとのリモート・デバッグ・セッションを確立できるようにします。

詳しくは、『[リモート・デバッグ](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug)』を参照してください。

*debug* ユーティリティーは *proxy* も開始します。

#### jmx
{: #jmx}

*jmx*: ユーティリティーは、JMX REST Connector を使用可能にして、リモート JMX クライアントが {{site.data.keyword.Bluemix_notm}} ユーザー資格情報を使用してアプリケーションを管理できるようにします。

JMX コネクターの構成について詳しくは、『[Configuring secure JMX connection to the Liberty profile](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}』を参照してください。

*jmx* ユーティリティーは proxy を開始しません。

### 以下のユーティリティーでは、Node.js のみがサポートされます
{: #node_utilities}

#### inspector
{: #inspector}

Node.js の 6.3.0 より前のバージョンで、*inspector* は、*devconsole* ユーティリティーまたは *https://myApp.mybluemix.net/bluemix-debug/inspector* からアクセス可能なノード・インスペクター・デバッガー・インターフェースを使用可能にします。

*インスペクター*・プロセスは、アプリケーション・コンテナーで実行されます。このユーティリティーを使用することで、CPU 使用プロファイルの作成、ブレークポイントの追加、コードのデバッグを行うことができます。それも、{{site.data.keyword.Bluemix_notm}} でのアプリケーションの実行中に行うことができます。ノード・インスペクター・モジュールについて詳しくは、[GitHub の node-inspector](https://github.com/node-inspector/node-inspector){:new_window} を参照してください。

*inspector* ユーティリティーは *proxy* も開始します。

Node.js バージョン 6.3.0 以上で、*inspector* は [V8 Inspector Integration for Node.js](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window} を使用します。Chrome DevTools をアプリに接続するために使用できる URL は、アプリのログにあります。ログ・メッセージは、以下のようなものになります。

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node-hc --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

このシナリオで、*devconsole* に *inspector* へのリンクは**表示されません**。これは、URL が存在しないためです。

このシナリオで、*proxy* は *inspector* にトラフィックをルーティングしません。Chrome DevTools の URL が機能するためには、アプリへの SSH トンネルを作成する必要があります。SSH トンネルを作成するには、以下と同じような方法で「cf ssh」コマンドを使用してください。

```
  cf ssh -N -T -L <port>:127.0.0.1:<hostport> <appName>
```

このコマンドで、*hostport* は、「Debugger listening on port xxxx」というログ・メッセージに含まれるポート値にしてください。また、*port* は、「cf ssh」コマンドの発行元のシステムで使用可能な任意のポートです。

#### trace
{: #trace}

*trace* ユーティリティーは、アプリケーションが *log4js*、*ibmbluemix*、または *bunyan* ロギング・モジュールを使用している場合のトレース・レベルを動的に設定できるようにします。

**注:** サポートされる依存関係バージョン:
* log4js: (0.6.0 から 0.6.24)
* bunyan: (1.0.0、1.0.1、1.1.0 から 1.1.3、1.2.0 から 1.2.3、1.3.0 から 1.3.5)
* ibmbluemix: (1.0.0-20140707-1250) から (1.0.0-20150409-1328)

{{site.data.keyword.Bluemix_notm}} Web コンソールで「インスタンスの詳細」ページに移動し、**「アクション」**を選択して UI を表示します。

*trace* ユーティリティーは、アプリケーションが "-b buildpack" オプションを使用して開始された場合は使用できません。

*trace* ユーティリティーは *proxy* を開始しません。

##  アプリ管理の構成方法
{: #configure}

アプリ管理ユーティリティーを使用可能にするには、*BLUEMIX_APP_MGMT_ENABLE* 環境変数を設定し、アプリケーションを再ステージングします。「+」で区切ることで、複数のユーティリティーを使用可能にすることができます。

例えば、*devconsole* ユーティリティーと *shell* ユーティリティーを使用可能にするには、以下のコマンドを実行します。

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

環境変数を設定したら、その後アプリケーションを再ステージングしてください。

```
cf restage myApp
```

アプリケーションに併せてアプリ管理ユーティリティーもインストールされることのないようにする場合は、*BLUEMIX_APP_MGMT_INSTALL* 環境変数を「false」に設定して、アプリケーションを再ステージングします。

例えば次のようにします。

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

## 制限
{: #restrictions}

* アプリ管理では、単一インスタンス・アプリケーションのみがサポートされます。
* アプリ管理を使用してアプリケーションに対して行った変更は一時的なものであり、このモードを終了すると失われます。このモードは一時的な開発での使用に限られ、パフォーマンスのために実稼働環境としての使用は意図されていません。
* manifest.yml ファイル (command) または CF CLI (-c) で開始コマンドを設定した場合、ほとんどのアプリ管理ユーティリティーは機能しません。
これらのメソッドはビルドパックのオーバーライドであり、Node.js アプリ
ケーションを開始するためのアンチパターンです。結果を最適化するには、package.json ファイルまたは Procfile で開始コマンドを設定します。

## Eclipse Tools の開発モード
{: #devmode}

開発モードは、アプリケーションがクラウドで実行されているときに開発者がアプリケーションを操作できるようにする、[Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) のフィーチャーです。

{{site.data.keyword.Bluemix_notm}} でアプリケーションを操作している間、開発者は、ローカル環境で実行しているような通常の開発アクティビティーを実行できないと感じる可能性があります。この問題に対処するため、Eclipse Tools を使用した開発モードでは、セキュアな一時ワークスペース内にいながら、クラウドで作業する手段を提供します。

開発モードは Liberty アプリケーションおよび Node.js アプリケーションの両方でサポートされています。開発モードを Liberty または Node.js アプリケーション用に使用可能にすると、アプリケーションをプッシュすることなく、アプリケーション・ファイルを増分的に更新できます。また、アプリケーションとのデバッグ・セッションを確立することもできます。Liberty アプリケーションの開発モードは、debug および jmx アプリ管理ユーティリティーを使用可能にした場合と同等です。Node.js アプリケーションの場合、*devconsole*、*inspector*、および *shell* ユーティリティーを使用可能にした場合と同等です。
