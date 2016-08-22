---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDK, 샘플 및 API 참조
*마지막 업데이트 날짜: 2016년 7월 17일*
{: .last-updated}

앱에 {{site.data.keyword.amashort}} SDK를 추가하려면, 사용하려는 SDK를 선택하십시오. 그런 다음 SDK를 앱으로 가져오도록 종속성 관리자를 구성하십시오.
{:shortdesc}

**참고:** 후속 섹션에서는 SDK 설치에 대한 추가 정보를 제공합니다. 

## 코어 SDK
{: #coresdk}

코어 SDK에는 사용자 정의 인증 사용, 로깅 및 모바일 앱 모니터링을 위한 API가 포함되어 있습니다. 

### Android
{: #coresdk-android}

[GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Gradle로 코어 SDK 설치
{: #coresdk-android-gradle}

컴파일 종속성을 앱의 `build.gradle` 파일에 추가하십시오. 

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS(Swift SDK)
{: #coresdk-ios-swift}

[GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### CocoaPods로 코어 SDK 설치
{: #coresdk-ios-siwft-cocoapods}
Podfile을 편집하여 다음 행을 필요한 대상에 추가한 후 실행하십시오. 

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

Podfile을 편집하여 다음 행을 필요한 대상에 추가한 후 실행하십시오. 
```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[GitHub 저장소 및 API 참조](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI로 코어 SDK 설치
{: #coresdk-cordova-cli}

Mobile Client Access Cordova 플러그인을 설치하십시오.

```Bash
cordova plugin add ibm-mfp-core
```

## Facebook 인증용 클라이언트 SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Gradle로 Facebook SDK 설치
{: #facebooksdk-android-gradle}

컴파일 종속성을 앱의 `build.gradle` 파일에 추가하십시오. 
```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS(Swift SDK)
{: #facebooksdk-ios-swift}

[GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### CocoaPods로 Facebook SDK 설치
{: #facebooksdk-ios-swift-cocoapods}

Podfile을 편집하여 다음을 필요한 대상에 추가한 후 실행하십시오. 
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS(Objective-C SDK)
{: #facebooksdk-ios}

[Git 저장소](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

*참고:* Objective-C SDK는 그대로 완벽하게 지원되며 여전히 {{site.data.keyword.Bluemix_notm}} 모바일 서비스의 기본 SDK로 간주되지만, 새로운 Swift SDK를 위해 올해 말에 중단될 계획입니다. 새 애플리케이션의 경우 Swift SDK를 사용하는 것이 좋습니다(iOS Swift SDK 설정 참조). 
#### CocoaPods로 Facebook SDK 설치
{: #facebooksdk-ios-cocoapods}

Podfile을 편집하여 다음 행을 추가한 후 실행하십시오. 

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[GitHub 저장소 및 API 참조](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI로 Facebook SDK 설치
{: #facebooksdk-cordova-cli}

Cordova 플러그인을 설치하십시오. 

```Bash
cordova plugin add ibm-mfp-core
```

## Google 인증용 클라이언트 SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[API 참조](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Gradle로 Google+ SDK 설치
{: #googlesdk-android-gradle}

컴파일 종속성을 앱의 `build.gradle` 파일에 추가하십시오. 

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS(Swift SDK)
{: #googlesdk-ios-swift}

[GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### CocoaPods로 Google+ SDK 설치
{: #googlesdk-ios-swift-cocoapods}

Podfile을 편집하여 다음을 추가한 후 실행하십시오. 

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

Podfile을 편집하여 다음 행을 추가한 후 실행하십시오. 

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[GitHub 저장소 및 API 참조](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI로 Google+ SDK 설치 
{: #googlesdk-cordova-cli}

플러그인을 설치하십시오. 

```Bash
cordova plugin add ibm-mfp-core
```

## Node.js 서버용 서버 SDK
{: #serversdk}

[GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### npm으로 서버 SDK 설치
{: #serversdk-npm}

SDK를 설치하기 위해 NPM을 실행하십시오. 

```Bash
npm install -save bms-mca-token-validation-strategy
```

## Liberty for Java&trade; 서버용 서버 SDK
{: #serverlibertysdk}

[TAI 아티팩트 다운로드](https://imf-tai.{DomainName}/public/TAI.zip)

#### Liberty SDK 설치
{: #libertysdk}
1. `com.ibm.worklight.oauth.tai_1.0.0.jar` 파일을 `${wlp.user.dir}/extensions/lib` 디렉토리로 복사하십시오. 

**팁:** `$<wlp.user.dir>`은 Liberty for Java 런타임에 대한 사용자 디렉토리입니다. 기본 디렉토리 이름은 `usr`입니다. 

1. `OAuthTai-1.0.mf` 디렉토리를 `$<wlp.user.dir>/extension/lib/features` 디렉토리로 복사하십시오. 


## Node.js OAuth SDK
{: #serverlibertysdk-github}

[GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### npm으로 OAuth SDK 설치
{: #oauthsdk}

SDK를 설치하기 위해 NPM을 실행하십시오. 
```Bash
npm install -save bms-mca-oauth-sdk
```

## 사용자 정의 ID 제공자 샘플
{: #customidprovider}

[단순 샘플 GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[고급 샘플 GitHub 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[API 참조 ](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### CocoaPods로 IMFURLProtocol 설치
{: #IMFURLProtocol-cocoapods}

Podfile을 편집하여 다음 행을 추가한 후 실행하십시오. 

```Bash
pod 'IMFURLProtocol'
```
