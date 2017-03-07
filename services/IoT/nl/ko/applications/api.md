---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 애플리케이션용 HTTP REST API
{: #api}

{{site.data.keyword.iot_full}} HTTP REST API를 사용하여 {{site.data.keyword.iot_short_notm}}에서 조직과 상호작용하는 애플리케이션을 빌드하고 사용자 정의할 수 있습니다.
{:shortdesc}

## 기능
{: #capabilities}

{{site.data.keyword.iot_short_notm}} HTTP REST API는 애플리케이션에 대해 다음 기능과 능력을 지원합니다. 

- 조직 정보 검색
- 벌크 디바이스 오퍼레이션(나열, 추가 및 제거)
- 디바이스 유형 오퍼레이션(나열, 작성, 삭제, 세부사항 보기 및 업데이트)
- 디바이스 오퍼레이션(나열, 추가, 제거, 세부사항 보기, 업데이트, 위치 보기 및 관리 정보 보기)
- 디바이스 진단 오퍼레이션(로그 지우기, 로그 검색, 로그 정보 추가, 로그 삭제, 특정 로그 가져오기, 오류 코드 지우기, 디바이스 오류 코드 가져오기 및 오류 코드 추가)
- 연결 문제점 판별(디바이스 연결 로그 이벤트 나열)
- 마지막 이벤트 캐시(특정 디바이스의 마지막 이벤트 보기)
- 디바이스 관리 요청 오퍼레이션(디바이스 관리 요청 나열, 요청 시작, 요청 상태 지우기, 요청 세부사항 가져오기, 디바이스별 모든 요청 상태 나열, 그리고 특정 디바이스의 요청 상태 가져오기)
- 사용량 관리 오퍼레이션(사용된 데이터 총량 검색)
- 디바이스 이벤트 공개(베타)
- 서비스 상태 조회(조직별 서비스 상태 검색)

## HTTP REST API 문서에 액세스
{: #api_link}

{{site.data.keyword.iot_short_notm}} HTTP REST API 문서에 액세스하고 애플리케이션을 빌드하고 사용자 정의하는 방법에 대한 자세한 정보를 얻으려면 URL [https://docs.internetofthings.ibmcloud.com/swagger/v0002.html](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)로 이동하십시오.

지원되는 {{site.data.keyword.iot_short_notm}} HTTP REST API의 유일한 버전은 버전 2입니다. {{site.data.keyword.iot_short_notm}} 솔루션이 버전 2를 사용 중인지 확인하십시오. 

# 애플리케이션용 HTTP REST 메시징 API
{: #rest_messaging_api}

## 이벤트 및 명령 공개
{: #event_command_publication}

MQTT 메시징 프로토콜의 사용과 함께, 다음 HTTP REST API 명령 중 하나를 사용하여 HTTP를 통해 {{site.data.keyword.iot_short_notm}}에 이벤트 및 명령을 공개하도록 애플리케이션을 구성할 수도 있습니다. 

### 비보안 이벤트 POST 요청
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 보안 이벤트 POST 요청
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**참고:** 기본 SSL 포트인 443 포트가 보안 HTTP API 호출에 대해 지정될 수도 있습니다. 

### 비보안 명령 POST 요청
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 보안 명령 POST 요청
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

디바이스 또는 애플리케이션을 Quickstart 서비스에 연결 중인 경우에는 **orgId**를 'quickstart' 문자열로 대체하십시오. 

**참고:**
- 애플리케이션이 HTTP 연결을 재사용하여 이벤트 또는 명령을 다른 디바이스에 게시할 수 있지만, 권한 부여 HTTP 헤더는 변경될 수 없습니다. 
- 기본 SSL 포트인 443 포트가 보안 HTTP API 호출에 대해 지정될 수도 있습니다. 

### 인증

모든 요청에는 권한 부여 헤더가 포함되어야 합니다. 기본 인증은 지원되는 유일한 메소드입니다. 애플리케이션은 API 키를 사용하여 인증됩니다. 애플리케이션이 {{site.data.keyword.iot_short_notm}} HTTP REST API를 통해 요청을 작성할 때는 다음 신임 정보가 필요합니다. 

```
username = API key (for example, a-orgId-a84ps90Ajs)
password = Authentication token
```

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
