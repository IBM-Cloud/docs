---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.iotmapinsights_short}} 入门
{: #iotdriverinsights_index}
上次更新时间：2016 年 6 月 22 日
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} 是 {{site.data.keyword.Bluemix}} 上的一种服务，您可以使用它将地理空间功能用于您的应用程序，例如基于全球道路网络的地图匹配和最短路径搜索。  
{:shortdesc}

可以通过 {{site.data.keyword.iotmapinsights_short}} REST API 使用以下功能：

|功能|用于...|
|:---|:---|
|高度精确的地图匹配|将您的 GPS 位置与映射的实际道路网络进行匹配|
|道路几何数据检索|检索映射的道路网络以在地图上绘制道路形状|
|动态最短路径搜索|搜索最短路线（包含交通等实时事件）|
|实时交通事件操作|添加实时地图匹配的事件（例如交通状况）来改善路线规划结果|

## 开始之前
{: #byb}

1. 从 [{{site.data.keyword.Bluemix_notm}} 目录](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}添加服务实例时，确保该实例未绑定到应用程序，并务必记下自动生成的租户标识、用户名和密码值。在后面通过 {{site.data.keyword.iotmapinsights_short}} API 访问该服务时会用到这些值。

2. 熟悉和了解 [OpenStreetMap](http://www.openstreetmap.org/){: new_window}。  

 {{site.data.keyword.iotmapinsights_short}} 服务使用从 [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 抽取的道路网络数据（以 WGS84 坐标的形式）。只有车辆可通行的道路才能用于分析。  

 支持以下地图区域：

|区域|地图标识|
|:---|:---|
|欧洲|map_id=1|
|非洲|map_id=2|
|亚洲|map_id=3|
|澳大利亚/大洋洲|map_id=4|
|北美洲|map_id=5|
|中美洲|map_id=6|
|南美洲|map_id=7|

## 地图匹配
{: #map_matching}
要将原始 GPS 坐标与地图匹配的坐标进行映射，请完成以下步骤：

1. 准备一组要分析的原始 GPS 坐标。
2. 使用 `mapMatching` API 命令来发送原始 GPS 坐标。或者，设置每个位置的方位角（以角度表示），以指定通行的方向。
 - 请求：原始 GPS 数据
 - 响应：地图匹配的 GPS 数据，连接标识
3. 可选：使用 `getLinkInformation` API 命令来获取道路类型数据。您可以使用 `getLinkInformation` REST API 将匹配的道路形状数据检索为一系列坐标。
 - 请求：连接标识
 - 响应：道路类型

## 路线搜索
{: #route_searching}

使用以下步骤来查找所指定源和目标坐标之间的最短路径信息：

1. 确定最短路径的起始位置和终止位置。
2. 使用 `routeSearch` REST API 来发送起始坐标和终止坐标。或者，设置每个位置的方位角（以角度表示），以指定通行的方向。
 - 请求：源和目标坐标
 - 响应：地图匹配的最短路线

使用返回的连接形状数据，在地图上绘制所找到路径的形状。

## 添加交通事件
{: #traffic_events}

要将交通事件信息添加到 {{site.data.keyword.iotmapinsights_short}} 服务中，请完成以下步骤：

1. 选择要创建的交通事件的类型和位置。
2. 使用 `createEvent` API 命令来注入事件。将交通事件信息发送到 {{site.data.keyword.iotmapinsights_short}} 服务中。
 - 请求：事件信息
 - 响应：事件标识
3. 使用 `queryEvent` REST API 命令来查找事件。搜索特定矩形区域内的交通事件，或者搜索特定交通事件类型的交通事件。
 - 请求：区域信息。
 - 响应：事件信息。  
4. 可选：使用 `deleteEvent` API 命令来除去不再有效的交通事件。
5. 可选：使用 `getAffectedLinksInformation` API 命令来检索道路上受交通事件影响的区域。

# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 教程第 1 部分](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 教程第 2 部分](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive Starter 应用程序](https://iot-automotive-starter.mybluemix.net){:new_window}

## API 参考
{: #api}

* [API 文档](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## 相关链接
{: #general}

* [{{site.data.keyword.iotdriverinsights_short}} 入门](../IotDriverInsights/index.html){:new_window}
* [{{site.data.keyword.iot_full}} 入门](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [IBM developerWorks 上的 dW Answers](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [Bluemix 服务中的新增功能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}
* [&copy; OpenStreetMap 贡献者](http://www.openstreetmap.org/copyright){:new_window}
* [开放数据共享开放数据库许可协议 (ODbL)](http://opendatacommons.org/licenses/odbl/){:new_window}
