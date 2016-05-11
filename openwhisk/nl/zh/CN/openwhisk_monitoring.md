---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 {{site.data.keyword.openwhisk_short}}“仪表板”监视 {{site.data.keyword.openwhisk_short}} 活动
*上次更新时间：2016 年 2 月 9 日*

[{{site.data.keyword.openwhisk}}“仪表板”](https://{DomainName}/whisk/dashboard/)提供了对您活动的图形化摘要。使用该仪表板可确定您的 {{site.data.keyword.openwhisk_short}} 操作的性能和运行状况。
{:shortdesc}

随时单击“重新装入”可使用最新的活动日志数据更新该仪表板。

## 活动摘要
{: #summary}

此视图提供了您的 {{site.data.keyword.openwhisk_short}} 环境的高层次摘要。使用**活动摘要**视图可监视启用了 {{site.data.keyword.openwhisk_short}} 的服务的总体运行状况和性能。通过此视图中的度量值，可以执行以下操作：
* 对于服务的启用了 {{site.data.keyword.openwhisk_short}} 的操作，通过查看调用这些操作的次数，确定这些操作的使用率。
* 确定所有操作中的总体故障率。如果发现错误，可以通过查看**活动直方图**视图来确定哪些服务或操作发生了错误。通过查看**活动日志**来确定错误本身。
* 通过查看与每个操作关联的平均完成时间，确定操作的执行情况。 

<!-- For tips on improving performance, see troubleshooting? -->

## 活动时间线
{: #timeline}

**活动时间线**视图显示垂直条形图，用于查看过去和现在操作的活动情况。红色指示特定操作中有错误。将此视图与**活动日志**相关联，可了解有关错误的更多详细信息。

## 活动直方图
{: #histogram}

**活动直方图**视图显示水平条形图，用于查看过去和现在操作的活动情况。红色指示特定操作中有错误。将此视图与**活动日志**相关联，可了解有关错误的更多详细信息。

## 活动日志
{: #log}

此视图显示已设置格式的活动日志版本。其中显示每个活动的详细信息，但一分钟只会轮询一次，以确定是否有新的活动。单击某个操作可显示详细日志。
**注**：要使用 CLI 获取“活动日志”中显示的输出，请使用以下命令： 

  ```
  wsk activation poll
  ```
  {: pre} 

## 过滤选项
{: #filtering}

选择要查看的操作日志，然后选择记录的活动的时间范围。 

**注**：这些过滤器会应用于仪表板上的所有视图。
