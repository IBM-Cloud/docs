---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-25"

---
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# {{site.data.keyword.amashort}} SDK、範例及 API 參考資料


若要將 {{site.data.keyword.amafull}} SDK 新增至用戶端應用程式，請選擇您要使用的 SDK。然後，配置相依關係管理程式將 SDK 取回至應用程式。
{:shortdesc}

**附註：**後續的小節會提供安裝 SDK 的相關資訊。

## 核心 SDK
{: #coresdk}

「核心 SDK」包含用於啟用自訂鑑別和記載的 API。

### Android
{: #coresdk-android}

[GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

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

[GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### 使用 CocoaPods 安裝核心 SDK
{: #coresdk-ios-siwft-cocoapods}
編輯 Podfile，然後將下行新增至必要目標並執行：

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}

### iOS (Objective-C SDK)
{: #coresdk-ios}

雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主要 SDK，不過預計在今年稍晚停止使用它，改用新的 Swift SDK（請參閱[設定 iOS Swift SDK](getting-started-ios-swift-sdk.html)）。

[Git 儲存庫](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### 使用 CocoaPods 安裝核心 SDK
{: #coresdk-ios-cocoapods}

編輯 Podfile，然後將下行新增至必要目標並執行：
```Bash
pod 'IMFCore'
```
{: codeblock}

### Cordova
{: #coresdk-cordova}

[GitHub 儲存庫及 API 參考資料](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

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

[GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

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

[GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### 使用 CocoaPods 安裝 Facebook SDK
{: #facebooksdk-ios-swift-cocoapods}

編輯 Podfile，然後將下行新增至必要目標並執行：
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}

### iOS (Objective-C SDK)
{: #facebooksdk-ios}

[Git 儲存庫](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

**附註：**雖然仍然完全支援 Objective-C SDK 且將它視為 {{site.data.keyword.Bluemix_notm}} Mobile Services 的主要 SDK，不過預計在今年稍晚將停止使用此 SDK，改用新的 Swift SDK。對於新的應用程式，強烈建議使用 Swift SDK（請參閱「設定 iOS Swift SDK」）。
#### 使用 CocoaPods 安裝 Facebook SDK
{: #facebooksdk-ios-cocoapods}

編輯 Podfile，然後新增下行並執行：

```Bash
pod 'IMFFacebookAuthentication'
```
{: codeblock}

### Cordova
{: #facebooksdk-cordova}

[GitHub 儲存庫及 API 參考資料](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

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

[GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

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

[GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### 使用 CocoaPods 安裝 Google+ SDK
{: #googlesdk-ios-swift-cocoapods}

編輯 Podfile，然後新增下行並執行：

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}

### iOS（Objective-C SDK - 已淘汰）
{: #googlesdk-ios}

[Git 儲存庫](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### 使用 CocoaPods 安裝 Google+ SDK
{: #googlesdk-ios-cocoapods}

編輯 Podfile，然後新增下行並執行：

```Bash
pod 'IMFGoogleAuthentication'
```
{: codeblock}

### Cordova
{: #googlesdk-cordova}

[GitHub 儲存庫及 API 參考資料](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### 使用 Cordova CLI 安裝 Google+ SDK
{: #googlesdk-cordova-cli}

安裝外掛程式：

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## 用於 Node.js 伺服器的伺服器 SDK
{: #serversdk}

[GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

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

[GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### 使用 npm 安裝 OAuth SDK
{: #oauthsdk}

執行 NPM 來安裝 SDK：
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## 自訂身分提供者範例
{: #customidprovider}

[簡單範例 GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)

[進階範例 GitHub 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### 使用 CocoaPods 安裝 IMFURLProtocol
{: #IMFURLProtocol-cocoapods}

編輯 Podfile，然後新增下行並執行：

```Bash
pod 'IMFURLProtocol'
```
{: codeblock}
