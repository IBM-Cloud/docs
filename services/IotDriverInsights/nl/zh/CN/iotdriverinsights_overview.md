---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 关于 {{site.data.keyword.iotdriverinsights_short}}
{: #iotdriverinsights_overview}

可以使用 {{site.data.keyword.iotdriverinsights_full}} 通过汽车探测数据和前后关联数据来分析驾驶员的行为。
{:shortdesc}

## 驾驶员行为分析
{: #driver_behavior_analysis}
可以通过汽车探测数据和前后关联的数据来分析驾驶员行为（例如，突然加速或急刹车、频繁刹车、超速、急转弯和其他操作）。

包括以下活动和综合因素：
 - 驾驶行为 
    - 与速度相关
       - 突然加速
       - 急刹车
       - 超速
       - 频繁停车
       - 频繁加速
       - 频繁刹车
    - 与转弯相关
       - 急转弯（高速转弯）
       - 转弯前加速
       - 转弯期间过度刹车
    - 其他
       - 疲劳驾驶
 - 驾驶方面的综合因素
    - 时间范围
       - 早高峰
       - 晚高峰
       - 白天
       - 夜间
    - 道路类型
       - 高速公路
       - 城市快速路
       - 城市主路
       - 城市公路
       - 其他道路类型
    - 基于道路类型的速度模式
       - 畅通无阻
       - 车流平稳
       - 塞车
       - 严重塞车
       - 各种情况混合

## 大数据分析基础架构
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} 使用 Hadoop 作为后端基础架构。Hadoop 使 {{site.data.keyword.iotdriverinsights_short}} 能够通过分析来自汽车探测数据和前后关联数据的大数据来实现高扩展性。

## REST API
{: #rest_api}
开发者可以通过 REST API 检索分析结果，并将其用在 {{site.data.keyword.Bluemix_notm}} 应用程序中。
 1. 车辆数据
   - `sendCarProbeData` 发送要被分析的汽车探测数据。
   - `getCarProbeDataListAsDate` 返回按日期的汽车探测数据列表。
   - `deleteCarProbeDataListByDate` 删除汽车探测数据。
 2. 分析作业
   - `sendJobRequest` 发送驾驶行为分析作业请求。
   - `getJobInfo` 返回指定作业的信息。
   - `getJobInfoList` 返回作业信息的列表。
 3. 分析结果 
   - `getAnalyzedTripSummaryList` 返回分析后的轨迹摘要信息列表。
   - `getAnalyzedTripInfo` 返回指定的分析后轨迹的信息。
   - `deleteJobResult` 删除与作业相关的所有分析后的结果。

## 可配置性
{: #configurability}
可以从用户界面 (UI) 配置某些分析阈值参数（例如，每种道路类型的速度范围，转弯角度范围等）。
