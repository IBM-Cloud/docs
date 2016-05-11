---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Liberty アプリおよび Node.js アプリの管理
{: #app_management}

*最終更新日: 2016 年 3 月 17 日*

アプリ管理は、開発用およびデバッグ用のユーティリティーの一式であり、{{site.data.keyword.Bluemix}} 上の Liberty および Node.js アプリケーション用に使用可能にすることができます。
{:shortdesc}

##アプリ管理ユーティリティー
{: #Utilities}

これらのユーティリティーでは、Liberty と Node.js の両方がサポートされます。

  1. *proxy*: アプリケーションと {{site.data.keyword.Bluemix_notm}} 間のプロキシーとして機能する最小アプリケーション管理。

    有効にすると、ビルドパックは、アプリケーションのランタイムとコンテナーの間に配置されたプロキシー・エージェントを開始します。*proxy* ユーティリティーは、アプリケーションが受信したすべての要求を処理します。要求のタイプに基づいて、アプリ管理アクションを実行するか、要求をアプリケーションに転送します。*proxy* により、他のほとんどのアプリ管理ユーティリティーを有効化できます。*proxy* を有効にすることで、アプリケーション・コンテナーは、アプリケーションが異常終了した場合でも存続します。また、プロキシー・エージェントでは、増分ファイル更新も可能です。これにより、Node.js アプリケーションの「Live Edit」モードが使用可能になります。
	
  2. *devconsole*: 以下の URL からアクセス可能な開発コンソール・ユーティリティーを使用可能にします。
    ```
    http://<yourappname>.mybluemix.net/bluemix-debug/manage
    ```
	
    開発コンソールを使用することで、ユーザーは、アプリケーションを再始動、停止、または一時停止できます。また、ユーザーは、shell および inspector ユーティリティーを使用可能にしたり、それらにアクセスしたりすることもできます。

    devconsole ユーティリティーは *proxy* も開始します。
	
  3. *hc*: アプリケーションをヘルス・センター・ク
ライアントによってモニターできるようにするヘルス・センター・エージェ
ント。

    ヘルス・センターでは、IBM Monitoring and Diagnostic Tools を使用した Liberty アプリケーションおよび Node.js アプリケーションのパフォーマンスの分析がサポートされます。詳しくは、『[How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}』を参照してください。</p></li>
	
  4. *shell*: devconsole ユーティリティーから、または以下の URL にアクセスすることでアクセス可能な Web ベースのシェルを使用可能にします。```
    http://<yourappname>.mybluemix.net/bluemix-debug/shell
    ```
	
    shell ユーティリティーにアクセスすると、アプリケーションにシェルでアクセスできる端末ウィンドウが表示されます。ファイルの編集、メモリー使用量の確認、診断コマンドの実行など、通常のシェルでサポートされる任意の操作を実行できます。
	
    *shell* ユーティリティーは *proxy* も開始します。

以下のユーティリティーでは、Liberty のみがサポートされます。

  1. *debug*: Liberty アプリケーションをデバッグ・モードにし、IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} などのクライアントがアプリケーションとのリモート・デバッグ・セッションを確立できるようにします。
  
   詳しくは、『[リモート・デバッグ](../manageapps/eclipsetools/eclipsetools.html#remotedebug)』を参照してください。
   
   *debug* ユーティリティーは *proxy* も開始します。
   
  2. *jmx*: JMX REST Connector を使用可能にして、リモート JMX クライアントが {{site.data.keyword.Bluemix_notm}} ユーザー資格情報を使用してアプリケーションを管理できるようにします。
  
  JMX コネクターの構成について詳しくは、『[Configuring secure JMX connection to the Liberty profile](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}』を参照してください。
  
  *jmx* ユーティリティーは proxy を開始しません。

以下のユーティリティーでは、Node.js のみがサポートされます。

  1. *inspector*: *devconsole* ユーティリティーまたは *https://myApp.mybluemix.net/bluemix-debug/inspector* からアクセス可能なノード・インスペクター・デバッガー・インターフェースを使用可能にします。
  
  インスペクター・プロセスは、アプリケーション・コンテナーで実行されます。このユーティリティーを使用することで、CPU 使用プロファイルの作成、ブレークポイントの追加、コードのデバッグを行うことができます。それも、{{site.data.keyword.Bluemix_notm}} でのアプリケーションの実行中に行うことができます。ノード・インスペクター・モジュールについて詳しくは、[GitHub の node-inspector](https://github.com/node-inspector/node-inspector){:new_window} を参照してください。
  
  *inspector* ユーティリティーは *proxy* も開始します。
  
  2. *strongpm*: [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} を使用して、[StrongLoop Metrics、Profiling、Tracing](https://strongloop.com/node-js/devops-tools/){:new_window} などのユーティリティーによって Node.js アプリケーションを分析できるようにします。
    
  *strongpm* ユーティリティーは *proxy* も開始します。
  
  以下のステップを実行して、[StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} によって Node.js アプリケーションを構成します。

    1. *strongpm* BlUEMIX_APP_MGMT_ENABLE 環境変数を構成し、アプリケーションを再ステージングします。
    
	```
    cf set-env <appname> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <appname>
    ```
	
    2. Cloud Foundry コマンド・ラインから、アプリケーションへの経路を追加します。ここで、経路のアプリケーション名には「-pm」を追加します (例えば、<appname>-pm.mybluemix.net)。
    
	```
    cf map-route <appname> ng.bluemix.net -n <appname>-pm
    ```
	
    3. ローカル・ワークステーションで [StrongLoop npm モジュール](https://www.npmjs.com/package/strongloop){:new_window}をインストールします。
    
	```
    npm install -g strongloop
    ```
	
    4. [StrongLoop の Web サイト](https://strongloop.com/register/){:new_window}でアカウントを作成します。
    5. ローカル・ワークステーションで Arc を起動し、作成したアカウントでログインします。
    
	```
    slc arc
    ```
	
    6. Arc 内の「Process Manager」ビューにナビゲートします。新しく作成した経路とポート 80 を Process Manager に入力します。「Activate」ボタンを押します。詳しくは、[Arc の使用に関する完全な資料](https://docs.strongloop.com/display){:new_window}を参照してください。
	
  3. *trace*: アプリケーションが *log4js*、*ibmbluemix*、または *bunyan* ロギング・モジュールを使用している場合のトレース・レベルを動的に設定します。
  
  **注:** サポートされる依存関係バージョン:

    * log4js: (0.6.0 から 0.6.24)
    * bunyan: (1.0.0、1.0.1、1.1.0 から 1.1.3、1.2.0 から 1.2.3、1.3.0 から 1.3.5)
    * ibmbluemix: (1.0.0-20140707-1250) から (1.0.0-20150409-1328)
  
  {{site.data.keyword.Bluemix_notm}} Web コンソールで「インスタンスの詳細」ページに移動し、**「アクション」**を選択して UI を表示します。

  *trace* ユーティリティーは *proxy* を開始しません。

##アプリ管理の構成方法
{: #configure}

アプリ管理ユーティリティーを使用可能にするには、*BLUEMIX_APP_MGMT_ENABLE* 環境変数を設定し、アプリケーションを再ステージングします。「+」で区切ることで、複数のユーティリティーを使用可能にすることができます。

例えば、devconsole ユーティリティーと *shell* ユーティリティーを使用可能にするには、以下のコマンドを実行します。

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

環境変数を設定したら、その後忘れずにアプリケーションを再ステージングしてください。

```
cf restage myApp
```

アプリケーションに併せてアプリ管理ユーティリティーもインストールされることのないようにする場合は、*BLUEMIX_APP_MGMT_INSTALL* 環境変数を「false」に設定して、アプリケーションを再ステージングします。

例えば次のようにします。

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

##制限
{: #restrictions}

* アプリ管理では、単一インスタンス・アプリケーションのみがサポートされます。
* アプリ管理を使用してアプリケーションに対して行った変更は一時的なものであり、このモードを終了すると失われます。このモードは一時的な開発での使用に限られ、パフォーマンスのために実稼働環境としての使用は意図されていません。
* manifest.yml ファイル (command) または CF CLI (-c) で開始コマンドを設定した場合、ほとんどのアプリ管理ユーティリティーは機能しません。
これらのメソッドはビルドパックのオーバーライドであり、Node.js アプリ
ケーションを開始するためのアンチパターンです。結果を最適化するには、package.json ファイルまたは Procfile で開始コマンドを設定します。

##Eclipse Tools の開発モード
{: #devmode}

開発モードは、アプリケーションがクラウドで実行されているときに開発者がアプリケーションを操作できるようにする、[Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools) のフィーチャーです。

{{site.data.keyword.Bluemix_notm}} でアプリケーションを操作している間、開発者は、ローカル環境で実行しているような通常の開発アクティビティーを実行できないと感じる可能性があります。この問題に対処するため、Eclipse Tools を使用した開発モードでは、セキュアな一時ワークスペース内にいながら、クラウドで作業する手段を提供します。

開発モードは Liberty アプリケーションおよび Node.js アプリケーションの両方でサポートされています。開発モードを Liberty または Node.js アプリケーション用に使用可能にすると、アプリケーションをプッシュすることなく、アプリケーション・ファイルを増分的に更新できます。また、アプリケーションとのデバッグ・セッションを確立することもできます。Liberty アプリケーションの開発モードは、debug および jmx アプリ管理ユーティリティーを使用可能にした場合と同等です。Node.js アプリケーションの場合、*devconsole*、*inspector*、および *shell* ユーティリティーを使用可能にした場合と同等です。
