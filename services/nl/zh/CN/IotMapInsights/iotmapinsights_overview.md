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

{{site.data.keyword.iotmapinsights_short}} 服务基于存储在内存高速缓存中的道路网络数据。该服务可高速访问静态道路网络数据、动态事件数据和基于道路网络的地理空间工具，这样使得应用程序能够集成地理空间功能。
{:shortdesc}

## 静态地图数据查询
{: #static_map_data_query}

要访问道路连接属性数据，{{site.data.keyword.iotmapinsights_short}} 服务提供“连接查询 REST API”界面。该界面接收连接标识作为地图匹配功能可以识别的参数，并返回所请求的连接的详细信息，例如，道路类型、长度、详细形状点数组、相邻节点和相邻连接。使用查询到的详细连接信息，应用程序可以通过观察相邻连接信息来遍历道路连接网络。

## 动态事件数据
{: #dynamic_event_data}

{{site.data.keyword.iotmapinsights_short}} 服务中的事件是动态放置在特定道路连接上的交通事件的对象模型。该事件具有交通事件的基本属性，例如，GPS 坐标、时间、类型、事件持续时间和受影响的长度。您可以动态插入和删除事件。

## 事件插入和删除
{: #inject_event}

使用事件插入 REST API 界面，您可以在地图上存储事件。要插入事件，您可以将事件信息发布到界面上，根据应用程序的预期用途使用已定义的事件类型对事件及其属性进行分类。使用事件删除 REST API 界面，您可以从地图中除去事件，以便管理过时的事件。

## 事件查询
{: #query_event}

使用事件查询 REST API 界面，您可以在设置为请求参数的指定条件下查询事件。对于查询条件，您可以使用经度和纬度范围设置区域，并设置事件属性来缩小作为请求响应返回的目标事件的范围。

## 地理空间工具
{: #geospatial_tools}

对于地理空间工具，{{site.data.keyword.iotmapinsights_short}} 服务提供 REST API 界面用于地图匹配和路线搜索功能。

## 地图匹配
{: #map_matching}

如果来自设备的 GPS 数据不够准确，不能用于分析或可视化，或者如果应用程序需要道路连接网络的属性，您可以使用地图匹配 REST API 界面。地图匹配 REST API 使您的应用程序能够将原始 GPS 数据点安置到道路连接上的匹配点。地图匹配 REST API 界面接收某一点的经度和纬度 GPS 坐标数据，并返回地图匹配的点。通过考虑特定时间段内每台车辆的历史数据来分析此点，以实时查找最可能的点。对于没有历史位置数据的点，地图匹配界面会返回地图连接上距离所请求的 GPS 点最近的点。

## 路线搜索
{: #route_search}

如果需要应用程序执行地理空间功能，您将需要搜索两点之间的最短路径。{{site.data.keyword.iotmapinsights_short}} 服务的路线搜索 REST API 界面会计算起始点和终止点 GPS 坐标之间的最短路径。使用地图匹配功能，使接收到的坐标与地图的最近连接相匹配，并计算这些地图匹配的点之间的最短路径。

## 受影响的连接搜索
{: #link_search}

道路上发生事件时，该事件可能会影响各种道路连接。您可以使用 REST API 来搜索受影响的连接，并找到车辆可能到达该事件的道路连接。搜索会将道路连接网络的拓扑考虑在内，而不仅仅是从车辆到事件的距离。

