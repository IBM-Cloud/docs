---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 애플리케이션 개발자용 Java
{: #java}

마지막 업데이트 날짜: 2016년 9월 7일
{: .last-updated}

Java를 사용하여 {{site.data.keyword.iot_full}}에서 조직과 상호작용하는 애플리케이션을 빌드하고 사용자 정의할 수 있습니다. 제공된 정보와 예제를 사용하면 Java를 사용한 애플리케이션 개발을 시작할 수 있습니다.
{:shortdesc}

## Java 클라이언트 및 자원 다운로드
{: #java_client_download}

{{site.data.keyword.iot_short_notm}}의 Java 클라이언트 라이브러리 및 샘플에 액세스하려면 GitHub의 [iot-java](https://github.com/ibm-watson-iot/iot-java) 저장소로 이동하여 설치 지시사항을 완료하십시오. 


## 생성자
{: #constructor}

생성자는 클라이언트 인스턴스를 빌드하며 다음 정의가 포함된 `Properties` 오브젝트를 허용합니다. 

| 정의     |설명     |
|----------------|----------------|
|`org` |조직 ID입니다. 이는 필수 값입니다. Quickstart 플로우를 사용 중인 경우 `quickstart`를 지정하십시오. |
|`id` |조직 내에서 애플리케이션의 고유 ID입니다. |
|`auth-method`  |인증 메소드이며, 이에 대해 현재 지원되는 유일한 값은 `apikey`입니다. |
|`auth-key`   |auth-method가 `apikey`로 설정될 때 필요한 선택적 API 키입니다.   |
|`auth-token`   |auth-method가 `apikey`로 설정될 때 필요한 API 키 토큰입니다.  |
|`clean-session`|지속 가능한 구독 모드로 애플리케이션에 연결을 원하는 경우에만 필요한 true 또는 false 값입니다. 기본적으로 `clean-session`은 `true`로 설정됩니다. |
|`shared-subscription`|부울 값입니다. 애플리케이션의 여러 인스턴스 간에 메시지를 로드 밸런싱하는 확장 가능한 애플리케이션을 빌드하려면 `true`로 설정하십시오. 자세한 정보는 [확장 가능한 애플리케이션](mqtt.html#/scalable-applications#scalable-applications)을 참조하십시오.

`Properties` 오브젝트는 {{site.data.keyword.iot_short_notm}} 모듈과 상호작용하는 데 사용되는 정의를 작성합니다. 이 오브젝트의 특성을 지정하지 않거나 `quickstart`를 지정하는 경우, 클라이언트는 미등록 디바이스로서 {{site.data.keyword.iot_short_notm}} Quickstart 서비스에 연결합니다. 

다음 코드 샘플은 `quickstart` 모드에서 ApplicationClient 인스턴스를 생성할 수 있는 방법을 표시합니다. 

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

다음 코드 샘플은 등록된 플로우 모드에서 ApplicationClient 인스턴스를 생성할 수 있는 방법을 표시합니다. 

```
    Properties options = new Properties();
    options.put("org", "uguhsp");
    options.put("id", "app" + (Math.random() * 10000));
    options.put("Authentication-Method","apikey");
    options.put("API-Key", "<API-Key>");
    options.put("Authentication-Token", "<Authentication-Token>");

    ApplicationClient myClient = new ApplicationClient(options);
```

### 구성 파일 사용

`Properties` 오브젝트를 직접 포함하는 대신, 다음 형식으로 `Properties` 오브젝트에 대한 이름-값 쌍이 포함된 구성 파일을 사용할 수 있습니다. 

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
애플리케이션 구성 파일은 다음 형식이어야 합니다.

```
    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token
    enable-shared-subscription=true|false
```

## {{site.data.keyword.iot_short_notm}}에 연결
{: #connecting_to_iotp}

{{site.data.keyword.iot_short_notm}}에 연결하려면 `connect()` 함수를 사용하십시오. `connect()` 함수에는 MqttException 연결에 실패할 때 라이브러리가 다시 연결을 시도하는지 여부를 판별하는 `autoRetry`라고 하는 선택적 부울 매개변수가 포함되어 있습니다. 기본적으로, `autoRetry`는 true로 설정됩니다. 잘못된 디바이스 등록 세부사항이 전달되었으므로 MqttSecurityException 연결에 실패하는 경우에는 `autoRetry`가 `true`로 설정되어 있어도 라이브러리가 다시 연결을 시도하지 않습니다. 

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);

    myClient.connect();
```

{{site.data.keyword.iot_short_notm}} 서비스에 성공적으로 연결된 후에는 애플리케이션 클라이언트가 디바이스 이벤트를 구독하고 디바이스 상태를 구독하며 디바이스 이벤트와 명령을 공개할 수 있습니다. 

## 디바이스 이벤트 구독
{: #subscribing_device_events}

이벤트는 디바이스가 {{site.data.keyword.iot_short_notm}}에 데이터를 공개하는 메커니즘입니다. 디바이스는 이벤트의 컨텐츠를 제어하며 전송 중인 각 이벤트에 대해 이름을 지정합니다. 

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신할 때 수신된 이벤트의 신임 정보는 전송 중인 디바이스를 식별하며, 이는 디바이스가 다른 디바이스로 위장할 수 없음을 의미합니다. 


기본적으로, 애플리케이션은 연결된 모든 디바이스의 모든 이벤트를 구독합니다. 디바이스 유형, 디바이스 ID, 이벤트 및 메시지 형식 매개변수를 사용하면 구독의 범위를 제어할 수 있습니다. 다음 코드 샘플은 이러한 매개변수를 사용하여 구독의 범위를 정의할 수 있는 방법을 표시합니다. 

### 모든 디바이스의 모든 이벤트 구독


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### 특정 유형인 모든 디바이스의 모든 이벤트 구독


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino");
```

### 특정 디바이스의 모든 이벤트 구독


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee");
```
### 둘 이상의 서로 다른 디바이스의 특정 이벤트 구독

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-arduino", "10aabbccddee", "myEvent");
```
### JSON 형식으로 공개된 이벤트 구독


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent", "json", 0);
```

**참고**: 하나의 클라이언트는 여러 구독을 지원할 수 있습니다. 

## 디바이스에서 이벤트 처리
{: #handling_device_events}

구독으로 수신된 이벤트를 처리하려면 이벤트 콜백 메소드를 등록하십시오. 메시지는 이벤트 클래스의 인스턴스로 리턴되며, 해당 매개변수는 다음과 같습니다. 

|매개변수|데이터 유형|설명|
|:---|:---|
|`event.device`|문자열|조직의 모든 유형의 디바이스 간에 디바이스를 고유하게 식별합니다. |
|`event.deviceType`|문자열|디바이스 유형을 식별합니다. 일반적으로, deviceType은 특정 태스크를 수행하는 디바이스의 그룹화입니다(예: "weatherballoon"). |
|`event.deviceId`|문자열|디바이스의 ID를 표시합니다. 일반적으로, 제공된 디바이스 유형의 경우 deviceId는 해당 디바이스의 고유 ID입니다(예: 일련 번호 또는 MAC 주소). |
|`event.event`|문자열|일반적으로, 특정 이벤트를 그룹화하는 데 사용됩니다(예: "상태", "경고" 및 "데이터"). |
|`event.format`|문자열|형식은 임의의 문자열일 수 있습니다(예: JSON).   |
|`event.data`|사전|메시지 페이로드의 데이터입니다. 최대 길이는 131072바이트입니다. |
|`event.timestamp`|날짜 및 시간 |이벤트의 날짜 및 시간입니다. |


다음 코드는 이벤트 콜백의 샘플 구현을 제공합니다. 

```
  import com.ibm.iotf.client.app.Event;
  import com.ibm.iotf.client.app.EventCallback;
  import com.ibm.iotf.client.app.Command;

  import java.util.concurrent.BlockingQueue;
  import java.util.concurrent.LinkedBlockingQueue;

  /**
    * A sample Event callback class that processes the device events in a separate thread.
    *
    */
   class MyEventCallback implements EventCallback, Runnable {

	// A queue to hold and process the Events for smooth handling of MQTT messages
	private BlockingQueue<Event> evtQueue = new LinkedBlockingQueue<Event>();

	public void processEvent(Event e) {
		try {
			evtQueue.put(e);
		} catch (InterruptedException e1) {
			e1.printStackTrace();
		}
	}

	@Override
	public void processCommand(Command cmd) {
		System.out.println("Command received:: " + cmd);
	}

	@Override
	public void run() {
		while(true) {
			Event e = null;
			try {
				e = evtQueue.take();
				// In this example, the only output is the event
				System.out.println("Event:: " + e.getDeviceId() + ":" + e.getEvent() + ":" + e.getPayload());
			} catch (InterruptedException e1) {
				// Ignore the Interuppted exception, retry
				continue;
			}
		}
	}
    }
```

ApplicationClient에 이벤트 콜백이 추가되는 경우, `processEvent()` 메소드는 구독과 일치하는 이벤트가 공개될 때마다 호출됩니다. 다음 스니펫은 ApplicationClient 인스턴스에 이벤트 콜백을 추가하는 방법을 표시합니다. 



```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceEvents();
```

디바이스 이벤트 구독과 유사하게, 애플리케이션은 디바이스에 전송된 명령을 구독할 수 있습니다. 다음 코드 샘플은 조직의 모든 디바이스에 대해 모든 명령을 구독하는 방법을 표시합니다. 

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

오버로드된 메소드를 명령 구독을 제어하는 데 사용할 수 있습니다. `processCommand()` 메소드는 명령 구독과 일치하는 디바이스에 명령이 전송될 때 호출됩니다. 


## 디바이스 상태 구독
{: #subscribing_device_status}

디바이스 이벤트 구독과 유사하게, 애플리케이션은 디바이스 상태를 구독할 수 있습니다(예: {{site.data.keyword.iot_short_notm}}에 디바이스 연결 및 연결 끊기). 기본적으로, 이 구독은 연결된 모든 디바이스의 상태 업데이트를 구독합니다. 디바이스 유형 및 디바이스 id 매개변수를 사용하면 구독의 범위를 제어할 수 있습니다. 다음 코드 샘플은 이러한 매개변수를 사용하여 구독의 범위를 정의할 수 있는 방법을 표시합니다. 

### 모든 디바이스의 상태 업데이트 구독

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### 특정 유형인 모든 디바이스의 상태 업데이트 구독


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino");
```

### 두 개의 서로 다른 디바이스의 상태 업데이트 구독


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-arduino", "10aabbccddee");
```

**참고**: 하나의 클라이언트는 여러 구독을 지원할 수 있습니다. 

## 디바이스에서 상태 업데이트 처리
{: #handling_device_status_updates}

구독으로 수신된 상태 업데이트를 처리하려면 상태 이벤트 콜백 메소드를 등록해야 합니다. `Connect` 및 `Disconnect` 상태 이벤트의 경우에는 메시지가 상태 클래스의 인스턴스로서 리턴되며, 여기에는 다음 매개변수가 포함됩니다. 


| 매개변수     |데이터 유형     |
|----------------|----------------|
|`status.clientAddr` |문자열|
|`status.protocol`  |문자열|
|`status.clientId`   |문자열|
|`status.user`   |문자열|
|`status.time`   |java.util.Date|
|`status.action` |문자열|
|`status.connectTime`   |java.util.Date|
|`status.port`|정수|

다음 특성은 상태 이벤트가 `Disconnect`인 경우에만 설정됩니다. 

| 특성     |데이터 유형     |
|----------------|----------------|
|`status.writeMsg` |정수|
|`status.readMsg`  |정수|
|`status.reason`   |문자열|
|`status.readBytes`   |정수|
|`status.writeBytes`   |정수|


다음 코드 샘플은 상태 콜백의 구현 예제를 제공합니다. 

```

  private static class MyStatusCallback implements StatusCallback {

      public void processApplicationStatus(ApplicationStatus status) {
          System.out.println("Application Status = " + status.getPayload());
      }

      public void processDeviceStatus(DeviceStatus status) {
          if(status.getAction() == "Disconnect") {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction()
                                  + "  reason: " + status.getReason());
          } else {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction());
          }
      }
  }
```

상태 콜백이 ApplicationClient에 추가되는 경우, `processDeviceStatus()` 메소드는 기준과 일치하는 디바이스가 {{site.data.keyword.iot_short_notm}}에 연결되거나 이와 연결 끊어질 때마다 호출됩니다. 다음 코드 샘플은 상태 콜백 인스턴스를 ApplicationClient에 추가할 수 있는 방법을 표시합니다. 

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
애플리케이션은 기타 애플리케이션 상태를 구독할 수 있습니다(예: Watson IoT Platform에 애플리케이션 연결 및 연결 끊기). 다음 코드 스니펫은 조직의 애플리케이션 상태를 구독하는 방법을 표시합니다.

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
오버로드된 메소드를 특정 애플리케이션에 대한 상태 구독을 제어하는 데 사용할 수 있습니다. processApplicationStatus() 메소드는 기준과 일치하는 애플리케이션이 {{site.data.keyword.iot_short_notm}}에 연결되거나 이와 연결 끊어질 때마다 호출됩니다.


## 디바이스에서 이벤트 공개
{: #publishing_events_devices}

다음 코드 샘플에서는 애플리케이션이 디바이스에서 가져온 것처럼 이벤트를 공개할 수 있는 방법을 표시합니다. 

```

    myClient.connect()

    //Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // publish the event on behalf of device
    myClient.publishEvent(deviceType, deviceId, "blink", event);
```

### HTTP를 사용하여 이벤트 공개
{: #publishing_events_http}

MQTT와 함께, 다음 단계를 비교함으로써 HTTP를 사용하여 {{site.data.keyword.iot_short_notm}}에 디바이스 이벤트를 공개하도록 애플리케이션을 구성할 수 있습니다. 

* 특성 파일을 사용하여 ApplicationClient 인스턴스 생성
* 공개되어야 하는 이벤트 생성
* 이벤트 이름, 디바이스 유형 및 디바이스 ID 지정
* 다음 코드에 표시된 대로 `publishEventOverHTTP`() 메소드를 사용하여 이벤트 공개:

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	code = myClient.publishEventOverHTTP(deviceType, deviceId, "blink", event);
```

전체 코드 샘플은 다음 애플리케이션 예제를 참조하십시오. 

[HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java)

특성 파일의 설정에 따라, `publishEventOverHTTP()` 메소드는 Quickstart에서 또는 등록된 플로우에서 이벤트를 공개합니다. `quickstart`가 특성 파일에 지정된 조직 ID인 경우, `publishEventOverHTTP()` 메소드는 이벤트를 일반 HTTP 형식으로 {{site.data.keyword.iot_short_notm}} Quickstart 서비스에 공개합니다. 올바른 등록 조직이 특성 파일에 지정된 경우, 이벤트는 모든 통신의 보안이 유지되도록 항상 HTTPS를 사용하여 공개됩니다. 

HTTP 프로토콜은 '최대 한 번' 전달을 제공하며, 이는 MQTT 프로토콜의 '최대 한 번'(QoS 0) 서비스 품질 레벨과 유사합니다. '최대 한 번' 전달을 사용하여 이벤트를 공개하는 경우, 애플리케이션은 오류 발생 시의 재시도 로직을 구현해야 합니다. 


## 디바이스에 명령 공개
{: #publishing_commands_devices}

다음 예제에 표시된 대로, 애플리케이션은 연결된 디바이스에 대한 명령을 공개할 수 있습니다. 

```

    myClient.connect()

    //Generate the event to be published
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //Registered flow allows 0, 1 and 2 QoS
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```


## 예제
{: #examples}


-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - 디바이스 이벤트를 공개할 수 있는 방법을 표시하는 샘플 애플리케이션입니다. 
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - 디바이스에 대한 명령을 공개할 수 있는 방법을 표시하는 샘플 애플리케이션입니다. 
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - 디바이스 이벤트, 디바이스 명령, 디바이스 상태 및 애플리케이션 상태 등의 다양한 이벤트를 구독할 수 있는 방법을 표시하는 샘플 애플리케이션입니다. 
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - 애플리케이션의 여러 인스턴스 간의 메시지를 로드 밸런싱하는 확장 가능한 애플리케이션을 빌드할 수 있는 방법을 표시하는 샘플 애플리케이션입니다. 
-  [백업 및 복원 샘플](https://github.com/ibm-messaging/iot-backup-restore-sample) - Cloudant NoSQL 데이터베이스에서 디바이스 구성을 백업하고 복원할 수 있는 방법을 표시하는 샘플입니다. 
