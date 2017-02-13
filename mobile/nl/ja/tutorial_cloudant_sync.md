---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloudant Sync コード・スターターのエンドツーエンド・チュートリアル
{: #tutorial}

以下のエンドツーエンド・チュートリアルでは、インストールしておく必要があるツールを含め、Cloudant Sync コード・スターターからプロジェクトを作成するための手順を段階的に説明し、その後に、Android Studio でのスターターの実行手順を説明します。


### 開発者ツールのインストール
{: #dev_tools}

[前提条件の開発者ツール![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](get_code.html#prereq-dev-tools "外部リンク・アイコン"){: new_window}をインストール済みであることを確認します。


### Cloudant Sync コード・スターターからのプロジェクトの作成
{: #create_project}

1. {{site.data.keyword.Bluemix}} でモバイル・ダッシュボード・プロジェクトを作成します。

   1. モバイル・ダッシュボードの**「開始」**ページで**「プロジェクトの作成」**をクリックします。

      代替方法として、**「プロジェクト」**ページから**「プロジェクトの作成」**をクリックすることもできます。

   2. **「コード・スターター (Code Starters)」**をクリックします。

   3. **「Cloudant Sync」**を選択し、**「プロジェクトの作成」**をクリックします。

   4. プロジェクト名を入力します。このチュートリアルでは、`CloudantSyncProject` を使用します。
   
   5. **「作成」**をクリックします。

2. Data (データ) 機能を追加します。新しい {{site.data.keyword.cloudant}} サービス・インスタンスを作成するか、既存のサービス・インスタンスを追加できます。

   1. **「プロジェクト概要 (Project Overview)」**ページの**「データ (Data)」**タイルで**「表示」**をクリックします。

      代替方法として、**「作成」**または**「既存の追加 (Add Existing)」**をクリックし、**「データ (Data)」**ページで**「Cloudant NoSQL DB」**をクリックすることもできます。
      
   2. オプション: 新しいサービス・インスタンスを作成することを選択した場合は、サービス名を入力し、**「作成」**をクリックします。

   3. オプション: 既存のサービス・インスタンスを追加することを選択した場合は、リストからサービス・インスタンスを選択し、**「既存の追加 (Add Existing)」**をクリックします。

   4. サービス・タイル内の**「メニュー」**アイコンをクリックし、**「起動...」**を選択してサービス・インスタンスを起動します。

      1. **「起動 (LAUNCH)」**をクリックして {{site.data.keyword.cloudant}} コンソールを起動します。

      2. **「データベースの作成 (Create Database)」**をクリックし、データベース名を入力し、**「作成」**をクリックします。

      3. **「すべての文書 (All Documents)」**の横の **+** アイコンをクリックして、文書を追加します。

3. オプション: {{site.data.keyword.mobilepushshort}} 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」**ページで**「{{site.data.keyword.mobilepushshort}}」**に対して**「追加」**をクリックします。

      代替方法として、**「{{site.data.keyword.mobilepushshort}}」**ページから**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。

   3. Android の場合、[Firebase Cloud Messaging を構成します![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobilepush/t_push_provider_android.html "外部リンク・アイコン"){: new_window}。
   
4. オプション: Analytics (分析) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」** ページで、**「Analytics (分析)」**に対して**「追加」**をクリックします。

      代替方法として、**「Analytics (分析)」**ページから**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。
   
   3. アプリを実行した後、**「デモ・モード」**をオフに切り替えて、分析データを確認できます。
   
   4. Analytics の構成について詳しくは、[「{{site.data.keyword.mobileanalytics_short}} 概説」![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileanalytics/index.html "外部リンク・アイコン"){: new_window}を参照してください。
  
5. オプション: Authentication (認証) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」** ページで、**「Authentication (認証)」**に対して**「追加」**をクリックします。

      代替方法として、**「Authentication (認証)」**ページから**「作成」**を選択することもできます。

   2. サービス名を入力し、**「作成」**をクリックします。
   
   3. **「Authentication (認証)」**をオンに切り替えます。
   
   4. ID プロバイダーを選択し、必要な情報を入力して構成します。ID プロバイダーは 1 つだけ有効にすることができます。

   5. Authentication (認証) の構成について詳しくは、[「{{site.data.keyword.amashort}} 概説」![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileaccess/index.html "外部リンク・アイコン"){: new_window}を参照してください。

6. プロジェクト・コードを生成します。

   1. **「プロジェクト概要 (Project Overview)」 **ページで**「コードの取得」**をクリックして、プラットフォームと言語を選択します。
   
      代替方法として、**「コード」**ページで以下をクリックすることもできます。
      
   2. Android の場合、**「Android」**をクリックします。
   
   3. プロジェクト・コードの生成が完了したら、**「コードのダウンロード」**をクリックして、プロジェクトのアーカイブをダウンロードします。


### Android Studio での Android プロジェクトの実行
{: #run_android}

1. `CloudantSyncProject-Android.zip` ファイルを解凍します。

2. Markdown ビューアーで `README.md` ファイルを開き、プロジェクトを構成します。

   1. Android Studio で `CloudantSyncProject-Android` プロジェクトを開きます。

   2. Cloudant の資格情報を追加します。

      1. **「データ (Data)」**ページから、サービス・タイル内の**「メニュー」**アイコンをクリックし、**「起動...」**を選択してサービス・インスタンスを起動します。

         1. **「起動 (LAUNCH)」**をクリックして {{site.data.keyword.cloudant}} コンソールを起動します。

         2. データベース名をクリックし、**「許可 (Permissions)」**をクリックします。

         3. `res/values/cloudant_credentials.xml` ファイルの `cloudant_dbname` ストリングにデータベース名を入力します。

         4. **「API キーの生成 (Generate API Key)」**をクリックします。

             1. **キー**値をコピーし、`res/values/cloudant_credentials.xml` ファイル内の `cloudant_api_key` ストリングに貼り付けます。

             2. **パスワード**値をコピーし、`res/values/cloudant_credentials.xml` ファイル内の `cloudant_api_password` ストリングに貼り付けます。

             3. **_admin** 権限を選択します。
      
3. アプリを実行します。


## 次のタスク
{: #what_next}

他のチュートリアルを表示します。


### UI スターターのチュートリアル
{: #tutorials_UI}

* [チュートリアル - Store Catalog](tutorial_store_catalog.html)


### コード・スターターのチュートリアル
{: #tutorials_Code}

* [チュートリアル - ベーシック](tutorial.html)
* [チュートリアル - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [チュートリアル - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [チュートリアル - Watson Language](tutorial_watson_language.html)
* [チュートリアル - Weather](tutorial_weather.html)
