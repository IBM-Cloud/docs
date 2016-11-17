---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# {{site.data.keyword.iotinsurance_short}} の概説

{{site.data.keyword.iotinsurance_full}} は、接続された保険契約者からデータを収集、管理、および分析するために使用できる {{site.data.keyword.Bluemix_notm}} サービスです。{{site.data.keyword.iotinsurance_short}} により、パーソナライズされたリスク評価、リアルタイムの保護、および保険契約関連コストの削減が実現します。
{:shortdesc}

このサービスを稼働させるには、必要なサービスとアプリをデプロイし、サービスを構成する必要があります。[{{site.data.keyword.iotinsurance_short}} について](iotinsurance_overview.html)に記載されているサービスとアプリの概要、そしてアーキテクチャーの図を参照してください。

**前提条件:** 始めに、以下の前提条件が満たされていることを確認します。
- [{{site.data.keyword.iotinsurance_short}} サービス](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/)のインスタンスは、{{site.data.keyword.Bluemix_notm}} スペースにある必要があります。
- {{site.data.keyword.Bluemix_notm}} 組織でデプロイ機能を実行するには、少なくとも 2 GB の空きメモリーが必要です。

## 必須のサービスとアプリケーションのデプロイ
{: #deploying_services}

1. 必要なサービスとアプリケーションのすべてをデプロイするには、[{{site.data.keyword.Bluemix_notm}} コンソール](https://console.ng.bluemix.net/#all-items)において、{{site.data.keyword.iotinsurance_short}} サービスをクリックしてから、**「デプロイ (Deploy)」**をクリックします。

  {{site.data.keyword.iotinsurance_short}} は、必要なすべてのサービスと Node.js アプリケーションをデプロイします。これにより、アプリケーションが自動的にサービスにバインドされます。

  各サービス・インスタンスは、デフォルトのサービス・プランを使用します。サービスのコンソールに移動して、後からサービス・プランをアップグレードすることができます。新規インスタンスを削除して既存のインスタンスを {{site.data.keyword.iotinsurance_short}} サービスに手動でバインドすることにより、サービスの既存のインスタンスを使用することもできます。アプリケーションについて詳しくは、[{{site.data.keyword.iotinsurance_short}} について](iotinsurance_overview.html)を参照してください。

2. {{site.data.keyword.iotinsurance_short}} ダッシュボードが機能していること、また API にアクセスできることを確認します。
  1. **「開く (Open)」**をクリックして {{site.data.keyword.iotinsurance_short}} ダッシュボードを開きます。**「ログイン (Login)」**をクリックすることにより、事前に入力されている資格情報を受け入れます。
  2. {{site.data.keyword.iotinsurance_short}} サービス・コンソールに戻り、**「API (APIs)」**をクリックして API を表示します。

  **注:** デプロイメントの後は、ダッシュボードまたは API に対応する URL をブラウザーに入力することにより、それらに直接アクセスすることができます。この方法を使用する場合は、{{site.data.keyword.iotinsurance_short}} サービスの資格情報を入力する必要があります。資格情報を見つけるには、{{site.data.keyword.iotinsurance_short}} サービス・コンソールに戻ってください。**「サービス資格情報」**タブをクリックした後、**「資格情報の表示」**をクリックします。ユーザー ID とパスワードをメモしておいてください。

## サービスの構成
{: #iot4i_configservices}
サービスを構成するには、以下のタスクを実行します。

### {{site.data.keyword.amashort}} の構成
{: #config_ama}
1. Bluemix コンソールに戻ります。{{site.data.keyword.iotinsurance_short}} によってデプロイされたすべてのアプリとサービスが表示されます。

1. {{site.data.keyword.iotinsurance_short}} API アプリケーションの URL をコピーします。API アプリケーションを右クリックし、**「リンク・ロケーションのコピー (Copy Link Location)」**を選択します。

2. {{site.data.keyword.amashort}} サービスを開きます。{{site.data.keyword.Bluemix_notm}} コンソールの「サービス」セクションで、そのサービスを利用できるようになります。

3. **「オン」**をクリックすることにより、認証を有効にします。

4. **「カスタム」**セクションで、**「構成 (Configure)」**をクリックし、以下の認証資格情報を入力します。

  - **レルム名 (Realm name)**: `IoT4I`

  - **カスタム ID プロバイダー URL (Custom Identity Provider Url)**: 最初の手順でコピーした API アプリケーションの URL を貼り付けます。

  - **Web アプリケーション・リダイレクト URI (Your Web Application Redirect URIs)**: このフィールドはブランクのままにします。

5. 設定を保存します。これで、{{site.data.keyword.iotinsurance_short}} サービス・コンソール、または {{site.data.keyword.Bluemix_notm}} コンソールに戻ることができます。

### {{site.data.keyword.mobilepushshort}} の構成
{: #config_push}
既存のモバイル・アプリのプッシュ通知を有効にするには、{{site.data.keyword.mobilepushshort}} サービスを構成し、Public Key Cryptography Standards (PKCS) 12 ファイルを追加する必要があります。モバイル・アプリについて詳しくは、[サンプル・モバイル・アプリのインストールと接続](iotinsurance_mobile_app.html)を参照してください。{{site.data.keyword.mobilepushshort}} について詳しくは、[プッシュ通知の概説](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html)を参照してください。

  1. {{site.data.keyword.mobilepushshort}} サービスを開きます。
  2. **「構成 (Configure)」**をクリックします。
  3. 「Apple プッシュ通知証明書 (Apple Push Notifications Certificate)」セクションで、モバイル・アプリの PKCS 12 ファイルをアップロードし、パスワードを入力します。


次のステップ
{: #whats_next}
{{site.data.keyword.iotinsurance_short}} で何ができるかについて学びます。

- シールド・ツールキットに含まれている指示や API を使用して、[ユーザーとシールド関連付け](iotinsurance_shield_toolkit.html)を作成します。
- [サンプル・モバイル・アプリ](iotinsurance_mobile_app.html)のインストールと接続
- [GitHub サイトの API](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples) のすべてのダウンロードまたは表示

# 関連リンク
{: #rellinks}

## チュートリアルとサンプル
{: #samples}
* [GitHub のサンプル・モバイル・アプリ・コード](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API リファレンス
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API サンプル](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}


## 関連リンク
{: #general}
* [{{site.data.keyword.iot_full}} 資料](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [開発者サポート・フォーラム](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow サポート・フォーラム](http://stackoverflow.com/questions/tagged/ibm-bluemix)
