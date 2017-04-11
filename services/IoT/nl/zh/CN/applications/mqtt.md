---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 针对应用程序的 MQTT 连接
{: #mqtt}

MQTT 是设备和应用程序用于与 {{site.data.keyword.iot_full}} 通信的主要协议。提供的客户机库、信息和样本可帮助您连接和集成 {{site.data.keyword.iot_short_notm}} 应用程序。
{:shortdesc}

## 客户机连接
{: #client_connections}

有关客户机安全性以及如何将 MQTT 客户机连接到 {{site.data.keyword.iot_short_notm}} 中应用程序的信息，请参阅[将应用程序、设备和网关连接到 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。

## MQTT 认证
{: #mqtt_authentication}

{{site.data.keyword.iot_short_notm}} 应用程序需要 API 密钥以连接到组织。注册 API 密钥时，会生成认证令牌，此令牌必须与该 API 密钥配合使用。

以下示例显示了典型的 API 密钥：

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}


以下示例显示了典型的认证令牌：

```
MP$08VKz!8rXwnR-Q*
```

通过使用 API 密钥建立 MQTT 连接时，确保应用以下准则：

- MQTT 客户机标识采用以下格式：a:*orgId*:*appId*
- MQTT 用户名是 API 密钥（例如，a-*orgId*-a84ps90Ajs）
- MQTT 密码是认证令牌（例如，MP$08VKz!8rXwnR-Q*）


## 发布设备事件
{: #publishing_device_events}

应用程序可以将事件当作来自任何已注册设备的事件进行发布，例如：

-  发布到主题：iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

要将设备中的现有数据发送到 {{site.data.keyword.iot_short_notm}} 中，可以创建应用程序来处理数据，并将其发布到 {{site.data.keyword.iot_short_notm}} 中。

**重要信息：**消息有效内容限制为最大 131072 字节。超过此限制的消息将被拒绝。

### 保留消息
{{site.data.keyword.iot_short_notm}} 组织无权发布保留的 MQTT 消息。如果应用程序、网关或设备发送保留消息，{{site.data.keyword.iot_short_notm}} 服务将覆盖已设置为 true 的保留消息标志，并将消息当作该标志设置为 false 进行处理。

## 发布设备命令
{: #publishing_device_commands}

应用程序可以向任何已注册设备发布命令，例如：

-  发布到主题：iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

## 预订设备事件
{: #subscribe_device_events}

应用程序可以预订来自一个或多个设备的事件，例如：

-  预订主题：iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

**注：**要预订多种类型的事件或预订来自多个设备的事件，请对以下任一组件使用 MQTT“任意”通配符 (+)：

- device_type
- device_id
- event_id
- format_string

## 预订设备命令
{: #subscribe_device_commands}

应用程序可以预订要发送到一个或多个设备的命令，例如：

-  预订主题：iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

**注：**要预订多种类型的事件或预订来自多个设备的事件，请对以下任一组件使用 MQTT“任意”通配符 (+)：

-  device_type
-  device_id
-  cmd_id
-  format_string

## 预订设备状态消息
{: #subscribe_device_status}

应用程序可以预订监视一个或多个设备的状态，例如：

-  预订主题：iot-2/type/*device_type*/id/*device_id*/mon

**注：**要预订来自多个设备的更新，请对以下任一组件使用 MQTT“任意”通配符 (+)：

- device_type
- device_id

## 预订应用程序状态消息
{: #subscribe_app_status}

应用程序可以预订监视一个或多个应用程序的状态，例如：

- 预订主题：iot-2/app/*appId*/mon

**注：**要预订所有应用程序的更新，请对 *appId* 组件使用 MQTT“任意”通配符 (+)。


## Quickstart 限制
{: #quickstart_restrictions}
如果计划创建应用程序代码以用于 Quickstart 服务，注意 Quickstart 中不支持以下功能：

- 发布命令
- 预订命令
- 在 **deviceType** 或 **appId** 组件中使用 MQTT“任意”通配符 (+)
- 通过传输层安全性 (TLS) 建立 MQTT 连接
- 可扩展应用程序

## 可扩展应用程序
{: #scalable_apps}

通过调整应用程序的连接方式，并在应用程序的多个实例之间均衡事件消息的负载处理，可以提高 {{site.data.keyword.iot_short_notm}} 应用程序的可扩展性。

最佳负载均衡和可扩展性所需的客户机数量根据部署而变化。要确定最佳客户机数量，您需要对系统进行压力测试。

可扩展的应用程序定义为非持久预订或混合持久共享预订 (Beta)。

### 非持久预订
{: #shared_sub_non_durable}

要启用负载均衡，请确保应用程序预订是非持久的，并且预订中的客户机标识采用以下格式：

<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
{: codeblock}

其中：
-  字符 **A** 指示客户机是可扩展应用程序。
-  *orgId* 是注册服务时生成的 6 字符唯一组织标识。
-  *appId* 是客户机的用户定义唯一字符串标识。该字符串只能包含字母数字字符（a-z、A-Z 和 0-9）以及短划线 (-)、下划线 (_) 和点 (.) 特殊字符。


**重要信息：**
- 客户机标识必须以大写 **A** 字符开头，才能由 {{site.data.keyword.iot_short_notm}} 正确指定为可扩展应用程序。
- 属于可扩展应用程序一部分的其他客户机必须使用相同的客户机标识。
- 非持久预订的干净会话值必须设置为 false (0)。

### 混合持久共享预订 (Beta)
{: #shared_sub_mixed}

{{site.data.keyword.iot_short_notm}} 服务扩展了 MQTT V3.1.1 消息传递协议规范，以支持对混合持久共享预订的 Beta 试用。共享的预订为应用程序提供了负载均衡能力。如果后端企业应用程序无法处理正在发布到特定主题空间的消息量，可能需要共享的预订。例如，许多设备发布的消息正在由单个应用程序进行处理时，可能有必要使用共享的预订的负载均衡能力。

对于混合持久共享预订，请确保预订中的客户机标识采用以下格式：

<pre class="pre">A:<var class="keyword varname">org</var>:<var class="keyword varname">appId</var>:<var class="keyword varname">instanceId</var></pre>
{: codeblock}

其中：
- 客户机标识中的字符 **A**、*orgId* 和 *appId* 的定义方式与[非持久预订](#shared_sub_non_durable)的相同。
- *instanceID* 这一字符串不得超过 36 个字符，仅可包含以下字符：
   - 字母数字字符（a-z、A-Z 和 0-9）
   - 连字符 (-)
   - 下划线 (_)
   - 点 (.)

**重要信息：**
- 对混合持久共享预订的支持仅作为 Beta 功能提供。不要在生产应用程序中实施 Beta 功能。
- 在混合持久共享预订中，干净会话值可以设置为 true (1) 或 false (0)。
- 使用 instanceID 连接的客户机与不使用 instanceID 连接的客户机所使用的预订不同。因此，如果要在混合持久共享预订上连接多个客户机，您需要在所有预订中指定 instanceID。

**示例场景**

以下场景是有关非持久可扩展应用程序如何在 {{site.data.keyword.iot_short_notm}} 中工作的示例：

- 客户机 1 作为 **A:abc123:myApplication** 进行连接，并预订所有设备事件，这意味着客户机 1 会接收发布的 100% 的设备事件。
- 客户机 2 作为 **A:abc123:myApplication** 进行连接，也预订所有设备事件，这意味着客户机 1 和客户机 2 会共享发布的所有事件。处理负载会在客户机 1 和客户机 2 之间共享。
- 客户机 3 作为 **A:abc123:myApplication** 进行连接，也预订所有设备事件，这意味着客户机 1、客户机 2 和客户机 3 会共享事件的处理负载。
- 然后，客户机 2 和客户 3 取消预订所有设备事件，这意味着只有客户机 1 会接收发布的所有设备事件。虽然客户机 2 和客户机 3 仍连接到该服务，但客户机 1 会接收发布的 100% 的设备事件。
- 当两个或更多应用程序共享预订时，消息可能不会按其发送顺序到达。例如，尽管消息 A 是最先发送的，但消息 B 到达客户机 1 的时间可能会早于消息 A 到达客户机 2 的时间。
