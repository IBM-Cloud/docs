---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 디바이스용 MQTT 연결
{: #mqtt}

MQTT는 디바이스와 애플리케이션이 {{site.data.keyword.iot_full}}과 통신하는 데 사용하는 기본 프로토콜입니다. 디바이스를 연결하고 {{site.data.keyword.iot_short_notm}}에 통합하는 데 도움이 되는 클라이언트 라이브러리, 정보 및 샘플이 제공됩니다.
{:shortdesc}

## 클라이언트 연결
{: #client_connections}

클라이언트 보안에 대한 정보와 MQTT 클라이언트를 {{site.data.keyword.iot_short_notm}}의 디바이스에 연결하는 방법은 [{{site.data.keyword.iot_short_notm}}에 애플리케이션, 디바이스 및 게이트웨이 연결](../reference/security/connect_devices_apps_gw.html)을 참조하십시오.


## Quickstart 서비스에 디바이스 연결
{: #connecting_devices}

Quickstart 서비스는 서비스의 가장 빠른 레벨입니다. 수신 확인을 제공하지 않으며 0보다 큰 MQTT 서비스 품질(QoS) 레벨을 지원하지 않습니다. Quickstart 서비스에 연결할 때 인증 또는 등록이 필요하지 않으며 `orgId`를 `quickstart`로 설정해야 합니다.

Quickstart와 사용할 디바이스 코드를 쓰는 경우 다음 {{site.data.keyword.iot_short_notm}} 서비스 기능은 Quickstart 모드에서 지원되지 않는다는 점에 유의하십시오.

-  명령 구독
-  디바이스 관리 프로토콜
-  정리 또는 지속 가능 세션

**중요:** 초당 1보다 큰 비율로 디바이스에서 보내는 메시지는 버릴 수 있습니다.


## MQTT 인증
{: #mqtt_authentication}

게이트웨이와 디바이스의 경우 {{site.data.keyword.iot_short_notm}}에서는 MQTT 토큰 기반 인증을 사용합니다.

MQTT 인증을 사용하려면 MQTT 연결 시 사용자 이름과 비밀번호를 제출하십시오.

### 사용자 이름

`use-token-auth` 사용자 이름은 모든 디바이스에 동일한 값입니다. 이 값을 사용하면 {{site.data.keyword.iot_short_notm}}에서 비밀번호로 지정된 디바이스의 인증 토큰을 사용합니다.

### 비밀번호

각 디바이스의 비밀번호는 {{site.data.keyword.iot_short_notm}}에 디바이스를 등록할 때 생성된 고유 인증 토큰입니다.

## 이벤트 공개
{: #publishing_events}

디바이스는 다음 형식으로 이벤트 주제에 공개됩니다.

<pre class="pre">iot-2/evt/<var class="keyword varname">event_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

여기서

-  **event_id**는 이벤트의 ID입니다(예: `status`). 이벤트 ID는 MQTT에서 유효한 임의 문자열일 수 있습니다. 와일드카드를 사용하지 않으면 구독자 애플리케이션이 구독 주제에서 이 문자열을 사용하여 주제에 공개된 이벤트를 받아야 합니다.
-  **format_string**은 메시지 수신자가 컨텐츠를 구문 분석하는 방법을 판별할 수 있도록 메시지 페이로드의 컨텐츠 유형을 정의하는 문자열입니다. 공통 컨텐츠 유형 값에는 "json", "xml", "txt" 및 "csv"가 포함되나 이에 국한되지는 않습니다. 값은 MQTT에서 올바른 임의 문자열일 수 있습니다.

**중요:** 메시지 페이로드는 최대 131072바이트로 제한됩니다. 이 한계보다 큰 메시지는 거부됩니다.

### 보유 메시지
{{site.data.keyword.iot_short_notm}} 조직은 보유 MQTT 메시지를 공개할 권한이 없습니다. 디바이스가 보유 메시지를 전송하는 경우, 보유 메시지 플래그가 true로 설정되어 있으면 {{site.data.keyword.iot_short_notm}} 서비스에서 이를 대체하며 보유 메시지 플래그가 false로 설정된 것처럼 메시지를 처리합니다. 


## 명령 구독
{: #subscribing_to_commands}

디바이스는 다음 형식으로 명령 주제를 구독합니다.

<pre class="pre">iot-2/cmd/<var class="keyword varname">command_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

여기서
 - **command_id**는 명령의 ID입니다(예: `update`). 명령 ID는 MQTT 프로토콜에서 유효한 임의 문자열일 수 있습니다. 와일드카드를 사용하지 않으면 디바이스가 구독 주제에서 이 문자열을 사용하여 주제에 공개된 명령을 받아야 합니다.
 - **format_string**은 명령 수신자가 컨텐츠를 구문 분석하는 방법을 판별할 수 있도록 명령 페이로드의 컨텐츠 유형을 정의하는 문자열입니다. 공통 컨텐츠 유형 값에는 "json", "xml", "txt" 및 "csv"가 포함되나 이에 국한되지는 않습니다. 값은 MQTT에서 올바른 임의 문자열일 수 있습니다.

디바이스는 다른 디바이스의 이벤트를 구독할 수 없습니다. 디바이스는 고유 디바이스에만 공개되는 명령을 받습니다.

## 관리 디바이스
{: #managed-devices}

디바이스 라이프사이클 관리 지원은 선택사항입니다. 디바이스 관리 프로토콜은 디바이스에서 이벤트와 명령 제어에 이미 사용 중인 MQTT 연결을 사용합니다.

### 서비스 품질(QoS) 레벨 및 정리 세션

관리 디바이스는 서비스 품질(QoS) 레벨이 0 또는 1인 메시지를 공개할 수 있습니다. 

QoS=0인 메시지는 버릴 수 있으며 메시징 서버가 다시 시작된 후 유지되지 않습니다. QoS=1인 메시지는 큐에 넣을 수 있으며 메시징 서버가 다시 시작된 후 유지됩니다. 구독 지속성에 따라 요청을 큐에 넣을지가 판별됩니다. 구독한 연결의 `cleansession` 매개변수에 따라 구독 지속성이 판별됩니다.  

메시지 큐에 넣기를 지원하기 위해 {{site.data.keyword.iot_short_notm}}에서 QoS 레벨이 1인 요청을 공개합니다. 관리 디바이스가 연결되지 않은 동안 전송된 메시지를 큐에 넣으려면 `cleansession` 매개변수를 false로 설정하여 디바이스에서 정리 세션을 사용하지 않게 구성하십시오.

**경고:**
  관리 디바이스에서 지속 가능한 구독을 사용하는 경우 요청의 제한시간이 초과되기 전에 디바이스를 서비스에 다시 연결하지 않으면 오프라인 중에 디바이스에 보낸 모든 명령은 실패한 오퍼레이션으로 보고됩니다. 그러나 디바이스가 다시 연결되면 디바이스에서 해당 요청을 처리합니다. 지속 가능한 구독은 `cleansession=false` 매개변수로 지정합니다.

### 주제

관리 디바이스에서 {{site.data.keyword.iot_short_notm}} 서비스의 요청과 응답을 처리하려면 다음 주제를 구독해야 합니다.

```
iotdm-1/#
```


관리 디바이스는 수행 중인 관리 요청 유형에 고유한 주제에 공개됩니다.

- 관리 디바이스가 `iotdevice-1/response`에서 디바이스 관리 응답을 공개합니다.
- 관리 디바이스에서 공개할 수 있는 다른 주제는 [디바이스 관리 프로토콜](device_mgmt/index.html) 및 [디바이스 관리 요청](device_mgmt/requests.html)을 참조하십시오.



### 메시지 형식

모든 메시지는 JSON 형식으로 전송됩니다.

**요청**  
요청은 다음 코드 샘플에 표시된 대로 형식화됩니다.

<pre class="pre">{  "d": {...}, "<var class="keyword varname">reqId</var>": "b53eb43e-401c-453c-b8f5-94b73290c056" }</pre>
{: codeblock}

여기서,

 - **d**는 요청과 관련된 데이터를 전달합니다.
 - **reqId**는 요청의 ID이며 응답에 복사되어야 합니다. 응답이 필요하지 않으면 *reqId* 필드를 생략할 수 있습니다.

**응답**  
응답은 다음 코드 샘플에 표시된 대로 형식화됩니다.
```
        {
            "rc": 0,
            "message": "success",
            "d": {...},
            "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
        }
```
여기서,  
 - **rc**는 원래 요청의 결과 코드입니다.
 - **message**는 응답 코드의 텍스트 설명이 있는 선택적 요소입니다.
 - **d**는 응답을 수반하는 선택적 데이터 요소입니다.
 - **reqId**는 응답을 요청과 상관시키는 데 사용하는 원래 요청의 요청 ID입니다. 디바이스에서 모든 요청 ID가 고유한지 확인해야 합니다. {{site.data.keyword.iot_short_notm}} 요청에 대한 응답에 올바른 **reqId** 값이 있어야 합니다.

특정 요청 및 응답 메시지에 대한 자세한 정보는 [디바이스 관리 프로토콜](device_mgmt/index.html) 및 [디바이스 관리 요청](device_mgmt/requests.html)을 참조하십시오.
