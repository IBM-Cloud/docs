---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# {{site.data.keyword.visualrecognitionshort}} 코드 스타터의 엔드-투-엔드 튜토리얼
{: #tutorial_vr}

다음 엔드-투-엔드 튜토리얼에서는 설치해야 할 도구를 포함하여 {{site.data.keyword.visualrecognitionshort}} 코드 스타터에서 프로젝트를 작성하는 전체 단계와 그에 이어 Xcode 및 Android Studio에서 스타터를 실행하는 단계를 안내합니다. 


### 개발자 도구 설치
{: #dev_tools}

[전제조건 개발자 도구 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](get_code.html#prereq-dev-tools "외부 링크 아이콘"){: new_window}를 설치했는지 확인하십시오. 


### {{site.data.keyword.visualrecognitionshort}} 코드 스타터에서 프로젝트 작성
{: #create_project}

1. {{site.data.keyword.Bluemix}}에서 모바일 대시보드 프로젝트를 작성하십시오. 

   1. 모바일 대시보드의 **시작하기** 페이지에서 **프로젝트 작성**을 클릭하십시오. 

      또는 **프로젝트** 페이지에서 **프로젝트 작성**을 클릭할 수 있습니다. 

   2. **코드 스타터**를 클릭하십시오. 

   3. **Visual Recognition**을 선택하고 **프로젝트 작성**을 클릭하십시오. 

   4. 프로젝트 이름을 입력하십시오. 이 튜토리얼의 경우 `VisualRecognitionProject`를 사용하십시오. 
   
   5. **작성**을 클릭하십시오.

2. 선택사항: {{site.data.keyword.mobilepushshort}} 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 **{{site.data.keyword.mobilepushshort}}**에 대해 **추가**를 클릭하십시오. 

      또는 **{{site.data.keyword.mobilepushshort}}** 페이지에서 **작성**을 클릭할 수도 있습니다. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 

   3. iOS의 경우, [Apple Push Notification Service 구성 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobilepush/t_push_provider_ios.html "외부 링크 아이콘"){: new_window}을 수행하십시오. 

   4. Android의 경우, [FCM(Firebase Cloud Messaging) 구성 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobilepush/t_push_provider_android.html "외부 링크 아이콘"){: new_window}을 수행하십시오. 
   
3. 선택사항: 분석 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 **분석**에 대해 **추가**를 클릭하십시오. 

      또는 **분석** 페이지에서 **작성**을 클릭할 수 있습니다. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 
   
   3. 앱을 실행한 후 분석 데이터를 보려면 **데모 모드**를 토글하여 끄십시오. 
   
   4. 분석 구성에 대한 자세한 정보는 [{{site.data.keyword.mobileanalytics_short}} 시작하기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobileanalytics/index.html "외부 링크 아이콘"){: new_window}를 참조하십시오. 
  
4. 선택사항: 인증 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 **인증**에 대해 **추가**를 클릭하십시오. 

      또는 **인증** 페이지에서 **작성**을 선택할 수 있습니다. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 
   
   3. **인증**을 토글하여 켜십시오. 
   
   4. ID 제공자를 선택하고 필요한 정보를 입력하여 이를 구성하십시오. 하나의 ID 제공자만 사용 가능하게 설정할 수 있습니다. 

   5. 인증 구성에 대한 자세한 정보는 [{{site.data.keyword.amashort}} 시작하기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobileaccess/index.html "외부 링크 아이콘"){: new_window}를 참조하십시오. 

5. 프로젝트 코드를 생성하십시오. 

   1. **프로젝트 개요** 페이지에서 **코드 가져오기**를 클릭하여 사용하는 플랫폼 및 언어를 선택하십시오. 
   
      또는 **코드** 페이지를 클릭할 수 있습니다.
      
   2. iOS의 경우 **iOS Swift**를 클릭하십시오.
   
   3. Android의 경우 **Android**를 클릭하십시오.
   
   4. 프로젝트 코드 생성이 완료되면 **코드 다운로드**를 클릭하여 프로젝트 아카이브를 다운로드하십시오.


### Xcode에서 프로젝트 실행
{: #run_xcode}

1. `VisualRecognitionProject-Swift.zip` 파일의 압축을 푸십시오.

2. Markdown 뷰어에서 `README.md` 파일을 열어 프로젝트를 구성하는 단계를 검토하십시오. 

   1. [{{site.data.keyword.visualrecognitionshort}} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.{DomainName}/catalog/services/visual-recognition/ "외부 링크 아이콘"){: new_window} 서비스 인스턴스를 작성하십시오. 
   
   2. 터미널을 열고 프로젝트 폴더로 이동하십시오. 
   
      1. CocoaPods 저장소를 설정해야 하는 경우 `pod setup`을 실행하십시오. 
      
      2. 기존 pod를 업데이트해야 하는 경우 `pod update`를 실행하십시오. 
      
      3. 프로젝트에 필요한 pod를 설치하려면 `pod install`을 실행하십시오.
      
      4. {{site.data.keyword.ibmwatson}} Developer Cloud iOS SDK를 사용하기 위한 종속 항목 및 프레임워크를 빌드하려면 `carthage update --platform iOS`를 실행하십시오. 
      
   3. `VisualRecognitionProject.xcworkspace` Xcode 작업공간을 여십시오.
   
   4. {{site.data.keyword.visualrecognitionshort}} 서비스 신임 정보를 추가하십시오. 
   
      1. {{site.data.keyword.visualrecognition}} 서비스 신임 정보에서 `api_key`를 복사하십시오. 
      
      2. `api_key`를 `VisualRecognitionAPIKey` 키에 붙여넣어 `WatsonCredentials.plist` 파일에 추가하십시오. 
      
3. 앱을 실행하십시오. 


### Android Studio에서 프로젝트 실행
{: #run_studio}

1. `VisualRecognitionProject-Android.zip` 파일의 압축을 푸십시오.

2. Markdown 뷰어에서 `README.md` 파일을 열어 프로젝트를 구성하십시오. 

   1. [{{site.data.keyword.visualrecognitionshort}} ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.{DomainName}/catalog/services/visual-recognition/ "외부 링크 아이콘"){: new_window} 서비스 인스턴스를 작성하십시오. 
   
      {{site.data.keyword.visualrecognitionshort}} 서비스 인스턴스가 이미 있으면 이 단계를 건너뛰십시오. 
   
   2. Android Studio에서 `VisualRecognitionProject-Android` 프로젝트를 여십시오.
   
   4. {{site.data.keyword.visualrecognitionshort}} 서비스 신임 정보를 추가하십시오. 
   
      1. {{site.data.keyword.visualrecognitionshort}} 서비스 신임 정보에서 `api_key`를 복사하십시오. 
      
      2. `api_key`를 `watson_visual_recognition_api_key` 키에 붙여넣어 `res/values/watson_credentials.xml` 파일에 추가하십시오. 
      
3. 앱을 실행하십시오. 


## 다음에 수행할 작업
{: #what_next}

다른 튜토리얼을 참조하십시오. 


### UI 스타터 튜토리얼
{: #tutorials_UI}

* [튜토리얼 - Store Catalog](tutorial_store_catalog.html)


### 코드 스타터 튜토리얼
{: #tutorials_Code}

* [튜토리얼 - 기본](tutorial.html)
* [튜토리얼 - Cloudant Sync](tutorial_cloudant_synd.html)
* [튜토리얼 - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [튜토리얼 - Watson Language](tutorial_watson_language.html)
* [튜토리얼 - Weather](tutorial_weather.html)

