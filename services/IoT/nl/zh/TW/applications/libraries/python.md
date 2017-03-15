---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 適用於應用程式開發人員的 Python
{: #python}


您可以使用 Python 來建置及開發應用程式，在 {{site.data.keyword.iot_full}} 上與組織互動。適用於 {{site.data.keyword.iot_short_notm}} 的 Python 用戶端提供 API，透過抽離基礎通訊協定（例如 MQTT 及 HTTP），來協助與 {{site.data.keyword.iot_short_notm}} 特性的簡單互動。


{:shortdesc}

請使用所提供的資訊及範例，利用 Python 開始開發您的應用程式。

## 下載 Python 用戶端及資源
{: #python_client_download}

若要存取適用於 {{site.data.keyword.iot_short_notm}} 的 Python 用戶端及其他可用的資源，請移至 GitHub 中的 [iot-python ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://github.com/ibm-messaging/iot-python) 儲存庫，並完成安裝指示。

## 建構子
{: #constructor}

options 字典會建立用來與 {{site.data.keyword.iot_short_notm}} 模組互動的定義。建構子會建置用戶端實例，並接受包含下列定義的 options 字典：

|定義|說明 |
|:-----|:-----|
|`orgId`|您的組織 ID。|
|`appId`|組織中應用程式的唯一 ID。|
|`auth-method`|鑑別方法。唯一支援的方法是 `apikey`。|
|`auth-key`|選用性的 API 金鑰，當 auth-method 的值設為 `apikey` 時必須指定的項目。|
|`auth-token`|API 金鑰記號，當 auth-method 的值設為 `apikey` 時也為必要項目。|
|`clean-session`|true 或 false 值，只有在要於可延續訂閱模式中連接應用程式時才是必要項目。`clean-session` 預設為 true。|


如果未提供 options 字典，用戶端會連接至 {{site.data.keyword.iot_short_notm}} 的 Quickstart 服務，作為已取消登錄的裝置。

```python

import ibmiotf.application
try:
  options = {
    "org": organization,
    "id": appId,
    "auth-method": authMethod,
    "auth-key": authKey,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### 使用配置檔


如果您不是使用 options 字典，則必須包含一個配置檔，內含下列程式碼格式的 options 字典：

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
應用程式配置檔必須為下列格式：

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## API 呼叫
{: #api_calls}

API 用戶端中的每一種方法都會回應：

- 有效的 JSON 或布林回應（成功時）
- IoTFCReSTException 異常狀況（失敗時）

若要取得 API 呼叫失敗原因的相關資訊，或查看動作是否局部成功，應用程式可以剖析異常回應的內容。IoTFCReSTException 異常回應包含下列內容：

|內容|說明|
|:---|:---|
|`httpcode`|HTTP 狀態碼。|
|`message`|包含失敗原因的異常狀況訊息。|
|`response`|包含局部回應的 JSON 元素。如果不存在，此值會設為空值。|

## 訂閱裝置事件
{: #subscribe_device_events}

事件是裝置用來將資料發佈至 {{site.data.keyword.iot_short_notm}} 實例的機制。裝置會控制事件的內容，並指派名稱給它傳送的每個事件。

{{site.data.keyword.iot_short_notm}} 實例收到事件時，所收到事件的認證可識別傳送端裝置，讓裝置無法假冒另一個裝置。

應用程式預設會訂閱所有已連接裝置的所有事件。請使用 deviceType、deviceId、event 及 msgFormat 參數，以控制訂閱的範圍。單一用戶端可支援多個訂閱。下列程式碼範例顯示如何使用 deviceType、deviceId、event 及 msgFormat 參數來定義訂閱的範圍：


### 訂閱所有裝置的所有事件


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### 訂閱特定類型之所有裝置的所有事件


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### 訂閱所有裝置的特定事件


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### 訂閱兩個以上不同裝置的特定事件

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### 訂閱以 JSON 格式發佈的所有事件

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## 處理裝置的事件
{: #handling_events_devices}

若要處理訂閱所收到的事件，您需要登錄事件回呼方法。會以 Event 類別的實例傳回訊息：

|內容|資料類型|說明|
|:---|:---|
|`event.device`|字串|在組織所有類型裝置中唯一地識別出該裝置。|
|`event.deviceType`|字串|識別裝置類型。一般而言，deviceType 是執行特定作業的裝置分組，例如，"weatherballoon"。|
|`event.deviceId`|字串|代表裝置的 ID。一般而言，針對給定的裝置類型，deviceId 是該裝置的唯一 ID（例如，序號或 MAC 位址）。|
|`event.event`|字串|一般用來將特定事件分組（例如，"status"、"warning" 及 "data"）。
|`event.format`|字串|格式可以是任何字串（例如，JSON）。
|`event.data`|字典|訊息有效負載的資料。長度上限是 131072 個位元組。
|`event.timestamp`|日期和時間|事件的日期和時間|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  def myEventCallback(event):
      str = "%s event '%s' received from device [%s]: %s"
      print(str % (event.format, event.event, event.device, json.dumps(event.data)))

...
client.connect()
client.deviceEventCallback = myEventCallback
client.subscribeToDeviceEvents()
```


## 訂閱裝置狀態
{: #subscribe_device_status}


依預設，當您訂閱裝置狀態時，會收到所有已連接裝置的狀態更新。請使用 type 及 ID 參數，以控制訂閱的範圍。單一用戶端可支援多個訂閱。

### 訂閱所有裝置的狀態更新


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### 訂閱特定類型之所有裝置的狀態更新


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### 訂閱兩個不同裝置的狀態更新


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## 處理裝置的狀態更新
{: #handling_device_updates}

狀態事件

若要處理訂閱所收到的狀態更新，您需要登錄事件回呼方法。會以 Status 類別的實例傳回訊息。

有兩種類型的狀態事件：`Connect` 事件及 `Disconnect` 事件。所有狀態事件都包含下列內容：

|內容|資料類型|
|:---|:---|
|`status.clientAddr`|字串|
|`status.protocol`|字串|
|`status.clientId`|字串|
|`status.user`|字串|
|`status.time`|日期和時間|
|`status.action`|字串|
|`status.connectTime`|日期和時間|
|`status.port`|整數|


`status.action` 內容可決定狀態事件的類型是 `Connect` 還是 `Disconnect`。

`Disconnect` 狀態事件包含下列額外內容：

|內容|資料類型|
|:---|:---|
|`status.writeMsg`|整數|
|`status.readMsg`|整數|
|`status.reason`|字串|
|`status.readBytes`|整數|
|`status.writeBytes`|整數|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

def myStatusCallback(status):

  if status.action == "Disconnect":
    str = "%s - device %s - %s (%s)"
    print(str % (status.time.isoformat(), status.device, status.action, status.reason))
    else:
      print("%s - %s - %s" % (status.time.isoformat(), status.device, status.action))
  ...
client.connect()
client.deviceStatusCallback = myStatusCallback
client.subscribeToDeviceStstus()
```


## 發佈裝置的事件
{: #publishing_device_events}

應用程式可以發佈事件，就彷彿事件是源自裝置一樣。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## 將指令發佈至裝置
{: #publishing_commands_devices}


應用程式可對連接的裝置發佈指令。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", commandData)
```


## 組織詳細資料
{: #org_details}

應用程式可以使用 `getOrganizationDetails()` 方法來擷取組織配置的詳細資料。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

如需要求和回應模型以及 HTTP 狀態碼的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} API ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) 的 Organization Configuration 小節。


## 大量裝置作業
{: #bulk_device_ops}

您的應用程式可以使用大量作業，以同時取得、新增或移除多個裝置。

如需查詢參數清單、要求和回應模型以及 HTTP 狀態碼的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} API ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/) 的 Bulk Operations 小節。


### 擷取裝置資訊

使用 `getAllDevices()` 方法，即可擷取大量裝置資訊。此方法會擷取組織中所有已登錄裝置的資訊。每一個要求最多可以包含 512 KB。

回應包含應用程式所需的參數。使用回應中的字典結果，以取得所傳回裝置的陣列。回應中需要有其他參數，才能進行更多呼叫（例如，`_bookmark` 元素可以用來翻看結果）。在未指定書籤的情況下提交第一個要求，然後採用回應中傳回的書籤，並在下一頁的要求上提供它。請重複，直到結果集尾端（以沒有書籤來表示）。每一個要求都必須使用其他參數的相同值，否則結果將是未定義。


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### 新增多個裝置


使用 `addMultipleDevices()` 方法，將一個以上的裝置新增至 {{site.data.keyword.iot_short_notm}} 組織。要求不可以超過 512 KB。回應包含針對每一個裝置所產生的鑑別記號。請確定您已複製鑑別記號，因為如果遺失鑑別記號，便無法擷取它們。


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
  deviceList = client.api.addMultipleDevices(listOfDevicesToAdd)
except IoTFCReSTException as e:
  print("ERROR [" + e.httpcode + "] " + e.message)
```

### 刪除多個裝置


使用 `deleteMultipleDevices()` 方法，以刪除 {{site.data.keyword.iot_short_notm}} 組織中的多個裝置。要求不可以超過 512 KB。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToDelete = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
      deviceList = client.api.deleteMultipleDevices(listOfDevicesToDelete)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## 裝置類型作業
{: #device_type_ops}

您在組織中建立的裝置類型可以用來建立用於新增裝置的範本。使用 {{site.data.keyword.iot_short_notm}} API 特性，您的應用程式可以列出、建立、刪除、檢視或更新組織中的裝置類型。

如需查詢參數、要求和回應模型以及 HTTP 狀態碼的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} API ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) 文件的 Device Types 小節。


### 擷取所有裝置類型

使用 `getAllDeviceTypes()` 方法，以擷取 {{site.data.keyword.iot_short_notm}} 組織中的所有裝置類型。
使用回應中的字典結果，以取得所傳回裝置的陣列。回應中需要有其他參數，才能進行更多呼叫（例如，`_bookmark` 元素可以用來翻看結果）。在未指定書籤的情況下提交第一個要求，然後採用回應中傳回的書籤，並在下一頁的要求上提供它。請重複此處理程序，直到結果集尾端（以沒有書籤來表示）。每一個要求都必須使用其他參數的相同值，否則結果將是未定義。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

 listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
   options = {'_limit' : 2}
   deviceTypeList = client.api.getAllDeviceTypes(options)
except IoTFCReSTException as e:
   print("ERROR [" + e.httpcode + "] " + e.message)

```

### 新增裝置類型

使用 `addDeviceType()` 方法，以向 {{site.data.keyword.iot_short_notm}} 實例登錄裝置類型。在每一個要求中，您必須先定義要套用至所有這類型裝置的裝置資訊及裝置 meta 資料元素。裝置資訊元素包含數個變數，包括序號、製造商、機型、類別、說明、韌體、硬體版本及敘述性位置。meta 資料元素包含使用者可以定義的自訂變數及值。


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2"
  }

try:
      deviceType = client.api.addDeviceType(deviceType = "myDeviceType", description = "My first device type", deviceInfo = info, metadata = meta)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### 刪除裝置類型


使用 `deleteDeviceType()` 方法，以刪除 {{site.data.keyword.iot_short_notm}} 組織中的裝置類型。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### 擷取特定裝置類型的資訊


使用 `getDeviceType()` 方法，以擷取特定裝置類型的資訊。您要擷取之裝置類型的 `typeId` 必須指定為參數。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### 更新裝置類型


使用 `updateDeviceType()` 方法，以修改裝置類型的內容。當您使用 `updateDeviceType()` 方法時，請先指定要更新之裝置類型的 `typeId`，然後指定下列元素：

- `description`
- `deviceInfo`
- `metadata`

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2",
      "customField3": "customValue3"
  }

try:
      updatedDeviceTypeInfo = client.api.updateDeviceType("myDeviceType", "New description", deviceInfo, metadata)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## 裝置作業
{: #device_ops}

API 中可用的裝置作業，包括針對 {{site.data.keyword.iot_short_notm}} 組織中裝置的裝置進行列出、新增、移除、檢視、更新、檢視位置，以及檢視管理資訊。

如需查詢參數、要求和回應模型以及 HTTP 狀態碼的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} API ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) 的 Devices 小節。


### 擷取特定裝置類型的裝置

使用 `retrieveDevices()` 方法，以擷取 {{site.data.keyword.iot_short_notm}} 實例中組織內特定裝置類型的所有裝置，如下列範例所示：


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

使用回應中的字典結果，以取得所傳回裝置的陣列。回應中需要有其他參數，才能進行更多呼叫（例如，*_bookmark* 元素可以用來翻看結果）。在未指定書籤的情況下提交第一個要求，然後採用回應中傳回的書籤，並在下一頁的要求上提供它。請重複，直到結果集尾端（以沒有書籤來表示）。每一個要求都必須使用其他參數的相同值，否則結果將是未定義。

若要傳遞 *_bookmark* 或任何其他條件，必須使用超載方法。超載方法會採用字典形式的參數，如下列範例所示：

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

前一個程式碼範例會根據裝置 ID 來排序回應，然後使用書籤來翻頁結果。

### 新增裝置


若要將裝置新增至 {{site.data.keyword.iot_short_notm}} 組織，請使用 `registerDevice()` 方法。`registerDevice()` 方法會將單一裝置新增至 {{site.data.keyword.iot_short_notm}} 組織。當您新增裝置時，可以指定下列參數：

|參數|需求|說明
|:---|:---|
|`deviceTypeId`|選用|將裝置類型指派給裝置。如果裝置類型所定義的變數與 `deviceInfo` 變數所定義的變數之間發生衝突，則會優先使用裝置特有的變數。|
|`deviceId`|必要||
|`authToken`|選用|如果未提供，鑑別記號會產生並包含在回應中。|
|`deviceInfo`|選用|包含含有 serialNumber、manufacturer、model、deviceClass、description、descriptiveLocation、firmware 及硬體版本的數個變數。|
|`metadata`|選用|自訂欄位值字串配對，如[新增裝置類型的範例程式碼](#sample_device_type)中所概述。|
|`location`|選用|包含 longitude、latitude、elevation、accuracy 及 measuredDateTime 變數。|

如需這些參數以及回應格式和程式碼的相關資訊，請參閱 [API 文件 ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices)。

當您使用 `registerDevice()` 方法時，請定義裝置所需的必要 deviceID 參數及選用性參數，然後使用所選取的參數來呼叫方法。

### 新增裝置類型的範例程式碼
{: #sample_device_type}

在 Python(.py) Script 檔的建構子程式碼之後，插入下列程式碼。此範例示範透過定義 deviceId、authToken、metadata、deviceInfo 及 location 參數來新增裝置類型的方法。

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### 刪除裝置

使用 `deleteDevice()` 方法，以移除 {{site.data.keyword.iot_short_notm}} 上組織中的裝置。當您使用 `deleteDevice()` 方法來刪除裝置時，必須指定 deviceTypeId 及 deviceId 參數。

下列程式碼範例概述此方法所需的格式：

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### 取得裝置

使用 `getDevice()` 方法，以擷取 {{site.data.keyword.iot_short_notm}} 上組織中的裝置。當您使用 `getDevice()` 方法來擷取裝置詳細資料時，必須指定 deviceTypeId 及 deviceId 參數

下列程式碼範例概述此方法所需的格式。

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### 擷取所有裝置

使用 `getAllDevices()` 方法，以擷取 {{site.data.keyword.iot_short_notm}} 上組織中的所有裝置。

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### 更新裝置

若要修改裝置的一個以上內容，請使用 `updateDevice()` 方法。

您可以更新 deviceInfo 或 metadata 參數中的任何內容。若要更新裝置內容，請先定義 deviceInfo 參數，再呼叫 `updateDevice()` 方法。status 參數必須包含 `alert`: True。alert 內容可控制裝置是否在 {{site.data.keyword.iot_short_notm}} 使用者介面中顯示錯誤碼，而且預設必須設為 `enabled`: True，如下列程式碼範例所概述：

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### 更新 deviceInfo 內容的範例程式碼

下列程式碼範例可識別特定裝置，然後更新 deviceInfo 參數的數個內容。

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### 擷取位置資訊


使用 `getDeviceLocation()` 方法，以擷取裝置的位置資訊。擷取位置資料所需的參數是 deviceTypeId 及 deviceId。

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

此方法的回應包含經度、緯度、海拔高度、精確度、measuredTimeStamp 和 updatedTimeStamp 等內容。

### 更新位置資訊


使用 `updateDeviceLocation()` 方法，以修改裝置的位置資訊。與更新裝置內容相同，必須使用您想要套用的變更來定義 deviceLocation 參數。下列程式碼範例示範如何變更特定裝置的位置資料：

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

如果未提供日期，則會使用現行日期和時間。


### 取得管理資訊


使用 `getDeviceManagementInformation()` 方法，以取得裝置的裝置管理資訊。回應包含前次活動日期時間、裝置的休眠狀態 (True/False)、裝置和韌體動作支援，以及韌體資料。如需完整的回應內容清單，請參閱相關 API 文件。

下列程式碼範例傳回 deviceId 設為 "00aabbccde03" 且 deviceTypeId 設為 "iotsample-arduino" 之裝置的裝置管理資訊：

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## 裝置診斷作業
{: #device_diag_ops}

使用裝置診斷作業來實作下列疑難排解及日誌管理作業：
- 清除日誌
- 擷取裝置的所有或特定日誌
- 新增日誌資訊
- 刪除日誌
- 清除錯誤碼
- 擷取裝置錯誤碼
- 新增錯誤碼

如需查詢和回應模型、回應碼以及查詢參數的相關資訊，請參閱 [API 文件 ![外部鏈結圖示](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) {{site.data.keyword.iot_short_notm}} API 文件。

### 取得診斷日誌


使用 `getAllDiagnosticLogs()` 方法，以擷取特定裝置的所有診斷日誌。`getAllDiagnosticLogs()` 方法需要 deviceTypeId 及 deviceId 參數。

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

此方法的回應模型包含日誌 ID、訊息、嚴重性、資料及時間戳記內容。

### 清除裝置的診斷日誌


使用 `clearAllDiagnosticLogs()` 方法，以刪除特定裝置的所有診斷日誌。必要的參數是 deviceTypeId 和 deviceId。刪除日誌檔時請小心，因為刪除之後即無法回復。

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### 新增診斷日誌


使用 `addDiagnosticLog()` 方法，以在裝置的診斷日誌中新增項目。新增項目時，即可刪改日誌。如果未提供日期，則會將現行日期和時間新增至項目。若要使用此方法，您需要定義具有下列變數的 'logs' 參數：


|變數|需求|說明|
|:---|:---|:---|
|`message`|必要|包含您想要新增的診斷訊息|
|`severity`|選用|對應至診斷日誌的嚴重性，可以設為 0、1 或 2（分別對應於參考資訊、警告及錯誤種類） |
|`data`|選用|包含診斷資料|
|`timestamp`|選用|包含 ISO8601 格式之日誌項目的日期和時間，但是，如果未指定，則會使用現行日期和時間|


此方法中所需的其他參數是裝置的 deviceTypeId 及 deviceId 值。

下列程式碼範例包含 `addDiagnosticLog()` 方法的範例：

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### 擷取特定診斷日誌


使用 `getDiagnosticLog()` 方法，以根據日誌 ID 來擷取所指定裝置的特定診斷日誌。此方法的必要參數是 deviceTypeId、deviceId 及 logId。

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### 刪除診斷日誌


使用 `deleteDiagnosticLog()` 方法，以刪除特定診斷日誌。若要指定診斷日誌，必須提供 deviceTypeId、deviceId 及 logID 參數。

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### 擷取裝置錯誤碼


使用 `getAllDiagnosticErrorCodes()` 方法，以擷取與特定裝置相關聯的所有診斷錯誤碼。

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### 清除診斷錯誤碼


使用 `clearAllErrorCodes()` 方法，以清除與裝置相關聯的錯誤碼清單。此清單會取代為單一錯誤碼零。

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### 新增單一診斷錯誤碼


使用 `addErrorCode()` 方法，以將錯誤碼新增至與裝置相關聯的錯誤碼清單。新增項目時，即可刪改清單。此方法中所需的參數是 deviceTypeId、deviceId 及 errorCode。errorCode 參數包含下列變數：

- errorCode：這是必要的變數，應設為整數。此變數會設定所建立的錯誤碼數目。
- timestamp：這是選用性的變數，而且包含 ISO8601 格式之日誌項目的日期和時間。如果未包含此變數，將會以現行日期和時間自動加以新增。

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## 連線問題判斷
{: #connection_problem_determination}

使用 `getDeviceConnectionLogs()` 方法，以列出裝置的連線日誌事件。連線日誌事件可以用來協助診斷裝置與 {{site.data.keyword.iot_short_notm}} 服務之間的連線問題。這些項目會記錄成功連線、不成功的連線嘗試、故意斷線以及伺服器起始的斷線事件。

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

回應包含內含日誌訊息及時間戳記的日誌項目清單。
