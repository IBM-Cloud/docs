---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty アプリケーションのプッシュのオプション
{: #options_for_pushing}

*最終更新日時: 2016 年 3 月 23 日*

Bluemix における Liberty サーバーの動作は、Liberty ビルドパックによって制御されます。 ビルドパックは、特定のクラスのアプリケーションに対して、完全なランタイム環境を提供することができます。また、
クラウド間の移植性を可能にし、また、オープンなクラウド・アーキテクチャーに寄与する上で要となります。Liberty ビルドパックは、
Java EE 7 アプリケーションおよび OSGi アプリケーションを実行することのできる WebSphere Liberty コンテナーを提供します。
また、Spring などの一般的なフレームワークをサポートし、IBM JRE を含んでいます。WebSphere Liberty は素早いアプリケーション開発を可能にし、これはクラウドに適しています。
Liberty ビルドパックは、単一の Liberty サーバーにデプロイされた複数のアプリケーションをサポートします。Bluemix への Liberty ビルドパック統合の一部として、ビルドパックは、サービスをバインドするための環境変数が必ず Liberty サーバー内に構成変数として表示されるようにします。

以下の方法を使用して、Liberty アプリケーションを Bluemix にデプロイできます。

* スタンドアロン・アプリケーションをプッシュする
* サーバー・ディレクトリーをプッシュする
* パッケージされたサーバーをプッシュする

重要: Liberty ビルドパックでアプリケーションをデプロイする際には、アプリケーションのメモリー限度として最小 512M を指定してください。[『メモリー制限および Liberty ビルドパック』](memoryLimits.html)を参照してください。

## スタンドアロン・アプリケーション
{: #stand_alone_apps}

WAR または EAR ファイルなどのスタンドアロン・アプリケーションを Bluemix 内の Liberty にデプロイできます。

スタンドアロン・アプリケーションをデプロイするには、WAR または EAR ファイルをポイントする -p パラメーターを使用して cf push コマンドを実行します。例えば、次のとおりです。

```
    $ cf push <yourappname> -p myapp.war
```
{: #codeblock}

スタンドアロン・アプリケーションがデプロイされるとき、デフォルト Liberty 構成がアプリケーションに提供されます。デフォルト構成では、以下の Liberty フィーチャーが使用可能です。

* beanValidation-1.1
* [cdi-1.2](optionsForPushing.html#cdi12)
* ejbLite-3.2
* el-3.0
* jaxrs-2.0
* jdbc-4.1
* jndi-1.0
* jpa-2.1
* jsf-2.2
* jsonp-1.0
* jsp-2.3
* managedBeans-1.0
* servlet-3.1
* websocket-1.1
* icap:managementConnector-1.0
* appstate-1.0

これらのフィーチャーは、Java EE 7 Web Profile フィーチャーに対応します。JBP_CONFIG_LIBERTY 環境変数を設定することによって、異なる Liberty フィーチャー・セットを指定できます。例えば、
jsp-2.3 フィーチャーと websocket-1.1 フィーチャーのみを使用可能にするには、次のコマンドを実行し、アプリケーションの再ステージングを行います。

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: {features: [jsp-2.3, websocket-1.1]}"
```
{: #codeblock}

注: 最高の結果を得るには、JBP_CONFIG_LIBERTY 環境変数で Liberty フィーチャーを設定するか、または、カスタム server.xml ファイルを使用して、アプリケーションを[サーバー・ディレクトリー](optionsForPushing.html#server_directory)または r [パッケージされたサーバー](optionsForPushing.html#packaged_server)としてデプロイします。この環境変数を設定すると、アプリケーションは必要なフィーチャーのみを使用して、ビルドパックのデフォルト Liberty フィーチャー・セットの変更による影響を受けないことが確実になります。フィーチャー・セット以外にさらに Liberty 構成が必要な場合、
[サーバー・ディレクトリー](optionsForPushing.html#server_directory)または[パッケージされたサーバー](optionsForPushing.html#packaged_server)のオプションを使用してアプリケーションをデプロイします。

WAR ファイルをデプロイした場合、Web アプリケーションは組み込み ibm-web-ext.xml ファイルで設定されたコンテキスト・ルートの下でアクセス可能です。ibm-web-ext.xml ファイルが存在しないか、ファイルにコンテキスト・ルートが指定されていない場合、アプリケーションはルート・コンテキストの下でアクセス可能です。以下に例を示します。


```
    http://<yourappname>.mybluemix.net/
```
{: #codeblock}

EAR ファイルをデプロイした場合、組み込み Web アプリケーションは EAR デプロイメント記述子で定義されたコンテキスト・ルートでアクセス可能です。
以下に例を示します。


```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

デフォルト Liberty server.xml 構成ファイル全体は以下のようになります。
```
    <server>
       <featureManager>
          <feature>beanValidation-1.1</feature>
          <feature>cdi-1.2</feature>
          <feature>ejbLite-3.2</feature>
          <feature>el-3.0</feature>
          <feature>jaxrs-2.0</feature>
          <feature>jdbc-4.1</feature>
          <feature>jndi-1.0</feature>
          <feature>jpa-2.1</feature>
          <feature>jsf-2.2</feature>
          <feature>jsonp-1.0</feature>
          <feature>jsp-2.3</feature>
          <feature>managedBeans-1.0</feature>
          <feature>servlet-3.1</feature>
          <feature>websocket-1.1</feature>
          <feature>icap:managementConnector-1.0</feature>
          <feature>appstate-1.0</feature>
       </featureManager>

       <application name='myapp' location='myapp.war' type='war' context-root='/'/>
       <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='${port}'/>
       <webContainer trustHostHeaderPort='true' extractHostHeaderPort='true'/>
       <include location='runtime-vars.xml'/>
       <logging logDirectory='${application.log.dir}' consoleLogLevel='INFO'/>
       <httpDispatcher enableWelcomePage='false'/>
       <applicationMonitor dropinsEnabled='false' updateTrigger='mbean'/>
       <config updateTrigger='mbean'/>
       <cdi12 enableImplicitBeanArchives='false'/>
       <appstate appName='myapp' markerPath='${home}/../.liberty.state'/>
    </server>
```
{: #codeblock}

### CDI 1.2
{: #cdi12}

パフォーマンス上の理由により、WAR ファイルおよび EAR ファイルのみをデプロイする場合、[CDI 1.2 暗黙的 Bean アーカイブのスキャン](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_cdi_behavior.html)はデフォルトで使用不可になります。暗黙的 Bean アーカイブのスキャンは、JBP_CONFIG_LIBERTY 環境変数を使用して使用可能にすることができます。
例えば、次のとおりです。

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: { implicit_cdi: true }"
```    
{: #codeblock}

重要: 環境変数の変更を有効にするには、次のようにアプリケーションの再ステージングを実行する必要があります。

```
    $ cf restage myapp
```
{: #codeblock}

## サーバー・ディレクトリー
{: #server_directory}

場合によっては、アプリケーションにカスタム Liberty サーバー構成を提供することが必要になることがあります。WAR ファイルまたは EAR ファイルをデプロイして、デフォルト server.xml ファイルにアプリケーションが必要とする特定の設定がない場合に、このカスタム構成が必要になることがあります。

Liberty プロファイルをワークステーションにインストールして、アプリケーションに Liberty サーバーを既に作成済みの場合、そのディレクトリーの内容を Bluemix にプッシュできます。
例えば、Liberty サーバーの名前が defaultServer の場合、次のコマンドを実行します。

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer
```
{: #codeblock}

ワークステーションに Liberty プロファイルがインストールされていない場合、以下の手順を使用して、アプリケーションのサーバー・ディレクトリーを作成できます。

1. defaultServer という名前のディレクトリーを作成します。
2. defaultServer ディレクトリーに apps ディレクトリーを作成します。
3. WAR または EAR ファイルを defaultServer/apps ディレクトリーにコピーします。
4. defaultServer ディレクトリーで、以下のコンテンツ例を使用して server.xml ファイルを作成します。さらに、以下を行います。
  * アプリケーションのファイル名やタイプに一致するように、アプリケーション・エレメントの location または type 属性を必ず更新してください。
  * 図の server.xml ファイルは、最小のフィーチャー・セットを示しています。アプリケーションの必要に応じて、フィーチャー・セットの調整が必要な場合があります。

```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
        </featureManager>

        <httpEndpoint id="defaultHttpEndpoint" host="*" httpPort="8080" />

        <application name="myapp" context-root="/" type="war" location="myapp.war"/>
    </server>
```
{: #codeblock}

サーバー・ディレクトリーの準備ができたら、それを Bluemix にデプロイできます。

```
    $ cf push <yourappname> -p defaultServer
```
{: #codeblock}

注: サーバー・ディレクトリーの一部としてデプロイされた Web アプリケーションは、[Liberty プロファイルで決定されたコンテキスト・ルート](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_dep_war.html?cp=SSAW57_8.5.5%2F1-3-11-0-5-6)からアクセス可能です。例えば、次のとおりです。

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

## パッケージされたサーバー
{: #packaged_server}

パッケージされたサーバー・ファイルを Bluemix にプッシュすることもできます。パッケージされたサーバー・ファイルは、Liberty のサーバー・パッケージ・コマンドを使用して作成されます。アプリケーションと構成ファイルに加えて、パッケージされたサーバー・ファイルも、アプリケーションに必要な共有リソースおよび Liberty ユーザー・フィーチャーを含むことができます。

Liberty サーバーをパッケージするには、Liberty インストール・ディレクトリーから ./bin/server package コマンドを使用します。サーバー名を指定して、'––include=usr' オプションを含めます。例えば、Liberty サーバーが defaultServer の場合、次のコマンドを実行します。

```
    $ wlp/bin/server package defaultServer --include=usr
```
{: #codeblock}

このコマンドはサーバーのディレクトリーに serverName.zip ファイルを生成します。その後 cf push コマンドで圧縮ファイルを Bluemix にプッシュできます。例えば、次のとおりです。

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer/defaultServer.zip
```
{: #codeblock}

注: パッケージされたサーバーの一部としてデプロイされた Web アプリケーションは、 Liberty プロファイルで決定されたコンテキスト・ルートからアクセス可能です。

### server.xml ファイルの変更
{: #modifications_of_serverxml}

パッケージされたサーバーまたは Liberty サーバー・ディレクトリーがプッシュされると、Liberty ビルドパックは、アプリケーションと共に server.xml ファイルを検出します。Liberty ビルドパックは、server.xml ファイルに以下の変更を加えます。

* ビルドパックは、確実に 1 つのみの httpEndpoint エレメントがファイル内にあるようにします。
* ビルドパックは、httpEndpoint エレメント内の httpPort 属性が ${port} という名前のシステム変数をポイントするようにします。ビルドパックはホスト属性のオーバーライドもします。
* ビルドパックは、ロギング・エレメントの logDirectory 属性がシステム・ログ・ディレクトリーをポイントするように設定します。
* ビルドパックは、runtime-vars.xml ファイルが server.xml ファイルと論理的にマージされるようにします。具体的には、ビルドパックは、server.xml ファイルに行 *&lt;include location="runtime-vars.xml" /&gt;* を付加します。

### 参照可能変数
{: #referenceable_variables}

以下の変数は、runtime-vars.xml ファイル内に定義され、プッシュされた server.xml ファイルから参照されます。すべての変数で大/小文字の区別があります。

* ${port}: Liberty サーバーが listen を行う HTTP ポート。
* ${vcap_console_port}: vcap コンソールが稼働しているポート (通常は ${port} と同じ)。
* ${vcap_app_port}: app サーバーが listen を行うポート (通常は ${port} と同じ)。
* ${vcap_console_ip}: vcap コンソールの IP アドレス (通常は Liberty サーバーが listen を行う IP アドレス)。
* ${application_name}: cf push コマンドでオプションを使用して定義された、アプリケーションの名前。
* ${application_version}: アプリケーションのこのインスタンスのバージョン。形式は UUID です (例: b687ea75-49f0-456e-b69d-e36e8a854caa)。この変数は、新規コードを含んでいるか、アプリケーション成果物への変更を含んでいるアプリケーションが次にプッシュされるたびに変更されます。
* ${host}: アプリケーションを実行している DEA の IP アドレス (通常は ${vcap_console_ip} と同じ)。
* ${application_uris}: このアプリケーションにアクセスするために使用できるエンドポイントの JSON スタイルの配列 (例: myapp.mydomain.com)。
* ${start}: アプリケーションが開始した日時。2013-08-22 10:10:18 -0400 のような形式で表されます。

### バインドされたサービスのアクセス情報
{: #accessing_info_of_bound_services}

アプリケーションにサービスをバインドしたい場合、そのサービスについての情報 (接続資格情報など) は [VCAP_SERVICES 環境変数](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html#VCAP-SERVICES)に含まれ、
それを Cloud Foundry がアプリケーション用に設定します。[自動構成されるサービス](autoConfig.html)の場合、
Liberty ビルドパックが server.xml ファイル内のサービス・バインディングのエントリーを生成または更新します。サービス・バインディングのエントリーの内容は、以下のいずれかの形式です。

* cloud.services.&lt;service-name&gt;.&lt;property&gt; は、サービスの名前、タイプ、プランなどの情報を記述します。
* cloud.services.&lt;service-name&gt;.connection.&lt;property&gt; は、サービスの接続情報を記述します。

情報の典型的なセットは、次のとおりです。
* name: サービスの名前。例えば、mysql-e3abd です。label: 作成されたサービスのタイプ。例えば、mysql-5.5 です。
* plan: サービス・プラン。そのプランの固有 ID によって識別されます。例えば、100 です。connection.name: UUID の形式で表される接続の固有 ID。例えば、d01af3a5fabeb4d45bb321fe114d652ee です。
* connection.hostname: サービスを実行しているサーバーのホスト名。例えば、mysql-server.mydomain.com です。
* connection.host: サービスを実行しているサーバーの IP アドレス。例えば、9.37.193.2 です。
* connection.port: サービスが着信接続を listen するポート。例えば、3306,3307 です。
* connection.user: このアプリケーションをサービスに対して認証するために使用されるユーザー名。このユーザー名は Cloud Foundry によって自動生成されます。例えば、unHwANpjAG5wT です。
* connection.username: connection.user の別名。
* connection.password: このアプリケーションをサービスに対して認証するために使用されるパスワード。このパスワードは Cloud Foundry によって自動生成されます。例えば、pvyCY0YzX9pu5 です。

バインドされたサービスが Liberty ビルドパックによって自動構成されないサービスの場合、アプリケーション自体がバックエンド・リソースのアクセスを管理する必要があります。

# 関連リンク
## 一般
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
