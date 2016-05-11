---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDK、样本和 API 参考
要将 {{site.data.keyword.amashort}} SDK 添加到应用程序，请选择要使用的 SDK，然后将依赖关系管理器配置为将这些 SDK 拉入到应用程序中。

## 核心 SDK
{: #coresdk}
核心 SDK 包含用于在移动应用程序中启用定制认证、监视和日志记录的 API。

### Android
{: #coresdk-android}
[Git 存储库](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)和 [API 参考](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### 使用 Gradle 安装核心 SDK
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

[Git 存储库](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)

#### 使用 CocoaPods 安装核心 SDK
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSCore'
```

### iOS (Objective-C SDK)
{: #coresdk-ios}

[Git 存储库](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)和 [API 参考](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### 使用 CocoaPods 安装核心 SDK
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Git 存储库和 API 参考](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### 使用 Cordova CLI 安装核心 SDK
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## 用于 Facebook 认证的 {{site.data.keyword.amashort}} 客户端 SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Git 存储库](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication)和 [API 参考](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### 使用 Gradle 安装 Facebook SDK
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

[Git 存储库](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### 使用 CocoaPods 安装 Facebook SDK
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (Objective-C SDK)
{: #facebooksdk-ios}

[Git 存储库](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)和 [API 参考](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

#### 使用 CocoaPods 安装 Facebook SDK
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Github 存储库和 API 参考](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### 使用 Cordova CLI 安装 Facebook SDK
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## 用于 Google 认证的 {{site.data.keyword.amashort}} 客户端 SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[Github 存储库](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication)，[API 参考](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### 使用 Gradle 安装 Google+ SDK
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

[Git 存储库](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### 使用 CocoaPods 安装 Google+ SDK
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (Objective-C SDK)
{: #googlesdk-ios}

[Git 存储库](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git)和 [API 参考](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### 使用 CocoaPods 安装 Google+ SDK
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Git 存储库和 API 参考](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### 使用 Cordova CLI 安装 Google+ SDK
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## 用于 Node.js 服务器的 {{site.data.keyword.amashort}} 服务器 SDK
{: #serversdk}

[Git 存储库](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### 使用 npm 安装服务器 SDK
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## 用于 Liberty for Java&trade; 服务器的 {{site.data.keyword.amashort}} 服务器 SDK
{: #serverlibertysdk}

[下载 TAI 工件](https://imf-tai.{DomainName}/public/TAI.zip)

## {{site.data.keyword.amashort}} Node.js OAuth SDK
{: #serverlibertysdk-github}

[Git 存储库](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### 使用 npm 安装 OAuth SDK
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## 定制身份提供者样本
{: #customidprovider}

[简单样本 Git 存储库](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[高级样本 Git 存储库](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API 参考](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### 使用 CocoaPods 安装 IMFURLProtocol
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
