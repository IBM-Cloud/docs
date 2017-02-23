---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 애플리케이션용 MQTT 연결
{: #mqtt}

MQTT는 디바이스와 애플리케이션이 {{site.data.keyword.iot_full}}과 통신하는 데 사용하는 기본 프로토콜입니다. {{site.data.keyword.iot_short_notm}} 애플리케이션을 연결하고 통합하는 데 도움이 되도록 클라이언트 라이브러리, 정보 및 샘플이 제공됩니다.
{:shortdesc}

## 클라이언트 연결
{: #client_connections}

클라이언트 보안 및 {{site.data.keyword.iot_short_notm}}의 애플리케이션에 MQTT 클라이언트를 연결하는 방법에 대한 정보는 [{{site.data.keyword.iot_short_notm}}에 애플리케이션, 디바이스 및 게이트웨이 연결](../reference/security/connect_devices_apps_gw.html)을 참조하십시오. 

## MQTT 인증
{: #mqtt_authentication}

{{site.data.keyword.iot_short_notm}} 애플리케이션이 조직에 연결하려면 API 키가 필요합니다. API 키가 등록되면 인증 토큰이 생성되며, 이는 해당 API 키와 함께 사용되어야 합니다. 

다음 예제는 일반적인 API 키를 표시합니다. 

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}


다음 예제는 일반적인 인증 토큰을 보여줍니다.

```
MP$08VKz!8rXwnR-Q*
```

API 키를 사용하여 MQTT 연결하는 경우, 다음 가이드라인이 적용되는지 확인하십시오.

- MQTT 클라이언트 ID의 형식: a:*orgId*:*appId*
- MQTT 사용자 이름이 API 키임(예: a-*orgId*-a84ps90Ajs)
- MQTT 비밀번호가 인증 토큰임(예: MP$08VKz!8rXwnR-Q*)


## 디바이스 이벤트 공개
{: #publishing_device_events}

애플리케이션은 임의의 등록된 디바이스에서 가져온 것처럼 이벤트를 공개할 수 있습니다. 예를 들면, 다음과 같습니다. 

-  주제 iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*에 공개

디바이스의 기존 데이터를 {{site.data.keyword.iot_short_notm}}에 전송하기 위해, 사용자는 데이터를 처리하고 이를 {{site.data.keyword.iot_short_notm}}에 공개하는 애플리케이션을 작성할 수 있습니다. 

**중요:** 메시지 페이로드는 최대 131072바이트로 제한됩니다. 한계를 초과하는 메시지는 거부됩니다. 

### 보유 메시지
{{site.data.keyword.iot_short_notm}} 조직은 보유 MQTT 메시지를 공개할 권한이 없습니다. 애플리케이션, 게이트웨이 또는 디바이스가 보유 메시지를 전송하는 경우, 보유 메시지 플래그가 true로 설정되어 있으면 {{site.data.keyword.iot_short_notm}} 서비스에서 이를 대체하며 플래그가 false로 설정된 것처럼 메시지를 처리합니다. 

## 디바이스 명령 공개
{: #publishing_device_commands}

애플리케이션은 등록된 디바이스에 대한 명령을 공개할 수 있습니다. 예를 들면, 다음과 같습니다. 

-  주제 iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*에 공개

## 디바이스 이벤트 구독
{: #subscribe_device_events}

애플리케이션은 하나 이상의 디바이스에서 이벤트를 구독할 수 있습니다. 예를 들면, 다음과 같습니다. 

-  주제 iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string* 구독

**참고:** 둘 이상의 이벤트 유형을 구독하거나 둘 이상의 디바이스의 이벤트를 구독하려면 다음 컴포넌트에 대해 MQTT "any" 와일드카드 문자(+)를 사용하십시오. 

- device_type
- device_id
- event_id
- format_string

## 디바이스 명령 구독
{: #subscribe_device_commands}

애플리케이션은 하나 이상의 디바이스에 전송 중인 명령을 구독할 수 있습니다. 예를 들면, 다음과 같습니다. 

-  주제 iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string* 구독

**참고:** 둘 이상의 이벤트 유형을 구독하거나 둘 이상의 디바이스의 이벤트를 구독하려면 다음 컴포넌트에 대해 MQTT "any" 와일드카드 문자(+)를 사용하십시오. 

-  device_type
-  device_id
-  cmd_id
-  format_string

## 디바이스 상태 메시지 구독
{: #subscribe_device_status}

애플리케이션은 하나 이상의 디바이스의 상태 모니터를 구독할 수 있습니다. 예를 들면, 다음과 같습니다. 

-  주제 iot-2/type/*device_type*/id/*device_id*/mon 구독

**참고:** 둘 이상의 디바이스의 업데이트를 구독하려면 다음 컴포넌트에 대해 MQTT "any" 와일드카드 문자(+)를 사용하십시오. 

- device_type
- device_id

## 애플리케이션 상태 메시지 구독
{: #subscribe_app_status}

애플리케이션은 하나 이상의 애플리케이션의 상태 모니터를 구독할 수 있습니다. 예를 들면, 다음과 같습니다. 

- 주제 iot-2/app/*appId*/mon 구독

**참고:** 모든 애플리케이션에 대한 업데이트를 구독하려면 *appId* 컴포넌트에 대해 MQTT "any" 와일드카드 문자(+)를 사용하십시오. 


## Quickstart 제한사항
{: #quickstart_restrictions}
Quickstart 서비스에서 사용할 애플리케이션 코드를 작성하려는 경우, 다음 기능이 Quickstart에서 지원되지 않습니다. 

- 명령 공개
- 명령 구독
- **deviceType** 또는 **appId** 컴포넌트에서 MQTT "any" 와일드카드 문자(+) 사용
- TLS(Transport Layer Security)을 통한 MQTT 연결
- 확장 가능 애플리케이션

## 확장 가능 애플리케이션
{: #scalable_apps}

애플리케이션의 연결 방식을 조정하면, 애플리케이션의 여러 인스턴스 간의 이벤트 메시지 처리를 로드 밸런싱하여 {{site.data.keyword.iot_short_notm}} 애플리케이션의 확장성을 높일 수 있습니다. 

최적 로드 밸런싱 및 확장성에 필요한 클라이언트의 수는 배치에 따라 다양합니다. 최적의 클라이언트 수를 식별하려면 시스템의 스트레스 테스트를 실행해야 합니다. 

확장 가능 애플리케이션은 지속 불가능 구독 또는 혼합 지속성 공유 구독(베타)으로서 정의됩니다. 

### 지속 불가능 구독
{: #shared_sub_non_durable}

로드 밸런싱을 사용하려면 애플리케이션 구독이 비지속적이며 구독의 클라이언트 ID가 다음 형식과 일치하는지 확인하십시오. 

<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
{: codeblock}

여기서, 
-  **A** 문자는 클라이언트가 확장 가능한 애플리케이션임을 표시합니다. 
-  *orgId*는 서비스 인스턴스를 등록할 때 생성된 6자의 고유 구성 ID입니다.
-  *appId*는 클라이언트의 사용자 정의 고유 문자열 ID입니다. 문자열에는 영숫자 문자(a-z, A-Z, 0-9) 및 대시(-), 밑줄(_), 점(.) 특수 문자만 포함될 수 있습니다. 


**중요:**
- {{site.data.keyword.iot_short_notm}}에서 확장 가능한 애플리케이션으로 올바르게 지정하려면, 클라이언트 ID가 대문자 **A**로 시작되어야 합니다. 
- 확장 가능한 애플리케이션의 일부인 기타 클라이언트는 동일한 클라이언트 ID를 사용해야 합니다. 
- 정리 세션 값은 지속 불가능 구독에 대해 false(0)로 설정되어야 합니다. 

### 혼합 지속성 공유 구독(베타)
{: #shared_sub_mixed}

{{site.data.keyword.iot_short_notm}} 서비스는 혼합 지속성 공유 구독의 베타 시험판을 지원하기 위해 MQTT V3.1.1 메시징 프로토콜 스펙을 확장합니다. 공유 구독은 애플리케이션에 대한 로드 밸런싱 기능을 제공합니다. 특정 주제 영역에 공개 중인 메시지의 볼륨을 백엔드 엔터프라이즈 애플리케이션이 처리할 수 없으면 공유 구독이 필요할 수 있습니다. 예를 들어, 많은 디바이스가 단일 애플리케이션이 처리 중인 메시지를 공개하는 경우에는 공유 구독의 로드 밸런싱 기능을 사용해야 할 수 있습니다. 

혼합 지속성 공유 구독인 경우에는 구독의 클라이언트 ID가 다음 형식과 일치하는지 확인하십시오. 

<pre class="pre">A:<var class="keyword varname">org</var>:<var class="keyword varname">appId</var>:<var class="keyword varname">instanceId</var></pre>
{: codeblock}

여기서, 
- 클라이언트 ID의 문자 **A**, *orgId* 및 *appId*는 [지속 불가능 구독](#shared_sub_non_durable)의 경우와 동일한 방법으로 정의됩니다. 
- *instanceID*는 36자 이하인 문자열이며 다음 문자만 포함될 수 있습니다. 
   - 영숫자 문자(a-z, A-Z, 0-9)
   - 대시(-)
   - 밑줄(_)
   - 점( . )

**중요:**
- 혼합 지속성 공유 구독에 대한 지원은 베타 기능으로만 사용 가능합니다. 프로덕션 애플리케이션에서는 베타 기능을 구현하지 마십시오. 
- 정리 세션 값은 혼합 지속성 공유 구독에서 true(1) 또는 false(0)로 설정될 수 있습니다. 
- instanceId로 연결된 클라이언트는 instanceId 없이 연결된 클라이언트와는 다른 구독을 사용합니다. 따라서 혼합 지속성 공유 구독에서 여러 클라이언트의 연결을 원하는 경우에는 모든 구독에서 instanceID를 지정해야 합니다. 

**예제 시나리오**

다음 시나리오는 지속 불가능한 확장 가능 애플리케이션이 {{site.data.keyword.iot_short_notm}}에서 작동되는 방법에 대한 하나의 예입니다. 

- 클라이언트 1이 **A:abc123:myApplication**으로 연결되고 모든 디바이스 이벤트를 구독합니다. 이는 클라이언트 1이 공개된 디바이스 이벤트의 100% 를 수신함을 의미합니다. 
- 클라이언트 2가 **A:abc123:myApplication**으로 연결되고 역시 모든 디바이스 이벤트를 구독합니다. 이는 클라이언트 1과 클라이언트 2 모두가 공개된 모든 이벤트를 공유함을 의미합니다. 처리 로드는 클라이언트 1과 클라이언트 2 간에 공유됩니다. 
- 클라이언트 3이 **A:abc123:myApplication**으로 연결되고 역시 모든 디바이스 이벤트를 구독합니다. 이는 클라이언트 1, 클라이언트 2와 클라이언트 3 모두가 이벤트에 대한 처리 로드를 공유함을 의미합니다. 
- 그리고 클라이언트 2와 클라이언트 3이 모든 디바이스 이벤트의 구독을 취소합니다. 이는 오직 클라이언트 1만 공개되는 모든 디바이스 이벤트를 수신함을 의미합니다. 클라이언트 2와 클라이언트 3이 아직 디바이스에 연결되어 있지만, 클라이언트 1은 공개된 디바이스 이벤트의 100% 를 수신합니다. 
- 둘 이상의 애플리케이션이 구독을 공유할 때 메시지는 전송된 순서대로 도착하지 않을 수 있습니다. 예를 들어, 메시지 A가 먼저 전송되었지만 메시지 A가 클라이언트 2에 도착하기 전에 메시지 B가 클라이언트 1에 도착할 수 있습니다. 
