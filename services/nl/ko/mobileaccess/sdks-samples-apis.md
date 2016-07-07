---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDK, 샘플, API 참조
*마지막 업데이트 날짜: 2016년 4월 30일*
{: .last-updated}

{{site.data.keyword.amashort}} SDK를 앱에 추가하려면, 사용하려는 SDK를 선택한 다음 SDK를 앱으로 풀링하도록 종속성 관리자를 구성하십시오.
{:shortdesc}

## 코어 SDK
{: #coresdk}
코어 SDK에는 모바일 앱에서 사용자 정의 인증, 모니터링 및 로깅을 사용하기 위한 API가 포함되어 있습니다. 

### Android
{: #coresdk-android}
[Git 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Gradle로 코어 SDK 설치
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS(Swift SDK)
{: #coresdk-ios-swift}

[Git 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### CocoaPods로 코어 SDK 설치
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSSecurity'
```

### iOS(Objective-C SDK)
{: #coresdk-ios}

Objective-C SDK는 그대로 완벽하게 지원되며 여전히 {{site.data.keyword.Bluemix_notm}} 모바일 서비스의 기본 SDK로 간주되지만, 새로운 Swift SDK를 위해 올해 말에 중단될 계획입니다([iOS Swift SDK 설정](getting-started-ios-swift-sdk.html) 참조).

[Git 저장소](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### CocoaPods로 코어 SDK 설치
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Git 저장소 및 API 참조](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI로 코어 SDK 설치
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## Facebook 인증용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Git 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Gradle로 Facebook SDK 설치
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS(Swift SDK)
{: #facebooksdk-ios-swift}

[Git 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### CocoaPods로 Facebook SDK 설치
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS(Objective-C SDK)
{: #facebooksdk-ios}

[Git 저장소](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

*참고:* Objective-C SDK는 그대로 완벽하게 지원되며 여전히 {{site.data.keyword.Bluemix_notm}} 모바일 서비스의 기본 SDK로 간주되지만 새로운 Swift SDK를 위해 올해 말해 중단될 계획입니다. 새 애플리케이션에서는 Swift SDK를 사용하는 것이 좋습니다(iOS Swift SDK 설정 참조).
#### CocoaPods로 Facebook SDK 설치
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Github 저장소 및 API 참조](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI로 Facebook SDK 설치
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## Google 인증용 {{site.data.keyword.amashort}} 클라이언트 SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[Github 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Gradle로 Google+ SDK 설치
{: #googlesdk-android-gradle}

```Gradle
compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS(Swift SDK)
{: #googlesdk-ios-swift}

[Git 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### CocoaPods로 Google+ SDK 설치
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS(Objective-C SDK - 더 이상 사용되지 않음)
{: #googlesdk-ios}

[Git 저장소](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### CocoaPods로 Google+ SDK 설치
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Git 저장소 및 API 참조](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI로 Google+ SDK 설치
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## Node.js 서버용 {{site.data.keyword.amashort}} 서버 SDK
{: #serversdk}

[Git 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### npm으로 서버 SDK 설치
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## Liberty for Java&trade; 서버용 {{site.data.keyword.amashort}} 서버 SDK
{: #serverlibertysdk}

[TAI 아티팩트 다운로드](https://imf-tai.{DomainName}/public/TAI.zip)

## {{site.data.keyword.amashort}} Node.js OAuth SDK
{: #serverlibertysdk-github}

[Git 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### npm으로 OAuth SDK 설치
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## 사용자 정의 ID 제공자 샘플
{: #customidprovider}

[단순 샘플 Git 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[고급 샘플 Git 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### CocoaPods로 IMFURLProtocol 설치
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
