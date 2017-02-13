---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# iOS용 Hello Bluemix 샘플 시작하기
{: #gettingstarted-android}
마지막 업데이트 날짜: 2016년 6월 1일
{: .last-updated}  

새 iOS 앱을 시작하고자 하는 경우 Hello Bluemix 앱을 사용할 수 있습니다. 이 앱에서는 인증 없이 모바일 앱에서 {{site.data.keyword.Bluemix}} 백엔드에 연결하는 방법을 예시합니다. 준비가 완료되면 사용자는 앱에서 사용할 특정 라이브러리를 가져올 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}}에서 모바일 백엔드를 작성하십시오.
    1. {{site.data.keyword.Bluemix_notm}} 카탈로그의 표준 유형 섹션에서 MobileFirst Services 스타터를 클릭하십시오.
    2. 앱에 대한 이름 및 호스트를 입력하고 **작성**을 클릭하십시오.
    3. **완료**를 클릭하십시오.
2. Hello Bluemix 샘플 애플리케이션을 실행하십시오.
	1. GitHub에서 프로젝트를 가져오십시오. 선택에 따라 git clone 명령을 사용하여 프로젝트를 가져올 수도 있습니다. 컴퓨터에서 터미널을 열고, 다음 명령을 입력하십시오.
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. 프로젝트가 복제된 `bms-samples-swift-hellobluemix` 디렉토리 내에서 `pod install` 명령을 실행하십시오. Cocoapods가 설치되어 있지 않은 경우 [https://cocoapods.org](https://cocoapods.org)에서 가져오십시오.
	3. `open HelloBluemix.xcworkspace` 명령을 사용하여 Xcode 작업공간을 여십시오.
	4. `AppDelegate.swift` 파일에서, appRoute 및 appGuid 값을 이전에 작성한 Bluemix 백엔드에서 확보한 값으로 업데이트하십시오.

3. 개발 환경에서 샘플을 실행하십시오. Xcode에서 **Product &gt; Run**을 클릭하십시오. iOS 시뮬레이터가 시작됩니다.

	**중요:** appRoute는 `http`가 아닌 `https` 프로토콜을 사용해야 합니다. 그렇지 않으면, 앱 전송 보안 설정으로 인해 연결에 실패할 수 있습니다. [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/) 블로그 게시물에서 이러한 설정에 대해 자세히 살펴볼 수 있습니다.
	
4. 시뮬레이터에서 **Ping {{site.data.keyword.Bluemix_notm}}**를 클릭하십시오. 샘플 앱이 Mobile Client Access 서비스에서 권한 부여 헤더를 가져옵니다. ping 실행이 성공하면 시뮬레이터의 텍스트가 업데이트됩니다.

  Xcode의 모바일 앱에서 {{site.data.keyword.Bluemix_notm}}에 연결하면 다음이 표시됩니다.
  `Yay! You are connected`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  연결이 실패하면 다음이 표시됩니다.
  `Bummer. Something went wrong`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

	다음과 같이 실패한 연결의 문제점을 해결할 수 있습니다. 
	* 라우트 및 GUID 값을 올바로 붙여넣었는지 확인하십시오.
	* 자세한 정보는 디버그 로그를 검토하십시오. 


## 다음 단계:
{: #next}
SDK를 가져와 모바일 앱에 통합하는 방법에 대한 정보는 Bluemix 서비스 설정에 대한 정보를 참조하십시오.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## 샘플
   * [Hello Bluemix 샘플(iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## SDK
   * [코어 SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## API
   * [코어 API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
