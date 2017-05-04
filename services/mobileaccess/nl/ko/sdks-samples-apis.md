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

**중요: {{site.data.keyword.amafull}} 서비스는 {{site.data.keyword.appid_full}} 서비스로 대체되었습니다. **

# {{site.data.keyword.amashort}} SDK, 샘플 및 API 참조


클라이언트 앱에 {{site.data.keyword.amafull}} SDK를 추가하려면 사용하려는 SDK를 선택하십시오. 그런 다음 SDK를 앱으로 가져오도록 종속성 관리자를 구성하십시오.
{:shortdesc}

**참고:** 후속 섹션에서는 SDK 설치에 대한 추가 정보를 제공합니다. 

## 코어 SDK
{: #coresdk}

코어 SDK에는 사용자 정의 인증 및 로깅을 사용하기 위한 API가 포함되어 있습니다. 

### Android
{: #coresdk-android}

[GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}

#### Gradle로 코어 SDK 설치
{: #coresdk-android-gradle}

컴파일 종속성을 앱의 `build.gradle` 파일에 추가하십시오. 

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS(Swift SDK)
{: #coresdk-ios-swift}

[GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security){: new_window}

#### CocoaPods로 코어 SDK 설치
{: #coresdk-ios-siwft-cocoapods}
Podfile을 편집하여 다음 행을 필요한 대상에 추가한 후 실행하십시오. 

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}


### Cordova
{: #coresdk-cordova}

[GitHub 저장소 및 API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Cordova CLI로 코어 SDK 설치
{: #coresdk-cordova-cli}

Mobile Client Access Cordova 플러그인을 설치하십시오.
```Bash
cordova plugin add bms-core
```
{: codeblock}

## Facebook 인증용 클라이언트 SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication){: new_window},

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
{: codeblock}

### iOS(Swift SDK)
{: #facebooksdk-ios-swift}

[GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication){: new_window}

#### CocoaPods로 Facebook SDK 설치
{: #facebooksdk-ios-swift-cocoapods}

Podfile을 편집하여 다음을 필요한 대상에 추가한 후 실행하십시오. 
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}


### Cordova
{: #facebooksdk-cordova}

[GitHub 저장소 및 API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Cordova CLI로 Facebook SDK 설치
{: #facebooksdk-cordova-cli}

Cordova 플러그인을 설치하십시오. 

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Google 인증용 클라이언트 SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication){: new_window},


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
{: codeblock}

### iOS(Swift SDK)
{: #googlesdk-ios-swift}

[GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication){: new_window}

#### CocoaPods로 Google+ SDK 설치
{: #googlesdk-ios-swift-cocoapods}

Podfile을 편집하여 다음을 추가한 후 실행하십시오. 

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}


### Cordova
{: #googlesdk-cordova}

[GitHub 저장소 및 API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Cordova CLI로 Google+ SDK 설치 
{: #googlesdk-cordova-cli}

플러그인을 설치하십시오. 

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## Node.js 서버용 서버 SDK
{: #serversdk}

[GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy){: new_window}

#### npm으로 서버 SDK 설치
{: #serversdk-npm}

SDK를 설치하기 위해 NPM을 실행하십시오. 

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

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

[GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk){: new_window}

#### npm으로 OAuth SDK 설치
{: #oauthsdk}

SDK를 설치하기 위해 NPM을 실행하십시오. 
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## 사용자 정의 ID 제공자 샘플
{: #customidprovider}

[단순 샘플 GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}

[고급 샘플 GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}
