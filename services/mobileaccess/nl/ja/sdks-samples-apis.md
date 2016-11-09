---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---

{:shortdesc: .shortdesc}


# {{site.data.keyword.amashort}} SDK、サンプル、および API リファレンス
{{site.data.keyword.amafull}} SDK をアプリに追加するには、使用する SDK を選択します。次に、それらの SDK をアプリにプルするように依存関係マネージャーを構成します。
{:shortdesc}

**注:** 以降のセクションに、SDK のインストールについての追加情報があります。

## Core SDK
{: #coresdk}

Core SDK には、モバイル・アプリのカスタム認証、ロギング、およびモニタリングを使用可能にするための API が含まれています。

### Android
{: #coresdk-android}

[GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Gradle を使用した Core SDK のインストール
{: #coresdk-android-gradle}

アプリの `build.gradle` ファイルにコンパイル依存関係を追加します。

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
    	name:'core',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift SDK)
{: #coresdk-ios-swift}

[GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### CocoaPods を使用した Core SDK のインストール
{: #coresdk-ios-siwft-cocoapods}
Podfile を編集して、必要なターゲットに以下の行を追加し、実行します。

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}

### iOS (Objective-C SDK)
{: #coresdk-ios}

Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix_notm}} モバイル・サービス用の主要 SDK とされていますが、今年後半には廃止され、新しい Swift SDK が後継になる予定です ([iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html) を参照してください)。

[Git リポジトリー](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### CocoaPods を使用した Core SDK のインストール
{: #coresdk-ios-cocoapods}

Podfile を編集して、必要なターゲットに以下の行を追加し、実行します。
```Bash
pod 'IMFCore'
```
{: codeblock}

### Cordova
{: #coresdk-cordova}

[GitHub リポジトリーおよび API リファレンス](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI を使用した Core SDK のインストール
{: #coresdk-cordova-cli}

Mobile Client Access Cordova プラグインをインストールします。
```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Facebook 認証用の Client SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Gradle を使用した Facebook SDK のインストール
{: #facebooksdk-android-gradle}

アプリの `build.gradle` ファイルにコンパイル依存関係を追加します。
```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift SDK)
{: #facebooksdk-ios-swift}

[GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### CocoaPods を使用した Facebook SDK のインストール
{: #facebooksdk-ios-swift-cocoapods}

Podfile を編集して、必要なターゲットに以下を追加し、実行します。
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}

### iOS (Objective-C SDK)
{: #facebooksdk-ios}

[Git リポジトリー](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

**注:** Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix_notm}} モバイル・サービス用の主要 SDK とされていますが、この SDK は今年後半には廃止され、新しい Swift SDK が後継になる予定です。新規アプリケーションには Swift SDK を強くお勧めします (『iOS Swift SDK のセットアップ』を参照してください)。
#### CocoaPods を使用した Facebook SDK のインストール
{: #facebooksdk-ios-cocoapods}

Podfile を編集して以下の行を追加し、実行します。

```Bash
pod 'IMFFacebookAuthentication'
```
{: codeblock}

### Cordova
{: #facebooksdk-cordova}

[GitHub リポジトリーおよび API リファレンス](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI を使用した Facebook SDK のインストール
{: #facebooksdk-cordova-cli}

以下のようにして、 Cordova プラグインをインストールします。

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Google 認証用の Client SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Gradle を使用した Google+ SDK のインストール
{: #googlesdk-android-gradle}

アプリの `build.gradle` ファイルにコンパイル依存関係を追加します。

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (Swift SDK)
{: #googlesdk-ios-swift}

[GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### CocoaPods を使用した Google+ SDK のインストール
{: #googlesdk-ios-swift-cocoapods}

Podfile を編集して以下を追加し、実行します。

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}

### iOS (Objective-C SDK - 非推奨)
{: #googlesdk-ios}

[Git リポジトリー](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)、
[API リファレンス](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### CocoaPods を使用した Google+ SDK のインストール
{: #googlesdk-ios-cocoapods}

Podfile を編集して以下の行を追加し、実行します。

```Bash
pod 'IMFGoogleAuthentication'
```
{: codeblock}

### Cordova
{: #googlesdk-cordova}

[GitHub リポジトリーおよび API リファレンス](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI を使用した Google+ SDK のインストール
{: #googlesdk-cordova-cli}

プラグインをインストールします。

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Server SDK for Node.js サーバー
{: #serversdk}

[GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### npm を使用した Server SDK のインストール
{: #serversdk-npm}

NPM を実行して SDK をインストールします。

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## Server SDK for Liberty for Java&trade; サーバー
{: #serverlibertysdk}

[TAI 成果物のダウンロード](https://imf-tai.{DomainName}/public/TAI.zip)

#### Liberty SDK のインストール
{: #libertysdk}

1. `com.ibm.worklight.oauth.tai_1.0.0.jar` ファイルを `$<wlp.user.dir>/extensions/lib` ディレクトリーにコピーします。

  **ヒント:** `$<wlp.user.dir>` は、Liberty for Java ランタイム用のユーザー・ディレクトリーです。デフォルトのディレクトリー名は `usr` です。

1. `OAuthTai-1.0.mf` ディレクトリーを `$<wlp.user.dir>/extension/lib/features` ディレクトリーにコピーします。


## Node.js OAuth SDK
{: #serverlibertysdk-github}

[GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### npm を使用した OAuth SDK のインストール
{: #oauthsdk}

NPM を実行して SDK をインストールします。
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## カスタム ID プロバイダーのサンプル
{: #customidprovider}

[簡単なサンプル GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)

[高度なサンプル GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API リファレンス ](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### CocoaPods を使用した IMFURLProtocol のインストール
{: #IMFURLProtocol-cocoapods}

Podfile を編集して以下の行を追加し、実行します。

```Bash
pod 'IMFURLProtocol'
```
{: codeblock}
