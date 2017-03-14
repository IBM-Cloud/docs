---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 针对应用程序的 HTTP REST API
{: #api}

使用 {{site.data.keyword.iot_full}} HTTP REST API 可构建和定制应用程序，以用于与 {{site.data.keyword.iot_short_notm}} 上的组织进行交互。
{:shortdesc}

## 功能
{: #capabilities}

{{site.data.keyword.iot_short_notm}} HTTP REST API 支持将以下能力和功能用于应用程序：

- 组织信息检索
- 批量设备操作（列示、添加和除去）
- 设备类型操作（列示、创建、删除、查看详细信息和更新）
- 设备操作（列示、添加、除去、查看详细信息、更新、查看位置和查看管理信息）
- 设备诊断操作（清除日志、检索日志、添加日志信息、删除日志、获取特定日志、清除错误代码、获取设备错误代码和添加错误代码）
- 连接问题确定（列出设备连接日志事件）
- 最后一个事件高速缓存（查看特定设备的最后一个事件）
- 设备管理请求操作（列出设备管理请求、启动请求、清除请求状态、获取请求的详细信息、按设备列出所有请求状态和获取特定设备的请求状态）
- 使用情况管理操作（检索使用的数据总量）
- 设备事件发布 (beta)
- 服务状态查询（按组织检索服务状态）

## 访问 HTTP REST API 文档
{: #api_link}

要访问 {{site.data.keyword.iot_short_notm}} HTTP REST API 文档并获取有关如何构建和定制应用程序的更多信息，请转至以下 URL：[https://docs.internetofthings.ibmcloud.com/swagger/v0002.html](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)

{{site.data.keyword.iot_short_notm}} HTTP REST API 的唯一受支持版本是 V2。请确保您的 {{site.data.keyword.iot_short_notm}} 解决方案使用的是 V2。

# 针对应用程序的 HTTP REST 消息传递 API
{: #rest_messaging_api}

## 发布事件和命令
{: #event_command_publication}

除了使用 MQTT 消息传递协议外，还可将应用程序配置为使用以下某个 HTTP REST API 命令通过 HTTP 将事件和命令发布到 {{site.data.keyword.iot_short_notm}}：

### 非安全事件 POST 请求
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 安全事件 POST 请求
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**注：**还可以为安全 HTTP API 调用指定端口 443（缺省 SSL 端口）。

### 非安全命令 POST 请求
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### 安全命令 POST 请求
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

如果要将设备或应用程序连接到 Quickstart 服务，请将 **orgId** 替换为字符串“quickstart”。

**注：**
- 虽然应用程序可以复用 HTTP 连接来向不同设备发布事件或命令，但无法更改授权 HTTP 头。
- 还可以为安全 HTTP API 调用指定端口 443（缺省 SSL 端口）。

### 认证

所有请求都必须包含授权头。基本认证是唯一受支持的方法。应用程序是使用 API 密钥进行认证的。应用程序通过 {{site.data.keyword.iot_short_notm}} HTTP REST API 发起任何请求时，以下凭证是必需的：

```
username = API 密钥（例如，a-orgId-a84ps90Ajs）
password = 认证令牌
```

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
