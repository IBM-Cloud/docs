---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-18"

---

# {{site.data.keyword.mobileanalytics_short}} クライアント SDK のインストール

{: #mobileanalytics_sdk}

最終更新日: 2016 年 10 月 18 日
{: .last-updated}

{{site.data.keyword.mobileanalytics_short}} クライアント SDK は、現在 Android、iOS および WatchOS で使用できます。

{: #shortdesc}

## Android クライアント SDK のインストール
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)(https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)]

{{site.data.keyword.mobileanalytics_short}} クライアント SDK は、Gradle (Android プロジェクト用の依存関係マネージャー) で配布されています。Gradle は自動的に成果物をリポジトリーからダウンロードし、それらを Android アプリケーションで使用できるようにします。

1. [Android Studio](http://developer.android.com/sdk/index.html) プロジェクトを作成するか、既存のプロジェクトを開きます。

2. ご使用の**アプリ・モジュール**にある `build.gradle` ファイルを開きます。

  **ヒント**: ご使用の Android プロジェクトには、プロジェクト用とアプリ・モジュール用の 2 つの `build.gradle` ファイルがある場合があります。必ず**アプリ・モジュール**のファイルを使用してください。

3. `build.gradle` ファイルの `Dependencies` セクションを探し、{{site.data.keyword.mobileanalytics_short}} クライアント SDK のコンパイル依存関係を追加します。リポジトリー・ステートメントは、以下のコード例のようにする必要があります。

	```Gradle
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  ```
  {: codeblock}

4. **「ツール」&gt;「Android」&gt;「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**の順にクリックしてプロジェクトを Gradle と同期します。

5. Android プロジェクト用の `AndroidManifest.xml` ファイルを開きます。このファイルは、**app > manifests** にあります。以下のインターネット・アクセス許可を `<manifest>` 要素の下に追加します。

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
6. これで Android Client SDK がインストールできました。次に、Analytics Client SDK の[インポートおよび初期設定](sdk.html#initalize-ma-sdk-android)を行います。   

## Swift SDK のインストール
{: #installing-sdk-ios}

![CocoaPods 対応](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

{{site.data.keyword.mobileanalytics_full}} SDK によって、モバイル・アプリケーションを装備できるようになります。Swift SDK は iOS および watchOS で使用できます。

### 始める前に
{: #before-you-begin-ios}

Xcode が正しくセットアップされていることを確認します。iOS 開発環境のセットアップ方法について詳しくは、[Apple Developer Web サイト](https://developer.apple.com/support/xcode/)を参照してください。Client SDK Swift Analytics の [Xcode 要件](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements)についてお読みください。

{{site.data.keyword.mobileanalytics_short}} SDK は、Cocoa プロジェクトの依存関係マネージャーである [CocoaPods](https://cocoapods.org/) および [Carthage](https://github.com/Carthage/Carthage#getting-started) で配布されています。CocoaPods および Carthage は、自動的に成果物をリポジトリーからダウンロードし、それらをアプリケーションで使用できるようにします。

#### CocoaPods
{: #cocoapods}

1. CocoaPods がインストールされていない場合は、次のコマンドを実行します:

    ```
sudo gem install cocoapods
    ```
    {: codeblock}
    
    Xcode 8 の場合: `sudo gem install cocoapods --pre`
    
   以下のようにしてローカルの CocoaPods リポジトリーを更新することによって、最新バージョンの `BMSAnalytics` を用意してください。
   
    ```
    pod repo update master
    ```
    {: codeblock}

2. GitHub の [{{site.data.keyword.Bluemix_notm}} Mobile Services Swift SDK の説明](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods)に従ってください。
	
3. iOS Client SDK をインストールしたら、Analytics Client SDK の[インポートおよび初期設定](sdk.html#init-ma-sdk-ios)を行います。   

#### Carthage
{: #carthage}

[Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) を使用してプロジェクトにフレームワークを追加します。

1. GitHub の [Carthage のインストールの説明](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage)に従ってください。

2. iOS Client SDK をインストールしたら、Analytics Client SDK の[インポートおよび初期設定](sdk.html#init-ma-sdk-ios)を行います。

# 関連リンク

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API リファレンス
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
