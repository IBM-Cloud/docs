---

copyright:
  years: 2015,2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.iotrtinsights_full}} 入門
{: #gettingstartedtemplate}
*最終更新日: 2016 年 2 月 11 日*

{{site.data.keyword.iotrtinsights_full}} on Bluemix ({{site.data.keyword.iotrtinsights_short}}) を使用して、モノのインターネット・デバイスからのリアルタイム・データに対して分析を実行し、デバイスの正常性や全体的な運用状態に関する洞察を得ることができます。
{:shortdesc}

{{site.data.keyword.iotrtinsights_short}} の使用を開始するには、その前に、分析エンジンをデバイスに接続するように {{site.data.keyword.iot_full}} サービス ({{site.data.keyword.iot_short}}) をセットアップする必要があります。既存の {{site.data.keyword.iot_short}} サービスを使用することも、新規サービスを作成することもできます。迅速に稼働を開始するために、モノのインターネット電話アプリケーションおよび関連 {{site.data.keyword.iot_short}} サービスを組織にデプロイできます。

迅速にこのサービスの稼働を開始するには、以下のステップに従います。
1. {{site.data.keyword.iotrtinsights_short}} サービスを Bluemix 組織にデプロイします。
  1. Bluemix アカウントの「ダッシュボード」で、**「サービスまたは API の使用」**をクリックします。
  2. サービス・カタログの「モノのインターネット」セクションを見つけ、**「{{site.data.keyword.iotrtinsights_short}}」**を選択します。
  3. 「{{site.data.keyword.iotrtinsights_short}}」ページで、「サービスの追加」の選択項目を確認します。  
    - スペース - {{site.data.keyword.iot_short}} サービスをデプロイしたのと同じスペースにサービスをデプロイすることを確認します。
    - アプリ - アンバインドのままにします。
    - サービス名 - オプションとして、覚えやすい名前にサービス名を変更します。この名前は、Bluemix ダッシュボードの IoT {{site.data.keyword.iotrtinsights_short}} タイルで表示されます。
    - 選択済みプラン - ニーズに合わせて、「無料」または購入プランを選択します。  
    > **重要:** {{site.data.keyword.iotrtinsights_short}} の無料プランでは、1 組織ごとにデプロイできるサービス・インスタンスは 1 つに限られます。
  4. **「使用」**をクリックして、{{site.data.keyword.iotrtinsights_short}} を Bluemix サービスにデプロイします。
2. オプション: IoT {{site.data.keyword.iotrtinsights_short}} での IoT デバイスとして、ご使用の電話を使用します。
モノのインターネット電話アプリケーションを使用して、{{site.data.keyword.iotrtinsights_short}} 環境を確認してデータに対するリアルタイム分析の定義を開始するために使用できる IoT デバイスとして機能するように、ご使用のスマートフォンを迅速にセットアップします。モノのインターネット電話アプリケーションについて詳しくは、[モノのインターネット電話アプリケーション](https://github.com/ibm-messaging/IoT-html5-phone)のプロジェクトを参照してください。

  アプリケーションを作成し、ご使用の電話を {{site.data.keyword.iot_full}} に接続するには、以下のようにします。
  1. 以下のボタンをクリックして、デプロイメント・プロセスを開始します。
  [![「Bluemix にデプロイ」アイコン](https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "IoT 電話を Bluemix にデプロイ")(images/deploy_to_bluemix.png "「Bluemix にデプロイ」アイコン")]  
  > **注:** モノのインターネット電話アプリケーションをデプロイすると、電話アプリケーションに自動的にバインドされる {{site.data.keyword.iot_short}} サービス (*iot-phone-iotf-service*) もデプロイされます。モノのインターネット電話アプリケーションをテストするためのデータ・ソースとしてこの {{site.data.keyword.iot_short}} を追加します。また、アプリケーションで使用される Cloudant NoSQL DB サービス (*iot-phone-cloudant-cloudantNoSQLDB*) も作成されます。

  2. IBM Single Sign On サービスのアクセスを自己承認するように求めるプロンプトが出されたら (OAuth 同意)、**「承認 (Approve)」**をクリックします。  
  >**ヒント:** Bluemix アカウントがない場合は、登録して無料 Bluemix トライアルをアクティブ化できます。
  2. 「アプリ名」フィールドを覚えやすいものに変更します。ここでの残りの説明では、これを「*phone application*」と呼びます。この名前は、Bluemix ダッシュボード内のアプリケーション・タイルに表示され、電話を {{site.data.keyword.iot_short}} に接続する際に使用する URL の一部になります。
  2. **「デプロイ (Deploy)」**をクリックします。
  2. デプロイメント・プロセスが完了し、「完了 (Success)」メッセージが表示されたら、Bluemix ダッシュボードに戻ります。
  *phone application* タイルおよび *iot-phone-iotf-service* タイルがアカウントに追加されています。
  1. Bluemix ダッシュボードで、*phone application* タイルをクリックします。
  2. ご使用の電話でブラウザーを開き、アプリケーション名の下に表示されている経路 URL にアクセスします。プロンプトが出されたら、{{site.data.keyword.iot_short}} および IoT {{site.data.keyword.iotrtinsights_short}}ダッシュボードでのデバイスとしてご使用の電話を識別する任意のデバイス ID を入力します。
  3. **「接続 (Connect)」**をクリックして、電話を {{site.data.keyword.iot_short}} *iot-phone-iotf-service* に接続します。
  ビューが最新表示され、電話から {{site.data.keyword.iot_short}} に送信されたデータが表示されます。
2. 「モノのインターネット」サービスを作成して構成します。  
> **ヒント:** モノのインターネット電話アプリケーションをデプロイした場合、*iot-phone-iotf-service* は既に作成済みなので、このステップをスキップできます。  

  1. Bluemix 組織にログインし、IoT {{site.data.keyword.iotrtinsights_short}} をデプロイするスペースを選択します。
  2. Bluemix ダッシュボードで、**「サービスまたは API の使用」**をクリックします。
  3. サービス・カタログの「モノのインターネット」セクションを見つけ、**「モノのインターネット」**を選択します。
  4. 「{{site.data.keyword.iot_full}}」ページで「サービスの追加」の選択項目を確認し、**「使用」**をクリックして {{site.data.keyword.iot_short}} を Bluemix サービスに追加します。
  {{site.data.keyword.iot_short}} サービスがデプロイされると、サービス管理ページが表示されます。
3. 接続 API キーを見つけます。
新規 {{site.data.keyword.iot_short}} サービスを作成した場合は、ここで 2 つのサービスに接続するための API キーを作成する必要があります。既存のサービスを使用している場合は、既存のキーを使用できます。  
  1. Bluemix ダッシュボードで、「モノのインターネット」タイルをクリックします。  
  >**注:** モノのインターネット電話アプリケーションを使用している場合、*iot-phone-iotf-service* タイルをクリックします。  

  1. **「ダッシュボードの起動 (Launch dashboard)」**をクリックして、{{site.data.keyword.iot_full}} ダッシュボードを開きます。
  2. **「アクセス (Access)」>「API キー (API Keys)」**にナビゲートします。
  3. **「API キーの生成 (Generate API Key)」**をクリックします。
  3. API キー、認証トークン、および {{site.data.keyword.iot_short}} ダッシュボードの上部に表示されている組織 ID をメモします。
  IoT {{site.data.keyword.iotrtinsights_short}} でこの情報を使用してサービスを接続します。
4. {{site.data.keyword.iot_short}} サービスと IoT {{site.data.keyword.iotrtinsights_short}} サービスを接続します。
  1. Bluemix ダッシュボードで IoT {{site.data.keyword.iotrtinsights_short}} タイルをクリックします。  
  2. サービス・ページで、**「データ・ソースの追加 (Add a data source)」**をクリックします。
  2. {{site.data.keyword.iotrtinsights_short}} コンソールの「データ・ソースの管理 (Manage Data Sources)」ページで、**「新規データ・ソースの追加 (Add New Data Source)」**をクリックします。
  3. データ・ソースに記述名を付け、前に収集した以下の情報を指定します。
    - 組織 ID
    - API キー
    - 認証トークン
  4. ![「作成」アイコン](images/create.png "「作成」アイコン") をクリックしてデータ・ソースを作成し、それに接続します。
4. {{site.data.keyword.iotrtinsights_short}} の使用を開始します。
これで、ユーザーを追加し、デバイスを接続し、関連するデバイス・データを表示するようにダッシュボードを構成し、アラートをセットアップすることで、{{site.data.keyword.iotrtinsights_short}} の使用を開始できるようになりました。
>**{{site.data.keyword.iotrtinsights_short}} インスタンスの選択:** オペレーターまたは管理者として追加の {{site.data.keyword.iotrtinsights_short}} インスタンスに対するアクセス権限が付与されている場合には、インスタンスを迅速に切り替えることができます。{{site.data.keyword.iotrtinsights_short}} コンソールでユーザー名をクリックし、アクセスするインスタンスを選択します。   

# 関連リンク
## サンプル
* [モノのインターネット電話アプリケーション](https://github.com/ibm-messaging/IoT-html5-phone)
* [developerWorks のモノのインターネットのレシピ](https://developer.ibm.com/recipes/)
* [モノのインターネット・スターター・アプリケーションによるアプリの作成](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## API
* [API 資料](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## 一般
* [製品情報](iotrtinsights_overview.html)   
* [Bluemix サービスの新機能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [{{site.data.keyword.iot_full}} の概要](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [IBM developerWorks 上の dW Answers](https://developer.ibm.com/answers/topics/iot-real-time/)
