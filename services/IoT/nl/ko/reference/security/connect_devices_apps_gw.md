---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}}에 애플리케이션, 디바이스 및 게이트웨이 연결
{: #connect_devices_apps_gw}
마지막 업데이트 날짜: 2016년 9월 08일
{: .last-updated}

MQTT 프로토콜을 통해 애플리케이션, 디바이스 및 게이트웨이를 {{site.data.keyword.iot_full}}에 연결할 수 있습니다. 디바이스에서 HTTP API를 통해 {{site.data.keyword.iot_short_notm}}에 연결하고 이벤트를 공개할 수 있습니다.
{: shortdesc}


## 클라이언트 연결 URL
{: #client_connect_url}

디바이스, 애플리케이션 및 게이트웨이 클라이언트를 {{site.data.keyword.iot_short_notm}} 인스턴스에 연결하려면 다음 연결 URL을 사용하십시오.

### 메시징 주소

<pre class="pre"><var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com</pre>
{: codeblock}

### HTTP REST API 연결 URL

<pre class="pre">https://<var class="keyword varname">orgId</var>.internetofthings.ibmcloud.com/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**참고**
- *orgId*는 서비스 인스턴스를 등록할 때 생성된 고유 구성 ID입니다.
- Quickstart 서비스에 디바이스 또는 애플리케이션을 연결하는 경우 *orgId* 값으로 'quickstart'를 지정하십시오.

## 포트 보안
{: #client_port_security}

필수 포트가 열리고 통신에 사용 가능한지 확인하십시오.

|연결 유형 |포트 번호|
|:---|:---|
|비보안|1883|
|보안|8883|
|보안|443|

MQTT 클라이언트에서는 디바이스 인증 토큰(디바이스의 경우) 및 API 키와 토큰(애플리케이션의 경우)과 같은 적절한 신임 정보를 사용하여 연결합니다. 비보안 포트 1883에 보내는 MQTT 메시징에서는 일반 텍스트로 신임 정보를 보내므로 항상 보안 대체 포트인 8883 또는 443을 대신 사용하십시오. 보안 포트에서는 TLS 신임 정보를 강제로 암호화합니다. Python MQTT 라이브러리에서 tls_set() 메소드를 사용하여 애플리케이션에서 TLS를 사용으로 설정해야 합니다. 그렇지 않으면 데이터가 보안되지 않은 상태로 전송될 수 있습니다.

8883 또는 443 포트에서 보안 MQTT 메시징을 사용하면 새 클라이언트 라이브러리는 {{site.data.keyword.iot_short_notm}}에서 제공하는 인증서를 자동으로 신뢰합니다. 사용자의 클라이언트 환경에서는 이와 다른 경우 [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem)에서 전체 인증서 체인을 다운로드하여 사용할 수 있습니다.


## TLS 요구사항
{: #tls_requirements}
일부 TLS(Transport Layer Security) 클라이언트 라이브러리에서는 와일드 카드를 포함하는 도메인을 지원하지 않습니다. 라이브러리를 변경할 수 없으면 인증 검사를 사용 안함으로 설정하십시오.

{{site.data.keyword.iot_short_notm}}에는 TLS V1.2와 다음 암호 스위트가 필요합니다.
- ECDHE-RSA-AES256-GCM-SHA384
- AES256-GCM-SHA384
- ECDHE-RSA-AES128-GCM-SHA256
- AES128-GCM-SHA256

## MQTT 클라이언트 인증
{: #mqtt_authentication}

**중요:** 각 MQTT 클라이언트에는 고유 클라이언트 ID가 필요합니다. 이미 연결된 클라이언트 ID를 사용하여 조직의 클라이언트에 연결하면 첫 번째 연결이 끊깁니다.

{{site.data.keyword.iot_short_notm}}에 직접 연결된 디바이스와 게이트웨이는 현재 연결되어 있음을 표시하기 위해 대시보드에 상태 아이콘이 표시됩니다. 대시보드에서는 게이트웨이를 통해 연결된 디바이스를 인식하지 못하므로 게이트웨이를 통해 간접적으로 연결된 디바이스는 연결이 끊김으로 표시됩니다.

### MQTT 클라이언트 ID

디바이스, 애플리케이션 및 게이트웨이가 성공적으로 인증되도록 다음 클라이언트 ID와 형식을 사용하여 각 MQTT 클라이언트를 정의하십시오.

|클라이언트 유형 |ID|MQTT ID 형식|
|:---|:---|:---|
|애플리케이션|a|<pre class="pre">a:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|확장 가능 애플리케이션|A|<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|디바이스|d|<pre class="pre">d:<var class="keyword varname">orgId</var>:<var class="keyword varname">deviceType</var>:<var class="keyword varname">deviceId</var></pre>|
|게이트웨이|g|<pre class="pre">g:<var class="keyword varname">orgId</var>:<var class="keyword varname">typeId</var>:<var class="keyword varname">deviceId</var></pre>|

여기서

- *orgId*는 서비스 인스턴스를 등록할 때 생성된 6자의 고유 구성 ID입니다.
- *appId*는 클라이언트의 사용자 정의 고유 문자열 ID입니다.
- *deviceId*는 모든 유형에서 디바이스나 게이트웨이를 고유하게 식별하며 일련 번호와 비슷합니다.
- *device_type*은 연결 중인 디바이스 유형의 ID이며 모델 번호와 비슷합니다.
- *typeId*는 연결 중인 게이트웨이 유형의 ID이며 모델 번호와 비슷합니다.

*appId*, *type_id*, *device_type* 및 *device_id* 값은 36자 이하여야 하며 다음만 포함할 수 있습니다.
- 영숫자 문자(a-z, A-Z, 0-9)
- 대시(-)
- 밑줄(_)
- 점( . )

**참고:**
- Quickstart 서비스에 연결할 때는 인증이 필요하지 않습니다.
- 연결하기 전에 애플리케이션을 등록하지 않아도 됩니다.


### MQTT을 사용하여 애플리케이션 연결

{{site.data.keyword.iot_short_notm}} 애플리케이션을 조직에 연결하려면 API 키가 필요합니다. API 키를 등록할 때 토큰이 생성되므로 해당 API 키와 사용해야 합니다.

다음 코드에서는 API 키의 예를 제공합니다.

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}

다음 예는 일반적인 인증 토큰을 보여줍니다.

```
 MP$08VKz!8rXwnR-Q*
```

API 키를 사용하여 MQTT 연결 시, 다음 요구사항이 충족되는지 확인하십시오.

- MQTT 클라이언트 ID의 형식이 다음과 같습니다. a:*orgId*:*appId*
- MQTT 사용자 이름은 API 키입니다(예: a-*orgId*-a84ps90Ajs).
- MQTT 비밀번호는 인증 토큰입니다(예: *MP$08VKz!8rXwnR-Q*).

자세한 정보는 [애플리케이션용 MQTT 연결](../../applications/mqtt.html)을 참조하십시오.

### 디바이스 인증

#### 사용자 이름
{{site.data.keyword.iot_short_notm}} 서비스에서는 디바이스의 토큰 기반 인증만 지원하므로 각 디바이스에는 올바른 사용자 이름이 하나뿐입니다.
`use-token-auth`의 값을 사용하여 게이트웨이 또는 디바이스의 인증 토큰을 MQTT 연결의 비밀번호로 사용함을 서비스에 표시합니다.

자세한 정보는 [디바이스용 MQTT 연결](../../devices/mqtt.html)을 참조하십시오.

#### 비밀번호
클라이언트에서 토큰 기반 인증을 사용 중인 경우 모든 MQTT 연결에 사용하는 비밀번호로 디바이스 인증 토큰을 제출하십시오.
