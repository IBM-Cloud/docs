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


# 设备管理协议
{: #index}

## 简介
{: #introduction}

{{site.data.keyword.iot_full}} 可识别两类设备：**受管设备**和**非受管设备**。

**受管设备**定义为包含设备管理代理程序的设备。设备管理代理程序是一组逻辑，允许设备通过使用设备管理协议与 {{site.data.keyword.iot_short_notm}} 设备管理服务交互。受管设备可执行设备管理操作，包括位置更新、固件下载和更新、重新引导和出厂重置。

设备管理协议定义了一组受支持的操作。设备管理代理程序可以支持其中一部分操作，但必须支持**管理**和**取消管理**操作。支持固件操作的设备还必须支持观察。

设备管理协议基于 MQTT 消息传递协议进行构建。有关设备管理协议如何与 MQTT 进行交互的更多信息，请参阅[设备的 MQTT 连接](../mqtt.html)。


### 设备管理生命周期

1. 设备及其关联的设备类型使用仪表板或 REST API 在 {{site.data.keyword.iot_short_notm}} 中进行创建。
2. 设备连接到 {{site.data.keyword.iot_short_notm}}，并使用**受管设备**操作变成受管设备。
3. 可以使用设备操作来查看和处理设备的元数据。这些操作（例如，固件更新和设备重新启动操作）在“设备模型”文档中进行了概述。有关设备模型的更多信息，请参阅[设备模型](https://console.ng.bluemix.net/docs/services/IoT/reference/device_model.html)。
4. 设备可以使用设备管理协议传达有关其位置、诊断信息和错误代码的更新。
5. 为了处理大量设备群中失效的设备，**受管设备**操作请求会包含可选的 lifetime 参数。lifetime 参数是秒数，设备必须在此期间发起另一个**受管设备**请求，才能避免被分类为休眠而变成非受管设备。
6. 设备退役后，可以使用仪表板或 REST API 将其从 {{site.data.keyword.iot_short_notm}} 中除去。

请参阅 [ConnectRaspberry Pi as Managed Device to IBM Watson IoT Platform ![外部链接图标](../../../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/){: new_window}。

### 返回码摘要


下表显示了在设备管理生命周期内各个阶段生成的返回码。

|返回码 |消息 |
|:---|:---|
|200   |操作成功|
|202   |已接受（用于启动命令）|
|204   |已更改（用于属性更新）|
|400   |请求错误（例如，如果对于此命令，设备不处于相应的状态）|
|404   |找不到属性（如果操作发布到无效主题，也会使用此代码）|
|409   |资源由于冲突而无法更新（例如，两个请求同时在更新该资源，所以更新可以在稍后重试）|
|500   |意外的设备错误|
|501   |操作未实现|


## “管理设备”请求
{: #manage_device_request}

设备使用“管理设备”请求来变成受管设备。“管理设备”请求必须是设备在连接到 {{site.data.keyword.iot_short_notm}} 后发送的第一个设备管理请求。每当设备管理代理程序启动或重新启动后，通常都会发送此类型的请求。

**重要信息：**任何受管设备都必须支持此操作。


### “管理设备”请求的主题

设备将“管理设备”请求发布到以下主题：

```
iotdevice-1/mgmt/manage
```

服务器在以下主题上响应“管理设备”请求：

```
iotdm-1/response
```




### “管理设备”请求的消息格式


在“管理设备”请求中，`d` 字段及其所有子字段都是可选的。如果发送了 `metadata` 和 `deviceInfo` 字段，那么这两个字段的值将替换发送设备的相应属性。

可选的 `lifetime` 字段指定时间长度（以秒为单位），设备必须在此期间发送另一个“管理设备”请求，才能避免被分类为休眠而变成非受管设备。如果省略 `lifetime` 字段或将其设置为 `0`，那么受管设备不会变为休眠。`lifetime` 字段支持的最小值设置为 `3600` 秒，即 1 小时。

可选的 `supports.deviceActions` 和 `supports.firmwareActions` 字段指示设备管理代理程序的能力。如果设置了 `supports.deviceActions`，那么代理程序同时支持重新启动和恢复出厂设置操作。对于不区分重新启动和恢复出厂设置的设备，对这两个操作使用相同行为是可接受的。如果设置了 `supports.firmwareActions`，那么代理程序同时支持固件下载和固件更新操作。

以下样本显示了请求格式：

```
来自设备的出局消息：

Topic: iotdevice-1/mgmt/manage
{
    "d": {
        "metadata":{},
        "lifetime": number,
        "supports": {
            "deviceActions": boolean,
            "firmwareActions": boolean
        },
        "deviceInfo": {
            "serialNumber": "string",
            "manufacturer": "string",
            "model": "string",
            "deviceClass": "string",
            "description" :"string",
            "fwVersion": "string",
            "hwVersion": "string",
            "descriptiveLocation": "string"
        }
    },
    "reqId": "string"
}
```

以下样本显示了响应格式：

```
来自服务器的入局消息：

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### “管理设备”请求的响应代码

|响应代码 |消息 |
|:---|:---|
|200   |操作成功。|
|400   |输入消息与预期格式不匹配，或者其中一个值不在有效范围内。|
|404   |主题名称不正确，或者设备不在数据库中。|
|409   |设备数据库更新期间发生冲突。要解决此冲突，请根据需要简化操作。|


## “取消管理设备”请求
{: #manage-unmanage}


设备不再需要进行管理时，可以使用“取消管理设备”请求。设备变为非受管时，{{site.data.keyword.iot_short_notm}} 不会再向该设备发送新的设备管理请求。非受管设备会继续发布错误代码、日志消息和位置消息。**重要信息：**任何受管设备都必须支持此操作。

### “取消管理设备”请求的主题


设备将“取消管理设备”请求发布到以下主题：

```
iotdevice-1/mgmt/unmanage
```

服务器在以下主题上响应“取消管理设备”请求：

```
iotdm-1/response
```

### “取消管理设备”请求的消息格式

请求格式：

```
来自设备的出局消息：

Topic: iotdevice-1/mgmt/unmanage
{
    "reqId": "string"
}
```

响应格式：

```
来自服务器的入局消息：

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### “取消管理设备”请求的响应代码

|响应代码 |消息 |
|:---|:---|
|200   |操作成功。|
|400   |输入消息与预期格式不匹配，或者其中一个值不在有效范围内。|
|404   |主题名称不正确，或者设备不在数据库中。|
|409   |设备数据库更新期间发生冲突。要解决此冲突，请根据需要简化操作。|


## “更新位置”请求
{: #update-location}

设备使用“更新位置”请求来管理设备的位置数据。设备的位置元数据可以通过以下方式在 {{site.data.keyword.iot_short_notm}} 中进行更新：

#### 自动设备位置更新
- 设备将向 {{site.data.keyword.iot_short_notm}} 通知有关位置更新的信息。设备从 GPS 接收器检索其位置，然后向 {{site.data.keyword.iot_short_notm}} 实例发送设备管理消息以更新其位置。时间戳记会捕获从 GPS 接收器检索到位置的时间。即便发送位置更新消息有所延迟，该时间戳记也仍有效。如果在设备管理消息中省略时间戳记，那么会使用接收消息的日期和时间来更新位置元数据。

#### 使用 REST API 手动更新设备位置
- 注册设备时，可以使用 {{site.data.keyword.iot_short_notm}} REST API 手动设置静态设备的位置元数据。以后也可以修改位置。时间戳记设置是可选的，但省略时，会在设备的位置元数据中设置当前日期和时间。

### 设备触发的位置更新

可以确定其位置的设备可以选择向 {{site.data.keyword.iot_short_notm}} 设备管理服务器通知有关位置更改的信息。

### 设备触发的“更新位置”请求的主题：


设备将“更新位置”请求发布到以下主题：

```
iotdevice-1/device/update/location
```

服务器在以下主题上响应“更新位置”请求：

```
iotdm-1/response
```

### 用户或应用程序触发的位置更新


用户或应用程序更新活动受管设备的位置时，该设备会检索更新消息。




### 用户或应用程序触发的“更新位置”请求的主题


服务器将“更新位置”请求发布到以下主题：

```
iotdm-1/device/update
```

### “更新位置”请求的消息格式


`measuredDateTime` 字段是度量位置的日期。`updatedDateTime` 字段是更新设备信息的日期。出于效率原因，{{site.data.keyword.iot_short_notm}} 有时会批量更新位置信息，所以更新会略有延迟。必须使用 1984 年世界大地坐标系 (WGS84) 以十进制度数指定纬度和经度。

每当更新位置时，为纬度、经度、海拔和不确定性提供的值都会视为单次多值更新。纬度和经度是必需项，每次更新时都必须提供这两项。海拔高度和不确定性是可选项，可以将其省略。

如果某次更新时提供了某个可选值，而某次后续更新时省略了该可选值，那么该后续更新将删除先前的值。每次更新都视为完整的多值集。

### 设备触发的位置更新


请求格式：

```
来自设备的出局消息：

Topic: iotdevice-1/device/update/location
{
    "d": {
        "longitude": number,
        "latitude": number,

        "elevation": number,
        "measuredDateTime": "string in ISO8601 format",
        "updatedDateTime": "string in ISO8601 format",
        "accuracy": number
    },
    "reqId": "string"
}
```

响应格式：

```
来自服务器的入局消息：

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### “更新位置”请求的响应代码

|响应代码 |消息 |
|:---|:---|
|200   |操作成功。|
|400   |输入消息与预期格式不匹配，或者其中一个值不在有效范围内。|
|404   |主题名称不正确，或者设备不在数据库中。|
|409   |设备数据库更新期间发生冲突。要解决此冲突，请根据需要简化操作。|


### 用户或应用程序触发的位置更新


以下样本概述了有效内容格式：

```
来自服务器的入局消息：

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": {
                    "latitude": number,
                    "longitude": number,
                    "elevation": number,
                    "accuracy": number,
                    "measuredDateTime": "string in ISO8601 format"
                }
            }
        ]
    }
}
```

**注：**未使用 `reqID` 参数，因为设备无需响应。

## “更新设备属性”请求
{: #update-attributes}

通过使用 REST API，{{site.data.keyword.iot_short_notm}} 可以向设备发送请求，以更新以下一个或多个设备属性的值：


|属性 | 更多信息|
|:---|:---|
|location  | 请参阅[更新位置](index.html#update-location)|
|metadata  | 可选|
|deviceInfo | 可选|
|mgmt.firmware | 请参阅[固件更新过程](requests.html#firmware-actions-update)|

### “更新设备属性”请求的主题


服务器将设备更新请求发布到以下主题：

```
iotdm-1/device/update
```


### “更新设备属性”请求的消息格式


以下样本概述了请求的有效内容格式：

```
来自服务器的入局消息：

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": ""
            }
        ]
    }
}
```


## “添加错误代码”请求
{: #diag-add-error-code}

设备可以选择使用“添加错误代码”请求类型，向 {{site.data.keyword.iot_short_notm}} 设备管理服务器通知有关其错误状态更改的信息。

### “添加错误代码”请求的主题


设备将“添加错误代码”请求发布到以下主题：

```
iotdevice-1/add/diag/errorCodes
```

### “添加错误代码”请求的消息格式


与 `errorCode` 关联的值是当前设备错误代码，此值必须添加到 {{site.data.keyword.iot_short_notm}}。

请求格式：

```
来自设备的出局消息：

