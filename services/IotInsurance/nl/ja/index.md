---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# {{site.data.keyword.iotinsurance_short}} の概説
{: #gettingstarted}

{{site.data.keyword.iotinsurance_full}} は、接続された保険契約者からデータを収集、管理、および分析するために使用できる {{site.data.keyword.Bluemix_notm}} サービスです。{{site.data.keyword.iotinsurance_short}} により、パーソナライズされたリスク評価、リアルタイムの保護、および保険契約関連コストの削減が実現します。
{:shortdesc}

このサービスを稼働させるには、必要なサービスとアプリをデプロイし、サービスを構成する必要があります。[{{site.data.keyword.iotinsurance_short}} について](iotinsurance_overview.html)に記載されているサービスとアプリの概要、そしてアーキテクチャーの図を参照してください。

**前提条件:** 始めに、以下の前提条件が満たされていることを確認します。
- [{{site.data.keyword.iotinsurance_short}} サービス](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/)のインスタンスは、{{site.data.keyword.Bluemix_notm}} スペースにある必要があります。
- {{site.data.keyword.Bluemix_notm}} 組織でデプロイ機能を実行するには、少なくとも 2 GB の空きメモリーが必要です。以前のバージョンからアップグレードする場合は、少なくとも 2.5 GB 必要です。

## 必須のサービスとアプリケーションのデプロイ
{: #deploying_services}

1. 必要なサービスとアプリケーションのすべてをデプロイするには、[{{site.data.keyword.Bluemix_notm}} コンソール](https://console.ng.bluemix.net/#all-items)において、{{site.data.keyword.iotinsurance_short}} サービスをクリックしてから、**「デプロイ (Deploy)」**をクリックします。

  {{site.data.keyword.iotinsurance_short}} は、必要なすべてのサービスと Node.js アプリケーションをデプロイします。これにより、アプリケーションが自動的にサービスにバインドされます。

  各サービス・インスタンスは、デフォルトのサービス・プランを使用します。サービスのコンソールに移動して、後からサービス・プランをアップグレードすることができます。新規インスタンスを削除して既存のインスタンスを {{site.data.keyword.iotinsurance_short}} サービスに手動でバインドすることにより、サービスの既存のインスタンスを使用することもできます。アプリケーションについて詳しくは、[{{site.data.keyword.iotinsurance_short}} について](iotinsurance_overview.html)を参照してください。

  **重要:** {{site.data.keyword.iotinsurance_short}} の試用版をデプロイする場合、一緒にデプロイされる他のサービスやアプリケーションの無料版については、その機能が制限されていることにご注意ください。{{site.data.keyword.iot_short_notm}} は最大 500 デバイスに制限されており 、{{site.data.keyword.cloudant_short_notm}} は 1 GB のデータに制限され、読み取り/書き込みのスレッド化機能は制限されています。

  **注**: {{site.data.keyword.iotinsurance_short}} は、{{site.data.keyword.amafull}} と {{site.data.keyword.mobilepushfull}} のいずれもデプロイしなくなりました。旧バージョンの {{site.data.keyword.iotinsurance_short}} は、{{site.data.keyword.amashort}} サービスを使用してモバイル・アプリからの応答を処理していました。このプロセスは、既存のすべての {{site.data.keyword.iotinsurance_short}} インスタンスで引き続き機能します。しかし、新規の {{site.data.keyword.iotinsurance_short}} インスタンスでモバイル・アプリを使用するには、カスタムの認証プロセスを作成する必要があります。
またオプションで、[{{site.data.keyword.mobilepushshort}} のインスタンスを作成し](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)、それを構成し、{{site.data.keyword.iotinsurance_short}} API にバインドすることができます。

2. {{site.data.keyword.iotinsurance_short}} ダッシュボードが機能していること、また API にアクセスできることを確認します。
  1. **「開く (Open)」**をクリックして {{site.data.keyword.iotinsurance_short}} ダッシュボードを開きます。**「ログイン (Login)」**をクリックすることにより、事前に入力されている資格情報を受け入れます。
  2. {{site.data.keyword.iotinsurance_short}} サービス・コンソールに戻り、**「API (APIs)」**をクリックして API を表示します。

  **注:** デプロイメントの後は、ダッシュボードまたは API に対応する URL をブラウザーに入力することにより、それらに直接アクセスすることができます。この方法を使用する場合は、{{site.data.keyword.iotinsurance_short}} サービスの資格情報を入力する必要があります。資格情報を見つけるには、{{site.data.keyword.iotinsurance_short}} サービス・コンソールに戻ってください。**「サービス資格情報」**タブをクリックした後、**「資格情報の表示」**をクリックします。ユーザー ID とパスワードをメモしておいてください。


<!--
## Configuring
{: #iot4i_configservices}



### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. Return to your Bluemix console. All apps and services that were deployed by {{site.data.keyword.iotinsurance_short}} are displayed.

2. Copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right-click the API application and select **Copy Link Location**.

3. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

4. Enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in a previous step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

6. Save your settings. You can now return to the {{site.data.keyword.iotinsurance_short}} service console or your {{site.data.keyword.Bluemix_notm}} console.
-->


## {{site.data.keyword.mobilepushshort}} の作成と構成
{: #config_push}

(オプション) 既存のモバイル・アプリのプッシュ通知を有効にするには、オプションで {{site.data.keyword.mobilepushshort}} サービスのインスタンスを作成し、それを {{site.data.keyword.iotinsurance_short}} API にバインドし、Public Key Cryptography Standards (PKCS) 12 ファイルを追加することができます。モバイル・アプリについて詳しくは、[サンプル・モバイル・アプリのインストールと接続](iotinsurance_mobile_app.html)を参照してください。{{site.data.keyword.mobilepushshort}} について詳しくは、[プッシュ通知の概説](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)を参照してください。

このサービスを作成後に構成するには、以下の手順を実行します。

  1. {{site.data.keyword.mobilepushshort}} サービスを開きます。
  2. **「構成 (Configure)」**をクリックします。
  3. 「Apple プッシュ通知証明書 (Apple Push Notifications Certificate)」セクションで、モバイル・アプリの PKCS 12 ファイルをアップロードし、パスワードを入力します。

## Weather Company データの使用
{: #weather_company}

(オプション) {{site.data.keyword.iotinsurance_short}} は、デモンストレーション目的で表示できる Weather Company の一連の静的データを提供します。さらにオプションで、[{{site.data.keyword.weatherfull}} サービス](../Weather/index.html)のインスタンスを作成し、それを {{site.data.keyword.iotinsurance_short}} 天気アプリにバインドすることで、Weather Company のライブ・データにアクセスできます。

**重要:** {{site.data.keyword.weather_short}} サービスの無料版は、10,000 件の要求に制限されています。それ以上の要求を処理する必要がある場合は、有料バージョンにアップグレードすることができます。

次のステップ
{: #whats_next}
{{site.data.keyword.iotinsurance_short}} で何ができるかについて学びます。

- シールド・ツールキットに含まれている指示や API を使用して、[ユーザーとシールド関連付け](iotinsurance_shield_toolkit.html)を作成します。
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- [GitHub サイトの API の例![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window} をすべてダウンロードまたは表示します。
