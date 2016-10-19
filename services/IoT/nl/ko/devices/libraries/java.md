---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 디바이스 개발자용 Java
{: #java}

마지막 업데이트 날짜: 2016년 8월 2일
{: .last-updated}


{{site.data.keyword.iot_full}}에서 조직과 상호작용하는 디바이스를 빌드하고 사용자 정의하는 데 Java를 사용할 수 있습니다. Java를 사용하여 디바이스 디버깅을 시작하도록 제공된 예와 정보를 사용하십시오.
{:shortdesc}

## Java 클라이언트 및 자원 다운로드
{: #java_client_download}

{{site.data.keyword.iot_short_notm}}의 Java 클라이언트 라이브러리 및 샘플에 액세스하려면 GitHub의 [iot-java](https://github.com/ibm-watson-iot/iot-java) 저장소로 이동하여 설치 지시사항을 완료하십시오.


## 생성자
{: #constructor}

생성자가 클라이언트 인스턴스를 빌드하고 다음 정의를 포함하는 특성 오브젝트를 승인합니다.

|정의 |설명  |
|:---|:---|
|`org` |조직 ID입니다. 이 필드는 필수입니다. Quickstart 플로우를 사용 중인 경우 `quickstart`를 지정하십시오.|
|`type`  |디바이스 유형입니다. 이 필드는 필수입니다. |
|`id`  |디바이스 ID입니다. 이 필드는 필수입니다. |
|`auth-method`   |사용할 인증 메소드입니다. 현재 지원되는 값은 `토큰`뿐입니다.|
|`auth-token`   |디바이스를 Watson IoT Platform에 안전하게 연결하기 위한 인증 토큰입니다.|
|`clean-session`|지속 가능한 구독 모드로 애플리케이션에 연결을 원하는 경우에만 필요한 true 또는 false 값입니다. 기본적으로 `clean-session`은 `true`로 설정됩니다.|

**참고:** 지속적 구독 모드에서 디바이스를 연결하려면 `clean-session`을 `false`로 설정하십시오. 정리 세션에 대한 자세한 정보는 [MQTT 문서](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)의 '구독 버퍼 및 정리 세션' 섹션을 참조하십시오.

특성 오브젝트가 {{site.data.keyword.iot_short_notm}} 모듈과 상호작용하는 데 사용하는 정의를 작성합니다.

다음 코드는 Quickstart 모드에서 이벤트를 공개하는 디바이스를 보여줍니다.

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

특성 오브젝트를 직접 사용하지 않고 특성의 이름-값 쌍을 포함하는 구성 파일을 사용할 수 있습니다. 특성 오브젝트를 포함하는 구성 파일을 사용하는 경우 다음 코드 형식을 사용하십시오.

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

커넥터 함수를 호출하여 {{site.data.keyword.iot_short_notm}}에 연결하십시오. 연결 함수는 선택적 부울 매개변수 `autoRetry`를 사용하며, 이 값은 기본적으로 `true`입니다. `autoRetry` 매개변수를 사용하면 MqttException 오류 발생 시 라이브러리를 다시 연결할 수 있습니다. 올바르지 않은 디바이스 등록 세부사항이 사용되었으므로 `autoRetry` 매개변수가 `true`로 설정된 경우에도 MqttSecurityException 오류 발생 시 라이브러리가 다시 연결하지 않습니다.

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

{{site.data.keyword.iot_short_notm}} 서비스에 정상적으로 연결하고 나면 디바이스 클라이언트에서 이벤트 공개 및 애플리케이션에서 디바이스 명령 구독과 같은 오퍼레이션을 수행할 수 있습니다.


## 이벤트 공개
{: #publishing_events}

이벤트는 디바이스가 {{site.data.keyword.iot_short_notm}}에 데이터를 공개하는 데 사용하는 메커니즘입니다. 디바이스에서 이벤트의 컨텐츠를 제어하고 전송하는 각 이벤트의 이름을 지정합니다.

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신하면 수신된 이벤트의 신임 정보를 통해 전송 디바이스를 식별합니다. 즉, 디바이스가 다른 디바이스로 위장할 수 없습니다.

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

### HTTP를 사용하여 이벤트 공개

MQTT 외에도 디바이스는 HTTP 및 다음 단계를 사용하여 {{site.data.keyword.iot_short_notm}}에 이벤트를 공개할 수 있습니다.

* 특성 파일을 사용하여 DeviceClient 인스턴스를 생성합니다.
* 공개해야 하는 이벤트를 생성합니다.
* 다음 코드에 표시된 대로 이벤트 이름을 지정하고 `publishEventOverHTTP()` 메소드를 사용하여 이벤트를 공개합니다.

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

[HttpDeviceEventPublish] 디바이스 예에 전체 코드가 있습니다.

특성 파일의 설정을 기반으로 `publishEventOverHTTP()` 메소드가 Quickstart 모드 또는 등록된 플로우 모드로 이벤트를 공개합니다. 특성 파일의 조직 ID가 `quickstart`이면 `publishEventOverHTTP()` 메소드에서 디바이스 예제 Quickstart 서비스에 이벤트를 공개하고 일반 HTTP 형식으로 이벤트를 공개합니다. 특성 파일에서 올바른 등록 조직이 사용되는 경우 이 메소드는 모든 통신이 안전하도록 SSL을 통한 HTTP인 HTTPS로 언제나 이벤트를 공개합니다.

HTTP 프로토콜에서는 MQTT 프로토콜의 '최대 한 번'(QoS 0) 서비스 품질 레벨과 비슷한 '최대 한 번' 전달을 제공합니다. '최대 한 번' 제공을 사용하여 이벤트를 공개하는 경우 애플리케이션에서 오류 발생 시 재시도하는 로직을 구현해야 합니다.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## 명령 처리
{: #handling_commands}

디바이스 클라이언트가 연결되면 이 디바이스에 대한 명령을 자동으로 구독합니다. 특정 명령을 처리하려면 명령 콜백 메소드를 등록해야 합니다.
메시지는 명령 클래스의 인스턴스로 리턴되며, 다음과 같은 특성이 있습니다.

| 특성     |데이터 유형     | 설명 |
|----------------|----------------|
|`payload` |java.lang.String| 메시지 페이로드에 대한 데이터입니다.|
|`format`  |java.lang.String| 형식은 임의의 문자열(예: JSON)일 수 있습니다.|
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

{{site.data.keyword.iot_short_notm}} Java Client Library를 사용하여 개발한 디바이스 및 디바이스 관리 샘플 목록은 [GitHub 저장소](https://github.com/ibm-messaging/iot-device-samples/tree/master/java)를 참조하십시오.
