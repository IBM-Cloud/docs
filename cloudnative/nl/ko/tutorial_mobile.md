---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 모바일 기본 스타터의 엔드-투-엔드 튜토리얼
{: #tutorial}

다음의 엔드-투-엔드 튜토리얼에서는 모바일 기본 스타터에서 프로젝트를 작성하는 단계를 안내합니다. 여기에는 전제조건 도구의 설치와  Xcode 및 Android Studio에서 프로젝트를 실행하는 단계가 포함됩니다. 

웹 기반 [{{site.data.keyword.dev_console}}](#create-devex)을 사용하거나 명령어 방식 [{{site.data.keyword.dev_cli_notm}}](#create-cli)을 통해 프로젝트를 작성할 수 있습니다. 

## 개발자 도구 설치
{: #dev_tools}

[전제조건 개발자 도구 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](get_code.html#prereq-dev-tools){: new_window}를 설치했는지 확인하십시오. 


## {{site.data.keyword.dev_console}}을 사용하여 프로젝트 작성
{: #create-devex}

1. {{site.data.keyword.Bluemix}}에서 {{site.data.keyword.dev_console}} 프로젝트를 작성하십시오. 

   1. {{site.data.keyword.dev_console}}의 [**시작하기** ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/developer/getting-started/) 페이지에서 **프로젝트 작성**을 클릭하십시오. 

      또는 **프로젝트** 페이지에서 **프로젝트 작성**을 클릭할 수 있습니다. 

   2. **모바일 앱**을 선택하고 **다음**을 클릭하십시오. 

   3. **기본**을 선택하고 **다음**을 클릭하십시오. 

   4. 프로젝트 이름을 입력하십시오. 이 튜토리얼의 경우 `MobileBasicProject`를 사용하십시오. 

   5. 플랫폼을 선택하십시오. 이 튜토리얼의 경우 `Swift`를 사용하십시오. 
   
   6. **작성**을 클릭하십시오.

2. 선택사항: 인증 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 **인증**에 대해 **추가**를 클릭하십시오. 

      **기능 > 인증** 페이지에서 **작성** 또는 **기존 추가**를 선택할 수도 있습니다. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 
   
   3. **인증**을 토글하여 켜십시오. 
   
   4. ID 제공자를 선택하고 이를 구성하기 위한 정보를 입력하십시오. 하나의 ID 제공자만 사용 가능하게 설정할 수 있습니다. 
   
   5. 인증 구성에 대한 자세한 정보는 [ID 제공자 구성 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/appid/identity-providers.html){: new_window}을 참조하십시오. 

3. 선택사항: 분석 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 **분석**에 대해 **추가**를 클릭하십시오. 

      **기능 > 분석** 페이지에서 **작성** 또는 **기존 추가**를 클릭할 수도 있습니다. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 
   
   3. 앱을 실행한 후 분석 데이터를 보려면 **데모 모드**를 토글하여 끄십시오. 
   
   4. 분석 구성에 대한 자세한 정보는 [{{site.data.keyword.mobileanalytics_short}} 시작하기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobileanalytics/index.html){: new_window}를 참조하십시오. 

4. 선택사항: {{site.data.keyword.mobilepushshort}} 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 **{{site.data.keyword.mobilepushshort}}**에 대해 **추가**를 클릭하십시오. 

      **기능 > {{site.data.keyword.mobilepushshort}}** 페이지에서 **작성** 또는 **기존 추가**를 클릭할 수도 있습니다. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 

   3. iOS의 경우, [Apple Push Notification Service 구성 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}을 수행하십시오. 

   4. Android의 경우, [FCM(Firebase Cloud Messaging) 구성 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}을 수행하십시오. 

5. 선택사항: 데이터 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 **데이터**에 대한 **보기**를 클릭하십시오. 

      또는 **데이터** 페이지에서 **작성**을 선택할 수 있습니다. 
      
   2. **{{site.data.keyword.cloudant_short_notm}}** 또는 **{{site.data.keyword.objectstorageshort}}**를 선택하십시오. 

   3. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 

   4. {{site.data.keyword.cloudant_short_notm}} 구성에 대한 자세한 정보는 [{{site.data.keyword.cloudant_short_notm}} 시작하기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/Cloudant/index.html){: new_window}를 참조하십시오. 

   5. {{site.data.keyword.objectstorageshort}} 구성에 대한 자세한 정보는 [{{site.data.keyword.objectstorageshort}} 시작하기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/ObjectStorage/index.html){: new_window}를 참조하십시오. 

6. 프로젝트 코드를 생성하십시오. 

   1. **프로젝트 개요** 페이지에서 **코드 가져오기**를 클릭하여 언어를 선택하십시오. 
   
      또는 **코드** 페이지를 클릭할 수 있습니다.
      
   2. **Swift 생성**을 클릭하십시오. 
   
   3. 프로젝트 코드 생성이 완료되면 **Swift 다운로드**를 클릭하여 프로젝트 아카이브를 다운로드하십시오. 

7. 다운로드된 프로젝트 관련 작업을 시작하십시오. 

	1. 아카이브된 파일을 펼치십시오. 
	
	2. 새 프로젝트 디렉토리로 이동하십시오. 
	
	3. {{site.data.keyword.dev_cli_notm}}을 사용하여 계속 진행하십시오. 

8. 선택사항: 새 언어를 생성하도록 [프로젝트를 업데이트하십시오](project_overview_page.html#update_language). 


## {{site.data.keyword.dev_cli_notm}}을 사용하여 프로젝트 작성
{: #create-cli}

1. [{{site.data.keyword.dev_cli_short}}](dev_cli.html)을 설치해야 합니다. 

2. 터미널 프롬프트에서 원하는 로컬 디렉토리로 이동하여 다음 명령을 실행하십시오. 

	```
	bx dev create
	```
	{: codeblock}
	
3. 프롬프트가 표시되면 다음 값을 제공하십시오. 

	* 패턴 선택: 2(모바일)
	* 스타터 선택: 1(기본)
	* 플랫폼 선택: 3(iOS Swift)
	* 프로젝트의 이름 입력: `MobileBasicProjectCLI`

4. 프로젝트에 서비스를 추가하려면 질문 프롬프트에서 `y`를 입력하고 나머지 질문에 응답하십시오. 

5. `MobileBasicProjectCLI`가 정상적으로 저장되면 `MobileBasicProjectCLI/MobileBasicProjectCLI-Swift` 폴더로 이동하십시오. 


## Xcode에서 Swift 프로젝트 실행
{: #run_swift}

1. `MobileBasicProject-Swift.zip` 파일의 압축을 푸십시오. 

2. Markdown 뷰어에서 `README.md` 파일을 열어 프로젝트를 구성하는 단계를 검토하십시오. 

   1. 터미널을 열고 프로젝트 폴더로 이동하십시오. 
   
      1. CocoaPods 저장소를 설정해야 하는 경우 `pod setup`을 실행하십시오. 
      
      2. 기존 pod를 업데이트해야 하는 경우 `pod update`를 실행하십시오. 
      
      3. 프로젝트에 필요한 pod를 설치하려면 `pod install`을 실행하십시오.
      
   3. `BasicProject.xcworkspace` Xcode 작업공간을 여십시오.
      
3. 앱을 실행하십시오. 


## Xcode에서 Cordova 프로젝트 실행
{: #run_cordova_xcode}

1. `MobileBasicProject-Cordova.zip` 파일의 압축을 푸십시오. 

2. Markdown 뷰어에서 `README.md` 파일을 열어 프로젝트를 구성하십시오. 

   1. Xcode에서 `platforms/ios` 프로젝트를 여십시오.
      
3. 앱을 실행하십시오. 


## Android Studio에서 Cordova 프로젝트 실행
{: #run_cordova_studio}

1. `BasicProject-Cordova.zip` 파일의 압축을 푸십시오.

2. Markdown 뷰어에서 `README.md` 파일을 열어 프로젝트를 구성하십시오. 

   1. Android Studio에서 `platforms/android` 프로젝트를 여십시오.
      
3. 앱을 실행하십시오. 


## Android Studio에서 Android 프로젝트 실행
{: #run_android}

1. `MobileBasicProject-Android.zip` 파일의 압축을 푸십시오. 

2. Markdown 뷰어에서 `README.md` 파일을 열어 프로젝트를 구성하십시오. 

   1. Android Studio에서 `BasicProject-Android` 프로젝트를 여십시오.
      
3. 앱을 실행하십시오. 
