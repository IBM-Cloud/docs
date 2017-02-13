---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# 튜토리얼 - Weather 코드 스타터
{: #tutorial_weather}

Weather용 {{site.data.keyword.Bluemix}} 모바일 코드 스타터에서는 Swift를 사용하여 Weather에 대한 작업을 시작할 기반 프로젝트를 소개하며 푸시 및 분석 통합 지점을 제공합니다. 


## 요구사항
{: #tutorial_requirements}

* [Bluemix ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net "외부 링크 아이콘") 계정
* [Bluemix 카탈로그 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.{DomainName}/catalog/)에서 얻은 [Weather Company Data ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.{DomainName}/catalog/services/weather-company-data/) 서비스 인스턴스


## 시작하기
{: #tutorial_gs}

Weather 코드 스타터를 빨리 시작하고 실행하려면 다음 단계를 수행하십시오. 

1. {{site.data.keyword.Bluemix_notm}}에서 모바일 대시보드 프로젝트를 작성하십시오. 

   1. 모바일 대시보드의 **시작하기** 페이지에서 **프로젝트 작성**을 클릭하십시오. 

      또는 **프로젝트** 페이지에서 **새 프로젝트**를 클릭할 수 있습니다. 

   2. **코드 스타터**를 클릭하십시오. 

   3. **Weather**를 선택하고 **프로젝트 작성**을 클릭하십시오. 

   4. 프로젝트 이름을 입력하고 **작성**을 클릭하십시오. 

2. 선택사항: {{site.data.keyword.mobilepushshort}} 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 **{{site.data.keyword.mobilepushshort}}**에 대해 **추가**를 클릭하십시오. 

      또는 **{{site.data.keyword.mobilepushshort}}** 페이지에서 **작성**을 클릭할 수도 있습니다. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 

   3. iOS의 경우, [Apple Push Notification Service 구성 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobilepush/t_push_provider_ios.html "외부 링크 아이콘"){: new_window}을 수행하십시오. 

   4. Android의 경우, [GCM(Google Cloud Messaging) 구성 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobilepush/t_push_provider_android.html "외부 링크 아이콘"){: new_window}을 수행하십시오. 
   
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

   5. 인증 구성에 대한 자세한 정보는 [Mobile Client Access 시작하기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobileaccess/index.html "외부 링크 아이콘"){: new_window}를 참조하십시오. 

5. 프로젝트를 다운로드하십시오. 

   1. **코드**를 클릭하고 선호 언어를 선택하십시오. 

   2. **코드 다운로드**를 클릭하십시오. 

5. 아카이브의 압축을 풀고 `README.md` 파일의 지시사항을 수행하십시오. 


## 다음에 수행할 작업
{: #tutorial_next}

[사용해 보기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399 "외부 링크 아이콘"){: new_window}


### UI 스타터 튜토리얼
{: #tutorials_UI}

* [튜토리얼 - Store Catalog](tutorial_store_catalog.html)


### 코드 스타터 튜토리얼
{: #tutorials_Code}

* [튜토리얼 - 기본](tutorial.html)
* [튜토리얼 - Cloudant Sync](tutorial_cloudant_synd.html)
* [튜토리얼 - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [튜토리얼 - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [튜토리얼 - Watson Language](tutorial_watson_language.html)
