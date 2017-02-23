---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-30"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#Java를 사용하여 {{site.data.keyword.iot_short_notm}}에서 게이트웨이 개발
{: #java_cli_gw}

디바이스가 {{site.data.keyword.iot_full}}에서 조직에 직접 연결할 수 없는 경우에는 Java™을 사용하여 게이트웨이를 빌드하고 사용자 정의할 수 있습니다. 게이트웨이 개발을 시작하는 데 도움이 되도록 {{site.data.keyword.iot_short_notm}}용 Java 클라이언트 라이브러리, 문서 및 예제가 제공됩니다.
{:shortdesc}

## Java 클라이언트 및 자원 다운로드
{: #java_client_download}

{{site.data.keyword.iot_short_notm}}의 Java 클라이언트 라이브러리 및 샘플에 액세스하려면 GitHub의 [iot-java](https://github.com/ibm-watson-iot/iot-java) 저장소로 이동하여 설치 지시사항을 완료하십시오. 

## 생성자
{: #constructor}

생성자는 게이트웨이 클라이언트 인스턴스를 빌드하며, 다음 정의가 포함된 `Properties` 오브젝트를 허용합니다. 

|정의 |설명  |
|:----|:----|
|`org`|조직 ID로 설정해야 하는 필수 값입니다. Quickstart 플로우를 사용 중인 경우 `quickstart`를 지정하십시오.|
|`domain`|메시징 엔드포인트 URL이며, 이는 선택사항입니다. 도메인의 값을 지정하지 않으면 URL의 기본값은 `internetofthings.ibmcloud.com`이며, 이는 {{site.data.keyword.iot_short_notm}} 프로덕션 서버입니다. |
|`type`|게이트웨이의 유형을 지정하는 필수 값입니다. |
|`id` |게이트웨이의 고유 ID를 지정하는 필수 값입니다. |
|`auth-method`|사용할 인증 메소드입니다. 지원되는 유일한 메소드는 `token`입니다.|
|`auth-token`|게이트웨이를 {{site.data.keyword.iot_short_notm}}에 안전하게 연결하기 위한 API 키 인증 토큰입니다. |
|`clean-session`|지속 가능한 구독 모드로 게이트웨이 연결을 원하는 경우에만 필요한 true 또는 false 값입니다. 기본적으로 `clean-session`은 true로 설정됩니다.|
|`WebSocket`|WebSocket을 사용한 게이트웨이 연결을 원하는 경우에만 필요한 true 또는 false 값입니다. |
|`Port`|연결할 포트 번호입니다. 8883 또는 443을 지정하십시오. 포트 번호를 지정하지 않으면 기본적으로 클라이언트가 포트 번호 8883의 {{site.data.keyword.iot_short_notm}}에 연결됩니다.|
|`MaxInflightMessages`|연결을 위한 인플라이트 메시지의 최대 수를 설정합니다. 기본값은 100입니다.|
|`Automatic-Reconnect`|연결이 끊어진 상태인 동안에 게이트웨이를 {{site.data.keyword.iot_short_notm}}에 자동으로 다시 연결하려는 경우에만 필요한 true 또는 false 값입니다. 기본값은 false입니다.|
|`Disconnected-Buffer-Size`|클라이언트가 연결이 끊겼을 때 메모리에 저장할 수 있는 최대 메시지 수입니다. 기본값은 5000입니다.|

**참고:** 지속 가능한 구독 모드로 게이트웨이를 연결하려면 `clean-session`을 `false`로 설정하십시오. 정리 세션에 대한 자세한 정보는 [MQTT 문서](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)의 '구독 버퍼 및 정리 세션' 섹션을 참조하십시오.

`Properties` 오브젝트는 {{site.data.keyword.iot_short_notm}} 모듈과 상호작용하는 데 사용되는 정의를 작성합니다. 

다음 코드 샘플은 게이트웨이 클라이언트 인스턴스를 생성하는 방법을 표시합니다. 

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### 구성 파일 사용

`Properties` 오브젝트를 사용하여 직접 게이트웨이 인스턴스를 작성하는 대신, 게이트웨이의 특성에 대한 이름-값 쌍이 포함된 구성 파일을 사용할 수 있습니다. 구성 파일을 사용하여 게이트웨이에 대한 `Properties` 오브젝트를 빌드하려면  다음 코드 형식을 사용하십시오. 

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

구성 파일 컨텐츠의 형식은 다음 형식이어야 합니다.

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## {{site.data.keyword.iot_short_notm}}에 연결
{: #connecting_to_iotp}

{{site.data.keyword.iot_short_notm}}에 연결하려면 `connect()` 함수를 사용하십시오. `connect()` 함수에는 MQTT 예외(MqttException) 연결 실패 시에 라이브러리가 재연결을 시도하는지 여부를 판별하는 `autoRetry`라고 하는 선택적 부울 매개변수가 포함되어 있습니다. 기본적으로, `autoRetry`는 true로 설정됩니다. 잘못된 디바이스 등록 세부사항이 전달되었으므로 MqttSecurityException 연결에 실패하는 경우에는 `autoRetry`가 true로 설정되어 있어도 라이브러리가 다시 연결을 시도하지 않습니다.

MQTT에 대한 활성 유지 간격을 설정하기 위해 `connect()` 함수를 호출하기 전에 `setKeepAliveInterval(int)` 메소드를 선택적으로 사용할 수 있습니다. `setKeepAliveInterval(int)` 값은 초 단위로 측정되며, 보내거나 받는 메시지 간의 최대 시간 간격을 정의합니다. `setKeepAliveInterval(int)` 값이 지정된 경우, 클라이언트는 TCP/IP 제한시간의 끝에 도달할 때까지 기다리지 않고도 서버가 더 이상 사용 가능하지 않음을 감지할 수 있습니다. 클라이언트는 최소한 하나의 메시지가 각 활성 유지 간격 기간 내에 네트워크에서 이동되도록 보장합니다. 0개의 데이터 관련 메시지가 제한시간 중에 수신되면 클라이언트는 서버가 수신확인하는 작은 `ping` 메시지를 발송합니다. `setKeepAliveInterval(int)`는 기본적으로 60초로 설정됩니다. 클라이언트에서 활성 유지 처리 기능을 사용하지 않으려면 `setKeepAliveInterval(int)` 값을 0으로 설정하십시오. 

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

연결에 실패할 때 발생하는 재시도의 횟수를 제어하려면 오버로드된 connect(int numberOfTimesToRetry) 함수를 사용하십시오. 

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

게이트웨이 클라이언트가 {{site.data.keyword.iot_short_notm}}에 정상적으로 연결된 이후, 게이트웨이는 독자적으로 또한 게이트웨이에 연결된 디바이스 대신 이벤트를 공개하고 명령을 구독할 수 있습니다. 

## 게이트웨이 뒤에 있는 디바이스 등록
{: #register_device_gateway}

자동으로 또는 API를 사용하여 코드를 개발하여 {{site.data.keyword.iot_short_notm}} 인스턴스에 연결된 게이트웨이 뒤에 있는 디바이스를 등록할 수 있습니다. 

### 자동 디바이스 등록
게이트웨이가 이벤트를 공개하거나 이에 연결된 디바이스에 대한 명령을 구독할 때마다 사용자는 {{site.data.keyword.iot_short_notm}}에서 디바이스를 자동으로 등록할 수 있습니다. 

### API 디바이스 등록
또한 {{site.data.keyword.iot_short_notm}} API를 사용하여 게이트웨이 뒤에 있는 디바이스를 {{site.data.keyword.iot_short_notm}} 인스턴스에 등록할 수도 있습니다. 

{{site.data.keyword.iot_short_notm}} API를 사용한 개발을 단순화하려면 api() 메소드를 호출하여 API 클라이언트 인스턴스를 시작하십시오. 이는 다음 코드 샘플에서 간략히 설명되어 있습니다. 

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
API 클라이언트의 핸들을 수신하는 경우에는 게이트웨이에 디바이스 등록을 시작할 수 있습니다. 이는 다음 코드 샘플에서 간략히 설명되어 있습니다.

```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

게이트웨이의 뒤에 있는 디바이스가 등록될 때 해당 디바이스는 `gwDeviceId` 및 `gwDeviceType` 속성의 값으로 게이트웨이와 연관됩니다. 

## 이벤트 공개
{: #publish_events}

이벤트는 게이트웨이 및 디바이스가 {{site.data.keyword.iot_short_notm}}에 데이터를 공개하는 메커니즘입니다. 게이트웨이 또는 디바이스는 이벤트의 컨텐츠를 제어하며, 자신이 전송하는 각 이벤트마다 이름을 지정합니다. 게이트웨이는 자체에서 이벤트를 공개하고 게이트웨이를 통해 연결된 디바이스 대신 이벤트를 공개할 수 있습니다. 

{{site.data.keyword.iot_short_notm}} 인스턴스가 이벤트를 수신할 때 수신된 이벤트의 신임 정보는 전송 중인 게이트웨이를 식별하며, 이는 게이트웨이가 다른 디바이스로 위장할 수 없음을 의미합니다. 

이벤트는 MQTT 프로토콜을 통해 정의한 세 개의 [서비스 품질(QoS) 레벨](../../reference/mqtt/index.html#qos-levels)에서 공개할 수 있습니다. 기본적으로 이벤트는 QoS=0에서 공개됩니다.

### 기본 QoS 레벨에서 게이트웨이 이벤트를 공개하기 위한 코드

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### 이벤트의 기본 QoS 레벨 증가를 위한 코드

공개된 게이트웨이 이벤트의 [QoS 레벨](../../reference/mqtt/index.html#qos-levels)을 증가시킬 수 있습니다. 포함된 추가 확인 수신 정보로 인해 QoS 레벨이 0보다 큰 이벤트는 공개하는 데 더 오래 걸릴 수 있습니다. 


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### 사용자 정의 형식의 이벤트를 공개하기 위한 코드

여러 형식(예: JSON, 문자열, 2진 등)으로 이벤트를 공개할 수 있습니다. 기본적으로 라이브러리는 JSON 형식의 이벤트를 공개하지만 원하는 경우 다른 형식의 데이터를 지정할 수 있습니다. 예를 들어, 문자열 형식으로 데이터를 공개하려면 다음 코드 스니펫을 사용하십시오. 

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**참고:** 이전 코드 예에서 이벤트의 페이로드는 문자열 형식이어야 합니다.

XML 데이터는 다음 코드 샘플에서 간략하게 설명된 대로 문자열 형식으로 변환되고 공개될 수 있습니다. 

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

이와 유사하게 2진 형식의 이벤트를 공개하려면 다음 예에 설명된 바이트 배열을 사용하십시오.

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### 디바이스의 이벤트를 공개하기 위한 코드
{: #publishing_events_devices}

게이트웨이는 원래 이벤트의 적합한 유형 ID 및 디바이스 ID 값을 전달하여 게이트웨이를 통해 연결된 디바이스 대신 이벤트를 공개할 수 있으며, 이는 다음 샘플에서 간략하게 설명되어 있습니다. 

```java

gwClient.connect()

//Generate the event to be published
JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  60);
event.addProperty("mem",  40);

// publish the event on behalf of device
gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

오버로드된 `publishDeviceEvent()` 메소드를 사용하면 원하는 서비스 품질(QoS) 레벨에서 디바이스 이벤트를 공개할 수 있습니다. 사용되는 주제 구조에 대한 자세한 정보는 [게이트웨이용 MQTT 연결](../mqtt.html)을 참조하십시오. 

### 사용자 정의 형식인 디바이스 이벤트를 공개하기 위한 코드

게이트웨이 이벤트와 유사하게, 디바이스 이벤트 역시 다양한 형식으로 공개될 수 있습니다. 기본적으로 라이브러리는 JSON 형식으로 디바이스 이벤트를 공개하지만, 사용자가 원하면 다양한 형식으로 데이터를 지정할 수 있습니다. 예를 들어, 문자열 형식으로 데이터를 공개하려면 다음 코드 샘플을 사용하십시오. 

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**참고:** 이벤트의 페이로드는 문자열 형식이어야 합니다. 

XML 데이터는 다음 예제에 표시된 대로 문자열 형식으로 변환되고 공개될 수 있습니다. 

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

유사하게, 2진 형식으로 디바이스 이벤트를 공개하려면 다음 예제에서 간략하게 설명된 바이트 배열을 사용하십시오. 
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## 명령 처리
{: #handling_commands}

게이트웨이는 게이트웨이 자체에서 지시된 명령과 게이트웨이 뒤에서 연결된 디바이스를 구독할 수 있습니다. 게이트웨이 클라이언트의 연결 시에 이는 이 게이트웨이에 대한 명령을 자동으로 구독합니다. 그러나 게이트웨이를 통해 연결된 디바이스에 대한 명령을 구독하려면 오버로드된 `subscribeToDeviceCommands()` 메소드를 사용하십시오. 이는 다음 예제에서 간략하게 설명되어 있습니다. 

```java
gwClient.connect()

// subscribe to commands on behalf of device
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

특정 명령을 처리하려면 `Command` 콜백 메소드를 등록해야 합니다. 메시지는 `Command` 클래스의 인스턴스로서 리턴되며 다음 특성을 포함하고 있습니다. 


| 특성     |데이터 유형     | 설명 |
|----------------|----------------|---------------
|`deviceType`|문자열| 명령이 수신되는 디바이스 유형입니다. |
|`deviceId`|문자열| 명령이 수신되는 디바이스 ID이며, 이는 게이트웨이 또는 게이트웨이를 통해 연결된 디바이스일 수 있습니다. |
|`data`|오브젝트| 명령 페이로드입니다. |
|`format`|문자열| 명령 페이로드의 형식이며, 이는 문자열(예: JSON), 2진, 텍스트 또는 기타 형식일 수 있습니다. |
|`command`|문자열|명령의 이름입니다. |
|`timestamp`|org.joda.time.DateTime|명령이 전송된 시점의 날짜 및 시간입니다. |

다음 코드 샘플은 `Command` 콜백 메소드를 구현할 수 있는 방법을 간략하게 설명합니다. 

```java
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
	// A queue to hold and process the commands
	private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

	public void processCommand(Command cmd) {
  	    queue.put(cmd);
  	}

  	public void run() {
  	    while(true) {
  	        Command cmd = queue.take();
  	        System.out.println("Command " + cmd.getData());

  	        // code to process the command
  	    }
  	}

  	/**
	 * If a gateway subscribes to a topic of a device or sends data on behalf of a device
	 * that the gateway does not have permission to connect to, the message or the subscription is ignored.
	 * This behavior is different compared with the behavior of applications, where the connection is terminated.
	 * The Gateway is notified on the the notification topic:
	 */
  	@Override
public void processNotification(Notification notification) {

}
  }

```
`Command` 콜백이 게이트웨이 클라이언트에 추가되는 경우, `processCommand()` 메소드는 구독된 기준이 있는 명령이 호출될 때마다 공개됩니다.

다음 코드 샘플은 게이트웨이 클라이언트 인스턴스로 `Command` 콜백을 추가하는 방법을 간략하게 설명합니다. 

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Subscribe to a device that is connected to the gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

오버로드된 메소드를 명령 구독을 제어하는 데 사용할 수 있습니다. 

### 게이트웨이를 통해 연결된 디바이스 나열
{: #list_devices_gw}


지정된 게이트웨이(typeId, deviceId)를 통해 {{site.data.keyword.iot_short_notm}}에 연결된 모든 디바이스를 검색하려면 `getDevicesConnectedThroughGateway()` 메소드를 호출하십시오. 

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## 샘플
{: #samples}

게이트웨이 및 게이트웨이 뒤에 있는 디바이스를 {{site.data.keyword.iot_short_notm}} 인스턴스에 연결하는 데 도움이 되도록 여러 샘플이 사용 가능합니다. 샘플은 {{site.data.keyword.iot_short_notm}} Java 클라이언트 라이브러리를 사용하며 [게이트웨이 샘플 GitHub 저장소](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples)에 있습니다. 

## 레시피
{: #recipes}

| 레시피     | 설명 |
|----------------|----------------
|[{{site.data.keyword.iot_short_notm}}에 게이트웨이로서 디바이스 연결](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/)| Raspberry Pi 게이트웨이 및 게이트웨이 뒤의 Arduino Uno 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하는 방법을 설명하는 GitHub 프로젝트 및 세부 지시사항입니다.
|[{{site.data.keyword.iot_short_notm}}의 관리 게이트웨이로서 Raspberry Pi](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/)|{{site.data.keyword.iot_short_notm}}에서 관리 디바이스로서 Raspberry Pi를 연결하는 방법과 디바이스 관리 오퍼레이션을 수행하는 방법을 설명하는 이전 게이트웨이 레시피의 확장판입니다.
