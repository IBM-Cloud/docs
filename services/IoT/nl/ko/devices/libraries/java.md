---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 디바이스 개발자용 Java
{: #java}

Java™를 사용하여 {{site.data.keyword.iot_full}}에서 조직과 상호작용하는 디바이스를 빌드하고 사용자 정의할 수 있습니다. 디바이스 개발을 시작하는 데 도움이 되도록 {{site.data.keyword.iot_short_notm}}의 Java 클라이언트 라이브러리, 문서 및 예가 제공됩니다.
{:shortdesc}

## Java 클라이언트 및 자원 다운로드
{: #java_client_download}

{{site.data.keyword.iot_short_notm}}의 Java 클라이언트 라이브러리 및 샘플에 액세스하려면 GitHub의 [iot-java](https://github.com/ibm-watson-iot/iot-java) 저장소로 이동하여 설치 지시사항을 완료하십시오.

## 생성자
{: #constructor}

생성자는 클라이언트 인스턴스를 빌드하며 다음 정의가 포함된 `Properties` 오브젝트를 허용합니다.

|정의 |설명  |
|:----|:----|
|`org` |조직 ID로 설정해야 하는 필수 값입니다. Quickstart 플로우를 사용 중인 경우 `quickstart`를 지정하십시오.|
|`type`  |디바이스의 유형을 지정하는 필수 값입니다.|
|`id`  |디바이스의 고유 ID를 지정하는 필수 값입니다.|
|`auth-method`  |사용할 인증 메소드입니다. 지원되는 유일한 메소드는 `token`입니다.|
|`auth-token`   |디바이스를 {{site.data.keyword.iot_short_notm}}에 안전하게 연결하기 위한 인증 토큰입니다.|
|`clean-session`|지속 가능한 구독 모드로 애플리케이션에 연결을 원하는 경우에만 필요한 true 또는 false 값입니다. 기본적으로 `clean-session`은 true로 설정됩니다.|
|`Port`|연결할 포트 번호입니다. 8883 또는 443을 지정하십시오. 포트 번호를 지정하지 않으면 기본적으로 클라이언트가 포트 번호 8883의 {{site.data.keyword.iot_short_notm}}에 연결됩니다.|
|`MaxInflightMessages`  |연결을 위한 인플라이트 메시지의 최대 수를 설정합니다. 기본값은 100입니다.|
|`Automatic-Reconnect`  |연결이 끊긴 상태일 때 {{site.data.keyword.iot_short_notm}}에 디바이스를 자동으로 다시 연결하려는 경우에 필요한 true 또는 false 값입니다. 기본값은 false입니다.|
|`Disconnected-Buffer-Size`|클라이언트가 연결이 끊겼을 때 메모리에 저장할 수 있는 최대 메시지 수입니다. 기본값은 5000입니다.|
|`WebSocket`|{{site.data.keyword.iot_short_notm}}에서 WebSocket 연결을 사용하고자 할 때 필요한 true 또는 false 값입니다. 기본값은 false입니다.|

**참고:** 지속적 구독 모드에서 디바이스를 연결하려면 `clean-session`을 `false`로 설정하십시오. 정리 세션에 대한 자세한 정보는 [MQTT 문서](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)의 '구독 버퍼 및 정리 세션' 섹션을 참조하십시오.

`Properties` 오브젝트는 {{site.data.keyword.iot_short_notm}} 모듈과 상호작용하는 데 사용되는 정의를 작성합니다. 

다음 코드 샘플은 디바이스가 Quickstart 모드에서 이벤트를 공개하는 방법을 표시합니다.

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data using Properties class
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Quickstart flow allows only QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

다음 코드 샘플에서는 디바이스가 등록된 플로우에서 이벤트를 공개하는 방법을 보여줍니다.


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### 구성 파일 사용

`Properties` 오브젝트를 직접 사용하지 않고 특성의 이름-값 쌍을 포함하는 구성 파일을 사용할 수 있습니다. `Properties` 오브젝트를 포함하는 구성 파일을 사용하는 경우 다음 코드 형식을 사용하십시오.

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

구성 파일 컨텐츠의 형식은 다음 형식이어야 합니다.

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## {{site.data.keyword.iot_short_notm}}에 연결
{: #connecting_to_iotp}


{{site.data.keyword.iot_short_notm}}에 연결하려면 `connect()` 함수를 사용하십시오. `connect()` 함수에는 MqttException 연결에 실패할 때 라이브러리가 다시 연결을 시도하는지 여부를 판별하는 `autoRetry`라고 하는 선택적 부울 매개변수가 포함되어 있습니다. 기본적으로, `autoRetry`는 true로 설정됩니다. 잘못된 디바이스 등록 세부사항이 전달되었으므로 MqttSecurityException 연결에 실패하는 경우에는 `autoRetry`가 true로 설정되어 있어도 라이브러리가 다시 연결을 시도하지 않습니다.

MQTT에 대한 '활성 유지' 간격을 설정하기 위해 `connect()` 함수를 호출하기 전에 선택적으로 `setKeepAliveInterval(int)` 메소드를 사용할 수 있습니다. `setKeepAliveInterval(int)` 값은 초 단위로 측정되며 보내거나 받는 메시지 간 최대 시간 간격을 정의합니다. 이 메소드를 사용하면 클라이언트는 TCP/IP 제한시간이 끝나기를 기다리지 않고도 서버를 더 이상 사용할 수 없는 경우를 발견할 수 있습니다. 클라이언트에서는 하나 이상의 메시지가 각 '활성 유지' 간격 내에 네트워크를 통과할 수 있습니다. 0개의 데이터 관련 메시지가 제한시간 중에 수신되면 클라이언트는 서버가 수신확인하는 작은 `ping` 메시지를 발송합니다. `setKeepAliveInterval(int)`는 기본적으로 60초로 설정됩니다. 클라이언트에서 '활성 유지' 처리 기능을 사용 안함으로 설정하려면 `setKeepAliveInterval(int)` 값을 0으로 설정하십시오.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

연결이 실패할 때 발생하는 재시도 수를 제어하려면 오버로드된 connect(int numberOfTimesToRetry) 함수를 사용하십시오.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

디바이스가 {{site.data.keyword.iot_short_notm}}에 연결되면 이벤트를 공개하고 애플리케이션의 디바이스 명령을 구독할 수 있습니다.


## 이벤트 공개
{: #publishing_events}

이벤트는 디바이스가 {{site.data.keyword.iot_short_notm}}에 데이터를 공개하는 데 사용하는 메커니즘입니다. 디바이스에서 이벤트의 컨텐츠를 제어하고 전송하는 각 이벤트의 이름을 지정합니다.

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신할 때 수신된 이벤트의 신임 정보는 전송 중인 디바이스를 식별하며, 이는 디바이스가 다른 디바이스로 위장할 수 없음을 의미합니다. 

이벤트는 MQTT 프로토콜을 통해 정의한 세 개의 [서비스 품질(QoS) 레벨](../../reference/mqtt/index.html#qos-levels)에서 공개할 수 있습니다. 기본적으로 이벤트는 QoS=0에서 공개됩니다.

### 기본 QoS 레벨에서 이벤트 공개

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### 이벤트의 QoS 레벨 증가

공개된 이벤트의 [QoS 레벨](../../reference/mqtt/index.html#qos-levels)을 늘릴 수 있습니다. 포함된 추가 확인 수신 정보로 인해 QoS 레벨이 0보다 큰 이벤트는 공개하는 데 더 오래 걸릴 수 있습니다.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### 사용자 정의 형식의 이벤트 공개

여러 형식(예: JSON, 문자열, 2진 등)으로 이벤트를 공개할 수 있습니다. 기본적으로 라이브러리는 JSON 형식의 이벤트를 공개하지만 원하는 경우 다른 형식의 데이터를 지정할 수 있습니다. 예를 들어, 문자열 형식의 데이터를 공개하려면 다음 코드 스니펫을 사용하십시오.

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
status = myClient.publishEvent("load", data, "text", 2);
```

**참고:** 이전 코드 예에서 이벤트의 페이로드는 문자열 형식이어야 합니다.

임의 XML 데이터를 다음과 같이 문자열 형식으로 변환하고 공개할 수 있습니다.

```
status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

이와 유사하게 2진 형식의 이벤트를 공개하려면 다음 예에 설명된 바이트 배열을 사용하십시오.

```
myClient.connect();

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### HTTP를 사용하여 이벤트 공개
{: #publishing_events_http}


MQTT 외에 HTTP를 사용하여 {{site.data.keyword.iot_short_notm}}에 이벤트를 공개하도록 디바이스를 구성할 수 있습니다. 다음 단계에서는 HTTP를 통해 이벤트를 공개하는 순서를 설명합니다.

1. 특성 파일을 사용하여 `DeviceClient` 인스턴스를 생성하십시오.
2. 공개해야 하는 이벤트를 생성하십시오.
3. 다음 코드 샘플에 표시된 대로 이벤트 이름을 지정한 다음 `publishEventOverHTTP()` 메소드를 사용하여 이벤트를 공개하십시오.

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

전체 코드를 보려면 [HttpDeviceEventPublish] 디바이스 예를 참조하십시오.

특성 파일의 설정을 기반으로 `publishEventOverHTTP()` 메소드가 Quickstart 모드 또는 등록된 플로우 모드로 이벤트를 공개합니다. 특성 파일의 조직 ID를 `quickstart`로 설정한 경우 `publishEventOverHTTP()` 메소드는 이벤트를 디바이스 예제 Quickstart 서비스에 이벤트를 공개하고 일반 HTTP 형식의 이벤트를 공개합니다. 올바른 등록 조직이 특성 파일에 지정된 경우, 이벤트는 HTTPS를 통해 안전하게 공개됩니다.

HTTP 프로토콜은 '최대 한 번' 전달을 제공하며, 이는 MQTT 프로토콜의 '최대 한 번'(QoS 0) 서비스 품질 레벨과 유사합니다. '최대 한 번' 제공을 사용하여 이벤트를 공개하는 경우 애플리케이션은 오류가 발생할 때마다 재시도하는 로직을 구현해야 합니다.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## 명령 처리
{: #handling_commands}

디바이스 클라이언트가 연결되면 이 디바이스에 대한 명령을 자동으로 구독합니다. 특정 명령을 처리하려면 명령 콜백 메소드를 등록해야 합니다.
메시지는 `Command` 클래스의 인스턴스로 리턴되며, 다음과 같은 특성이 있습니다.

| 특성     |데이터 유형     | 설명 |
|----------------|----------------|
|`payload` |java.lang.String| 메시지 페이로드의 데이터입니다.|
|`format`  |java.lang.String| 형식은 임의의 문자열일 수 있습니다(예: JSON). |
|`command`   |java.lang.String|명령을 식별합니다.|
|`timestamp`   |org.joda.time.DateTime|이벤트의 날짜 및 시간입니다.|


``` sourceCode
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//Implement the CommandCallback class to provide the way in which you want the command to be handled
class MyNewCommandCallback implements CommandCallback, Runnable {

    // A queue to hold & process the commands for smooth handling of MQTT messages
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    /**
    * This method is invoked by the library whenever there is command matching the subscription criteria
    */
    @Override
    public void processCommand(Command cmd) {
        try {
            queue.put(cmd);
            } catch (InterruptedException e) {
        }
    }

    @Override
    public void run() {
        while(true) {
            Command cmd = null;
            try {
                //In this sample, we just display the command
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Pass the above implemented CommandCallback as an argument to this device client
        myClient.setCommandCallback(new MyNewCommandCallback());

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## 샘플
{: #samples}

{{site.data.keyword.iot_short_notm}} Java 클라이언트 라이브러리를 사용하여 개발된 디바이스 관리 샘플 및 디바이스의 목록은 [iot-device-samples GitHub 저장소](https://github.com/ibm-messaging/iot-device-samples/tree/master/java)를 참조하십시오. 
