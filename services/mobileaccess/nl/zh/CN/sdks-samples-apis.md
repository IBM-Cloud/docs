---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.amashort}} SDK、样本和 API 参考
要将 {{site.data.keyword.amafull}} SDK 添加到客户端应用程序，请选择要使用的 SDK。然后，配置依赖关系管理器，以将 SDK 拉入到应用程序中。
{:shortdesc}

**注：**后续部分提供有关安装 SDK 的其他信息。

## 核心 SDK
{: #coresdk}

核心 SDK 包含用于启用定制认证和日志记录的 API。

### Android
{: #coresdk-android}

[GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "外部链接图标"){: new_window}

#### 使用 Gradle 安装核心 SDK
{: #coresdk-android-gradle}

向应用程序的 `build.gradle` 文件添加编译依赖关系：

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

[GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security "外部链接图标"){: new_window}

#### 使用 CocoaPods 安装核心 SDK
{: #coresdk-ios-siwft-cocoapods}
编辑 Podfile，并将以下行添加到所需目标并运行：

```
use_frameworks!
pod 'BMSSecurity'
 ```
{: codeblock}


### Cordova
{: #coresdk-cordova}

[GitHub 存储库和 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core "外部链接图标"){: new_window}

#### 使用 Cordova CLI 安装核心 SDK
{: #coresdk-cordova-cli}

安装 Mobile Client Access Cordova 插件：
```Bash
cordova plugin add bms-core
```
{: codeblock}

## 用于 Facebook 认证的客户端 SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication "外部链接图标"){: new_window}

#### 使用 Gradle 安装 Facebook SDK
{: #facebooksdk-android-gradle}

向应用程序的 `build.gradle` 文件添加编译依赖关系：
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

[GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication "外部链接图标"){: new_window}

#### 使用 CocoaPods 安装 Facebook SDK
{: #facebooksdk-ios-swift-cocoapods}

编辑 Podfile，并将以下行添加到所需目标并运行：
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}


### Cordova
{: #facebooksdk-cordova}

[GitHub 存储库和 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core "外部链接图标"){: new_window}

#### 使用 Cordova CLI 安装 Facebook SDK
{: #facebooksdk-cordova-cli}

安装 Cordova 插件：

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## 用于 Google 认证的客户端 SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication "外部链接图标"){: new_window}


#### 使用 Gradle 安装 Google+ SDK
{: #googlesdk-android-gradle}

向应用程序的 `build.gradle` 文件添加编译依赖关系：

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

[GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication "外部链接图标"){: new_window}

#### 使用 CocoaPods 安装 Google+ SDK
{: #googlesdk-ios-swift-cocoapods}

编辑 Podfile，添加以下行并运行：

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}


### Cordova
{: #googlesdk-cordova}

[GitHub 存储库和 API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core "外部链接图标"){: new_window}

#### 使用 Cordova CLI 安装 Google+ SDK
{: #googlesdk-cordova-cli}

安装插件：

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## 用于 Node.js 服务器的服务器 SDK

{: #serversdk}

[GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy "外部链接图标"){: new_window}

#### 使用 npm 安装服务器 SDK
{: #serversdk-npm}

运行 NPM 以安装 SDK：

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## 用于 Liberty for Java&trade; 服务器的服务器 SDK
{: #serverlibertysdk}

[下载 TAI 工件](https://imf-tai.{DomainName}/public/TAI.zip)

#### 安装 Liberty SDK
{: #libertysdk}

1. 将 `com.ibm.worklight.oauth.tai_1.0.0.jar` 文件复制到 `$<wlp.user.dir>/extensions/lib` 目录。

  **提示：**`$<wlp.user.dir>` 是 Liberty for Java 运行时的用户目录。缺省目录名称为 `usr`。

1. 将 `OAuthTai-1.0.mf` 目录复制到 `$<wlp.user.dir>/extension/lib/features` 目录。


## Node.js OAuth SDK
{: #serverlibertysdk-github}

[GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk "外部链接图标"){: new_window}

#### 使用 npm 安装 OAuth SDK
{: #oauthsdk}

运行 NPM 以安装 SDK：
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## 定制身份提供者样本
{: #customidprovider}

[简单样本 GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "外部链接图标"){: new_window}

[高级样本 GitHub 存储库 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "外部链接图标"){: new_window}


