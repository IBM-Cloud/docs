---



copyright:

  years: 2016, 2017
lastupdated: "2017-02-02"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# IBM {{site.data.keyword.Bluemix_notm}} 标准帐户 Beta 版 
{: #betaintro}

{{site.data.keyword.Bluemix}} 标准帐户 Beta 版引入了全新的免费帐户，其提供了一种在 {{site.data.keyword.Bluemix_notm}} Public Cloud 中工作的新方法。与 30 天 {{site.data.keyword.Bluemix_notm}} 试用版不同，标准帐户永不过期。您可以持续使用 {{site.data.keyword.Bluemix_notm}} 应用程序，而无需考虑任何时间限制。
{:shortdesc}

只有受到邀请才能参与标准帐户 Beta 版。在您接受邀请并创建标准帐户后，您可以邀请朋友和同事参与 Beta 版。  

## {{site.data.keyword.Bluemix_notm}} 标准帐户简介
{: #standardaccount}

您可能想知道标准帐户与试用帐户相比有何不同。下表汇总了 {{site.data.keyword.Bluemix_notm}} 标准帐户的重要详细信息。 

|标准帐户中的新增功能？ |    
|-----------------|
| 帐户永不过期。 |
| Cloud Foundry 应用程序可以访问高达 256 MB 的可用即时运行时内存。 |
| 您可以使用即将推出的更多服务，访问 Cloudant NoSQL DB 和 Internet of Things Platform 的免费 Lite 套餐。 |
| 如果超过 10 天没有任何开发活动，那么您的应用程序将休眠。 |
| 您的服务实例将在处于不活动状态 30 天后删除。 |
{:caption="表 1. 标准帐户中的新增内容" caption-side="top"}

|转换试用帐户时未发生更改的内容？ | 
|-----------------|
|帐户是免费的 -- 不需要信用卡。 |
|Cloudant NoSQL DB 和 Internet of Things Platform 的任何 Lite 实例。上述每个服务的一个 Lite 实例可转移到您的新帐户。 |
|您的组织、空间和相关联团队成员权限设置仍保持相同。一个组织可转移到您的新帐户。 |
|{{site.data.keyword.Bluemix_notm}} 支持的级别仍相同。 |
{:caption="表 2. 未发生更改的内容" caption-side="top"}

**注**：如果未转换试用帐户，那么您将看到一条说明原因的消息。您可能在现有试用帐户或应用程序中具有无法转移的多个组织。您可以采取适当的操作，然后重新尝试转换帐户。

当您注册标准帐户时，您可以邀请团队成员在您组织和空间中进行协作、查看使用情况、创建空间、更新帐户概要文件并管理组织。有关更多信息，请参阅[设置帐户](/docs/admin/adminpublic.html#account)。

### Lite 套餐
{: #liteplans}
   
Lite 套餐（也在现买现付帐户中提供）构造为免费配额。您可以高枕无忧地处理您的项目，而不会有生成意外帐单的风险。配额可能会运作一段特定时间，例如，一个月或一次性使用。以下是 Lite 套餐配额的一些示例：

<ul>
<li>最大数目的已注册设备。</li>
<li>最大数目的应用程序绑定。</li>
<li>加密数据存储限制，例如 1 GB。</li>
<li>供应的吞吐量。</li>
</ul> 

在标准帐户中，您可以使用 {{site.data.keyword.Bluemix_notm}}“目录”中具有 Lite 套餐的任何项目。Lite 套餐很容易找到。缺省情况下，当您打开“目录”时，即会以 Lite 标记 ![Lite 标记](../icons/Lite.svg) 显示和识别具有 Lite 套餐的所有服务。选择某个服务以查看相关联 Lite 套餐的配额详细信息。

### 标准帐户中提供的功能？
{: #whatsavailable}

在标准帐户中，Cloud Foundry 应用程序可以访问最多 256 MB 的即时运行时内存。如果您超过分配的配额，那么您可以停止一些应用程序，以释放运行时内存。 

在标准帐户 Beta 版中，以下服务提供 Lite 套餐：

<ul>
<li>Cloudant NoSQL DB</li>
<li>Internet of Things Platform</li>
</ul>

我们将随时对此服务列表进行补充，敬请关注！

当达到配额限制时，将停止您的应用程序或禁用您的服务。如果 Lite 套餐指定按月提供配额，那么将在每月的 1 日重置资源使用情况，这时您可以恢复使用服务。当您将要达到或已达到配额限制时，您将收到通知电子邮件。 

您可以每个 Lite 套餐供应 1 个实例。 

**注**：这些限制仅适用于标准帐户。您可以随时升级到现买现付或预订缴费帐户。您仅需要为超出免费限额的使用部分付费。有关现买现付帐户和预订帐户的更多信息，请参阅[计费方式](/docs/pricing/index.html#pay-accounts)。

### 开发活动
{: #devactivity}

为了帮助标准帐户用户最佳地管理其资源，我们构建了一组基于开发活动和使用情况的效率特性：

 * 如果应用程序的开发处于不活动状态的时间超过 10 天，该应用程序将进入休眠。当您想要使用新应用程序时，这非常有用，因为您将发现自己不会达到 256 MB 的内存配额限制。要唤醒应用程序，可在 Cloud Foundry 命令行或 {{site.data.keyword.Bluemix_notm}} 控制台中重新开始使用它们。 
 
 以下是可唤醒应用程序的所有命令的列表：
  * cf push
  * cf restate
  * cf restart
  * cf ssh
  * cf scale
  * cf stop
  * cf start
  * cf create-route
  * cf map-route
  * cf unmap-route
  * cf delete-route
  * cf enable-ssh
  * cf disable-ssh

 **注**：如果您的应用程序已启用 ssh，那么 `cf enable-ssh` 和 `cf disable-sh` 命令将不会唤醒应用程序。 

 * 如果 Lite 套餐服务处于不活动状态超过 30 天，那么将会删除 Lite 套餐服务。然后，当您想要创建新实例时，无需删除处于不活动状态的实例。目前，仅 Internet of Things Platform 服务使用此功能。 
 
 通过登录到 Internet of Things Platform 服务实例仪表板，使 Internet of Things Platform Lite 实例处于活动状态。
 
### 参与标准帐户 Beta 版
{: #betainvitation}

如果您被选中参与 Beta 版，那么会向与您 {{site.data.keyword.Bluemix_notm}} 试用帐户相关联的电子邮件地址发送邀请。当您收到邀请时，请完成电子邮件中的指示，以注册标准帐户。 

有兴趣参与标准帐户 Beta 版产品吗？邀请您的朋友和同事。如果他们已受邀加入 Beta 版并创建了自己的标准帐户，那么他们也可以邀请您。 
