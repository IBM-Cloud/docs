---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 操作类型{: #actions}

除了在“警报”仪表板中显示警报外，{{site.data.keyword.iotrtinsights_short}} 还支持多种类型的规则触发操作，例如发送电子邮件和发送 Webhook。
{: shortdesc}

## 创建操作{: #shared}
您可以[直接从规则编辑器创建操作](rules.html "创建规则")，也可以在“操作”面板中创建操作，然后在创建规则时选择这些操作。

要在“操作”面板中创建操作，请执行以下步骤：
1. 在 {{site.data.keyword.iotrtinsights_short}} 控制台中，转至**分析 > 操作**。
2. 单击**添加新操作**，选择操作类型，为操作命名，并提供描述。
3. 为要创建的操作类型提供必需参数。
操作类型：  
 - [发送电子邮件](#email "发送电子邮件")
 - [Webhook](#webhook "Webhook")
 - [Node-RED](#nodered "Node-RED")
 - [IFTTT](#ifttt "IFTTT")
4. 单击**确定**以创建新操作。

现在，该操作在[规则编辑器](rules.html#rules "规则编辑器")中可用。



## 发送电子邮件{: #email}
使用“发送电子邮件”操作可在规则触发时向一个或多个收件人发送电子邮件。

示例：[发送电子邮件](action_examples.html#emailex)。

以下参数用于配置“发送电子邮件”操作：

参数   | 描述
---|---
名称   | 操作的名称，在“警报”仪表板中使用。
描述   | 操作的简短描述。
收件人 | 一个或多个电子邮件地址，以逗号分隔。
抄送   | 一个或多个电子邮件地址，以逗号分隔。
主题   | 电子邮件的主题行。（可选）可以使主题自动以“IoT Real-Time Insight 警报”开头。

在规则触发时，会自动根据设备的消息创建电子邮件正文。  
**重要信息：**如果设备数据包含敏感信息，那么可以选择不在电子邮件中包含设备数据，而只在“警报”面板中显示敏感数据。


## Webhook{: #webhook}
使用 Webhook 操作可在触发警报时向支持 Webhook 的 Web Service 发起 HTTP 请求。例如，Webhook 可用于在设备中的传感器报告异常读数时提交对资产的服务请求。

示例：[使用 Webhook 在 Slack 上进行发布](action_examples.html#webhookex)。

以下参数用于配置 Webhook 操作：

参数     | 描述
---|---
名称     | 操作的名称，在“警报”仪表板中使用。
描述     | 操作的简短描述。
URL      | 支持 Webhook 的目标服务器的 URL。**提示：**您可以使用[变量替换](#variable_substitution)在 URL 中动态包含更多数据。
方法     | 要执行的 Webhook 调用的类型。选择以下某种类型：GET、HEAD、OPTIONS、PATCH、PUT、POST 或 DELETE。
用户名   | Web Service 需要时包含。
密码     | Web Service 需要时包含。**重要信息：**密码是以明文形式发送的。
头       | 头由键值对构成。**提示：**您可以使用[变量替换](#variable_substitution)在头中动态包含更多数据。
内容类型 | 正文内容的类型：JSON、XML、WWW 表单 URL 编码的内容或纯文本。适用于 OPTIONS、PATCH、PUT、POST 和 DELETE 方法。
主体     | Webhook 调用的主体。适用于 OPTIONS、PATCH、PUT、POST 和 DELETE 方法。缺省情况下，“主体”字段已预填充[变量替换](#variable_substitution)中列出的所有变量。选择**使用定制的消息体**来编辑“主体”字段的内容。**重要信息：**Webhook 服务器可能要求主体中包含某些特定字段。例如，Slack Webhook 必须包含“text”字段。   



## Node-RED{: #nodered}
使用 Node-RED 操作可在触发规则时连接到 Node-RED 应用程序。有关使用 Node-RED 的更多信息，请参阅[使用 Internet of Things Starter 应用程序创建应用程序](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)。

示例：[使用 Node-RED 发送短信](action_examples.html#noderedex)。

以下参数用于配置 Node-RED 操作：

参数   | 描述
---|---
名称   | 操作的名称，在“警报”仪表板中使用。
描述   | 操作的简短描述。
URL    | 目标 Node-RED HTTP 输入节点的 URL。
用户名 | Node-RED 服务需要时包含。
密码   | Node-RED 服务需要时包含。**重要信息：**密码是以明文形式发送的。
主体   | 缺省情况下，“主体”字段已预填充[变量替换](#variable_substitution)中列出的所有变量。选择**使用定制的消息体**来编辑“主体”字段的内容。

## IFTTT {: #ifttt}
使用 IFTTT 操作可在触发规则时触发 IFTTT 配方。有关触发 Real-Time Insights 操作作为 IFTTT 配方的更多信息，请参阅 IFTTT 站点上的 [Maker Channel](https://ifttt.com/maker)。

示例：[使用 IFTTT 发布 Trello 卡](action_examples.html#iftttex)。

以下参数用于配置 IFTTT 操作：

参数   | 描述
---|---
名称   | 操作的名称，在“警报”仪表板中使用。
描述   | 操作的简短描述。
密钥   | 用于触发事件的 Maker 通道密钥。
事件   | 配置为 Maker 事件触发器的事件的名称。可以创建具有不同触发器的多个配方，每个配方具有不同的事件名称。
值 1-3 | 可以在这些参数中传递任何内容，这些内容会传递到 IFTTT 配方中的操作。**提示：**您可以使用[变量替换](#variable_substitution)在头中动态包含更多数据。

## 变量替换{: #variable_substitution}
包含以下变量替换可动态包含设备数据。变量必须用双大括号括起。

变量 | 描述
---|---
**URL、头和主体** |
`{{timestamp}}` | 消息中的时间戳记
`{{tenantId}}` | Real-Time Insights 服务的标识
`{{deviceId}}` | 设备的标识
`{{ruleName}}` | 包含操作的规则的名称
**仅限主体** |
`{{ruleDescription}}`| 包含操作的规则的描述
`{{ruleCondition}}` | 触发操作的规则条件
`{{message}}` | 包含触发了规则的数据点的原始设备消息
