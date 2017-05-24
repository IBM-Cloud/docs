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


# 適用於裝置開發人員的 mBed C++
{: #mbedcpp}

使用 [mBed C++ 用戶端程式庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window} 可輕鬆將 [mBed 裝置 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.mbed.com/en/){: new_window}（例如 [LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) 或 [FRDM-K64F ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/platforms/FRDM-K64F/){: new_window}）連接至 {{site.data.keyword.iot_full}} 服務。
{:shortdesc}

如需相關資訊，請參閱 [developer.mbed.org ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/){: new_window} 上的 [ibmiotf ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window}。

雖然程式庫使用 C++，但是它仍會避免動態記憶體配置及使用 STL 函數，因為 mBed 裝置有時具有讓移轉難以進行的特殊記憶體模型。在任何情況下，程式庫都可讓您使記憶體盡可能如預期般使用。

## 相依關係
{: #dependencies}

|相依關係 |說明|
|:---|:---|
|[Eclipse Paho MQTT 程式庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/teams/mqtt/code/MQTT/){: new_window}|提供 mBed 裝置的 MQTT 用戶端程式庫。如需相關資訊，請參閱[嵌入式 MQTT C/C++ 用戶端程式庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}|
|[EthernetInterface 程式庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/){: new_window}|透過乙太網路的 mBed IP 程式庫。|

## 如何使用程式庫
{: #library_use}

當您使用 mBed C++ IBMIoTF 用戶端程式庫時，請使用 [mBed 編譯器 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/compiler/){: new_window} 來建立您的應用程式。mBed 編譯器提供小型線上 C/C++ IDE，其配置適用於撰寫、編譯及下載要在 mBed 微型控制器上執行的程式。

**附註：**您不必安裝或設定任何項目，即可開始執行 mBed。

如需如何將 ARM mBed NXP LPC 1768 微型控制器連接至 {{site.data.keyword.iot_short_notm}} 的相關資訊，請參閱 [IBM Watson IoT Platform 的 mBed C++ 用戶端程式庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/){: new_window} 秘訣。

## 建構子
{: #constructor}

建構子會建置用戶端實例，並接受下列參數：

|參數 |說明 |
|:---|:---|
|`org` |您的組織 ID。這是必要值。如果您使用的是 Quickstart 流程，請指定 `quickstart`。|
|`type`   |您的裝置類型。這是必要欄位。|
|`id`   |您的裝置 ID。這是必要欄位。|
|`auth-method`   |鑑別方法，這是選用欄位，只有已登錄流程需要此欄位。目前唯一支援的值是 `token`。|
|`auth-token`   |將裝置安全地連接至 Watson IoT Platform 的鑑別記號。這是選用欄位，只有已登錄流程需要此欄位。|

這些參數會建立用來與 {{site.data.keyword.iot_short_notm}} 服務互動的定義。

下列程式碼範例概述 DeviceClient 實例如何與 {{site.data.keyword.iot_short_notm}} 的 Quickstart 服務互動：

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

如前一個程式碼範例所示，如果未指定裝置 ID，則 DeviceClient 會使用裝置的 MAC 位址，作為要連接至 {{site.data.keyword.iot_short_notm}} 的裝置 ID。裝置程式碼可以使用 `getDeviceId()` 方法，從 DeviceClient 實例中擷取裝置 ID。

下列程式碼區塊顯示如何建立 DeviceClient 實例，與 {{site.data.keyword.iot_short_notm}}「已登錄」組織互動。

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

## 連接至 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

裝置可在 DeviceClient 實例上呼叫 connect 函數來連接至 {{site.data.keyword.iot_short_notm}}。

```
  #include "DeviceClient.h"
  ....
  ....

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
在連線成功後，裝置可將事件發佈至 {{site.data.keyword.iot_short_notm}}，而且可以接聽指令。

另外，裝置可以使用 `isConnected()` 方法查詢連線的狀態，如下列範例所示：

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## 發佈事件
{: #publishing_events}

事件是裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 的機制。裝置會控制事件的內容，並指派名稱給它傳送的每個事件。

{{site.data.keyword.iot_short_notm}} 實例收到事件時，所收到事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。

可使用三種[服務品質 (QoS) 水準](../../reference/mqtt/index.html#qos-levels)的任一種發佈事件，這些水準由 MQTT 通訊協定定義。依預設，事件是以 QoS 0 來發佈。

### 使用預設服務品質發佈事件

下列範例顯示如何以 JSON 格式將下列資料點發佈至 {{site.data.keyword.iot_short_notm}}：

- LPC1768，例如 x、y 及 z 軸
- 搖桿位置
- 現行溫度讀數

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
如需完整的範例，請參閱 [ IBMIoTClientLibrarySample ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}。
### 提高事件的 QoS 水準

您可以為發佈的事件提高 [QoS 水準](../../reference/mqtt/index.html#qos-levels)。QoS 水準大於 `0` 的事件可能需要較長的發佈時間，因為包含額外的確認接收資訊。

**附註：**Quickstart 流程模式僅支援 QoS 0。

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

### 處理事件發佈期間失去連線的錯誤


當 `publishEvent()` 方法傳回 false 值時，您可以檢查連線的狀態，如果失去連線，則可以呼叫 `reConnect()`。

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
程式庫不會儲存未連接狀態期間發佈的事件，因此裝置需要重新呼叫 `publishEvent()` 方法，才能在重新建立連線之後傳送那些事件。

## 處理指令
{: #handling_commands}

當裝置用戶端連接時，它會自動訂閱此裝置的任何指令。若要處理特定指令，您必須登錄指令回呼方法。會以 Command 類別的實例傳回訊息，而這個實例具有下列內容：

|內容 |說明|
|:---|:---|
|`command` | 呼叫的指令名稱。|  
|`format`  |事件的格式。格式可以是任何字串（例如，JSON）。 |
|`payload`  |指令有效負載的資料。長度上限是 131072 個位元組。 |


下列程式碼定義範例指令回呼函數，其會處理來自應用程式的 LED 閃爍間隔指令，並在 DeviceClient 實例上設定函數控點，以在裝置收到閃爍指令，即執行回呼方法。

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
如需完整的範例，請參閱 [ IBMIoTClientLibrarySample ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}。
**附註：**必須定期呼叫 `client.yield()` 函數，才能接收指令。
`client.yield()` 函數可讓裝置接收來自 Watson IoT Platform 的指令，並保持連線作用中。如果未在 keepAlive 間隔所指定的時間範圍內呼叫 `client.yield()` 函數，則裝置將不會收到從平台送出的任何指令。指派給 `client.yield()` 函數的值指定在將控制權還給應用程式之前，可從 Socket 讀取資料的時間長度（毫秒）。

## 中斷用戶端連線
{: #disconnect_client}

若要中斷用戶端連線並釋出連線，請執行下列程式碼 Snippet：

```
	...
	client.disconnect();
	....
```
## 範例
{: #samples}

[IBMIoTClientLibrarySample ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/){: new_window} 是程式碼範例，顯示如何使用 {{site.data.keyword.iot_short_notm}} 用戶端程式庫，將 mbed LPC1768 或 FRDM-K64F 裝置連接至服務實例。
