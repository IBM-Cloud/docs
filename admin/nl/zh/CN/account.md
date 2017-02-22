---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 管理您的 {{site.data.keyword.Bluemix_notm}} 帐户
{: #mngacct}

转至**帐户**链接以设置通知、查看您帐户的使用情况或查看您的帐单。
{:shortdesc}

## 注册 {{site.data.keyword.Bluemix_notm}}
{: #signup}

您可以使用现有的 IBM 标识，通过创建新 IBM 标识或使用联合标识，来注册 {{site.data.keyword.Bluemix_notm}} 帐户。联合标识是公司域内已向 IBM 注册的标识，因此域和用户凭证可用于访问 IBM Web 应用程序。  

仅当您的公司已经和 IBM 合作进行注册时，联合标识才可用于注册 {{site.data.keyword.Bluemix_notm}}。通过向 IBM 注册公司域，用户可以使用现有公司用户凭证，登录到 IBM 产品和服务。公司的身份提供者随后会处理认证。当您使用联合标识登录到 {{site.data.keyword.Bluemix_notm}} 时，系统会提示您通过您公司的登录页面进行登录。有关向 IBM 请求注册公司或组织域的信息，或者有关流程的更多信息，请参阅 [IBMid Enterprise Federation Adoption Guide ![外部链接图标](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window}。当您请求注册联合标识时，需要 IBM 产品负责人（如产品支持者或客户支持者）。

| 注册方法 | 详细信息 |    
|-----------------|---------|
|现有 IBM 标识 | 如果您已经具有 IBM 标识，请使用您用于其他 IBM 产品和服务的现有凭证来注册 {{site.data.keyword.Bluemix_notm}}。注册时，您需要输入电话号码。 |
|新 IBM 标识 | 如果您没有 IBM 标识，那么您可以选择创建一个。有了 IBM 标识，您就可以使用一个登录用户名登录您所使用的所有 IBM 产品和服务，包括 {{site.data.keyword.Bluemix_notm}}。您需要输入个人信息，包括姓和名、电话号码和新凭证的密码。使用其他 IBM 产品与服务时，您可以使用此 IBM 标识进行登录。  |
|联合 ID | 如果您的公司已请求从您的公司域向 IBM 注册用户凭证，那么您可以使用已用于您公司登录的凭证，来注册 {{site.data.keyword.Bluemix_notm}}。注册时，您需要输入电话号码。 |
{:caption="Table 1. Sign up methods" caption-side="top"}

## 设置通知
{: #notifications}

单击**帐户** &gt; **通知**，以设置总帐帐户和花费通知。花费通知仅可供预订和现买现付 {{site.data.keyword.Bluemix_notm}} 帐户所有者使用。

您可以设置 {{site.data.keyword.Bluemix_notm}} 事件和计划维护的平台电子邮件通知，您也可以设置花费通知，以在帐户接近指定的花费阈值时对您发出警报。完成以下任务，以设置帐户的不同通知类型。

### 设置平台通知

单击**帐户** &gt; **通知** &gt; **平台**，以针对 {{site.data.keyword.Bluemix_notm}} 事件和计划内维护设置电子邮件通知。您可以选择或清除每个选项，以启用或禁用电子邮件通知。

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### 设置花费通知
{: #spendingnotifications}

如果您是预订或现买现付 {{site.data.keyword.Bluemix_notm}} 帐户所有者，那么可以设置电子邮件花费通知。设置有关总帐户花费、总运行时花费、总容器花费、总服务花费以及个别服务（不包括第三方服务）花费的通知。在达到所指定花费阈值的 80%、90% 和 100% 时，您会收到通知。您可以在您的需要发生变化时，随时编辑每个花费通知。

要设置花费限制的电子邮件通知，请完成以下步骤：

<ol>
<li>单击**帐户** &gt; **通知** &gt; **花费**。</li>
<li>输入数字值，以便为每种类型的通知设置用于触发通知的花费阈值：<br />
<ul>
<li>总帐户</li>
<li>总运行时</li>
<li>总服务</li>
<li>总容器</li>
<li>特定服务的花费</li>
</ul>
</li>
<li>完成后，单击**保存**。</li>
</ol>

**注**：如果您拥有试用帐户，那么可以升级到预订帐户或现买现付帐户来设置花费限制。有关现买现付帐户和预订帐户的更多信息，请参阅[计费方式](/docs/pricing/index.html#pay-accounts)。

## 查看使用情况
{: #acctusage}

作为组织的帐户所有者或记帐管理员，您可使用“使用情况仪表板”页面来查看组织中每月使用的运行时、容器、服务和支持的实时费用。您可以查看所有区域中的运行时 GB-小时数和服务使用情况，也可选择查看特定区域的情况。

要打开“使用情况仪表板”页面，请单击**帐户** &gt; *your_account_name* &gt; **使用情况仪表板**。记帐管理员只能查看其作为记帐管理员的组织的详细信息。

在每个记帐周期结束时，将向帐户所有者收取所有组织中发生的总使用量费用。作为帐户所有者，您可以按区域和组织过滤使用情况摘要。您还可以单击特定的月份来查看该月份的使用情况。从**组织**列表中选择**所有组织**以查看帐户中所有组织的使用情况。

## 更新记帐信息
{: #account_billing}

作为帐户所有者，您可以编辑、添加或除去与您的 {{site.data.keyword.Bluemix_notm}} 帐户关联的已保存信用卡信息。单击**帐户** &gt; *your_account_name*&gt; **记帐**。

如果您具有与 {{site.data.keyword.Bluemix_notm}} 帐户相链接的 SoftLayer 帐户，请参阅[链接帐户时 {{site.data.keyword.Bluemix_notm}} 使用情况的帐单](/docs/admin/softlayerlink.html#bill_usage)，以获取记帐方式的更多信息。
