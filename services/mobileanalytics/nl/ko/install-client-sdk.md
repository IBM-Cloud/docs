---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK 설치
{: #mobileanalytics_sdk}

{{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK는
현재 Android, iOS, WatchOS 및 Cordova에서 사용 가능합니다.
{: #shortdesc}

## Android 클라이언트 SDK 설치
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

{{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK는 Android 프로젝트에 대한 종속성 관리자인 Gradle과 함께 배포됩니다. Gradle은 저장소에서 아티팩트를 자동으로 다운로드하여 Android 애플리케이션에서 사용 가능하도록 설정합니다.

1. [Android Studio](http://developer.android.com/sdk/index.html) 프로젝트를 작성하거나 기존 프로젝트를 여십시오.

2. **앱 모듈**에 있는 `build.gradle` 파일을 여십시오. 

  **팁**: Android 프로젝트에는 두 개의 `build.gradle` 파일이 있습니다. 하나는 프로젝트용이고 다른 하나는 앱 모듈용입니다. **앱 모듈** 파일을 사용해야 합니다. 

3. `build.gradle` 파일의 `Dependencies` 섹션을 찾아 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK의 컴파일 종속성을 추가하십시오. 저장소 명령문이 다음 코드 예와 유사해야 합니다.

	```
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  ```
  	{: codeblock}

4. **도구 &gt; Android &gt; 프로젝트와 Gradle 파일 동기화**를 클릭하여 프로젝트와 Gradle을 동기화하십시오.

5. Android 프로젝트의 `AndroidManifest.xml` 파일을 여십시오. 이 파일은 **앱 > Manifest**에 있습니다. `<manifest>` 요소에 인터넷 액세스 권한을 추가하십시오. 

	```
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
   
6. Android 클라이언트 SDK를 설치했습니다. 다음으로 분석 클라이언트 SDK [가져오기 및 초기화](sdk.html#initalize-ma-sdk)를 수행하십시오.    

## Swift SDK 설치
{: #installing-sdk-ios}

![CocoaPods 호환 가능](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

{{site.data.keyword.mobileanalytics_full}} SDK를 사용하면 모바일 애플리케이션을 인스트루먼트할 수 있습니다. Swift SDK는 iOS 및 watchOS에 대해 사용 가능합니다.

### 시작하기 전에
{: #before-you-begin-ios}

Xcode를 올바르게 설정했는지 확인하십시오. iOS 개발 환경을 설정하는 방법에 대해 학습하려면 [Apple 개발자 웹 사이트](https://developer.apple.com/support/xcode/)를 참조하십시오. 클라이언트 SDK Swift 분석에 필요한 [Xcode 요구사항](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements)에 대해 읽으십시오. 

{{site.data.keyword.mobileanalytics_short}} SDK는 Cocoa 프로젝트의 종속성 관리자인 [CocoaPods](https://cocoapods.org/), [Carthage](https://github.com/Carthage/Carthage#getting-started)와 함께 배포됩니다. CocoaPods 및 Carthage는 저장소에서 아티팩트를 자동으로 다운로드하여 사용자의 애플리케이션에서 사용 가능하도록 설정합니다.CocoaPods 또는 Carthage를 선택하십시오.

#### CocoaPods
{: #cocoapods}

1. GitHub의 [{{site.data.keyword.Bluemix_notm}} 모바일 서비스 Swift SDK 지시사항](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods)에 따라 Cocoapods를 사용하여 `BMSAnalytics`를 설치하고 이를 프로파일에 추가하십시오.  
	
2. iOS 클라이언트 SDK를 설치한 후 분석 클라이언트 SDK [가져오기 및 초기화](sdk.html#initalize-ma-sdk)를 수행하십시오.    

#### Carthage
{: #carthage}

CocoaPods를 사용하지 않는 경우 [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)를 사용하여 프로젝트에 프레임워크를 추가할 수 있습니다. 

1. GitHub의 [Carthage 설치 지시사항](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage)에 따라 `BMSAnalytics`를 설치하십시오.

2. iOS 클라이언트 SDK를 설치한 후 분석 클라이언트 SDK [가져오기 및 초기화](sdk.html#initalize-ma-sdk)를 수행하십시오. 

## Cordova 플러그인 설치
{: #installing-sdk-cordova}

{{site.data.keyword.mobileanalytics_full}} Cordova 플러그인을 사용하면 모바일 애플리케이션을 인스트루먼트할 수 있습니다.  

1. Android 및 iOS 플랫폼을 Cordova 애플리케이션에 추가하십시오. 명령행에서 다음 명령문 중 하나 또는 둘 다를 실행하십시오.
   
   Android:

	 ```
	 cordova platform add android
	 ```
	 {: codeblock}
	
   iOS:
   	
	```
	cordova platform add ios
	```
   {: codeblock}
	
2. Android 플랫폼을 추가한 경우, 지원되는 최소 API 레벨을 Cordova 애플리케이션의 `config.xml` 파일에 추가해야 합니다. `config.xml` 파일을 열어 다음 행을 `<platform name="android">` 요소에 추가하십시오.

	```
	<platform name="android">
  	<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
  	</platform>
	```
   {: codeblock}

 *minSdkVersion* 값은 `15`보다 높아야 합니다. Android SDK용으로 지원되는 *targetSdkVersion*을 최신 상태로 유지하려면 [Android Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/android/)를 참조하십시오.  

3. iOS 운영 체제를 추가한 경우, `<platform name="ios">` 요소를 다음과 같은 대상 선언으로 업데이트하십시오.

	```
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  	</platform>
	```
	{: codeblock}

4. {{site.data.keyword.mobileanalytics_short}} 플러그인을 설치하십시오. 현재는 Cordova-CLI V6.3.0 이하가 지원됩니다.

 	```
	cordova platform add android@5.2.2
	```
	{: codeblock}

5. 다음 명령을 실행하여 플러그인이 성공적으로 설치되었는지 확인하십시오.
	
	```
	cordova plugin list
	```
	{: codeblock}
	
6. 이제 Cordova 플러그인이 설치되었습니다. 다음으로 분석 클라이언트 SDK [가져오기 및 초기화](sdk.html#initalize-ma-sdk)를 수행하십시오. 

# 관련 링크

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova 플러그인 코어 SDK](https://www.npmjs.com/package/bms-core){: new_window}

## API 참조
{: #api}
* [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
