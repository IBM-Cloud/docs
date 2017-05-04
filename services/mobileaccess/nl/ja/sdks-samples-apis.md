---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**重要: {{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービス**に置き換えられます。

# {{site.data.keyword.amashort}} SDK、サンプル、および API リファレンス
{{site.data.keyword.amafull}} SDK をクライアント・アプリに追加するには、使用する SDK を選択します。次に、それらの SDK をアプリにプルするように依存関係マネージャーを構成します。
{:shortdesc}

**注:** 以降のセクションに、SDK のインストールについての追加情報があります。

## Core SDK
{: #coresdk}

Core SDK には、カスタム認証およびロギングを使用可能にするための API が含まれています。

### Android
{: #coresdk-android}

[GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}

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

[GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security){: new_window}

#### CocoaPods を使用した Core SDK のインストール
{: #coresdk-ios-siwft-cocoapods}
Podfile を編集して、必要なターゲットに以下の行を追加し、実行します。

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}


### Cordova
{: #coresdk-cordova}

[GitHub リポジトリーおよび API リファレンス![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Cordova CLI を使用した Core SDK のインストール
{: #coresdk-cordova-cli}

Mobile Client Access Cordova プラグインをインストールします。
```Bash
cordova plugin add bms-core
```
{: codeblock}

## Facebook 認証用の Client SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication){: new_window}

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

[GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication){: new_window}

#### CocoaPods を使用した Facebook SDK のインストール
{: #facebooksdk-ios-swift-cocoapods}

Podfile を編集して、必要なターゲットに以下を追加し、実行します。
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}


### Cordova
{: #facebooksdk-cordova}

[GitHub リポジトリーおよび API リファレンス![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

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

[GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication){: new_window}


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

[GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication){: new_window}

#### CocoaPods を使用した Google+ SDK のインストール
{: #googlesdk-ios-swift-cocoapods}

Podfile を編集して以下を追加し、実行します。

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}


### Cordova
{: #googlesdk-cordova}

[GitHub リポジトリーおよび API リファレンス![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Cordova CLI を使用した Google+ SDK のインストール
{: #googlesdk-cordova-cli}

プラグインをインストールします。

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Server SDK for Node.js サーバー
{: #serversdk}

[GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy){: new_window}

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

[GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk){: new_window}

#### npm を使用した OAuth SDK のインストール
{: #oauthsdk}

NPM を実行して SDK をインストールします。
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## カスタム ID プロバイダーのサンプル
{: #customidprovider}

[簡単なサンプル GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}

[高度なサンプル GitHub リポジトリー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}
