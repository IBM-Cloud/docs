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

OpenWhisk 조치는 API 관리를 통해 관리된다는 점에서 유용할 수 있습니다. 

API 관리를 사용하면 {{site.data.keyword.openwhisk_short}} 조치를 API로서 노출할 수 있습니다. 일단 API가 정의되면, 보안 및 속도 제한 정책을 적용하고 API 사용량 및 응답 로그를 볼 수 있으며 API 공유 정책을 정의할 수 있습니다.   

{{site.data.keyword.openwhisk_short}} API를 작성하려면 다음 단계를 완료하십시오. 

1. {{site.data.keyword.openwhisk_short}} 대시보드에서 **API** 탭을 클릭하십시오. {{site.data.keyword.openwhisk_short}} API가 이미 작성된 경우에는 {{site.data.keyword.openwhisk_short}} API의 목록이 표시됩니다. 아직 {{site.data.keyword.openwhisk_short}} API가 없는 경우에는 시작하기 화면이 표시됩니다.  
2. **{{site.data.keyword.openwhisk_short}} API 작성**을 클릭하십시오. {{site.data.keyword.openwhisk_short}}의 API 작성 대화 상자가 표시됩니다.  
3. API 정보 섹션의 필드를 채우고 **작성 조작**을 클릭하십시오. 작성 조작 창이 표시됩니다. API에 대한 메소드 및 https 경로, 엔드포인트를 정의하는 조작을 작성할 수 있습니다. 
4. "작성 조작" 창에서 필수 필드를 채우고 **작성**을 선택하십시오. 조작이 {{site.data.keyword.openwhisk_short}} 조치 테이블을 호출하는 조작에 추가됩니다. 
5. 채우고 싶은 나머지 정보를 채우십시오. 나중에 API를 관리할 때 나머지 정보를 추가하거나 업데이트할 수도 있습니다. 
6. **저장**을 클릭하십시오. API에 대한 API 관리 개요 페이지가 열리며 방금 정의한 모든 정보가 표시됩니다. 
7. [API 관리](manage_apis.html)를 사용하여 API 관리를 계속 진행하십시오. 
