{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#管理 {{site.data.keyword.Bluemix_notm}}
{: #administer}
*上次更新时间：2015 年 11 月 18 日*

单击**帐户和支持** &gt; **管理组织**可管理组织、空间和分配的用户。如果您是 {{site.data.keyword.Bluemix_notm}} Local 或 {{site.data.keyword.Bluemix_notm}} Dedicated 用户，请参阅[管理 {{site.data.keyword.Bluemix_notm}} Local 和 {{site.data.keyword.Bluemix_notm}} Dedicated](index.html#mng)，以了解有关管理本地或专用实例的更多信息。{:shortdesc}

##管理您的帐户
{: #mngacct}

在 {{site.data.keyword.Bluemix}} 中，无论是管理组织和空间，还是管理用户访问权，都可以从用户界面中的仪表板来进行操作。也可以监视您的使用情况和费用。{:shortdesc}

###组织和空间
{: #orgsandspaces}

如果您是组织管理员或帐户所有者，那么可以使用“管理组织”页面来查看和管理组织或空间的设置，包括用户访问权。要打开“管理组织”页面，请转至菜单上的*帐户和支持* &gt; **管理组织**。

####组织

组织由以下项定义：

<dl>
<dt>Users</dt>
<dd>组织和空间中具有基本许可权的角色。您必须先分配到组织，然后才能被授予组织内空间的其他许可权。有关详细信息，请参阅[用户和角色](index.html#userroles)。</dd>
<dt>域</dt>
<dd>在分配给组织的因特网上提供路径。路径具有子域和域。子域通常是应用程序名称。域可以是系统域，也可以是为应用程序注册的定制域。<br/><p>**注**：添加定制域时，必须将 DNS 服务器配置为解析您的定制域，以指向 {{site.data.keyword.Bluemix_notm}} 系统域。这样，当 {{site.data.keyword.Bluemix_notm}} 接收到定制域的请求时，它可以将其正确路由到您的应用程序。</p></dd>
<dt>配额</dt>
<dd>表示组织的资源限制，包括可分配供组织使用的服务数和内存量。创建组织时会分配配额。组织的空间中任何应用程序和服务导致配额的使用。通过“现买现付”或“预订”套餐，可以根据您组织的需求变化来调整 Cloud Foundry 应用程序和容器的配额。</dd>
</dl>

在 {{site.data.keyword.Bluemix_notm}} 中，您可以通过以下方式，使用组织来启用用户间的协作并促进项目资源的逻辑分组：

<ul>
<li>您可以将组织中的空间、应用程序、服务、域、路径和用户集分组到一起。</li>
<li>您可以管理每个用户对空间和组织的访问权。</li>
</ul>

当您创建组织时，组织名称在 {{site.data.keyword.Bluemix_notm}} 中必须是唯一的。创建组织之后，系统会自动为您分配*组织管理员*许可权，该权限允许您编辑组织名称、删除组织以及在组织中创建空间。

删除组织时，组织内的所有空间、应用程序和服务都会删除。

{{site.data.keyword.Bluemix_notm}} 通过在组织内和组织中空间内分配用户，启用项目上的协作。您可以使用**用户**选项卡来显示和管理组织的用户。还可以通过单击**用户**选项卡上的**邀请新用户**链接来邀请用户加入组织。以下许可权可分配给组织中的用户：

<ul>
<li>组织用户</li>
<li>组织管理员</li>
<li>组织记帐管理员</li>
<li>组织审计员</li>
</ul>

####空间

在组织内，您可以使用空间来分组应用程序、服务和用户集。

在将用户添加到组织之后，您可以为其授予组织内空间的许可权。与组织类似，空间也具有可分配给用户的许可权集：

<ul>
<li>空间管理员</li>
<li>空间开发者</li>
<li>空间审计员</li>
</ul>

**注**：必须至少为用户分配一种空间许可权。

空间的**域**选项卡是分配给空间的域的只读列表。系统域始终可供空间使用，定制域也可分配给空间。在空间中创建的应用程序可能将任何列出的域用于空间。

###用户和角色
{: #userroles}

帐户所有者对组织和空间执行所有操作。

####用户类型

您可以是帐户的成员或合作者。

<dl>
<dt>成员</dt>
<dd>如果您创建了帐户，或者您被邀请加入帐户，然后从邀请进行了注册并初次体验了 {{site.data.keyword.Bluemix_notm}}，那么您是 {{site.data.keyword.Bluemix_notm}} 帐户的成员。</dd>
<dt>合作者</dt>
<dd>如果您先前通过其他帐户使用了 {{site.data.keyword.Bluemix_notm}}，但随后您被邀请加入此帐户，并且您接受了邀请，那么您是 {{site.data.keyword.Bluemix_notm}} 帐户的合作者。</dd>
</dl>

####用户角色

可以为用户分配以下许可权，以便用户在组织或空间中承担不同的用户角色：

<dl>
<dt>组织管理员</dt>
<dd>组织管理员具有以下许可权：<ul>
<li>创建或删除组织中的空间。</li>
<li>邀请用户加入组织（如果您还是组织的成员或帐户所有者）。</li>
<li>管理已经在组织中的现有用户。</li>
<li>管理组织的域。</li>
</ul>
<p>**注**：如果您的用户类型是合作者，并且先前通过其他帐户使用过 {{site.data.keyword.Bluemix_notm}}，那么您无法邀请用户加入组织，即便为您分配了组织管理员角色也不例外。您的用户类型必须是成员，才能邀请用户。请参阅<a href="../troubleshoot/accessing.html#tr_adduser">无法向组织添加用户</a>，以获取有关如何解决此问题的信息。</p>
</dd>
<dt>记帐管理员</dt>
<dd>记帐管理员有权查看组织的运行时和服务使用情况信息。</dd>
<dt>组织审计员</dt>
<dd>组织审计员有权查看空间中的应用程序和服务内容。</dd>
<dt>空间管理员</dt>
<dd>空间管理员具有以下许可权：<ul>
<li>将用户添加到空间和管理用户。</li>
<li>启用空间的功能</li>
</ul>
</dd>
<dt>空间开发者</dt>
<dd>空间开发者具有以下许可权：<ul>
<li>创建、删除和管理空间内的应用程序和服务。</li>
<li>访问空间内的日志</li>
</ul>
</dd>
<dt>空间审计员</dt>
<dd>空间审计员对有关空间的所有信息具有只读访问权，如应用程序和服务的相关信息、设置、报告和日志。</dd>
</dl>

###管理组织
{: #orgmng}

作为组织管理员或帐户所有者，您可以管理您的组织。管理任务包括创建组织、重命名组织、创建空间、邀请用户加入空间以及删除现有组织。

<ul>
<li>创建组织<p>只有拥有付费帐户的用户，才能创建组织。使用付费帐户，您可以通过执行以下步骤来创建组织：</p>
<ol>
<li>转至 {{site.data.keyword.Bluemix_notm}}“仪表板”，单击右上方的图标，然后选择**管理组织**。</li>
<li>单击**创建组织**，然后按照提示创建组织。</li>
</ol>
</li>
<li>重命名组织<p>要重命名组织，请执行以下步骤：</p>
<ol>
<li>转至 {{site.data.keyword.Bluemix_notm}}“仪表板”，单击右上方的图标，然后选择**管理组织**。</li>
<li>选择要重命名的组织。</li>
<li>在**组织**字段中键入新名称，然后单击**保存**。</li>
</ol>
</li>
<li>列出成员<p>执行以下步骤来列出组织或空间的成员：
</p>
<ol>
<li>转至 {{site.data.keyword.Bluemix_notm}}“仪表板”，单击右上方的图标，然后选择**管理组织**。在**用户**选项卡中可以看到组织成员及其角色。</li>
<li>单击组织中的空间名称以查看此空间的成员及其角色。</li>
</ol>
</li>
<li>创建空间<p>您可以在组织中创建空间；例如，*dev* 空间（作为开发环境）、*test* 空间（作为测试环境）和 *production* 空间（作为生产环境）。然后，可以将应用程序与空间相关联。要创建空间，请执行以下步骤：</p>
<ol>
<li>转至 {{site.data.keyword.Bluemix_notm}}“仪表板”，单击右上方的图标，然后选择**管理组织**。</li>
<li>单击组织名称下的**创建空间**，然后按照提示创建空间。</li>
</ol>
</li>
<li>邀请用户加入空间<p>您可以邀请用户以合作者身份加入您的组织。还可以将您组织中的用户添加到不同的空间中。将用户添加到哪个空间，用户就只能访问哪个空间。要将用户添加到空间中，请执行以下步骤：</p>
<ol>
<li>转至 {{site.data.keyword.Bluemix_notm}}“仪表板”，单击右上方的图标，然后选择**管理组织**。然后，单击组织中的**添加用户**，并遵循提示将用户添加到组织中。</li>
<li>将用户添加到空间中。从左侧导航窗格中选择空间，单击**添加用户**，然后按照提示将用户添加到空间中。</li>
</ol>
</li>
<li>删除现有组织<p>要删除组织，请联系 {{site.data.keyword.Bluemix_notm}} 注册和标识支持人员。</p>
<p>**注**：删除操作不可撤销。您会失去与组织相关联的所有应用程序和服务。</p>
</li>
</ul>

## 管理 {{site.data.keyword.Bluemix_notm}} Local 和 {{site.data.keyword.Bluemix_notm}} Dedicated
{: #mng}

在 {{site.data.keyword.Bluemix}} Local 或 Dedicated 环境中，可以使用管理控制台来管理资源、监视使用情况、管理用户许可权以及查看安全报告、日志、状态和升级通知。{:shortdesc}

### 访问管理控制台
{: #oc_access}

您可以通过输入以下 URL 来访问管理控制台：

`https://opsconsole.&lt;subdomain&gt;.bluemix.net/`。

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>此值是您本地或专用实例的名称。{{site.data.keyword.Bluemix}} 实例的子域名称已在上线时进行了分配。</dd>
</dl>

### 查看系统信息
{: #oc_system}

使用管理控制台可以监视系统信息。

要查看系统信息，请单击**管理 &gt; 系统信息**。

可以展开并查看有关暂挂更新、常规系统信息和 LDAP 配置详细信息的各个部分。

* 在“更新”部分中，可以查看需要您执行操作的任何暂挂更新。您还可以使用日历链接来轻松跟踪更新，以将安排的更新导入日历应用程序。

<ol>
<li>要对特定更新执行操作，请完成以下步骤：<ol type="a">
<li>单击 <strong><em>Number</em> 个暂挂更新</strong>以查看所有暂挂更新。</li>
<li>选择要执行的更新，或查看更新的详细信息，包括更新时段、安排的日期或中断状态。</li>
<li>单击<strong>设置不可用的日期</strong>以在更新时段中设置不方便应用更新的特定日期。如果设置了不可用的日期，IBM 将根据您的选择来批准并安排更新。更新得到批准并安排后，您将收到通知。</li>
<li>单击<strong>批准</strong>以批准更新（如果没有任何不可用的日期）。如果批准，那么将在安排的更新时段应用更新。更新部署开始和结束后，IBM 都会发送通知。</li>
</ol>
</li>
<li>要将安排的更新导入所选日历应用程序，请完成以下步骤：
<ol type="a">
<li>打开日历应用程序。</li>
<li>通过粘贴应用程序中“系统信息”页面上列出的**日历 URL** 来导入更新日历。或者，通过单击“日历 URL”来下载日历文件，然后使用 `.ics` 文件将其导入日历应用程序。</li>
<li>输入凭证。</li>
<li>查看安排的更新。</li>
</ol>
</li>
</ol>

* 在“常规信息”部分中，可以查看以下信息：
    * 有关 {{site.data.keyword.Bluemix_notm}} 构建的基本信息。
    * API 信息，包括版本、URL、区域和 CLI 文档的链接。
    * 有关系统和服务的共享域信息。
    * 有关应用程序总数、用户总数和组织总数的统计信息。
* 在“LDAP 配置详细信息”部分中，可以选择 LDAP 服务器，并查看有关用户和组映射的信息。如果使用的是 {{site.data.keyword.IBM}} WebID，这些信息将在“LDAP 配置详细信息”部分中予以说明。

### 查看使用情况信息
{: #oc_resource}

使用管理控制台可以监视资源和网络使用情况。

要查看资源信息，请单击**管理 &gt; 使用情况**。

在“资源监视”部分中，可以查看以下信息：

* 资源使用情况信息，例如，使用的内存量 (GB) 和磁盘空间量 (GB)。您可以查看在所有 Droplet Execution Agent (DEA) 上的平均 CPU 使用量。单击 **CPU** 磁贴即可查看每个 DEA 的 CPU 使用量。使用量最高的 DEA 列在最前面，每个 DEA 都通过其作业和 IP 地址进行标识。CPU 使用量分为三个类别，包括系统进程中所用的 CPU 量，用户进程中所用的 CPU 量，以及等待进程中所用的 CPU 量。
* 最近一天、最近一周或最近一个月的网络使用情况信息，包括流入和流出带宽。显示的数据基于公用和专用网络的流入与流出流量总和。
* 最近 10 分钟、最近一小时或最近一天 {{site.data.keyword.Bluemix_notm}} 的平均响应时间。
* 最近 10 分钟、最近一小时或最近一天 {{site.data.keyword.Bluemix_notm}} 的平均每秒事务数。

### 查看报告
{: #oc_report}

您可以查看 {{site.data.keyword.Bluemix_notm}} 实例的安全报告和日志，例如 DataPower&trade;、防火墙和登录审计。

要查看报告和日志，请单击**管理 &gt; 报告和日志**。

从以下选项中进行选择：

* 可以从字段中选择开始日期和结束日期，以过滤出要显示的报告和日志。
* 可以从左侧导航窗格中展开并查看各种报告。
* 可以在报告和日志集合中进行搜索。搜索既适用于报告名称，也适用于报告和日志内包含的文本内容。您还可以选择按**管理事件**、**DataPower 报告**、**防火墙**和**登录审计**来过滤搜索。
* 显示报告或日志时，可以单击报告右上方的 ![下载](images/icon_download.png) 图标进行下载。

### 查看状态
{: #oc_status}

您可以通过管理控制台来监视 {{site.data.keyword.Bluemix_notm}} 实例的状态。您还可以预订 RSS 订阅源来获取通知，这样就不必检查是否有通知。

要查看 {{site.data.keyword.Bluemix_notm}} 实例的状态，请完成以下步骤：

1. 在管理控制台的右上角，单击**概要文件设置**图标。

2. 然后，单击**状态**。

这将显示“系统状态”页面。左侧窗格中显示各区域上运行时和服务的状态以及 {{site.data.keyword.Bluemix_notm}} 实例的状态。右侧窗格中显示通知。

3. 如果已为浏览器配置 RSS 订阅源相关设置，那么可以预订 RSS 订阅源来获取通知。在通知列表的左上角，找到**更新**右侧的 ![RSS](images/icon_RSS.png) 图标，然后选择以下某项操作：

* 将 ![RSS](images/icon_RSS.png) 图标拖入 RSS 阅读器。
* 右键单击 RSS 图标，选择**复制链接地址**，然后将 URL 粘贴到 RSS 阅读器中。

4. 过滤要显示的通知。单击通知列表右上方的**过滤器**。然后，通过键入要在通知中找到的字词（例如“maintenance”），即可缩小搜索范围在通知列表中进行搜索。也可以通过单击来选择是要按**类型**、**区域**、**类别**、**开始日期**还是**结束日期**显示通知。

### 管理“目录”
{: #oc_catalog}

您可以管理用户可以在 {{site.data.keyword.Bluemix_notm}}“目录”中查看哪些 {{site.data.keyword.Bluemix_notm}} 服务和入门模板。

要使用管理控制台来管理“目录”，请单击**管理 &gt; 目录管理**。

选择服务或入门模板磁贴，以编辑服务或入门模板套餐可视性。要编辑可视性，请从以下选项中进行选择：
* 要显示隐藏的服务或入门模板以使用户可在“目录”中进行查看，请选择**启用所有套餐**。
* 要隐藏服务或入门模板以使用户无法在 {{site.data.keyword.Bluemix_notm}}“目录”中进行查看，请选择**禁用所有套餐**。
* 要控制单个套餐的可视性，请选择套餐名称，然后使用下拉菜单来选择**对所有组织启用**、**对所有组织禁用**或**对特定组织启用套餐**。

### 管理组织
{: #oc_organizations}

您可以通过创建和删除组织，向组织添加管理员以及监视配额使用情况来管理组织。

要使用管理控制台来管理组织，请单击**管理 &gt; 组织管理**。

可以展开并查看各个部分。您还可以查看和管理组织的配额计划。

* 要创建新组织并添加管理员，请单击<strong>创建组织</strong>。输入组织的名称，接着输入要添加为管理员的人员的姓名或电子邮件。可以通过输入并选择多个姓名来添加多个管理员。单击<strong>创建组织</strong>以保存更改并创建组织。
* 在“配额监视”部分中，可以展开该部分并查看以下信息：
    * 环境内存使用情况。此部分详细描述了整个系统环境的内存使用情况。图表提供的信息包括已用系统内存量、系统内存总量、已用配额和分配的配额总量。以下术语列表定义了图表中显示的内存使用量的类型。
	<dl>
	<dt><strong>已用系统内存量</strong></dt>
	<dd>环境使用的物理内存量。</dd>
	<dt><strong>系统内存总量</strong></dt>
	<dd>环境可用的物理内存总量。</dd>
	<dt><strong>部署的配额</strong></dt>
	<dd>在所有组织中为所有部署的应用程序分配的内存总和。
	部署的配额总和可能会超过环境的物理系统内存总量。例如，如果系统内存总量为 16 GB，而您对总共 5 个不同组织分别分配 4 GB 的内存，那么配额总量会超过针对所有组织分配的系统内存总量。但是，在许多情况下，组织可能不会使用单独分配给每个组织的配额总量。此外，也不是所有组织都会同时使用分配的内存配额总量。</dd>
	<dt><strong>配额总量</strong></dt>
	<dd>在所有组织中分配的内存总量。</dd>
	</dl>
	* 组织内存使用情况。此部分详细描述了组织级别的内存使用情况。可以查看配额限额总量和为每个组织部署的配额。该图表提供的信息按每个组织的最高内存使用量列出，缺省情况下，使用内存量最多的组织列在最前面。可以按**最高内存使用量**和**多余内存分配量**进行排序。
	<dl>
	<dt><strong>最高内存使用量</strong></dt>
	<dd>使用此选项可识别内存使用量最高的组织。
	按最高内存使用量排序可识别使用内存量最多的组织。此列表按部署的配额进行排序。</dd>
	<dt><strong>多余内存分配量</strong></dt>
	<dd>使用此选项可识别其配额计划大于需求的组织。	按多余内存分配量排序可识别在为组织分配的配额中所使用的内存量最低的组织。</dd>
	</dl>
* 要更改组织的配额计划，请在“组织内存使用情况”部分中，单击您要编辑的组织所对应的图表中的条形，或者从“组织列表”部分中选择组织的名称。在“编辑组织”页面上，可以更改配额计划，更改组织的名称，以及添加或除去管理员。如果所选的配额计划无法满足组织的当前使用量，那么您会收到一条消息。要保存在“编辑组织”页面上进行的任何更改，请单击**保存**。
* 在“组织列表”部分中，可以查看 {{site.data.keyword.Bluemix_notm}} 环境中的所有组织。
	* 要删除组织，请单击“操作”列中的 ![删除](images/icon_trash.png)。
	* 要查看并编辑组织的配额计划，请在列表中单击组织的名称。
	* 要编辑组织的名称，以及添加或除去管理员，请在列表中单击组织的名称。

### 管理用户和许可权
{: #oc_useradmin}
您可以通过 LDAP 将公司用户注册表中的用户添加到 {{site.data.keyword.Bluemix_notm}} 实例。您可以添加单个用户或添加用户组，还可以查看用户许可权。如果分配给您的权限是 `admin` 许可权，那么您还可以设置和管理其他用户的许可权。

要使用管理控制台来管理用户，请单击**管理 &gt; 用户管理**。

“用户管理”页面显示本地或专用实例的所有用户。还会显示每个用户的许可权。许可权可以为以下值：无、`Admin`、`Catalog`、`Login`、`Reports` 和 `Users`。可以启用这些许可权，或者可以授予用户该许可权的 `view` 或 `write` 能力，如图标所示。有关每种类型的描述和图标说明，请参阅[许可权](#permissions)。

从以下选项中进行选择：
* 查找用户。您可以使用顶部的**搜索**字段在表中查找用户。
* 添加用户。如果您拥有 `admin` 许可权或具有 `write` 能力的 `users` 许可权，那么可以添加用户。要添加单个用户或用户组，请单击**添加单个用户**或**添加用户组**。在**搜索**字段中，键入要搜索的用户名或组名，然后从**组织**列表中选择要将用户或用户组添加到其中的组织。找到要添加的用户或组后，单击用户名，然后单击**添加一个用户**或**添加多个用户**以进行添加。如果组中的用户数超过 50 个，那么可通过后台批处理作业进行添加。添加操作成功后，即可在表中查看和搜索所添加的用户或组。所添加的用户没有分配的许可权。
* 编辑许可权和组织。如果您拥有 `admin` 许可权，那么可以编辑其他用户的许可权和组织。要编辑许可权，请找到用户，然后单击用户名。要启用或禁用许可权，请在打开的窗口中选择以下选项：
	* 从列表中选择**打开**，以启用许可权。
	* 从列表中选择**读取**，以允许用户拥有该许可权的 `view`（只读）能力，或者选择**写入**，以允许用户拥有该许可权的 `write`（编辑或添加和除去）能力。
	* 选择**关闭**，以禁用许可权。要编辑组织，请从以下选项中进行选择：
	* 将用户添加到组织，方法是使用搜索字段来查找组织，单击选择选项，然后单击**添加**。
	* 通过单击 ![“除去”，用减号表示](images/icon_remove.png) 图标，从组织中除去用户。完成后，单击**保存**。
* 除去用户。如果您拥有 `admin` 许可权或具有 `write` 能力的 `users` 许可权，那么可以除去用户。要除去用户，请找到该用户，单击 ![删除](images/icon_trash.png) 图标，然后单击**除去**。

#### 许可权
{: #permissions}

可以为用户分配以下许可权：

| **用户许可权** | **描述** |
|-----------------|-------------------|
| Admin | 拥有 `admin` 许可权的用户可以编辑其他用户的许可权。 |
| Catalog | 可以为拥有 `catalog` 许可权的用户分配 `view` 或 `write`（修改）本地或专用实例中哪些服务可用的能力。 |
| Login | 拥有 `login` 许可权的用户可以登录到管理控制台。没有此许可权的用户无法登录。 |
| Reports | 可以为拥有 `reports` 许可权的用户分配 `view` 或 `write`（修改）安全报告的能力。 |
| Users | 可以为拥有 `users` 许可权的用户分配 `view` 用户列表或 `write`（添加或除去）用户的能力。此许可权不允许设置其他用户的许可权。|

*表 1. 许可权*

可以启用这些许可权，或者可以授予用户该许可权的 `view` 或 `write` 能力，如以下图标所示：

* 许可权旁边的 ![“已启用”，用复选标记表示](images/icon_enabled.png) 图标表示已启用。
* ![“查看”，用眼睛表示](images/icon_read.png) 图标表示用户具有该许可权的 `view`（只读）能力。
* ![“写入”，用画笔表示](images/icon_write.png) 图标表示用户具有该许可权的 `write`（编辑、添加或除去）能力。

### 使用 Admin REST API 管理用户
{: #usingadminapi}

您可以使用 `Admin` REST API 为 {{site.data.keyword.Bluemix_notm}} 实例添加和除去用户。为了能够从命令行执行基本操作，提供了试验性 `Admin` REST API 端点和 JSON 响应。本信息的示例中的端点和 URL 可能会发生变化，也可能会临时通知停止使用。

下面是使用后续示例时所需的必备工具。也可以选择使用其他工具。
* cURL - 将 REST API 请求作为命令进行输入。cURL 是一个免费的实用程序，可用于通过命令行界面将 HTTP 请求发送到服务器并接收服务器响应。可以从 [cURL 下载站点](http://curl.haxx.se/download.html){: new_window}来下载 cURL。
* Python - 使用 Python 精细打印 JSON 工具。此可选工具接受 JSON 文本作为输入，并提供易读输出。可以从 [Python 下载站点](https://www.python.org/downloads){: new_window}来下载 Python。

#### 登录到管理控制台

运行任何 `Admin` API 请求之前，都必须登录到管理控制台。如果您拥有 `admin` 许可权或具有 `write` 能力的 `users` 许可权，那么可以添加或除去用户。必须拥有 `admin` 许可权，才能编辑其他用户的许可权。

要登录到管理控制台，可以在 `https://<your_host>.ibm.com/login` 端点上使用基本访问认证。服务器会使用您的会话返回 cookie。您使用该 cookie 来执行所有管理控制台操作。

**注：**如果几个小时不使用会话，会话将变为无效。

要登录到管理控制台，请运行以下命令：

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://<your_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>user_id</em>:<em>password</em></dt>
<dd class="pd">接受用户标识和密码，并发送基本授权头。</dd>


<dt class="pt dlterm">-c <em>filename</em></dt>
<dd class="pd">将指定的用户标识和密码作为 cookie 存储在指定的文件中。</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">发送 Accept 头。</dd>

</dl>

以下示例显示了此命令的输出：```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

#### 列出组织
{: #listingorg}

添加用户时，必须指定组织。可以使用 `Admin` REST API 来列出所有组织。您必须拥有具有 `read` 能力的 `users` 许可权，才能列出组织。要列出所有组织，请运行以下命令：

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">将先前使用 <samp class="ph codeph">-c</samp> 选项存储到文件中的用户标识和密码作为 cookie 传递到 HTTP 服务器。</dd>

</dl>

对于每个组织，结果会包含以下信息：
* `"guid"`：组织的 GUID
* `"name"`：组织的名称

以下示例显示了此命令的输出：```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

#### 列出用户
{: #listingusr}

您可以使用 `Admin` REST API 来列出已注册的用户，以确定用户是否已添加到 {{site.data.keyword.Bluemix_notm}} 环境。您必须拥有具有 `read` 能力的 `users` 许可权，才能列出已注册的用户。要列出所有用户，请运行以下命令：

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">将先前使用 <samp class="ph codeph">-c</samp> 选项存储到文件中的用户标识和密码作为 cookie 传递到 HTTP 服务器。</dd>
</dl>

对于每个注册用户，结果会包含以下信息：
* `"first_name"`（名字）和 `"last_name"`（姓氏）
* `"user_id"`：用户标识和电子邮件地址
* `"guid"`：组织的 GUID。
* `"permissions"`：分配给管理控制台的用户的许可权。

以下示例显示了此命令的输出：

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
},
                {
                    "display": "ops.catalog.write"
},
                {
                    "display": "ops.reports.write"
},
                {
                    "display": "ops.catalog.read"
},
                {
                    "display": "ops.users.write"
},
                {
                    "display": "ops.reports.read"
},
                {
                    "display": "ops.login"
},
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

#### 添加用户

您可以使用 `Admin` REST API 将用户添加到 {{site.data.keyword.Bluemix_notm}} 实例。必须拥有具有 `write` 能力的 `users` 许可权，才能添加用户。

您可以添加一个用户或用户列表。可以将用户添加到单个组织或多个组织。--> 要添加用户，必须提供以下信息：

* 用户的 first_name（名字）和 last_name（姓氏）。通过[列出用户](index.html#listingusr)来提供 `"first_name"` 和 `"last_name"`。
* 电子邮件地址和用户标识：通过[列出用户](index.html#listingusr)来提供 `"user_id"`（电子邮件地址和用户标识都是如此）。
* `"guid"`。通过[列出用户](index.html#listingorg)来提供组织的 GUID。

您需要使用 JSON 文件来提供信息。

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">将先前使用 <samp class="ph codeph">-c</samp> 选项存储到文件中的用户标识和密码作为 cookie 传递到 HTTP 服务器。</dd>
</dl>

<ol>
<li>创建 JSON 文件来包含具有正确 JSON 格式的信息。<p>例如，创建名为 `user.json` 的文件来包含以下内容：</p>
<code>
{
    "members": [
        {
            "emails": [
"some_user_id@domain.com"
],
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</code><br/><br/>
</li>
<li>通过运行以下命令，将 JSON 文件的内容发布到用户的端点：<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<your_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v</dt>
<dd class="pd">指定详细输出。</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">指定 POST 请求（覆盖缺省 GET 请求）。</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">指定 Content-Type 头，本例中为 JSON。</dd>


<dt class="pt dlterm">-d *data*</dt>
<dd class="pd">指定要通过 POST 请求发送到 HTTP 服务器的数据，本例中为 `user.json` 文件。</dd>

</dl>



以下示例显示了此命令的输出：

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; vary: X-HTTP-Method-Override
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 19:32:54 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

#### 除去用户

您可以使用 `Admin` REST API 从 {{site.data.keyword.Bluemix_notm}} 实例中除去用户。必须拥有具有 `write` 能力的 `users` 许可权，才能除去用户。

要除去用户，必须提供用户的用户标识。运行以下命令：

`curl -v -b ./cookies.txt -X DELETE https://<your_host>.ibm.com/codi/v1/users?user_id=<some_user_id@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">指定 DELETE 请求。</dd>
</dl>

以下示例显示了此命令的输出：

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 &gt; DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 &gt; User-Agent: curl/7.37.1
 &gt; Host: localhost:3000
 &gt; Accept: */*
 &gt; Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 &gt; 
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 21:01:09 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 1922 msec
 &lt; 
 ```
{: screen}

### 使用 cf CLI 管理用户
{: #usingadmincli}

您可以将 Cloud Foundry 命令行界面与 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件一起使用来管理 {{site.data.keyword.Bluemix_notm}} 环境的用户。例如，可以从 LDAP 注册表添加用户。

开始之前，请先安装 cf 命令行界面。{{site.data.keyword.Bluemix_notm}} 管理 CLI 插件需要 cf V6.11.2 或更高版本。[下载 Cloud Foundry 命令行界面](https://github.com/cloudfoundry/cli/releases){: new_window}

**限制：**Cygwin 不支持 Cloud Foundry 命令行界面。请在非 Cygwin 命令行窗口中使用 Cloud Foundry 命令行界面。

#### 添加 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件

安装了 cf 命令行界面后，可以添加 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件。

完成以下步骤来添加存储库并安装该插件：

<ol>
<li>要添加 {{site.data.keyword.Bluemix_notm}} 管理插件存储库，请运行以下命令：<br/><br/><code>
cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 实例的 URL 的子域。</dd>
</dl>
</li>
<li>要安装 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件，请运行以下命令：<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

#### 使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件

您可以使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件来添加或除去用户、分配或取消分配组织中的用户，以及执行其他管理任务。要查看命令的列表，请运行以下命令：

`cf plugins`
{: codeblock}

有关命令的其他帮助，请使用 `--help` 选项。

#### 连接并登录到 {{site.data.keyword.Bluemix_notm}}

您必须连接并登录到（如果尚未这样做）管理 CLI 插件后，才能使用该插件来管理用户。

<ol>
<li>要连接到 {{site.data.keyword.Bluemix_notm}}> API 端点，请运行以下命令：<br/><br/>
<code>
cf api https://api.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 实例的 URL 的子域。</dd>
</dl>
<p>您可以查看管理控制台的“资源和信息”页面，以获取正确的 URL。此 URL 显示在“API 信息”部分的 **API URL** 字段中。</p>
</li>
<li>使用以下命令登录到 {{site.data.keyword.Bluemix_notm}}：<br/><br/>
<code>
cf login
</code>
</li>
</ol>

#### 添加用户

您可以从 LDAP 注册表向 {{site.data.keyword.Bluemix_notm}} 环境添加用户。输入以下命令：

`cf bluemix-admin-add-user <user_name> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP 注册表中用户的名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其添加用户的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：**您还可以将 **baau** 用作较长 **bluemix-admin-add-user** 命令名的别名。

#### 除去用户

您可以通过输入以下命令从 {{site.data.keyword.Bluemix_notm}} 环境中除去用户：

`cf bluemix-admin-remove-user <user_name>`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>

</dl>

**提示：**您还可以将 **baru** 用作较长 **bluemix-admin-remove-user** 命令名的别名。

#### 添加和删除组织

可以添加和删除组织。

* 要添加组织，请输入以下命令：

`cf Bluemix-admin-create-organization <organization> <manager>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要添加的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">组织的管理员的用户名。</dd>
</dl>

**提示：**您还可以将 **baco** 用作较长 **bluemix-admin-create-organization** 命令名的别名。

* 要删除组织，请输入以下命令：

`cf Bluemix-admin-delete-organization <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要删除的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：**您还可以将 **bado** 用作较长 **bluemix-admin-create-organization** 命令名的别名。

#### 向组织分配用户

您可以将 {{site.data.keyword.Bluemix_notm}} 环境中的用户分配给特定组织。输入以下命令：

`cf bluemix-admin-set-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其分配用户的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">有关 {{site.data.keyword.Bluemix_notm}} 用户角色和描述的信息，请参阅[角色](#roles)。</dd>
</dl>

**提示：**您还可以将 **baso** 用作较长 **bluemix-admin-set-org** 命令名的别名。

#### 取消向组织分配用户

您可以取消将 {{site.data.keyword.Bluemix_notm}} 环境中的用户分配给特定组织。输入以下命令：

`cf bluemix-admin-unset-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其分配用户的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">有关 {{site.data.keyword.Bluemix_notm}} 用户角色和描述的信息，请参阅[角色](#roles)。</dd>
</dl>

**提示：**您还可以将 **bauo** 用作较长 **bluemix-admin-unset-org** 命令名的别名。

#### 角色

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">组织管理员。组织管理员有权执行以下操作：<ul>
<li>创建或删除组织中的空间。</li>
<li>邀请用户加入组织并管理用户。</li>
<li>管理组织的域。</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">记帐管理员。记帐管理员可以查看组织的运行时和服务使用情况信息。</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">组织审计员。组织审计员可以查看空间中的应用程序和服务内容。</dd>
</dl>

#### 设置组织的配额

可以为特定组织设置使用量配额。

`cf bluemix-admin-set-quota <organization> <plan>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要为其设置配额的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">组织的配额计划。</dd>
</dl>

**提示：**您还可以将 **basq** 用作较长 **bluemix-admin-set-quota** 命令名的别名。

#### 添加、删除和检索报告

可以添加、删除和检索安全报告。
* 要添加报告，请输入以下命令：

`cf bluemix-admin-add-report <category> <date> <PDF|TXT|LOG> <RTF>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">报告的类别。如果名称中有空格，请使用引号将名称括起。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">报告日期，格式为 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">要上传的报告 PDF、文本文件或日志文件的路径。</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">用于包含富文本格式 (RTF) 版本的 PDF 的选项。仅当包含报告 PDF 的路径时，此选项才适用。RTF 版本用于建立索引和执行搜索。</dd>
</dl>

**提示：**您还可以将 **baar** 用作较长 **bluemix-admin-add-report** 命令名的别名。

* 要删除报告，请输入以下命令：

`cf bluemix-admin-delete-report <category> <date> <name>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">报告的类别。如果名称中有空格，请使用引号将名称括起。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">报告日期，格式为 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">报告的名称。</dd>
</dl>

**提示：**您还可以将 **badr** 用作较长 **bluemix-admin-delete-report** 命令名的别名。

* 要检索报告，请输入以下命令：

`cf bluemix-admin-retrieve-report <category> <date> <name>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">报告的类别。如果名称中有空格，请使用引号将名称括起。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">报告日期，格式为 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">报告的名称。</dd>
</dl>

**提示：**您还可以将 **barr** 用作较长 **bluemix-admin-retrieve-report** 命令名的别名。

#### 对所有组织启用和禁用服务

您可以针对所有组织启用或禁用在 {{site.data.keyword.Bluemix_notm}}“目录”中显示的某个服务。

* 要针对所有组织启用在 {{site.data.keyword.Bluemix_notm}}“目录”中显示的某个服务，请输入以下命令：

`cf bluemix-admin-enable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要启用的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
</dl>

**提示：**您还可以将 **baesp** 用作较长 **bluemix-admin-enable-service-plan** 命令名的别名。

* 要针对所有组织禁用在 {{site.data.keyword.Bluemix_notm}}“目录”中显示的某个服务，请输入以下命令：

`cf bluemix-admin-disable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要禁用的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
</dl>

**提示：**您还可以将 **badsp** 用作较长 **bluemix-admin-disable-service-plan** 命令名的别名。

#### 添加、除去和编辑组织的服务可视性

对于能够在 {{site.data.keyword.Bluemix_notm}}“目录”中查看特定服务的组织的列表，可以在其中添加或除去组织。您还可以编辑和替换特定组织可以在 {{site.data.keyword.Bluemix_notm}}“目录”中查看的服务列表。

* 要允许某个组织在 {{site.data.keyword.Bluemix_notm}}“目录”中查看特定服务，请输入以下命令：

`cf bluemix-admin-add-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要为其添加可视性的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要添加到服务的可视性列表的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：**您还可以将 **baaspv** 用作较长 **bluemix-admin-add-service-plan-visibility** 命令名的别名。

* 要在 {{site.data.keyword.Bluemix_notm}}“目录”中除去某个服务对组织的可视性，请输入以下命令：

`cf bluemix-admin-remove-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要除去其可视性的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要从中除去服务的可视性列表的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：**您还可以将 **barspv** 用作较长 **bluemix-admin-remove-service-plan-visibility** 命令名的别名。

* 要替换一个组织或多个组织的所有现有可视服务，请使用以下命令：

`cf bluemix-admin-edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>`
{: codeblock}

**注：**此命令会将指定组织的现有可视服务替换为在命令中指定的服务。

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要使其可视的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要为其添加可视性的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。可以通过在命令中输入其他组织名称或 GUID，对多个组织启用服务可视性。</dd>
</dl>

**提示：**您还可以将 **baespv** 用作较长 **bluemix-admin-edit-service-plan-visibility** 命令名的别名。
