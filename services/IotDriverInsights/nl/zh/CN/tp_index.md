---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 轨迹模式分析入门
{: #tp_index}
上次更新时间：2016 年 6 月 16 日
{: .last-updated}

“轨迹模式分析”API 是 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.iotdriverinsights_full}} 服务中的一项服务，可用来通过汽车探测数据，分析驾驶行程的始发地/目的地 (O/D) 和路线模式。

{:shortdesc}

下图概述“轨迹模式分析”中的典型 API 调用序列：

![典型分析顺序](images/tp_sequence_diagram.png "典型分析顺序")

创建和部署 {{site.data.keyword.iotdriverinsights_short}} 作为未绑定服务实例之后，请完成以下任务，以将应用程序与“轨迹模式分析”API 集成。

## 开始之前
{: #tp_byb}
- 复查[关于轨迹模式分析](tp_iotdriverinsights_overview.html)主题，以熟悉可分析的行为和上下文。
- 获取自动生成的*租户标识*、*用户名*和*密码*值，在访问 {{site.data.keyword.iotdriverinsights_short}} API 时需要这些内容：

  1. 从 {{site.data.keyword.Bluemix_notm}} 仪表板，单击 {{site.data.keyword.iotdriverinsights_short}} 服务磁贴。
  2. 选择服务实例的**管理**视图。
  3. 记下租户标识、用户名和密码值。

## 任务 1：上传车辆数据
{: #tp_task1}
将多组驾驶行程数据上传至 {{site.data.keyword.iotdriverinsights_short}} 租户，以使驾驶员数据可用于轨迹模式分析。

1. 使用 `sendCarProbeData` API 将汽车探测数据发送到存储库，以进行分析。将汽车探测数据上传至 {{site.data.keyword.iotdriverinsights_short}}。
   - 请求：汽车探测数据

## 任务 2：处理车辆数据
{: #tp_task2}

处理汽车数据，以分析 O/D（始发地/目的地）模式和路线模式

1. 使用“轨迹模式分析”API 的 `sendJobRequest` 发送作业请求，以分析特定时间段的汽车探测数据。
   - 请求：日期范围
   - 响应：作业标识
2. 使用“轨迹模式分析”API 的 `getJobInfo` 检查作业状态。当返回的作业状态为“成功”时，即表示已完成数据处理。您现在可以请求轨迹模式分析结果数据。
   - 请求：作业标识
   - 响应：作业状态

## 任务 3：分析行程
{: #tp_task3}
分析特定日期范围的行程，以了解行程如何符合分析阈值参数。

1. 要获取分析后（始发地/目的地）模式摘要列表，请使用“轨迹模式分析”API 的 `getResultSummary`。
O/D 模式摘要列表包含根据输入参数分析的行程摘要信息：
   - 请求：作业标识
   - 响应：摘要和 O/D（始发地/目的地）模式标识列表
2. 要获取详细的分析后 O/D 模式和路线模式信息，请使用“轨迹模式分析”API 命令的 `getAnalyzedDetail`。
获取分析后行程的详细轨迹模式信息。
   - 请求：作业标识 / O/D 模式标识
   - 响应：O/D 的详细信息（包括路线模式标识）
3. 要检索每一个路线模式的 GPS 点列表，请使用“轨迹模式分析”API 的 `getRouteGPSList`。
最后，获取特定路线模式的 GPS 点列表。
   - 请求：作业标识 / O/D 模式标识 / 路线模式标识
   - 响应：路线模式的经度/维度列表

## 后续步骤
{: #tp_post}
完成上述步骤时，会在组织中生成一组分析后轨迹模式数据。使用应用程序或首选分析软件，对信息进行进一步处理，以获取更有意义的商业数据。

# 相关链接
{: #rellinks}

## API 参考
{: #api}

* [API 文档](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}

## 其他资源
{: #general}

* [{{site.data.keyword.iotmapinsights_short}} 入门](../IotMapInsights/index.html){:new_window}
* [{{site.data.keyword.iot_full}} 入门](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [IBM developerWorks 上的 dW Answers](https://developer.ibm.com/answers/topics/iot-driver-behavior){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-driver-behavior){:new_window}
* [Bluemix 服务中的新增功能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
