---

copyright:
  years: 2015, 2016

---
<!-- Attribute definitions -->
{:codeblock: .codeblock}

# HelloWorld 샘플 시작하기
{: #gettingstarted-cordova}
*마지막 업데이트 날짜: 2016년 3월 17일*

새 Cordova 애플리케이션을 시작하고자 하는 경우 HelloWorld 앱을 사용할 수 있습니다. 이 앱에서는 인증 없이 모바일 앱에서 {{site.data.keyword.Bluemix}}의 모바일 백엔드에 연결하는 방법을 예시합니다. 앱에는 이미 SDK가 설치되어 있습니다. 준비가 완료되면 사용자는 앱에서 사용할 특정 라이브러리를 가져올 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}}에서 모바일 백엔드를 작성하십시오.

	1. {{site.data.keyword.Bluemix_notm}} 카탈로그의 표준 유형 섹션에서 MobileFirst Services 스타터를 클릭하십시오.
	1. 앱에 대한 이름 및 호스트를 입력하고 **작성**을 클릭하십시오.
	1. **완료**를 클릭하십시오.

2. GitHub에서 프로젝트를 가져오십시오. git clone 명령을 사용하여 프로젝트를 가져올 수 있습니다. 컴퓨터에서 터미널을 열고, 다음 명령을 입력하십시오.

	```Bash
	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
	```

3. 프로젝트 디렉토리에서 다음 명령을 실행하여 Android 및 iOS 플랫폼 환경을 추가하십시오.

	### Android

	```Bash
	cordova platform add android
	```

	### iOS

	```Bash
	cordova platform add ios
	```

4. 다음 명령으로 Cordova 플러그인을 추가하십시오.

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. HelloWorld 샘플을 구성하십시오.

	* 프로젝트를 복제한 디렉토리로 변경하십시오.
	* *&lt;your_app_dir&gt;*/www/js/index.js 파일을 열고 *&lt;APPLICATION_ROUTE&gt;* 및 *&lt;APPLICATION_ID&gt;*를 사용자의 Bluemix 애플리케이션 ID 및 라우트 값으로 바꾸십시오.

		**참고:** 라우트가 안전하게 https 프로토콜을 사용 중인지 확인하십시오.

		```Javascript
		// Bluemix credentials
		route: "<APPLICATION_ROUTE>",
		GUID: "<APPLICATION_GUID>",
		```

6. iOS용 Cordova 앱을 구성하십시오. Android 플랫폼에서는 추가 구성이 필요하지 않습니다.

	### iOS
  다음과 같이 Xcode 프로젝트를 구성하여 빌드 오류를 방지하십시오.

	1. 최신 Xcode 버전을 사용하여 *&lt;app_name&gt;*/platforms/ios 디렉토리에서 `xcode.proj` 파일을 여십시오.

		**중요:** "Convert to Latest Swift Syntax" 메시지를 수신하는 경우 **Cancel**을 클릭하십시오.

	2. **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header**로 이동하여 다음 경로를 추가하십시오.

		```
		<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
		```

	3. **Build settings > Linking > Runpath Search Paths**로 이동하여 다음 프레임워크 매개변수를 추가하십시오.

		```
		@executable_path/Frameworks
		```

7. 모바일 에뮬레이터 또는 디바이스에서 샘플을 빌드하고 실행하십시오.

  ### Android
	1. 다음 명령을 사용하여 Cordova 앱을 빌드하십시오.

    **중요:** Android Studio에서 프로젝트를 열기 전에, 우선 Cordova 명령행 인터페이스(CLI)를 통해 Cordova 애플리케이션을 빌드해야 합니다. 그렇지 않으면, 빌드 오류가 발생합니다.

	```Bash
	cordova build android
	```

	2. Android Studio에서 샘플 앱을 실행하십시오.

  ### iOS
  1. Xcode에서 Cordova 앱을 빌드하십시오.

    **팁:** Xcode에서 빌드하면 디버깅, 프로젝트 구성과 같은 추가 옵션을 사용할 수 있습니다.

  2. Xcode에서 샘플 앱을 실행하십시오.

**PING BLUEMIX** 단추가 있는 단일 보기 애플리케이션이 표시됩니다. 단추를 누르면 애플리케이션이 클라이언트에서 백엔드 {{site.data.keyword.Bluemix_notm}} 애플리케이션으로의 연결을 테스트합니다. `index.js` 파일에 지정한 애플리케이션 라우트를 사용하여 연결을 테스트합니다.


![Hello World 애플리케이션이 Bluemix에 성공적으로 연결됨](images/yayconnected.jpg "그림 1. Hello World 애플리케이션이 Bluemix에 성공적으로 연결됨")


모바일 앱에서 {{site.data.keyword.Bluemix_notm}}에 연결되면 "Yay! You are connected"라는 메시지가 표시됩니다.


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

연결이 실패하면 오류 메시지가 표시됩니다. 오류에 대한 자세한 정보가 메시지에 포함되어 있습니다. 다음 항목을 확인하여 오류의 문제점을 해결할 수 있습니다.

- 라우트 및 GUID 값을 올바로 붙여넣었는지 확인하십시오.
- Xcode 또는 Android 디버그 로그를 보십시오.
- {{site.data.keyword.Bluemix_notm}}에서 앱의 상태를 확인하십시오.

## 다음 단계:
{: #next}
SDK를 가져와서 모바일 앱에 통합하는 방법에 대한 정보는 다음을 참조하십시오.
* [Mobile Client Access: Cordova 플러그인 설정](../../services/mobileaccess/getting-started-cordova.html)
* [Push Notifications: Cordova 플러그인 설정](../../services/mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# 관련 링크

## 샘플
   * [HelloWorld(Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## SDK
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
