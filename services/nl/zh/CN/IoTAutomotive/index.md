---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot4auto_short}} (Beta) 入门
{: #getting_started_iotautomotive}

上次更新时间：2016 年 7 月 29 日
{: .last-updated}

{{site.data.keyword.iot4auto_full}} 是一种 {{site.data.keyword.Bluemix_notm}} 服务，您可以使用它来检索、管理和分析来自所连接车辆的大数据。{{site.data.keyword.iot4auto_short}} 的分析功能非常强大，可帮助您深入了解驾驶行为、车辆位置以及其他感兴趣的汽车相关活动和事件，并据此采取可行的措施。

{:shortdesc}

使用 {{site.data.keyword.iot4auto_short}}，您可以执行以下任务：

- 将汽车探测数据和规范化数据发送到数据存储中，以供分析
- 将事件注入上下文映射中，并检索对特定车辆有影响的事件
- 从汽车探测数据中识别新事件
- 检索有关所连接车辆的信息
- 为司机、车辆、事件规则、事件类型和供应商管理资产数据


{{site.data.keyword.iot4auto_short}} 服务包含以下 {{site.data.keyword.Bluemix_notm}} 服务，这些服务也在 {{site.data.keyword.Bluemix_notm}} 目录中单独提供：

|服务|描述|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html){:new_window}| 该服务可分析司机行为，并根据从所连接车辆检索到的汽车探测和上下文数据来识别行程的轨迹模式。
|[Context Mapping](../IotMapInsights/index.html){:new_window}| 该服务提供地理空间功能，例如基于道路网络的地图匹配和最短路径搜索。
*表 1. {{site.data.keyword.iot4auto_short}}* 的服务

在开始将您的汽车设备和应用程序与该服务进行集成之前，请确保已完成以下步骤：

1. 查看[关于 {{site.data.keyword.iot4auto_short}}](iotautomotive_overview.html) 主题，以熟悉和了解该服务所提供和支持的功能和分析能力。
2. 从 [{{site.data.keyword.Bluemix_notm}} 目录](https://console.ng.bluemix.net/catalog/labs/){:new_window}添加服务实例时，确保该实例未绑定到应用程序，并务必记下自动生成的租户标识、用户名和密码值。在后面通过 {{site.data.keyword.iot4auto_short}} API 访问该服务时会用到这些值。
3. 使用仪表板上的控制台，为您的 {{site.data.keyword.iot4auto_short}} 配置端口、目标主机名以及其他设置。有关更多信息，请参阅[管理](iotautomotive_admin.html)。

您可以使用 {{site.data.keyword.iot4auto_short}} REST API 命令将您的汽车设备和应用程序与此服务进行集成。

要快速入门并熟悉运用，请完成以下步骤：

1. 注入事件，方法是使用 `sendEvent` API 请求命令来发送要分析的事件。
  - 请求：事件数据（含位置）
2. 确认所存储的事件数据含有地图匹配信息，方法是使用 `getEvent` API 请求命令来检索事件。
  - 请求：区域数据（起点或终点的经度和纬度）
  - 响应：事件数据（含道路连接标识）
3.  使用 `sendCarProbe` API 请求命令来发送要分析的汽车探测数据。
  - 请求：汽车探测数据（含位置）
4. 确认所存储的汽车探测数据含有地图匹配信息，方法是使用 `getCarProbe` API 请求命令来检索数据。
  - 请求：区域数据（起点或终点的经度和纬度）
  - 响应：汽车探测数据（含道路连接标识）
5. 分析司机数据。有关更多信息，请参阅 [Driver Behavior](../IotDriverInsights/index.html){:new_window}。

# 相关链接
{: #rellinks}

## API 参考
{: #api}
* [{{site.data.keyword.iot4auto_short}} API 文档](http://ibm.biz/IoT4Automotive_APIdoc){:new_window}
* [Context Map 服务 API](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}
* [Driver Behavior 服务 API]( http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}


## 相关链接
{: #general}
* [{{site.data.keyword.iotdriverinsights_short}} 入门](../IotDriverInsights/index.html){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} 入门](../IotMapInsights/index.html){:new_window}
* [{{site.data.keyword.iot_full}} 入门](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Bluemix 服务中的新增功能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [IBM developerWorks 上的 dW Answers](https://developer.ibm.com/answers/topics/iot-for-automotive){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-for-automotive){:new_window}
