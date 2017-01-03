---

copyright:
  years: 2016
lastupdated: "2016-11-22"

---
{:new_window: target="_blank"}

# ベーシック・コード・スターターのエンドツーエンド・チュートリアル
{: #tutorial}

以下のエンドツーエンド・チュートリアルでは、インストールしておく必要があるツールを含め、ベーシック・コード・スターターからのプロジェクトの作成手順を段階的に説明し、その後に Xcode と Android Studio でのスターターの実行手順を説明します。


### 開発者ツールのインストール
{: #dev_tools}

[前提条件の開発者ツール](get_code.html#prereq-dev-tools){: new_window}がインストール済みであることを確認してください。


### ベーシック・コード・スターターからのプロジェクトの作成
{: #create_project}

1. {{site.data.keyword.Bluemix}} でモバイル・ダッシュボード・プロジェクトを作成します。

   1. モバイル・ダッシュボードの**「開始」**ページで**「プロジェクトの作成」**をクリックします。

      代替方法として、**「プロジェクト」**ページから**「プロジェクトの作成」**をクリックすることもできます。

   2. **「コード・スターター (Code Starters)」**をクリックします。

   3. **「ベーシック (Basic)」**を選択し、**「プロジェクトの作成」**をクリックします。

   4. プロジェクト名を入力します。このチュートリアルでは、`BasicProject` を使用します。
   
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
   
   4. Analytics (分析) の構成について詳しくは、[{{site.data.keyword.mobileanalytics_short}} 概説](/docs/services/mobileanalytics/index.html){: new_window}を参照してください。
  
4. オプション: Authentication (認証) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」** ページで、**「Authentication (認証)」**に対して**「追加」**をクリックします。

      代替方法として、**「Authentication (認証)」**ページから**「作成」**を選択することもできます。

   2. サービス名を入力し、**「作成」**をクリックします。
   
   3. **「Authentication (認証)」**をオンに切り替えます。
   
   4. ID プロバイダーを選択し、必要な情報を入力して構成します。ID プロバイダーは 1 つだけ有効にすることができます。

   5. Authentication (認証) の構成について詳しくは、[{{site.data.keyword.amashort}} 概説](/docs/services/mobileaccess/index.html){: new_window}を参照してください。

5. プロジェクト・コードを生成します。

   1. **「プロジェクト概要 (Project Overview)」 **ページで**「コードの取得」**をクリックして、プラットフォームと言語を選択します。
   
      代替方法として、**「コード」**ページで以下をクリックすることもできます。
      
   2. Objective-C の場合、**「iOS Obj-C」**をクリックします。

   3. Swift の場合、**「iOS Swift」**をクリックします。
   
   4. Cordova の場合、**「Cordova」**をクリックします。

   5. Android の場合、**「Android」**をクリックします。
   
   6. プロジェクト・コードの生成が完了したら、**「コードのダウンロード」**をクリックして、プロジェクトのアーカイブをダウンロードします。


### Xcode での Objective-C プロジェクトの実行
{: #run_obj-c}

1. `BasicProject-ObjC.zip` ファイルを解凍します。

2. Markdown ビューアーで `README.md` ファイルを開き、プロジェクトを構成する手順を確認します。

   1. ターミナルを開き、プロジェクト・フォルダーに移動します。
   
      1. CocoaPods リポジトリーをセットアップする必要がある場合は、`pod setup` を実行します。
      
      2. 既存の Pods を更新する必要がある場合は、`pod update` を実行します。
      
      3. プロジェクトに必要な Pods をインストールするには、`pod install` を実行します。
      
   2. `BasicProject.xcworkspace` Xcode ワークスペースを開きます。
      
3. アプリを実行します。


### Xcode での Swift プロジェクトの実行
{: #run_swift}

1. `BasicProject-Swift.zip` ファイルを解凍します。

2. Markdown ビューアーで `README.md` ファイルを開き、プロジェクトを構成する手順を確認します。

   1. ターミナルを開き、プロジェクト・フォルダーに移動します。
   
      1. CocoaPods リポジトリーをセットアップする必要がある場合は、`pod setup` を実行します。
      
      2. 既存の Pods を更新する必要がある場合は、`pod update` を実行します。
      
      3. プロジェクトに必要な Pods をインストールするには、`pod install` を実行します。
      
   3. `BasicProject.xcworkspace` Xcode ワークスペースを開きます。
      
3. アプリを実行します。


### Xcode での Cordova プロジェクトの実行
{: #run_cordova_xcode}

1. `BasicProject-Cordova.zip` ファイルを解凍します。

2. Markdown ビューアーで `README.md` ファイルを開き、プロジェクトを構成します。

   1. Xcode で `platforms/ios` プロジェクトを開きます。
      
3. アプリを実行します。


### Android Studio での Cordova プロジェクトの実行
{: #run_cordova_studio}

1. `BasicProject-Cordova.zip` ファイルを解凍します。

2. Markdown ビューアーで `README.md` ファイルを開き、プロジェクトを構成します。

   1. Android Studio で `platforms/android` プロジェクトを開きます。
      
3. アプリを実行します。


### Android Studio での Android プロジェクトの実行
{: #run_android}

1. `BasicProject-Android.zip` ファイルを解凍します。

2. Markdown ビューアーで `README.md` ファイルを開き、プロジェクトを構成します。

   1. Android Studio で `BasicProject-Android` プロジェクトを開きます。
      
3. アプリを実行します。


## 次のタスク
{: #what_next}

他のチュートリアルを表示します。


### UI スターターのチュートリアル
{: #tutorials_UI}

* [チュートリアル - Store Catalog](tutorial_store_catalog.html)


### コード・スターターのチュートリアル
{: #tutorials_Code}

* [チュートリアル - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [チュートリアル - Watson Language](tutorial_watson_language.html)
* [チュートリアル - Weather](tutorial_weather.html)
