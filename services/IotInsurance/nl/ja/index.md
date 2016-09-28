---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# {{site.data.keyword.iotinsurance_short}} (ベータ) 概説
{: #iotins_gettingstarted}
最終更新日: 2016 年 9 月 12 日
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} は、接続された保険契約者からデータを収集、管理、および分析するために使用できる {{site.data.keyword.Bluemix_notm}} サービスです。{{site.data.keyword.iotinsurance_short}} により、パーソナライズされたリスク評価、リアルタイムの保護、および保険契約関連コストの削減が実現します。
{:shortdesc}

このサービスを稼働させるには、必要なサービスとアプリをデプロイし、サービスを構成する必要があります。

**前提条件:** 始めに、以下の前提条件が満たされていることを確認します。
- [{{site.data.keyword.iotinsurance_short}} サービス](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/)のインスタンスは、{{site.data.keyword.Bluemix_notm}} スペースにある必要があります。
- 少なくとも 10 GB のストレージがコンピューターで使用可能である必要があります。

## 必須のサービスとアプリケーションのデプロイ
{: #deploying_services}

1. 必要なすべてのサービスとアプリケーションをデプロイするには、{{site.data.keyword.Bluemix_notm}} ダッシュボードで、{{site.data.keyword.iotinsurance_short}} サービス・タイルをクリックし、**「デプロイ (Deploy)」**をクリックします。

  {{site.data.keyword.iotinsurance_short}} は、必要なすべてのサービスと Node.js アプリケーションをデプロイします。これにより、アプリケーションが自動的にサービスにバインドされます。

  各サービス・インスタンスは、デフォルトのサービス・プランを使用します。サービスのコンソールに移動して、後からサービス・プランをアップグレードすることができます。新規インスタンスを削除して既存のインスタンスを {{site.data.keyword.iotinsurance_short}} サービスに手動でバインドすることにより、サービスの既存のインスタンスを使用することもできます。アプリケーションについて詳しくは、[{{site.data.keyword.iotinsurance_short}} について](iotinsurance_overview.html)を参照してください。

2. すべてのサービスとアプリが作成され、適切に機能していることを確認します。{{site.data.keyword.Bluemix_notm}} ダッシュボードで、すべてのアプリの状況が`「実行中」`になっていることを確認します。

3. {{site.data.keyword.iotinsurance_short}} ダッシュボードが機能していること、および API にアクセスできることを確認します。
  1. {{site.data.keyword.iotinsurance_short}} サービス・タイルをクリックし、**「サービス資格情報」**タブを選択します。
  2. **「サービス資格情報の表示 (View Service Credentials)」**をクリックし、ユーザー ID とパスワードをメモします。これらの資格情報は、以下のステップで使用します。
  3. **「管理」**タブを選択して**「開く (Open)」**をクリックし、{{site.data.keyword.iotinsurance_short}} ダッシュボードを開きます。
  4. **「API」**をクリックして、API を表示します。

## サービスの構成
{: #iot4i_configservices}
サービスを構成するには、以下のタスクを実行します。

### {{site.data.keyword.amashort}} の構成
{: #config_ama}
1. {{site.data.keyword.iotinsurance_short}} API アプリケーションの基本 URL を識別します。この URL は、アプリケーション・タイルに *appName*-api.mybluemix.net という形式で表示されます。

2. {{site.data.keyword.amashort}} サービスを開きます。

3. **「カスタム」**セクションで、**「構成 (Configure)」**をクリックし、以下の認証資格情報を入力します。

  - **レルム名 (Realm name)**: `IoT4I`

  - **カスタム ID プロバイダー URL (Custom Identity Provider Url)**: 次の形式のAPI アプリケーションの URL:
  ```
  https://appName-api.mybluemix.net
  ```

  - **Web アプリケーション・リダイレクト URI (Your Web Application Redirect URIs)**: このフィールドはブランクのままにします。

### {{site.data.keyword.mobilepushshort}} の構成
{: #config_push}
既存のモバイル・アプリのプッシュ通知を有効にするには、{{site.data.keyword.mobilepushshort}} サービスを構成し、Public Key Cryptography Standards (PKCS) 12 ファイルを追加する必要があります。モバイル・アプリについて詳しくは、[サンプル・モバイル・アプリのインストールと接続](iotinsurance_mobile_app.html)を参照してください。{{site.data.keyword.mobilepushshort}} について詳しくは、[プッシュ通知の概説](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html)を参照してください。

  1. {{site.data.keyword.mobilepushshort}} サービスを開きます。
  2. **「プッシュのセットアップ (Setup Push)」**をクリックします。
  3. 「Apple プッシュ通知証明書 (Apple Push Notifications Certificate)」セクションで、モバイル・アプリの PKCS 12 ファイルをアップロードし、パスワードを入力します。

次のステップ
{: #whats_next}
{{site.data.keyword.iotinsurance_short}} で何ができるかについて学びます。

- [ユーザーとシールド関連付け](iotinsurance_create_users.html)の作成
- [サンプル・モバイル・アプリ](iotinsurance_mobile_app.html)のインストールと接続
- [拡張サービス](iotinsurance_advancedservices.html)を使用したパフォーマンスの改善
- [API](https://iot4i-docs-api.mybluemix.net/dist/) の表示

# 関連リンク
{: #rellinks}

## チュートリアルとサンプル
{: #samples}
* [Github のサンプル・モバイル・アプリ・コード](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API リファレンス
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API サンプル](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## 関連リンク
{: #general}
* [{{site.data.keyword.iot_full}} 資料](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [開発者サポート・フォーラム](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow サポート・フォーラム](http://stackoverflow.com/questions/tagged/ibm-bluemix)
