---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Docker 컨테이너의 Kibana 로그 형식
{: #kibana_log_format_containers}

*검색* 페이지에 각 로그 항목의 다음 필드를 표시하도록 Kibana를 구성할 수 있습니다.
{:shortdesc}

| 필드  | 설명 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> 로그된 이벤트의 시간입니다. <br> 시간소인은 밀리초 단위까지 정의됩니다.  |
| @version | 이벤트의 버전입니다. |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} 영역의 ID입니다. |
| \_id | 로그 문서의 고유 ID입니다. |
| \_index | 로그 항목의 색인입니다. |
| \_type | 로그의 유형(예: *logs*)입니다. |
| group_id | 그룹 ID<br> * 단일 컨테이너의 경우 값은 **0000**입니다. <br> * 컨테이너 그룹의 경우 값은 그룹의 GUID 입니다.  |
| host | 컨테이너가 실행되는 호스트 이름입니다. |
| instance | 단일 컨테이너의 인스턴스 GUID 입니다. 컨테이너 그룹의 인스턴스 ID 목록입니다.|
| log | 간단한 메시지입니다. |
| message | 전체 메시지입니다. |
| path | 로그가 컨테이너 내부에 있는 경로 및 로그 이름입니다. |
| stream | 로그의 유형을 지정합니다(stdout, stderr). |
| time | 이벤트 발생 날짜 및 시간입니다. 시간소인은 밀리초 단위까지 정의됩니다. |
| timestamp | 로깅된 이벤트의 날짜 및 시간입니다. 시간소인은 밀리초 단위까지 정의됩니다.  |



