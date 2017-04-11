---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 게이트웨이용 MQTT 연결
{: #mqtt}

MQTT는 디바이스와 애플리케이션이 {{site.data.keyword.iot_full}}과 통신하는 데 사용하는 기본 프로토콜입니다. {{site.data.keyword.iot_short_notm}}에 디바이스를 연결하기 위한 게이트웨이로 MQTT 클라이언트를 사용하는 데 도움이 되는 클라이언트 라이브러리, 정보 및 샘플이 제공됩니다.
{:shortdesc}

## 클라이언트 연결
{: #client_connections}

클라이언트 보안에 대한 정보와 MQTT 클라이언트를 게이트웨이로 연결하는 방법은 [{{site.data.keyword.iot_short_notm}}에 애플리케이션, 디바이스 및 게이트웨이 연결](../reference/security/connect_devices_apps_gw.html)을 참조하십시오.

## MQTT 인증
{: #authentication}
게이트웨이와 디바이스의 경우 {{site.data.keyword.iot_short_notm}}에서는 MQTT 토큰 기반 인증을 사용합니다.

MQTT 인증을 사용하려면 MQTT 연결 시 사용자 이름과 비밀번호를 제출하십시오.

### 사용자 이름
{: #username}

`use-token-auth` 사용자 이름은 모든 게이트웨이에 동일한 값입니다. 이 값을 사용하면 {{site.data.keyword.iot_short_notm}}에서 비밀번호로 지정된 게이트웨이의 인증 토큰을 사용합니다.

### 비밀번호
{: #password}

각 게이트웨이의 비밀번호는 {{site.data.keyword.iot_short_notm}}에 게이트웨이를 등록할 때 생성된 고유 인증 토큰입니다.

## 이벤트 공개
{: #pub_events}

게이트웨이는 자체에서 이벤트를 공개하고 게이트웨이를 통해 연결된 디바이스 대신 이벤트를 공개할 수 있습니다. 이벤트를 공개하려면 다음 주제를 사용하고 예정된 이벤트 원본을 기반으로 적절한 `typeId` 및 `deviceId`를 대체합니다.

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/evt/<var class="keyword varname">eventId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}


**예제**


|    |'typeID'|'deviceID'|
|:---|:---|:---|
|게이트웨이 1 |mygateway |gateway1 |
|디바이스 1 |mydevice |device1 |

-   게이트웨이 1은 고유 상태 이벤트를 공개할 수 있습니다.  
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   게이트웨이 1은 디바이스 1 대신 상태 이벤트를 공개할 수 있습니다.  
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**중요:** 메시지 페이로드는 최대 131072바이트로 제한됩니다. 이 한계보다 큰 메시지는 거부됩니다.

### 보유 메시지
{{site.data.keyword.iot_short_notm}} 조직은 보유 MQTT 메시지를 공개할 권한이 없습니다. 게이트웨이가 보유 메시지를 전송하는 경우, 보유 메시지 플래그가 true로 설정되어 있으면 {{site.data.keyword.iot_short_notm}} 서비스에서 이를 대체하며 보유 메시지 플래그가 false로 설정된 것처럼 메시지를 처리합니다. 

## 명령 구독
{: #subscribing_cmds}

게이트웨이는 게이트웨이 자체에서 지시하는 명령 및 조직에 있는 다른 디바이스(다른 게이트웨이 포함)를 구독할 수 있습니다. 명령을 구독하려면 다음 주제를 사용하고 적절한 `typeId` 및 `deviceId`를 대체하십시오.

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/cmd/<var class="keyword varname">commandId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}

MQTT `+` 와일드카드는 여러 명령 소스를 구독하기 위해 `typeId`, `deviceId`, `commandId` 및 `formatString`에 사용할 수 있습니다.

**예:**

|디바이스 |`typeId`|`deviceId`|
|:---|:---|
|게이트웨이 1| mygateway   | gateway1   |
|디바이스 1 | mydevice    | device1    |


-   게이트웨이 1은 게이트웨이에서 지시하는 명령을 구독할 수 있습니다.  
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   게이트웨이 1은 디바이스 1에 보낸 명령을 구독할 수 있습니다.  
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   게이트웨이 1은 `mydevice` 유형의 디바이스에 전송되는 명령을 구독할 수 있습니다.  
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**중요:** `cleansession=false`로 지정되는 MQTT 지속적 세션은 게이트웨이에 연결되는 디바이스를 검색하지 않습니다. 디바이스가 게이트웨이 A에 연결한 다음 나중에 게이트웨이 B에 연결하면 연결이 끊긴 동안 해당 디바이스의 게이트웨이 A에 공개된 메시지는 받지 않습니다. 게이트웨이는 게이트웨이에 연결된 디바이스가 아니라 MQTT 클라이언트와 구독을 소유합니다.

## 게이트웨이 자동 등록
{: #auto-reg}

게이트웨이 디바이스에서는 연결된 디바이스를 자동으로 등록합니다. 게이트웨이가 등록되지 않은 디바이스 대신 메시지를 공개하거나 주제를 구독하면 해당 디바이스가 자동으로 등록됩니다.

게이트웨이 디바이스의 등록 요청에서 보류 중인 요청은 한 번에 128개로 제한됩니다. 여러 새 디바이스에 연결하면 게이트웨이를 통해 디바이스를 등록할 때 지연될 수 있습니다.

**경고**

게이트웨이가 자동으로 디바이스를 등록하는 데 실패하면 잠시 동안 해당 디바이스를 다시 등록하지 않습니다. 이 시간 동안 실패한 디바이스에서 메시지 또는 구독이 삭제됩니다.

## 게이트웨이 알림
{: #notification}

주제 구독 또는 공개 유효성 검증 중이나 자동 등록 중에 오류가 발생하면 게이트웨이 디바이스에 알림을 보냅니다. 게이트웨이에서 다음 주제를 구독하여 이러한 알림을 받으므로 `typeId` 및 `deviceId` 값을 대체할 수 있습니다.

```
iot-2/type/**typeId**/id/**deviceId**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/notify</pre>
{: codeblock}

알림 주제에 대해 받은 메시지는 다음 형식을 사용합니다.

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID>",
   "RC": "<Return_Code>",
   "Message": "<Message>"
}
```
여기서
-   `Request_Type` 값은 `publish` 또는 `subscribe`입니다.
-   `Timestamp`는 ISO 8601 형식의 시간입니다.
-   `Topic`은 게이트웨이의 요청 주제입니다.
-   `Device_Type`은 주제의 디바이스 유형입니다.
-   `Device_Id`는 주제의 디바이스 ID입니다.
-   `Client_ID`는 요청의 클라이언트 ID입니다.
-   `Return_Code`는 리턴 코드입니다.
-   `Message`는 오류 메시지입니다.

게이트웨이에서 다음 알림을 받을 수 있습니다.

-   주제가 허용된 주제 규칙과 일치하지 않습니다.
-   디바이스 유형이 올바르지 않습니다.
-   디바이스 ID가 올바르지 않습니다.
-   게이트웨이당 디바이스의 최대수에 도달했습니다.
-   조직당 디바이스의 최대수에 도달했습니다.
-   내부 오류로 인해 디바이스를 작성하지 못했습니다.

## 관리 게이트웨이
{: #managed_gateways}

디바이스 라이프사이클 관리 지원은 선택사항입니다. {{site.data.keyword.iot_short_notm}}에서 사용하는 디바이스 관리 프로토콜은 게이트웨이가 이벤트와 명령 제어에 사용하는 MQTT 연결와 동일한 연결을 사용합니다.

### 서비스 품질(QoS) 레벨 및 정리 세션
{: #quality_service}

관리 게이트웨이는 서비스 품질(QoS) 레벨이 0 또는 1인 메시지를 공개할 수 있습니다. 

QoS=0인 메시지는 버릴 수 있으며 메시징 서버가 다시 시작된 후 유지되지 않습니다. QoS=1인 메시지는 큐에 넣을 수 있으며 메시징 서버가 다시 시작된 후 유지됩니다. 구독 지속성에 따라 요청을 큐에 넣을지가 판별됩니다. 구독한 연결의 `cleansession` 매개변수에 따라 구독 지속성이 판별됩니다.  

메시지 큐에 넣기를 지원하기 위해 {{site.data.keyword.iot_short_notm}}에서 QoS 레벨이 1인 요청을 공개합니다. 관리 게이트웨이가 연결되지 않은 동안 전송된 메시지를 큐에 넣으려면 `cleansession` 매개변수를 false로 설정하여 디바이스에서 정리 세션을 사용하지 않게 구성하십시오.

**경고**

관리 게이트웨이에서 지속 가능한 구독을 사용하는 경우, 요청 제한시간이 초과되기 전에 게이트웨이에서 서비스에 다시 연결하지 않으면 오프라인인 동안 게이트웨이에 전송된 디바이스 관리 명령은 실패한 오퍼레이션으로 보고됩니다. 게이트웨이가 다시 연결되면 게이트웨이에서 해당 요청을 처리합니다. 지속 가능한 구독은 `cleansession=false` 매개변수를 사용하여 지정합니다.

관련된 디바이스와 상관없이 게이트웨이에서 MQTT 세션을 소유합니다. 디바이스에서 게이트웨이를 통해 구독 요청을 제출하면 `cleansession=false` 옵션 설정 여부와 상관없이 요청이 다른 게이트웨이로 로밍되지 않습니다.

### 주제
{: #topics}

관리 게이트웨이에서 {{site.data.keyword.iot_short_notm}}의 요청과 응답을 처리하려면 다음 주제를 구독해야 합니다.

-   관리 게이트웨이가 다음에서 디바이스 관리 응답을 구독합니다.  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/+</pre>
{: codeblock}
-   관리 게이트웨이가 다음에서 디바이스 관리 요청을 구독합니다.  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/+</pre>
{: codeblock}

관리 게이트웨이에서 다음 응답과 요청을 공개합니다.

- 디바이스 관리 응답은 다음에서 공개됩니다.  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/</pre>
{: codeblock}
- 디바이스 관리 요청은 다음에서 공개됩니다.  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/</pre>
{: codeblock}

게이트웨이는 자체적으로뿐 아니라 관련 **typeId** 및 **deviceId**를 사용하여 연결된 다른 디바이스 대신 디바이스 관리 프로토콜 메시지를 처리할 수 있습니다.

### 메시지 형식
{: #msg_format}

모든 메시지는 JSON 형식으로 전송됩니다.

**요청**

요청은 다음 코드 샘플에 표시된 대로 형식화됩니다.

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d`는 요청과 관련된 데이터를 전달합니다.
-   `reqId`는 요청의 ID이며 응답에 복사되어야 합니다. 응답이 필요하지 않으면 필드가 사용되지 않습니다.

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
-   `rc`는 원래 요청의 결과 코드입니다.
-   `message`는 응답 코드의 텍스트 설명이 있는 선택적 요소입니다.
-   `d`는 응답을 수반하는 선택적 데이터 요소입니다.
-   `reqId`는 원래 요청의 요청 ID입니다. 요청 ID는 요청과 응답을 연관시키는 데 사용하며 디바이스에서 모든 요청 ID가 고유한지 확인해야 합니다. {{site.data.keyword.iot_short_notm}} 요청에 대한 응답에 올바른 `reqId` 값이 있어야 합니다.
