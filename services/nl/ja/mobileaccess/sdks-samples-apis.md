{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDK、サンプル、API リファレンス
{{site.data.keyword.amashort}} SDK をアプリに追加するには、使用する SDK を選択し、依存関係マネージャーを構成して SDK をアプリにプルします。

## Core SDK
{: #coresdk}
Core SDK には、モバイル・アプリでのカスタム認証、モニタリング、およびロギングを可能にするための API が含まれています。

### Android
{: #coresdk-android}
[Github repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[API reference](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Gradle を使用した Core SDK のインストール
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS
{: #coresdk-ios}

[Github repo](#),
[API reference](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### CocoaPods を使用した Core SDK のインストール
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Github repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI を使用した Core SDK のインストール
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## Facebook 認証用の {{site.data.keyword.amashort}} Client SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Github repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[API reference](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Gradle を使用した Facebook SDK のインストール
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS
{: #facebooksdk-ios}

[Github repo (近日公開)](#),
[API reference](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

#### CocoaPods を使用した Facebook SDK のインストール
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Github repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI を使用した Facebook SDK のインストール
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## Google 認証用の {{site.data.keyword.amashort}} Client SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[Github repo](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[API reference](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Gradle を使用した Google+ SDK のインストール
{: #googlesdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS
{: #googlesdk-ios}

[Github repo (近日公開)](#),
[API reference](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### CocoaPods を使用した Google+ SDK のインストール
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Github repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI を使用した Google+ SDK のインストール
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}} Server SDK for Node.js サーバー
{: #serversdk}

[Github repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### npm を使用した Server SDK のインストール
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## {{site.data.keyword.amashort}} Server SDK for Java for Liberty サーバー
{: #serverlibertysdk}

[TAI 成果物のダウンロード](https://imf-tai.{DomainName}/public/TAI.zip)

## {{site.data.keyword.amashort}} Node.js OAuth SDK
{: #serverlibertysdk-github}

[Github repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### npm を使用した OAuth SDK のインストール
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## カスタム ID プロバイダーのサンプル
{: #customidprovider}

[Github repo and API reference](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)


## IMFURLProtocol
{: #IMFURLProtocol}

[API reference](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### CocoaPods を使用した IMFURLProtocol のインストール
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
