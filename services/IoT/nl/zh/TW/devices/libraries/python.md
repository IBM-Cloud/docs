---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 適用於裝置開發人員的 Python
{: #python}
前次更新：2016 年 7 月 29 日
{: .last-updated}

您可以在 {{site.data.keyword.iot_full}} 上使用 Python 來建置及開發與組織互動的裝置程式碼。適用於 {{site.data.keyword.iot_short_notm}} 的 Python 用戶端提供 API，透過抽出基礎通訊協定（例如 MQTT 及 HTTP）來協助與 {{site.data.keyword.iot_short_notm}} 特性的簡單互動。{:shortdesc}

使用提供的資訊及範例，利用 Python 開始開發您的裝置。

## 下載 Python 用戶端及資源
{: #python_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 Python 用戶端及其他可用的資源，請移至 GitHub 中的 [iot-python](https://github.com/ibm-watson-iot/iot-python) 儲存庫，並完成安裝指示。

## 建構子
{: #constructor}

options 字典會建立用來與 {{site.data.keyword.iot_short_notm}} 模組互動的定義。建構子會建置用戶端實例，並接受包含下列定義的 options 字典：

|定義|說明 |
|:---|:---|
|`orgId`|您的組織 ID。|
|`type`|您的裝置類型。一般而言，deviceType 是執行特定作業（例如，"weatherballoon"）的裝置分組。|
|`id`|您的裝置 ID。一般而言，針對給定的裝置類型，deviceId 是該裝置的唯一 ID（例如，序號或 MAC 位址）。|
|`auth-method`|要使用的鑑別方法。目前唯一支援的值是 `token`。|
|`auth-token`|將裝置安全地連接至 Watson IoT Platform 的鑑別記號。|

如果未提供 options 字典，用戶端會連接至 Watson IoT Platform 的「快速入門」服務，作為已取消登錄的裝置。

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### 使用配置檔

您也可以在配置檔中個別定義 options 字典，而非直接定義 options 字典，如下列程式碼範例所概述：

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

包含 options 字典的配置檔必須為下列格式：

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token

```

## 發佈事件
{: #publishing_events}

事件是裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 的機制。裝置會控制事件的內容，並指派所傳送之每一個事件的名稱。

{{site.data.keyword.iot_short_notm}} 實例接收到事件時，所收到事件的認證可識別傳送端裝置，這表示，裝置無法假冒另一個裝置。

可在三個服務品質 (QoS) 水準的任一個上發佈事件，這些水準由 MQTT 通訊協定予以定義。依預設，事件是在 QoS 水準 `0` 時發佈。

### 使用預設服務品質發佈事件

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### 提高事件的 QoS 水準

您可以為發佈的事件提高[服務品質 (QoS) 水準](../../reference/mqtt/index.html#qos-levels)。QoS 水準高於 `0` 的事件可能需要較長的發佈時間，因為包括額外的確認接收資訊。

**附註：**「快速入門」流程模式僅支援 QoS 水準 `0`。

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## 處理指令
{: #handling_commands}

當裝置用戶端連接時，它會自動訂閱針對此裝置指定的任何指令。若要處理特定指令，您必須登錄指令回呼方法。
會以 Command 類別的實例傳回訊息，而這個實例包含下列內容：

|內容|資料類型|說明|
|:---|:---|
|`command`|字串|識別指令。|
|`format`|字串|格式可以是任何字串（例如，JSON）。|
|`data`|字典|有效負載的資料。長度上限是 131072 個位元組。|
|`timestamp`|日期和時間|事件的日期和時間。|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## 自訂訊息格式支援
{: #custom_message_format}

訊息格式預設為 `json`，這表示，程式庫支援 JSON 格式的編碼及解碼 Python 字典物件。當訊息格式設為 `json-iotf` 時，訊息會根據 {{site.data.keyword.iot_short_notm}}「JSON 有效負載」規格進行編碼。若要為您自己的自訂訊息格式新增支援，請參閱 GitHub 中的[自訂訊息格式範例](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat)。

建立自訂編碼器模組時，您必須在裝置用戶端中登錄它，如下列範例所概述：

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
如果是以不明格式傳送事件，或如果裝置無法辨識格式，則用戶端程式庫會傳回 `MissingMessageDecoderException` 狀況。
