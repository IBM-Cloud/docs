---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 





# アプリの管理に関するトラブルシューティング
{: #managingapps}


アプリケーションの管理に関する一般的な問題には、アプリケーションを更新できない、2 バイト文字を表示できない、などがあります。しかし多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}





## アプリをデバッグ・モードに切り替えられない
{: #ts_debug}

Java 仮想マシン (JVM) バージョンが 8 以下の場合、デバッグ・モードを有効にできないことがあります。 


**「アプリケーションのデバッグを有効にする (Enable application debug)」**を選択すると、ツールはアプリケーションをデバッグ・モードに切り替えようとします。これにより、Eclipse ワークベンチはデバッグ・セッションを開始します。ツールがデバッグ・モードを有効にするのに成功した場合、Web アプリケーションの状況には `Updating mode`、`Developing`、および `Debugging` が表示されます。
{: tsSymptoms}

しかし、ツールがデバッグ・モードを有効にするのに失敗した場合は、Web アプリケーションの状況には、`Updating mode` と `Developing` のみが表示され、`Debugging` は表示されません。ツールは、「コンソール」ビューに以下のエラー・メッセージを表示することもあります。

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at  org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at  com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the  websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
```
 

Java 仮想マシン (JVM) のバージョンが IBM JVM 7、IBM JVM 8、または Oracle JVM 8 より前のバージョンである場合、デバッグ・セッションを確立できません。
{: tsCauses}

ワークベンチの JVM が、これらのバージョンのいずれかである場合、デバッグ・セッションの作成時に問題が生じることがあります。ワークベンチの JVM バージョンは、通常はローカル・コンピューターのシステム JVM です。システム JVM は、実行中の Bluemix Java アプリケーションの JVM と同じではありません。Bluemix Java アプリケーションは、ほとんどの場合、IBM JVM 上で実行され、時には OpenJDK JVM 上で実行されることもあります。
  

IBM Eclipse Tools for Bluemix が稼働している Java のバージョンを確認するには、以下の手順を実行します。
{: tsResolve}

  1. IBM Eclipse Tools for Bluemix で、**「ヘルプ」** > **「Eclipse について」** > **「インストールの詳細」** > **「構成」**を選択します。
  2. リストから `eclipse.vm` プロパティーを検索します。次の行は、`eclipse.vm` プロパティーの例を示しています。
	
	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. コマンド・ラインで、Java のインストール先の `bin` ディレクトリーから `java -version` を入力します。IBM JVM バージョン情報が表示されます。

ワークベンチの JVM が、IBM JVM 7 または 8、あるいは Oracle JVM 8 より前のバージョンである場合は、以下の手順を実行して、Oracle JVM 8 に切り替えます。

  1. Oracle JVM 8 をダウンロードし、インストールします。詳しくは、[Java SE Downloads ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window} を参照してください。
  2. Eclipse を再始動します。
  3. `eclipse.vm` プロパティーが、Oracle JVM 8 の新しいインストール先を指しているかどうかを確認します。

  
## 削除したアプリの名前を再使用できない
{: #ts_reuse_appname}
  
アプリを削除したら、アプリ経路を削除した場合に限り、アプリ名を再使用できます。 

アプリ名を再使用しようとしたときに、以下のメッセージを受け取ります。
{: tsSymptoms}

`名前は別のアプリによって既に使用されています。`

アプリが削除されるとき、アプリの URL である経路は自動的に削除されません。そのため、それは再使用できません。アプリを再使用するため経路を削除するには、アプリが作成されたスペースに移動する必要があります。
{: tsCauses}

使用されていない経路を削除するには、以下の手順を実行します。
{: tsResolve}

  1. 以下のコマンドを入力して、該当経路が現行スペースに属しているかどうかを確認します。 
     ```
	 cf routes
	 ```
  2. 該当経路が現行スペースに属していない場合は、以下のコマンドを入力して、それが属しているスペースまたは組織に切り替えます。 
     ```
	 cf target -o org_name -s space_name
	 ```
  3. 以下のコマンドを入力して、アプリ経路を削除します。
     ```
	 cf delete-route domain_name -n host_name
	 ```
	 例:
	    ```
	 cf delete-route mybluemix.net -n app001
	 ```


	 
	 

## 組織のスペースを取得できない
{: #ts_retrieve_space}
現行組織に関連付けられたスペースがない場合、アプリまたはサービスを作成できません。

Bluemix でアプリを作成しようとすると、以下のエラー・メッセージが表示されます。
{: tsSymptoms}

`BXNUI0515E: 組織のスペースは取得されませんでした。 ネットワーク接続問題が発生したか、現在の組織に関連付けられているスペースがないかのいずれかです。`

このエラーは、多くの場合、カタログからアプリまたはサービスを初めて作成しようとしたときに、スペースがまだ作成されていない場合に受け取ります。
{: tsCauses}

現行組織にスペースを作成したことを確認してください。スペースを作成するには、次のいずれかの方法を使用します。
{: tsResolve}

  * メニュー・バーで**「アカウント」**&gt;**「組織の管理」**をクリックします。スペースを作成する組織を選択してから、**「スペースの作成」**をクリックします。
  * cf コマンド・ライン・インターフェースに `cf create-space <space_name>
-o <organization_name>` と入力します。

やり直してください。
このメッセージが再び表示される場合は、[Bluemix 状況 ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://ibm.biz/bluemixstatus){: new_window} ページにアクセスして、サービスまたはコンポーネントに問題があるかを確認してください。



## 要求したアクションを実行できない
{: #ts_authority}

適切なアクセス権限がない場合、アクションを実行できないことがあります。

 

サービス・インスタンスまたはアプリ・インスタンスに対してアクションを実行しようとしたとき、要求したアクションを実行できず、以下のいずれかのエラー・メッセージが表示されます。
{: tsSymptoms}

`BXNUI0514E: <orgName> 組織内のいずれのスペースの開発者でもありません。(You are not a developer for any of the spaces in the <orgName> organization.)`


`サーバー・エラー、状況コード: 403、エラー・コード: 10003、メッセージ: 要求されたアクションの実行を許可されていません`

 

アクションの実行に必要な、適切なレベルの権限を備えていません。
{: tsCauses}

  
適切な権限レベルを取得するには、以下のいずれかの方法を使用します。
{: tsResolve}
 * 開発者役割を備えている別の組織およびスペースを選択します。 
 * 自分の役割を開発者に変更するように、またはスペースを作成して自分に開発者役割を割り当てるように組織マネージャーに依頼します。詳しくは、『[組織とスペースの管理](/docs/admin/orgs_spaces.html)』を参照してください。
 



## 許可エラーのため、{{site.data.keyword.Bluemix_notm}} サービスにアクセスできない
{: #ts_vcap}

許可エラーは、アプリでサービス資格情報がハードコーディングされている場合にアプリが {{site.data.keyword.Bluemix_notm}} サービスにアクセスすると生じることがあります。 

{{site.data.keyword.Bluemix_notm}} サービスと通信するようにアプリを構成した後に、そのアプリを {{site.data.keyword.Bluemix_notm}} にデプロイします。しかし、アプリを使用して {{site.data.keyword.Bluemix_notm}} サービスにアクセスできず、許可エラーを受け取ります。
{: tsSymptoms}

アプリ内にハードコーディングされた資格情報が正しくない可能性があります。サービスが再作成されるごとに、そのサービスにアクセスするための資格情報が変更されます。
{: tsCauses}


アプリ内に資格情報をハードコーディングするのではなく、VCAP_SERVICES 環境変数からの接続パラメーターを使用してください。VCAP_SERVICES 環境変数からの接続パラメーターを使用する方法は、プログラミング言語によって異なります。例えば、Node.js アプリの場合、以下のコマンドを使用できます。
{: tsResolve}

```
process.env.VCAP_SERVICES
```
他のプログラム言語で使用できるコマンドについて詳しくは、[Java ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} および [Ruby ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window} を参照してください。








## IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} を使用してアプリをデプロイできない
{: #ts_bm_tools_facet}

サポートされないファセットが Eclipse プロジェクトに適用された場合、IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} を使用してアプリを {{site.data.keyword.Bluemix_notm}} にデプロイできない可能性があります。 

 

Cloud Foundry CLI を使用すると、正常にアプリを {{site.data.keyword.Bluemix_notm}} にデプロイすることができます。ただし、IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} を使用すると {{site.data.keyword.Bluemix_notm}} にアプリをデプロイできず、`「Project facet <facet_name> is not supported.」`というエラー・メッセージが表示されます。例えば、`「Project facet Cloud Foundry Standalone Application version 1.0 is not supported.」`というようなメッセージです。
{: tsSymptoms}

 

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} は、プロジェクト・ファセットによって {{site.data.keyword.Bluemix_notm}} ランタイムにプロジェクトをマップします。ファセットは、Eclipse 内の Java EE プロジェクトの要件を定義し、異なるランタイムが異なるプロジェクトに関連付けられるようにランタイム構成の一部として使用されます。 プロジェクトに適用されるファセットが IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} によってサポートされていない場合、IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} を使用してアプリをデプロイできない可能性があります。
{: tsCauses}


IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} を使用してアプリをデプロイできるように、Eclipse プロジェクトからファセットを削除する必要があります。
{: tsResolve} 

ファセットを削除するには、IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} で、プロジェクトについて**「プロジェクト」>「プロパティー」>「プロジェクト・ファセット」**をクリックします。次に、サポートされないファセットのチェック・ボックスをクリアします。 



## 502 Bad Gateway エラーを受信した
{: #ts_502_error}

{{site.data.keyword.Bluemix_notm}} でアプリと対話していて 502 Bad Gateway エラーを受信した場合は、{{site.data.keyword.Bluemix_notm}} 状況ページを確認して、対応したアクションを実行してください。

 

502 Bad Gateway で始まるエラー・メッセージを受信します。例えば、`「502 Bad Gateway: 登録済みエンドポイントが要求の処理に失敗しました。(Registered endpoint failed to handle the request.)」`と表示されます。
{: tsSymptoms}

 

Bad Gateway エラーは通常、Web サイトをホストするメイン・サーバーのデータの保管と中継を行うためにプロキシー・サーバーを使用している Web サイトにアクセスしたときに発生します。メイン・サーバーとプロキシー・サーバーが正しく接続されていない可能性があるため、ブラウザー・ウィンドウに HTTP 状況コード 502 が表示されます。この状況コードは、サイトのメイン・サーバーが、予期した HTTP 実装をプロキシー・サーバーから受信しなかったことを示します。
{: tsCauses}

それほど頻繁ではありませんが、Bad Gateway エラーの原因として他に、インターネット・サービス・プロバイダー (ISP) のドロップアウト、ファイアウォール構成の誤り、ブラウザー・キャッシュのエラーがあります。 

 

ダウンしている {{site.data.keyword.Bluemix_notm}} サービスがあると疑われる場合は、まず、[{{site.data.keyword.Bluemix_notm}} 状況 ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://ibm.biz/bluemixstatus){: new_window} ページを確認してください。回避策として、別の {{site.data.keyword.Bluemix_notm}} 地域でそのサービスを使用することもできます。『[サービスを別の地域で使用](/docs/services/reqnsi.html#cross_region_service)』に詳しい説明があります。サービスの状況が正常の場合には、以下のステップで問題を解決してください。
{: tsResolve}

  * アクションを再試行します。
    * キーボードで F5 を押すか、最新表示ボタンをクリックして、ページを再ロードします。このステップでうまくいかない場合は、ブラウザーのキャッシュと Cookie を消去してから、もう一度再ロードしてください。
	* 異なるブラウザーを使用します。
	* ルーター、モデム、およびコンピューターをリブートします。これらのデバイスをリブートすると、エラー 502 につながる各種エラーが解消する可能性があります。 
  * 時間をおいて、後で再試行します。場合によっては、インターネット・サービス・プロバイダーまたは {{site.data.keyword.Bluemix_notm}} サービスで一時的な問題が発生していることがあります。一時的な問題が解決されるまで待ちます。
  * 問題が解決しない場合は、{{site.data.keyword.Bluemix_notm}} サポートに連絡してください。詳しくは、[{{site.data.keyword.Bluemix_notm}} サポートへのお問い合わせ ![「外部リンク」アイコン](../icons/launch-glyph.svg)](/docs/support/index.html#contacting-bluemix-support){: new_window} を参照してください。 




## ディスク割り当て量を超えた
{: #ts_disk_quota}

ディスク・スペースを使い尽くした場合には、手動でディスク割り当て量を変更して、ディスク・スペースを追加することができます。

  

ディスク・スペースを使い尽くしたときに、ディスク割り当て量を超えたというメッセージが表示される場合があります。この問題を解決するために、アプリ・インスタンスをスケールアップしてディスク・スペースを追加しようとした可能性があります。例えば、アプリ詳細ページでメモリー割り当て量を変更して 256 MB から 1256 MB に拡大した、などです。しかし、ディスク割り当て量は同じままであったために、ディスク・スペースは追加されませんでした。
{: tsSymptoms}


アプリに割り当てられるデフォルトのディスク割り当て量は 1 GB です。追加のディスク・スペースが必要な場合は、ディスク割り当て量を手動で指定する必要があります。
{: tsCauses}

 
以下のいずれかの方法でディスク割り当て量を指定します。指定できる最大ディスク割り当て量は 2 GB です。2 GB でも不十分な場合は、[オブジェクト・ストア](/docs/services/ObjectStorage/index.html)などの外部サービスを試してください。
{: tsResolve}

  * manifest.yml ファイルに以下の項目を追加します。

    ```
	disk_quota: <disk_quota>
	```
  * アプリを {{site.data.keyword.Bluemix_notm}} にプッシュするときに、`cf push` コマンドで **-k** オプションを使用します。

    ```
	cf push appname -p app_path -k <disk_quota>
	```


## Android アプリが {{site.data.keyword.mobilepushshort}} を受信できない
{: #ts_push}

Google にアクセス不能な特定地域の Android アプリは、IBM {{site.data.keyword.mobilepushshort}} サービスで送信した通知を受信できません。この場合には、回避策としてサード・パーティー・サービスを使用できます。

Bluemix アプリに {{site.data.keyword.mobilepushshort}} サービスをバインドして、登録デバイスにメッセージを送信します。ただし、Android プラットフォームで開発されたアプリは、特定の地域で通知を受信できません。
{: tsSymptoms}

IBM {{site.data.keyword.mobilepushshort}} サービスは、Google Cloud Messaging (GCM) サービスを使用して、Android プラットフォームで開発されたモバイル・アプリに通知を送ります。Android アプリが通知を受信できるようにするには、Google Cloud Messaging (GCM) サービスがモバイル・アプリからアクセス可能でなければなりません。GCM サービスが Android アプリから到達不能の地域では、Android アプリは{{site.data.keyword.mobilepushshort}}を受信できません。
{: tsCauses}

 
回避策としては、GCM サービスに依存しないサード・パーティー・サービス (例えば、[Pushy ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://pushy.me){: new_window}、[igetui ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://www.getui.com/){: new_window}、[jpush ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://www.jpush.cn/){: new_window} など) を使用します。
{: tsResolve}



## 組織のサービス上限の超過
{: #ts_servicelimit}

トライアル・ユーザーの場合、組織のサービス上限を超過すると、 {{site.data.keyword.Bluemix_notm}} でアプリケーションを作成できなくなる場合があります。
 

 {{site.data.keyword.Bluemix_notm}} でアプリケーションを作成しようとすると、以下のエラー・メッセージが表示されます。
{: tsSymptoms}

`BXNUI2032E: <service_instances> リソースは作成されませんでした。リソースを作成するために Cloud Foundry に接続している時にエラーが発生しました。Cloud Foundry メッセージ:「組織のサービス上限を超過しました。」`



このエラーは、そのアカウントで持つことのできるサービス・インスタンス数の上限を超過した時に発生します。トライアル・アカウントでは、サービス・インスタンスの最大数は 10 です。
{: tsCauses} 

 

不要なサービス・インスタンスはすべて削除するか、あるいは持つことのできるサービス・インスタンスの数に対する上限を撤廃してください。
{: tsResolve}
 
  * サービス・インスタンスを削除するには、{{site.data.keyword.Bluemix_notm}} コンソールか、またはコマンド・ライン・インターフェースが使用できます。{{site.data.keyword.Bluemix_notm}} コンソールを使用してサービス・インスタンスを削除するには、以下の手順を実行します。
	  1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、削除するサービスをクリックします。サービス・カードが表示されます。
	  2. サービス・カード上で**「メニュー」**アイコンをクリックします。
	  3. **「サービスの削除 (Delete Service)」**をクリックします。サービス・インスタンスを削除すると、その後、そのサービス・インスタンスがバインドされていたアプリケーションを再ステージングするようプロンプトが出ます。
コマンド・ライン・インターフェースを使用してサービス・インスタンスを削除するには、以下の手順を実行します。
	  1. 次を入力して、アプリケーションからサービス・インスタンスをアンバインドします: `cf unbind-service <appname> <service_instance_name>`。
	  2. 次を入力して、サービス・インスタンスを削除します: `cf delete-service <service_instance_name>`。
	  3. サービス・インスタンスを削除した後、次を入力して、サービス・インスタンスがバインドされていたアプリケーションを再ステージングしなければならない場合があります: `cf restage <appname>`.
  * 持つことのできるサービス・インスタンスの数に対する上限を撤廃するには、トライアル・アカウントを支払アカウントに変更します。トライアル・アカウントを支払アカウントに変更する方法については、『[プラン変更方法](/docs/pricing/index.html#changing)』を参照してください。

  
  
## 実行可能ファイルが {{site.data.keyword.Bluemix_notm}} で実行できない
{: #ts_executable}

実行可能ファイルは、別の環境で開発とビルドを行った時は、 {{site.data.keyword.Bluemix_notm}} で実行できない場合があります。 

 

実行可能ファイルは、別の環境で開発とビルドを行った時は、{{site.data.keyword.Bluemix_notm}} で実行することができません。
{: tsSymptoms}

 

 {{site.data.keyword.Bluemix_notm}} にプッシュしたいコンテンツが既に実行可能ファイルであれば、そのコンテンツは前にビルドされており、{{site.data.keyword.Bluemix_notm}} でビルドする必要はありません。その場合、{{site.data.keyword.Bluemix_notm}} でその実行可能ファイルを実行するためにビルドパックは必要ありません。しかし、{{site.data.keyword.Bluemix_notm}} には、ビルドパックが不要であることを明示的に示さなければなりません。
{: tsCauses}

 

その実行可能ファイルを {{site.data.keyword.Bluemix_notm}} にプッシュする際に、ヌルのビルドパックを指定する必要があります。ヌルのビルドパックによって、ビルドパックが不要であることを示します。ヌルのビルドパックは、**-b** オプションを指定した `cf push` コマンドを使用することで指定します。
{: tsResolve}

```
cf push appname -p app_path -c <start_command> -b <null-buildpack>
```
以下に例を示します。
```
cf push appname -p app_path -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```


## 組織のメモリー上限を超過
{: #ts_outofmemory}

トライアル・アカウントのユーザーの場合、組織のメモリー上限を超過すると、アプリを {{site.data.keyword.Bluemix_notm}} にデプロイできない場合があります。ユーザーにできるのは、自分のアプリが使用するメモリーを削減すること、あるいは自分のアカウントのメモリー割り当て量を増やすことです。 



アプリを {{site.data.keyword.Bluemix_notm}} にデプロイする際、次のエラー・メッセージが表示されます。
{: tsSymptoms} 

`失敗 サーバー・エラー、状況コード: 400、エラー・コード: 100005、メッセージ: 組織のメモリー上限を超過しました。`

 

このエラーは、組織の残りメモリー量が、デプロイしたいアプリに必要なメモリー量を下回っている時に発生します。トライアル・アカウントの最大メモリー割り当て量は 2 GB です。
{: tsCauses}



自分のアカウントのメモリー割り当て量を増やすか、自分のアプリが使用するメモリーを減らすか、そのいずれかを行うことができます。
{: tsResolve} 

  * アカウントのメモリー割り当て量を増やすには、トライアル・アカウントを支払アカウントに変更してください。トライアル・アカウントを支払アカウントに変更する方法については、『[支払アカウント](/docs/pricing/index.html#pay-accounts)』を参照してください。 
  * アプリが使用するメモリーを削減するには、{{site.data.keyword.Bluemix_notm}} コンソールまたは cf コマンド・ライン・インターフェースのいずれかを使用します。 {{site.data.keyword.Bluemix_notm}} コンソールを使用する場合は、以下の手順を実行します。
	  1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、アプリケーションを選択します。アプリ詳細ページが開きます。
	  2. 「ランタイム」ペインで、そのアプリの最大メモリー上限またはアプリ・インスタンス数のいずれか、あるいはその両方を減らすことができます。 
	  
	cf コマンド・ライン・インターフェースを使用する場合は、以下の手順を実行します。
	
	  1. アプリで使用しているメモリー量を調べます。
	  ```
	  cf apps
	  ```
	     cf apps コマンドで、自分が現行スペースにデプロイしたアプリがすべてリストされます。各アプリの状況も表示されます。
      2. アプリが使用するメモリー量を削減するには、アプリ・インスタンス数または最大メモリー上限のいずれか、あるいはその両方を減らします。
	  ```
	  cf push appname -p app_path -i instance_number -m memory_limit
      ```
	  3. アプリを再始動して、変更を有効にします。



	  
## アプリが自動的に再始動しない
{: #ts_apps_not_auto_restarted}


アプリは、アプリにバインドしているサービスが機能を停止した時、自動的に再始動されません。	  
	  
 

アプリにバインドしているサービスが異常終了すると、そのアプリで停止、例外、接続障害といった問題が発生した可能性があります。{{site.data.keyword.Bluemix_notm}} では、それらの問題から復旧するためにアプリを自動的に再始動することはありません。
{: tsSymptoms}



この動作は Cloud Foundry の設計によるものです。
{: tsCauses} 

 

コマンド・ライン・インターフェースで以下のコマンドを入力すれば、アプリを手動で再始動できます。
{: tsResolve}

```
cf push appname -p app_path
  ```
さらに、停止、例外、接続障害といった問題を見つけて、そのような問題から復旧するようにアプリをコーディングすることもできます。  

## アプリケーションがプッシュされたときにユーザー定義変数が失われる
{: #ts_varsnotretained}

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} からアプリを {{site.data.keyword.Bluemix_notm}} にプッシュすると、指定した変数は、マニフェスト・ファイルに保存しない限りリセットされてしまいます。



IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} からアプリを {{site.data.keyword.Bluemix_notm}} にプッシュすると、指定した変数は失われます。
{: tsSymptoms} 


ユーザーが指定した変数は、それらをマニフェスト・ファイルに保存した場合のみ保存されます。
{: tsCauses} 

 

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} からアプリを {{site.data.keyword.Bluemix_notm}} にプッシュするときは、「アプリケーション」ウィザードの「アプリケーションの詳細 (Application details)」ページで**「マニフェスト・ファイルに保存 (Save to the manifest file)」**チェック・ボックスを選択してください。これにより、ウィザードで指定した変数が、アプリケーション用のマニフェスト・ファイルに保存されます。次にそのウィザードを開いたときに、それらの変数は自動的に表示されます。
{: tsResolve}



## {{site.data.keyword.Bluemix_notm}} Live Sync アイコンが表示されない
{: #ts_llz_lkb_3r}

IBM Bluemix DevOps Services でアプリを作成したが、Web IDE に IBM Bluemix Live Sync アイコンが表示されません。

 

DevOps Services Web IDE で Node.js アプリを編集するときは、{{site.data.keyword.Bluemix_notm}} ライブ編集、即時再始動、およびデバッグの各アイコンは表示されません。
{: tsSymptoms}

 

以下の場合にはアイコンは使用できません。
{: tsCauses}

  * `manifest.yml` ファイルがプロジェクトの最上位に格納されていない。
  * アプリはプロジェクトの最上位ではなくサブディレクトリーに格納されているが、そのサブディレクトリーのパスが `manifest.yml` ファイルに指定されていない。
  * アプリに `package.json` ファイルが含まれていない。


問題を解決するには、以下のいずれかの方法を使用します。
{: tsResolve} 

  * `manifest.yml` ファイルがプロジェクトの最上位に格納されていなければ、最上位に格納します。
  * アプリがサブディレクトリーに格納されている場合は、そのサブディレクトリーのパスを `manifest.yml` ファイルに指定します。

  ```
path: path_to_application
   ```
  * アプリと同じディレクトリーに `package.json` ファイルを作成します。

  
  
  
<!-- begin STAGING ONLY --> 

## Bluemix Live Sync Debug がコマンド・ラインから開始しない
{: #ts_no_debug}

コマンド・ラインを使用して IBM Bluemix Live Sync Debug フィーチャーをアプリに対して使用可能にしたが、デバッグ・インターフェースにアクセスできません。  
  
 

**BLUEMIX_APP_MGMT_ENABLE** 環境変数を設定し、アプリにデバッグ・フィーチャーを使用可能にしました。しかし、`app_url/bluemix-debug/manage` でデバッグ・ユーザー・インターフェースにアクセスできません。
{: tsSymptoms}



以下の状況では、デバッグ・フィーチャーを使用可能にすることができません。
{: tsCauses} 

  * `manifest.yml` に command 属性が含まれる場合
  * **-c** オプションを使用してアプリを {{site.data.keyword.Bluemix_notm}} にプッシュする場合

 
  
以下のいずれかのオプションを使用して問題を解決します。
{: tsResolve}

  * 推奨されるのは、IBM Node.js ビルドパックを使用してアプリを開始する方法です。詳しくは、『[{{site.data.keyword.Bluemix_notm}} への Node.js アプリケーションのデプロイ](/docs/runtimes/nodejs/index.html#nodejs_runtime)』トピックの「開始コマンド」セクションを参照してください。 
  * `manifest.yml` の command 属性を command: null に修正するか、push コマンドを編集して `-c null` を組み込むことで、既存アプリにコマンドを使用不可にします。 
  * `manifest.yml` から **command** 属性を削除します。その後、{{site.data.keyword.Bluemix_notm}} から現行アプリを削除し、アプリを再びプッシュします。
  
<!-- end STAGING ONLY -->  
  
  

  
  
## 組織が {{site.data.keyword.Bluemix_notm}} で見つからない
{: #ts_orgs}

ある {{site.data.keyword.Bluemix_notm}} 地域で作業しているときに、{{site.data.keyword.Bluemix_notm}} で自分の組織が見つからない場合があります。
  
 

{{site.data.keyword.Bluemix_notm}} コンソールに正常にログインできますが、cf コマンド・ライン・インターフェースまたは Eclipse プラグインを使用してアプリをプッシュすることができません。
{: tsSymptoms}

cf コマンド・ライン・インターフェースを使用してアプリケーションを  {{site.data.keyword.Bluemix_notm}} にプッシュしようとすると、メッセージ内に組織名が指定された、次のいずれかのメッセージが表示されます。 

`組織の検索中にエラーが発生しました (Error finding org)`

`組織が見つかりません (Organization not found)`


Cloud Foundry Eclipse プラグインを使用してアプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュしようとすると、以下のエラー・メッセージが表示されます。

`cloudspace が見つかりません。(cloudspace not found.)`



この問題は、処理したい地域の API エンドポイントが指定されていないことが原因で発生します。探している組織が、別の地域にある可能性があります。
{: tsCauses} 

   
  
cf コマンド・ライン・インターフェースを使用して {{site.data.keyword.Bluemix_notm}} にアプリケーションをプッシュする場合は、cf api コマンドを入力し、地域の API エンドポイントを指定します。例えば、以下のコマンドを入力して、{{site.data.keyword.Bluemix_notm}} の欧州英国地域に接続します。
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
Eclipse ツールを使用してアプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュする場合は、まず {{site.data.keyword.Bluemix_notm}} サーバーを作成し、自分の組織が作成された {{site.data.keyword.Bluemix_notm}} 地域の API エンドポイントを指定します。Eclipse ツールの使用について詳しくは、『[IBM Eclipse Tools for Bluemix を使用したアプリのデプロイ (Deploying apps with IBM Eclipse Tools for Bluemix)](/docs/manageapps/eclipsetools/eclipsetools.html)』を参照してください。  
  
  


## アプリの経路を作成できない
{: #ts_hostistaken}

アプリを {{site.data.keyword.Bluemix_notm}} にデプロイする際、指定したホスト名がすでに使用されていると、アプリの経路を作成できません。



アプリを {{site.data.keyword.Bluemix_notm}} にデプロイする際、次のエラー・メッセージが表示されます。
{: tsSymptoms} 

`経路 hostname.domainname を作成中... 失敗サーバー・エラー、状況コード: 400、エラー・コード: 210003、メッセージ: ホストは使用済みです: hostname (Creating route hostname.domainname ... FAILED Server error, status code: 400, error code: 210003, message: The host is  taken: hostname)`



この問題は、ユーザーが指定したホスト名が既に使用されている場合に発生します。
{: tsCauses} 


  
指定するホスト名は、使用するドメイン内で固有でなければなりません。別のホスト名を指定するには、以下のいずれかの方法を使用して下さい。
{: tsResolve} 

  * `manifest.yml` ファイルを使用してアプリケーションをデプロイする場合は、host オプションでホスト名を指定します。
	 
    ```
    host: host_name	
	```
  * コマンド・プロンプトからアプリケーションをデプロイする場合は、`cf
push` コマンドを **-n** オプションで使用します。 
    ```
    cf push appname -p app_path -n host_name
    ```


## cf push コマンドを使用して WAR アプリをプッシュできない
{: #ts_cf_war}

アプリのロケーションが正しく指定されていないと、cf push コマンドを使用してアーカイブ済み Web アプリを {{site.data.keyword.Bluemix_notm}} にデプロイできない場合があります。
	


`cf push` コマンドを使用して WAR アプリを {{site.data.keyword.Bluemix_notm}} にアップロードする際に、`「ステージング・エラー: ステージングに失敗したため、インスタンスを取得できません (Staging error: cannot get instances since staging failed)」`というエラー・メッセージが表示されます。
{: tsSymptoms} 

 

この問題は、WAR ファイルが指定されていない場合や、WAR ファイルへのパスが指定されていない場合に発生する可能性があります。
{: tsCauses}

 	
	
**-p** オプションを使用して、WAR ファイルを指定するか、WAR ファイルへのパスを追加してください。以下に例を示します。
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
`cf push` コマンドの詳細な情報を確認するには、`cf push -h` を入力してください。





## Liberty アプリケーションが {{site.data.keyword.Bluemix_notm}} にプッシュされる際、2 バイト文字が適切に表示されない
{: #ts_doublebytes}

サーブレットまたは JSP ファイルに対して Unicode サポートが適切に構成されていない場合、2 バイト文字が適切に表示されない可能性があります。

 

Liberty アプリケーションが {{site.data.keyword.Bluemix_notm}} にプッシュされたときは、アプリ内に指定されている 2 バイト文字は正しく表示されません。
{: tsSymptoms}

 

この問題は、サーブレットまたは JSP ファイルに対して Unicode サポートが適切に構成されていない場合に発生する可能性があります。
{: tsCauses}


サーブレットまたは JSP ファイル内で、以下のコードを使用できます。
{: tsResolve} 

  * サーブレット・ソース・ファイル内 
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * JSP 内 
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```
	
	
	

## Node.js アプリをデプロイできない
{: #ts_nodejs_deploy}

Node.js アプリを更新する際、または Node.js アプリを {{site.data.keyword.Bluemix_notm}} にデプロイする際、問題が発生する場合があります。



Node.js アプリを更新する際、または Node.js アプリを {{site.data.keyword.Bluemix_notm}} にデプロイする際に、以下のいずれかのエラー・メッセージが表示される場合があります。
{: tsSymptoms} 

`使用可能なビルドパックによってアプリが正常に検出されませんでした。`


`インスタンス (インデックス 0) は接続の受け入れを開始できませんでした。`


`ステージングに失敗したため、インスタンスを取得できません。`


 

問題の原因としては、以下の理由が考えられます。
{: tsCauses}
 
  * 開始コマンドが指定されていません。
  * Node.js アプリのデプロイに必要なファイルがアプリから欠落しているか、ルート・ディレクトリー以外のフォルダーに置かれています。
  


	
問題を引き起こしている原因に基づいて、以下のアクションを実行してください。
{: tsResolve} 

  * 以下のいずれかの方法で開始コマンドを指定します。 
      * cf コマンド・ライン・インターフェースを使用します。例えば次のようにします。 
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
	  * [package.json ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://docs.npmjs.com/json){: new_window} ファイルを使用します。例えば次のようにします。
	    ```
		{
      ...
  	   "scripts": {
"start": "node app.js"
 	   }
	}
	    ```
	  * `manifest.yml` ファイルを使用します。例えば次のようにします。 
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * Node.js ビルドパックがアプリを認識できるようにするために、`package.json` ファイルがご使用の Node.js アプリ内に必ず存在するようにしてください。また、このファイルはご使用のアプリのルート・ディレクトリーに置く必要があります。以下は単純な `package.json` ファイルの例です。  
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
　　　　},
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```
	
Node.js アプリについてさらにヒントを見るには、[Node.js アプリケーションに関するヒント (Tips for Node.js Applications) ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window} を参照してください。	




## Bluemix DevOps Services から Eclipse に {{site.data.keyword.Bluemix_notm}} Liberty アプリをインポートした後、`server.xml` ファイル内に構成エラーが現れる
{: #ts_eclipse}

{{site.data.keyword.Bluemix_notm}} Liberty アプリを IBM Bluemix DevOps Services から Eclipse にインポートした後、`server.xml` ファイル内に構成エラーを認めた場合は、プロジェクトから `server.xml` ファイルを削除しなければならないことがあります。 

 

{{site.data.keyword.Bluemix_notm}} Liberty アプリを {{site.data.keyword.Bluemix_notm}} DevOps Services から Eclipse にインポートした後、Eclipse の「問題」ビューから `server.xml` ファイル内の構成エラーを確認できます。
{: tsSymptoms}

 

Liberty アプリが {{site.data.keyword.Bluemix_notm}} にプッシュされると、Liberty ビルドパックは `server.xml` ファイルを使用してアプリを構成し、`runtime-vars.xml` ファイルを生成します。アプリを Eclipse にインポートする際、`runtime-vars.xml` ファイルはご使用のローカル環境に存在しません。
{: tsCauses}

 

server.xml ファイルをプロジェクトから削除することで、この問題を解決できます。アプリを WAR アプリとしてプッシュすると、ビルドパックは `server.xml` ファイルを動的に作成します。詳しくは、[『Liberty for
Java』](/docs/runtimes/liberty/index.html)を参照してください。
{: tsResolve}
	
	
## カスタム・ビルドパックを使用してアプリをステージングできない
{: #ts_bp_compilation}

カスタム・ビルドパック内のスクリプトが実行可能でない場合は、そのビルドパックを使用して {{site.data.keyword.Bluemix_notm}} にアプリをデプロイできないことがあります。



カスタム・ビルドパックを使用して {{site.data.keyword.Bluemix_notm}} にアプリをデプロイすると、`「アプリケーションがステージングに失敗したため、表示するインスタンスはありません」`というエラー・メッセージが表示されます。
{: tsSymptoms} 


この問題は、検出スクリプト、コンパイル・スクリプト、リリース・スクリプトなどのスクリプトが実行可能でない場合は発生する可能性があります。
{: tsCauses}

 

[git update ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://git-scm.com/docs/git-update-index){: new_window} コマンドを使用すると、各スクリプトの許可を「実行可能」に変更できます。例えば、`git update --chmod=+x script.sh` と入力できます。
{: tsResolve}
	
	
	
## DevOps Services から {{site.data.keyword.Bluemix_notm}} にアプリをデプロイできない
{: #ts_devops_to_bm}

`manifest.yml` ファイルがアプリ内に存在しない場合、IBM Bluemix DevOps Services から {{site.data.keyword.Bluemix_notm}} にアプリをプッシュできないことがあります。

 

DevOps Services から {{site.data.keyword.Bluemix_notm}} にアプリをデプロイすると、`「サポートされるアプリケーション・タイプを検出できません (Unable to detect a supported application type)」`というエラー・メッセージが表示される場合があります。
{: tsSymptoms}

 

この問題は、{{site.data.keyword.Bluemix_notm}} にアプリをデプロイする際に DevOps Services が `manifest.yml` ファイルを必要とすることが原因で発生する場合があります。
{: tsCauses}

 

この問題を解決するには、`manifest.yml` ファイルを作成する必要があります。`manifest.yml` ファイルの作成方法について詳しくは、『[アプリケーション・マニフェスト](/docs/manageapps/depapps.html#appmanifest)』を参照してください。
{: tsResolve}	
	




## Meteor アプリをプッシュできない
{: #ts_meteor}

ビルドパックが正しく指定されていない場合、Meteor アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュできない可能性があります。

 

{{site.data.keyword.Bluemix_notm}} に Meteor アプリをデプロイすると、`「アプリケーションがステージングに失敗したため、表示するインスタンスはありません」`というエラー・メッセージが表示されることがあります。
{: tsSymptoms}


この問題は、Meteor アプリ用に組み込みビルドパックが提供されていないことが原因で発生します。カスタム・ビルドパックを使用する必要があります。
{: tsCauses} 


 

Meteor アプリにカスタム・ビルドパックを使用するには、以下のいずれかの方法を使用します。
{: tsResolve}

  * `manifest.yml` ファイルを使用してアプリをデプロイする場合は、buildpack オプションを使用して、カスタム・ビルドパックの URL または名前を指定します。例えば次のようにします。
  ```
buildpack: https://github.com/Sing-Li/bluemix-bp-meteor 
  ```
  * コマンド・プロンプトからアプリケーションをデプロイする場合は、`cf push` コマンドを使用し、**-b** オプションによってカスタム・ビルドパックを指定します。例えば次のようにします。
    ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor
	```
	
  

    
## 「{{site.data.keyword.Bluemix_notm}} へのデプロイ (Deploy to Bluemix)」ボタンがアプリをデプロイしない
{: #deploytobluemixbuttondoesntdeployanapp}

「{{site.data.keyword.Bluemix_notm}} へのデプロイ (Deploy to Bluemix)」ボタンをクリックしても、Git リポジトリーが複製されない場合、あるいはアプリがデプロイされない場合は、以下の問題に対するトラブルシューティング方法を試してください。
  * [Bluemix DevOps Services プロジェクトが作成できない](#project-cannot-be-created)
  * [Git リポジトリーが見つからず、DevOps Services で複製できない](#repo-not-found)
  * [Git リポジトリーは DevOps Services で複製されるが、アプリが {{site.data.keyword.Bluemix_notm}}](#repo-cloned-app-not-deployed) にデプロイされない

ボタンの作成方法について詳しくは、『「{{site.data.keyword.Bluemix_notm}} へのデプロイ (Deploy to Bluemix)」ボタンの作成』を参照してください。

### Bluemix DevOps Services プロジェクトが作成できない
{: #project-cannot-be-created}

DevOps Services プロジェクトを作成できない場合は、ご使用の IBM {{site.data.keyword.Bluemix_notm}} アカウントの有効期限が切れている可能性があります。



**「Bluemix へのデプロイ (Deploy to Bluemix)」**ボタンをクリックしても、「プロジェクトの作成 (Creating project)」ステップが正常に完了しません。
{: tsSymptoms} 


お使いの {{site.data.keyword.Bluemix_notm}} アカウントの有効期限が切れている場合があります。
{: tsCauses} 

問題を修正するには、以下のいずれかの方法を使用します。
{: tsResolve}

  * {{site.data.keyword.Bluemix_notm}} にログインして、アカウント情報を更新します。
  * 再度**「Bluemix へのデプロイ (Deploy to Bluemix)」**ボタンをクリックします。


### Git リポジトリーが見つからず、DevOps Services で複製できない
{: #repo-not-found}

Git リポジトリーが複製されない場合は、リポジトリーまたはボタン・スニペットに問題がある場合があります。



**「Bluemix へのデプロイ (Deploy to Bluemix)」**ボタンをクリックしても、Git リポジトリーを見つけることができず、DevOps Services で複製することもできません。「リポジトリーの複製 (Cloning repository)」ステップが正常終了しません。そのため、アプリを {{site.data.keyword.Bluemix_notm}} にデプロイできません。
{: tsSymptoms} 

この問題は、以下の理由で発生することがあります。
{: tsCauses} 

  * Git リポジトリーが存在しないか、アクセスできない可能性があります。
  * ボタン・スニペットの HTML または Markdown に問題が存在する可能性があります。
  * 特殊文字、照会パラメーター、または URL 内のフラグメント化により、Git リポジトリーに正しくアクセスできないという問題が存在する可能性があります。

問題を修正するには、以下のいずれかの方法を使用します。
{: tsResolve}

  * Git リポジトリーが存在し、公的にアクセス可能であること、および URL が正しいことを検証します。
  * スニペットに HTML のエラーも Markdown のエラーも含まれていないことを検証します。
  * 特殊文字、照会パラメーター、またはフラグメントが原因で Git リポジトリーの URL に問題が生じる場合は、ボタン・スニペット内で URL をエンコードします。
  

  
  
### Git リポジトリーは DevOps Services で複製されるが、アプリが {{site.data.keyword.Bluemix_notm}} にデプロイされない
{: #repo-cloned-app-not-deployed}

アプリがデプロイされない場合は、リポジトリーに含まれるコードに問題が存在する可能性があります。
     


**「Bluemix へのデプロイ (Deploy to Bluemix)」**ボタンをクリックすると、Git リポジトリーは DevOps Services で複製されるが、アプリが {{site.data.keyword.Bluemix_notm}} にデプロイされません。「Bluemix へのデプロイ」ステップが正常に完了しません。
{: tsSymptoms} 

この問題は、以下の理由で発生することがあります。
{: tsCauses}  

  * ご使用の {{site.data.keyword.Bluemix_notm}} スペースに、アプリをデプロイするための十分なスペースがない場合があります。 
  * 必要なサービスが `manifest.yml` ファイルで宣言されていない可能性があります。
  * 必要なサービスは `manifest.yml` ファイルで宣言されていても、そのサービスは既にターゲット・スペース内にあります。
  * リポジトリーに含まれるコードに問題が存在する可能性があります。
問題を診断するには、デプロイメントからのビルド・ログとデプロイ・ログを調査します。
  1. 「Bluemix へのデプロイ」ステップが正常に完了しない場合は、前の「パイプラインの構成」ステップに含まれるリンクをクリックして Delivery Pipeline を開きます。
  2. 失敗したビルドまたはデプロイのステージを特定します。
  3. 失敗したステージで、**「ログと履歴の表示 (View logs and history)」**をクリックします。
  4. エラー・メッセージを見つけます。
   
問題を修正するには、以下のいずれかの方法を使用します。
{: tsResolve}

  * エラー・メッセージに、{{site.data.keyword.Bluemix_notm}} スペースにアプリをデプロイするための十分なスペースがないと示されている場合は、別のスペースを対象にします。
  * エラー・メッセージに、必要なサービスが `manifest.yml` ファイルで宣言されていないと示されている場合は、リポジトリーの所有者に、必要なサービスを追加する必要があることを知らせます。
  * エラー・メッセージに、必要なサービスは既にターゲット・スペースに存在すると示されている場合は、別のスペースを選択して使用します。
  * エラー・メッセージに、ビルドに問題が存在すると示されている場合は、アプリのビルドを妨げている、コードに関わる問題をすべて修正します。そのコードに問題が含まれていないことを検証するには、Git コマンドを使用してコードをビルドします。
    1. Git リポジトリーを複製します。
    ```
git clone <git_repository_URL>
    ```
	2. アプリのディレクトリーを開きます。
	```
	cd <appname>
	```
	3. アプリを作成します。
	```
	<appname> create
	```
	4. 必要な場合はアドオンをプロビジョンします。
	5. 必要な構成変数をすべて追加します。
	6. コードをプッシュします。
	```
	git push <appname> master
	```
	7. アプリが正しくビルドされていることを検証します。
	8. 必要な場合は、ポスト・デプロイメント・コマンドを実行します。
	```
	<appname> run
	```
	9. アプリを開き、そのアプリが正常に機能していることを検証します。
	```
	<appname> open
	```
	
## 実行バーからアプリをデプロイできない
{: #deployinganappfromtherunbarfails}

このシナリオで、デプロイメントは黄色の「非同期」状態で失敗します。 

デプロイしているアプリの経路が、実行中の別のアプリと同じです。この問題を修正するには、固有な経路に変更してください。

## 実行バーが見つからない
{: #runbarcannotbefound}

Eclipse Orion {{site.data.keyword.webide}} に実行バーが見つからない場合は、以下のいずれかの問題が発生しています。

1. {{site.data.keyword.jazzhub}} がご使用のプロジェクトをプロジェクトとして識別していない。
   * 修正: プロジェクトのルート・ディレクトリーに `project.json` ファイルを作成します。
2. アプリが含まれているフォルダーを {{site.data.keyword.jazzhub_short}} が判別できなかった。
   * 修正: プロジェクト・ルート以外のディレクトリーにアプリが含まれる場合は、以下のいずれかの手順を行ってください。
      * プロジェクトのルート・ディレクトリーに `manifest.yml` ファイルを作成します。アプリの場所を指すようにファイルを編集します。例えば、`path: path_to_your_app` などです。
      * プロジェクトのルート・ディレクトリーに含まれるようにアプリを移動します。
3. アプリが Node.js アプリであることが {{site.data.keyword.jazzhub_short}} によって検出されない。
   * 修正: プロジェクトのアプリ・フォルダーに `package.json` ファイルを作成します。
   

## GitHub フックが動作しない
{: #githubhookisntworking}

コミットのプッシュ時にワークアイテムのリンクを作成するように GitHub プロジェクトを構成したが、リンクが期待どおり動作していない場合は、以下の手順で問題点を見つけてください。

1. GitHub リポジトリーで**「Settings」**をクリックします。
   ![GitHub の「Settings」リンク](images/github_settings.png)

2. **「Webhooks & services」**をクリックします。
   ![GitHub の「Web hooks and services」リンク](images/github_webhook.png)

3. メッセージを表示するには、{{site.data.keyword.jazzhub}} 状況アイコンの上にマウスを移動します。
   ![サービス・フックに関するエラー・メッセージ](images/github_error.png)

4. GitHub のメッセージに従って、エラーを解決します。

5. 修正により問題が解決したことを確認するには、別の変更をコミットしてプッシュするか、{{site.data.keyword.jazzhub_short}} のサービス・ページに移動して**「Test service」**をクリックします。
   ![GitHub の「Test Service」ボタン](images/github_test.png)

6. 状況アイコンを再びチェックして、エラーがないことを確認します。
   ![エラーのない状況アイコン](images/githubResolved_small.png)

詳しくは、[Setting up GitHub for Bluemix DevOps Services projects ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/githubhooks/){: new_window} を参照してください。


# アカウントの管理に関するトラブルシューティング
{: #managingaccounts}

アカウントを管理しているとき、異なるアプリが同一のドメイン・ネームを共有しているとか、管理者がすべての組織を表示できないといった問題が発生することがあります。しかし多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}


## アカウントが非アクティブである
{: #ts_accnt_inactive}

アカウントが非アクティブの場合は、{{site.data.keyword.Bluemix_notm}} 内でアプリを作成することはできません。この問題を修正するには、サポート・チームに連絡する必要があります。



{{site.data.keyword.Bluemix_notm}} でアプリを作成しようとすると、以下のエラー・メッセージが表示されます。
{: tsSymptoms} 

`BXNUI0096E: アプリは作成されませんでした。アカウントは取り消されたか中断されたため、非アクティブです。`


{{site.data.keyword.Bluemix_notm}} アカウントの状況は、アカウントが取り消されるか、または中断されると非アクティブになります。
{: tsCauses}

 

アカウントを再アクティブ化するには、[{{site.data.keyword.Bluemix_notm}} サポート ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window} にお問い合わせください。E メールには、以下の情報を含めてください。
{: tsResolve}

  * {{site.data.keyword.Bluemix_notm}} へのログインに使用している IBMid。
  * アプリを作成している組織の名前。この情報は、サポート・チームが、組織内の正しい役割またはメンバーシップがユーザーに割り当てられているかどうかを判別するのに役立ちます。



## 現行組織に関連付けられたスペースがない
{: #ts_no_space}

現行組織に関連付けられたスペースがない場合、アプリケーションを作成することはできません。



{{site.data.keyword.Bluemix_notm}} でアプリを作成しようとすると、以下のエラー・メッセージが表示されます。
{: tsSymptoms} 


`BXNUI0097E: アプリを追加するには、その前に、少なくとも 1 つのスペースが組織と地域に関連付けられていなければなりません。ダッシュボードで、「スペースの作成」をクリックします。スペースが作成されたら、やり直してください。`



{{site.data.keyword.Bluemix_notm}} 内のアプリは、組織のスペース内に作成される必要があります。
{: tsCauses} 

 

スペースを作成するには、次のいずれかの方法を使用します。
{: tsResolve}
 
  * {{site.data.keyword.Bluemix_notm}} ダッシュボードで、スペースを作成する組織を選択し、次に**「スペースの作成」**をクリックします。
  * cf コマンド・ライン・インターフェースに `cf create-space <space_name>
-o <organization_name>` と入力します。
  
  
  
  
## 複数のアプリが同じドメイン・ネームを共有している
{: #ts_domain_diff}

{{site.data.keyword.Bluemix_notm}} で、複数のアプリケーションが同じ URL を共有していることがあります。

 

この問題は、同じスペース内の異なるアプリケーションに対して同一の URL 経路を指定した場合に発生する可能性があります。
{: tsCauses}

例えば、myApp1 アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュし、そのドメインを「mynewapp.stage1.mybluemix.net」に設定します。次に、別の myApp2 アプリケーションを同じスペースにプッシュし、その URL 経路の 1 つを「mynewapp.stage1.mybluemix.net」に設定します。この経路は、この時点で両方のアプリケーションにマップされています。

 

これは {{site.data.keyword.Bluemix_notm}} のサポートされている動作で、このプラクティスを用いてアプリケーションのアップグレードにおけるゼロ・ダウン時間を実現することができます。詳しくは、『Blue-green デプロイメント (Blue-green deployments)』を参照してください。
{: tsResolve}
  
	
	
<!-- begin STAGING ONLY --> 
	
	
## 管理者が {{site.data.keyword.Bluemix_notm}} コンソールを使用してすべての組織を表示できない
{: #ts_ui_org}

管理者として {{site.data.keyword.Bluemix_notm}} コンソールを使用したときに、管理のためにすべての組織を表示することはできません。自分が所属する組織のみを表示して管理することができます。

 

管理者として、{{site.data.keyword.Bluemix_notm}} コンソールを使用してすべての組織を表示することはできません。
{: tsSymptoms}

 

これは、{{site.data.keyword.Bluemix_notm}} コンソールの制限です。
{: tsCauses}

 

すべての組織を管理するには、cf コマンド・ライン・インターフェースから `cf orgs`、`cf create-org`、`cf delete-org` などのコマンドを使用できます。cf コマンドの全リストを表示するには、`cf help` と入力してください。
{: tsResolve}
	
<!-- end STAGING ONLY -->




## クレジット・カードを追加できない
{: #ts_addcc}

トライアル・アカウントを従量課金 (PAYG) アカウントに変換するためにクレジット・カード情報を送信することができません。

 

「クレジット・カードの追加」ページの「送信」ボタンが使用不可になっています。
{: tsSymptoms}

 

この問題は、「クレジット・カードの追加」ページに情報が正しく入力されていない場合に発生します。
{: tsCauses}

 

この問題を解決するには、以下のステップを実行してください。
{: tsResolve}

  1. 「クレジット・カードの追加」ページで、連絡先情報、連絡先住所、および請求先住所の各セクションに含まれているすべての必須フィールドに記入します。
  2. **「IBM の使用条件を読み、これに同意します (I have read and agree to IBM's Terms and Conditions)」**を選択して**「送信 (Submit)」**をクリックします。**「お支払い方法の選択 (Select a payment method)」**セクションが表示されます。
  3. クレジット・カード番号、カードの有効期限、およびカードに記載されたセキュリティー・コードを入力します。次に**「送信 (Submit)」**をクリックします。





# ランタイムに関するトラブルシューティング
{: #runtimes}

IBM® Bluemix™ ランタイムを使用すると問題が発生することがあります。しかし多くの場合、いくつかの簡単なステップを実行することで、これらの問題から復旧することが可能です。
{:shortdesc}


## アプリがプッシュされたときに使用できないビルドパックが使用される
{: #ts_loading_bp}


アプリをプッシュしたときに、最新のビルドパック・コンポーネントを使用できない場合があります。使用できないコンポーネントがロードされないように組み込みメカニズムを備えたビルドパックを使用するか、アプリのプッシュや再ステージを行う前にアプリのキャッシュ・ディレクトリー内のコンテンツを削除します。 

 

ビルドパックが更新されてからアプリをプッシュまたは再ステージすると、最新のビルドパック・コンポーネントのロードが自動的に行われません。その結果、アプリは使用できないビルドパック・コンポーネントをキャッシュから使用することになります。アプリを最後にプッシュしてからビルドパックに適用された更新は実装されていません。
{: tsSymptoms}



ビルドパックによっては、すべての更新コンポーネントをインターネットから自動的にダウンロードして、いつでも最新バージョンを使用できるように構成されていないものもあります。
{: tsCauses} 

 

組み込みメカニズムを備えたビルドパックを使用して、使用できないコンポーネントをロードしないようにすることができます。以下に 2 つのビルドパックの例を示します。
{: tsResolve}

  * [Cloud Foundry Java ビルドパック ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack){: new_window}。 このビルドパックには、最新バージョンのビルドパックが使用されるように組み込みメカニズムが装備されています。このメカニズムがどのように機能するのかについて詳しくは、[extending-caches.md ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window} を参照してください。 
  * [Cloud Foundry Node.js ビルドパック ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}。 このビルドパックは、環境変数を使用して同様の機能を提供します。この Node.js ビルドパックを有効にして、毎回インターネットからノード・モジュールをダウンロードするには、cf コマンド・ライン・インターフェースに次のコマンドを入力します。 	
  ```
  set NODE_MODULES_CACHE=false
  ```
使用中のビルドパックが最新のコンポーネントを自動的にロードするメカニズムを提供していない場合は、以下のステップに従って手動でキャッシュ・ディレクトリー内のコンテンツを削除し、アプリを再度プッシュします。
  1. ヌル・ビルドパックのブランチ (例えば https://github.com/ryandotsmith/null-buildpack) をチェックアウトします。ブランチをチェックアウトする方法については、[Git Basics - Getting a Git Repository ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window} を参照してください。  
  2. `null-buildpack/bin/compile` ファイルに以下の行を追加して変更をコミットします。変更をコミットする方法については、[Git Basics - Recording Changes to the Repository ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window} を参照してください。
  ```
rm -rfv $2/*
  ```
  3. 以下のコマンドを使用して、キャッシュを削除するように変更されたヌル・ビルドパックでアプリをプッシュします。このステップを完了すると、アプリのキャッシュ・ディレクトリー内にあるすべてのコンテンツが削除されます。
  ```
cf push appname -p app_path -b <modified_null_buildpack>
  ```
  4. 以下のコマンドを使用して、希望する最新のビルドパックでアプリをプッシュします。 
  ```
cf push appname -p app_path -b <latest_buildpack>
  ```
  
	


## PHP ビルドパックからの NOTICE メッセージ
{: #ts_phplog}

ログからの NOTICE を含むメッセージが表示されることがあります。このようなメッセージのロギングは、ロギング・レベルを変更すれば止めることができます。	
	
 

PHP ビルドパックを使用してアプリケーションを Bluemix にプッシュすると、以下のような `NOTICE` を含むメッセージが表示されることがあります。
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



PHP ビルドパックでは、ロギング・レベルを定義するために error_log パラメーターを使用しています。デフォルトでは、`error_log` パラメーターの値は **stderr notice** です。以下の例には、Cloud Foundry で提供されている PHP ビルドパックの `nginx-defaults.conf` ファイルに含まれる、デフォルトのロギング・レベル構成が示されています。詳しくは、[cloudfoundry/php-buildpack ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window} を参照してください。
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
`NOTICE` メッセージは情報を提供するメッセージであり、必ずしも問題の発生を示すものではありません。これらのメッセージのロギングは、ビルドパックの nginx-defaults.conf ファイルに含まれるロギング・レベルを stderr notice から stderr error に変更することで停止できます。例:
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
デフォルトのロギング構成を変更する方法について詳しくは、[error_log ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window} を参照してください。
	

## サード・パーティーの Python ライブラリーを {{site.data.keyword.Bluemix_notm}} にインポートできない
{: #ts_importpylib}

サード・パーティーの Python ライブラリーを {{site.data.keyword.Bluemix_notm}} にインポートできない場合があります。この問題は、構成ファイルを Python アプリケーションのルート・ディレクトリーに追加することで解決できます。


サード・パーティーの Python ライブラリー、例えば `web.py` ライブラリーをインポートしようとすると、`cf push` コマンドが失敗します。
{: tsSymptoms}


 

この問題は、Python アプリケーションの構成情報が欠落している時に発生します。
{: tsCauses}


 

この問題を解決するには、`requirements.txt` ファイルと `Procfile` ファイルを Python アプリのルート・ディレクトリーに追加します。以下の情報は、web.py ライブラリーをインポートしていると仮定しています。
{: tsResolve}

  1. `requirements.txt` ファイルを Python アプリのルート・ディレクトリーに追加します。
`requirements.txt` ファイルには、Python アプリケーションに必要なライブラリー・パッケージとそのパッケージのバージョンが指定されています。以下の例には、`requirements.txt` ファイルの内容が示されています。ここで、`web.py==0.37` は、ダウンロードされる `web.py` ライブラリーのバージョンが 0.37 であることを示しています。`wsgiref==0.1.2` は、web.py ライブラリーに必要な Web サーバー・ゲートウェイ・インターフェースのバージョンが 0.1.2 であることを示しています。

	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	`requirements.txt` ファイルの構成方法について詳しくは、 「[Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html)」を参照してください。

  2. `Procfile` ファイルを Python アプリケーションのルート・ディレクトリーに追加します。
`Procfile` ファイルには、Python アプリケーションの開始コマンドを含めてください。以下のコマンドでは、*yourappname* が Python アプリケーションの名前で、*PORT* は、アプリのユーザーから要求を受信するために Python アプリケーションが使用しなければならないポート番号です。*$PORT* はオプションです。開始コマンドに PORT を指定しない場合は、代わりに、アプリ内部にある `VCAP_APP_PORT` 環境変数下のポート番号が使用されます。
 
	```
	web: python <yourappname>.py $PORT
	```
これでサード・パーティーの Python ライブラリーを {{site.data.keyword.Bluemix_notm}} にインポートできます。



## 「インスタンスの詳細」ページの「アクション」ボタンが使用不可になっている
{: #ts_actionsbutton}



「インスタンスの詳細」ページの「アクション」ボタンが使用不可になっています。
{: tsSymptoms} 

 

この問題は、以下の理由で発生します。
{: tsCauses}

  * アプリケーションが Java™ Web アプリケーションではない。ランタイム管理ユーティリティー (RMU) がサポートするのは、Liberty ビルドパックでデプロイされた Web アプリケーションのみです。
  * アプリケーションが組み込みの Liberty ビルドパックでデプロイされていない。
  * アプリケーションが古いバージョンの Liberty ビルドパックでデプロイされている。



問題の原因が古いバージョンの Liberty ビルドパックである場合は、{{site.data.keyword.Bluemix_notm}} でアプリケーションを再デプロイしてください。それ以外の場合は、以下のクライアント・アプリケーションのログ・ファイルをサポート・チームにご提供ください。
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## トレース・ウィンドウまたはダンプ・ウィンドウを開く際に資格情報が要求される
{: #ts_username}


 

トレースおよびダンプ・ウィンドウが開く際にユーザー名とパスワードが要求されます。
{: tsSymptoms}

 

この問題は、ログイン・セッションのタイムアウトが原因で発生します。
{: tsCauses}

 

解決方法は、ユーザー名とパスワードを再入力することです。
{: tsResolve}




## トレース操作またはダンプ操作の実行中にエラーが発生する
{: #ts_target}

 

トレース操作またはダンプ操作の実行中にエラー・メッセージが表示されます。そのメッセージは、アプリのターゲット・インスタンスが実行状態にないことを示しています。
{: tsSymptoms}

```
インスタンス 0: トレース仕様が正常に設定されました (Instance 0: Trace specification is set successfully)
インスタンス 2: トレース仕様が正常に設定されました (Instance 2: Trace specification is set successfully)
インスタンス 1: アプリ abcd のターゲット・インスタンス 1 は実行状態にありません (Instance 1: Target instance 1 for app abcd is not in the running state.)。
インスタンス 3: トレース仕様が正常に設定されました (Instance 3: Trace specification is set successfully)
インスタンス 4: トレース仕様が正常に設定されました (Instance 4: Trace specification is set successfully)
```



この問題は、以下の理由で発生します。
{: tsCauses} 

  * トレースまたはダンプ管理の機能は、実行中のアプリケーション・インスタンスのみを対象としている。停止中、開始中、または異常終了状態のアプリケーション・インスタンスには、トレースまたはダンプ操作は使用できません。
  * トレースまたはダンプ・ダイアログが開く時点でアプリケーション・インスタンスの状況が移行中である。 
  


解決方法は、ウィンドウをいったん閉じて、再度開くことです。
{: tsResolve} 



## インスタンスに異なる traceSpecification 構成がある
{: #ts_different_config}

 

1 つのアプリケーションに異なるインスタンスがある場合は、異なる traceSpecification 構成が表示されることがあります。
{: tsSymptoms}

 

この問題は、以下の理由で発生します。
{: tsCauses}

  * 1 つ以上のインスタンスの構成を以前に変更した可能性がある。あるインスタンスの traceSpecification 構成を変更した場合、その構成は同じアプリケーションの他のインスタンスには適用されません。例えば、アプリケーションで log4j を使用していて、このアプリケーションのインスタンスが 2 つあるものとします。インスタンス 0 のログ・レベルを info から debug に変更できますが、インスタンス 1 のログ・レベルは info のままになります。 
  * アプリケーションが拡大し、新規インスタンスが追加された。RMU は、既存のインスタンスの traceSpecification 構成を新規の拡大されたインスタンスに適用しません。新規インスタンスは、デフォルト構成を使用します。例えば、アプリケーションで log4j を使用していて、それに 1 つのインスタンスがあるものとします。このインスタンスのログ・レベルを info から debug に変更できます。この変更を行った後に、アプリケーションを 2 つのインスタンスに拡大した場合、新規インスタンスのログ・レベルは、debug ではなく info になります。
  


この動作は予期されたものです。
{: tsResolve} 





## ディスク割り当て量の超過
{: #ts_diskquota}

アプリ・ログでディスク割り当て量の超過に気付くことがあります。

 

`「ディスク割り当て量の超過 (Disk quota exceeded)」`エラー・メッセージがアプリのログに示されます。
{: tsSymptoms}



この問題は、以下のいずれかの理由で発生します。
{: tsCauses} 

  * ダンプ・ファイルは実行中のアプリケーション・インスタンスと共に生成され、割り振られたディスク割り当て量を使い尽くします。デフォルトでは、1 つのアプリケーション・インスタンスあたりのディスク割り当て量は 1 GB です。ディスク使用量を確認するには、**「ダッシュボード」>「アプリケーション」>「アプリ・ランタイム」**とクリックします。以下の例では、アプリケーションの 2 つのインスタンスについての、ディスク使用量を含むランタイム情報を示しています。
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * ディスク割り当て量は、現在の組織の割り当て量によって制限されます。
  
  


この問題は、以下のいずれかの方法で解決できます。
{: tsResolve} 

  * ダンプ・ファイルをダウンロード後に削除します。
  * デプロイメント・マニフェストに以下の入力内容を含めて、ディスク割り当て量をもっと大きくしてアプリケーションを再デプロイします。
    ```
	ディスク割り当て量: 2048
```
	
	
<!-- begin STAGING ONLY --> 

	
## Log4js ロガー・オブジェクトが Node.js トレースのポップアップ・ウィンドウに表示されない
{: #ts_logger}

log4js と ibmbluemix のモジュールがともにアプリで使用されている場合に、log4js ロガー・オブジェクトが Node.js トレースのポップアップ・ウィンドウに表示されません。 	

 
log4js、winston、および ibmbluemix のモジュールがともにアプリで使用されている場合に、log4js ロガー・オブジェクトが Node.js トレースのポップアップ・ウィンドウに表示されません。
{: tsSymptoms}


log4js と winston のモジュールを使用するログ操作の統合 API を ibmbluemix モジュールが提供しているため、Node.js トレースのポップアップ・ウィンドウには ibmbluemix ロガー・オブジェクトのみが表示されます。これにより、ibmbluemix、log4js、および winston のロガー・オブジェクトのログ・レベル設定が相互に上書きすることを防ぎます。
{: tsCauses}


この動作は予期されたものです。
{: tsResolve}

<!-- end STAGING ONLY -->




<!-- begin STAGING ONLY -->


## 「アプリケーションのすべてのインスタンスにトレース設定を適用 (Apply trace setting to all instances of the application)」チェック・ボックスが無効
{: #ts_bunyan}

Bunyan ロガー・レベルが変更されたときに Node.js トレースのポップアップ・ウィンドウで**「アプリケーションのすべてのインスタンスにトレース設定を適用 (Apply trace setting to all instances of the application)」**のチェック・ボックスがチェックされず、無効になっています。



Bunyan ロガー・オブジェクトのレベルを変更したときに、Node.js トレースのポップアップ・ウィンドウで**「アプリケーションのすべてのインスタンスにトレース設定を適用 (Apply trace setting to all instances of the application)」**のチェック・ボックスがチェックされず、無効になっています。
{: tsSymptoms} 

 

複数の Bunyan ログ・レベルが変更されたとき、アプリケーションのすべてのインスタンスにトレース設定を適用できません。これは、Bunyan ライブラリーでは、Bunyan ロガー・オブジェクトの名前や ID が固有である必要がないためです。アプリケーションのログ・メッセージのレベルを指定するために使用される複数の Bunyan ロガー・オブジェクトで、名前または ID が同じであることが可能です。そのため、アプリケーションのトレース設定が有効であると、アプリケーションのログ・メッセージで指定されるログ・レベルが不正確になる可能性があります。
{: tsCauses}




この動作は予期されたものです。
{: tsResolve} 

<!-- end STAGING ONLY -->

