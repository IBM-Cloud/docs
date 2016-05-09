---

 

copyright:

  years: 2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}

# 创建 Cloud Foundry 应用程序
*上次更新时间：2016 年 4 月 18 日*

通过 {{site.data.keyword.Bluemix}}，您可以在 {{site.data.keyword.Bluemix_notm}} 用户界面中创建应用程序。创建应用程序后，可以决定是否要继续使用 UI、cf 命令行界面或 {{site.data.keyword.jazzhub_title}} 来开发、跟踪、规划和部署应用程序。
{:shortdesc}

在 {{site.data.keyword.Bluemix_notm}} 中创建应用程序时，首先需要使用入门模板。*入门模板*是一种模板，其中包含预定义的服务以及使用特定 buildpack 配置的应用程序代码。入门模板有两种类型：样板和运行时。

*样板*是一种容器，其中包含一个应用程序及其关联的运行时环境，以及为特定域预定义的服务。例如，“移动云”样板包含 Node.js 运行时，以及 Mobile Data、Mobile Application Security 和 Push 服务。样板还包含一个 SDK 和一些样本应用程序，您可以基于它们来开发用于访问这些服务的移动应用程序。

*运行时*是用于运行应用程序的一组资源。{{site.data.keyword.Bluemix_notm}} 提供了多种运行时环境，用于包含不同类型的应用程序。运行时环境是以 buildpack 的形式集成到 {{site.data.keyword.Bluemix_notm}} 中，由系统自动配置使用，几乎不需要维护。

要开始创建应用程序，请执行以下步骤：
  1. 在 {{site.data.keyword.Bluemix_notm}} 用户界面中，转至“仪表板”。
  2. 单击**创建应用程序**。
  3. 单击 **Web**，然后按照指导经验来选择入门模板，指定名称以及选择编码方式。
  4. 按照指导经验完成操作后，单击**查看应用程序概述**。此时，“仪表板”上将显示您的应用程序的“概述”。
  5. 在 Bluemix 用户界面中，单击应用程序“概述”上的**添加服务或 API**，可以向您的应用程序中添加服务。浏览目录并从中选择服务，或者滚动到目录结尾并单击 **{{site.data.keyword.Bluemix_notm}} 试验性服务**以浏览试验性服务。也可以使用 cf 命令行界面。请参阅“用于处理应用程序的选项”。
  6. 在应用程序“概述”上，单击“添加 Git”可将应用程序源代码保存到 Git 存储库中，然后创建 Git 托管的项目。您还可以从 {{site.data.keyword.jazzhub_title}} 部署应用程序。

**注：**如果绑定到应用程序的服务崩溃，那么该应用程序可能会停止运行或发生错误。{{site.data.keyword.Bluemix_notm}} 不会自动重新启动应用程序，以便从这些问题中进行恢复。请考虑对应用程序进行编码，使其能够识别中断、异常和连接失败状况并从中进行恢复。有关更多信息，请参阅“应用程序不会自动重新启动”故障诊断主题。

## 用于处理应用程序的选项

创建应用程序后，您可以通过一些选项继续处理应用程序（例如，向应用程序中添加服务，构建和部署应用程序）：

<dl><dt>cf 命令行界面</dt>
<dd>使用 cf 命令行界面可更新应用程序，创建服务实例或将服务绑定到应用程序。您还可以使用 cloud-cli 命令行界面来创建、更新和删除服务产品。</dd>
<dt>{{site.data.keyword.Bluemix_notm}} 用户界面</dt>
<dd>使用 {{site.data.keyword.Bluemix_notm}} 用户界面可构建应用程序，包括将哪些服务和运行时组合在一起来解决您的业务问题。</dd>
<dt>{{site.data.keyword.jazzhub_title}}</dt>
<dd>使用 {{site.data.keyword.jazzhub_title}} 可在云中创建应用程序，并将其部署到 {{site.data.keyword.Bluemix_notm}}。{{site.data.keyword.jazzhub_title}} 提供的服务包括 Track & Plan 和 Delivery Pipeline（列在 {{site.data.keyword.Bluemix_notm}}“目录”的“DevOps”下），还包括 Web IDE 和 Git Hosting。</dd>
</dl>

## 提示

开发 Web 应用程序时，请参考以下提示：

<dl><dt>持久性</dt>
<dd>请不要为应用程序指定任何本地存储器。应用程序的每个实例随时都可能会重新启动或被移动到其他虚拟机上（通常是为了实现负载均衡），即使只有一个实例在运行也不例外。移动或删除应用程序时，会擦除本地存储器中存储的所有内容。请使用某个 Bluemix 数据存储服务来实现持久性。</dd>
<dt>资源限制</dt>
<dd>请注意，试用帐户在资源数量方面具有使用限制。这些限制如下：<table style="width:100%">
  <th>资源类型</th>	<th>数量限制</th>
<tr><td>在所有应用程序上使用的服务数</td> <td>10</td>
<tr><td>在所有应用程序上使用的内存</td> <td>	2 G</td>
<tr><td>路径数</td> <td>500</td>
</table>
</dd></dl>

*表 1. 试用帐户的 {{site.data.keyword.Bluemix_notm}} 资源限制*
