---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-23"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 디바이스용 HTTP REST API
{: #api}

**중요:** 디바이스용 {{site.data.keyword.iot_full}} HTTP REST API 기능은 제한된 베타 프로그램의 일부로서만 사용 가능합니다. 향후 업데이트에는 이 기능의 현재 버전과 호환 가능한 변경사항이 포함될 수 있습니다. 이를 시도해 보고 [의견을 알려 주십시오](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html). 

## HTTP REST API 문서에 액세스
{: #api_link}

{{site.data.keyword.iot_short_notm}} HTTP REST API 문서에 액세스하고 디바이스를 조직에 통합하는 방법에 대한 자세한 정보를 얻으려면 URL [https://docs.internetofthings.ibmcloud.com/swagger/v0002.html](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)로 이동하십시오.

지원되는 {{site.data.keyword.iot_short_notm}} HTTP REST API의 유일한 버전은 버전 2입니다. {{site.data.keyword.iot_short_notm}} 솔루션이 버전 2를 사용 중인지 확인하십시오. 

## 클라이언트 연결
{: #client_connections}

{{site.data.keyword.iot_short_notm}}에서 디바이스에 클라이언트를 연결하는 방법과 클라이언트 보안에 대한 정보는 [{{site.data.keyword.iot_short_notm}}에 애플리케이션, 디바이스 및 게이트웨이 연결](../reference/security/connect_devices_apps_gw.html)을 참조하십시오. 

# 디바이스용 HTTP REST 메시징 API
{: #rest_messaging_api}

## 이벤트 공개
{: #event_publication}

MQTT 메시징 프로토콜의 사용과 함께, HTTP REST API 명령을 사용하여 HTTP를 통해 {{site.data.keyword.iot_short_notm}}에 이벤트를 공개하도록 디바이스를 구성할 수도 있습니다. 

다음 URL 중 하나를 사용하여 {{site.data.keyword.iot_short_notm}}에 연결된 디바이스에서 `POST` 요청을 제출하십시오. 

### 비보안 POST 요청
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### 보안 POST 요청

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**참고:* *기본 SSL 포트인 443 포트가 보안 HTTP API 호출에 대해 지정될 수도 있습니다. 

디바이스 또는 애플리케이션을 Quickstart 서비스에 연결 중인 경우에는 다음 URL 중 하나를 대신 사용하십시오. 

### Quickstart에 대한 비보안 POST 요청
<pre class="pre"><code class="hljs">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Quickstart에 대한 보안 POST 요청
<pre class="pre"><code class="hljs">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**중요 참고사항:**
- 현재 HTTP REST API 버전에서는 HTTP 메시징을 사용해서만 디바이스 이벤트를 제출할 수 있습니다. 기타 디바이스 관리 및 제어 기능에 대한 요청을 제출하려면 MQTT 메시징 프로토콜을 사용하십시오. 
- 권한 부여 HTTP 헤더를 변경할 수 없으므로, HTTP 연결은 동일한 디바이스에 대해서만 이벤트의 공개에 재사용될 수 있습니다. 
- 기본 SSL 포트인 443 포트가 보안 HTTP API 호출에 대해 지정될 수도 있습니다. 

### 인증

모든 요청에는 권한 부여 헤더가 포함되어야 합니다. 기본 인증은 지원되는 유일한 메소드입니다. 디바이스가 {{site.data.keyword.iot_short_notm}} HTTP REST API를 통해 HTTP 요청을 작성할 때는 다음 신임 정보가 필요합니다. 

|신임 정보|필수 입력|
|:---|:---|
|사용자 이름|`use-token-auth`
|비밀번호| 디바이스를 등록할 때 자동으로 생성하거나 수동으로 지정한 인증 토큰입니다.


### Content-Type 요청 헤더

`Content-Type` 요청 헤더는 요청과 함께 제공되어야 합니다. 다음 표에는 지원되는 유형이 {{site.data.keyword.iot_short_notm}} 내부 형식으로 맵핑되는 방법이 표시되어 있습니다. 

|Content-Type 헤더|{{site.data.keyword.iot_short_notm}}의 형식|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### 서비스 품질(QoS)

MQTT 서비스 품질(QoS) "최대 한 번" 전달 서비스 레벨 0과 유사하게 HTTP REST 메시징은 비지속적 메시지 전달을 제공하지만, 이는 요청이 올바른지와 HTTP 응답을 전송하기 전에 이를 서버에 전달할 수 있는지를 유효성 검증합니다. HTTP 상태 코드 200이 포함된 응답은 메시지가 서버에 전달되었는지 확인합니다. "최대 한 번" MQTT 서비스 품질(QoS) 레벨 또는 HTTP 등가물을 사용하여 이벤트 메시지를 전달하는 경우, 디바이스 및 애플리케이션은 전달을 보장하기 위한 재시도 로직을 구현해야 합니다. 

MQTT 프로토콜 및 {{site.data.keyword.iot_short_notm}}의 서비스 품질(QoS) 레벨에 대한 자세한 정보는 [MQTT 메시징](../reference/mqtt/index.html)을 참조하십시오. 

## 마지막 이벤트 캐시
{: #last-event-cache}

{{site.data.keyword.iot_short_notm}} 마지막 이벤트 캐시 API를 사용하면 디바이스에서 보낸 마지막 이벤트를 검색할 수 있습니다. 이 작업은 디바이스의 온라인 또는 오프라인 여부에 상관없이 작동하므로, 디바이스의 실제 위치나 사용 상태와 무관하게 디바이스 상태를 검색할 수 있습니다. 특정 디바이스에 대한 이벤트 ID의 마지막으로 기록된 값 또는 특정 디바이스가 보고한 각 이벤트 ID의 마지막으로 기록된 값을 검색할 수 있습니다. 디바이스의 마지막 이벤트 데이터는 최대 365일 전에 발생한 특정 이벤트에 대해서만 검색할 수 있습니다.

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
