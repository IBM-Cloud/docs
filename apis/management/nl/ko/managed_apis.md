---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 내 API
{: #manage_api}

**관리되는 API 보기** 탭을 사용하면 관리 중인 API와 이전에 관리했지만 현재 노출되지 않은 API의 전체 상태를 볼 수 있습니다. **공유되는 API** 탭에서 사용자는 API 관리를 통해 또는 {{site.data.keyword.apiconnect_short}} 서비스를 통해 {{site.data.keyword.Bluemix_notm}} 조직과 공유된 모든 API를 볼 수 있습니다. 

API 관리와 함께 API 대시보드를 사용하여 관리 중인 모든 API를 볼 수 있습니다.  

## 관리되는 API 보기
{: #view_api}

여기서는 {{site.data.keyword.openwhisk_short}} 조치 및 기타 외부 소스에 대해 작성된 API를 볼 수 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 **메뉴** 아이콘 > **서비스** > **API**를 선택하십시오. 
2. 소스를 선택하려면 **API 관리**를 클릭하십시오. 현재 관리되는 API의 목록이 표시됩니다. API의 유형에는 다음 유형이 포함됩니다. 
    * 사용자 정의된 엔드포인트 - 이 항목은 {{site.data.keyword.Bluemix_notm}} 환경의 외부에 있으며 해당 URL 엔드포인트에 의해 추적되는 API입니다.  
    * {{site.data.keyword.openwhisk_short}} 앱 - 이 항목은 API 내부에 랩핑된 {{site.data.keyword.openwhisk_short}} 조치입니다. 

해당 API에 대한 추가 세부사항을 보려면 API의 이름을 선택하십시오. 

## 관리되는 API 작성
{: #create_mgd_api}

**관리되는 API 작성**을 선택하면 관리되는 API의 목록에서 나가지 않고도 API를 목록에 추가할 수 있습니다. 

일단 {{site.data.keyword.openwhisk_short}} 또는 API 프록시(외부) API의 작성을 원하는지 여부가 선택되면 새 API에 대한 정보를 입력하십시오.   

오직 여기서만 API 프록시 또는 외부 API를 추가할 수 있습니다. 외부 API는 {{site.data.keyword.Bluemix_notm}} 조직 영역에서 작성되거나 저장되지 않은 API입니다. 외부 엔드포인트의 URL을 지정하여 외부 API를 관리할 수 있습니다. 이는 사용자의 요구사항을 충족하는지 여부를 확인하기 위해 API 관리를 시도 중인 경우거나 중지되기를 원치 않는 기존 URL로 실행 중인 API가 이미 있는 경우에 유용합니다.  

API 작성과 관련된 필수 설정에 대한 추가 정보는 [API 관리](manage_apis.html)를 참조하십시오. 

## 공유되는 API 관련 작업
{: #share_api}

**공유되는 API 탐색** 탭에서 다른 사용자에 의해 작성되어 함께 공유되는 API를 볼 수 있습니다. 또한 {{site.data.keyword.openwhisk_short}} 조치 및 {{site.data.keyword.appconserviceshort}} 서비스와 연관된 API에 대한 API 키를 작성할 수도 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 **메뉴** 아이콘 > **서비스** > **API**를 클릭하십시오. 
2. 탐색에서 **공유되는 API 탐색**을 선택하십시오. 이용 가능한 모든 API가 여기에 표시됩니다. 
3. API를 이용하려면 이를 선택하여 해당 개발자 포털을 여십시오. 여기서 이를 사용하기 위해 플랜을 구독할 수 있습니다.  
4. 관리할 API를 선택한 이후, 다음 태스크를 완료하는 방법에 대한 자세한 정보는 [API 관리](manage_apis.html)를 참조하십시오.  
    * API 사용량 보기
    * API 키 작성
    * API 탐색기를 사용하여 문서를 보고 API를 테스트합니다. 
