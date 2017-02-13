---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-15"

---
{:new_window: target="_blank"}

# 튜토리얼 - Store Catalog UI 스타터
{: #tutorial_store_catalog}

{{site.data.keyword.Bluemix}} Store Catalog UI 스타터는 사용자 정의할 수 있는 기본 판매 앱 구조와 각 {{site.data.keyword.Bluemix_notm}} 모바일 서비스의 통합 지점을 제공합니다. 


## 요구사항
{: #tutorial_requirements}

* [Bluemix ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://bluemix.net "외부 링크 아이콘") 계정


## 시작하기
{: #tutorial_gs}

Store Catalog UI 스타터를 빨리 시작하고 실행하려면 다음 단계를 수행하십시오. 

1. {{site.data.keyword.Bluemix_notm}}에서 모바일 대시보드 프로젝트를 작성하십시오. 

   1. 모바일 대시보드의 **시작하기** 페이지에서 **프로젝트 작성**을 클릭하십시오. 

      또는 **프로젝트** 페이지에서 **프로젝트 작성**을 클릭할 수 있습니다. 

   2. **UI 스타터**가 아직 선택되지 않은 경우 이를 선택하십시오. 

   3. **Store Catalog**를 선택하고 **프로젝트 작성**을 클릭하십시오. 

   4. 프로젝트 이름을 입력하고 **작성**을 클릭하십시오. 

2. 선택사항: {{site.data.keyword.mobilepushshort}} 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 **{{site.data.keyword.mobilepushshort}}**에 대해 **추가**를 클릭하십시오. 

      또는 **{{site.data.keyword.mobilepushshort}}** 페이지에서 **작성**을 클릭할 수도 있습니다. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 

   3. iOS의 경우, [Apple Push Notification Service 구성 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobilepush/t_push_provider_ios.html "외부 링크 아이콘"){: new_window}을 수행하십시오. 

   4. Android의 경우, [GCM(Google Cloud Messaging) 구성 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](/docs/services/mobilepush/t_push_provider_android.html "외부 링크 아이콘"){: new_window}을 수행하십시오. 

3. 선택사항: 기타 기능을 추가하십시오. 

   1. **프로젝트 개요** 페이지에서 해당 기능에 대해 **추가**를 클릭하십시오. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 

   3. 서비스에서 제공하는 지시사항에 따라 서비스를 설정하십시오. 

4. 앱을 디자인하십시오. 

   1. 탐색 메뉴에서 **UI 빌더**를 선택하여 앱의 디자인을 사용자 정의하십시오. 
   
		**팁:** UI 빌더의 빠른 개요를 보려면 UI 빌더를 선택한 후 탐색에서 **작동 방법 보기**를 선택하십시오. 

   2. 탐색에서 **디자인** 탭을 선택하십시오. 

      앱 모양의 시뮬레이션된 보기와 앱의 디자인에 사용할 수 있는 작업공간이 있습니다. 

   3. 선택적으로 **화면 작성**을 선택하여 새 화면을 추가하십시오. 앱에서 참조하기 쉽도록 새 화면의 이름을 지정하십시오. 새 화면은 트리에서 선택된 항목에 상관없이 기본 화면과 동일한 레벨에서 작성됩니다. 다음 유형의 화면 중에서 선택할 수 있습니다. 
      * 메뉴
      * 목록
      * 맵
      * 사용자 정의
      * 차트	   

   4. 인터페이스의 **레이아웃** 섹션에서 *메뉴* 텍스트 상자를 선택하고 **표시할 데이터** 필드의 컨텐츠를 바꿔 앱의 메뉴 제목을 변경할 수 있습니다. 시뮬레이션된 디바이스 섹션에서 업데이트를 보십시오. 

      필요에 따라 각 항목을 선택하고 정보를 업데이트하여 디자인 항목을 업데이트하십시오. 이들 항목은 트리 형식으로 표시됩니다. 항목을 새 위치로 끌어와 메뉴 항목의 순서 또는 위치를 변경할 수 있습니다. 모든 하위 항목도 상위와 함께 이동합니다. **표시할 데이터** 필드에 표시되는 트리 항목의 텍스트 정보는 데이터 소스 스프레드시트의 컨텐츠를 참조합니다. *해당 항목을 **데이터** 보기에서 식별된 데이터 소스의 컨텐츠로 겹쳐쓰므로 **디자인** 보기에서 해당 항목을 변경하지 마십시오. *

		트리에서 *양식*으로 식별되는 항목은 독립적이며 인라인으로 수정될 수 있습니다. 이 항목은 데이터 소스의 정보를 참조하지 않습니다. 

   5. 탐색에서 **데이터**를 선택하여 앱에서 사용 중인 데이터를 표시하십시오. 템플리트에 기본 정보가 있지만 **새로 작성**을 선택하여 데이터의 소스를 변경할 수 있습니다. 둘 이상의 데이터 소스를 참조할 수 있으므로 사용하는 각 소스의 이름을 제공하십시오. 다음 데이터 소스 옵션 중에서 선택할 수 있습니다. 
      * 클라우드
      * 로컬
      * Cloudant
      * Google 스프레드시트
      * Excel Online
      * Google 드라이브

      또한 단추를 사용하고 테이블에서 컨텐츠를 선택하여 테이블에 있는 컨텐츠를 가져오거나, 내보내거나, 수정할 수 있습니다(컨텐츠가 로컬인 경우). 

	  주의사항: 기본 데이터의 구조와 일치하지 않는 데이터를 가져오는 경우 *스키마 대체* 슬라이더를 켜십시오. 해당 예는 스타터에서 제공되는 데이터보다 열 수가 적은 .csv 파일입니다. 
	  
   6. **탐색**을 선택하여 앱의 탐색 조치를 사용자 정의하십시오. 대부분의 화면의 경우 탐색 조치는 화면의 관계에 따라 자동으로 작성되므로 이는 선택사항입니다. 다음의 과정을 통해 대상 화면을 변경할 수 있습니다. 먼저 메뉴 항목 목록에서 탐색을 *시작할* 화면 또는 필드를 선택하십시오. 그다음, 대상 화면 필드에서 해당 항목이 탐색하여 *도달할* 화면을 선택하십시오.  

   7. 탐색에서 **사용자 액세스**를 선택하여 프로젝트의 액세스 요구사항을 수정하십시오. 스위치를 사용하여 사용자 액세스 켜기와 끄기를 토글할 수 있습니다. 사용자 액세스가 켜진 경우 비활성 사용자 제한시간과 앱에 액세스할 수 있는 사용자의 신임 정보를 설정할 수 있습니다. 

   8. 탐색 메뉴에서 **설정**을 선택하여 프로젝트의 전체 정보와 색상을 수정하십시오. 이 화면에서, 프로젝트에 추가한 서비스에 필요한 경우 Google API 키를 입력할 수 있습니다. 또한 이 화면에서 Apple Store 또는 Google Play 스토어에 등록된 고유 번들 ID를 추가할 수 있습니다. 

      프로젝트에 IBM MobileFirst Foundation SDK를 추가하려면 스위치를 토글하여 켜십시오. 

   9. *설정* 화면에서 프로젝트에 IBM MobileFirst Platform Foundation을 추가하도록 스위치를 토글한 경우 탐색에 **Foundation** 선택사항이 표시됩니다. **Foundation**을 선택하고 IBM MobileFirst Platform Foundation에 특정한 필수 정보를 완료하십시오. 

   10. 탐색 메뉴에서 **공개**를 선택하여 모바일 앱을 작성하는 데 필요한 최종 정보를 입력하십시오. iOS용 번들 ID와 Android용 애플리케이션 ID를 입력할 수 있습니다.

       iOS 앱을 작성할 경우 번들 ID, 배포 인증서를 *.p12* 파일로 얻고 Apple 프로비저닝 포털에서 프로비저닝 프로파일을 *.mobileprovision* 파일로 얻어야 합니다. 이 세 항목을 Apple Store에 앱을 게시할 때 사용할 컴퓨터에서 동시에 작성해야 합니다. 배포 인증서와 프로비저닝 프로파일은 번들 ID를 기반으로 해야 합니다.  	

5. 프로젝트를 다운로드하십시오. 

   1. **코드**를 클릭하고 선호하는 플랫폼 또는 프로그래밍 언어를 선택하십시오. 

   2. Android의 경우 코드를 생성한 후 다음 옵션 중에서 선택할 수 있습니다. 

      * 코드 다운로드

      * APK 다운로드

      * QR 코드를 사용하여 다운로드

   3. iOS의 경우 코드를 생성한 후 다음 옵션 중에서 선택할 수 있습니다. 

      * 코드 다운로드

6. 디바이스 또는 시뮬레이터에서 앱을 실행하십시오. 


## 다음에 수행할 작업
{: #tutorial_next}

[사용해 보기 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://console.{DomainName}/mobile/create-project?starter=fb5e31a9-1186-4d46-939e-2f620f35b83b "외부 링크 아이콘"){: new_window}


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
* [튜토리얼 - Weather](tutorial_weather.html)

