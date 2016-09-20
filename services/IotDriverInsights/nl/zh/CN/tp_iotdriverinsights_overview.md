---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 关于轨迹模式分析
{: #tp_iotdriverinsights_overview}
上次更新时间：2016 年 6 月 16 日
{: .last-updated}

“轨迹模式分析”API 是 {{site.data.keyword.iotdriverinsights_full}} 提供的服务，可用于通过汽车探测数据，分析驾驶行程的始发地/目的地 (O/D) 和路线模式。

{:shortdesc}

## 路线轨迹模式分析
{: #tpa}

您可以通过多个驾驶行程，识别并分析 O/D 和路线模式。
下图显示从多个行程中获取的车辆（车辆 1）的 O/D 和路线模式的简单示例。在此示例中，“轨迹模式分析”识别两种 O/D 模式：
- 具有两个路线模式的住宅（始发地 1）到办公室（目的地 1）的 O/D 模式
- 具有一个路线模式的住宅（始发地 1）到商店（目的地 2）的 O/D 模式

![OD 路线示例](images/tp_odroute_example.png "O/D 和路线模式示例")

“轨迹模式分析”还会计算每一个车辆的一些驾驶多样性度量，如下表所示。您可以使用这些度量，来判断驾驶员的驾驶特征。

|度量名称|描述|
|:---|:---|
|特殊 O/D 比率|未由 O/D 模式转换的行程数与输入行程总数的比率。|
|特殊里程比率|未由路线模式转换的里程与输入行程的总里程的比率。|
|特殊行程比率|未由路线模式转换的行程数与输入行程总数的比率。|


## REST API
{: #rest_api}

“轨迹模式分析”REST API 提供可用来定制和构建 {{site.data.keyword.Bluemix_notm}} 应用程序的请求：

 1. 汽车数据命令：
   - `sendCarProbeData` 发送要分析的汽车探测数据
   - `getCarProbeDataListAsDate` 返回按日期的汽车探测数据列表
   - `deleteCarProbeDataListByDate` 删除汽车探测数据
 2. 分析作业命令：
   - `sendJobRequest` 发送轨迹模式分析作业请求
   - `getJobInfo` 返回指定作业的信息
   - `getJobInfoList` 返回作业信息的列表
 3. 分析结果命令：
   - `getResultSummary` 返回轨迹模式分析的分析后摘要信息
   - `getAnalyzedODDetail` 返回指定分析后 O/D 模式的详细信息
   - `getRouteGPSList` 返回指定分析后路线模式的 GPS 信息列表
   - `getODList` 返回指定自变量的 O/D 模式信息列表
   - `deleteJobResult` 删除与作业相关的所有分析后的结果

有关更多信息，请参阅 [{{site.data.keyword.iotdriverinsights_short}} API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window} 文档。
