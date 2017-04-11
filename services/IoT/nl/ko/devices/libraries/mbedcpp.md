---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 디바이스 개발자용 mBed C++
{: #mbedcpp}

[mBed C++ 클라이언트 라이브러리 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window}를 사용하여 [mBed 디바이스 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.mbed.com/en/){: new_window}(예: [LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) 또는 [FRDM-K64F ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/platforms/FRDM-K64F/){: new_window})를 {{site.data.keyword.iot_full}} 서비스에 쉽게 연결합니다.
{:shortdesc}

자세한 정보는 [developer.mbed.org ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/){: new_window}의 [ibmiotf ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window}를 참조하십시오. 

라이브러리에서 C++를 사용하기는 하지만 mBed 디바이스에 간혹 포팅을 어렵게 하는 특이한 메모리 모델이 있으므로 동적 메모리 할당과 STL 함수 사용을 방지합니다. 이 경우 라이브러리를 사용하면 메모리 사용을 최대한 예측할 수 있습니다.

## 종속 항목
{: #dependencies}

|종속 항목 |설명 |
|:---|:---|
|[Eclipse Paho MQTT 라이브러리 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/teams/mqtt/code/MQTT/){: new_window}|mBed 디바이스의 MQTT 클라이언트 라이브러리를 제공합니다. 자세한 정보는 [임베디드 MQTT C/C++ 클라이언트 라이브러리 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}|
|[EthernetInterface 라이브러리 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/){: new_window}|이더넷을 통한 mBed IP 라이브러리.|

## 라이브러리 사용 방법
{: #library_use}

mBed C++ IBMIoTF 클라이언트 라이브러리를 사용하는 경우 [mBed 컴파일러 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/compiler/){: new_window}를 사용하여 애플리케이션을 작성하십시오. mBed 컴파일러에서는 mBed 마이크로 컨트롤러에서 실행할 프로그램을 쓰고 컴파일하며 다운로드하도록 구성된 경량의 온라인 C/C++ IDE를 제공합니다.

**참고:** mBed와 실행하도록 설치하거나 설정할 사항이 없습니다.

ARM mBed NXP LPC 1768 마이크로 컨트롤러를 {{site.data.keyword.iot_short_notm}}에 연결하는 방법에 대한 정보는 [IBM Watson IoT Platform용 mBed C++ 클라이언트 라이브러리 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/){: new_window} 레시피를 참조하십시오. 

## 생성자
{: #constructor}

생성자가 클라이언트 인스턴스를 빌드하고 다음 매개변수를 승인합니다.

|매개변수 |설명  |
|:---|:---|
|`org` |조직 ID입니다. 이 값은 필수입니다. Quickstart 플로우를 사용 중인 경우 `quickstart`를 지정하십시오.|
|`type`   |디바이스 유형입니다. 이 필드는 필수입니다. |
|`id`   |디바이스 ID입니다. 이 필드는 필수입니다. |
|`auth-method`   |등록된 플로우에만 필요한 선택적 필드인 인증 메소드입니다. 현재 지원되는 값은 `token`입니다.|
|`auth-token`   |디바이스를 Watson IoT Platform에 안전하게 연결하기 위한 인증 토큰입니다. 이 필드는 등록된 플로우에만 필요한 선택적 필드입니다.|

이러한 매개변수는 {{site.data.keyword.iot_short_notm}} 서비스와 상호작용하는 데 사용되는 정의를 작성합니다.

다음 코드 샘플은 DeviceClient 인스턴스가 {{site.data.keyword.iot_short_notm}} Quickstart 서비스와 상호작용할 수 있는 방법을 간략하게 설명합니다.

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "quickstart";     // For a registered connection, replace with your org
  char deviceType[8] = "LPC1768";           // For a registered connection, replace with your device type
  char deviceId[3] = "01";                  // For a registered connection, replace with your device id

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId);

  // Get the DeviceID(MAC Address) if we are in quickstart mode and device ID is not specified
  if((strcmp(organization, QUICKSTART) == 0) && (strcmp("", deviceId) == 0))
  {
  	char tmpBuf[50];
  	client.getDeviceId(tmpBuf, sizeof(tmpBuf));
  }
  ....
```

이전 코드 샘플에 표시된 대로 디바이스 ID가 지정되지 않으면 DeviceClient에서 디바이스의 MAC 주소를 디바이스 ID로 사용하여 {{site.data.keyword.iot_short_notm}}에 연결합니다. 디바이스 코드에서 `getDeviceId()` 메소드를 사용하여 DeviceClient 인스턴스에서 디바이스 ID를 검색할 수 있습니다.

다음 코드 블록에서는 {{site.data.keyword.iot_short_notm}} 등록 조직과 상호작용하는 DeviceClient 인스턴스를 작성하는 방법을 보여줍니다.

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "hrcl78";
  char deviceType[8] = "LPC1768";
  char deviceId[3] = "LPC176801";
  char method[6] = "token";
  char token[9] = "password";

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);
  ....
```

## {{site.data.keyword.iot_short_notm}}에 연결
{: #connecting_to_iotp}

디바이스는 DeviceClient 인스턴스에서 연결 함수를 호출하여 {{site.data.keyword.iot_short_notm}}에 연결할 수 있습니다.

```
  #include "DeviceClient.h"
  ....
  ....

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
정상적으로 연결한 후 디바이스가 {{site.data.keyword.iot_short_notm}}에 이벤트를 공개하고 명령을 청취할 수 있습니다.

또한 디바이스에서 다음 예제에 표시된 `isConnected()` 메소드를 사용하여 연결 상태를 조회할 수 있습니다.

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## 이벤트 공개
{: #publishing_events}

이벤트는 디바이스가 {{site.data.keyword.iot_short_notm}}에 데이터를 공개하는 데 사용하는 메커니즘입니다. 디바이스에서 이벤트의 컨텐츠를 제어하고 전송하는 각 이벤트의 이름을 지정합니다.

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신할 때 수신된 이벤트의 신임 정보는 전송 중인 디바이스를 식별하며, 이는 디바이스가 다른 디바이스로 위장할 수 없음을 의미합니다. 

이벤트는 MQTT 프로토콜을 통해 정의한 세 개의 [서비스 품질(QoS) 레벨](../../reference/mqtt/index.html#qos-levels)에서 공개할 수 있습니다. 기본적으로, 이벤트는 QoS 0에서 공개됩니다. 

### 기본 서비스 품질(QoS)을 사용하여 이벤트 공개

다음 샘플은 JSON 형식으로 다음 데이터 점을 {{site.data.keyword.iot_short_notm}}에 공개하는 방법을 보여줍니다.

- LPC1768(예: x,y 및 z축)
- 조이스틱 위치
- 현재 온도 표시값

```
	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf);
	....
```
전체 샘플은 [ IBMIoTClientLibrarySample ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}을 참조하십시오.

### 이벤트의 QoS 레벨 증가

공개된 이벤트의 [QoS 레벨](../../reference/mqtt/index.html#qos-levels)을 늘릴 수 있습니다. 포함된 추가 확인 수신 정보로 인해 QoS 레벨이 `0`보다 큰 이벤트는 공개하는 데 더 오래 걸릴 수 있습니다.

**참고:** Quickstart 플로우 모드에서는 QoS 0만 지원합니다.

```
	#include "MQTTClient.h"

	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf, MQTT::QOS2);
	....
```

### 이벤트 공개 중에 연결 유실 오류 처리


`publishEvent()` 메소드에서 false 값을 리턴하면 연결 상태를 확인하고 연결이 유실된 경우 `reConnect()`를 호출할 수 있습니다.

```
	#include "MQTTClient.h"

	status = client.publishEvent("blink", buf, MQTT::QOS2);

	if(status == false) {
	    // Check if connection is lost and retry
	    while(!client.isConnected())
	    {
	        client.reConnect();
	        wait(5.0);
	    }
	}
	....
```
연결이 끊긴 상태에서 공개된 이벤트는 라이브러리에 저장되지 않으므로, 연결을 다시 설정한 후 해당 이벤트를 보내려면 디바이스에서 `publishEvent()` 메소드를 다시 호출해야 합니다.


## 명령 처리
{: #handling_commands}

디바이스 클라이언트가 연결되면 이 디바이스에 대한 명령을 자동으로 구독합니다. 특정 명령을 처리하려면 명령 콜백 메소드를 등록해야 합니다.
메시지는 명령 클래스의 인스턴스로 리턴되며, 다음과 같은 특성이 있습니다.

|특성 |설명 |
|:---|:---|
|`command` | 호출된 명령의 이름입니다.|  
|`format`  |이벤트의 형식입니다. 형식은 임의의 문자열일 수 있습니다(예: JSON).  |
|`payload`  |명령 페이로드의 데이터입니다. 최대 길이는 131072바이트입니다. |


다음 코드에서는 디바이스에서 blink 명령을 받을 때마다 callback 메소드를 실행하도록 애플리케이션의 LED blink interval 명령을 처리하고 DeviceClient 인스턴스에서 함수 처리를 설정하는 샘플 명령 호출 함수를 정의합니다.

```
    #include "DeviceClient.h"
    #include "Command.h"

    // Process the command and set the LED blink interval
    void processCommand(IoTF::Command &cmd)
    {
        if (strcmp(cmd.getCommand(), "blink") == 0)
    	{
    	    char *payload = cmd.getPayload();
    	    char* pos = strchr(payload, '}');
    	    if (pos != NULL) {
    	        *pos = '\0';
    	        char* ratepos = strstr(payload, "rate");
    	        if(ratepos == NULL)
    	            return;
    	        if ((pos = strchr(ratepos, ':')) != NULL)
    	        {
    	            int blink_rate = atoi(pos + 1);
    	            blink_interval = (blink_rate <= 0) ? 0 : (blink_rate > 50 ? 1 : 50/blink_rate);
    	        }
    	    }
    	} else {
            WARN("Unsupported command: %s\n", cmd.getCommand());
        }
    }

    client.setCommandCallback(processCommand);

    client.yield(1000);  // allow the MQTT client to receive messages
    ....
```
전체 샘플은 [ IBMIoTClientLibrarySample ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}을 참조하십시오.

**참고:** 명령을 받으려면 `client.yield()` 함수를 주기적으로 호출해야 합니다. `client.yield()` 함수를 사용하면 디바이스가 Watson IoT Platform에서 명령을 받고 연결을 활성 상태로 유지할 수 있습니다. keepAlive 간격으로 지정된 시간 범위 동안 `client.yield()` 함수가 호출되지 않으면 플랫폼에서 보낸 모든 명령을 디바이스에서 받지 못합니다. `client.yield()` 함수에 지정된 값은 애플리케이션에 제어를 리턴하기 전에 소켓에서 데이터를 읽을 수 있는 기간(밀리초)을 지정합니다.

## 클라이언트 연결 끊기
{: #disconnect_client}

클라이언트의 연결을 끊고 연결을 해제하려면 다음 코드 스니펫을 실행하십시오.

```
	...
	client.disconnect();
	....
```
## 샘플
{: #samples}

[IBMIoTClientLibrarySample ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/){: new_window}은 mbed LPC1768 또는 FRDM-K64F 디바이스를 서비스 인스턴스에 연결하기 위해 {{site.data.keyword.iot_short_notm}} 클라이언트 라이브러리의 사용 방법을 보여주는 코드 샘플입니다. 
