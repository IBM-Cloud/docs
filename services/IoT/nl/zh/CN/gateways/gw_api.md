---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 针对网关设备的 HTTP REST API
{: #api_link}


要访问 {{site.data.keyword.iot_short_notm}} HTTP REST API 文档，并找到有关创建、更新、删除和列出设备的更多信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)。

{{site.data.keyword.iot_short_notm}} HTTP REST API 的唯一受支持版本是 V2。请确保您的 {{site.data.keyword.iot_short_notm}} 解决方案使用的是 V2。

## 客户机连接
{: #client_connections}

有关客户机安全性以及如何将客户机连接到 {{site.data.keyword.iot_short_notm}} 中网关设备的信息，请参阅[将应用程序、设备和网关连接到 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。


### 认证

所有请求都必须包含授权头。基本认证是唯一受支持的方法。设备使用 {{site.data.keyword.iot_short_notm}} HTTP REST API 发起 HTTP 请求时，以下凭证是必需的：

|凭证|必需的输入|
|:---|:---|
|用户名| `g/{orgId}/{gwType}/{gwDevId}`
|密码| 注册网关设备时自动生成或手动指定的认证令牌。

其中：

<dl>
<dt>orgId</dt>  
<dd>组织名称，必须与主机头中指定的名称相匹配。</dd>

<p></p>
<dt>gwType</dt>  
<dd>网关的类型。</dd>
<p></p>
<dt>gwDevId</dt>  
<dd>是网关的设备标识。</dd>
</dl>


### Content-Type 请求头

必须为请求提供 `Content-Type` 请求头。下表显示了如何将受支持的类型映射到 {{site.data.keyword.iot_short_notm}} 内部格式：

|Content-Type 头|{{site.data.keyword.iot_short_notm}} 中的格式|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

## 上次事件高速缓存
{: #last-event-cache}

通过使用 {{site.data.keyword.iot_short_notm}} 上次事件高速缓存 API，可检索设备上次所发送的事件。此 API 在设备联机或脱机的情况下都适用，这样不管设备的物理位置或使用状态如何，您都可检索设备状态。您可以检索特定设备的事件标识的上次记录值，或检索特定设备报告的每个事件标识的上次记录值。对于最多 365 天之前发生的任何特定事件，可检索设备的上次事件数据。

要请求特定事件标识的最新值，请使用以下 API 请求，此请求将返回“power”事件标识的上次记录值：

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

返回的响应为以下 JSON 格式：

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**注：**虽然 API 响应为 JSON 格式，但是可以采用任何格式写入事件有效内容。上次事件高速缓存 API 返回的有效内容以基本 64 位格式编码。

要请求设备报告的每个事件标识的最新值，请使用以下 API 请求：

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

响应包含设备发送的所有事件标识。在以下示例中，将返回“power”和“temperature”事件的值。

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
