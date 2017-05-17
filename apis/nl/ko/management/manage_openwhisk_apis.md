---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 조치에서 API 작성
{: #manage_openwhisk_apis}

OpenWhisk 조치에서는 API Management를 통해 관리하는 것이 이로울 수 있습니다.

API Management를 사용하면 {{site.data.keyword.openwhisk_short}} 조치를 API로 표시할 수 있습니다. API를 정의한 후 보안 및 비율 제한 정책을 적용하고 API 사용 및 응답 로그를 보고 API 공유 정책을 정의할 수 있습니다.  

{{site.data.keyword.openwhisk_short}} API를 작성하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.openwhisk_short}} 대시보드에서 **API** 탭을 클릭하십시오. {{site.data.keyword.openwhisk_short}} API가 이미 작성되어 있는 경우 {{site.data.keyword.openwhisk_short}} API의 목록이 표시됩니다. {{site.data.keyword.openwhisk_short}} API가 없는 경우 시작하기 화면이 표시됩니다. 
2. **{{site.data.keyword.openwhisk_short}} API 작성**을 클릭하십시오. {{site.data.keyword.openwhisk_short}}의 API 작성 창이 표시됩니다. 
3. API 정보 섹션에 있는 필드를 완료한 다음 **오퍼레이션 작성**을 클릭하십시오. 오퍼레이션 작성 창이 표시됩니다. 오퍼레이션을 작성하여 API의 엔드포인트, https 경로 및 메소드를 정의할 수 있습니다.
4. "오퍼레이션 작성" 창에서 필수 필드를 완료하고 **작성**을 선택하십시오. 오퍼레이션이 {{site.data.keyword.openwhisk_short}} 조치 테이블을 호출하는 오퍼레이션에 추가됩니다.
5. 완료할 나머지 정보를 완성하십시오. 또한 API 관리 시 나중에 나머지 정보를 추가하거나 업데이트할 수 있습니다.
6. **저장**을 클릭하십시오. API의 API Management 개요 페이지가 열리고 정의한 모든 정보가 표시됩니다.
7. [API 관리](manage_apis.html)를 사용하여 API 관리를 계속하십시오.
