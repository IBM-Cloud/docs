---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDK、範例、API 參考資料
若要將 {{site.data.keyword.amashort}} SDK 新增至應用程式，請選擇您要使用的 SDK，然後配置相依關係管理程式將 SDK 拉出到應用程式。

## Core SDK
{: #coresdk}
Core SDK 包括用於啟用自訂鑑別、監視及登入行動式應用程式的 API。

### Android
{: #coresdk-android}
[Git 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### 使用 Gradle 安裝 Core SDK
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #coresdk-ios-swift}

[Git 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)

#### 使用 CocoaPods 安裝 Core SDK
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSCore'
```

### iOS (Objective-C SDK)
{: #coresdk-ios}

[Git 儲存庫](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### 使用 CocoaPods 安裝 Core SDK
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Git 儲存庫及 API 參考資料](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### 使用 Cordova CLI 安裝 Core SDK
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## 用於 Facebook 鑑別的 {{site.data.keyword.amashort}} Client SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Git 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### 使用 Gradle 安裝 Facebook SDK
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #facebooksdk-ios-swift}

[Git 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### 使用 CocoaPods 安裝 Facebook SDK
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (Objective-C SDK)
{: #facebooksdk-ios}

[Git 儲存庫](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

#### 使用 CocoaPods 安裝 Facebook SDK
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Github 儲存庫及 API 參考資料](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### 使用 Cordova CLI 安裝 Facebook SDK
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## 用於 Google 鑑別的 {{site.data.keyword.amashort}} Client SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[Github 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### 使用 Gradle 安裝 Google+ SDK
{: #googlesdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #googlesdk-ios-swift}

[Git 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### 使用 CocoaPods 安裝 Google+ SDK
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (Objective-C SDK)
{: #googlesdk-ios}

[Git 儲存庫](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)、[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### 使用 CocoaPods 安裝 Google+ SDK
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Git 儲存庫及 API 參考資料](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### 使用 Cordova CLI 安裝 Google+ SDK
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## 用於 Node.js 伺服器的 {{site.data.keyword.amashort}} Server SDK
{: #serversdk}

[Git 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### 使用 npm 安裝 Server SDK
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## 用於 Liberty for Java&trade; 伺服器的 {{site.data.keyword.amashort}} Server SDK
{: #serverlibertysdk}

[下載 TAI 構件](https://imf-tai.{DomainName}/public/TAI.zip)

## {{site.data.keyword.amashort}} Node.js OAuth SDK
{: #serverlibertysdk-github}

[Git 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### 使用 npm 安裝 OAuth SDK
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## 自訂身分提供者範例
{: #customidprovider}

[簡式範例 Git 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[進階範例 Git 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API 參考資料](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### 使用 CocoaPods 安裝 IMFURLProtocol
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
