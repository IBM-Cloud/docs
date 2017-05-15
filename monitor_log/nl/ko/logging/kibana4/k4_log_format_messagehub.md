---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Message Hub의 Kibana 로그 형식
{: #kibana_log_format_messagehub}

*검색* 페이지에 각 로그 항목의 다음 필드를 표시하도록 Kibana를 구성할 수 있습니다.
{:shortdesc}

| 필드  | 설명 |
|-------|-------------|
| @timestamp | `yyyy-MM-ddTHH:mm:ss:SS-0500`  <br> 로그된 이벤트의 시간입니다. <br> 시간소인은 밀리초 단위까지 정의됩니다.  |
| @version | 이벤트의 버전입니다. |
| ALCH_TENANT_ID | {{site.data.keyword.Bluemix_notm}} 영역의 ID입니다. |
| \_id | 로그 문서의 고유 ID 입니다. |
| \_index | 로그 항목의 색인입니다. |
| \_type | 로그 유형(예: *syslog*)입니다. |
| loglevel | 로깅된 이벤트의 심각도입니다(예: **Info**). |
| module | 이 필드는 **MessageHub**로 설정됩니다. |
{: caption="표 1. 메시지 허브 이벤트의 필드" caption-side="top"}

로그 항목의 예:

```
March 8th 2017, 17:15:16.454	

message:
    Creating topic ABC
@version:
    1
@timestamp:
    March 8th 2017, 17:15:16.454
loglevel:
    Info
module:
    MessageHub
ALCH_TENANT_ID:
    3d8d2eae-f3f0-44f6-9717-126113a00b51
&#95;id:
    AVqu6vJl1zcfr8KYMI95
&#95;type:
    logs
&#95;index:
    logstash-2017.03.08
```
