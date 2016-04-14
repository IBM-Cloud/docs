---

copyright:
  years: 2015, 2016
  
---

# 应用程序监视
{: #app-monitoring}

除了安全功能外，{{site.data.keyword.amafull}} 还为移动应用程序提供了监视和分析功能。可以通过 {{site.data.keyword.amashort}} 客户端 SDK 来记录客户端日志并监视数据。开发者可以控制何时将这些数据发送到 {{site.data.keyword.amashort}} 服务。在 {{site.data.keyword.amashort}} 服务中发生的所有安全事件（例如，认证成功或失败）都会自动记录。

数据传递到 {{site.data.keyword.amashort}} 后，可以使用 {{site.data.keyword.amashort}}“监视仪表板”来获取有关移动应用程序、设备和客户端日志的分析洞察。缺省情况下会记录有关应用程序对 {{site.data.keyword.amashort}} 所保护资源提出的请求的信息。

自动记录的数据包括认证数、新设备数和新用户数等信息。此外，还可以配置 {{site.data.keyword.amashort}} 客户端 SDK 来报告以下信息：

### 移动应用程序的使用情况统计信息
{: #usage-stats}

可以将移动应用程序配置为通过一些简单的 API 调用，记录应用程序生命周期事件，并将记录的数据发送到 {{site.data.keyword.amashort}} 服务。您也可以记录应用程序打开次数、接收到的推送通知数等。

### 客户机端日志捕获
{: #client-side-logcapture}

现场的应用程序有时会遇到问题，需要引起开发者注意以进行修复。通常很难重现这些问题。<!--in R&D.--> 处理代码的开发者可能缺乏用于测试的环境或确切设备。在这些情况下，能够在环境中发生问题时从客户机设备中检索调试日志就会非常有用。

## 保存捕获到的数据
{: #preserve-captureddata}

没有方法能保证在客户端保存所有捕获到的数据。您的用户可能正在脱机运行移动应用程序，并且同时在积累捕获到的分析和日志数据。由于客户机处于脱机状态且文件系统空间有限，因此必须清除较早的记录事件，以腾出空间来保存更新的记录事件。由开发者决定何时使用提供的 API 将捕获到的数据发送到 {{site.data.keyword.amashort}} 服务。

## 使用 {{site.data.keyword.amashort}}“监视仪表板”
{: #monitoring-dashboard}

1. 打开 {{site.data.keyword.Bluemix}}“仪表板”，然后单击 {{site.data.keyword.Bluemix_notm}} 应用程序

2. {{site.data.keyword.Bluemix_notm}} 应用程序仪表板打开时，单击 {{site.data.keyword.amashort}} 磁贴

3. 在 {{site.data.keyword.amashort}}“仪表板”上，单击左侧菜单中的`监视`链接

## 后续步骤
{: #next-steps}
* [启用、配置和使用记录器](app-monitoring-logger.html)
* [收集使用情况分析信息](app-monitoring-gathering-analytics.html)
