#サービス
*Last Updated: 8/25/2015*

{{site.data.keyword.Bluemix}} ユーザー・インターフェースの**「サービス」**の下の**「カタログ」**で、使用可能なサービスを見つけることができます。

{{site.data.keyword.Bluemix_notm}} には、モバイル・アプリケーション用の定義済みのサービスが用意されています。{{site.data.keyword.Bluemix_notm}} によって、
モバイル・アプリ用のこれらのモバイル・サービスの実装、ホスト、および拡大を簡単に行うことができます。それにより、
アプリケーション・ロジックとアプリケーション設計に集中することができます。

{{site.data.keyword.Bluemix_notm}} は、Web アプリケーションの
ミドルウェア・サービスのホストと管理を行います。アプリケーション開発者は、
必要なミドルウェア・サービスを指定できます。そうすると、{{site.data.keyword.Bluemix_notm}} は、
指定されたミドルウェア・サービスの新規インスタンスの提供と、
サービス・インスタンスのアプリケーションへのバインドを自動的に行います。

{{site.data.keyword.Bluemix_notm}} がサービスを表示する方法には、サービス・カテゴリーごと、およびサービス・サポート・タイプごとの 2 とおりがあります。

**カテゴリー**

{{site.data.keyword.Bluemix_notm}} サービスは、さまざまなカテゴリーで編成されています。それぞれのサービス・カテゴリー内では、IBM が作成したサービス、サード・パーティー・サービス、コミュニティー・サービスの順にサービスがリストされています。

**サポート**

{{site.data.keyword.Bluemix_notm}} サービスには複数レベルのサポートが提供されています。
以下の表では、{{site.data.keyword.Bluemix_notm}} サービスの一般的なサポート情報を説明します。

*Table 1. {{site.data.keyword.Bluemix_notm}} services support information*

