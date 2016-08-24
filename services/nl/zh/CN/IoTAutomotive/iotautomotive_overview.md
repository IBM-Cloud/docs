---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# 关于 {{site.data.keyword.iot4auto_short}} (Beta)
{: #iotautomotive_overview}

上次更新时间：2016 年 7 月 29 日
{: .last-updated}

{{site.data.keyword.iot4auto_full}} 是 {{site.data.keyword.Bluemix_notm}} 上的一种服务，您可以使用它来查看和分析来自车辆的大数据。

使用 {{site.data.keyword.iot4auto_short}} 服务，您可以收集和处理来自车辆的大量数据。{{site.data.keyword.iot4auto_short}} 的分析功能非常强大，可帮助您深入了解司机行为、车辆位置以及其他感兴趣的汽车相关活动和事件，并据此采取可行的措施。
{:shortdesc}

## 体系结构
{: #architecture}
{{site.data.keyword.iot4auto_short}} 是一个基础的实时基础架构平台，适用于汽车应用程序和连接的车辆设备。该服务还可支持未来的新兴自主驾驶功能。

![{{site.data.keyword.iot4auto_full}} 体系结构](images/architecture_iotautomotive.png "{{site.data.keyword.iot4auto_full}} 体系结构")

{{site.data.keyword.iot4auto_short}} 服务包含以下 {{site.data.keyword.Bluemix_notm}} 服务，这些服务也在 {{site.data.keyword.Bluemix_notm}} 目录中单独提供：

|服务|描述|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html)| 该服务可分析司机行为，并根据从所连接车辆检索到的汽车探测和上下文数据来识别行程的轨迹模式。
|[Context Mapping](../IotMapInsights/index.html)| 该服务提供地理空间功能，例如基于道路网络的地图匹配和最短路径搜索。
*表 1. {{site.data.keyword.iot4auto_short}} 服务*

## 功能
{: #features}

{{site.data.keyword.iot4auto_short}} 为提供汽车探测数据（来自连接的车辆设备）的解决方案提供以下功能支持：

### 从 {{site.data.keyword.iot4auto_short}} 设备检索数据

- 支持以下协议和数据模型：
   - TPEG
   - ITS
   - ISO 汽车标准
- 支持其他非车辆设备和传感器

### 数据规范化和存储

- 识别和过滤异常数据
- 将数据映射、转换和格式化为标准数据模型，以供分析
- 根据应用程序或服务的数量、等待时间和使用情况，将数据放入以下某个数据存储中：
   -  Hadoop 数据存储（用于大数据分析）
   -  代理程序数据存储（用于实时分析）

### 基于地理空间图的服务

- 实时地图匹配
- 事件服务
- 从车辆和外部源动态注入事件
- 基于连接或节点的拓扑相关搜索
- 集成了天气数据的周边地图支持

### 高可扩展性且等待时间短的实时分析平台

- 基于代理程序的技术
- 个性化的分析
- 基于规则的灵活分析

### 移动对象图分析 (MOMA)

- 使用来自车辆的数据进行批量（大数据）分析
- 司机行为分析
- 司机概要分析
- 轨迹模式分析

### 数据提供程序服务

- 适用于第三方应用程序和服务的 API

### 与资产管理集成

- 车辆资产管理系统

## REST API
{: #api}

[{{site.data.keyword.iot4auto_short}} API](http://ibm.biz/IoT4Automotive_APIdoc) 提供的命令可帮助您进一步开发 {{site.data.keyword.iot4auto_short}} 来满足您的需求。

使用可用的 REST API 命令，您可以定制您的 {{site.data.keyword.iot4auto_short}} 服务实例：

- 将特定事件注入系统中
- 将来自车辆的规范化汽车探测数据存储在首选的分析数据存储中
- 实时检索感兴趣的事件以及车辆的地理位置

### REST API 命令

|目标 |API 命令 |描述 |
|:---|:---|:---|
|注入事件|`sendEvent`|将交通或其他事件发送给平台。|
|发送汽车探测数据|`sendCarProbe`|发送来自车辆的基于位置的传感器数据，并根据实时分析的结果，为车辆检索受影响的事件。|
|创建车辆数据|`createVehicle`|将一条车辆记录创建为资产。此信息用于认证和库存管理等用途。|
|映射 API|不适用|有关更多信息，请参阅 [Contextual Map 服务 API](http://ibm.biz/IoTContextMapping_APIdoc)。|
|分析 API|不适用|有关更多信息，请参阅 [Driver Behavior 服务 API]( http://ibm.biz/IoTDriverBehavior_APIdoc)。|
|获取汽车探测数据|`getCarProbe`|获取 `sendCarProbe` API 命令所发送的车辆的最新汽车探测数据。|
|获取地图事件|`getEvent` |获取 `sendEvent` API 命令所发送的地图上的事件。|
|获取车辆资产数据|`getVehicle`| 从 `createVehicle` API 命令获取车辆数据，作为资产。|
*表 2. {{site.data.keyword.iot4auto_short}} REST API 命令*
