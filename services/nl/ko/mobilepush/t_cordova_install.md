---

copyright:
 years: 2015, 2016

---

# Cordova 푸시 플러그인 설치
{: #cordova_install}

클라이언트 푸시 플러그인을 설치하고 이를 사용하여 추가적으로 Cordova 애플리케이션을 개발할 수 있습니다. 이 때 사용자와 Bluemix의 연결을 초기화하는 Cordova 코어 플러그인도 설치됩니다. 

### 시작하기 전에

1. 최신 Android Studio SDK 및 Xcode 버전을 다운로드하십시오. 
1. 에뮬레이터를 설정하십시오. Android Studio의 경우 Google Play API를 지원하는 에뮬레이터를 사용하십시오.
1. Git 명령행 도구를 설치하십시오. Windows의 경우 **Window 명령 프롬프트에서 Git 실행** 옵션을 선택하십시오. 이 도구의 다운로드 및 설치에 대한 정보는 [Git](https://git-scm.com/downloads)을 참조하십시오.

1. Node.js 및 NPM(Node Package Manager) 도구를 설치하십시오. NPM 명령행 도구는 Node.js와 함께 번들로 제공됩니다. Node.js를 다운로드하고 설치하는 방법에 대한 정보는 [Node.js](https://nodejs.org/en/download/)를 참조하십시오. 
1. 명령행에서 **npm install -g cordova** 명령을 사용하여 Cordova 명령행 도구를 설치하십시오. Cordova 푸시 플러그인을 사용하려면 필요합니다. Cordova 설치 및 Cordova 앱 설정 정보를 보려면 [Cordova Apache](https://cordova.apache.org/#getstarted)를 참조하십시오. 

	**참고**: Cordova 푸시 플러그인 Readme 파일을 보려면 [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)로 이동하십시오. 


## Cordova 푸시 플러그인 설치
1. Cordova 앱을 작성하려는 폴더로 변경하고 다음 명령을 실행하여 Cordova 애플리케이션을 작성하십시오. 기존의 Cordova 앱이 있을 경우 3단계로 가십시오. 


	cordova create your_app_name
	cd your_app_name
	```
1. 선택사항: **config.xml** 파일을 편집하고 <name> 요소에서 애플리케이션 이름을 기본값인 HelloCordova 이름 대신 원하는 이름으로 변경하십시오. 

	**참고**: 올바른 번들 ID를 지정하십시오. 그렇지 않은 경우 다음 오류 메시지가 Xcode에 표시됩니다.
	* 실행 파일이 올바르지 않은 인타이틀먼트로 서명되었습니다.
	* 애플리케이션의 코드 서명 인타이틀먼트에 지정된 인타이틀먼트가 프로비저닝 프로파일에 지정된 인타이틀먼트와 일치하지 않습니다.

	이 문제를 수정하려면 Xcode 또는 Cordova 앱 **config.xml** 파일에서 올바른 번들 ID를 지정하십시오. 

1. Corova 애플리케이션의 config.xml 파일에 최소 지원 API 또는 배치 대상 선언을 추가하십시오. minSdkVersion 값은 15보다 커야 합니다. targetSdkVersion 값은 항상 Google을 통해 제공받을 수 있는 최신 Android SDK를 반영해야 합니다. 
	* **Android** - 편집기에서 config.xml 파일을 열어
```<platform name="android">``` 요소를 최소 및 대상 SDK 버전으로 업데이트하십시오. 

	```
	<!-- add deployment target declaration -->
	<platform name="android">    
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - 배치 대상 선언으로 <platform name="ios"> 요소를 업데이트하십시오.


	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Cordova 명령행 인터페이스(CLI)에서 다음 명령을 사용하여 플랫폼(iOS, Android 또는 둘 다)을 추가하십시오.

	```
	cordova platform add ios
	cordova platform add android
	```
1. Cordova 애플리케이션 루트 디렉토리에서 다음 명령을 입력하여 Cordova 푸시 플러그인을 설치하십시오. **cordova plugin add ibm-mfp-push**

	추가한 플랫폼에 따라 다음과 유사하게 표시됩니다. 

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. *your-app-root-folder*에서 다음 명령을 사용하여 Cordova 코어 및 푸시 플러그인이 정상적으로 설치되었는지 확인하십시오. **cordova plugin list**

	추가한 플랫폼에 따라 다음과 유사하게 표시됩니다. 

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (iOS만 해당) - iOS 개발 환경을 구성하십시오.
	a. Xcode가 있는 *your-app-name***/platforms/ios** 디렉토리에서 your-app-name.xcodeproj 파일을 여십시오. 

	b. 브릿지 헤더를 추가하십시오. **빌드 설정 > Swift 컴파일러 - 코드 생성 > Objective-C 브릿지 헤더**로 이동하여 다음 경로를 추가하십시오. *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. 프레임워크 매개변수를 추가하십시오. **빌드 설정 > 링크 > Runpath 검색 경로**로 이동하여 다음 매개변수를 추가하십시오.
	```
	@executable_path/Frameworks
	```
	d. 브릿지 헤더에서 다음 푸시 가져오기 명령을 주석 해제하십시오. *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**로 이동하십시오. 

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Xcode를 사용하여 애플리케이션을 빌드하고 실행하십시오.
1. (Android만 해당) - 다음 명령을 사용하여 Android 프로젝트를 빌드하십시오.
**cordova build android**.

	**참고**: Android Studio에서 프로젝트를 열기 전에 먼저 Cordova CLI를 통해 Cordova 애플리케이션을 빌드해야 합니다. 그렇지 않으면 빌드 오류가 발생합니다. 

1. 다음 단계. [Cordova 플러그인 초기화](t_cordova_initalize.html).
