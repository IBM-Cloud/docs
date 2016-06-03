---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


#サービス
{: #services}
*最終更新日: 2016 年 1 月 20 日*

{{site.data.keyword.Bluemix}} ユーザー・インターフェースの**「サービス」**の下の**「カタログ」**で、使用可能なサービスを見つけることができます。
{:shortdesc}


{{site.data.keyword.Bluemix_notm}} には、モバイル・アプリケーション用の定義済みのサービスが用意されています。{{site.data.keyword.Bluemix_notm}} によって、モバイル・アプリ用のこれらのモバイル・サービスの実装、ホスト、および拡大を簡単に行うことができます。それにより、アプリケーション・ロジックとアプリケーション設計に集中することができます。

{{site.data.keyword.Bluemix_notm}} は、Web アプリケーションのミドルウェア・サービスのホストと管理を行います。アプリケーション開発者は、必要なミドルウェア・サービスを指定できます。そうすると、{{site.data.keyword.Bluemix_notm}} は、指定されたミドルウェア・サービスの新規インスタンスの提供と、サービス・インスタンスのアプリケーションへのバインドを自動的に行います。

{{site.data.keyword.Bluemix_notm}} がサービスを表示する方法には、サービス・カテゴリーごと、およびサービス・サポート・タイプごとの 2 とおりがあります。



<dl>
<dt><strong>カテゴリー</strong></dt>
<dd>{{site.data.keyword.Bluemix_notm}} サービスは、さまざまなカテゴリーで編成されています。それぞれのサービス・カテゴリー内では、IBM が作成したサービス、サード・パーティー・サービス、コミュニティー・サービスの順にサービスがリストされています。</dd>
<dt><strong>サポート</strong></dt>
<dd>{{site.data.keyword.Bluemix_notm}} サービスには複数レベルのサポートが提供されています。
以下の表では、{{site.data.keyword.Bluemix_notm}} サービスの一般的なサポート情報を説明します。</dd>
</dl>



|タイプ 	|説明	|サポートの詳細|
|:------|:--------------|:--------------|
|IBM	|IBM が提供するサービスで、一般出荷可能。	|IBM が提供する一般出荷可能なサービスの欠陥であると判定された問題は、サポート対象となります。サポートは、ユーザーが設定した重大度に基づいて提供されます。チケット重大度について詳しくは、『[サポートへのお問い合わせ](../support/index.html#contacting-bluemix-support){: new_window}』を参照してください。|
|サード・パーティー	|IBM 以外の企業が提供するサービス。	|サード・パーティー・サービスに対するサポートは、各サービス・プロバイダーから提供されます。IBM が問題を調査し、その問題がサード・パーティー・サービスの欠陥であると判定された場合、IBM は修正を提供する義務を負いません。IBM は、必要に応じてサード・パーティー・サービスのプロバイダーと分析内容を共有します。|
|コミュニティー	|オープン・ソース・コミュニティーにより提供されるサービス。	|コミュニティー・サービスに対するサポートは、{{site.data.keyword.Bluemix_notm}} Developers Community から提供されます。IBM が問題を調査し、その問題がコミュニティー・サービスの欠陥であると判定された場合、IBM は修正を提供する義務を負いません。|
|ベータ	|生産準備が未完了で、開発のトライアル・ステージにあるサービス。ベータ・サービスは、開発チームやマーケティング・チームがサービスを一般出荷可能にする前にそのサービスの価値を評価するのに役立ちます。	|IBM が提供するベータ・サービスの欠陥であると判定された問題はサポート対象となりますが、IBM は修正を提供する義務を負いません。また、該当する場合、問題チケットには重大度 3 または 4 が割り当てられます。
チケット重大度については、『[サポートへのお問い合わせ](../support/index.html#contacting-bluemix-support){: new_window}』を参照してください。|
*表 1. {{site.data.keyword.Bluemix_notm}} サービスのサポート情報*



{{site.data.keyword.Bluemix_notm}} には、試すことができる試験的サービスもあります。使用可能な試験的サービス、ボイラープレート、およびランタイムをすべて表示するには、{{site.data.keyword.Bluemix_notm}} にログインした後、「カタログ」の下部にスクロールし、**「{{site.data.keyword.Bluemix_notm}} ラボ・カタログ」**をクリックします。

試験的サービスは安定していない可能性があり、前のバージョンとは互換性のない方向で変更される場合があります。これらのサービスを実稼働環境で使用することは推奨されません。試験的サービスに対するサポートは、{{site.data.keyword.Bluemix_notm}} Developers Community を通じて提供されます。IBM が問題を調査し、その問題が試験的サービスの欠陥であると判定された場合、IBM は修正を提供する義務を負いません。

サービスを {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェース、cf コマンド・ライン・インターフェース、IBM {{site.data.keyword.Bluemix_notm}} DevOps Services、またはサポートされる任意のツールで使用するには、以下のステップを実行します。

1. サービスのインスタンスを作成します。ほとんどの場合、アプリケーションを作成するときに、サービスのインスタンスを作成できます。

2. 新規サービス・インスタンスを使用するアプリケーションを識別します。Web アプリケーションに対しては、同じサービス・インスタンス (たいていの場合はデータ共有のため) を使用する複数のアプリケーションを指定できます。

3. サービスとの対話のためのコードをアプリケーション内に作成します。

##地域別のサービス

各 {{site.data.keyword.Bluemix_notm}} 地域ですべてのサービスが利用できるわけではありません。
以下の表は、IBM が提供するサービスを示しています。



|サービス	|米国南部地域で利用可能	|ヨーロッパ英国地域で利用可能 |オーストラリア、シドニー地域で利用可能|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.activedeployshort}}	|はい		|はい		|いいえ|
|{{site.data.keyword.alchemyapishort}} 		|はい	   	|はい  		|はい|
|{{site.data.keyword.appsecshort}}		|はい		|いいえ		|いいえ|
|{{site.data.keyword.alertnotificationshort}}|はい		|いいえ			|いいえ		|
|{{site.data.keyword.APS_DA}}			|はい		|いいえ		|いいえ|
|{{site.data.keyword.APS_MA}}			|はい		|いいえ		|いいえ|
|{{site.data.keyword.amashort}}			|はい		|はい		|はい|
|{{site.data.keyword.hadoopst}}			|はい		|いいえ		|いいえ|
|{{site.data.keyword.APIM}}			|はい		|はい		|いいえ|
|{{site.data.keyword.autoscaling}}		|はい		|はい		|はい|
|{{site.data.keyword.bigicloudst}}		|はい		|いいえ		|いいえ|
|{{site.data.keyword.rules_short}}		|はい		|はい		|いいえ|
|{{site.data.keyword.cloudint}}			|はい		|はい		|いいえ|
|{{site.data.keyword.cloudant}}			|はい		|はい		|いいえ|
|{{site.data.keyword.conceptexpansionshort}}	|はい		|はい		|はい|
|{{site.data.keyword.conceptinsightsshort}}	|はい		|はい		|はい|
|{{site.data.keyword.dashdbshort}}		|はい		|はい		|いいえ|
|{{site.data.keyword.datacshort}}		|はい		|はい		|はい|
|{{site.data.keyword.DB2OnCloud_short}}		|はい		|はい		|はい|
|{{site.data.keyword.deliverypipeline}}		|はい		|はい		|いいえ|
|{{site.data.keyword.dialogshort}}		|はい		|はい		|はい|
|{{site.data.keyword.documentconversionshort}}	|はい		|はい		|はい|
|{{site.data.keyword.creshort}}			|はい		|いいえ		|いいえ|
|{{site.data.keyword.game}}			|はい		|はい		|はい|
|{{site.data.keyword.geospatialshort_Geospatial}}	|はい	|はい		|いいえ|
|{{site.data.keyword.globalizationshort}}	|はい		|いいえ		|いいえ|
|{{site.data.keyword.dataworks_short}}		|はい		|はい		|いいえ|
|{{site.data.keyword.twittershort}}		|はい		|はい		|はい|
|{{site.data.keyword.weather_short}}		|はい		|はい		|はい|
|{{site.data.keyword.IntegrationTestingshort}}	|はい		|はい		|いいえ|
|{{site.data.keyword.iot_short}}		|はい		|いいえ		|いいえ|
|{{site.data.keyword.keymanagementserviceshort}}|いいえ		|はい		|いいえ|
|{{site.data.keyword.languagetranslationshort}}	|はい		|はい		|いいえ|
|{{site.data.keyword.messagehub}}		|はい		|はい		|いいえ|
|{{site.data.keyword.messageresonanceshort}}	|はい		|はい		|いいえ|
|{{site.data.keyword.APS_MAiOS}} 		|はい		|いいえ		|いいえ|
|{{site.data.keyword.macm_short}}		|はい		|はい		|はい|
|{{site.data.keyword.mobilemam}}		|はい		|はい		|いいえ|
|{{site.data.keyword.mobiledata}}		|はい		|はい		|いいえ|
|{{site.data.keyword.manda}}			|はい		|はい		|いいえ|
|{{site.data.keyword.mqa}}			|はい		|はい		|いいえ|
|{{site.data.keyword.mql}}			|はい		|はい		|いいえ|
|{{site.data.keyword.nlclassifierlshort}} 	|はい 		|はい 		|はい|
|{{site.data.keyword.objectstorageshort}}	|はい		|いいえ		|いいえ|
|{{site.data.keyword.personalityinsightsshort}}	|はい		|はい		|はい|
|{{site.data.keyword.mobilepush}}Push		|はい		|はい		|いいえ|
|Push for iOS 8					|はい		|はい		|いいえ|
|{{site.data.keyword.questionandanswershort}}	|はい		|はい		|はい|
|{{site.data.keyword.rapidApps}}		|はい		|はい		|いいえ|
|{{site.data.keyword.relationshipextractionshort}}	|はい	|はい		|はい|
|{{site.data.keyword.retrieveandrankshort}}	|はい 		|はい 		|はい|
|{{site.data.keyword.SecureGateway}}		|はい		|はい		|いいえ|
|{{site.data.keyword.servicediscoveryshort}}	|はい		|いいえ		|いいえ|
|{{site.data.keyword.sescashort}}		|はい		|はい		|はい|
|{{site.data.keyword.ssofull}}			|はい		|いいえ		|いいえ|
|{{site.data.keyword.speechtotextshort}}	|はい 		|はい	 	|はい|
|{{site.data.keyword.sqldb}}			|はい		|はい		|いいえ|
|{{site.data.keyword.staticanalyzershort}}	|はい		|はい		|いいえ|
|{{site.data.keyword.streaminganalyticsshort}}	|はい		|いいえ		|いいえ|
|{{site.data.keyword.texttospeechshort}} 	|はい 		|はい	 	|はい|
|{{site.data.keyword.times}}			|はい		|はい		|いいえ|
|{{site.data.keyword.toneanalyzershort}} 	|はい 		|はい 		|はい|
|{{site.data.keyword.trackplan}}		|はい		|はい		|いいえ|
|{{site.data.keyword.tradeoffanalyticsshort}}	|はい		|はい		|はい|
|{{site.data.keyword.visualinsightsshort}}	|はい		|はい		|はい|
|{{site.data.keyword.visualizationrenderingshort}} |はい		|はい		|いいえ|
|{{site.data.keyword.workflow}}			|はい		|はい		|いいえ|
|{{site.data.keyword.workloadscheduler}}	|はい		|はい		|いいえ|
|{{site.data.keyword.xpagesservice_short}}	|はい		|はい		|いいえ|
*表 2. サービスの利用可能性*


# アプリケーションへのサービスの追加
{: #add_service}
*最終更新日: 2016 年 3 月 8 日*

{{site.data.keyword.Bluemix}} にはサービスのリストがあり、開発者に代わってそれらのサービスを管理します。アプリケーションで使用するサービスを追加するには、そのサービスのインスタンスを要求し、そのサービスと対話するようアプリケーションを構成する必要があります。

以下の方法で、{{site.data.keyword.Bluemix_notm}} で使用可能なサービスをすべて表示できます。

* {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースから。{{site.data.keyword.Bluemix_notm}} カタログを表示します。
* cf コマンド・ライン・インターフェースから。**cf marketplace** コマンドを使用します。
* ご使用のアプリケーションから。[GET /v2/services Services API](http://apidocs.cloudfoundry.org/197/services/list_all_services.html){: new_window} を使用します。

アプリケーションを開発するときに、必要なサービスを選択できます。選択すると、{{site.data.keyword.Bluemix_notm}} はサービスと対話し、サービスのリソースをプロビジョンするのに必要な手順を実行します。提供のプロセスは、異なるタイプのサービスに対しては異なる可能性があります。例えば、データベース・サービスはデータベースを作成し、モバイル・アプリケーションのプッシュ通知サービスは構成情報を生成します。

{{site.data.keyword.Bluemix_notm}} は、サービス・インスタンスを使用してサービスのリソースをアプリケーションに提供します。サービス・インスタンスは Web アプリケーション間で共有できます。

他の地域でホストされているサービスがその地域内で使用可能である場合、それらのサービスを使用することもできます。これらのサービスはインターネットからアクセスできる必要があり、さらに API エンドポイントを持つ必要があります。{{site.data.keyword.Bluemix_notm}} サービスを利用するために外部アプリケーションやサード・パーティー・ツールをコード化するのと同様に、これらのサービスを利用するにはお使いのアプリケーションを手動でコード化する必要があります。詳しくは、『[{{site.data.keyword.Bluemix_notm}} サービスを利用するための外部アプリケーションとサード・パーティー・ツールの使用可能化](#accser_external)』を参照してください。



## 新規サービス・インスタンスの要求
{: #req_instance}

新規サービス・インスタンスを要求するには、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースまたは cf コマンド・ライン・インターフェースを使用する必要があります。

**注:** サービス名を指定するときは、英字と数字のみを使用してください。英字と数字以外を使用すると、予測できない結果が生じる可能性があります。

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用してサービス・インスタンスを要求する場合、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} **カタログ**で、追加するサービスのタイルをクリックします。サービス詳細ページが開きます。

2. 「サービスの追加」ペインで、このサービス・インスタンスをバインドするアプリケーションを**「アプリ」**リストから選択します。

3. **「サービス名」**フィールドに名前を入力します。
デフォルトのサービス名が表示されます。このフィールドで名前を変更できますし、変更せずにそのままにすることもできます。

4. 追加のフィールドまたは選択に入力してから、**「作成」**をクリックします。

cf コマンド・ライン・インターフェースを使用してサービス・インスタンスを要求する場合、以下のステップを実行します。

1. **cf marketplace** コマンドを使用して、要求するサービスの名前とプランを見つけます。

2. 以下のコマンドを使用してサービス・インスタンスを作成します。ここで、service_name はサービスの名前、service_plan はサービスのプラン、service_instance はこのサービス・インスタンス用に使用する名前です。

    ```
    cf create-service service_name service_plan service_instance
    ```

3. 以下のコマンドを使用してサービス・インスタンスをアプリケーションにバインドします。ここで、appname はアプリケーションの名前、service_instance はサービス・インスタンスの名前です。

    ```
    cf bind-service appname service_instance
    ```

サービス・インスタンスは、同じスペースまたは組織内のアプリ・インスタンスにのみバインド可能です。ただし、外部アプリと同じように他のスペースまたは組織からサービス・インスタンスを使用できます。バインディングを作成する代わりに、資格情報を使用してアプリ・インスタンスを直接構成します。外部アプリが {{site.data.keyword.Bluemix_notm}} サービスを使用する方法について詳しくは、[『外部アプリが {{site.data.keyword.Bluemix_notm}} サービスを使用できるようにする』](#accser_external){: new_window}を参照してください。


## サービスと対話するようアプリケーションを構成する 
{: #config}

ご使用のアプリケーションにサービス・インスタンスをバインドした後、そのサービスと対話するようアプリケーションを構成する必要があります。

各サービスは、アプリケーションと通信するために別のメカニズムを必要とする場合もあります。これらのメカニズムについては、アプリケーションを開発するときに、サービス定義の一部として情報が文書化されます。一貫性のために、メカニズムは、アプリケーションがサービスと対話するために必要です。

* データベース・サービスと対話するには、ユーザー ID、パスワード、およびアプリケーションのアクセス URI など、{{site.data.keyword.Bluemix_notm}} が提供する情報を使用します。
* モバイル・バックエンド・サービスと対話するには、アプリケーション ID (アプリ ID)、クライアント固有のセキュリティー情報、およびアプリケーションのアクセス URI など、{{site.data.keyword.Bluemix_notm}} が提供する情報を使用します。アプリケーション開発者の名前やアプリケーションを使用するユーザーなどのコンテキスト情報を一連のサービスで共有できるように、モバイル・サービスは、通常、互いのコンテキストで作業します。
* Web アプリケーションと、またはモバイル・アプリケーションのサーバー・サイドのクラウド・コードと対話するには、アプリケーションの *VCAP_SERVICES* 環境変数内のランタイム資格情報など、{{site.data.keyword.Bluemix_notm}} が提供する情報を使用します。*VCAP_SERVICES* 環境変数の値は、JSON オブジェクトの直列化です。変数には、アプリケーションにバインドされているサービスと対話するために必要なランタイム・データが含まれます。データのフォーマットは、サービスごとに異なります。期待される情報と、情報の各部分を解釈する方法について、サービスの文書を読み取る必要が生じる場合もあります。

アプリケーションにバインドしたサービスが異常終了すると、そのアプリケーションが稼動を停止したり、エラーを起こしたりする場合があります。{{site.data.keyword.Bluemix_notm}} がアプリケーションを自動的に再始動してこれらの問題から復旧することはありません。障害、例外、および接続失敗を識別して復旧するように、アプリケーションのコーディングを検討してください。詳しくは、[アプリの非自動再始動](../troubleshoot/index.html#ts_topmenubar)のトラブルシューティングのトピックを参照してください。

## 外部アプリが {{site.data.keyword.Bluemix_notm}} サービスを使用できるようにする
{: #accser_external}

{{site.data.keyword.Bluemix_notm}} の外部で作成および実行されるアプリケーションがある場合や、サード・パーティー・ツールを使用する場合があります。インターネットからアクセスできるエンドポイントを {{site.data.keyword.Bluemix_notm}} サービスが提供する場合は、それらのサービスをローカル・アプリやサード・パーティー・ツールで使用できます。

外部アプリまたはサード・パーティー・ツールで {{site.data.keyword.Bluemix_notm}} サービスを使用できるようにするには、以下のステップを実行します。

1. サービスのインスタンスを要求します。
    1. {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースの「ダッシュボード」で、**「サービスまたは API を使用 (Use Services or APIs)」**をクリックします。「カタログ」が表示されます。
    2. 「カタログ」で、サービス・タイルをクリックして必要なサービスを選択します。サービス詳細ページが開きます。
    3. 「サービスの追加」ウィンドウで、**「アプリ:」**リスト選択を**「アンバインドのまま」**にしておきます。この選択は、サービスが {{site.data.keyword.Bluemix_notm}} アプリに接続されないことを意味します。
    4. 必要に応じてその他の選択を行います。その後、**「作成」**をクリックします。サービス・インスタンスが作成され、サービスの「ダッシュボード」が表示されます。
2. サービスの「ダッシュボード」の左方ナビゲーション・ペインで、**「サービス資格情報 (Service Credentials)」**を選択すると JSON 形式で資格情報を表示および追加することができます。資格情報として表示されている API キーを使用して、サービス・インスタンスに接続します。

これで、{{site.data.keyword.Bluemix_notm}} の外部で実行されるアプリケーションが、{{site.data.keyword.Bluemix_notm}} サービスにアクセスできるようになりました。

**注:** サービス・インスタンスの削除または請求情報の確認を行う場合は、ユーザー・インターフェースの「ダッシュボード」に戻ってサービス・インスタンスを管理する必要があります。

## ユーザー提供のサービス・インスタンスの作成
{: #user_provide_services}

{{site.data.keyword.Bluemix_notm}} の外部で管理されているリソースが存在する場合もあります。そうした外部リソースにインターネットからアクセスするための資格情報を持っていれば、{{site.data.keyword.Bluemix_notm}} のユーザー提供サービス・インスタンスを作成することによって、外部リソースを表現し、そのリソースと通信することができます。

ユーザー提供のサービス・インスタンスを作成し、それをアプリケーションにバインドするには、以下のステップを実行します。

1. **cf create-user-provided-service** コマンドまたは **cf cups** コマンドを使用して、ユーザー提供のサービス・インスタンスを作成します。
    * 一般的なユーザー提供のサービス・インスタンスを作成するには、**-p** オプションを使用し、パラメーター名をコンマで区切ります。cf コマンド・ライン・インターフェースはその後、各パラメーターについて順にプロンプトを出します。以下に例を示します。```
        cf cups testups1 -p "host, port, dbname, username, password"
        host> pubsub01.example.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Creating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * サード・パーティーのログ管理ソフトウェアに情報をドレーンするサービス・インスタンスを作成するには、**-l** オプションを使用し、そのサード・パーティーのログ管理ソフトウェアが提供する宛先を指定します。例えば次のようにします。

        ```
        cf cups testups2 -l syslog://example.com
        Creating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

    ユーザー提供のサービス・インスタンスの 1 つ以上のパラメーターを更新する場合は、**cf update-user-provided-service** コマンドまたは **cf uups** コマンドを使用します。

    * 一般的なユーザー提供のサービス・インスタンスを更新するには、**-p** オプションを使用して、パラメーターのキーと値を JSON オブジェクトで指定します。例えば次のようにします。

        ```
        cf uups testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Updating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * サード・パーティーのログ管理ソフトウェアに情報をドレーンするサービス・インスタンスを作成するには、-l オプションを使用します。例えば次のようにします。

        ```
        cf uups testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. cf bind-service コマンドを使用して、サービス・インスタンスをアプリケーションにバインドします。例えば次のようにします。

	```
	cf bind-service myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

外部リソースを使用するようアプリケーションを構成できるようになりました。サービスと対話するようアプリケーションを構成する方法については、[「サービスと対話するようアプリケーションを構成する」](#config){: new_window}を参照してください。

## 他の地域でサービスを利用する
{: #cross_region_service}

ある地域でサービス・インスタンスを作成してアプリにバインドした場合、以下のいずれかの方法でそのサービス・インスタンスを他の地域で利用できます。

  * サービス資格情報を使用して、アプリ・インスタンスを直接構成します。詳しくは、[『外部アプリが {{site.data.keyword.Bluemix_notm}} サービスを使用できるようにする』](#accser_external){: new_window}を参照してください。
  * ブリッジとしてユーザー提供サービスを作成します。
    
	サービス・インスタンスを利用する地域で開始すると想定します。他の地域にあるサービス・インスタンスを利用するには、以下のステップを実行します。

      1. サービス・インスタンスが存在する地域に切り替えます。{{site.data.keyword.Bluemix_notm}} の上部メニュー・バーで、**「地域」**を展開するか、または**「地域」**アイコンをクリックしてから、 サービス・インスタンスの存在する地域を選択します。

      2. サービスの存在する地域にあるサービス・インスタンスの VCAP_SERVICES 環境変数から、資格情報と接続パラメーターを取り出します。以下のステップを実行します。

	       1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、アプリケーション・タイルをクリックします。「概要」ページが表示されます。
	       2. 左方のナビゲーション・ペインで、**「環境変数」**をクリックします。*VCAP_SERVICES* 環境変数の詳細が、右方のペインに表示されます。サービス・インスタンスの JSON コンテンツを記録します。

      3. サービス・インスタンスを利用する地域に切り替えます。{{site.data.keyword.Bluemix_notm}} の上部メニュー・バーで、**「地域」**を展開するか、または**「地域」**アイコンをクリックして、サービス・インスタンスを利用する地域を選択します。

      4. *VCAP_SERVICES* 環境変数から記録した資格情報と接続パラメーターを使用して、ユーザー提供のサービス・インスタンスを作成します。ユーザー提供のサービス・インスタンスを作成する方法について詳しくは、[ユーザー提供のサービス・インスタンスの作成](#user_provide_services){: new_window} を参照してください。

      5. 以下のコマンドを使用して、ユーザー提供のサービス・インスタンスをアプリにバインドします。

	     ```
	     cf bind-service myapp user-provided_service_instance
	```






## 他のサービスでのサービスの使用
{: #s2s_binding}

サービス・アクセス許可は、あるサービスが別のサービスに直接アクセスする手段を提供します。{{site.data.keyword.Bluemix_notm}} ダッシュボードで、あるサービス・インスタンスから別のサービス・インスタンスへのアクセスを許可および構成できます。

別のサービスのサービス・インスタンスを使用するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、
アクセスするサービスのタイルをクリックします。そのサービスのダッシュボードが表示されます。
2. 左側のナビゲーション・ペインで、*Manage* をクリックし、サービス・インスタンスのコンソールを使用した他のサービス・インスタンスからのバインディングを許可します。
3. 他のサービスによるサービス・インスタンスへのアクセスを拒否する場合は、左側のナビゲーション・ペインの*「サービス・アクセス許可 (Service Access Authorization)」*をクリックしてから、*「取り消し (Revoke)」*を使用してサービス・バインディングを削除します。 

# 関連リンク
{: #rellinks}

## 一般
{: #general}

* [{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用したサービスのバインド](../cfapps/ee.html#ee_bindui)
* [VCAP_SERVICES の取得](../cli/vcapsvc.html#retrieving)


