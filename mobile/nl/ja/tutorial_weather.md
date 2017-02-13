---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# チュートリアル - Weather コード・スターター
{: #tutorial_weather}

{{site.data.keyword.Bluemix}} モバイルの Weather コード・スターターは、気象に関する作業を開始するためのスキャフォールド・プロジェクトを示します。これは、Swift を使用し、Push (プッシュ) および Analytics (分析) 統合ポイントを含んでいます。


## 必要条件
{: #tutorial_requirements}

* [Bluemix ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net "外部リンク・アイコン") アカウント
* [Bluemix カタログ![外部リンク・アイコン](../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/ "外部リンク・アイコン")から取得する [Weather Company Data ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.{DomainName}/catalog/services/weather-company-data/ "外部リンク・アイコン")サービス・インスタンス


## 開始
{: #tutorial_gs}

Weather コード・スターターを使用して素早く稼働中にするには、以下のステップに従ってください。

1. {{site.data.keyword.Bluemix_notm}} でモバイル・ダッシュボード・プロジェクトを作成します。

   1. モバイル・ダッシュボードの**「開始」**ページで**「プロジェクトの作成」**をクリックします。

      代替方法として、**「プロジェクト」**ページから**「新規プロジェクト」**をクリックすることもできます。

   2. **「コード・スターター (Code Starters)」**をクリックします。

   3. **「Weather」**を選択し、**「プロジェクトの作成」**をクリックします。

   4. プロジェクト名を入力し、**「作成」**をクリックします。

2. オプション: {{site.data.keyword.mobilepushshort}} 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」**ページで**「{{site.data.keyword.mobilepushshort}}」**に対して**「追加」**をクリックします。

      代替方法として、**「{{site.data.keyword.mobilepushshort}}」**ページから**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。

   3. iOS の場合、[Apple Push Notification Service を構成します![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobilepush/t_push_provider_ios.html "外部リンク・アイコン"){: new_window}。

   4. Android の場合、[Google Cloud Messaging を構成します![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobilepush/t_push_provider_android.html "外部リンク・アイコン"){: new_window}。
   
3. オプション: Analytics (分析) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」** ページで、**「Analytics (分析)」**に対して**「追加」**をクリックします。

      代替方法として、**「Analytics (分析)」**ページから**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。
   
   3. アプリを実行した後、**「デモ・モード」**をオフに切り替えて、分析データを確認できます。

   4. Analytics の構成について詳しくは、[「{{site.data.keyword.mobileanalytics_short}} 概説」![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileanalytics/index.html "外部リンク・アイコン"){: new_window}を参照してください。

4. オプション: Authentication (認証) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」** ページで、**「Authentication (認証)」**に対して**「追加」**をクリックします。

      代替方法として、**「Authentication (認証)」**ページから**「作成」**を選択することもできます。

   2. サービス名を入力し、**「作成」**をクリックします。
   
   3. **「Authentication (認証)」**をオンに切り替えます。
   
   4. ID プロバイダーを選択し、必要な情報を入力して構成します。ID プロバイダーは 1 つだけ有効にすることができます。

   5. 認証の構成について詳しくは、[「Mobile Client Access 概説」![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileaccess/index.html "外部リンク・アイコン"){: new_window}を参照してください。

5. プロジェクトをダウンロードします。

   1. **「コード」**をクリックし、優先言語を選択します。

   2. **「コードのダウンロード (Download Code)」**をクリックします。

5. アーカイブを解凍して、`README.md` ファイル内の指示に従います。


## 次のタスク
{: #tutorial_next}

[試してみてください![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399 "外部リンク・アイコン"){: new_window}


### UI スターターのチュートリアル
{: #tutorials_UI}

* [チュートリアル - Store Catalog](tutorial_store_catalog.html)


### コード・スターターのチュートリアル
{: #tutorials_Code}

* [チュートリアル - ベーシック](tutorial.html)
* [チュートリアル - Cloudant Sync](tutorial_cloudant_synd.html)
* [チュートリアル - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [チュートリアル - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [チュートリアル - Watson Language](tutorial_watson_language.html)
