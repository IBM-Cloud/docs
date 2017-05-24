---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 设备模型
{: #device_model}

设备模型描述了设备的元数据和管理特征。{{site.data.keyword.iot_full}} 中的设备数据库是设备信息的主来源。应用程序和受管设备可将更新（包括位置更改或固件更新的进度）发送到设备数据库。{{site.data.keyword.iot_short_notm}} 收到这些更新后，会立即更新数据库，从而使这些信息可用于应用程序。

**注：**除了[设备管理扩展](#devicemanagementextension)之外，整个设备模型同时可用于受管设备及非受管设备。但是，非受管设备不能直接在数据库中更新其设备模型。

## 设备标识
{: #device_id}

每个设备都有 `typeId` 和 `deviceId` 属性。通常，`typeId` 表示设备的模型，而 `deviceId` 可表示其序列号。在 {{site.data.keyword.iot_short_notm}} 组织中，`typeId` 和 `deviceId` 的组合对于每个设备必须唯一。

除了这些属性之外，{{site.data.keyword.iot_short_notm}} 还会为每个设备构造另一个标识。此标识称为 `clientId`。`clientId` 基于您的 `organizationId` 以及设备的 `typeId` 和 `deviceId` 值。`clientId` 可唯一地标识单个设备。这些标识中可使用的字符受到限制，以便符合通信协议和 REST API。

还可以使用以下可选设备标识：

- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

有关标识以及其他设备管理标准中对应标识的描述的更多信息，请参阅[属性](#attributes)。


## 标识和设备类型
{: #id_and_device_types}

每个连接到 {{site.data.keyword.iot_short_notm}} 的设备必须与一种设备类型关联。设备类型为共享特征或行为的设备组。

设备类型有一组属性。将设备添加到 {{site.data.keyword.iot_short_notm}} 时，其设备类型中的属性用作模板。如果设备具有值，那么将使用该值。如果设备没有值，那么将使用设备类型值。例如，设备类型可能有 `deviceInfo.fwVersion` 属性的值，此属性反映了制造时的固件版本。在添加设备时，会将此值从设备类型复制到设备。添加设备时，如果已存在 `deviceInfo.fwVersion` 值，那么不会覆盖此值。

更新设备类型的属性时，仅注册的新设备会继承对设备类型模板进行的修改。

## 属性
{: #attributes}

下表显示可应用于 {{site.data.keyword.iot_short_notm}} 中设备的属性的列表。此外，以斜体显示的属性还可应用于设备类型。

键：
  - API：可以使用 API 更新
  - DMA：可以使用设备管理代理程序更新
  - R：只读
  - W：读写
  - A：附加

属性                        | 类型       | 描述                                       | API | DMA   
------------- | ------------- | ------------- | ------------- | -------------  |
        clientId                               | 字符串     | 用于 MQTT 连接的客户机标识                     |  R  |   -  
 *typeId*                         | 字符串     | 设备类型                                       |  R  |   -  
        deviceId                               | 字符串     | 设备标识                                         |  R  |    -
 classId                          | 字符串     | 设备类（“设备”或“网关”）                  |  R  |   -  
        gatewayTypeId                          | 字符串     | 此设备使用的网关的类型标识                    |  R  |    -
 gatewayId                        | 字符串     | 此设备使用的网关的设备标识                                 |  R  |   -  
        status.alert                           | 布尔值     | 指示设备是否有警报                            |  W  |  -   
 *deviceInfo.serialNumber*        | 字符串     | 设备的序列号                                  |  W  |  W    
 *deviceInfo.manufacturer*        | 字符串     | 设备的制造商                                  |  W  |  W   
 *deviceInfo.model*               | 字符串     | 设备的模型                                    |  W  |  W  
 *deviceInfo.deviceClass*         | 字符串     | 设备的类                                      |  W  |  W  
 *deviceInfo.description*         | 字符串     | 设备的描述性名称                              |  W  |  W  
 *deviceInfo.fwVersion*           | 字符串     | 设备上当前已知的固件版本                      |  W  |  W  
 *deviceInfo.hwVersion*           | 字符串     | 设备的硬件版本                                |  W  |  W  
 *deviceInfo.descriptiveLocation* | 字符串     | 描述性位置（例如，房间、楼栋号或地理区域）      |  W  |  W  
 *metadata*                       | 复杂       | 自由格式元数据                                |  W  |  W  
       added.auth.id                           | 字符串     | 添加此设备时所用的标识                          |  R  |   -  
       added.dateTime                          | 字符串     | ISO8601 日期时间：添加设备时的日期和时间      |  R  |    -
 refs.diag.errorCodes             | 字符串     | 错误代码诊断扩展的 URI（如果有）                           |  R  |   -  
       refs.diag.logs                          | 字符串     | 日志诊断扩展的 URI（如果有）                  |  R  |   -  
       refs.location                           | 字符串     | 位置扩展的 URI（如果有）                      |  R  |   -  
       refs.mgmt                               | 字符串     | 设备管理扩展的 URI（如果有）                      |  R  |    -



## 扩展属性
{: #extended_attributes}

除了以上在“属性”部分中列出的核心属性，还有一些被视为核心设备模型扩展的额外属性。关于设备的简单查询将返回核心设备模型（而不是扩展）中的信息。必须发出专门的请求，才会返回扩展中的信息。


扩展名         | 属性前缀             | 用途      
------------- | ------------- | -------------                                         
 诊断          | diag                 | 错误日志和诊断信息                 
 位置          | location             | 设备的位置，可能会定期更新
 设备管理      | mgmt                 | 设备管理操作（如固件更新）       


### 诊断扩展


诊断属性为可选属性，而且只能用于包含错误日志信息的设备。这些属性用于诊断设备问题，而不用于对 {{site.data.keyword.iot_short_notm}} 的连接进行故障诊断。在诊断属性中存储的信息量可能非常大，因此必须进行具体查询。

诊断日志信息存储为条目数组。每个条目均由消息、严重性指示符、时间戳记和可选的数据字节数组组成。可以使用 API 来附加条目。但是，附加条目可能会导致丢失较早的条目，以使诊断日志的大小可控。


属性            | 类型       | 描述                                                 | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | 整数        </br> 数组  | 错误代码数组                                         |  A  |  A  
 diag.log[]           | 数组                    | 诊断数据数组                                         |  A  |  A  
 diag.log[].message   | 字符串     | 诊断消息                                             |  -   |    -
 diag.log[].timestamp | 字符串     | ISO8601 日期时间：日志条目的日期和时间               |  -   |    -
 diag.log[].logData   | 字符串     | 字节：诊断数据，基本 64 位编码                         |  -   |    -
 diag.log[].severity  | 数值                    | 消息的严重性（0：参考，1：警告，2：错误）            |  -   |    -


### 位置扩展

位置属性为可选属性，而且只能用于包含位置信息的设备。位置信息单独进行存储，以允许使用更适合动态信息的存储机制。频繁更新信息时（例如，使用移动设备时），这一点非常重要。

对于重点关注频繁位置更新的解决方案，预期会将位置视为设备事件有效内容的一部分，以实现更高的更新速率、更简单的历史存储和更轻松的数据分析。


属性                 | 类型   | 描述                                             | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | 数值                | 使用 WGS84 的经度（以十进制度为单位）                       |  W  |  W  
 location.latitude         | 数值                | 使用 WGS84 的纬度（以十进制度为单位）                       |  W  |  W  
 location.elevation        | 数值                | 使用 WGS84 的海拔（以米为单位）                         |  W  |  W  
 location.measuredDateTime | 字符串 | ISO8601 日期时间：位置测量的日期和时间                      |  W  |  W  
 location.updatedDateTime  | 字符串 | ISO8601 日期时间：日期和时间                                |  R  |   
 location.accuracy         | 数值                | 位置的精度（以米为单位）                                    |  W  |  W  


### 设备管理扩展
{: #devicemanagementextension}

管理属性仅适用于受管设备。受管设备休眠时，会变为非受管设备，并且会删除 `mgmt.` 属性。`mgmt.` 属性由 {{site.data.keyword.iot_short_notm}} 在处理设备管理请求后设置。这些属性不能直接使用 API 写入。

设备有管理生命周期，此生命周期通过其作为受管设备的设备状态进行定义。设备上的设备管理代理程序负责使用设备管理协议发送“管理设备”请求。要在大量设备中处理失效的设备，可以将受管设备设置为定期发送“管理设备”请求。如果此请求未在指定时间段内发送到 {{site.data.keyword.iot_short_notm}}，那么受管设备会变为休眠。为了方便使用此功能，“管理设备”请求有一个可选的 lifetime 参数。{{site.data.keyword.iot_short_notm}} 收到设置了 lifetime 参数的“管理设备”请求时，会计算在需要发出另一个“管理设备”请求之前的时间，并将其存储在 `mgmt.dormantDateTime` 属性中。


属性                     | 类型    | 描述                             | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | 布尔值  | 指示设备是否已休眠                                  |  R  |  -
 mgmt.dormantDateTime           | 字符串  | ISO8601 日期时间：受管设备将休眠的日期和时间          |  R  |  -   
 mgmt.lastActivityDateTime      | 字符串  | ISO8601 日期时间：上一次定期更新活动的日期和时间    |  R  |    -
 mgmt.supports.deviceActions    | 布尔值  | 指示设备是否支持“重新引导”和“恢复出厂设置”操作  |  R  |   -  
 mgmt.supports.firmwareActions  | 布尔值  | 指示设备是否支持“固件下载”和“固件更新”操作      |  R  |     -
 mgmt.firmware.version          | 字符串  | 设备上的固件版本                                |  R  |  W  
 mgmt.firmware.name             | 字符串  | 设备上使用的固件的名称                            |  R  |  W  
 mgmt.firmware.uri              | 字符串  | 可从其中下载固件映像的 URI                          |  R  |  W  
 mgmt.firmware.verifier         | 字符串  | 固件映像的用于验证其完整性的验证器（如校验和）          |  R  |  W  
 mgmt.firmware.state            | 数值                 | 指示固件下载状态                                    |  R  |  W  
 mgmt.firmware.updateStatus     | 数值                 | 指示更新状态                                        |  R  |  W  
 mgmt.firmware.updatedDateTime  | 字符串  | ISO8601 日期时间：上次更新的日期                    |  R  |    -