Topic: iotdevice-1/add/diag/errorCodes
{
    "d": {
        "errorCode": number
    },
    "reqId": "string"
}
```

响应格式：

```
来自服务器的入局消息：

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### “添加错误代码”请求的响应代码

|响应代码 |消息 |
|:---|:---|
|200   |操作成功。|
|400   |输入消息与预期格式不匹配，或者其中一个值不在有效范围内。|
|404   |主题名称不正确，或者设备不在数据库中。|
|409   |设备数据库更新期间发生冲突。要解决此冲突，请根据需要简化操作。|


## “清除错误代码”请求
{: #diag-clear-error-codes}

设备可以使用“清除错误代码”请求类型，请求 {{site.data.keyword.iot_short_notm}} 清除设备的所有错误代码。

### “清除错误代码”请求的主题


设备将此请求发布到以下主题：

```
iotdevice-1/clear/diag/errorCodes
```

### “清除错误代码”请求的消息格式


请求格式：

```
来自设备的出局消息：

Topic: iotdevice-1/clear/diag/errorCodes
{
    "reqId": "string"
}
```

响应格式：

```
来自服务器的入局消息：

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### “清除错误代码”请求的响应代码

|响应代码 |消息 |
|:---|:---|
|200   |操作成功。|
|400   |输入消息与预期格式不匹配，或者其中一个值不在有效范围内。|
|404   |主题名称不正确，或者设备不在数据库中。|
|409   |设备数据库更新期间发生冲突。要解决此冲突，请根据需要简化操作。|


## “添加日志”请求
{: #diag-add-log}

设备可以选择是否通过添加新日志条目向 {{site.data.keyword.iot_short_notm}} 设备管理支持通知有关更改的信息。日志条目包含日志消息、时间戳记、严重性和可选的基本 64 位编码的二进制诊断数据。

### “添加日志”请求的主题
设备将此请求发布到以下主题：

```
iotdevice-1/add/diag/log
```


### “添加日志”请求的消息格式

下表描述了出局消息属性的格式：

|属性 |描述 |
|:---|:---|
|`message`|指定需要添加到 {{site.data.keyword.iot_short_notm}} 的诊断消息|
|`timestamp`|指定 ISO8601 格式的日志条目日期和时间 |
|`data`|指定可选的基本 64 位编码的诊断数据|
|`severity`|指定消息的严重性（0：参考，1：警告，2：错误）|


请求格式：

```
来自设备的出局消息：

Topic: iotdevice-1/add/diag/log
{
    "d": {
        "message": string,
        "timestamp": string,
        "data": string,
        "severity": number
    },
    "reqId": "string"
}
```

响应格式：

```
来自服务器的入局消息：

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### “添加日志”请求的响应代码

|响应代码 |消息 |
|:---|:---|
|200   |操作成功。|
|400   |输入消息与预期格式不匹配，或者其中一个值不在有效范围内。|
|404   |主题名称不正确，或者设备不在数据库中。|
|409   |设备数据库更新期间发生冲突。要解决此冲突，请根据需要简化操作。|

## “清除日志”请求
{: #diag-clear-logs}

设备可以使用“清除日志”请求类型，请求 {{site.data.keyword.iot_short_notm}} 清除设备的所有日志条目。

### “清除日志”请求的主题


设备将“清除日志”请求发布到以下主题：

```
iotdevice-1/clear/diag/log
```

### “清除日志”请求的消息格式


请求格式：

```
来自设备的出局消息：

Topic: iotdevice-1/clear/diag/log
{
    "reqId": "string"
}
```

响应格式：

```
来自设备的入局消息：

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### “清除日志”请求的响应代码

|响应代码 |消息 |
|:---|:---|
|200   |操作成功。|
|400   |输入消息与预期格式不匹配，或者其中一个值不在有效范围内。|
|404   |主题名称不正确，或者设备不在数据库中。|
|409   |设备数据库更新期间发生冲突。要解决此冲突，请根据需要简化操作。|

## “观察属性更改”请求
{: #observations-observe}

{{site.data.keyword.iot_short_notm}} 可以使用“观察属性更改”请求类型，向设备发送“观察属性更改”请求来观察一个或多个设备属性的更改。设备收到该请求时，每当被观察属性的值更改时，该设备都必须向 {{site.data.keyword.iot_short_notm}} 发送通知请求。

**重要信息：**设备必须实现、观察、通知和取消操作，才能支持[固件操作 - 更新](requests.html#firmware-actions-update)请求类型。

### “观察属性更改”请求的主题


服务器将“观察属性更改”请求发布到以下主题：

```
iotdm-1/observe
```

### “观察属性更改”请求的消息格式


`fields` 数组是设备模型中设备属性的数组。如果指定了复杂字段（例如 `mgmt.firmware`），那么应该同时更新其底层字段，这样才能仅生成单个通知消息。

如果 `rc` 参数的值不是 `200`，那么可以指定响应中使用的 `message` 参数。如果无法检索到任何指定的参数值，那么必须将 `rc` 参数的值设置为 `404`（如果找不到设备）或 `500`（对于其他任何原因）。找不到参数的值时，`fields` 数组应该包含其 `field` 设置为无法读取的每个参数的名称的元素。应该忽略 `value` 参数。要使响应代码参数设置为 `200`，必须指定 `field` 和 `value`，其中 `value` 是 `field` 参数值标识的属性的当前值。

请求格式：

```
来自服务器的入局消息：

Topic: iotdm-1/observe
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

响应格式：

```
来自设备的出局消息：

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "d": {
        "fields": [
            {
                "field": "field_name",
                "value": "field_value"
            }
        ]
    },
    "reqId": "string"
}
```


## “取消属性观察”请求
{: #observations-cancel}

{{site.data.keyword.iot_short_notm}} 可以使用“取消属性观察”请求类型，向设备发送请求来取消一个或多个设备属性的当前观察。请求的 `fields` 部分是设备模型中设备属性名称的数组，例如 `location`、`mgmt.firmware` 或 `mgmt.firmware.state` 参数。

如果 `rc` 参数的值不是 `200`，那么必须指定 `message` 参数。

**重要信息：**设备必须实现、观察、通知和取消操作，才能支持[固件操作 - 更新](requests.html#firmware-actions-update)请求类型。

### “取消属性观察”请求的主题


服务器将“取消属性观察”请求发布到以下主题：

```
iotdm-1/cancel
```


### “取消属性观察”请求的消息格式


请求格式：

```
来自服务器的入局消息：

Topic: iotdm-1/cancel
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

响应格式：

```
来自设备的出局消息：

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "reqId": "string"
}
```



## “通知属性更改”请求
{: #observations-notify}

{{site.data.keyword.iot_short_notm}} 可以使用“通知属性更改”请求类型，对特定属性或一组值发起观察请求。当一个或多个属性的值更改时，设备必须发送包含最新值的通知。

`field_name` 参数的值是已更改属性的名称，`field_value` 是该属性的当前值。属性可以为复杂字段。如果复杂字段中的多个值作为单个操作的结果进行了更新，那么仅发送单个通知消息。

成功处理通知请求后，`rc` 参数的值会设置为 `200`。如果请求不正确，`rc` 参数的值会设置为 `400`。如果未观察到在通知请求中指定的参数，`rc` 参数的值会设置为 `404`。

**重要信息：**设备必须实现、观察、通知和取消操作，才能支持[固件操作 - 更新](requests.html#firmware-actions-update)请求类型。


### “通知属性更改”请求的主题


设备将“通知属性更改”请求发布到以下主题：

```
iotdevice-1/notify
```


### “通知属性更改”请求的消息格式


请求格式：

```
来自设备的出局消息：

Topic: iotdevice-1/notify
{
    "d": {
        "field": "field_name",
        "value": "field_value"
    }
    "reqId": "string"
}
```

响应格式：

```
来自服务器的入局消息：

Topic: iotdm-1/response
{
    "rc": number,
    "reqId": "string"
}
```

### “通知属性更改”请求的响应代码

|响应代码 |消息 |
|:---|:---|
|200   |操作成功。|
|400   |输入消息与预期格式不匹配，或者其中一个值不在有效范围内。|
|404   |主题名称不正确，设备不在数据库中，或者没有观察报告的字段。|
|409   |设备数据库更新期间发生冲突。要解决此冲突，请根据需要简化操作。|
|500   |发生内部错误。|
