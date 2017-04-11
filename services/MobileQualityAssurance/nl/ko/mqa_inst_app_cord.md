---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cordova 앱을 사용하여 MQA 인스트루먼트(더 이상 사용되지 않음)
{: #instrumentcord}

{{site.data.keyword.mqafull}}를 Cordova 앱과 함께 사용하려면, SDK를 다운로드하고 명령행 인터페이스로 몇 가지 변경사항을 작성하여 이를 인스트루먼트해야 합니다.
{: shortdesc}

{{site.data.keyword.mqa}}를 사용하여 앱을 인스트루먼트할 수 있으려면 {{site.data.keyword.Bluemix}} 계정이 있어야 하며 인스트루먼트하는 앱의 플랫폼에 대한 배치 환경의 버전이 올바르게 설치되어 있어야 합니다. 

Cordova 앱과 작동하도록 {{site.data.keyword.mqa}}를 인스트루먼트하려면, 다음 태스크를 완료하십시오. 

1. 필수 권한 및 다운로드한 SDK를 Cordova 프로젝트에 추가하십시오. 

	1. 명령 프롬프트를 열고 프로젝트 파일을 포함하는 디렉토리로 이동하십시오. 

	2. 사용자 환경에 따라 다음 단계를 완료하여 {{site.data.keyword.mqa}} 플러그인을 Cordova 프로젝트에 추가하십시오. 

		**중요**: iOS 9에서 Xcode 7.x를 사용 중인 경우 Xcode 빌드 설정에서 비트코드 사용(Enable Bitcode) 값을 아니오로 설정해야 합니다. platform\iPhone 폴더에 있는 Cordova 프로젝트 파일 .xcodeproj를 사용하여 Xcode를 열어서 이 설정을 변경할 수 있습니다. 

		* IBM MobileFirst™ Platform Foundation 버전 7.1:

			1. {{site.data.keyword.mqa}} 플러그인을 설치하려면 다음 명령을 입력하십시오. 

				```
				mfp cordova plugin add plugin_location
				```
				{: codeblock}

			여기서 *plugin_location*은 다운로드한 {{site.data.keyword.mqa}} 플러그인을 추출한 디렉토리의 경로입니다. 

			2. 앱을 Android에서 실행하는 경우 `project_name/app_name/platforms/android/custom_rules.xml` 파일의 이름을 `custom_rules.xml.bak`로 변경하십시오. 

		* Apache Cordova 버전 4.0 미만:
			1. {{site.data.keyword.mqa}} 플러그인을 설치하려면 다음 명령을 입력하십시오. 

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			여기서 *plugin_location*은 다운로드한 {{site.data.keyword.mqa}} 플러그인을 추출한 디렉토리의 경로입니다. 

			2. 추가적인 필수 플러그인을 추가하려면 다음 명령을 입력하십시오. 

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. 앱을 Android에서 실행하는 경우 `project_name/app_name/platforms/android/custom_rules.xml` 파일의 이름을 `custom_rules_bak.xml`로 변경하십시오. 

		* Apache Cordova 버전 4.0 이상: 

			1. 다음 명령을 입력하십시오. 

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			여기서 *plugin_location*은 다운로드한 {{site.data.keyword.mqa}} Cordova 플러그인을 추출한 디렉토리의 경로입니다. 

			2. 추가적인 필수 플러그인을 추가하려면 다음 명령을 입력하십시오. 

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. 로그인할 때마다 {{site.data.keyword.mqa}}의 새 세션을 시작하십시오. 

	1. 다음 `your_project_name\www\js` 디렉토리에 있는 `index.js` 파일을 여십시오. 

	2. 다음 함수 및 매개변수를 `index.js` 파일에 있는 `onDeviceReady()` 함수 내부에 추가하십시오. 함수의 닫는 중괄호 앞에 해당 함수를 배치하십시오. 

	제한사항: Cordova 버전 3.0.18 이상을 위한 Mobile Quality Assurance 플러그인에 포함되어 있는 기능을 사용하기 위해 이전 버전의 Cordova용 플러그인을 사용하여 Mobile Quality Assurance에 대해 이미 인스트루먼트된 앱의 경우, 앱 키를 재생성한 후 대체해야 합니다. 앱 키 재생성 방법에 대한 자세한 정보는 앱 설정 관리를 참조하십시오. 2016년 2월 이전에 생성된 앱 키는 이전 플러그인에 대해 계속 작동되지만, 버전 3.0.18 이상으로 플러그인을 업그레이드한 후에는 더 이상 작동하지 않습니다. 

		```
		MQA.startNewSession(
			{
				mode: "QA",
				// or mode: "MARKET" for production mode.
			android: {
				appKey: "your_MQA_Android_appKey" ,
				notificationsEnabled: true},
			ios: {
				appKey: "your_MQA_iOS_appKey" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session
			   Started successfully");},
			error: function (string) { console.log("Session
			   error" + string);}
			}
			);
		```
		{: codeblock}

	3. [{{site.data.keyword.mqa}} 시작하기](index.html)의 단계를 계속하십시오. 



# 관련 링크
{: #rellinks notoc}

## 관련 링크
{: #general notoc}
* [{{site.data.keyword.mqa}} 시작하기](index.html){:new_window}
