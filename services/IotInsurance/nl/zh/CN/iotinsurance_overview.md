---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}


# 关于 {{site.data.keyword.iotinsurance_short}}
{: #about_servicename}
上次更新时间：2016 年 9 月 15 日
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} 是集成的 IoT 生产实例，该实例收集和分析保单持有者的全部上下文数据以提供个性化的风险评估、实时保护并降低保单成本。
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} 提供保单持有者资产和情况的全部上下文视图，包括的信息有位置、天气、交通和整体运行状况。对此信息进行深度分析可使承保人能够为保单持有者提供个性化风险评估和实时保护。对保单持有者的益处包括通过早期警报避免风险，提供个性化建议和简化理赔流程和结算。对承包人的益处包括客户满意度、客户忠诚，以及通过避免理赔和自动化结算来降低费用。

## 过程流
{: #processFlow}
保险提供者在 {{site.data.keyword.Bluemix_notm}} 服务代理程序中有一个实例。承保人的客户在家中具有传感器，可连接到传感器提供者的云。房主从移动设备授权 {{site.data.keyword.iotinsurance_short}} 服务接收来自 {{site.data.keyword.iotinsurance_short}} 的传感器数据。{{site.data.keyword.iotinsurance_short}} 服务连接到传感器提供者的云，为每个用户拉取数据并将其发送给 IoT 服务器。如果传感器显示客户家中可提供在承保
人保障中指定的参数，那么将向承保人仪表板和客户设备发送通知。

## 组件
{: #components}

### 保险仪表板
{: #insurance_dashboard}
保险仪表板向保险公司用户（例如，代理）提供客户承保资产现状的完整视图。他们可以看到国家或地区、省/直辖市/自治区或帐户级别的保障和事件。

样本保险仪表板装入了模拟数据，以显示您可以收集和分析的信息类型的示例。

### 移动 Starter 应用程序
{: #mobileapp}
保单持有者（例如，房主）使用移动 Starter 应用程序查看和响应 {{site.data.keyword.iotinsurance_short}} 从其家中的传感器发送的信息。

使用移动设备，房主授权服务连接到传感器提供者的云中，以发送和接收数据。例如，当传感器检测到漏水时，房主可在移动 Starter 应用程序中接收到通知。有关更多信息，请参阅[安装和连接移动 Starter 应用程序](iotinsurance_mobile_app.html)。

### REST API
{: #rest_api}
移动 Starter 应用程序、保险仪表板、保障引擎和危险控制器使用 REST API。通过 REST API，用户可以得知设备与保障和操作之间的关联。使用此 API，程序员可以创建新用户，生成事件数据，创建和注册新保障，以及访存事件数据。

您从服务控制台访问的 API 是为您的 {{site.data.keyword.iotinsurance_short}} 实例定制的。

在 API 页面，您可以  
  - 查看所有可用的 API 调用和关联的文档。
  - 尝试使用各个 API 调用。选择 API 调用以显示所有信息，然后单击**试试看！**。

API 示例可用于帮助您初步使用常见的方案。有关更多信息，请参阅 [{{site.data.keyword.iotinsurance_short}} API 示例](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)。

### 云提供者
{: #cloudprovider}
用户必须授权 Transformer 组件访问传感器云数据和处理记录的数据。授权通过移动 Starter 应用程序完成。Wink 是目前支持的唯一一家云供应商。

### Transformer
{: #transformer}
Transformer 向云服务器 API 请求新信息，并转换信息以匹配 {{site.data.keyword.iotinsurance_short}} 中的数据。然后，发布数据以供后面的 {{site.data.keyword.iotinsurance_short}} 实施使用。

### 分析引擎
{: #analytics_engine}
分析引擎根据事件中存储的信息，确定是否存在漏水等危险。如果发现危险，数据将传递给危险控制器。操作引擎查看数据库中的数据以根据保障中指定的信息确定要采取的操作。

您可以使用 {{site.data.keyword.iotinsurance_short}} API 在 JavaScript 中创建新保障。

### 保障
{: #shields}
保障是客户从保险提供者获取的特定保护。例如，房主对房屋购买保险，以保障火灾、浸水、抢劫和其他危险对房屋带来的损失。{{site.data.keyword.iotinsurance_short}} 解决方案提供内置的水灾保障。当与水相关的事件危及他们的房屋时，将向客户发出警报，客户可以进行响应。使用 REST API，开发人员可以添加更多保障。
保障在 {{site.data.keyword.iotinsurance_short}} 分析引擎中运行。分析引擎识别危险类型（例如，*检测到水灾*）、发送危险的传感器的用户帐户以及与帐户相关的保障。可以根据该信息采取操作。
