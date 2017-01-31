---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} クライアント SDK のインストール
{: #mobileanalytics_sdk}

{{site.data.keyword.mobileanalytics_short}} クライアント SDK は、現在 Android、iOS、WatchOS、Cordova で使用できます。

{: #shortdesc}

## Android クライアント SDK のインストール
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

{{site.data.keyword.mobileanalytics_short}} クライアント SDK は、Gradle (Android プロジェクト用の依存関係マネージャー) で配布されています。Gradle は自動的に成果物をリポジトリーからダウンロードし、それらを Android アプリケーションで使用できるようにします。

1. [Android Studio ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://developer.android.com/sdk/index.html "外部リンク・アイコン"){: new_window} プロジェクトを作成するか、既存のプロジェクトを開きます。

2. ご使用の**アプリ・モジュール**にある `build.gradle` ファイルを開きます。

  **ヒント**: ご使用の Android プロジェクトには、プロジェクト用とアプリ・モジュール用の 2 つの `build.gradle` ファイルがある場合があります。必ず**アプリ・モジュール**のファイルを使用してください。

3. `build.gradle` ファイルの `Dependencies` セクションを探し、{{site.data.keyword.mobileanalytics_short}} クライアント SDK のコンパイル依存関係を追加します。リポジトリー・ステートメントは、以下のコード例のようにする必要があります。

	```
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  ```
  	{: codeblock}

4. **「ツール」&gt;「Android」&gt;「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**の順にクリックしてプロジェクトを Gradle と同期します。

5. Android プロジェクト用の `AndroidManifest.xml` ファイルを開きます。このファイルは、**app > manifests** にあります。以下のインターネット・アクセス許可を `<manifest>` 要素の下に追加します。

	```
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

Xcode が正しくセットアップされていることを確認します。iOS 開発環境のセットアップ方法について詳しくは、[Apple Developer Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.apple.com/support/xcode/ "外部リンク・アイコン"){: new_window} を参照してください。Client SDK Swift Analytics の [Xcode の要件 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements "外部リンク・アイコン"){: new_window} を参照してください。

{{site.data.keyword.mobileanalytics_short}} SDK は、[CocoaPods ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cocoapods.org/ "外部リンク・アイコン"){: new_window} および [Carthage ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/Carthage/Carthage#getting-started "外部リンク・アイコン"){: new_window} で配布されています。これらは、Cocoa プロジェクト用の依存関係管理プログラムです。CocoaPods および Carthage は、自動的に成果物をリポジトリーからダウンロードし、それらをアプリケーションで使用できるようにします。CocoaPods または Carthage を選択します。

#### CocoaPods
{: #cocoapods}

1. GitHub の [{{site.data.keyword.Bluemix_notm}} Mobile Services Swift SDK の説明 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods "外部リンク・アイコン"){: new_window} に従い、Cocoapods を使用して `BMSAnalytics` をインストールし、それを Podfile に追加します。 
	
2. iOS Client SDK をインストールしたら、Analytics Client SDK の[インポートと初期設定](sdk.html#initalize-ma-sdk)を実行します。   

#### Carthage
{: #carthage}

CocoaPods を使用していない場合、[Carthage ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos "外部リンク・アイコン"){: new_window} を使用してプロジェクトにフレームワークを追加することができます。

1. GitHub の [Carthage のインストールの説明 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage "外部リンク・アイコン"){: new_window} に従い、`BMSAnalytics` をインストールします。

2. iOS Client SDK をインストールしたら、Analytics Client SDK の[インポートと初期設定](sdk.html#initalize-ma-sdk)を実行します。

## Cordova プラグインのインストール
{: #installing-sdk-cordova}

{{site.data.keyword.mobileanalytics_full}} Cordova プラグインによって、モバイル・アプリケーションを装備できるようになります。 

1. [Cordova ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://cordova.apache.org/#getstarted "外部リンク・アイコン"){: new_window} プロジェクトを作成するか、既存のプロジェクトを開きます。

2. Android と iOS のプラットフォームを、Cordova アプリケーションに追加します。コマンド・ラインから、以下のコマンドのいずれかまたは両方を実行します。現在、Cordova-CLI V6.3.0 以前がサポートされています。
   
   Android:

	 ```
	 cordova platform add android@5.2.2
	```
	 {: codeblock}
	
   iOS:
   	
	```
	cordova platform add ios
	```
   {: codeblock}
	
3. Android プラットフォームを追加した場合、サポートされる最小限の API レベルを、Cordova アプリケーションの `config.xml` ファイルに追加する必要があります。`config.xml` ファイルを開き、`<platform name="android">` 要素に以下の行を追加します。

	```
	<platform name="android">  
  	<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
  	</platform>
	```
   {: codeblock}

 *minSdkVersion* の値は、バージョン `15` 以上でなければなりません。Android SDK 用にサポートされる *targetSdkVersion* を最新の状態に保つ方法については、[Android プラットフォーム・ガイド (Android Platform Guide) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/ "外部リンク・アイコン"){: new_window} を参照してください。

4. iOS オペレーティング・システムを追加した場合、ターゲット宣言で `<platform name="ios">` 要素を更新します。

	```
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  	</platform>
	```
	{: codeblock}

5. `bms-core` プラグインを追加します。
 	
	 ```
	 cordova plugin add bms-core
	 ```
	 {: codeblock}

6. 以下のコマンドを実行して、プラグインが正常にインストールされたことを確認します。
	
	```
	cordova plugin list
	```
	{: codeblock}
	
7. [Android および iOS 環境の構成 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.npmjs.com/package/bms-core#4-configuring-your-platform "外部リンク・アイコン"){: new_window} を実行します。

8. これで、Cordova プラグインがインストールされ、環境が構成されました。次に、Analytics Client SDK の[インポートと初期設定](sdk.html#initalize-ma-sdk)を実行します。

# 関連リンク

## SDK
* [Android SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics "外部リンク・アイコン"){: new_window}  
* [iOS SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics "外部リンク・アイコン"){: new_window}
* [Cordova Plugin Core SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.npmjs.com/package/bms-core "外部リンク・アイコン"){: new_window}

## API リファレンス
{: #api}
* [REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "外部リンク・アイコン"){:new_window}
