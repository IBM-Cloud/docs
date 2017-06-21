---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 创建组织和空间
{: #orgsspacesusers}

作为帐户所有者，您可以使用“管理组织”页面来管理组织和空间。组织管理员还可以使用“管理组织”页面来管理自己被设置为其管理员的任何组织。
{:shortdesc}

要管理组织和空间，请单击 {{site.data.keyword.Bluemix_notm}} 菜单栏中的**管理** &gt; **帐户** &gt; **组织**。 

**注**：您必须是现买现付帐户的帐户所有者才可创建组织。

## 创建组织
{: #createorg}

组织可以跨多个区域，并且组织通过以下各项进行定义：

<dl>
<dt>团队成员</dt>
<dd>组织和空间中具有基本许可权的角色。您必须先分配到组织，然后才能被授予组织内空间的其他许可权。有关详细信息，请参阅[用户和角色](/docs/iam/users_roles.html#userrolesinfo)。</dd>
<dt>域</dt>
<dd>在分配给组织的因特网上提供路径。路径具有子域和域。子域通常是应用程序名称。域可能是系统域，或者为应用程序注册的定制域。请参阅[管理定制域](/docs/admin/manageorg.html#managedomains)。<br/>
<p>**注**：添加定制域时，必须将 DNS 服务器配置为解析您的定制域，以指向 {{site.data.keyword.Bluemix_notm}} 系统域。这样，当 {{site.data.keyword.Bluemix_notm}} 接收到定制域的请求时，它可以将其正确路由到您的应用程序。</p></dd>
<dt>配额</dt>
<dd>表示组织可用的资源，包括可分配供组织使用的服务数和内存量。创建组织时会分配配额。组织的空间中的任何应用程序或服务都会使用一定的配额。通过“现买现付”或“预订”套餐，可以根据您组织的需求变化来调整 Cloud Foundry 应用程序和容器的配额。请参阅[管理配额](/docs/admin/manageorg.html#managequota)。<p>**注**：在预订帐户中，配额是用户定义的限制，用于触发花费通知。</p></dd>
</dl>

在 {{site.data.keyword.Bluemix_notm}} 中，您可以通过以下方式，使用组织来启用团队成员间的协作并促进项目资源的逻辑分组：

<ul>
<li>您可以将一组空间、应用程序、服务、域、路径和团队成员一起分组到组织中。</li>
<li>您可以管理每个用户对空间和组织的访问权。</li>
</ul>

当您创建组织时，组织名称在 {{site.data.keyword.Bluemix_notm}} 中必须是唯一的。如果组织名称已经由其他 {{site.data.keyword.Bluemix_notm}} Public、Dedicated 或 Local 用户使用，那么必须指定新名称。创建组织之后，系统会自动为您分配*组织管理员*许可权，该许可权允许您编辑组织名称、添加团队成员以及在组织中创建或删除空间。

可以使用 [`bx iam org-delete`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_org_delete) 命令来删除组织。删除组织时，会删除该组织内的所有空间、应用程序和服务。

以下[用户角色](/docs/iam/users_roles.html#userrolesinfo)可以分配给组织中的团队成员：

<ul>
<li>组织管理员</li>
<li>组织记帐管理员</li>
<li>组织审计员</li>
</ul>

只有拥有现买现付帐户的帐户所有者才能创建组织。您可以通过完成以下步骤来创建组织：

1. 单击**管理** &gt; **帐户** &gt; **组织**。
2. 单击**添加新组织**。
3. 输入组织名称。
4. 单击**添加**。

<!-- Add info on Manage infrastructure option under a space -->

## 创建空间
{: #spaceinfo}

在组织内，您可以使用空间将一组应用程序、服务和团队成员分组在一起。空间与 {{site.data.keyword.Bluemix_notm}} 中的特定区域联系在一起。

在将团队成员添加到组织之后，您可以对其授予空间的许可权。与组织类似，空间也具有一组[用户角色](/docs/iam/users_roles.html#userrolesinfo)，这些角色带有分配给团队成员的特定许可权：

<ul>
<li>空间管理员</li>
<li>空间开发者</li>
<li>空间审计员</li>
</ul>

**注**：必须为团队成员分配空间中的至少一个许可权。

您可以在组织中创建空间；例如，*dev* 空间（作为开发环境）、*test* 空间（作为测试环境）和 *production* 空间（作为生产环境）。然后，可以将应用程序与空间相关联。要创建空间，请完成以下步骤：

1. 单击**管理** &gt; **帐户** &gt; **组织**。
2. 确定要向其添加空间的组织，然后选择**查看详细信息**。
4. 单击**添加空间**。
5. 输入空间名称。
6. 单击**添加**。
