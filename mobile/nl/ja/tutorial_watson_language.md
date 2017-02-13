---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# チュートリアル - Watson Language コード・スターター
{: #tutorial_watson_language}

{{site.data.keyword.Bluemix}} モバイルの Watson Language コード・スターターは、Watson の Text to Speech (音声合成) サービスおよび Language Translation (言語翻訳) サービスを示し、各 {{site.data.keyword.Bluemix_notm}} モバイル・サービスの統合ポイントを提供します。


## 必要条件
{: #tutorial_requirements}

* [Bluemix ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net "外部リンク・アイコン") アカウント
* [Bluemix カタログ ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.{DomainName}/catalog/ "外部リンク・アイコン") から取得される [Language Translator ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.{DomainName}/catalog/services/language-translator/ "外部リンク・アイコン")サービス・インスタンスと [Text to Speech ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.{DomainName}/catalog/services/text-to-speech/ "外部リンク・アイコン")サービス・インスタンス。


## 開始
{: #tutorial_gs}

Watson Language コード・スターターを使用して素早く稼働中にするには、以下のステップに従ってください。

1. {{site.data.keyword.Bluemix_notm}} でモバイル・ダッシュボード・プロジェクトを作成します。

   1. モバイル・ダッシュボードの**「開始」**ページで**「プロジェクトの作成」**をクリックします。

      代替方法として、**「プロジェクト」**ページから**「プロジェクトの作成」**をクリックすることもできます。

   2. **「コード・スターター (Code Starters)」**をクリックします。

   3. **「Watson Language」**を選択し、**「プロジェクトの作成」**をクリックします。

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

6. アーカイブを解凍し、`README.md` ファイルを Markdown ビューアーで表示して、セットアップを完了してください。


## 次のタスク
{: #tutorial_next}

[試してみてください![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375 "外部リンク・アイコン"){: new_window}



### UI スターターのチュートリアル
{: #tutorials_UI}

* [チュートリアル - Store Catalog](tutorial_store_catalog.html)


### コード・スターターのチュートリアル
{: #tutorials_Code}

* [チュートリアル - ベーシック](tutorial.html)
* [チュートリアル - Cloudant Sync](tutorial_cloudant_synd.html)
* [チュートリアル - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [チュートリアル - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [チュートリアル - Weather](tutorial_weather.html)

