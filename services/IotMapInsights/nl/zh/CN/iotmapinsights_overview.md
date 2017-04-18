---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 关于 {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}
上次更新时间：2016 年 7 月 20 日
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} 是 {{site.data.keyword.Bluemix_notm}} 上的一种服务，您可以使用它来快速访问静态道路网络数据和动态事件数据。{{site.data.keyword.iotmapinsights_short}} 还提供了适用于道路网络的地理空间工具，您可以使用它们将地理空间功能与您的应用程序进行集成。
{:shortdesc}

{{site.data.keyword.iotmapinsights_short}} 服务提供以下功能：

- 静态地图数据
- 动态事件数据
- 地理空间工具

{{site.data.keyword.iotmapinsights_short}} 服务会收集和使用服务内存高速缓存中存储的 [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 道路网络数据来进行处理。

OpenStreetMap 是开放数据，由 OpenStreetMap 基金会 (OSMF) 采用开放数据共享开放数据库许可协议 (ODbL) 授权。有关更多信息，请参阅 [OpenStreetMap 著作权与许可](http://www.openstreetmap.org/copyright){: new_window}。

## 静态地图数据
{: #static_map_data_query}

该产品的主要功能之一是可检索详细的道路信息以用于您的应用程序。使用“连接查询”REST API 界面可按连接标识来查询静态地图道路属性数据。使用 {{site.data.keyword.iotmapinsights_short}} 的[地图匹配功能](#map_matching)可识别所需的连接标识参数。

返回的数据包含有关所请求连接标识的以下信息：

- 道路类型
- 道路长度
- 详细形状点数组
- 有关相邻节点和相邻连接的信息

使用查询到的详细道路连接信息，您的应用程序可以通过智能地使用返回的相邻连接信息来遍历道路连接网络。

## 动态事件数据
{: #dynamic_event_data}

除了静态地图数据之外，实际的道路状况必定还会包括交通拥堵和道路施工等动态事件。使用 {{site.data.keyword.iotmapinsights_short}} 可创建和管理交通事件，并将交通事件与[受影响的连接搜索](#link_search)结合起来，从而合理规划路线。

### 注入和删除事件
{: #inject_event}

使用 {{site.data.keyword.iotmapinsights_short}} 服务事件注入 REST API 可通过放置在特定道路连接上的地图对象模型形式动态注入和除去交通事件。每个事件都包含一些基本属性，例如 GPS 坐标、开始时间、事件类型、事件持续时间以及受影响的道路长度。

使用事件删除 REST API 界面可从地图中除去过时的事件。

### 事件查询
{: #query_event}

使用事件查询 REST API 可获取有关特定地理区域中所有动态事件的详细信息。您可以按区域（含经度和纬度范围）进行查询，还可以包含事件属性，以减少返回的目标事件数。

## 地理空间工具
{: #geospatial_tools}

使用 {{site.data.keyword.iotmapinsights_short}} 地理空间工具所提供的地图匹配和路线搜索功能来增强您的应用程序。

### 地图匹配
{: #map_matching}

将地图匹配 REST API 界面与您的应用程序配合使用，可将实际的设备 GPS 坐标与 [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 道路网络数据进行映射，从而提高位置准确性，减少不正确的 GPS 数据。您还可以根据位置接收有关道路属性的信息。地图匹配 REST API 使您的应用程序能够将原始 GPS 数据点安置到道路连接上的匹配点。

地图匹配 REST API 界面接收某一点的经度和纬度 GPS 坐标数据，并返回地图匹配的点。通过考虑特定时间段内每台车辆的历史数据来分析地图匹配的点，以实时查找最可能的点。对于没有历史位置数据的点，地图匹配界面会返回道路连接上距离所请求的 GPS 点最近的点。

### 路线搜索
{: #route_search}

集成了地理空间功能的应用程序的基本功能之一是可查找两个点之间的最短路径。  

{{site.data.keyword.iotmapinsights_short}} 服务的路线搜索 REST API 界面会计算起始点和终止点 GPS 坐标之间的最短路径。使用地图匹配功能，使接收到的坐标与地图的最近连接相匹配，并计算这些地图匹配的点之间的最短路径。

### 受影响的连接搜索
{: #link_search}

道路上发生事件时，该事件可能会影响各种道路连接。您可以使用 REST API 来搜索受影响的连接，还可以查找车辆可能到达该事件的道路连接。搜索会将道路连接网络的拓扑考虑在内，而不仅仅是从车辆到事件的距离。
