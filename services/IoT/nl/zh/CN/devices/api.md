---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 针对设备的 HTTP REST API
{: #api}
上次更新时间：2016 年 9 月 9 日
{: .last-updated}

**重要信息：**针对设备的 {{site.data.keyword.iot_full}} HTTP REST API 功能只作为受限 Beta 程序的一部分提供。未来更新可能会包含与此功能当前版本不兼容的更改。请尝试此功能，[让我们了解您的想法](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html)。

## 访问 HTTP REST API
{: #api_link}

要访问 {{site.data.keyword.iot_short_notm}} HTTP REST API，并获取有关如何将设备集成到组织中的更多信息，请转至 https://docs.internetofthings.ibmcloud.com/swagger/v0002.html。

{{site.data.keyword.iot_short_notm}} HTTP REST API V2 是唯一支持的版本。请确保您的 {{site.data.keyword.iot_short_notm}} 解决方案使用的是 V2。

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

如果要将设备或应用程序连接到 Quickstart 服务，请改为使用以下某个 URL：

### 向 Quickstart 发布的非安全 POST 请求
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 向 Quickstart 发布的安全 POST 请求
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**重要说明：**
- 在当前 HTTP REST API 版本中，只能使用 HTTP 消息传递来提交设备事件。使用 MQTT 消息传递协议可提交其他设备管理和控制功能的请求。
- HTTP 连接只能复用于发布同一设备的事件，因为无法更改授权 HTTP 头。

### 认证

所有请求都必须包含授权头。基本认证是支持的唯一方法。设备通过 {{site.data.keyword.iot_short_notm}} HTTP REST API 发起 HTTP 请求时，以下凭证是必需的：

```
username = "use-token-auth"
password = 认证令牌
```

### Content-Type 请求头

必须为请求提供 `Content-Type` 请求头。下表显示了如何将支持的类型映射到 {{site.data.keyword.iot_short_notm}} 内部格式。

|Content-Type 头|{{site.data.keyword.iot_short_notm}} 中的格式|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### 服务质量

与 MQTT 服务质量“至多一次”传递服务级别 0 类似，HTTP REST 消息传递提供的也是非持久性消息传递，但它会验证请求是否正确，并在发送 HTTP 请求之前，验证其是否可以传递到服务器。包含 HTTP 状态码 200 的回复确认消息已传递到服务器。使用“至多一次”MQTT 服务质量或 HTTP 同等级别来传递事件消息时，设备或应用程序必须实现重试逻辑以保证传递。

有关 {{site.data.keyword.iot_short_notm}} 的 MQTT 协议和服务质量级别的更多信息，请参阅 [MQTT 消息传递](../reference/mqtt/index.html)。
