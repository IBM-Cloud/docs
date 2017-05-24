---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 针对应用程序开发者的 Python
{: #python}


您可以使用 Python 来构建和开发应用程序，以在 {{site.data.keyword.iot_full}} 上与您的组织进行交互。{{site.data.keyword.iot_short_notm}} 的 Python 客户机提供了 API，通过剥离底层协议（例如，MQTT 和 HTTP）来帮助与 {{site.data.keyword.iot_short_notm}} 功能进行简单交互。

{:shortdesc}

使用提供的信息和示例通过 Python 开始开发应用程序。

## 下载 Python 客户机和资源
{: #python_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 Python 客户机和其他可用资源，请转至 GitHub 中的 [iot-python ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-messaging/iot-python){: new_window} 存储库，并完成安装指示信息。

## 构造方法
{: #constructor}

使用选项字典可创建用于与 {{site.data.keyword.iot_short_notm}} 模块进行交互的定义。构造方法用于构建客户机实例，并接受包含以下定义的选项字典：

|定义|描述 |
|:-----|:-----|
|`orgId`|组织标识。|
|`appId`|组织中应用程序的唯一标识。|
|`auth-method`|认证方法。支持的唯一方法是 `apikey`。|
|`auth-key`|可选的 API 密钥，将 auth-method 的值设置为 `apikey` 时必须指定。|
|`auth-token`|API 密钥令牌，将 auth-method 的值设置为 `apikey` 时，此参数也是必需的。|
|`clean-session`|true 或 false 值，仅当要以持久预订方式连接应用程序时是必需的。缺省情况下，`clean-session` 设置为 true。|


如果未提供选项字典，那么客户机将作为未注册的设备连接到 {{site.data.keyword.iot_short_notm}} Quickstart 服务。

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

### 使用配置文件


如果未使用选项字典，那么必须包含具有选项字典的配置文件，字典的编码格式如下：

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
应用程序配置文件必须为以下格式：

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## API 调用
{: #api_calls}

API 客户机中的每个方法对应于以下任一项：

- 如果成功，为有效 JSON 或布尔值响应
- 如果失败，为 IoTFCReSTException 异常

要获取有关 API 调用失败原因的更多信息，或要查看操作是否部分成功，应用程序可以解析异常响应的属性。IoTFCReSTException 异常响应包含以下属性：

|属性|描述|
|:---|:---|
|`httpcode`|HTTP 状态码。|
|`message`|异常消息，其中包含失败的原因。|
|`response`|包含部分响应的 JSON 元素。如果不存在任何响应，此值设置为空。|

## 预订设备事件
{: #subscribe_device_events}

事件是设备用于将数据发布到 {{site.data.keyword.iot_short_notm}} 实例的机制。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送设备，这使得一台设备无法冒充其他设备。

缺省情况下，应用程序会预订来自所有已连接设备的所有事件。使用 deviceType、deviceId、event 和 msgFormat 参数可控制预订的范围。单个客户机可支持多个预订。以下代码样本显示可以如何使用 deviceType、deviceId、event 和 msgFormat 参数来定义预订范围：


### 预订来自所有设备的所有事件


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### 预订来自特定类型的所有设备的所有事件


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### 预订来自所有设备的特定事件


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### 预订来自两个或更多不同设备的特定事件

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### 预订以 JSON 格式发布的所有事件

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## 处理来自设备的事件
{: #handling_events_devices}

要处理预订接收到的事件，需要注册事件回调方法。消息将作为 Event 类的实例返回：

|属性|数据类型|描述|
|:---|:---|
|`event.device`|字符串|在组织内所有类型的设备中作为该设备的唯一标识。|
|`event.deviceType`|字符串|标识设备类型。通常，deviceType 是对执行特定任务的设备的一种分组，例如“weatherballoon”。|
|`event.deviceId`|字符串|表示设备的标识。通常，对于给定设备类型，deviceId 是该设备的唯一标识，例如序列号或 MAC 地址。|
|`event.event`|字符串|通常用于对特定事件分组，例如“status”、“warning”和“data”。
|`event.format`|字符串|格式可以为任意字符串，例如 JSON。
|`event.data`|字典|消息有效内容的数据。最大长度为 131072 字节。
|`event.timestamp`|日期和时间|事件的日期和时间|

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


## 预订设备状态
{: #subscribe_device_status}


缺省情况下，预订设备状态时，会收到所有已连接设备的状态更新。使用类型和标识参数可控制预订范围。单个客户机可支持多个预订。

### 预订所有设备的状态更新


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### 预订特定类型的所有设备的状态更新


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### 预订两种不同设备的状态更新


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## 处理来自设备的状态更新
{: #handling_device_updates}

状态事件

要处理预订接收到的状态更新，需要注册事件回调方法。消息将作为 Status 类的实例返回。

有两种类型的状态事件：`Connect` 事件和 `Disconnect` 事件。所有状态事件都包含以下属性：

|属性|数据类型|
|:---|:---|
|`status.clientAddr`|字符串|
|`status.protocol`|字符串|
|`status.clientId`|字符串|
|`status.user`|字符串|
|`status.time`|日期和时间|
|`status.action`|字符串|
|`status.connectTime`|日期和时间|
|`status.port`|整数|


`status.action` 属性确定状态事件的类型是 `Connect` 还是 `Disconnect`。

`Disconnect` 状态事件包含以下额外的属性：

|属性|数据类型|
|:---|:---|
|`status.writeMsg`|整数|
|`status.readMsg`|整数|
|`status.reason`|字符串|
|`status.readBytes`|整数|
|`status.writeBytes`|整数|

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


## 发布来自设备的事件
{: #publishing_device_events}

应用程序可以将事件当作源自设备的事件进行发布。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## 将命令发布到设备
{: #publishing_commands_devices}


应用程序可以将命令发布到已连接设备。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", commandData)
```


## 组织详细信息
{: #org_details}

应用程序可以使用 `getOrganizationDetails()` 方法来检索有关组织配置的详细信息。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

有关请求和响应模型以及 HTTP 状态码的信息，请参阅 [{{site.data.keyword.iot_short_notm}} API ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} 的“组织配置”部分。


## 批量设备操作
{: #bulk_device_ops}

应用程序可以使用批量操作来同时获取、添加或除去多个设备。

有关查询参数的列表、请求和响应模型以及 HTTP 状态码的信息，请参阅 [{{site.data.keyword.iot_short_notm}} API ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} 的“批量操作”部分。


### 检索设备信息

批量设备信息可以使用 `getAllDevices()` 方法进行检索。此方法会检索有关组织中所有已注册设备的信息。每个请求最多可以包含 512 KB。

响应包含应用程序需要的参数。使用来自响应的字典结果可获取返回的设备数组。响应中的其他参数对于进行更多调用是必需的，例如，`_bookmark` 元素可用于逐页浏览结果。在不指定书签的情况下提交第一个请求，然后获取响应中返回的书签，并在下一页的请求上提供该书签。重复此过程直到结果集末尾，没有书签即指示到达了末尾。每个请求必须对其他参数使用相同的值，否则结果将为“未定义”。


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### 添加多台设备


使用 `addMultipleDevices()` 方法可向 {{site.data.keyword.iot_short_notm}} 组织添加一台或多台设备。请求不能大于 512 KB。响应包含为每台设备生成的认证令牌。请确保生成认证令牌的副本，因为如果认证令牌丢失，将无法取回这些令牌。


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

### 删除多台设备


使用 `deleteMultipleDevices()` 方法可从 {{site.data.keyword.iot_short_notm}} 组织中删除多台设备。请求不能大于 512 KB。

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


## 设备类型操作
{: #device_type_ops}

在组织中创建的设备类型可用于创建设备添加模板。通过使用 {{site.data.keyword.iot_short_notm}} API 功能，应用程序可以列出、创建、删除、查看或更新组织中的设备类型。

有关查询参数、请求和响应模型以及 HTTP 状态码的信息，请参阅 [{{site.data.keyword.iot_short_notm}} API ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} 文档的“设备类型”部分。


### 检索所有设备类型

使用 `getAllDeviceTypes()` 方法可检索位于 {{site.data.keyword.iot_short_notm}} 组织中的所有设备类型。
使用来自响应的字典结果可获取返回的设备数组。响应中的其他参数对于进行更多调用是必需的，例如，`_bookmark` 元素可用于逐页浏览结果。在不指定书签的情况下提交第一个请求，然后获取响应中返回的书签，并在下一页的请求上提供该书签。重复此过程直到结果集末尾，没有书签即指示到达了末尾。每个请求必须对其他参数使用相同的值，否则结果将为“未定义”。

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

### 添加设备类型

使用 `addDeviceType()` 方法可向 {{site.data.keyword.iot_short_notm}} 实例注册设备类型。在每个请求中，必须首先定义要应用于此类型的所有设备的设备信息和设备元数据元素。设备信息元素由多个变量组成，变量包括序列号、制造商、型号、类、描述、固件、硬件版本和描述性位置。元数据元素由定制变量和值组成，这些变量和值可以由用户进行定义。


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

### 删除设备类型


使用 `deleteDeviceType()` 方法可从 {{site.data.keyword.iot_short_notm}} 组织中删除设备类型。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### 检索特定设备类型的信息


使用 `getDeviceType()` 方法可检索特定设备类型的信息。要检索的设备类型的 `typeId` 必须指定为参数。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### 更新设备类型


使用 `updateDeviceType()` 方法可修改设备类型的属性。使用 `updateDeviceType()` 方法时，请先指定要更新的设备类型的 `typeId`，然后指定以下元素：

- `描述`
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


## 设备操作
{: #device_ops}

在 API 中可用的设备操作包括列出、添加、除去、查看、更新 {{site.data.keyword.iot_short_notm}} 组织中的设备以及查看设备位置和查看设备的设备管理信息。

有关查询参数、请求和响应模型以及 HTTP 状态码的信息，请参阅 [{{site.data.keyword.iot_short_notm}} API 文档![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} 的“设备”部分。


### 检索特定设备类型的设备

使用 `retrieveDevices()` 方法可在 {{site.data.keyword.iot_short_notm}} 实例的组织中检索特定设备类型的所有设备，如以下示例中所示：


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

使用来自响应的字典结果可获取返回的设备数组。响应中的其他参数对于进行更多调用是必需的，例如 *_bookmark* 元素可用于逐页浏览结果。在不指定书签的情况下提交第一个请求，然后获取响应中返回的书签，并在下一页的请求上提供该书签。重复此过程直到结果集末尾，没有书签即指示到达了末尾。每个请求必须对其他参数使用相同的值，否则结果将为“未定义”。

要传递 *_bookmark* 或其他任何条件，必须使用重载方法。重载方法采用字典形式的参数，如以下示例中所示：

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

先前的代码样本根据设备标识对响应排序，然后使用书签来逐页浏览结果。

### 添加设备


要向 {{site.data.keyword.iot_short_notm}} 组织添加设备，请使用 `registerDevice()` 方法。`registerDevice()` 方法可向 {{site.data.keyword.iot_short_notm}} 组织添加单个设备。添加设备时，可以指定以下参数：

|参数|要求|描述
|:---|:---|
|`deviceTypeId`|可选|为设备指定设备类型。如果设备类型定义的变量与 `deviceInfo` 变量定义的变量之间存在冲突，那么特定于设备的变量优先。|
|`deviceId`|必需||
|`authToken`|可选|如果未提供，将生成认证令牌并包含在响应中。|
|`deviceInfo`|可选|包含多个变量，其中包括 serialNumber、manufacturer、model、deviceClass、description、descriptiveLocation、firmware 和 hardware versions。|
|`metadata`|可选|定制字段值字符串对，如[用于添加设备类型的样本代码](#sample_device_type)中所示。|
|`location`|可选|包含 longitude、latitude、elevation、accuracy 和 measuredDateTime 变量。|

有关这些参数以及响应格式和代码的更多信息，请参阅 [API文档 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices){: new_window}。

使用 `registerDevice()` 方法时，请定义需要用于设备的必需 deviceID 参数和可选参数，然后使用所选参数来调用此方法。

### 用于添加设备类型的样本代码
{: #sample_device_type}

将以下代码插入到 Python(.py) 脚本文件中的构造方法代码之后。该样本演示了用于通过定义 deviceId、authToken、metadata、deviceInfo 和 location 参数来添加设备类型的方法。

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### 删除设备

使用 `deleteDevice()` 方法可从 {{site.data.keyword.iot_short_notm}} 上的某个组织中除去设备。使用 `deleteDevice()` 方法删除设备时，必须指定 deviceTypeId 和 deviceId 参数。

以下代码样本概述了此方法所需的格式：

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### 获取设备

使用 `getDevice()` 方法可在 {{site.data.keyword.iot_short_notm}} 上的组织中检索设备。使用 `getDevice()` 方法检索设备详细信息时，必须指定 deviceTypeId 和 deviceId 参数。

以下代码样本概述了此方法所需的格式。

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### 检索所有设备

使用 `getAllDevices()` 方法可在 {{site.data.keyword.iot_short_notm}} 上的组织中检索所有设备。

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### 更新设备

要修改设备的一个或多个属性，请使用 `updateDevice()` 方法。

可以更新 deviceInfo 或 metadata 参数中的任何属性。要更新设备属性，请在调用 `updateDevice()` 方法之前，先定义 deviceInfo 参数。status 参数必须包含 `alert`: True。alert 属性控制设备是否在 {{site.data.keyword.iot_short_notm}} 用户界面中显示错误代码，并且缺省情况下必须设置为 `enabled`: True，如以下代码示例中所示：

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### 用于更新 deviceInfo 属性的样本代码

以下代码样本识别特定设备，然后更新 deviceInfo 参数的多个属性。

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### 检索位置信息


使用 `getDeviceLocation()` 方法可检索设备的位置信息。检索位置数据所必需的参数是 deviceTypeId 和 deviceId。

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

该方法的响应中包含经度、纬度、海拔高度、准确性、measuredTimeStamp 和 updatedTimeStamp 属性。

### 更新位置信息


使用 `updateDeviceLocation()` 方法可修改设备的位置信息。与更新设备属性一样，deviceLocation 参数也必须通过要应用的更改进行定义。以下代码样本演示了更改特定设备的位置数据：

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

如果未提供日期，那么将使用当前日期和时间。


### 获取管理信息


使用 `getDeviceManagementInformation()` 方法可获取设备的设备管理信息。响应包含上次活动日期/时间、设备的休眠状态 (True/False)、对设备和固件操作的支持以及固件数据。有关综合的响应内容列表，请参阅相关的 API 文档。

以下代码样本将返回 deviceId 设置为“00aabbccde03”且 deviceTypeId 设置为“iotsample-arduino”的设备的设备管理信息。

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## 设备诊断操作
{: #device_diag_ops}

使用设备诊断操作可实现以下故障诊断和日志管理任务：
- 清除日志
- 检索设备的所有日志或特定日志
- 添加日志信息
- 删除日志
- 清除错误代码
- 检索设备错误代码
- 添加错误代码

有关查询和响应模型、响应代码以及查询参数的更多信息，请参阅 [{{site.data.keyword.iot_short_notm}} API 文档 ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}。

### 获取诊断日志


使用 `getAllDiagnosticLogs()` 方法可检索特定设备的所有诊断日志。`getAllDiagnosticLogs()` 方法需要 deviceTypeId 和 deviceId 参数。

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

此方法的响应模型包含日志标识、消息、严重性、数据和时间戳记属性。

### 清除设备的诊断日志


使用 `clearAllDiagnosticLogs()` 方法可删除特定设备的所有诊断日志。必需参数为 deviceTypeId 和 deviceId。删除日志文件时请谨慎，因为日志文件一旦删除后即无法恢复。

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### 添加诊断日志


使用 `addDiagnosticLog()` 方法可在设备的诊断日志中添加条目。添加新条目时，可以修剪日志。如果未提供日期，那么会将当前日期和时间添加到该条目。要使用此方法，您需要使用以下变量来定义“logs”参数：


|变量|要求|描述|
|:---|:---|:---|
|`message`|必需|包含要添加的诊断消息|
|`severity`|可选|对应于诊断日志的严重性，可以设置为 0、1 或 2，分别对应于参考、警告和错误类别|
|`data`|可选|包含诊断数据|
|`timestamp`|可选|包含 ISO8601 格式的日志条目日期和时间，但如果未指定，那么将使用当前日期和时间|


此方法中必需的其他参数为设备的 deviceTypeId 和 deviceId 值。

以下代码样本包含 `addDiagnosticLog()` 方法的示例：

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### 检索特定诊断日志


使用 `getDiagnosticLog()` 方法可基于日志标识来检索指定设备的特定诊断日志。此方法的必需参数为 deviceTypeId、deviceId 和 logId。

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### 删除诊断日志


使用 `deleteDiagnosticLog()` 方法可删除特定诊断日志。要指定诊断日志，必须提供 deviceTypeId、deviceId 和 logID 参数。

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### 检索设备错误代码


使用 `getAllDiagnosticErrorCodes()` 方法可检索与特定设备关联的所有诊断错误代码。

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### 清除诊断错误代码


使用 `clearAllErrorCodes()` 方法可清除与设备关联的错误代码的列表。该列表将替换为单个错误代码 0。

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### 添加单个诊断错误代码


使用 `addErrorCode()` 方法可向与设备关联的错误代码的列表添加错误代码。添加新条目时，可以修剪该列表。此方法中的必需参数为 deviceTypeId、deviceId 和 errorCode。errorCode 参数包含以下变量：

- errorCode：此变量为必需变量，应设置为整数。此变量设置创建的错误代码的编号。
- timestamp：此变量是可选的，包含 ISO8601 格式的日志条目日期和时间。如果未包含此变量，会自动使用当前日期和时间进行添加。

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## 连接问题确定
{: #connection_problem_determination}

使用 `getDeviceConnectionLogs()` 方法可列出设备的连接日志事件。连接日志事件可用于帮助诊断设备与 {{site.data.keyword.iot_short_notm}} 服务之间的连接问题。这些条目会记录成功连接、失败连接尝试次数、有意断开连接和服务器发出的断开连接事件。

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

响应包含日志条目的列表，其中包含日志消息和时间戳记。
