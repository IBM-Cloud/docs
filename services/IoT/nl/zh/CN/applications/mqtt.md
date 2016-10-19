---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 针对应用程序的 MQTT 连接
{: #mqtt}
上次更新时间：2016 年 8 月 31 日
{: .last-updated}

MQTT 是设备和应用程序用于与 {{site.data.keyword.iot_full}} 通信的主要协议。提供的客户机库、信息和样本可帮助您连接 {{site.data.keyword.iot_short_notm}} 应用程序。
{:shortdesc}

## 客户机连接
{: #client_connections}

有关客户机安全性以及如何将 MQTT 客户机连接到 {{site.data.keyword.iot_short_notm}} 中应用程序的信息，请参阅[将应用程序、设备和网关连接到 {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html)。

## MQTT 认证
{: #mqtt_authentication}

{{site.data.keyword.iot_short_notm}} 应用程序需要 API 密钥以连接到组织。注册 API 密钥时，会生成认证令牌，此令牌必须与此 API 密钥配合使用。

以下示例显示典型 API 密钥：

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}


以下示例显示典型认证令牌：

```
MP$08VKz!8rXwnR-Q*
```

通过使用 API 密钥建立 MQTT 连接时，确保应用以下准则：

- MQTT 客户机标识采用以下格式：a:*orgId*:*appId*
- MQTT 用户名是 API 密钥（例如，a-*orgId*-a84ps90Ajs）
- MQTT 密码是认证令牌（例如，MP$08VKz!8rXwnR-Q*）


## 发布设备事件
{: #publishing_device_events}

应用程序可以把事件当作源自任何已注册设备的事件进行发布，例如：

-  发布到主题：iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

要将设备中的现有数据移植到 {{site.data.keyword.iot_short_notm}} 中，可以创建应用程序来处理数据，并将其发布到 {{site.data.keyword.iot_short_notm}} 中。

**重要信息：**消息有效内容限制为最大 131072 字节。超过此限制的消息将被拒绝。

## 发布设备命令
{: #publishing_device_commands}

应用程序可以向任何已注册设备发布命令，例如：

-  发布到主题：iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

## 预订设备事件
{: #subscribe_device_events}

应用程序可以预订来自一个或多个设备的事件，例如：

-  预订主题：iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

**注：**要预订多个类型的事件或预订多个单设备的事件，请对以下任一组件使用 MQTT“任意”通配符 (+)：

- device_type
- device_id
- event_id
- format_string

## 预订设备命令
{: #subscribe_device_commands}

应用程序可以预订要发送到一个或多个设备的命令，例如：

-  预订主题：iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

**注：**要预订多个类型的事件或预订多个单设备的事件，请对以下任一组件使用 MQTT“任意”通配符 (+)：

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

通过调整应用程序的连接方式，并均衡跨应用程序多个实例的事件消息负载，可以使 {{site.data.keyword.iot_short_notm}} 应用程序的可扩展性更强。

最佳负载均衡和可扩展性所需的客户机数根据部署而变化。要确定最佳客户机数，您需要对系统进行压力测试。

要启用负载均衡，请确保预订是非持久的，并且预订中的客户机标识采用以下格式：

<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
{: codeblock}

其中：
-  字符 **A** 指示客户机是可扩展应用程序。
-  *orgId* 是注册服务时生成的唯一 6 个字符组织标识，即首次注册服务时分配的字母数字字符串。
-  *appId* 是客户机的用户定义唯一字符串标识。字符串只能包含字母数字字符（a-z、A-Z 和 0-9）以及短划线 (-)、下划线 (_)、点 (.) 和特殊字符。

**重要信息：**
- 可扩展应用程序仅支持非持久预订。
- 客户机标识必须以大写 **A** 字符开头，才能由 {{site.data.keyword.iot_short_notm}} 正确指定为可扩展应用程序。
- 属于可扩展应用程序的其他客户机必须使用相同的客户机标识。


### 工作方式

{{site.data.keyword.iot_short_notm}} 服务扩展 MQTT V3.1.1 消息传递协议规范，以支持共享的预订。共享的预订为应用程序提供了负载均衡能力。如果后端企业应用程序无法处理正在发布到特定主题空间的消息量时，可能需要共享的预订。例如，许多设备发布的消息正在由单个应用程序进行处理时，可能有必要使用共享预订的负载均衡能力。{{site.data.keyword.iot_short_notm}} 共享预订支持仅限于非持续性预订。


**示例**

以下场景是可扩展应用程序如何在 {{site.data.keyword.iot_short_notm}} 中工作的示例：

- 客户机 1 使用 **A:abc123:myApplication** 进行连接，并预订所有设备事件，这意味着客户机 1 会接收发布的 100% 设备事件。
- 客户机 2 使用 **A:abc123:myApplication** 进行连接，也预订所有设备事件，这意味着客户机 1 和客户机 2 会共享发布的所有事件。处理负载在客户机 1 和客户机 2 之间共享。
- 客户机 3 使用 **A:abc123:myApplication** 进行连接，也预订所有设备事件，这意味着客户机 1、客户机 2 和客户机 3 会共享事件的处理负载。
- 然后，客户机 2 和客户 3 取消预订所有设备事件，这意味着只有客户机 1 会接收发布的所有设备事件。虽然客户机 2 和客户机 3 仍连接到服务时，但只有客户机 1 会接收发布的 100% 设备事件。
- 当两个或更多应用程序共享预订时，消息可能不会按其发送顺序到达。例如，虽然消息 A 先于消息 B 发出，但消息 B 到达客户机 1 的时间可能会早于消息 A 到达客户机 2 的时间。
