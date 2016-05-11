---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# バインドされたサービスの自動構成
{: #auto_config}

*最終更新日時: 2016 年 3 月 31 日*

さまざまなサービスを Liberty アプリケーションにバインドすることができます。
サービスは開発者の希望によって、コンテナー管理、アプリケーション管理、またはその両方にできます。

アプリケーション管理サービスとは、Liberty からの支援は何もなく、完全にアプリケーションによって管理されるサービスのことです。アプリケーションは、通常、
VCAP_SERVICES を読み取って、バインドされたサービスについての情報を取得し、サービスに直接アクセスします。必要なすべてのクライアント・アクセス・コードをアプリケーションが提供します。Liberty フィーチャーまたは server.xml ファイル構成にはまったく依存しません。このタイプのサービスには Liberty ビルドパックの自動構成は適用されません。

コンテナー管理サービスとは、Liberty ランタイムによって管理されるサービスのことです。バインドされたサービスをアプリケーションが JNDI で検索する場合もあり、
サービスが Liberty 自体によって直接使用される場合もあります。Liberty ビルドパックが VCAP_SERVICES を読み取って、
バインドされたサービスについての情報を取得します。ビルドパックは、各コンテナー管理サービスに 3 つの機能を実行します。

* バインドされたサービス用の[クラウド変数](optionsForPushing.html#accessing_info_of_bound_services)を生成する。
* バインドされたサービスへのアクセスに必要な Liberty フィーチャーおよびクライアント・アクセス・コードをインストールする。
* サービスで要求される server.xml ファイル・スタンザを生成または更新する。

このプロセスは自動構成と呼ばれます。Liberty ビルドパックは、以下のサービス・タイプに対して自動構成を提供します。

* [SQL Database](../../services/SQLDB/index.html#SQLDB)
* ClearDB MySQL Database
* [MySQL](../../services/MySQL/index.html#MySQL)
* ElephantSQL
* [PostgreSQL](../../services/PostgreSQL/index.html#PostgreSQL)
* [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant)
* MongoLab
* [dashDB](../../services/dashDB/index.html#dashDB)
* [Data Cache](../../services/DataCache/index.html#data_cache)
* [Session Cache](../../services/SessionCache/index.html#session_cache)
* [MQ Light](../../services/MQLight/index.html#mqlight010)
* [Monitoring and Analytics](../..//services/monana/index.html#gettingstartedtemplate)
* [Auto-Scaling](../../services/Auto-Scaling/index.html#autoscaling)
* [Single Sign On](../../services/SingleSignOn/index.html#sso_gettingstarted)
* [New Relic](newRelic.html)
* [Dynatrace](dynatrace.html)

前述の通り、一部のサービスは、アプリケーション管理またはコンテナー管理のいずれかにすることができます。Mongo と SQLDB は、そういったサービスの例です。デフォルトでは、
Liberty ビルドパックは、これらのサービスはコンテナー管理であると想定し、これらを自動的に構成します。アプリケーションがサービスを管理するようにしたい場合、services_autoconfig_excludes 環境変数を設定することで、サービスの自動構成をオプトアウトできます。詳しくは、[『サービス自動構成のオプトアウト』](autoConfig.html#opting_out)を参照してください。

## Liberty フィーチャーおよびクライアント・アクセス・コードのインストール
{: #installation_of_liberty_features}

コンテナー管理サービスにバインドする際、サービスによっては、server.xml ファイルの featureManager スタンザでの Liberty フィーチャーの構成が必要な場合もあります。Liberty ビルドパックは featureManager スタンザを更新し、
サポートされている必要なバイナリーをインストールします。
サービスがクライアント・ドライバーの jar を必要とする場合、
jar が Liberty インストール済み環境の既知の場所にダウンロードされます。

詳細については、バインドされたサービスのタイプに関する資料を参照してください。

## server.xml 構成スタンザの生成または更新
{: #generating_or_updating_serverxml}

Bluemix への [Options for Pushing Liberty Applications](optionsForPushing.html#options_for_pushing) に記述されているように、スタンドアロン・アプリケーションをプッシュすると、Liberty ビルドパックは server.xml スタンザを生成します。スタンドアロン・アプリケーションをプッシュし、コンテナー管理サービスにバインドすると、それらのバインドされたサービスに必要な server.xml スタンザが Liberty ビルドパックによって生成されます。

server.xml ファイルを用意し、コンテナー管理サービスにバインドすると、Liberty ビルドパックによって以下が行われます。

* 用意された server.xml ファイルに、バインドされたサービスの構成スタンザが含まれていない場合、バインドされたサービスの構成を生成します。
* 用意された server.xml ファイルに、バインドされたサービスの構成スタンザが含まれている場合、バインドされたサービスの構成を更新します。

詳細については、バインドされたサービスのタイプに関する資料を参照してください。

## サービス自動構成のオプトアウト
{: #opting_out}

場合によっては、
バインドしたサービスを Liberty ビルドパックが自動的に構成するのが望ましくないことがあります。次のようなシナリオが考えられます。

* 自分のアプリケーションが MongoDB を使用している場合に、このアプリケーションでデータベースへの接続を直接管理したい。ア
プリケーションには、必要なクライアント・ドライバー jar が含まれている。Liberty ビルドパックによる Mongo サービスの自動構成を望まない。
* server.xml ファイルを用意しているところであり、非標準データ・ソース構成が必要なため、SQLDB インスタンス用の構成スタンザを作成した。この server.xml ファイルを、Liberty ビルドパックによって更新されないようにしたいが、Liberty ビルドパックによって、サポートされている適切なソフトウェアが確実にインストールされるようにもしたい。

自動サービス構成をオプトアウトするには、
services_autoconfig_excludes 環境変数を使用します。この環境変数を manifest.yml に組み込むか、または、cf クライアントを使用してこの環境変数を設定することができます。

サービス・タイプごとにサービスの自動構成をオプトアウトすることができます。
完全にオプトアウトする (上の Mongo シナリオ) か、または server.xml ファイル構成の更新のみをオプトアウトする (上の SQLDB シナリオ) ことを選択できます。services_autoconfig_excludes 環境変数に指定する値は、以下に示すようにストリングになります。

* このストリングは、1 つ以上のサービスのオプトアウト指定を含むことができます。
* 具体的なサービスのオプトアウト指定は、service_type=option で、それぞれの意味は次のとおりです。
  * service_type は、VCAP_SERVICES に表示される、サービスのラベルです。
  * option は、all または config のいずれかです。
* このストリングが複数のサービスのオプトアウト指定を含む場合、
個々のオプトアウト指定を 1 個の空白文字で区切る必要があります。

より正式に表すと、このストリングの文法は以下のようになります。

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*

    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type (service label as it appears in VCAP_SERVICES)
    <option> :: all | config
    <delimiter> :: one white space character
```
{: #codeblock}

**重要**: 指定するサービス・タイプは、VCAP_SERVICES 環境変数内で表示されるサービス・ラベルと一致しなければなりません。空白文字は使用できません。**重要**: <service_type_specification> 内に空白文字を含めることはできません。空白文字の使用が許可されるのは、
複数の <service_type_specification> インスタンスを区切る場合のみです。

上記の Mongo シナリオのように、特定のサービスに対するすべての自動構成アクションをオプトアウトするには、「all」オプションを使用します。上記の SQLDB シナリオのように、構成の更新アクションのみをオプトアウトするには、「config」オプションを使用します。

以下に、Mongo シナリオと SQLDB シナリオの manifest.yml ファイル内のオプトアウト指定の例を示します。

```
    env:
      services_autoconfig_excludes: mongodb-2.2=all

    env:
      services_autoconfig_excludes: sqldb=config

    env:
      services_autoconfig_excludes: sqldb=config mongodb-2.2=all
```
{: #codeblock}

以下の例は、
コマンド・ライン・インターフェースを使用して、アプリケーションの myapp の services_autoconfig_excludes 環境変数を設定する方法を示します。

```
    $ cf set-env myapp services_autoconfig_excludes sqldb=config
    $ cf set-env myapp services_autoconfig_excludes "sqldb=config mongodb-2.2=all"
```
{: #codeblock}

# 関連リンク
## 一般
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
