---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

# {{site.data.keyword.mobileanalytics_short}} クライアント SDK のインストール
{: #mobileanalytics_sdk}

{{site.data.keyword.mobileanalytics_short}} クライアント SDK は、現在 Android、iOS、WatchOS、Cordova で使用できます。

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
6. これで Android Client SDK がインストールできました。次に、Analytics Client SDK の[インポートと初期設定](sdk.html#initalize-ma-sdk)を実行します。   

## Swift SDK のインストール
{: #installing-sdk-ios}

![CocoaPods 対応](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

{{site.data.keyword.mobileanalytics_full}} SDK によって、モバイル・アプリケーションを装備できるようになります。Swift SDK は iOS および watchOS で使用できます。

### 始める前に
{: #before-you-begin-ios}

Xcode が正しくセットアップされていることを確認します。iOS 開発環境のセットアップ方法について詳しくは、[Apple Developer Web サイト](https://developer.apple.com/support/xcode/)を参照してください。Client SDK Swift Analytics の [Xcode 要件](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements)についてお読みください。

{{site.data.keyword.mobileanalytics_short}} SDK は、Cocoa プロジェクトの依存関係マネージャーである [CocoaPods](https://cocoapods.org/) および [Carthage](https://github.com/Carthage/Carthage#getting-started) で配布されています。CocoaPods および Carthage は、自動的に成果物をリポジトリーからダウンロードし、それらをアプリケーションで使用できるようにします。CocoaPods または Carthage を選択します。

#### CocoaPods
{: #cocoapods}

1. GitHub の [{{site.data.keyword.Bluemix_notm}} Mobile Services Swift SDK の説明](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods)に従い、Cocoapods を使用して `BMSAnalytics` をインストールし、それを Podfile に追加してください。 
	
2. iOS Client SDK をインストールしたら、Analytics Client SDK の[インポートと初期設定](sdk.html#initalize-ma-sdk)を実行します。   

#### Carthage
{: #carthage}

CocoaPods を使用していない場合、[Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) を使用してプロジェクトにフレームワークを追加することができます。

1. GitHub の [Carthage のインストールの説明](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage)に従って、`BMSAnalytics` をインストールしてください。

2. iOS Client SDK をインストールしたら、Analytics Client SDK の[インポートと初期設定](sdk.html#initalize-ma-sdk)を実行します。

## Cordova プラグインのインストール
{: #installing-sdk-cordova}

{{site.data.keyword.mobileanalytics_full}} Cordova プラグイン<!--SDK-->によって、モバイル・アプリケーションを装備できるようになります。 

1. Android と iOS のプラットフォームを、Cordova アプリケーションに追加します。コマンド・ラインから、以下のコマンドのうちの 1 つまたは両方を実行します。

	```Bash
	cordova platform add android
	```
	
	```Bash
	cordova platform add ios
	```
	
2. Android プラットフォームを追加した場合、サポートされる最小限の API レベルを、Cordova アプリケーションの `config.xml` ファイルに追加する必要があります。`config.xml` ファイルを開き、`<platform name="android">` 要素に以下の行を追加します。

	```XML
	<platform name="android">  
  	<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
  </platform>
```
*minSdkVersion* には `15` より大きい値を指定する必要があります。Android SDK 用にサポートされる *targetSdkVersion* を最新の状態に保つ方法については、[Android プラットフォーム・ガイド (Android Platform Guide)](https://cordova.apache.org/docs/en/latest/guide/platforms/android/) を参照してください。

3. iOS オペレーティング・システムを追加した場合、ターゲット宣言で `<platform name="ios">` 要素を更新します。

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  </platform>
```

4. {{site.data.keyword.mobileanalytics_short}} Cordova プラグインをインストールします。

 	```Bash
	cordova plugin add bms-core
	```

5. 以下のコマンドを実行して、プラグインが正常にインストールされたことを確認します。
	```Bash
	cordova plugin list
	```
	
6. これで、Cordova プラグインがインストールされました。次に、Analytics Client SDK の[インポートと初期設定](sdk.html#initalize-ma-sdk)を実行します。

# 関連リンク

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova Plugin Core SDK](https://www.npmjs.com/package/bms-core){: new_window}

## API リファレンス
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
