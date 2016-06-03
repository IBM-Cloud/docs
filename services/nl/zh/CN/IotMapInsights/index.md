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
{: #gettingstartedtemplate}
*上次更新时间：2016 年 5 月 13 日*

{{site.data.keyword.iotmapinsights_full}} 使开发者能够轻松允许其应用程序使用地理空间功能，例如，基于全球道路网络的地图匹配和最短路径搜索。
{:shortdesc}

可以通过 {{site.data.keyword.iotmapinsights_short}} REST API 使用以下功能：

- 使用道路网络几何图形的准确度高的地图匹配。
- 处理地图上的实时事件，例如交通。
- 考虑到实时事件的动态最短路径搜索（路线搜索），例如交通。
- 检索道路几何图形数据，可以用于在地图上绘制道路形状。

{{site.data.keyword.iotmapinsights_short}} 服务使用从 OpenStreetMap 抽取的道路网络数据（以 WGS84 坐标的形式）。只有车辆可通行的道路才用于分析。

受支持的地图区域如下所示：

- 欧洲 (map_id=1)
- 非洲 (map_id=2)
- 亚洲 (map_id=3)
- 澳大利亚/大洋洲 (map_id=4)
- 北美洲 (map_id=5)
- 中美洲 (map_id=6)
- 南美洲 (map_id=7)


遵循以下步骤来使用 {{site.data.keyword.iotmapinsights_short}} 服务的分析功能。

## 使用 {{site.data.keyword.iotmapinsights_short}} 进行地图匹配

1. 准备一组要进行分析的原始 GPS 坐标数据。
2. 通过使用 `mapMatching` REST API，将以时间序列排序的原始 GPS 坐标数据发送到 {{site.data.keyword.iotmapinsights_short}} 服务。或者，设置每个位置的方位角（以角度表示，北为 0，顺时针角），以指定通行的方向。
3. 接收响应 `mapMatching` REST API 调用的地图匹配的坐标和道路连接信息。
4. 或者，使用 `getLinkInformation` REST API 来检索地图匹配的道路连接的道路形状数据。使用连接标识调用 `getLinkInformation` REST API，以获取包含道路形状的一系列坐标。

## 使用 {{site.data.keyword.iotmapinsights_short}} 进行路线搜索

1. 确定要获取最短路径的起始位置和终止位置。
2. 使用 `routeSearch` REST API，将起始坐标和终止坐标发送到 {{site.data.keyword.iotmapinsights_short}} 服务。或者，设置每个位置的方位角（以角度表示，北为 0，顺时针角），以指定通行的方向。
3. 接收响应 `routeSearch` REST API 调用的道路连接列表。可以使用结果数据中包含的形状数据，在地图上绘制找到的路径的形状。

## 使用 {{site.data.keyword.iotmapinsights_short}} 处理交通事件

1. 确定要创建的交通事件的类型和位置。
2. 使用 `createEvent` REST API，将交通事件信息发送到 {{site.data.keyword.iotmapinsights_short}} 服务。
3. 接收响应 `createEvent` REST API 调用的已创建交通事件的事件标识。
4. 使用 `queryEvent` REST API，在特定矩形区域内搜索交通事件，或者搜索特定交通事件类型的交通事件。

- 或者，使用 `deleteEvent` REST API 除去不再有效的交通事件。
- 或者，使用 `getAffectedLinksInformation` REST API 检索道路上受交通事件影响的区域。


# 相关链接
{: #rellinks}
## 教程和样本
{: #samples}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 教程第 1 部分](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} 教程第 2 部分](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

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

