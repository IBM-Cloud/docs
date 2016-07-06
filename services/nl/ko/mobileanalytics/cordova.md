<!-- Attribute definitions -->
{:codeblock: .codeblock}

# HelloWorld 샘플 시작하기
{: #gettingstarted-cordova}

새 Cordova 애플리케이션을 시작하려면 HelloWorld 앱을 사용할 수 있습니다. 이 앱은 인증 없이 모바일 앱에서 Bluemix 백엔드에 연결하는 방법을 보여줍니다. 앱에는 이미 SDK가 설치되어 있습니다. 준비가 되었으면 앱에서 사용할 특정 라이브러리를 가져올 수 있습니다.

1. Bluemix에서 모바일 백엔드를 작성하십시오.
<ol>
	<li>표준 유형 섹션 Bluemix 카탈로그에서 MobileFirst Services Starter를 클릭하십시오.</li>
    	<li>앱에 대한 이름 및 호스트를 입력하고 **작성**을 클릭하십시오.</li>
    	<li>**완료**를 클릭하십시오.</li>
</ol>
2. GitHub에서 프로젝트를 가져오십시오. 필요에 따라 git clone 명령을 사용하여 프로젝트를 가져올 수 있습니다. 컴퓨터에서 터미널을 열고 다음 명령을 입력하십시오. 
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
```

3. 프로젝트 디렉토리에서 다음 명령을 실행하여 Android 및 iOS 플랫폼 환경을 추가하십시오.

Android:

```
cordova platform add android
```

iOS:

```
cordova platform add ios
```

4. 다음 명령을 사용하여 Cordova 플러그인을 추가하십시오. 
```
cordova plugin add ibm-mfp-core
```

5. Android, iOS 또는 둘 다에 대해 Cordova 앱을 구성하십시오.

 * Android

	 Android Studio에서 프로젝트를 열기 전에 명령행 인터페이스(CLI)를 통해 Cordova 애플리케이션을 빌드하고 실행하여 빌드 오류를 방지하십시오.

	 ```
	 cordova build android
	 ```

	 ```
	 cordova run android
	 ```

 * iOS

	 Xcode 프로젝트를 다음과 같이 구성하여 빌드 오류를 방지하십시오.

	    1. 최신 버전의 Xcode를 사용하여 &lt;app_name&gt;/platforms/ios 디렉토리에서 xcode.proj 파일을 여십시오.

			**중요:** "최신 Swift 구문으로 변환" 메시지를 수신하면 취소를 클릭하십시오.

		2. **빌드 설정 > Swift 컴파일러 - 코드 생성 > Objective-C Bridging Header**로 이동하여 다음 경로를 추가하십시오.

		```
		<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
		```
		3. **빌드 설정 > 링크 > Runpath Search Paths**로 이동하여 다음 프레임워크 매개변수를 추가하십시오.

		```
		@executable_path/Frameworks
		```
		4. Xcode를 사용하여 애플리케이션을 빌드하고 실행하십시오.

6. HelloWorld 샘플 구성
<ol>
	<li>프로젝트를 복제한 디렉토리로 변경하십시오.</li>
	<li>&lt;your_app_dir&gt;/www/js/index.js 파일을 열고 &lt;APPLICATION_ROUTE&gt; 및 &lt;APPLICATION_ID&gt;를 Bluemix 애플리케이션 ID 및 라우트 값으로 대체하십시오.</li>
</ol>

참고: &lt;APPLICATION_ROUTE&gt;가 https 프로토콜을 사용하여 보안되는지 확인하십시오.

```
// Bluemix credentials
route: "<APPLICATION_ROUTE>",
GUID: "<APPLICATION_GUID>",
```

7. 모바일 에뮬레이터 또는 디바이스에서 샘플을 실행하십시오.

   다음 명령을 사용하여 Cordova 앱을 빌드하십시오.
	 ```
	 cordova build ios
	 ```
	 ```
	 cordova build android
	 ```

   다음 명령을 사용하여 샘플 앱을 실행하십시오.
	 ```
	 cordova run ios
	 ```
   ```
	 cordova run android
	 ```


**PING BLUEMIX** 단추가 있는 단일 보기 애플리케이션이 표시됩니다. 단추를 누르면 애플리케이션이 클라이언트에서 백엔드 Bluemix 애플리케이션으로의 연결을 테스트합니다. index.js 파일에서 지정하는 애플리케이션 라우트를 사용하여 연결이 테스트됩니다.


![Hello World 애플리케이션이 Bluemix에 연결됨](images/yayconnected.jpg "그림 1. Hello World 애플리케이션이 Bluemix에 연결됨")

모바일 앱에서 Bluemix에 연결되면 "연결되었습니다."를 나타내는 메시지가 표시됩니다.
8. 모든 문제를 해결하십시오.

<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

연결이 실패하면 "문제점이 발생했습니다."라는 메시지가 표시됩니다. 오류에 대한 자세한 정보가 포함됩니다.
다음 항목을 확인하십시오. 
 * 라우트 및 GUID 값을 올바르게 붙여넣었는지 확인하십시오.
 * Xcode 또는 Android 디버그 로그를 보십시오.
 * Bluemix 내의 앱 상태를 확인하십시오.

## 다음 단계:
{: #next}
SDK를 가져와서 모바일 앱에 통합하는 방법에 대한 정보는 Cordova 클라이언트 SDK 설정을 참조하십시오.

# 관련 링크

## 샘플
   * [HelloWorld(Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
