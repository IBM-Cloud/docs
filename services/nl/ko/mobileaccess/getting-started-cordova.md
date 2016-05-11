---

copyright:
  years: 2015, 2016
  
---

# Cordova 플러그인 설정
{: #getting-started-cordova}

{{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 Cordova 애플리케이션을 계측하고, SDK를 초기화하고, 보호 및 비보호 자원에 대한 요청을 작성하십시오. 

## 시작하기 전에
{: #before-you-begin}

- {{site.data.keyword.amashort}} 서비스에서 보호하는 모바일 백엔드의 인스턴스가 있어야 합니다. 모바일 백엔드 작성 방법에 대한 자세한 정보는 [시작하기](getting-started.html)를 참조하십시오. 

- Cordova 애플리케이션을 작성하거나 기존 프로젝트를 사용하십시오. Cordova 애플리케이션을 설정하는 방법에 대한 자세한 정보는 [Cordova 웹 사이트](https://cordova.apache.org/)를 참조하십시오. 

## {{site.data.keyword.amashort}} Cordova 플러그인 설치
{: #getting-started-cordova-plugin}

Cordova용 {{site.data.keyword.amashort}} 클라이언트 SDK는 원시 {{site.data.keyword.amashort}} 클라이언트 SDK를 랩핑하는 Cordova 플러그인입니다. Cordova CLI(Command Line Interface) 및 `npmjs`, Cordova 프로젝트에 대한 플러그인 저장소를 사용하여 분배됩니다. Cordova CLI는 저장소에서 플러그인을 자동으로 다운로드하고 Cordova 애플리케이션에서 플러그인을 사용할 수 있게 합니다. 

1. Android 및 iOS 플랫폼을 Cordova 애플리케이션에 추가하십시오. 명령행에서 다음 명령 중 하나 또는 둘 다 실행하십시오. 

	```Bash
	cordova platform add android
	```

	```Bash
	cordova platform add ios
	```

1. Android 플랫폼을 추가한 경우 지원되는 최소 API를 Cordova 애플리케이션의 `config.xml` 파일에 추가해야 합니다. `config.xml` 파일을 열고 `<platform name="android">` 요소에 다음 행을 추가하십시오. 

	```XML
	<platform name="android">    
		<preference name="android-minSdkVersion" value="15"/>
		<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	*minSdkVersion* 값은 `15`보다 커야 합니다. *targetSdkVersion* 값은 Google에서 사용 가능한 최신 Android SDK여야 합니다.



1. iOS 운영 체제를 추가한 경우 `<platform name="ios">` 요소를 대상 선언으로 업데이트하십시오. 

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	</platform>
	```

1. {{site.data.keyword.amashort}} Cordova 플러그인을 설치하십시오. 

 	```Bash
	cordova plugin add ibm-mfp-core```

1. Android, iOS 또는 둘 다에 대해 플랫폼을 구성하십시오.

	* **Android**

		Android Studio에서 프로젝트를 열기 전에 빌드 오류를 방지하기 위해 명령행 인터페이스(CLI)를 통해 Cordova 애플리케이션을 빌드하십시오.

		```
		cordova build android
		```

	* **iOS**

		다음과 같이 Xcode 프로젝트를 구성하여 빌드 오류를 방지하십시오.

		1. 최신 Xcode 버전을 사용하여 &lt;*app_name*&gt;/platforms/ios 디렉토리에서 xcode.proj 파일을 여십시오.

		**중요:** "최신 Swift 구문으로 변환"에 대한 메시지를 수신하는 경우 취소를 클릭하십시오.

		2. **빌드 설정 > Swift 컴파일러 - 코드 생성 > Objective-C 브리징 헤더**로 이동하여 다음 경로를 추가하십시오.

			```
			<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		3. **빌드 설정 > 링크 > Runpath 검색 경로**로 이동하여 다음 프레임워크 매개변수를 추가하십시오.

			```
			@executable_path/Frameworks
			```

		4. Xcode로 애플리케이션을 빌드하고 실행하십시오.

1. 다음 명령을 실행하여 플러그인이 올바르게 설치되었는지 확인하십시오.
    

	```Bash
	cordova plugin list
	```

## {{site.data.keyword.amashort}} 클라이언트 플러그인 초기화
{: #getting-started-cordova-initialize}

{{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려면, *applicationGUID* 및 *applicationRoute* 매개변수를 전달하여 SDK를 초기화해야 합니다. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드의 기본 페이지에서 라우트 및 앱 GUID 값을 찾으십시오. SDK를 초기화하려면 앱 이름을 클릭한 다음 **애플리케이션 라우트** 및 **애플리케이션 GUID** 값을 표시하도록 **모바일 옵션**을 클릭하십시오. 

3. {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하려면 `index.js` 파일에 다음 호출을 추가하십시오. *applicationRoute* 및 *applicationGUID*를 {{site.data.keyword.Bluemix_notm}} 대시보드의 **모바일 옵션** 값으로 바꾸십시오.

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

## 모바일 백엔드에 대한 요청 작성
{: #getting-started-request}

{{site.data.keyword.amashort}} 클라이언트 SDK가 초기화되면 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다. 

1. 요청을 새 모바일 백엔드의 보호 엔드포인트로 전송하십시오. 브라우저에서 URL `{applicationRoute}/protected`를 여십시오. 예를 들면 다음과 같습니다.


	```
	http://my-mobile-backend.mybluemix.net/protected
	```

	MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호됩니다. 브라우저에 `Unauthorized` 메시지가 리턴됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 계측되는 모바일 애플리케이션에서만 액세스하기 때문에 이 메시지가 리턴됩니다.



1. Cordova 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. `BMSClient`를 초기화한 후에 다음 코드를 추가하십시오. 

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
		console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);```

1. 요청에 성공하는 경우 LogCat 또는 Xcode 콘솔에 다음 출력이 표시됩니다(사용 중인 플랫폼에 따라 다름). 

	![이미지](images/getting-started-android-success.png)

	## 다음 단계
	{: #next-steps}

	보호 엔드포인트에 연결된 경우 신임 정보는 필요하지 않습니다. 사용자가 애플리케이션에 로그인하게 하려면 Facebook, Google 또는 사용자 정의 인증을 구성해야 합니다. 
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [사용자 정의 ](custom-auth-cordova.html)
