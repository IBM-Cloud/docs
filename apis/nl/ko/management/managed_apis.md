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

**관리 API 보기** 탭을 사용하여 관리하는 API의 전체 상태 및 이전에 관리했지만 현재는 표시하지 않는 API를 확인하십시오. **공유 API** 탭에서 API Management 또는 {{site.data.keyword.apiconnect_short}} 서비스를 통해 {{site.data.keyword.Bluemix_notm}} 조직과 공유한 모든 API를 볼 수 있습니다.

API 대시보드를 사용하여 API Managemen와 함께 관리하는 모든 API를 볼 수 있습니다. 

## 관리 API 보기
{: #view_api}

여기서 {{site.data.keyword.openwhisk_short}} 조치 및 기타 외부 소스에 맞게 작성된 API를 볼 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 **메뉴** 아이콘 > **서비스** > **API**를 선택하십시오.
2. 소스를 선택하려면 **API 관리**를 클릭하십시오. 현재 관리되는 API의 목록이 표시됩니다. API 유형에 다음 유형이 포함됩니다.
    * 사용자 정의 엔드포인트 - 이러한 항목은 {{site.data.keyword.Bluemix_notm}} 환경 외부에 있는 API이며 URL 엔드포인트에 의해 추적됩니다. 
    * {{site.data.keyword.openwhisk_short}} 앱 - 이러한 항목은 API 내부에 랩핑된 {{site.data.keyword.openwhisk_short}} 조치입니다.

API 이름을 선택하여 해당 API에 대한 세부사항을 확인하십시오.

## 관리 API 작성
{: #create_mgd_api}

**관리 API 작성**을 선택하여 관리 API의 목록을 떠나지 않고 목록에 API를 추가할 수 있습니다.

선택 후 {{site.data.keyword.openwhisk_short}} 또는 API 프록시(외부) API를 작성하려는 경우 새 API의 정보를 입력하십시오.  

API 프록시 또는 외부 API를 추가할 수 있는 유일한 위치입니다. 외부 API는 {{site.data.keyword.Bluemix_notm}} 조직 영역에 작성되거나 저장되지 않은 API입니다. 외부 엔드포인트의 URL을 지정하여 외부 API를 관리할 수 있습니다. 이는 API Management를 시도하여 요구에 맞는지 확인하거나 방해하지 않으려는 기존 URL에서 실행되는 API가 이미 있는 경우에 유용합니다. 

API 작성을 위한 필수 설정의 추가 정보는 [API 관리](manage_apis.html)를 참조하십시오.

## 공유 API를 사용한 작업
{: #share_api}

**공유 API 탐색** 탭에서 다른 사용자가 작성하고 사용자와 공유한 API를 볼 수 있습니다. 또한 {{site.data.keyword.openwhisk_short}} 조치 및 {{site.data.keyword.appconserviceshort}} 서비스와 연관된 API의 API 키를 작성할 수 있습니다.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 **메뉴** 아이콘 > **서비스** > **API**를 클릭하십시오.
2. 탐색에서 **공유 API 탐색**을 선택하십시오. 이용할 수 있는 모든 API가 여기에 표시됩니다.
3. API를 이용하려면 이를 선택하여 해당 개발자 포털을 여십시오. 이 포털에서는 API 사용을 위해 플랜에 등록할 수 있습니다. 
4. 관리할 API를 선택한 후 다음 태스크를 완료하는 방법에 대한 자세한 정보를 보려면 [API 관리](manage_apis.html)를 참조하십시오. 
    * API 사용 보기
    * API 키 작성
    * API 탐색기를 사용하여 문서를 보고 API를 테스트하십시오.
