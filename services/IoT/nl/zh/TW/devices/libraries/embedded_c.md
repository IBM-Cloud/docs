---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 適用於裝置開發人員的嵌入式 C
{: #embedded_c}

您可以使用嵌入式 C 來建置及自訂裝置，在 {{site.data.keyword.iot_full}} 上與組織互動。請使用所提供的資訊及範例，利用嵌入式 C 開始開發您的裝置。
{:shortdesc}

## 下載嵌入式 C 用戶端及資源
{: #embeddedc_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的內嵌式 C 用戶端程式庫及範例，請移至 GitHub 中的 [iotf-embeddedc ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-messaging/iotf-embeddedc){: new_window} 儲存庫，並完成安裝指示。


## 相依關係
{: #dependencies}

|相依關係 |說明|
|:---|:---|
|[Eclipse Paho 內嵌式 C 程式庫 ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git){: new_window} |提供 MQTT C 用戶端程式庫。如需相關資訊，請參閱 [MQTT 用戶端套件 - 適用於嵌入式裝置的 C ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}。|


## 安裝
{: #installation}

若要安裝嵌入式 C 的 {{site.data.keyword.iot_short_notm}} 用戶端程式庫，請完成下列指示：

1. 若要安裝最新版的程式庫，請在指令行上輸入下列程式碼：
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. 將 Paho 程式庫 .tar 檔案複製到 *lib* 目錄。
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. 將程式庫檔案解壓縮
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
下載的用戶端具有下列檔案結構：

```
 |-lib - contains all the dependent files
 |-samples - contains the helloWorld and sampleDevice samples
   |-sampleDevice.c - sample device implementation
   |-helloworld.c - quickstart application
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c - Main client file
 |-iotfclient.h - Header file for the client
```

## 起始設定用戶端程式庫
{: #initialize_client_library}

在下載用戶端程式庫之後，必須將它起始設定並連接至 {{site.data.keyword.iot_short_notm}}。您可以傳遞參數或使用配置檔，來起始設定嵌入式 C 的 {{site.data.keyword.iot_short_notm}} 用戶端程式庫。

### 傳遞參數

`initialize` 函數會使用下列參數來連接至 {{site.data.keyword.iot_short_notm}} 服務：

|定義 |說明 |
|:---|:---|
|`client`|*iotfclient* 的指標。|
|`org`|您的組織 ID。|
|`type` |您的裝置類型。|
|`id` |裝置 ID。|
|`auth-method` |要使用的鑑別方法。目前唯一支援的值是 `token`。|
|`auth-token`|將裝置安全地連接至 Watson IoT Platform 的鑑別記號。|


```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	//quickstart
	rc = initialize(&client,"quickstart","iotsample","001122334455",NULL,NULL);
	//registered
	rc = initialize(&client,"org","type","id","auth-method","auth-token");
	....
```

### 使用配置檔

您也可以使用配置檔來起始設定嵌入式 C 用戶端程式庫。`initialize_configfile` 函數會採用配置檔路徑作為參數。

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

配置檔必須使用下列格式：

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## 連接至服務
{: #connecting_service}

在起始設定 {{site.data.keyword.iot_short_notm}} 嵌入式 C 用戶端程式庫之後，您可以呼叫 `connectiotf` 函數來連接至 {{site.data.keyword.iot_short_notm}}。

```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	char *configFilePath = "./device.cfg";

	rc = initialize_configfile(&client, configFilePath);

	if(rc != SUCCESS){
		printf("initialize failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}

	rc = connectiotf(&client);

	if(rc != SUCCESS){
		printf("Connection failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}
	....
```

## 處理指令
{: #handling_commands}

當裝置用戶端連接時，它會自動訂閱此裝置的任何指令。若要處理特定指令，您必須呼叫 `setCommandHandler` 函數來登錄指令回呼方法。回呼函數具有下列內容：

|內容 |說明|
|:---|:---|
|`commandName`  |呼叫的指令名稱。 |  
|`format`  |事件的格式。格式可以是任何字串（例如，JSON）。|
|`payload`  |指令有效負載的資料。長度上限是 131072 個位元組。 |


```
	#include "iotfclient.h"

	void myCallback (char* commandName, char* format, void* payload)
	{
	printf("The command received :: %s\n", commandName);
	printf("format : %s\n", format);
	printf("Payload is : %s\n", (char *)payload);
	}
	...
	...
	char *filePath = "./device.cfg";
	rc = connectiotfConfig(filePath);
	setCommandHandler(myCallback);

	yield(1000);
	....

```
**附註：**`yield()` 函數可讓裝置接收來自 Watson IoT Platform 的指令，並保持連線作用中。如果未在 keepAlive 間隔所指定的時間範圍內呼叫 `yield()` 函數，則裝置將不會收到從平台送出的任何指令。指派給 `yield()` 函數的值，會指定在將控制權還給應用程式之前，可從 Socket 讀取資料的時間長度（毫秒）。

## 發佈事件
{: #publishing_events}

事件可以搭配下列內容發佈：

|內容 |說明|
|:---|:---|
|eventType  |發佈的事件類型，例如，status 或 gps。 |  
|eventFormat  |格式可以是任何字串，例如，`json`。 |
|data  |有效負載的資料。長度上限是 131072 個位元組。 |
|QoS  |發佈事件的「服務品質」水準。支援的值為 `0`、`1`、`2`。|


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## 中斷用戶端連線
{: #disconnect_client}

若要中斷用戶端連線並釋出連線，請執行下列程式碼 Snippet：

```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", payload , QOS0);
	...
	rc = disconnect();
	....
```

## 範例
{: #samples}

[GitHub ![外部鏈結圖示](../../../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples){: new_window} 中提供裝置及應用程式碼範例。
