---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# {{site.data.keyword.visualrecognitionshort}} コード・スターターのエンドツーエンド・チュートリアル
{: #tutorial}

以下のエンドツーエンド・チュートリアルでは、{{site.data.keyword.visualrecognitionshort}} コード・スターターからプロジェクトを作成するための手順を、インストールされている必要があるツールを含めて説明し、その後に、Xcode および Android Studio でスターターを実行するための手順を説明します。


### 開発者ツールのインストール
{: #dev_tools}

[前提条件の開発者ツール](get_code.html#prereq-dev-tools){: new_window}がインストール済みであることを確認してください。


### {{site.data.keyword.visualrecognitionshort}} コード・スターターからのプロジェクトの作成
{: #create_project}

1. {{site.data.keyword.Bluemix}} 「モバイル」ダッシュボードでプロジェクトを作成します。

   1. 「モバイル」ダッシュボードの**「開始」**ページで**「プロジェクトの作成」**をクリックします。

      代替方法として、**「プロジェクト」**ページから**「プロジェクトの作成」**をクリックすることもできます。

   2. **「コード・スターター (Code Starters)」**をクリックします。

   3. **「Visual Recognition」**を選択し、**「プロジェクトの作成」**をクリックします。

   4. プロジェクト名を入力します。このチュートリアルでは、`VisualRecognitionProject` を使用します。
   
   5. **「作成」**をクリックします。

2. オプション: Push Notifications (プッシュ通知) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」**ページで、**「Push Notifications」**に対して**「追加」**をクリックします。

      代替方法として、**「Push Notifications」**ページから**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。

   3. iOS の場合、[Apple プッシュ通知サービスの構成](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}を行います。

   4. Android の場合、[configure Firebase Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window} を行います。
   
3. オプション: Analytics (分析) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」** ページで、**「Analytics (分析)」**に対して**「追加」**をクリックします。

      代替方法として、**「Analytics (分析)」**ページから**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。
   
   3. アプリを実行した後、**「デモ・モード」**をオフに切り替えて、分析データを確認できます。
   
   4. Analytics (分析) の構成について詳しくは、[Getting started with {{site.data.keyword.mobileanalytics_short}}](/docs/services/mobileanalytics/index.html){: new_window} を参照してください。
  
4. オプション: Authentication (認証) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」** ページで、**「Authentication (認証)」**に対して**「追加」**をクリックします。

      代替方法として、**「Authentication (認証)」**ページから**「作成」**を選択することもできます。

   2. サービス名を入力し、**「作成」**をクリックします。
   
   3. **「Authentication (認証)」**をオンに切り替えます。
   
   4. ID プロバイダーを選択し、必要な情報を入力して構成します。ID プロバイダーは 1 つだけ有効にすることができます。

   5. Authentication (認証) の構成について詳しくは、[Getting started with {{site.data.keyword.amashort}}](/docs/services/mobileaccess/index.html){: new_window} を参照してください。

5. プロジェクト・コードを生成します。

   1. **「プロジェクト概要 (Project Overview)」 **ページで**「コードの取得」**をクリックして、プラットフォームと言語を選択します。
   
      代替方法として、**「コード」**ページで以下をクリックすることもできます。
      
   2. iOS の場合、**「iOS Swift」**をクリックします。
   
   3. Android の場合、**「Android」**をクリックします。
   
   4. プロジェクト・コードの生成が完了したら、**「コードのダウンロード」**をクリックして、プロジェクトのアーカイブをダウンロードします。


### Xcode でのプロジェクトの実行
{: #run_xcode}

1. `VisualRecognitionProject-Swift.zip` ファイルを解凍します。

2. Markdown ビューアーで `README.md` ファイルを開き、プロジェクトを構成する手順を確認します。

   1. [{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window} サービス・インスタンスを作成します。
   
   2. ターミナルを開き、プロジェクト・フォルダーに移動します。
   
      1. CocoaPods リポジトリーをセットアップする必要がある場合は、`pod setup` を実行します。
      
      2. 既存の Pods を更新する必要がある場合は、`pod update` を実行します。
      
      3. プロジェクトに必要な Pods をインストールするには、`pod install` を実行します。
      
      4. {{site.data.keyword.ibmwatson}} Developer Cloud iOS SDK を使用するための依存関係およびフレームワークをビルドするには、`carthage update --platform iOS` を実行します。
      
   3. `VisualRecognitionProject.xcworkspace` Xcode ワークスペースを開きます。
   
   4. {{site.data.keyword.visualrecognitionshort}} サービス資格情報を追加します。
   
      1. {{site.data.keyword.visualrecognition}} サービス資格情報から `api_key` をコピーします。
      
      2. `api_key` を `WatsonCredentials.plist` ファイル内の `VisualRecognitionAPIKey` キーに貼り付けます。
      
3. アプリを実行します。


### Android Studio でのプロジェクトの実行
{: #run_studio}

1. `VisualRecognitionProject-Android.zip` ファイルを解凍します。

2. Markdown ビューアーで `README.md` ファイルを開き、プロジェクトを構成します。

   1. [{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window} サービス・インスタンスを作成します。
   
      {{site.data.keyword.visualrecognitionshort}} サービス・インスタンスが既にある場合は、このステップをスキップしてください。
   
   2. Android Studio で `VisualRecognitionProject-Android` プロジェクトを開きます。
   
   4. {{site.data.keyword.visualrecognitionshort}} サービス資格情報を追加します。
   
      1. {{site.data.keyword.visualrecognition}} サービス資格情報から `api_key` をコピーします。
      
      2. `api_key` を `res/values/watson_credentials.xml` ファイル内の `watson_visual_recognition_api_key` キーに貼り付けます。
      
3. アプリを実行します。


## 次のタスク
{: #what_next}

他のチュートリアルを表示します。


### UI スターターのチュートリアル
{: #tutorials_UI}

* [チュートリアル - Store Catalog](tutorial_store_catalog.html)


### コード・スターターのチュートリアル
{: #tutorials_Code}

* [チュートリアル - Watson Language](tutorial_watson_language.html)
* [チュートリアル - Weather](tutorial_weather.html)
