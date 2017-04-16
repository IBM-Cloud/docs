---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:new_window: target="_blank"}

# 开发应用程序 
{: #develop-apps-IDS}

*上次更新时间：2015 年 12 月 7 日*  

您既可以使用集成开发环境 (IDE) 或文本编辑器来开发应用程序，也可以使用 {{site.data.keyword.jazzhub}}。
{: shortdesc}

## 使用 Bluemix DevOps Services 开发应用程序
{: #dev_ops}

您可以使用 {{site.data.keyword.jazzhub_short}} 在云中开发、跟踪和计划应用程序，然后将其部署到 {{site.data.keyword.Bluemix_notm}}。只需几分钟就可以从源代码转至运行中应用程序。  

{{site.data.keyword.jazzhub_short}} 提供两种服务：{{site.data.keyword.trackplan}} 和 {{site.data.keyword.deliverypipeline}}。{{site.data.keyword.trackplan}} 服务用于灵活规划。{{site.data.keyword.deliverypipeline}} 服务可实现构建和部署自动化。在 {{site.data.keyword.Bluemix_notm}}“目录”中，可以找到这些服务。要了解有关如何使用它们的更多信息，请参阅 [Track & Plan 入门](../services/TrackPlan/index.html#gettingstartedtemplate)和 [Delivery Pipeline 入门](../services/DeliveryPipeline/index.html#getstartwithCD)。 

{{site.data.keyword.jazzhub_short}} 还提供用于源代码控制的 Git Hosting 以及用于编辑、管理和部署代码的 Web IDE。在应用程序中，可以单击**添加 GIT** 链接来启用 Git Hosting，该链接位于应用程序“概述”页面的右上角。然后，可以单击**编辑代码**，在 Web IDE 中编辑应用程序的代码。使用 Web IDE shell 时，可以利用内容辅助来运行 cf 命令。例如，您可以通过输入以下命令来获取所有 Cloud Foundry 命令的列表：  
```
help cfo
```
{:pre}
