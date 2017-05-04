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

**重要事項：{{site.data.keyword.amafull}} 服務取代為 {{site.data.keyword.appid_full}} 服務。**

# {{site.data.keyword.amashort}} SDK、範例及 API 參考資料


若要將 {{site.data.keyword.amafull}} SDK 新增至用戶端應用程式，請選擇您要使用的 SDK。然後，配置相依關係管理程式將 SDK 取回至應用程式。
{:shortdesc}

**附註：**後續的小節會提供安裝 SDK 的相關資訊。

## 核心 SDK
{: #coresdk}

「核心 SDK」包含用於啟用自訂鑑別和記載的 API。

### Android
{: #coresdk-android}

[GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}

#### 使用 Gradle 安裝核心 SDK
{: #coresdk-android-gradle}

將編譯相依關係新增至應用程式的 `build.gradle` 檔案：

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

[GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security){: new_window}

#### 使用 CocoaPods 安裝核心 SDK
{: #coresdk-ios-siwft-cocoapods}
編輯 Podfile，然後將下行新增至必要目標並執行：

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}


### Cordova
{: #coresdk-cordova}

[GitHub 儲存庫及 API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### 使用 Cordova CLI 安裝核心 SDK
{: #coresdk-cordova-cli}

安裝 Mobile Client Access Cordova 外掛程式：
```Bash
cordova plugin add bms-core
```
{: codeblock}

## 用於 Facebook 鑑別的用戶端 SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication){: new_window}。

#### 使用 Gradle 安裝 Facebook SDK
{: #facebooksdk-android-gradle}

將編譯相依關係新增至應用程式的 `build.gradle` 檔案：
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

[GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication){: new_window}

#### 使用 CocoaPods 安裝 Facebook SDK
{: #facebooksdk-ios-swift-cocoapods}

編輯 Podfile，然後將下行新增至必要目標並執行：
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}


### Cordova
{: #facebooksdk-cordova}

[GitHub 儲存庫及 API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### 使用 Cordova CLI 安裝 Facebook SDK
{: #facebooksdk-cordova-cli}

安裝 Cordova 外掛程式：

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## 用於 Google 鑑別的用戶端 SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication){: new_window}。


#### 使用 Gradle 安裝 Google+ SDK
{: #googlesdk-android-gradle}

將編譯相依關係新增至應用程式的 `build.gradle` 檔案：

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

[GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication){: new_window}

#### 使用 CocoaPods 安裝 Google+ SDK
{: #googlesdk-ios-swift-cocoapods}

編輯 Podfile，然後新增下行並執行：

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}


### Cordova
{: #googlesdk-cordova}

[GitHub 儲存庫及 API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### 使用 Cordova CLI 安裝 Google+ SDK
{: #googlesdk-cordova-cli}

安裝外掛程式：

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## 用於 Node.js 伺服器的伺服器 SDK
{: #serversdk}

[GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy){: new_window}

#### 使用 npm 安裝伺服器 SDK
{: #serversdk-npm}

執行 NPM 來安裝 SDK：

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## 用於 Liberty for Java&trade; 伺服器的伺服器 SDK
{: #serverlibertysdk}

[下載 TAI 構件](https://imf-tai.{DomainName}/public/TAI.zip)

#### 安裝 Liberty SDK
{: #libertysdk}

1. 將 `com.ibm.worklight.oauth.tai_1.0.0.jar` 檔案複製到 `$<wlp.user.dir>/extensions/lib` 目錄。

  **提示：**`$<wlp.user.dir>` 是 Liberty for Java 運行環境的使用者目錄。預設目錄名稱是 `usr`。

1. 將 `OAuthTai-1.0.mf` 目錄複製到 `$<wlp.user.dir>/extension/lib/features` 目錄。


## Node.js OAuth SDK
{: #serverlibertysdk-github}

[GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk){: new_window}

#### 使用 npm 安裝 OAuth SDK
{: #oauthsdk}

執行 NPM 來安裝 SDK：
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## 自訂身分提供者範例
{: #customidprovider}

[簡單範例 GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}

[進階範例 GitHub 儲存庫 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}
