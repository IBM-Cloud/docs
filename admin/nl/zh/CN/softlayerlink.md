---

 

copyright:

  years: 2016
lastupdated: "2016-11-03"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 升级和联合 {{site.data.keyword.Bluemix_notm}} 与 SoftLayer 缴费账户
{: #softlayerlink}

如果您拥有 {{site.data.keyword.Bluemix_notm}} 试用帐户，并且要访问“基础架构”仪表板，那么必须升级到 {{site.data.keyword.Bluemix_notm}}“现买现付”帐户。如果要使用在试用帐户内不可用的其他收费资源，或者试用帐户已到期，那么也必须升级。 

您可以通过将现有 {{site.data.keyword.Bluemix_notm}} 和 SoftLayer 缴费账户链接在一起，以联合这两个帐户。链接帐户时，您将通过 {{site.data.keyword.Bluemix_notm}} 同时对 {{site.data.keyword.Bluemix_notm}} 和 SoftLayer 资源进行记帐。
{:shortdesc}

## 升级到 {{site.data.keyword.Bluemix_notm}}“现买现付”帐户
{: #upgradetopayg}

使用试用帐户登录到 {{site.data.keyword.Bluemix_notm}} 时，不能访问 {{site.data.keyword.Bluemix_notm}}“基础架构”仪表板。如果希望应用程序使用基础架构资源，那么必须升级到“现买现付”帐户。

要将试用帐户升级到 {{site.data.keyword.Bluemix_notm}}“现买现付”帐户，请完成以下步骤：

 1. 单击**帐户** &gt; **记帐**。
 2. 然后，单击**添加信用卡**。
 3. 输入必需的记帐详细信息。 
 4. 阅读并接受“现买现付”帐户的条款和条件。 
 5. 完成后，单击**升级**。 
 
升级到“现买现付”帐户后，**基础架构**选项会列在 {{site.data.keyword.Bluemix_notm}} **目录**中。如果使用量超过免费限额，那么您将收到按月开具的 {{site.data.keyword.Bluemix_notm}} 发票。发票将采用美元 (USD) 计费，并将详细描述您的资源费用。 

## 联合 {{site.data.keyword.Bluemix_notm}} 和 SoftLayer 帐户
{: #unifyingaccounts}

您可以联合 {{site.data.keyword.Bluemix_notm}} 和 SoftLayer 帐户以利用组合资源。链接 {{site.data.keyword.Bluemix_notm}} 和 Softlayer 帐户后，您将收到单个 {{site.data.keyword.Bluemix_notm}} 发票。如果您有现有的 {{site.data.keyword.Bluemix_notm}} 帐户，那么通过 {{site.data.keyword.Bluemix_notm}} 对 SoftLayer 资源进行记帐会在链接帐户之后启动的新记帐周期生效。


**重要信息：**{{site.data.keyword.Bluemix_notm}} 中的所有链接帐户都必须是“现买现付”帐户。您可以创建新的“现买现付”帐户，或者链接现有的“现买现付”帐户。或者，您可以链接现有的试用帐户，但是它将升级到“现买现付”帐户。不能链接预订 {{site.data.keyword.Bluemix_notm}} 帐户。  

链接帐户后：

* 必须使用 IBM 标识凭证来访问 SoftLayer 和 {{site.data.keyword.Bluemix_notm}} 帐户。
* 将对全体 {{site.data.keyword.Bluemix_notm}} 费用应用所有现有的 SoftLayer 折扣。 
* 您将收到一张以美元 (USD) 计费的发票。
* 您可以在 {{site.data.keyword.BluSoftlayer}} 用户界面中监视 {{site.data.keyword.Bluemix_notm}} 资源的使用情况。 

**注意：**帐户链接之后即无法对它们取消链接。 

如果您具有 SoftLayer 帐户，且您想要链接 SoftLayer 和 {{site.data.keyword.Bluemix_notm}} 帐户，请完成以下步骤：

 1. 从 {{site.data.keyword.slportal}}，单击**链接 {{site.data.keyword.Bluemix_notm}} 帐户**。
 2. 阅读并接受链接 SoftLayer 和 {{site.data.keyword.Bluemix_notm}} 帐户的条款。
 3. 要求时，提供与 {{site.data.keyword.Bluemix_notm}} 帐户相关联的电子邮件地址。如果您没有 {{site.data.keyword.Bluemix_notm}} 帐户，请提供要使用的电子邮件地址，然后遵循指示受邀加入 {{site.data.keyword.Bluemix_notm}} 并创建帐户。

您必须是 SoftLayer 帐户中的主用户，才能链接帐户。

链接帐户之后，SoftLayer 全局标题中即可使用**转至 {{site.data.keyword.Bluemix_notm}}** 链接。单击此链接可带您进入 {{site.data.keyword.Bluemix_notm}} 登录页面。此外，**SoftLayer** 链接现在可在 {{site.data.keyword.Bluemix_notm}} 标题中使用。单击该链接可在新窗口中带您进入 {{site.data.keyword.slportal}} 的主页。

{{site.data.keyword.Bluemix_notm}} 基础架构产品连接到一个三层网络，对公共、专用和管理流量进行分段处理。客户的 {{site.data.keyword.Bluemix_notm}} 帐户上的基础架构产品可在专用网络上免费相互传输数据。基础架构产品（例如，裸机服务器、虚拟服务器和云存储器）在公用网络上连接到 {{site.data.keyword.Bluemix_notm}}“目录”中的其他应用程序和服务，如 Watson 服务、容器或运行时。这两种类型的产品之间的数据传输按标准公用网络带宽费率计量并收费。

## 链接帐户时 {{site.data.keyword.Bluemix_notm}} 使用情况的信用值
{: #slcredit}

从 SoftLayer 帐户链接 {{site.data.keyword.Bluemix_notm}} 帐户后，您将收到 200.00 美元的信用值，该信用值只能在 {{site.data.keyword.Bluemix_notm}} 内使用。必须在链接帐户的 30 天内使用该信用值。

有关如何查看信用值和到期日期的更多信息，请参阅[查看信用值](https://console.ng.bluemix.net/docs/pricing/index.html#credits)。

## 邀请 SoftLayer 团队成员加入 {{site.data.keyword.Bluemix_notm}}
{: #invite_users}

链接 {{site.data.keyword.Bluemix_notm}} 和 SoftLayer 帐户后，可以邀请 SoftLayer 团队成员加入 {{site.data.keyword.Bluemix_notm}}。或者，您可以在以后从 {{site.data.keyword.Bluemix_notm}} 用户界面邀请 SoftLayer 团队成员。
{:shortdesc}

从 {{site.data.keyword.Bluemix_notm}} 用户界面，您可以选择邀请 SoftLayer 帐户的所有成员，或者您可以选择个别成员。邀请团队成员时，您必须为被邀请者设置 {{site.data.keyword.Bluemix_notm}} 帐户角色。有关 {{site.data.keyword.Bluemix_notm}} 中不同角色的更多信息，请参阅[用户角色](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo)。

您必须是 SoftLayer 帐户中的主用户，才能邀请团队成员加入 {{site.data.keyword.Bluemix_notm}} 帐户。

要通过 {{site.data.keyword.Bluemix_notm}} 邀请团队成员，请完成以下步骤：

 1. 单击**帐户** &gt; **邀请团队成员**。
 2. 单击**添加**，以在 SoftLayer 帐户中进行认证，并查看 {{site.data.keyword.BluSoftlayer}} 帐户的团队成员列表。
 3. 选择要邀请的团队成员，然后单击**发送**。
 
团队成员接收包含**加入组织**链接的电子邮件。如果该团队成员没有 IBM 标识，那么会将该团队成员重定向到注册页面。接下来，该团队成员可以输入一些基本信息，并创建自己的 {{site.data.keyword.Bluemix_notm}} 帐户。

有关通过 {{site.data.keyword.Bluemix_notm}} 用户界面邀请团队成员的更多信息，请参阅[邀请团队成员](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers)。

## 切换到 IBM 标识
{: #ibmid_switch}

现在，在 SoftLayer 中进行认证将使用 IBM 标识来提供对 {{site.data.keyword.Bluemix_notm}} 的单点登录。如果您有现有的 SoftLayer 帐户，那么可以切换到 IBM 标识。迁移向导将指导您完成此切换。
{:shortdesc}

开始切换到 IBM 标识的过程后，只要尚未完成此过程，随时都可以将其取消。但是，下次登录时，系统仍将提示您切换到 IBM 标识。

要开始将现有 SoftLayer 用户名切换到 IBM 标识，请完成以下步骤：

 1. 在 {{site.data.keyword.slportal}} 中，转至“编辑用户个人档案”页面，然后单击**切换到 IBM 标识**。
 2. 遵循迁移向导提示来创建 IBM 标识。一旦创建 IBM 标识后，就不能更改该标识（即电子邮件地址）。可以更新与个人档案关联的电子邮件，但缺省情况下，该值会设置为您针对 IBM 标识定义的内容。完成向导后，会向您发送一封电子邮件。
 3. 收到电子邮件后，请访问相应链接或将相应 URL 复制到浏览器中，然后输入注册代码。此代码有效期为 7 天，属于一次性代码。此代码一旦使用后即失效。将 IBM 标识设置为 SoftLayer 用户链接后，即只能使用 IBM 标识登录到帐户。在登录对话框上，必须使用**使用 IBM 标识登录**按钮，而不是输入 SoftLayer 用户名和密码。
 
如果您是新客户，在检查订单时，系统会要求您输入现有 IBM 标识帐户的电子邮件地址或创建新的 IBM 标识帐户。 

### 将多个 SoftLayer 帐户映射到一个 IBM 标识
{: #map_multiple_accounts}

您可以在设置帐户时，使用现有的 IBM 标识电子邮件地址，将一个 IBM 标识与多个 SoftLayer 帐户相关联。每个帐户只能有一个 SoftLayer 用户映射到单个 IBM 标识。该 IBM 标识在每个 SoftLayer 帐户中必须唯一。但是，一个有权访问多个 SoftLayer 帐户的用户可以使用一个 IBM 标识来访问多个 SoftLayer 帐户。

例如，IBM 标识可以映射到帐户 A 和 B 中的主用户，并且可以映射到帐户 C 和 D 中的另一个用户。在映射到该 IBM 标识的这些帐户中，其中一个帐户是缺省帐户。通常，缺省帐户是第一个映射到 IBM 标识的帐户。但是，您可以通过客户门户网站中的帐户切换功能将其他帐户切换为缺省帐户。

对于具有有权访问多个帐户的 IBM 标识并启用了双因子认证的用户，在帐户登录和帐户切换期间，每个帐户都需要提供相应的双因子认证验证码。

## 使用 {{site.data.keyword.Bluemix_notm}} 服务与 SoftLayer 资产
{: #bluemix_services}

您可以轻松地使用基于 API 的公共 {{site.data.keyword.Bluemix_notm}} 服务与 SoftLayer 资产。所有 API 都很安全且已加密，以便保护您的数据。
{:shortdesc}

例如，您曾想要通过 SoftLayer，将认知功能从 Watson 添加到在裸机服务器上运行的应用程序吗？您可以使用四个简单的步骤，添加 {{site.data.keyword.personalityinsightsshort}} 等服务，以帮助了解您的应用程序用户：

1. 在 {{site.data.keyword.Bluemix_notm}} 目录中查找服务。
2. 仅使用几下单击，供应服务的实例。
3. 通过复制服务凭证并将它们添加到应用程序，设置服务以与现有代码一起运行。
4. 更新应用程序之后，在 SoftLayer 基础架构上部署新版本。

通过在 SoftLayer 中从应用程序调用 Watson API，使它们更具个性化，您可以获得*洞察和认知*知识。或者，使用*数据和分析*服务，以对您的应用程序使用高性能分析。或者，选择数据库即服务，在这里您可以让 {{site.data.keyword.Bluemix_notm}} 来进行管理。

将容器与 {{site.data.keyword.activedeployshort}} 和 {{site.data.keyword.deliverypipeline}} 等服务配合使用，使得您的应用程序开发更具现代化。然后，您可以使用 {{site.data.keyword.vpn_short}} 服务，通过隧道回到 SoftLayer，以将专用网络中的容器连接到 SoftLayer 专用网络。计算资源和服务的所有使用量费用都会反映在 {{site.data.keyword.Bluemix_notm}} 帐单中。 

### 基于 API 的 {{site.data.keyword.Bluemix_notm}} 服务
并非所有 {{site.data.keyword.Bluemix_notm}} 服务都可以和 SoftLayer 一起使用。以下服务可以设置为与应用程序代码一起运行：
* {{site.data.keyword.alchemyapishort}}
* {{site.data.keyword.alertnotificationshort}}
* {{site.data.keyword.sparks}}
* {{site.data.keyword.appseccloudshort}}
* {{site.data.keyword.blockchain}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.conceptinsightsshort}}
* {{site.data.keyword.iotmapinsights_short}}
* {{site.data.keyword.dashdbshort}}
* {{site.data.keyword.dialogshort}}
* {{site.data.keyword.documentconversionshort}}
* {{site.data.keyword.twittershort}}
* {{site.data.keyword.weather_short}}
* {{site.data.keyword.iotdriverinsights_short}}
* {{site.data.keyword.geospatialshort_Geospatial}}
* {{site.data.keyword.graphshort}}
* {{site.data.keyword.iotelectronics}}
* {{site.data.keyword.languagetranslationshort}}
* {{site.data.keyword.messagehub}}
* {{site.data.keyword.mqa}}
* {{site.data.keyword.mobileappbuilder_short}}
* {{site.data.keyword.mql}}
* {{site.data.keyword.nlclassifierlshort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.servicediscoveryshort}}
* {{site.data.keyword.speechtotextshort}}
* {{site.data.keyword.sqldb}}
* {{site.data.keyword.streaminganalyticsshort}}
* {{site.data.keyword.texttospeechshort}}
* {{site.data.keyword.toneanalyzershort}}
* {{site.data.keyword.tradeoffanalyticsshort}}
* {{site.data.keyword.visualinsightsshort}}
* {{site.data.keyword.visualrecognitionshort}}
* {{site.data.keyword.workflow}}
* {{site.data.keyword.workloadscheduler}}

**注：**并非这些服务的所有套餐都可用。只有针对“现买现付”帐户启用的套餐可用于与相链接的帐户一起使用。但是，如果您具有单独记帐的独立 {{site.data.keyword.Bluemix_notm}} 帐户，那么您可以对这些服务中的任何一个使用任何套餐。

## 链接帐户时 {{site.data.keyword.Bluemix_notm}} 使用情况的帐单
{: #bill_usage}

在您链接 {{site.data.keyword.Bluemix_notm}} 和 SoftLayer 缴费帐户之后，下一个记帐周期将会记入单个 {{site.data.keyword.Bluemix_notm}} 帐单。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} 使用情况周期以日历月为基础，因此您的帐户会在每月的建立收费协议的记帐日进行记帐。使用 SoftLayer，您的使用情况周期从您开始使用 SoftLayer 开始，因此每月会在您注册 SoftLayer 帐户的那一天进行记帐。 

当链接帐户时，{{site.data.keyword.Bluemix_notm}} 使用情况将继续在当前月份周期内测量，并会在 {{site.data.keyword.Bluemix_notm}} 发票上对该使用情况进行记帐。从下个月的第一天开始，您的 {{site.data.keyword.Bluemix_notm}} 和 SoftLayer 费用将会一并列在 {{site.data.keyword.Bluemix_notm}} 发票上。

例如，如果您在 4 月 16 日链接帐户，那么您将获得四月使用情况的 Bluemix 发票。根据链接帐户的时间，您可能会收到针对 SoftLayer 使用量的单独帐单。您在五月对 SoftLayer 和 {{site.data.keyword.Bluemix_notm}} 的使用量将通过 {{site.data.keyword.Bluemix_notm}} 帐户记帐。

![链接 Bluemix 和 SoftLayer 帐户摘要](images/BluemixSoftLayerBill.svg)

链接帐单后，{{site.data.keyword.Bluemix_notm}} 发票将在以下标题下列出针对所使用的每个资源的不同费用：

* **裸机服务器和连接的服务**
* **虚拟服务器和连接的服务**
* **未连接的服务**

有关如何查看 {{site.data.keyword.Bluemix_notm}} 使用情况的更多信息，请参阅[查看使用情况详细信息](https://console.ng.bluemix.net/docs/pricing/index.html#usage)。