|タイプ 	|説明	|サポートの詳細|
|:------|:--------------|:--------------|
|IBM	|A service that is provided by IBM and is generally available.	|IBM が提供する一般出荷可能なサービスの欠陥であると判定された問題は、サポート対象となります。
サポートは、ユーザーが設定した重大度に基づいて提供されます。For more information about ticket severity, see [Contacting {{site.data.keyword.Bluemix_notm}} support](https://www.ng.bluemix.net/docs/troubleshoot/getting_customer_support.html#bluemix_support).|
|サード・パーティー	|A service that is provided by a company other than IBM.	|サード・パーティー・サービスに対するサポートは、各サービス・プロバイダーから提供されます。If a problem is investigated by IBM and the problem is determined to be a defect in a third-party service, IBM is not obligated to provide a fix. IBM will share analysis with the third-party service provider if needed.|
|コミュニティー	|オープン・ソース・コミュニティーにより提供されるサービス。	|コミュニティー・サービスに対するサポートは、{{site.data.keyword.Bluemix_notm}} Developers [Community](https://developer.ibm.com/bluemix/) により、{{site.data.keyword.Bluemix_notm}} Developers
Community [フォーラム](https://developer.ibm.com/answers/smartspace/bluemix/)を通じて提供されます。If a problem is investigated by IBM and the problem is determined to be a defect in a community service, IBM is not obligated to provide a fix.|
|ベータ	|生産準備が未完了で、開発のトライアル・ステージにあるサービス。ベータ・サービスは、開発チームやマーケティング・チームがサービスを一般出荷可能にする前にそのサービスの価値を評価するのに役立ちます。	|Problems that are determined to be a defect in an IBM-provided beta service are supported, but IBM is not obligated to provide a fix. また、該当する場合、問題チケットには重大度 3 または 4 が割り当てられます。
For information about ticket severity, see [Contacting {{site.data.keyword.Bluemix_notm}} support](https://www.ng.bluemix.net/docs/troubleshoot/getting_customer_support.html#bluemix_support).|

{{site.data.keyword.Bluemix_notm}} には、試すことができる試験的サービスもあります。To view all available experimental services, boilerplates, and runtimes, log in to {{site.data.keyword.Bluemix_notm}}, scroll to the bottom of the Catalog, and then click **{{site.data.keyword.Bluemix_notm}} Lab Catalog**.

試験的サービスは安定していない可能性があり、前のバージョンとは互換性のない方向で変更される場合があります。これらのサービスを実稼働環境で使用することは推奨されません。試験的サービスに対するサポートは、{{site.data.keyword.Bluemix_notm}} Developers
Community [フォーラム](https://developer.ibm.com/answers/smartspace/bluemix/)を通じて提供されます。IBM が問題を調査し、その問題が試験的サービスの欠陥であると判定された場合、IBM は修正を提供する義務を負いません。

To use a service in the {{site.data.keyword.Bluemix_notm}} user interface, cf command line interface, IBM {{site.data.keyword.Bluemix_notm}} DevOps Services, or any supported tools, take the following steps:

1. サービスのインスタンスを作成します。ほとんどの場合、アプリケーションを作成するときに、サービスのインスタンスを作成できます。

2. 新規サービス・インスタンスを使用するアプリケーションを識別します。Web アプリケーションに対しては、同じサービス・インスタンス (たいていの場合はデータ共有のため) を使用する複数のアプリケーションを指定できます。

3. サービスとの対話のためのコードをアプリケーション内に作成します。

##地域別のサービス

各 {{site.data.keyword.Bluemix_notm}} 地域ですべてのサービスが利用できるわけではありません。
The following table shows the services that are provided by IBM.

*Table 2. Service availability*

|サービス	|米国南部地域で利用可能	|ヨーロッパ英国地域で利用可能|
|:----------|:------------------------------|:------------------|
|App Sec Manager	|はい	|いいえ|
|AppScan® Dynamic Analyzer	|はい	|いいえ|
|AppScan Mobile Analyzer	|はい	|いいえ|
|Advanced Mobile Access	|はい	|はい|
|Analytics for Apache Hadoop	|はい	|いいえ|
|API Management	|はい	|はい|
|Auto-Scaling	|はい	|はい|
|BigInsights®	|はい	|いいえ|
|Business Rules	|はい	|はい|
|Cloud Integration	|はい	|はい|
|Cloudant® NoSQL DB	|はい	|はい|
|Concept Expansion	|はい	|はい|
|dashDB™	|はい	|はい|
|Data Cache	|はい	|はい|
|Delivery Pipeline	|はい	|はい|
|Embeddable Reporting	|はい	|いいえ|
|Gamification	|はい	|はい|
|Geospatial Analytics	|はい	|はい|
|Globalization	|はい	|いいえ|
|IBM DataWorks	|はい	|はい|
|Insights for Twitter	|はい	|はい|
|Integration Testing	|はい	|はい|
|Internet of Things Foundation	|はい	|いいえ|
|Message Hub	|はい	|いいえ|
|Message Resonance	|はい	|はい|
|Mobile Analyzer for iOS	|はい	|いいえ|
|Mobile Application Security	|はい	|はい|
|Mobile Data	|はい	|はい|
|Monitoring and Analytics	|はい	|はい|
|Mobile Quality Assurance	|はい	|はい|
|MQ Light	|はい	|はい|
|Object Storage	|はい	|いいえ|
|Push	|はい	|はい|
|Push for iOS 8	|はい	|はい|
|Question and Answer	|はい	|はい|
|Rapid Apps	|はい	|はい|
|Relationship Extraction	|はい	|はい|
|Secure Gateway	|はい	|はい|
|Session Cache	|はい	|はい|
|Single Sign On	|はい	|いいえ|
|SQL Database	|はい	|はい|
|Static Analyzer	|はい	|はい|
|Streaming Analytics	|はい	|いいえ|
|Time Series Database	|はい	|はい|
|Track & Plan	|はい	|はい|
|Visualization Rendering	|はい	|はい|
|Workflow	|はい	|はい|
|Workload Scheduler	|はい	|はい|
|XPages NoSQL Database	|はい	|はい|


##アプリケーションへのサービスの追加
*Last Updated: 8/25/2015*

{{site.data.keyword.Bluemix}} にはサービスのリストがあり、開発者に代わってそれらのサービスを管理します。アプリケーションで使用するサービスを追加するには、そのサービスのインスタンスを要求し、そのサービスと対話するようアプリケーションを構成する必要があります。

以下の方法で、{{site.data.keyword.Bluemix_notm}} で使用可能なサービスをすべて表示できます。

* {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースから。View the {{site.data.keyword.Bluemix_notm}} Catalog.
* cf コマンド・ライン・インターフェースから。**cf marketplace** コマンドを使用します。
* ご使用のアプリケーションから。Use the [GET /v2/services Services API](http://apidocs.cloudfoundry.org/197/services/list_all_services.html).

アプリケーションを開発するときに、必要なサービスを選択できます。選択すると、{{site.data.keyword.Bluemix_notm}} はサービスと対話し、
サービスのリソースをプロビジョンするのに必要な手順を実行します。提供のプロセスは、異なるタイプのサービスに対しては
異なる可能性があります。例えば、データベース・サービスはデータベースを作成し、
モバイル・アプリケーションのプッシュ通知サービスは構成情報を生成します。

{{site.data.keyword.Bluemix_notm}} は、サービス・インスタンスを使用してサービスのリソースをアプリケーションに提供します。サービス・インスタンスは Web アプリケーション間で共有できます。

他の地域でホストされているサービスがその地域内で使用可能である場合、それらのサービスを使用することもできます。これらのサービスはインターネットからアクセスできる必要があり、さらに API エンドポイントを持つ必要があります。{{site.data.keyword.Bluemix_notm}} サービスを利用するために外部アプリケーションやサード・パーティー・ツールをコード化するのと同様に、これらのサービスを利用するにはお使いのアプリケーションを手動でコード化する必要があります。
For more information, see [Enabling external applications and third-party tools to use {{site.data.keyword.Bluemix_notm}} services](https://www.ng.bluemix.net/docs/services/reqnsi.html#accser_external).

{{site.data.keyword.Bluemix_notm}} アプリケーションで使用するために {{site.data.keyword.Bluemix_notm}} サービス・カタログにサービスを追加する場合、ユーザーは独自のサービスを構築し、それを {{site.data.keyword.Bluemix_notm}} と統合することができます。For more information, see [Integrating a service with {{site.data.keyword.Bluemix_notm}}](https://www.stage1.ng.bluemix.net/docs/services/v2api.html).

###新規サービス・インスタンスの要求

新規サービス・インスタンスを要求するには、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースまたは cf コマンド・ライン・インターフェースを使用する必要があります。

**Note:** When you specify the service name, avoid using characters other than alphabetic or numeric characters, because results might be unpredictable.

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用してサービス・インスタンスを要求する場合、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} **カタログ**で、追加するサービスのタイルをクリックします。サービス詳細ページが開きます。

2. In the Add Service pane, select an application that you want to bind this service instance to from the **App** list.

3. **「サービス名」**フィールドに名前を入力します。
デフォルトのサービス名が表示されます。このフィールドで名前を変更できますし、変更せずにそのままにすることもできます。

4. 追加のフィールドまたは選択に入力してから、**「作成」**をクリックします。

cf コマンド・ライン・インターフェースを使用してサービス・インスタンスを要求する場合、以下のステップを実行します。

1. **cf marketplace** コマンドを使用して、要求するサービスの名前とプランを見つけます。

2. Use the following command to create a service instance, where service_name is the name of the service, service_plan is the plan of the service, and service_instance is the name that you want to use for this service instance.

    ```
    cf create-service service_name service_plan service_instance
    ```

3. Use the following command to bind the service instance to an application, where appname is the name of the application, and service_instance is the name of the service instance.

    ```
    cf bind-service appname service_instance
    ```

**Note:** A service instance is specific to a space where the service instance is created. サービス・インスタンスを別のスペースまたは組織に移動することはできません。代わりに、サービス・インスタンスを使用するスペースごとに新しいサービス・インスタンスを要求する必要があります。

### <a id='config'></a> Configuring your application to interact with a service ###

ご使用のアプリケーションにサービス・インスタンスをバインドした後、そのサービスと対話するようアプリケーションを構成する必要があります。

各サービスは、アプリケーションと通信するために別のメカニズムを必要とする場合もあります。これらのメカニズムについては、
アプリケーションを開発するときに、サービス定義の一部として情報が文書化されます。一貫性のために、
メカニズムは、アプリケーションがサービスと対話するために必要です。

* データベース・サービスと対話するには、ユーザー ID、パスワード、およびアプリケーションのアクセス URI など、{{site.data.keyword.Bluemix_notm}} が提供する情報を使用します。
* モバイル・バックエンド・サービスと対話するには、アプリケーション ID (アプリ ID)、クライアント固有のセキュリティー情報、およびアプリケーションのアクセス URI など、{{site.data.keyword.Bluemix_notm}} が提供する情報を使用します。アプリケーション開発者の名前や
アプリケーションを使用するユーザーなどのコンテキスト情報を一連のサービスで共有できるように、
モバイル・サービスは、通常、互いのコンテキストで作業します。
* Web アプリケーションと、またはモバイル・アプリケーションのサーバー・サイドのクラウド・コードと対話するには、アプリケーションの *VCAP_SERVICES* 環境変数内のランタイム資格情報など、{{site.data.keyword.Bluemix_notm}} が提供する情報を使用します。*VCAP_SERVICES* 環境変数の値は、JSON オブジェクトの直列化です。変数には、
アプリケーションにバインドされているサービスと対話するために必要なランタイム・データが含まれます。データのフォーマットは、
サービスごとに異なります。
期待される情報と、情報の各部分を解釈する方法について、サービスの文書を読み取る必要が生じる場合もあります。

アプリケーションにバインドしたサービスが異常終了すると、そのアプリケーションが稼動を停止したり、エラーを起こしたりする場合があります。{{site.data.keyword.Bluemix_notm}} does not automatically restart the application to recover from these problems. 障害、例外、および接続失敗を識別して復旧するように、アプリケーションのコーディングを検討してください。詳しくは、[アプリの非自動再始動](https://www.ng.bluemix.net/docs/troubleshoot/managingapps.html#tr_appnotautorestarted)のトラブルシューティングのトピックを参照してください。

###外部アプリが {{site.data.keyword.Bluemix_notm}} サービスを使用できるようにする

{{site.data.keyword.Bluemix_notm}} の外部で作成および実行されるアプリケーションがある場合や、
サード・パーティー・ツールを使用する場合があります。インターネットからアクセスできるエンドポイントを {{site.data.keyword.Bluemix_notm}} サービスが提供する場合は、それらのサービスをローカル・アプリやサード・パーティー・ツールで使用できます。

To enable an external app or third-party tool to use a {{site.data.keyword.Bluemix_notm}} service, complete the following steps:

1. サービスのインスタンスを要求します。
    1. On the Dashboard in the {{site.data.keyword.Bluemix_notm}} user interface, click **Use Services or APIs**. The Catalog displays.
    2. From the Catalog, select the service that you want by clicking the service tile. サービス詳細ページが開きます。
    3. In the Add Service window, keep the **App**: list selection as **Leave unbound**. This selection means that the service will not be connected to a {{site.data.keyword.Bluemix_notm}} app.
    4. 必要に応じてその他の選択を行います。その後、**「作成」**をクリックします。A service instance is created, and the service Dashboard displays.
2. In the left navigation pane of the service Dashboard, you can select **Service Credentials** to view or add credentials in JSON format. 資格情報として表示されている API キーを使用して、サービス・インスタンスに接続します。

これで、{{site.data.keyword.Bluemix_notm}} の外部で実行されるアプリケーションが、
{{site.data.keyword.Bluemix_notm}} サービスにアクセスできるようになりました。

**Note:** If you want to delete service instances or check the billing information, you must go back to your Dashboard in the user interface to manage the service instances.

###ユーザー提供のサービス・インスタンスの作成

{{site.data.keyword.Bluemix_notm}} の外部で管理されているリソースが存在する場合もあります。そうした外部リソースにインターネットからアクセスするための資格情報を持っていれば、{{site.data.keyword.Bluemix_notm}} のユーザー提供サービス・インスタンスを作成することによって、外部リソースを表現し、そのリソースと通信することができます。

ユーザー提供のサービス・インスタンスを作成し、それをアプリケーションにバインドするには、以下のステップを実行します。

1. **cf create-user-provided-service** コマンドまたは **cf
cups** コマンドを使用して、ユーザー提供のサービス・インスタンスを作成します。
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

    * サード・パーティーのログ管理ソフトウェアに情報をドレーンするサービス・インスタンスを作成するには、**-l** オプションを使用し、そのサード・パーティーのログ管理ソフトウェアが提供する宛先を指定します。
例えば次のようにします。

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

    * To create a service instance that drains information to a third-party log management software, use the -l option. 例えば次のようにします。

        ```
        cf uups testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. Bind the service instance to your application by using the cf bind-service command. 例えば次のようにします。

	```
	cf bind-service myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

外部リソースを使用するようアプリケーションを構成できるようになりました。サービスと対話するようアプリケーションを構成する方法については、[「サービスと対話するようアプリケーションを構成する」](#config)を参照してください。

###他の地域でサービスを利用する

ある地域でサービス・インスタンスを作成してアプリにバインドした場合、ユーザー提供のサービスを作成すると、そのサービス・インスタンスを他の地域で利用できます。

サービス・インスタンスを利用する地域で開始すると想定します。他の地域にあるサービス・インスタンスを利用するには、以下のステップを実行します。

1. サービス・インスタンスが存在する地域に切り替えます。{{site.data.keyword.Bluemix_notm}} の上部メニュー・バーで、**「地域」**を展開するか、または**「地域」**アイコンをクリックしてから、 サービス・インスタンスの存在する地域を選択します。

2. Retrieve the credentials and the connection parameters from the VCAP_SERVICES environment variable of the service instance in the region where the service exists. 以下のステップを実行します。


	1. In the {{site.data.keyword.Bluemix_notm}} Dashboard, click your application tile. The Overview page is displayed.
	2. 左方のナビゲーション・ペインで、**「環境変数」**をクリックします。*VCAP_SERVICES* 環境変数の詳細が、右方のペインに表示されます。
サービス・インスタンスの JSON コンテンツを記録します。

3. サービス・インスタンスを利用する地域に切り替えます。{{site.data.keyword.Bluemix_notm}} の上部メニュー・バーで、**「地域」**を展開するか、または**「地域」**アイコンをクリックして、サービス・インスタンスを利用する地域を選択します。

4. *VCAP_SERVICES* 環境変数から記録した資格情報と接続パラメーターを使用して、ユーザー提供のサービス・インスタンスを作成します。ユーザー提供のサービス・インスタンスを作成する方法について詳しくは、[ユーザー提供のサービス・インスタンスの作成](creating-a-user-provided-service-instance) を参照してください。

5. 以下のコマンドを使用して、ユーザー提供のサービス・インスタンスをアプリにバインドします。

	```
	cf bind-service myapp user-provided_service_instance
	```

# 関連リンク
## 一般 
* [Binding a service by using {{site.data.keyword.Bluemix_notm}} user interface](https://www.ng.bluemix.net/docs/starters/ee.html#ee_bindui)
* [VCAP_SERVICES の取得](https://www.ng.bluemix.net/docs/cli/retrieving.html)


