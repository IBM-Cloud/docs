---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 操作示例

“发送电子邮件”、“IFTTT”、“Node-RED”和“Webhook”操作类型展示了大量用于执行任务的选项（只有您想不到的，没有您找不到的）以及其他工具使用的连接器。例如，在 Slack 上发布设备状态消息、向服务人员发送短信、创建设备服务请求等各种各样的操作。
{: shortdesc}

下面的示例全部表示在温度（以设备的温度数据点表示）超过 100 度时通知服务工程师的操作，使用的规则条件如下：
`temp >= 100`

可以在发生该规则条件时触发以下一个或多个操作类型：  
 - [发送电子邮件](#emailex "发送电子邮件")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## 使用“发送电子邮件”操作{: #emailex}
在此示例中，该操作配置为使用 Real-Time Insights 的“发送电子邮件”功能向主服务工程师发送电子邮件，同时向其经理发送备份电子邮件。

要创建“发送电子邮件”操作，请执行以下步骤：
1. 在 Real-Time Insights 中，转至**分析 > 操作**。
2. 单击**添加新操作**。
3. 选择**发送电子邮件**类型。
4. 输入操作名称：`发送服务请求电子邮件`。
5. 输入描述：`向服务工程师及其经理发送电子邮件`。
6. 在“收件人”字段中，输入：`service.engineer@company.com`。
7. 在“抄送”字段中，输入：`service.manager@company.com`。
8. 在主题行中，输入：`需要服务`。
9. 选择在前面附加“{{site.data.keyword.iotrtinsights_short}} 警报”以阐明电子邮件来源。
10. 要在电子邮件中包含设备数据，请清除**不在电子邮件中包含设备数据**复选框。
11. 单击**确定**以保存操作。  




## 使用 Webhook 在 Slack 上进行发布{: #webhookex}

在此示例中，该操作配置为使用 Webhook 将消息发布到我们的 #service-requests Slack 通道。

要创建“发布到 Slack”操作，请执行以下步骤：
1. 在 Slack 中，为通道 #service-requests 设置“入局 Webhook 集成”。记下 Webhook URL。有关更多信息，请参阅 [Slack 文档](https://api.slack.com/incoming-webhooks)。
2. 在 Real-Time Insights 中，转至**分析 > 操作**，然后创建具有以下参数的新操作：
 - 类型 - **Webhook**
 - 名称 - `在 Slack 上发布服务请求`
 - URL - `您的 Slack Webhook URL`
 - 方法 - **POST**
 - 内容类型 - application/json
 - 选择**使用定制消息体**
 - 主体
```{"text":"*有设备需要您的关注*\n 时间：{{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} 实例：{{tenantId}}\n 设备：{{deviceId}}\n 规则：{{ruleName}}\n 描述：{{ruleDescription}}\n 条件：{{ruleCondition}}\n 原始设备消息：\n{{message}}"}```
 {: codeblock}  
 **重要信息：**Slack Webhook 必须至少包含“text”字段。有关信息，请参阅 Slack 文档中的 [入局 Webhook](https://api.slack.com/incoming-webhooks "Slack 文档 ")。
11. 单击**确定**以保存操作。

## 使用 Node-RED 发送短信{: #noderedex}

在此示例中，该操作配置为将 Node-RED 用于 Twilio 节点，以向服务工程师发送短信。

要创建“发送短信”操作，请执行以下步骤：
1. 在 Twilio 中，找到消息传递服务或创建新的消息传递服务，以用于从 Twilio 帐户发送短信。有关更多信息，请参阅 [Twilio 文档](https://www.twilio.com/help)。
1. 在 Bluemix 中，使用 Node-RED URL (`http://mynodered.mybluemix.net/red/`) 来设置并访问 Node-RED 帐户。有关更多信息，请参阅 Bluemix 文档中的[使用 Node-RED 入门模板创建应用程序](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html)主题。
2. 在 Node-RED 中，创建简单的双节点流，例如 [RTI-alert]->[SMS]。
其中，第一个节点是 http 节点，第二个节点是 twilio 节点。
 1. 添加“http”输入节点，然后使用以下属性对其进行配置：
  <ul>
  <li>方法 - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>名称 - RTI 操作</li>
  </ul>
  2. 添加“http 响应”输出节点，然后将其与“http”输入节点连接在一起，方法是将其中一个节点的输出端口拖到另一个节点的输入端口。
  3. 添加“twilio”输出节点，然后使用以下属性对其进行配置：
  <ul>
  <li>服务 - **外部服务**</li>
  <li>Twilio - 添加新的 twilio-api</li>
  <li>SMS 接收方 - `服务工程师的电话号码`</li>
  <li>名称 - **SMS**</li>
  </ul>
  4. 将这些节点连线在一起
  将 http 节点与 twilio 节点连接在一起，方法是将其中一个节点的输出端口拖到另一个节点的输入端口。
  5. 单击**部署**按钮以将流部署到服务器
3. 在 {{site.data.keyword.iotrtinsights_short}} 中，转至**分析 > 操作**，然后创建具有以下参数的操作：
 - 类型 - **Node-RED**
 - 名称 - `使用 Node-RED 和 Twilio 发送短信`
 - 描述 - `向服务工程师发送短信警报。`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - 主体
 ```{"text":"*有设备需要您的关注*\n 时间：{{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} 实例：{{tenantId}}\n 设备：{{deviceId}}\n 规则：{{ruleName}}\n 描述：{{ruleDescription}}\n 条件：{{ruleCondition}}\n 原始设备消息：\n{{message}}"}```
 {: codeblock}
4. 单击**确定**以保存操作。

## 使用 IFTTT 发布 Trello 卡{: #iftttex}

在此示例中，我们配置的操作是使用 IFTTT 将卡发布到 Trello 上的服务请求列表。

要创建“在 Trello 上发布卡”操作，请执行以下步骤：
1.	在 IFTTT 中，连接到 Trello 通道。
2.	在 IFTTT 中，连接到 Maker 通道。记下您的 IFTTT 密钥。从 Real-Time Insights 连接到 IFTTT 时需要此密钥。
5.	在 IFTTT 中，创建配方：
 1. 单击 **THIS**。
 2. 选择 **Maker** 通道。  
 2. 单击**接收 Web 请求**。
 3. 输入事件名称 `post-Trello-card`。
 4. 单击 **THAT**。
 5. 选择 **Trello** 通道。
 6. 选择要在其中创建卡的 Trello 板。
 7. 输入要在其中添加卡的列表的名称。
 8. 编辑标题和描述。
 9. 指定 @service.engineer 和 @service.manager 成员。
 8. 单击**创建操作**。   
3. 在 {{site.data.keyword.iotrtinsights_short}} 中，转至**分析 > 操作**，然后创建具有以下参数的操作：
<ul>
<li>类型 - **IFTTT**</li>
<li>名称 - `发布服务请求卡`</li>
<li>描述 - `使用 IFTTT 在 Trello 中发布服务请求列表中的卡。`</li>
<li>密钥 - 您的 IFTTT 密钥</li>
<li>事件 - `post-Trello-card`</li>
<li>（可选）为值 1 到 3 添加值。**提示：**您可以使用[变量替换](actions.html#variable_substitution)来动态包含设备数据。</li>
</ul>
4. 单击**确定**以保存操作。
