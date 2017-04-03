---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# BMSClient 초기화
{: #sdk_BMSClient}

`BMSCore`에서는 다른 {{site.data.keyword.Bluemix}} 모바일 서비스 클라이언트 SDK가 이와 연관된 {{site.data.keyword.Bluemix_notm}} 서비스와 통신하는 데 사용하는 HTTP 인프라를 제공합니다. 


## Android 애플리케이션 초기화
{: #init-BMSClient-android}

`BMSCore` 패키지를 다운로드하여 Android Studio 프로젝트로 가져오거나 Gradle을 사용할 수 있습니다. 

1. 다음 `import` 문을 프로젝트 파일의 시작 부분에 추가하여 클라이언트 SDK를 가져오십시오. 

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
  ```
  {: codeblock}

2. Android 애플리케이션의 기본 활동의 `onCreate` 메소드 내 또는 프로젝트에 가장 적합한 위치에 초기화 코드를 추가하여 Android 애플리케이션에서 `BMSClient` SDK를 초기화하십시오.

  ```Java
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
  ```
  {: codeblock}

  **bluemixRegion** 매개변수를 사용하여 `BMSClient`를 초기화해야 합니다. 초기자(initializer)에서 **bluemixRegion** 값은 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치를 지정합니다(예: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` 또는 `BMSClient.REGION_SYDNEY`). 


## iOS 애플리케이션 초기화
{: #init-BMSClient-ios}

[CocoaPods](https://cocoapods.org){: new_window} 또는 [Carthage](https://github.com/Carthage/Carthage){: new_window}를 사용하여 `BMSCore` 패키지를 가져올 수 있습니다. 

1. CocoaPods를 사용하여 `BMSCore`를 설치하려면 Podfile에 다음 행을 추가하십시오. 프로젝트에 아직 Podfile이 없으면 `pod init` 명령을 사용하십시오. 

  ```Swift
  use_frameworks!

  target 'MyApp' do
    pod 'BMSCore'
  end
  ```
  {: codeblock}

  그런 다음 `pod install` 명령을 실행하고 생성된 `.xcworkspace` 파일을 여십시오. `BMSCore`의 새 릴리스로 업데이트하려면 `pod update BMSCore`를 사용하십시오. 

  CocoaPods 사용에 대한 자세한 정보는 [CocoaPods 안내서 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://guides.cocoapods.org/using/index.html){: new_window}를 참조하십시오. 

2. Carthage를 사용하여 `BMSCore`를 설치하려면 다음 [지시사항 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/Carthage/Carthage#getting-started){: new_window}을 따르십시오. 

  1. Cartfile에 다음 행을 추가하십시오. 

      ```
      github "ibm-bluemix-mobile-services/bms-clientsdk-swift-core"
      ```
      {: codeblock}

  2. `carthage update` 명령을 실행하십시오. 

  3. 빌드가 완료되면 Carthage 지시사항의 [3단계 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/Carthage/Carthage#getting-started)에 따라 `BMSCore.framework`를 프로젝트에 추가하십시오. 

      Swift 2.3으로 빌드된 애플리케이션의 경우 `carthage update --toolchain com.apple.dt.toolchain.Swift_2_3` 명령을 사용하십시오. 그 외의 경우에는 `carthage update` 명령을 사용하십시오. 

3. 모듈을 가져오십시오. 

  ```Swift
  import BMSCore
  ```
  {: codeblock}

4. 다음 코드를 사용하여 `BMSClient` 클래스를 초기화하십시오. 

  애플리케이션 위임의 `application(_:didFinishLaunchingWithOptions:)` 메소드 또는 프로젝트에 가장 적합한 위치에 초기화 코드를 배치하십시오.

  ```Swift
  BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
  ```
  {: codeblock}

  **bluemixRegion** 매개변수를 사용하여 `BMSClient`를 초기화해야 합니다. 초기자(initializer)에서 **bluemixRegion** 값은 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치를 지정합니다(예: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` 또는 `BMSClient.Region.sydney`). 


## Cordova 애플리케이션 초기화
{: #init-BMSClient-cordova}

1. Cordova 애플리케이션 루트 디렉토리에서 다음 명령을 실행하여 Cordova 플러그인을 추가하십시오. 

  ```
  cordova plugin add bms-core
  ```
  {: codeblock}

2. 기본 JavaScript 파일에서나 프로젝트에 대해 최적으로 작동하는 위치에서 초기화 코드를 추가하여 Cordova 애플리케이션에서 `BMSClient` 클래스를 초기화하십시오. 

  ```
  BMSClient.initialize(BMSClient.REGION_US_SOUTH);
  ```
  {: codeblock}
	
  **bluemixRegion** 매개변수를 사용하여 `BMSClient`를 초기화해야 합니다. 초기자(initializer)에서 **bluemixRegion** 값은 사용 중인 {{site.data.keyword.Bluemix_notm}} 배치를 지정합니다(예: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` 또는 `BMSClient.REGION_SYDNEY`). 


# 관련 링크
{: #rellinks notoc}

## 관련 링크
{: #general notoc}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova 플러그인](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
