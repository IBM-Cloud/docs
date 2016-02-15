{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDK, 샘플, API 참조
{{site.data.keyword.amashort}} SDK를 앱에 추가하려면, 사용하려는 SDK를 선택한 다음 SDK를 앱으로 풀링하도록 종속 항목 관리자를 구성하십시오. 

## 코어 SDK
{: #coresdk}
코어 SDK에는 모바일 앱에서 사용자 정의 인증, 모니터링 및 로깅을 사용하기 위한 API가 포함되어 있습니다. 

### Android
{: #coresdk-android}
[Github 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[API 참조](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Gradle로 코어 SDK 설치
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

[Github 저장소](#),
[API 참조](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### CocoaPods로 코어 SDK 설치
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Github 저장소 및 API 참조](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI로 코어 SDK 설치
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## Facebook 인증을 위한 {{site.data.keyword.amashort}} 클라이언트 SDK
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Github 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[API 참조](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Gradle로 Facebook SDK 설치
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

[Github 저장소(곧 출시 예정)](#),
[API 참조](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

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

## Google 인증을 위한 {{site.data.keyword.amashort}} 클라이언트 SDK
{: #googlesdk}

### Android
{: #googlesdk-android}

[Github 저장소](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[API 참조](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Gradle로 Google+ SDK 설치
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

[Github 저장소(곧 출시 예정)](#),
[API 참조](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### CocoaPods로 Google+ SDK 설치
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Github 저장소 및 API 참조](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Cordova CLI로 Google+ SDK 설치
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## Node.js 서버를 위한 {{site.data.keyword.amashort}} 서버 SDK
{: #serversdk}

[Github 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### npm으로 서버 SDK 설치
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## Liberty for Java 서버용 {{site.data.keyword.amashort}} 서버 SDK
{: #serverlibertysdk}

[TAI 아티팩트 다운로드](https://imf-tai.{DomainName}/public/TAI.zip)

## {{site.data.keyword.amashort}} Node.js OAuth SDK
{: #serverlibertysdk-github}

[Github 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### npm으로 OAuth SDK 설치
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## 사용자 정의 ID 제공자 샘플
{: #customidprovider}

[Github 저장소 및 API 참조](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)


## IMFURLProtocol
{: #IMFURLProtocol}

[API 참조](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### CocoaPods로 IMFURLProtocol 설치
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
