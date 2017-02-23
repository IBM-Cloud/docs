---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-16"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 云分析
{: #cloud_analytics}

通过使用 {{site.data.keyword.iot_short}} 云分析，可指定基于实时设备数据并且在满足条件时将触发警报和可选操作的规则条件。    
{: shortdesc}

例如，可以创建一条规则，用于确保在设备中断或设备温度达到峰值时，向用户设备上的仪表板发送警报，并向管理员发送电子邮件。

## 开始之前
{: #byb}
确保要用作规则中条件的设备属性已映射到模式。请参阅[连接设备](iotplatform_task.html)和[创建模式](im_schemas.html)以获取更多信息。

此外，请查看 [Using Rules and Actions with {{site.data.keyword.iot_short}} Cloud Analytics](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/) 诀窍，以了解 Cloud Analytics 中使用的规则和操作。

## 管理规则和操作  
{: #managing_rules}

使用**规则**仪表板可为组织创建和管理规则与操作。

要获取有关已对设备触发的规则和警报的概述，请使用以下板：

 |板名称 | 描述 |  
 |:---|:---|  
  |以规则为中心的分析 | 显示组织的规则。其他卡会列出已触发的警报、关联的设备、设备属性和警报信息。 |  
 |以设备为中心的分析 | 显示连接到组织的设备。其他卡会显示所选设备的警报、所选设备的信息、设备属性和警报信息。 |

 有关缺省分析板的更多信息，请参阅[使用板和卡可视化实时数据](data_visualization.html#default_boards)。


## 创建规则
{: #rules}

规则是基于条件的决策点，用于使实时设备数据与预定义的阈值或其他属性数据相匹配，以在满足条件时触发警报。除了在 {{site.data.keyword.iot_short}} 仪表板中显示的警报外，还可以添加一个或多个操作，用于在触发规则时运行业务逻辑。

**重要信息：**必须为设备类型创建模式后，才能为该设备类型创建规则。有关信息，请参阅[创建设备类型模式](im_schemas.html)。

要创建规则，请执行以下操作：
1. 在 {{site.data.keyword.iot_short}} 仪表板中，转至**规则**。
2. 单击**创建规则**，为规则命名，提供描述，选择要应用规则的设备类型，然后单击**下一步**。  
3. 要设置规则逻辑，请添加一个或多个 IF 条件以用作规则的触发器。  
可以通过并列行的方式添加条件以将其应用为 OR 条件，也可以通过顺序列的方式添加条件以将其应用为 AND 条件。
  
**重要信息：**要触发用于比较两个属性的条件，或者触发使用 AND 以顺序方式组合的两个或更多属性条件，触发数据点必须包含在同一设备消息中。如果数据是在多个消息中收到的，那么不会触发该条件或这些顺序条件。
  
**示例：**  
如果参数值大于指定值，那么可使用简单规则来触发警报：
条件 = `temp_cpu>80`  
如果满足阈值组合条件，那么可使用更复杂的规则来触发警报：
条件 = `temp_cpu>60 AND cpu_load>90`   

4. 为规则配置有条件触发需求。
  
要控制一段时间内为某个规则触发的警报数，可以为该规则配置有条件触发需求。
  
**重要信息：**有条件触发将作用于该规则中的任何条件。例如，如果某个规则使用 OR 设置了 5 个不同的并行条件，那么每个为 true 的条件都会计入有条件触发器计数。要为规则设置有条件触发，请执行以下操作：
 1. 在规则编辑器中，单击缺省的**每次满足条件时触发**链接，以打开“设置频率需求”对话框。
 2. 选择并配置要在规则中使用的有条件触发器。
 <ul>
 <li>每次满足条件时触发</li>
 <li>在 M *时间单位*内条件满足 N 次时触发</li>
 </ul>  
有关有条件触发器的更详细描述，请参阅[有条件规则触发](#conditional "有条件触发概述")。
5. 创建或选择在满足规则条件时执行的一个或多个操作。
  
有关操作的更多信息，请参阅[使用规则创建操作](#shared "创建操作")。   
例如：操作可以是发送电子邮件或发布 Webhook。
3. **可选**：为规则选择警报优先级。  
优先级用于对**基于规则的分析**板中显示的警报分类。缺省优先级为“低”。
6. 对规则满意后，单击**保存**以保存而不激活规则，或者单击**激活**以保存并激活规则。

您的规则已创建。如果激活规则，那么满足该规则的条件时，将向**板 > 基于规则的分析**板添加警报，并运行任何规则操作。

## 有条件规则触发
{: #conditional}

要控制一段时间内为某个规则触发的警报数，可以为该规则配置有条件触发需求。


根据消息频率和规则条件，一旦满足触发条件，规则可能会触发许多次。例如，如果条件为 `temp >= 90`，并且温度上升并稳定在 91，那么针对每条入局消息都会触发该规则。根据设备消息的频率以及规则设置为运行的操作，这种警报量可能会迅速填满您的电子邮件收件箱，或者使 Twitter 订阅源收到海量消息，而这些消息并没有提供任何额外的价值。

**重要信息：**有条件触发将作用于该规则中的任何条件。例如，如果某个规则使用 OR 设置了 5 个不同的并行条件，那么满足的每个条件都会计入有条件触发器计数。

条件 | 描述
------------- | -------------
每次满足条件时触发 | 每次满足规则条件时，就触发规则。
在 *M* *天/小时/分钟/定制*内条件满足 *N* 次时触发 | 在所选时间间隔内，条件满足 *N* 次时触发规则，然后在所配置的时间段之后才有可能再次触发规则。</br>示例：有条件触发需求 =`在 30 分钟内条件满足 4 次时只触发一次`。设备每 5 分钟发送一条新消息。在中午，温度初次超过 90 度，这满足了条件。有条件触发器计数器会启动，但还不会触发规则。在 15 分钟后，又收到三条消息指示 `temp > 90` 时，会触发规则。在接下来的 15 分钟内，不管温度高低，都不会再触发规则。
仅当第一次满足条件时触发，并在不再满足条件时重置。 | 条件第一次满足时，会触发规则，但对于也满足条件的后续消息，不会触发规则。触发条件会由不满足规则条件的第一条消息重置。
在 *M* *天/小时/分钟/定制*内条件持久存在时触发。 | 在所选时间间隔内收到的所有数据点都满足条件或者没有再收到其他数据点时，经过此时间间隔后会触发规则。时间间隔的起始时间为初次满足条件的时间。



## 在规则中使用操作
{: #shared}

除了在“警报”仪表板中显示警报外，{{site.data.keyword.iot_short}} 还支持多种类型的由规则触发的操作，例如发送电子邮件和发布 Webhook。

您可以直接在规则编辑器中创建操作，也可以在“操作”选项卡中创建操作，然后在创建规则时选择这些操作。

要在“操作”选项卡上创建操作，请执行以下操作：
1. 在 {{site.data.keyword.iot_short}} 仪表板中，转至**规则**。
2. 在“规则”仪表板中，选择**操作**选项卡。
2. 单击**创建操作**，为操作命名，提供描述，选择操作类型，然后单击**下一步**。

3. 为要创建的操作类型提供必需参数。
  
操作类型：  
 - [发送电子邮件](#email "发送电子邮件")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [Webhook](#webhook "Webhook")
4. 单击**确定**以创建新操作。

现在，该操作在规则编辑器中可用。

**注：**下面的示例均表示用于在温度（通过设备的 `temp_cpu` 属性表示）超过 80 度时通知服务工程师的操作，使用的是以下规则条件：`temp_cpu >= 80`

### 发送电子邮件  
{: #email}
使用“发送电子邮件”操作可在规则触发时向一个或多个收件人发送电子邮件。

示例：[发送电子邮件](#emailex)。

以下参数用于配置“发送电子邮件”操作：

参数 | 描述
---|---
名称 | 操作的名称，在“警报”仪表板中使用。
描述 | 操作的简短描述。
主题 | 电子邮件的主题行。缺省主题行是“IBM Watson IoT 警报：邮件操作”。
收件人 | 选择是只向您自己发送警报，还是向电子邮件地址的逗号分隔列表发送警报。如果选择向您自己发送警报，那么电子邮件会发送到您用于登录到 {{site.data.keyword.iot_short}} 的电子邮件地址。
抄送 | 无，或电子邮件地址的逗号分隔列表。
在规则触发时，会自动根据设备的消息创建电子邮件正文。  
**重要信息：**缺省情况下，电子邮件不包含可能带有敏感信息的设备数据。更改**包含数据**设置可包含设备数据。

#### 示例：使用“发送电子邮件”
{: #emailex}

在此示例中，操作配置为使用“发送电子邮件”功能，向主要服务工程师发送电子邮件，同时还向其经理发送备份电子邮件。

要创建“发送电子邮件”操作，请执行以下操作：
1. 在 {{site.data.keyword.iot_short}} 仪表板中，转至**规则**。
2. 单击**创建操作**。
4. 输入操作名称：`发送服务请求电子邮件`。
5. 输入描述：`向服务工程师及其经理发送电子邮件`。
3. 选择**电子邮件**类型。
6. 在“收件人”字段中，选择**特定人员**并输入 `service.engineer@company.com`。
7. 在“抄送”字段中，选择**特定人员**并输入：`service.manager@company.com`。
8. 在主题行中，输入：`需要服务。`
10. 选择**包含数据**以在电子邮件中包含设备数据。
11. 单击**完成**以保存操作。  


### IFTTT  
{: #ifttt}

使用 IFTTT 操作可在触发规则时触发 IFTTT 诀窍。有关触发操作作为 IFTTT 诀窍的更多信息，请参阅 IFTTT 站点上的 [Maker Channel](https://ifttt.com/maker)。

示例：[使用 IFTTT 发布 Trello 卡](#iftttex)。

以下参数用于配置 IFTTT 操作：

参数 | 描述
---|---
名称 | 操作的名称，在“警报”仪表板中使用。
描述 | 操作的简短描述。
密钥 | 用于触发事件的 Maker 通道密钥。
事件 | 配置为 Maker 事件触发器的事件的名称。可以创建具有不同触发器的多个诀窍，每个诀窍具有不同的事件名称。
值 1-3 | 可以在这些参数中传递任何内容，这些参数会传递到 IFTTT 诀窍中的操作。**提示：**您可以使用[变量替换](#variable_substitution)在头中动态包含更多数据。

#### 示例：使用 IFTTT 发布 Trello 卡 {: #iftttex}

在此示例中，操作配置为使用 IFTTT 将卡发布到 Trello 上的服务请求列表。

要创建“在 Trello 上发布卡”操作，请执行以下操作：
1.	在 IFTTT 中，连接到 Trello 通道。
2.	在 IFTTT 中，连接到 Maker 通道。记下您的 IFTTT 密钥。从 {{site.data.keyword.iot_short_notm}} 连接到 IFTTT 时需要此密钥。
5.	在 IFTTT 中，创建诀窍：
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
3. 在 {{site.data.keyword.iot_short}} 仪表板中，转至**规则 > 操作**，然后创建具有以下参数的新操作：
<ul>
<li>类型 - **IFTTT**</li>
<li>名称 - `发布服务请求卡`</li>
<li>描述 - `使用 IFTTT 在 Trello 的服务请求列表中发布卡。`</li>
<li>密钥 - 您的 IFTTT 密钥</li>
<li>事件 - `post-Trello-card`</li>
<li>（可选）为“值 1-3”添加值。**提示：**您可以使用[变量替换](#variable_substitution)来动态包含设备数据。</li>
</ul>
4. 单击**确定**以保存操作。


### Node-RED
{: #nodered}

使用 Node-RED 操作可在触发规则时连接到 Node-RED 应用程序。有关使用 Node-RED 的更多信息，请参阅[使用 Internet of Things 入门模板应用程序创建应用程序](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html)。

示例：[使用 Node-RED 发送短信](#noderedex)。

以下参数用于配置 Node-RED 操作：

参数 | 描述
---|---
名称 | 操作的名称，在“警报”仪表板中使用。
描述 | 操作的简短描述。
URL | 目标 Node-RED HTTP 输入节点的 URL。
用户名 | Node-RED 服务需要时包含。
密码 | Node-RED 服务需要时包含。
**重要信息：**密码是以明文形式发送的。
主体 | 缺省情况下，“主体”字段预填充了[变量替换](#variable_substitution)中列出的所有变量。

#### 示例：使用 Node-RED 发送短信
{: #noderedex}

在此示例中，操作配置为将 Node-RED 用于 Twilio 节点，以向服务工程师发送短信。

要创建“发送短信”操作，请执行以下操作：
1. 在 Twilio 中，找到或新建消息传递服务，以用于从 Twilio 帐户发送短信。有关信息，请参阅 [Twilio 文档](https://www.twilio.com/help)。
2. 在 Bluemix 中，使用 Node-RED URL (`http://mynodered.mybluemix.net/red/`) 来设置并访问 Node-RED 帐户。有关更多信息，请参阅 Bluemix 文档中的 [Creating apps with Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) 主题。
3. 在 Node-RED 中，创建简单的双节点流，例如 [RTI-alert]->[SMS]。
  
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
  4. 将节点连线在一起  
  将 http 节点与 twilio 节点连接在一起，方法是将其中一个节点的输出端口拖到另一个节点的输入端口。
  5. 单击**部署**按钮以将流部署到服务器
4. 在 {{site.data.keyword.iot_short}} 仪表板中，转至**规则 > 操作**，然后创建具有以下参数的新操作：
 - 类型 - **Node-RED**
 - 名称 - `使用 Node-RED 和 Twilio 发送短信`
 - 描述 - `向服务工程师发送短信警报。`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - 主体   
 ```json
 {"text":"*某个设备需要您的关注*\n 时间：{{timestamp}}\n {{site.data.keyword.iot_short}} 实例：{{tenantId}}\n 设备：{{deviceId}}\n 规则：{{ruleName}}\n 描述：{{ruleDescription}}\n 条件：{{ruleCondition}}\n 原始设备消息：\n{{message}}"}
 ```  
5. 单击**完成**以保存操作。



### Webhook
{: #webhook}

使用 Webhook 操作可在触发警报时向支持 Webhook 的 Web Service 发起 HTTP 请求。例如，Webhook 可用于在设备中的传感器报告异常读数时提交对资产的服务请求。

示例：[使用 Webhook 在 Slack 上进行发布](#webhookex)。

以下参数用于配置 Webhook 操作：

参数 | 描述
---|---
名称 | 操作的名称，在“警报”仪表板中使用。
描述 | 操作的简短描述。
URL | 支持 Webhook 的目标服务器的 URL。**提示：**您可以使用[变量替换](#variable_substitution)在 URL 中动态包含更多数据。
方法 | 要运行的 Webhook 调用的类型。选择以下某种类型：GET、HEAD、OPTIONS、PATCH、PUT、POST 或 DELETE。
用户名 | Web Service 需要时包含。
密码 | Web Service 需要时包含。
**重要信息：**密码是以明文形式发送的。
头 | 头由键值对构成。**提示：**您可以使用[变量替换](#variable_substitution)在头中动态包含更多数据。
内容类型 | 主体内容的类型：JSON、XML、WWW 表单 URL 编码的内容或纯文本。适用于 OPTIONS、PATCH、PUT、POST 和 DELETE 方法。
主体 | Webhook 调用的主体。适用于 OPTIONS、PATCH、PUT、POST 和 DELETE 方法。缺省情况下，“主体”字段预填充了[变量替换](#variable_substitution)中列出的所有变量。

**重要信息：**Webhook 服务器可能要求主体中包含某些特定字段。例如，Slack Webhook 必须包含“text”字段。   

#### 示例：使用 Webhook 在 Slack 上进行发布
{: #webhookex}

在此示例中，操作配置为使用 Webhook 将消息发布到 #service-requests Slack 通道。

要创建“发布到 Slack”操作，请执行以下操作：
1. 在 Slack 中，为通道 #service-requests 设置“入局 Webhook”集成。记下 Webhook URL。有关更多信息，请参阅 [Slack 文档](https://api.slack.com/incoming-webhooks)。
2. 在 {{site.data.keyword.iot_short}} 仪表板中，转至**规则 > 操作**，然后创建具有以下参数的新操作：
 - 名称 - `Post service request on Slack`
 - 类型 - **Webhook**
 - URL - `您的 Slack Webhook URL`
 - 方法 - **POST**
 - 内容类型 - `application/json`
 - 主体   
 ```json
 {"text":"*某个设备需要您的关注*\n 时间：{{timestamp}}\n {{site.data.keyword.iot_short}} 实例：{{tenantId}}\n 设备：{{deviceId}}\n 规则：{{ruleName}}\n 描述：{{ruleDescription}}\n 条件：{{ruleCondition}}\n 原始设备消息：\n{{message}}"}
 ```  
  **重要信息：**Slack Webhook 必须至少包含“text”字段。有关信息，请参阅 Slack 文档中的[入局 Webhook](https://api.slack.com/incoming-webhooks "Slack 文档")。
11. 单击**完成**以保存操作。


### 变量替换  
{: #variable_substitution}

包含以下变量替换可动态包含设备数据。变量必须用双大括号括起。

变量 | 描述
---|---
**URL、头和主体** |
`{{timestamp}}` | 消息中的时间戳记。
`{{orgId}}` | {{site.data.keyword.iot_short_notm}} 服务的组织标识。
`{{tenantId}}` | 不推荐：{{site.data.keyword.iotrtinsights_full}} 服务的标识。
`{{deviceId}}` | 设备的标识。
`{{ruleName}}` | 包含操作的规则的名称。
`{{ruleID}}` | 包含操作的规则的标识。
**仅限主体** |
`{{ruleDescription}}`| 包含操作的规则的描述。
`{{ruleCondition}}` | 触发了操作的规则条件。
`{{message}}` | 包含触发了规则的数据点值的原始设备消息。
## 关于 Cloud Analytics 的诀窍

以下诀窍描述了如何针对不同的用例来使用 Cloud Analytics 功能：

- [Real Time Data Analysis Using IBM Watson™ IoT Platform Analytics](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/)

- [Predictive Analytics on IOT Sample Data](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/)

- [Device List Card SIMPLIFIES Real Time Device Monitoring on WIoTP Dashboard](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/)

- [Perform Actions in IBM Watson IoT Platform Cloud Analytics](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/)

- [Use IBM Data Science Experience to detect time series anomalies](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/)
