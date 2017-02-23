---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 针对设备的 HTTP REST API
{: #api}

**重要信息：**针对设备的 {{site.data.keyword.iot_full}} HTTP REST API 功能只作为受限 Beta 程序的一部分提供。未来更新可能会包含与此功能当前版本不兼容的更改。请尝试此功能，[让我们了解您的想法](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html)。

## 访问 HTTP REST API 文档
{: #api_link}

要访问 {{site.data.keyword.iot_short_notm}} HTTP REST API 文档，并获取有关如何将设备集成到组织中的更多信息，请转至 [https://docs.internetofthings.ibmcloud.com/swagger/v0002.html](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)。

{{site.data.keyword.iot_short_notm}} HTTP REST API 的唯一受支持版本是 V2。请确保您的 {{site.data.keyword.iot_short_notm}} 解决方案使用的是 V2。

## 客户机连接
{: #client_connections}

有关客户机安全性以及如何将客户机连接到 {{site.data.keyword.iot_short_notm}} 中设备的信息，请参阅[将应用程序、设备和网关连接到 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。

# 针对设备的 HTTP REST 消息传递 API
{: #rest_messaging_api}

## 发布事件
{: #event_publication}

除了使用 MQTT 消息传递协议外，还可以配置设备，以使用 HTTP REST API 命令通过 HTTP 将事件发布到 {{site.data.keyword.iot_short_notm}}。

使用以下某个 URL 提交来自连接到 {{site.data.keyword.iot_short_notm}} 的设备的 `POST` 请求：

### 非安全 POST 请求
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 安全 POST 请求
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**注：**还可以为安全 HTTP API 调用指定端口 443（缺省 SSL 端口）。

如果要将设备或应用程序连接到 Quickstart 服务，请改为使用以下某个 URL：

### 向 Quickstart 发布的非安全 POST 请求
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 向 Quickstart 发布的安全 POST 请求
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**重要说明：**
- 在当前 HTTP REST API 版本中，只能使用 HTTP 消息传递来提交设备事件。使用 MQTT 消息传递协议可提交其他设备管理和控制功能的请求。
- 因为授权 HTTP 头是无法更改的，所以 HTTP 连接只能重复用于发布同一设备的事件。
- 还可以为安全 HTTP API 调用指定端口 443（缺省 SSL 端口）。

### 认证

所有请求都必须包含授权头。基本认证是唯一受支持的方法。设备通过 {{site.data.keyword.iot_short_notm}} HTTP REST API 发起 HTTP 请求时，以下凭证是必需的：

|凭证|必需的输入|
|:---|:---|
|用户名|`use-token-auth`
|密码| 注册设备时自动生成或手动指定的认证令牌。

### Content-Type 请求头

必须为请求提供 `Content-Type` 请求头。下表显示了如何将受支持的类型映射到 {{site.data.keyword.iot_short_notm}} 内部格式。

|Content-Type 头|{{site.data.keyword.iot_short_notm}} 中的格式|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### 服务质量

与 MQTT 服务质量“至多一次”传递服务级别 0 类似，HTTP REST 消息传递提供了非持久性消息传递，但它会验证请求是否正确，并在发送 HTTP 响应之前，验证其是否可以传递到服务器。包含 HTTP 状态码 200 的回复将确认消息已传递到服务器。使用“至多一次”MQTT 服务质量级别或 HTTP 同等级别来传递事件消息时，设备或应用程序必须实现重试逻辑以保证传递。

有关 {{site.data.keyword.iot_short_notm}} 的 MQTT 协议和服务质量级别的更多信息，请参阅 [MQTT 消息传递](../reference/mqtt/index.html)。

## 上次事件高速缓存
{: #last-event-cache}

通过使用 {{site.data.keyword.iot_short_notm}} 上次事件高速缓存 API，可检索设备上次所发送的事件。这在设备联机或脱机的情况下都适用，这样不管设备的物理位置或使用状态如何，您都可检索设备状态。您可以检索特定设备的事件标识的上次记录值，或检索特定设备报告的每个事件标识的上次记录值。对于最多 365 天之前发生的任何特定事件，可检索设备的上次事件数据。

要请求特定事件标识的最新值，请使用以下 API 请求，此请求将返回“power”事件标识的上次记录值。

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

响应将包含设备发送的所有事件标识。在以下示例中，将返回“power”和“temperature”事件的值。

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
