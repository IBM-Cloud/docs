---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.mobileanalytics_short}} 설치
클라이언트 SDK
{: #mobileanalytics_sdk}
*마지막 업데이트 날짜: 2016년 4월 21일*
{: .last-updated}

{{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK는
현재 Android, iOS 및 WatchOS에 대해 사용 가능합니다.
{: #shortdesc}

## Android 클라이언트 SDK 설치
{: #install-sdk-android}

{{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK는 Android 프로젝트에 대한 종속성 관리자인 Gradle과 함께 배포됩니다. Gradle은 저장소에서 아티팩트를 자동으로 다운로드하여 Android 애플리케이션에서 사용 가능하도록 설정합니다.

1. [Android Studio](http://developer.android.com/sdk/index.html) 프로젝트를 작성하거나 기존 프로젝트를 여십시오.

2. 애플리케이션 모듈에 있는 `build.gradle` 파일을 여십시오.

  **팁**: Android 프로젝트에는 두 개의 `build.gradle` 파일이 있습니다. 하나는 프로젝트용이며 다른 하나는 애플리케이션 모듈용입니다. **애플리케이션 모듈** 파일을 사용해야 합니다.

3. `build.gradle` 파일의 `Dependencies` 섹션을 찾아서 다음과 같이 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK에 대한 컴파일 종속성을 추가하십시오.

  ```Gradle
compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
      name:'analytics',
      version: '1.+',
      ext: 'aar',
      transitive: true
  ```
  {: codeblock}

  저장소 명령문이 다음 코드 예와 유사해야 합니다.

	```Gradle
      dependencies {
        compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
          name:'analytics',
          version: '1.+',
          ext: 'aar',
          transitive: true
    	// other dependencies  
      }
  ```
  {: screen}

4. **도구 &gt; Android &gt; 프로젝트와 Gradle 파일 동기화**를 클릭하여 프로젝트와 Gradle을 동기화하십시오.

5. 사용자의 Android 프로젝트에 대한 `AndroidManifest.xml` 파일을 열고 `<manifest>` 요소 아래에 인터넷 액세스 권한을 추가하십시오.

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}


## Swift SDK 설치
{: #installing-sdk-ios}

{{site.data.keyword.mobileanalytics_full}} SDK를 사용하면 모바일 애플리케이션을 인스트루먼트할 수 있습니다. Swift SDK는 iOS 및 watchOS에 대해 사용 가능합니다.

### 시작하기 전에
{: #before-you-begin-ios}

Xcode를 올바르게 설정했는지 확인하십시오. iOS 개발 환경을 설정하는 방법에 대해 학습하려면 [Apple 개발자 웹 사이트](https://developer.apple.com/support/xcode/)를 참조하십시오.

{{site.data.keyword.mobileanalytics_short}} SDK는 Cocoa 프로젝트에 대한 종속성 관리자인 [Cocoapods](https://cocoapods.org/) 및 [Carthage](https://github.com/Carthage/Carthage#getting-started)와 함께 배포됩니다. CocoaPods 및 Carthage는 저장소에서 아티팩트를 자동으로 다운로드하여 사용자의 애플리케이션에서 사용 가능하도록 설정합니다.

#### Cocoapods
{: #cocoapods}
1. CocoaPods이 설치되지 않은 경우, 다음을 실행하십시오.

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}

2. 아직 CocoaPods에 대한 작업공간을 초기화하지 않은 경우, 프로젝트의 루트 디렉토리에서 `pod init` 명령을 실행하십시오. 그러면 CocoaPods이 Xcode 프로젝트에 대한 종속성을 정의하는 `Podfile` 파일을 작성합니다.

3. `BMSAnalytics` 팟을 Podfile 내의 대상에 추가하십시오. 예를 들어, 다음과 같습니다.

	### iOS

  ```
  use_frameworks!

  target 'MyApp' do
platform :ios, '8.0'
     pod 'BMSAnalytics'
  end
  ```

4. `Podfile` 파일을 저장하고 명령행에서 `pod install`을 실행하십시오.

5. CocoaPods에 의해 생성된 `.xcworkspace` 파일을 사용하여 Xcode 프로젝트 작업공간을 여십시오.

#### Carthage
{: #carthage}

[Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)를 사용하여 프로젝트에 프레임워크를 추가하십시오.

1. `BMSAnalytics` 프레임워크를 Cartfile에 추가하십시오.
  ```
  github "ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics"
  ```
2. `carthage update` 명령을 실행하십시오. 빌드가 완료되면 `BMSAnalytics.framework`, `BMSCore.framework` 및 `BMSAnalyticsAPI.framework`를 Xcode 프로젝트로 끄십시오.
3. [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) 사이트의 지시사항에 따라 통합을 완료하십시오.

# 관련 링크

## SDK
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API 참조
{: #api}
* [REST API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
