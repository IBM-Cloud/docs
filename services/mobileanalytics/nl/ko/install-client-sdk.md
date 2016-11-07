---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-18"

---

# {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK 설치
{: #mobileanalytics_sdk}

마지막 업데이트 날짜: 2016년 10월 18일
{: .last-updated}

{{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK는
현재 Android, iOS 및 WatchOS에 대해 사용 가능합니다.
{: #shortdesc}

## Android 클라이언트 SDK 설치
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

{{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK는 Android 프로젝트에 대한 종속성 관리자인 Gradle과 함께 배포됩니다. Gradle은 저장소에서 아티팩트를 자동으로 다운로드하여 Android 애플리케이션에서 사용 가능하도록 설정합니다.

1. [Android Studio](http://developer.android.com/sdk/index.html) 프로젝트를 작성하거나 기존 프로젝트를 여십시오.

2. **앱 모듈**에 있는 `build.gradle` 파일을 여십시오. 

  **팁**: Android 프로젝트에는 두 개의 `build.gradle` 파일이 있습니다. 하나는 프로젝트용이고 다른 하나는 앱 모듈용입니다. **앱 모듈** 파일을 사용해야 합니다. 

3. `build.gradle` 파일의 `Dependencies` 섹션을 찾아 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK의 컴파일 종속성을 추가하십시오. 저장소 명령문이 다음 코드 예와 유사해야 합니다.

	```Gradle
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies
      }
  ```
  {: codeblock}

4. **도구 &gt; Android &gt; 프로젝트와 Gradle 파일 동기화**를 클릭하여 프로젝트와 Gradle을 동기화하십시오.

5. Android 프로젝트의 `AndroidManifest.xml` 파일을 여십시오. 이 파일은 **앱 > Manifest**에 있습니다. `<manifest>` 요소에 인터넷 액세스 권한을 추가하십시오. 

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
6. Android 클라이언트 SDK를 설치했습니다. 다음으로 분석 클라이언트 SDK [가져오기 및 초기화](sdk.html#initalize-ma-sdk-android)를 수행합니다.    

## Swift SDK 설치
{: #installing-sdk-ios}

![CocoaPods 호환 가능](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

{{site.data.keyword.mobileanalytics_full}} SDK를 사용하면 모바일 애플리케이션을 인스트루먼트할 수 있습니다. Swift SDK는 iOS 및 watchOS에 대해 사용 가능합니다.

### 시작하기 전에
{: #before-you-begin-ios}

Xcode를 올바르게 설정했는지 확인하십시오. iOS 개발 환경을 설정하는 방법에 대해 학습하려면 [Apple 개발자 웹 사이트](https://developer.apple.com/support/xcode/)를 참조하십시오. 클라이언트 SDK Swift 분석에 필요한 [Xcode 요구사항](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements)에 대해 읽으십시오. 

{{site.data.keyword.mobileanalytics_short}} SDK는 Cocoa 프로젝트의 종속성 관리자인 [CocoaPods](https://cocoapods.org/), [Carthage](https://github.com/Carthage/Carthage#getting-started)와 함께 배포됩니다. CocoaPods 및 Carthage는 저장소에서 아티팩트를 자동으로 다운로드하여 사용자의 애플리케이션에서 사용 가능하도록 설정합니다.

#### CocoaPods
{: #cocoapods}

1. CocoaPods이 설치되지 않은 경우, 다음을 실행하십시오.

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}
    
    Xcode 8의 경우: `sudo gem install cocoapods --pre`
    
   다음과 같이 로컬 CocoaPod 저장소를 업데이트하여 `BMSAnalytics`의 최신 버전을 확보하십시오. 
   
    ```
    pod repo update master
    ```
    {: codeblock}

2. GitHub의 [{{site.data.keyword.Bluemix_notm}} 모바일 서비스 Swift SDK 지시사항](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods)을 수행하십시오. 
	
3. iOS 클라이언트 SDK를 설치한 후 분석 클라이언트 SDK [가져오기 및 초기화](sdk.html#init-ma-sdk-ios)를 수행하십시오.    

#### Carthage
{: #carthage}

[Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)를 사용하여 프로젝트에 프레임워크를 추가하십시오.

1. GitHub의 [Carthage 설치 지시사항](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage)을 수행하십시오. 

2. iOS 클라이언트 SDK를 설치한 후 분석 클라이언트 SDK [가져오기 및 초기화](sdk.html#init-ma-sdk-ios)를 수행하십시오. 

# 관련 링크

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API 참조
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
