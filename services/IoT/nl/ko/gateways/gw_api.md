---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 게이트웨이 디바이스용 HTTP REST API
{: #api_link}


{{site.data.keyword.iot_short_notm}} HTTP REST API 문서에 액세스하고 디바이스 작성, 업데이트, 삭제 및 나열에 대한 자세한 정보를 찾으려면 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)를 참조하십시오. 

지원되는 {{site.data.keyword.iot_short_notm}} HTTP REST API의 유일한 버전은 버전 2입니다. {{site.data.keyword.iot_short_notm}} 솔루션이 버전 2를 사용 중인지 확인하십시오. 

## 클라이언트 연결
{: #client_connections}

클라이언트 보안 및 클라이언트를 {{site.data.keyword.iot_short_notm}}의 게이트웨이 디바이스에 연결하는 방법에 대한 정보는 [{{site.data.keyword.iot_short_notm}}에 애플리케이션, 디바이스 및 게이트웨이 연결](../reference/security/connect_devices_apps_gw.html)을 참조하십시오. 


### 인증

모든 요청에는 권한 부여 헤더가 포함되어야 합니다. 기본 인증은 지원되는 유일한 메소드입니다. 디바이스가 {{site.data.keyword.iot_short_notm}} HTTP REST API를 사용하여 HTTP 요청을 작성하는 경우 다음 신임 정보가 필요합니다. 

|신임 정보|필수 입력|
|:---|:---|
|사용자 이름| `g/{orgId}/{gwType}/{gwDevId}`
|비밀번호| 게이트웨이 디바이스를 등록할 때 수동으로 지정했거나 자동으로 생성된 인증 토큰입니다.

여기서: 

<dl>
<dt>orgId</dt>  
<dd>조직의 이름이며 호스트 헤더에 지정되어 있는 이름과 일치해야 합니다. </dd>

<p></p>
<dt>gwType</dt>  
<dd>게이트웨이 유형입니다. </dd>
<p></p>
<dt>gwDevId</dt>  
<dd>게이트웨이의 디바이스 ID입니다. </dd>
</dl>


### Content-Type 요청 헤더

`Content-Type` 요청 헤더는 요청과 함께 제공되어야 합니다. 다음 표에서는 지원되는 유형이 {{site.data.keyword.iot_short_notm}} 내부 형식에 맵핑되는 방법을 보여줍니다. 

|Content-Type 헤더|{{site.data.keyword.iot_short_notm}}의 형식|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

## 마지막 이벤트 캐시
{: #last-event-cache}

{{site.data.keyword.iot_short_notm}} 마지막 이벤트 캐시 API를 사용하면 디바이스에서 보낸 마지막 이벤트를 검색할 수 있습니다. 이 API는 디바이스의 온라인 또는 오프라인 여부에 상관없이 작동하며 디바이스의 실제 위치 또는 사용 상태와 무관하게 디바이스 상태를 검색할 수 있습니다. 특정 디바이스에 대한 이벤트 ID의 마지막으로 기록된 값 또는 특정 디바이스가 보고한 각 이벤트 ID의 마지막으로 기록된 값을 검색할 수 있습니다. 디바이스의 마지막 이벤트 데이터는 최대 365일 전에 발생한 특정 이벤트에 대해서만 검색할 수 있습니다.

특정 이벤트 ID의 최근 값을 요청하려면 다음 API 요청을 사용하십시오. 이 요청은 “power” 이벤트 ID의 마지막으로 기록된 값을 리턴합니다. 

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

응답은 다음 JSON 형식으로 리턴됩니다.

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**참고:** API 응답이 JSON 형식일 때 이벤트 페이로드를 임의 형식으로 쓸 수 있습니다. 마지막 이벤트 캐시 API에서 리턴된 페이로드는 base64로 인코딩됩니다.

디바이스가 보고한 각 이벤트 ID의 최근 값을 요청하려면 다음 API 요청을 사용하십시오.

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

응답에는 디바이스가 보낸 모든 이벤트 ID가 포함됩니다. 다음 예에서 “power” 및 “temperature” 이벤트에 대한 값이 리턴됩니다.

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
