---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 管理 {{site.data.keyword.Bluemix_notm}} Local 和 {{site.data.keyword.Bluemix_notm}} Dedicated
{: #mng}
*上次更新时间：2016 年 5 月 16 日*

如果您具有 {{site.data.keyword.Bluemix_notm}} Local 或 {{site.data.keyword.Bluemix_notm}} Dedicated 的管理员访问权，请转至**管理**页面来管理资源、监视配额使用情况、管理用户许可权、安排升级通知，以及查看安全报告和日志等。您可以通过创建空间并设置[用户角色和许可权](index.html#oc_useradmin)来管理组织；请参阅[管理组织](../admin/orgs_spaces.html)。
{:shortdesc}

*表 1. 用于管理 {{site.data.keyword.Bluemix_notm}} Local 或 Dedicated 实例的管理任务*

| 我能执行哪些操作？ | 详细信息 |    
|----------------|---------|
|监视系统使用情况 | 单击**管理 &gt; 使用情况**。查看系统信息、监视 CPU 使用情况以及计划使用情况，以便做出最佳业务决策。请参阅[查看使用情况信息](index.html#oc_resource)。|
|管理目录 | 单击**管理 &gt; 目录管理**可管理哪些服务对用户和组织可视。请参阅[管理目录](index.html#oc_catalog)。|
|管理组织 | 单击**管理 &gt; 组织管理**可创建组织、监视组织配额以及基于需求快速做出决策。请参阅[管理组织](index.html#oc_organizations)。|
|创建空间和分配用户角色 | 单击**帐户和支持**图标 ![帐户和支持](../support/images/account_support.svg)，然后选择**管理组织**可在您的组织内创建空间。添加用户并为用户分配组织和空间角色。请参阅[管理组织](../admin/orgs_spaces.html)。 |
|对管理用户许可权进行管理 | 单击**管理 &gt; 用户管理**可添加用户、除去用户和调整用户许可权。请参阅[管理用户和许可权](index.html#oc_useradmin)。 |
|查看报告和日志 | 单击**管理 &gt; 报告和日志**可查看针对您实例的安全报告和审计日志。请参阅[查看报告](index.html#oc_report)。 |
|查看系统信息 | 单击**管理 &gt; 系统信息**可查看系统信息，例如暂挂更新数、实例的名称和版本、区域、API URL、CLI URL、LDAP 配置详细信息、组和用户映射、统计信息以及共享域。还可以访问日历订阅源和事件预订来扩展“暂挂更新”部分中的通知。请参阅[查看系统信息](index.html#oc_system)。 |
|扩展通知和设置事件预订 | 单击**管理 &gt; 系统信息 &gt; *Number* 个暂挂更新**。可以使用 Web Hook 来与所选 Web Service 集成，以设置某个更新或事件的事件通知预订。请参阅[通知和事件预订](index.html#oc_eventsubscription)。 |


## 通知和事件预订
{: #oc_eventsubscription}

您始终可以通过检查“状态”页面来了解环境的状态。{{site.data.keyword.Bluemix_notm}} 还会向“管理”页面的“通知”区域发送有关事件（例如，安排的维护和升级）的通知。事件在“管理”页面上进行报告。

### 通知

可以查看 IBM 发来的有关您本地或专用环境的通知，以监视您环境的状态。查看下表以获取有关不同类型通知的信息以及通知发布位置。

*表 2. 事件类型和通知方法*

| **事件类型** | **通知方法** |       
|-----------------|-------------------|
| 维护更新 | 您将在“管理”页面的“通知”中获得有关即将到来的维护更新的警报。转至**管理**页面，然后选择**通知**图标 ![通知](images/icon_announcement.svg)。要查看暂挂和完成的通知的完整列表和历史记录，请单击**管理 &gt; 系统信息** &gt; *数字* **个更新暂挂**。您可以通过设置事件预订来扩展通知功能，此事件预订将“管理”页面中的维护更新警报与所选 Web Service 集成在一起，以将消息路由到帮助台电子邮件地址或向所选电话号码发送短信。 |
| 严重事件 | 您将在“状态”页面上获得有关严重事件的警报。单击**帐户和支持**图标 ![帐户和支持](../support/images/account_support.svg)，然后选择**状态**。您可以通过设置事件预订来扩展通知功能，此事件预订将“状态”页面中的事件警报与所选 Web Service 集成在一起，以将消息路由到帮助台电子邮件地址或向所选电话号码发送短信。 |  
| 状态 | 可以查看平台、服务和您的 {{site.data.keyword.Bluemix_notm}} 实例的最新状态。单击**帐户和支持**图标 ![帐户和支持](../support/images/account_support.svg)，然后选择**状态**。  |

### 设置事件预订

可以使用实现 Web Hook 的事件预订，扩展发送到“管理”页面和“状态”页面的通知的功能。Web Hook 会将通知直接路由到所选目标，例如帮助台电子邮件地址（通过电子邮件）或电话号码（通过短信）。可以定制通知类型（特别是维护更新或严重事件警报）和通知中包含的信息。

要使用 Web Hook 来设置特定事件预订，请完成以下步骤：

* 对于维护更新通知，请转至**系统信息** &gt; *数字* **个更新暂挂**，然后单击**预订**图标 ![预订](images/icon_subscribe.svg)。
* 对于事件警报通知，请单击**帐户和支持** 图标 ![帐户和支持](../support/images/account_support.svg) &gt; **状态**，然后单击**预订**图标 ![预订](images/icon_subscribe.svg)。

**注**：可以使用上述两种方法之一来访问事件预订页面以获取这两种类型的通知。

1. 单击**添加预订**。

2. 填写事件预订表单。有关表单上的字段以及要在有效内容部分中使用的值的信息，请查看以下各表：

*表 3. 事件预订表单字段*

| **字段** | **描述** |
|-----------------|-------------------|
| 类型 | 选择 Web Hook。 |
| 方法 | 选择 GET 或 POST。 |
| 事件 | 选择要预订有关更新还是事件的通知。 |
| URL | 输入要通过 Hook 连接到 Web Service 的 URL。 |
| 描述 | 添加要创建的事件预订的描述。 |
| 用户名 | 输入您的 Web Service 的用户名。如果不想使用个人凭证，那么可以设置功能标识以专门用于 {{site.data.keyword.Bluemix_notm}}。 |
| 密码 | 输入您的 Web Service 的密码。 |
| 有效内容 | 如果选择了 POST 方法，请输入特定于要使用的 Web Service 的属性，以及与属性成对的用于 IBM 通知的值。请参阅下表，以获取可用于填充通知的 IBM 值。如果未在此部分中输入信息，您会收到不含任何附加信息的通知。 |

*表 4. 有效内容部分值*

| **IBM 值** | **描述** | **事件类型** |
|----------------|----------------|------------------------|
| {{content.title}} | 消息标题 |  更新和事件  |
| {{status}} | 更新或事件的状态。 | 更新和事件 |
| {{type}} | 更新或事件 | 更新和事件 | 
| {{region}} | 受影响的区域 | 更新和事件 |
| {{content.message}} | 消息描述 |   更新和事件  |
| {{content.severity}} | 严重性分级 | 事件 |
| {{content.category}} | 受影响的服务 | 事件 |
| {{content.subCategoryName}} | 受影响的组件 | 事件 |
| {{content.scheduleWindow}} | 安排的更新日期 | 更新 |
| {{content.disruption}} | 受影响的组件 | 更新 |

保存事件预订时，您会通过借助 Web Service 设置的方法接收通知。对于事件，通知仍会发布在“状态”页面上，对于维护更新，将发布在“管理”页面的“通知”区域中。

可以选择任何保存的事件预订，并查看最近的活动。可以单击以展开任何最近活动条目来查看详细信息。详细信息中包含的内容是通知的 IBM 值，这些值可在“有效内容”部分中使用。要查看这些值，请展开最近活动条目，展开**事件**，然后展开**对象**。

## 维护更新
{: #oc_schedulemaintenance}

您可以通过转至**管理 &gt; 系统信息 &gt; *Number* 个暂挂更新**以访问**系统更新**页面，从而查看安排的和暂挂的维护更新。 

**注**：请参阅以下部分，以开始设置预先批准的维护时段。必须设置这些时段，IBM 才能安排对您环境的维护。

<dl>
<dt>非中断性更新</dt>
<dd>非中断性更新不会影响您的环境和正在运行的应用程序，也不会影响用户对您应用程序的访问。此更新类型不需要逐个批准更新，并将在“系统更新”页面中设置的预先批准的可用维护时段内应用。</dd>
<dt>中断性更新</dt>
<dd>中断性更新可能会影响您的环境、正在运行的应用程序，或影响用户对您应用程序的访问。必须安排并批准每个维护更新在分配的 21 天维护时段内执行。可以选择基于预先批准的更新时段而建议的部署日期和时间，也可以另外选择两个时间和日期，供 IBM 在安排更新时选择使用。</dd>
</dl>


### 设置预先批准的维护时段
{: #preapprovedmaintenance}

开始安排和批准更新之前，必须设置预先批准的维护时段。非中断性更新会安排在预先批准的时间内执行。非中断性更新不会影响您的环境和正在运行的应用程序，也不会影响用户对您应用程序的访问。此更新类型不需要逐个批准更新，并将在“系统更新”页面中设置的预先批准的可用维护时段内应用。

需要在一周中至少设置 3 天，并且至少设置 24 小时的可用小时数。例如，可以在不同的三天设置三个 8 小时时段，也可以在不同的四天设置 6 小时时段。为了确保这些时段有足够的时间来应用更新，每个时段的持续时间必须至少为 4 小时。

1. 转至**管理 &gt; 系统信息 &gt; *Number* 个暂挂更新 &gt; 管理可用性**。
2. 展开**管理可用更新时段**部分。
3. 单击**添加新时段** ![添加新时段](images/add-new.png)。
4. 通过选择时段的频率、持续时间和开始时间，设置第一个可用时段。
5. 单击**提交**。
6. 重复此过程，直到满足每周时段数的最低要求。

### 设置不可用的维护时段

设置了预先批准的可用维护时段后，可以选择设置您的环境不可用于更新的特定日期和时间。例如，可选择不希望应用任何维护的高流量周末或假期，以确保应用程序可供用户使用。

1. 转至**管理 &gt; 系统信息 &gt; *Number* 个暂挂更新 &gt; 管理可用性**。
2. 展开**管理不可用更新时段**部分。
3. 单击**添加新时段** ![添加新时段](images/add-new.png)。
4. 通过选择时段的频率、持续时间和开始时间，设置不可用时段。
5. 单击**提交**。

### 安排和批准更新
{: #scheduleandapprove}

设置了预先批准的维护时段后，非中断性更新将自动安排在这些时间内执行。无需您对这些类型的更新进行明确批准。然而，您可以查看每个维护更新的详细信息，包括要更新的内容、更新所需时间以及安排更新执行的时间。 

要查看非中断性更新的详细信息，请完成以下步骤：

1. 转至**管理 &gt; 系统信息 &gt; *Number* 个暂挂更新**。
2. 确定其**需要客户安排**设置为**否**的所有更新行。
3. 选择该更新所在的行以查看详细信息。

中断性更新可能会影响您的环境、正在运行的应用程序，或影响用户对您应用程序的访问。必须安排并批准每个维护更新在分配的 21 天维护时段内执行。可以选择基于预先批准的更新时段而建议的部署日期和时间，也可以另外选择两个时间和日期，供 IBM 在安排更新时选择使用。

对于需要批准的中断性更新，请完成以下步骤：

1. 转至**管理 &gt; 系统信息 &gt; *Number* 个暂挂更新**。
2. 确定其**需要客户安排**设置为**是**的所有更新行。
3. 选择该更新所在行，以查看更新的详细信息，包括更新描述、建议的更新日期和时间、受影响的组件以及更新的持续时间。
4. 选择**安排和批准**。
5. 从以下选项中进行选择：**建议的日期**、**替代日期**或**所有预先批准的时段**。
6. 选择**提交**。 

根据所选项，将在接受的建议日期内、某个预先批准的时段内或者某个替代日期和时间应用更新。IBM 最终确定了安排的更新日期后，您会在**系统更新**页面上的更新详细信息中看到安排的日期。

### 为安排的更新设置日历订阅源

在“系统更新”页面上，可以通过单击**日历**图标 ![日历](images/icon_calendar.svg) 并下载 `.ics` 文件，以将安排的更新导入到所选日历应用程序，从而选择跟踪您的更新计划安排：

<ol>
<li>打开日历应用程序。</li>
<li>通过单击**日历**图标 ![日历](images/icon_calendar.svg)，然后使用 `.ics` 文件将其导入日历应用程序来下载日历文件。</li>
<li>输入凭证。</li>
<li>查看安排的更新。</li>
</ol>

您还可以使用事件预订与所选 Web Service 集成，以扩展“管理”页面的通知功能。要设置更新或事件的事件通知预订，请参阅[事件预订和通知](index.html#oc_eventsubscription)。

## 查看系统信息
{: #oc_system}

要查看系统信息，请单击**管理 &gt; 系统信息**。

可以展开并查看有关暂挂维护更新、常规系统信息和 LDAP 配置详细信息的各个部分。

### 暂挂系统更新

在“更新”部分中，可以查看需要您执行操作的暂挂更新通知数。可能会看到两种类型的维护更新：

<dl>
<dt>非中断性更新</dt>
<dd>非中断性更新不会影响您的环境和正在运行的应用程序，也不会影响用户对您应用程序的访问。此更新类型不需要逐个批准更新。这些更新将在“系统更新”页面中设置的预先批准的可用维护时段内应用。</dd>
<dt>中断性更新</dt>
<dd>中断性更新可能会影响您的环境、正在运行的应用程序，或影响用户对您应用程序的访问。您可以安排并批准每个维护更新在分配的 21 天维护时段内执行，以确保更新不会在关键业务时间内应用。可以选择基于预先批准的更新时段而建议的部署日期和时间，也可以另外选择两个时间和日期，供 IBM 在应用更新时选择使用。</dd>
</dl>

有关设置预先批准的维护时段、设置特定的不可用维护日期以及设置日历订阅源的更多信息，请参阅[维护更新](index.html#oc_schedulemaintenance)。

### 常规系统信息

在“常规信息”部分中，可以查看以下信息：

- 有关 {{site.data.keyword.Bluemix_notm}} 构建的基本信息。
- API 信息，包括版本、URL、区域和 CLI 文档的链接。
- 有关系统和服务的共享域信息。
- 有关应用程序总数、用户总数和组织总数的统计信息。

### LDAP 配置详细信息

在“LDAP 配置详细信息”部分中，可以选择 LDAP 服务器，并查看有关用户和组映射的信息。如果使用的是 {{site.data.keyword.IBM}} WebID，这些信息将在此部分中予以说明。

## 查看使用情况和报告
{: #oc_resource}

可以查看本地或专用实例和 {{site.data.keyword.Bluemix_notm}} 帐户的不同类型使用情况信息。还可下载并查看 {{site.data.keyword.Bluemix_notm}} 实例的安全报告和日志。

- 资源信息，包括磁盘空间、CPU 使用情况、网络使用情况和平均响应时间。请参阅[资源使用情况](index.html#resourceusage)。
- 每个组织的帐户使用情况，包括有使用量的运行时应用程序数、运行时 GB-小时总数以及有使用量的服务实例数。请参阅[帐户使用情况](index.html#accountusage)。
- 组织内存配额使用情况，基于已用总内存配额分配的应用程序内存，以及特定组织每个应用程序的 GB-小时使用量视图。还可以在“组织管理”页面的“配额监视”部分中查看所有组织的配额使用情况。请参阅[组织管理](../admin/index.html#orgusage)。


### 资源使用情况
{: #resourceusage}

要查看资源使用情况信息，请单击**管理 &gt; 使用情况**。

在“资源监视”部分中，可以查看以下信息：

- 资源使用情况信息，例如，使用的内存量 (GB) 和磁盘空间量 (GB)。您可以查看在所有 Droplet Execution Agent (DEA) 上的平均 CPU 使用量。单击 **CPU** 磁贴即可查看每个 DEA 的 CPU 使用量。使用量最高的 DEA 列在最前面，每个 DEA 都通过其作业和 IP 地址进行标识。CPU 使用量分为三个类别，包括系统进程中所用的 CPU 量，用户进程中所用的 CPU 量，以及等待进程中所用的 CPU 量。
- 最近一天、最近一周或最近一个月的网络使用情况信息，包括流入和流出带宽。显示的数据基于公用和专用网络的流入与流出流量总和。
- 最近 10 分钟、最近一小时或最近一天 {{site.data.keyword.Bluemix_notm}} 的平均响应时间。
- 最近 10 分钟、最近一小时或最近一天 {{site.data.keyword.Bluemix_notm}} 的平均每秒事务数。

### 帐户使用情况
{: #accountusage}

可以查看您的帐户每月在专用或本地环境中的使用情况。可以使用这些数据，根据特定组织的使用量来确定相应费用。

<ol>
<li>单击<strong>帐户和支持</strong>图标 ![帐户和支持](../support/images/account_support.svg) &gt; <strong>帐户</strong> &gt; <strong>使用情况详细信息</strong>。</li>
<li>选择要查看其数据的组织。</li>
<li>可以查看以下类别的使用情况详细信息：
<ul>
<li>有使用量的运行时应用程序数</li>
<li>运行时应用程序使用总量（GB-小时）</li>
<li>有使用量的服务实例数</li>
</ul>
</li>
<li>可选：通过使用<strong>您的云活动</strong>菜单来选择月份，查看特定月份的数据。</li>
<li>可选：单击<strong>导出数据</strong>，然后选择 <strong>CSV</strong> 或 <strong>JSON</strong> 以将所选月份的数据导出为 <code>CSV</code> 或 <code>JSON</code> 文件。</li>
</ol>

您还可以在帐户级别查看从 {{site.data.keyword.Bluemix_notm}} Public 联合的运行时、应用程序和服务的每月使用量和关联费用。可以使用这些数据，根据特定组织的使用量来确定相应费用。

<ol>
<li>单击<strong>帐户和支持</strong>图标 ![帐户和支持](../support/images/account_support.svg) &gt; <strong>帐户</strong> &gt; <strong>使用情况详细信息</strong>。</li>
<li>单击 <strong>Public</strong>。</li>
<li>选择要查看其数据的组织，或者选择<strong>所有组织</strong>来一次性查看所有组织的数据。</li>
<li>可以查看以下类别的使用情况详细信息：
<ul>
<li>有使用量的运行时应用程序数</li>
<li>运行时应用程序使用总量（GB-小时）</li>
<li>有使用量的服务实例数</li>
<li>所有联合的运行时、服务和应用程序的费用汇总</li>
</ul>
</li>
<li>可选：通过从条形图中选择月份，查看特定月份的数据。缺省情况下，将显示当月的数据。</li>
<li>可选：单击<strong>导出数据</strong>，然后选择 <strong>CSV</strong> 或 <strong>JSON</strong> 以将所选月份的数据导出为 <code>CSV</code> 或 <code>JSON</code> 文件。</li>
</ol>


### 组织使用情况
{: #orgusage}

要查看每个组织的使用情况，请单击**管理 &gt; 组织管理**，然后从**组织列表**中选择组织。在所选组织的**管理组织**页面上，可以查看以下使用情况信息：

- 当前正在使用的服务数。
- 当前正在使用的路径数。
- 内存配额图，显示已用配额量和当前未使用的配额量。
- 应用程序分配图，显示哪些应用程序包含在已用内存配额中。
- 计量应用程序使用情况图，显示三个月的报告，内容是每个已部署应用程序使用的 GB-小时。可以选择**列表视图**来查看所有应用程序的数据，包括过去三个月中每个应用程序的内存分配和计量的 GB-小时使用量。

有关查看每个组织的使用情况、调整配额计划和管理组织的更多信息，请参阅[管理组织](../admin/index.html#oc_organizations)。

### Reports
{: #oc_report}

您可以查看 {{site.data.keyword.Bluemix_notm}} 实例的安全报告和日志，例如 DataPower&trade;、防火墙和登录审计。要查看报告和日志，请单击**管理 &gt; 报告和日志**。

从以下选项中进行选择：

- 可以从字段中选择开始日期和结束日期，以过滤出要显示的报告和日志。
- 可以从导航窗格中展开并查看各种报告。
- 可以在报告和日志集合中进行搜索。搜索既适用于报告名称，也适用于报告和日志内包含的文本内容。您还可以选择按**管理事件**、**DataPower 报告**、**防火墙**和**登录审计**来过滤搜索。
- 显示报告或日志时，可以单击 ![下载](images/icon_download.png) 图标来下载报告。

下表显示了为 {{site.data.keyword.Bluemix_notm}} Local 和 {{site.data.keyword.Bluemix_notm}} Dedicated 生成的安全报告的列表。

*表 5. 安全报告列表*

| **类别** | **报告** | **描述** |      
|-----------------|-------------------|---------------------|
| 防火墙 | 防火墙登录 | 与管理员登录到 Vyatta 防火墙设备相关的事件。 |
| 防火墙 | 防火墙拒绝 | 根据适用的防火墙规则，访问请求被拒绝时，Vyatta 防火墙设备生成的事件。 |
| {{site.data.keyword.Bluemix_notm}} 管理员登录事件 | {{site.data.keyword.Bluemix_notm}} 管理员登录 | 管理员在每个 {{site.data.keyword.Bluemix_notm}} 系统上启动 SSH 会话时，操作系统生成的事件。 |
| {{site.data.keyword.Bluemix_notm}} 应用程序开发者登录事件 | {{site.data.keyword.Bluemix_notm}} 应用程序开发者登录 | {{site.data.keyword.Bluemix_notm}} 平台用户使用命令行、REST API 或 {{site.data.keyword.Bluemix_notm}} 用户界面启动会话时，{{site.data.keyword.Bluemix_notm}} 平台登录组件生成的事件。 |
| {{site.data.keyword.Bluemix_notm}} 管理员管理事件 | {{site.data.keyword.Bluemix_notm}} 管理员操作系统管理事件 | 管理员在当前工作会话中执行操作时，操作系统生成的事件。 |
| {{site.data.keyword.Bluemix_notm}} 应用程序开发者管理事件 | {{site.data.keyword.Bluemix_notm}} (Cloud Foundry) 管理事件 | 与 {{site.data.keyword.Bluemix_notm}} 平台用户使用命令行、REST API 或 {{site.data.keyword.Bluemix_notm}} 用户界面执行的操作相关的事件。 |
| {{site.data.keyword.Bluemix_notm}} 管理员数据库管理事件 | 数据库管理事件 | 与数据库管理员在 {{site.data.keyword.Bluemix_notm}} 内部数据库上执行的操作相关的事件。 |
| 管理事件 | 用户管理事件 | 与在“管理”页面上执行的用户管理操作相关的事件。 |
| 管理事件 | 目录 | 与服务“目录”更改相关的事件。 |
| 管理事件 | 安全报告管理事件 | 与在“管理”页面上执行的安全报告管理操作相关的事件。 |
| 访问审核 | 访问审核报告 | 对特权访问的审核。 |
| 变更管理 | 软件变更管理 | 变更管理活动。 |
| 密钥管理 | 定制 SSL 证书管理 | 已上传并存储的定制 SSL 证书。 |
| 加密 | 传输中的数据加密 | 已配置的传输中的数据加密。 |
| 防病毒 | 防病毒扫描报告 | 已就位的防病毒软件。 |
| 软件修订管理 | 补丁安装报告 | 已应用的软件修订。 |
| 安全事件管理 | 安全事件补救报告 | 用于安全事件管理的安全事件证据。 |

## 查看状态
{: #oc_status}

您可以查看 {{site.data.keyword.Bluemix_notm}} 环境的状态和管理控制台的状态。

### {{site.data.keyword.Bluemix_notm}} 环境状态

您可以使用 {{site.data.keyword.Bluemix_notm}}“状态”页面来监视 {{site.data.keyword.Bluemix_notm}} 实例的状态。单击**帐户和支持**图标 ![帐户和支持](../support/images/account_support.svg)，然后选择**状态**。

“状态”页面是查找通知和公告的一个中心位置，从中可了解影响 {{site.data.keyword.Bluemix_notm}} 平台以及 {{site.data.keyword.Bluemix_notm}} 中主要服务的关键事件。您可以预订 RSS 订阅源来获取通知，这样就不必检查是否有通知。有关“状态”页面和设置 RSS 订阅源的更多信息，请参阅[查看 {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status)。

### 管理控制台状态

初始部署 {{site.data.keyword.Bluemix_notm}} 环境后，系统会对用于管理环境的组件自动完成验证检查。验证检查运行后，可以转至管理控制台的“验证检查”页面来检查组件的状态。要访问该页面，请转至 <code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>，其中 `<subdomain>` 是您的本地或专用实例的名称。

您可以随时运行验证，但必须登录才能选择用于运行验证的选项。如果在添加用户、编辑组织或管理服务时遇到故障，请运行此检查以确定是否有任何组件发生故障或断开连接。可以打开支持凭单并填写检查中获得的信息，以快速解决问题。

## 管理目录
{: #oc_catalog}

您可以管理用户可以在 {{site.data.keyword.Bluemix_notm}}“目录”中查看哪些 {{site.data.keyword.Bluemix_notm}} 服务和入门模板。单击**管理 &gt; 目录管理**。

选择服务或入门模板磁贴，以编辑服务或入门模板套餐可视性。要编辑可视性，请从以下选项中进行选择：

- 要显示隐藏的服务或入门模板以使用户可在“目录”中进行查看，请选择**启用所有套餐**。
- 要隐藏服务或入门模板以使用户无法在 {{site.data.keyword.Bluemix_notm}}“目录”中进行查看，请选择**禁用所有套餐**。
- 要控制单个套餐的可视性，请选择套餐名称，然后使用下拉菜单来选择**对所有组织启用**、**对所有组织禁用**或**对特定组织启用套餐**。

<!-- staging only start -->

### 注册服务代理程序
{: #servicebrokerui}

如果您有一个服务要显示在 {{site.data.keyword.Bluemix_notm}}“目录”中，那么必须实现并注册服务代理程序。注册代理程序后，可以选择哪些组织可在本地或专用实例中访问该服务。

服务代理程序的使用方法根据其管理的服务数，或根据其是否已向 {{site.data.keyword.Bluemix_notm}} 注册而有所不同。

- 如果服务代理程序管理一个服务，那么在实现了[服务代理程序 API](http://docs.cloudfoundry.org/services/api.html){: new_window} 之后，可以使用该用户界面来注册该服务代理程序。请参阅[注册管理一个服务的服务代理程序](index.html#registerbrokerui)。
- 如果服务代理程序管理多个服务，那么在实现了服务代理程序 API 之后，不能注册该服务代理程序。请改为将 cf CLI 与 [{{site.data.keyword.Bluemix_notm}} 管理 CLI](../cli/plugins/bluemix_admin/index.html) 插件（`ba` 子命令）一起使用，或者使用[定制服务 API](index.html#servicebrokerapi)。
- 如果服务代理程序已注册，但希望对其执行更新或删除操作，请将 cf CLI 与 [{{site.data.keyword.Bluemix_notm}} 管理 CLI](../cli/plugins/bluemix_admin/index.html) 插件（`ba` 子命令）一起使用，或者使用[定制服务 API](index.html#servicebrokerapi)。

#### 注册管理一个服务的服务代理程序
{: #registerbrokerui}

要注册服务代理程序，请完成以下步骤：

<ol>
<li><a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">实现 Cloud Foundry 服务代理程序 API</a> 以支持您的服务与 {{site.data.keyword.Bluemix_notm}} 之间的通信。服务代理程序 API 是由 {{site.data.keyword.Bluemix_notm}} 使用的一组 REST 端点。<br />
<br />
<p>要实现服务代理程序时，在 <code>GET /v2/catalog</code> 的 JSON 响应中，必须提供服务和服务套餐的定义，包括要显示的服务信息。例如，查看目录 (GET) 响应的以下样本 JSON：</p>
<p><pre>
"services": [ 
   {
      "bindable":true,
      "description":"Cool Service is a data warehousing and analytics solution.",
      "id":"cool-service-id",
      "name":"coolservice",
      "tags":[
         "customer_dedicated"
      ],
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Cool company",
         "longDescription":"Cool Service is a data warehousing and analytics solution. You can quickly move your data into a next-generation columnar in-memory database and start running complex analytical queries.",
         "bullets":[
            {
               "title":"Fast and Simple",
               "description":"Cool Service uses dynamic in-memory columnar technology and innovations, such as parallel vector processing and actionable compression to rapidly scan and return relevant data."
            },
            {
               "title":"Connectivity",
               "description":"Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data right away with familiar tools."
            }
         ],
         "featuredImageUrl":"http://path/to/icon_64x64.png",
         "imageUrl":"http://path/to/icon_50x50.png",
         "mediumImageUrl":"http://path/to/icon_32x32.png",
         "smallImageUrl":"http://path/to/icon_24x24.png",
         "documentationUrl":"http://path/to/documentation.html",
         "instructionsUrl":"http://path/to/servicesample.md",
         "termsUrl":"http://path/to/terms_of_agreement.pdf",
         "media":[
            {
               "type":"youtube",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/youtube/video",
               "caption":"Using Cool Service in 60 Seconds"
            },
            {
               "type":"image",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/image_file.png",
               "caption":"Cool Service connects applications"
            },
            {
               "type":"video",
               "thumbnailUrl":"http://path/to/thumb.png",
               "caption":"Cool Service works with tables",
               "source":[
                  {
                     "type":"video/mp4",
                     "url":"http://path/to/video_file.mp4"
                  },
                  {
                     "type":"video/ogg",
                     "url":"http://path/to/video_file.ogg"
                  }
               ]
            }
         ]
      },
      "plans":[
         {
            "name":"smallplan",
            "description":"Dedicated schema and tablespace per service instance on a shared server. 1GB and 10GB of compressed database storage can hold up to 5GB and 50GB of uncompressed data respectively based on typical compression ratios.",
            "free":false,
            "id":"cool-service-plan-id",
            "metadata":{
               "bullets":[
                  "1 GB Min per instance. 10 GB Max per instance."
               ],
               "costs":[
                  {
                     "unitId":"INSTANCES_PER_MONTH",
                     "unit":"MONTHLY",
                     "partNumber":"D15UTLL"
                  }
               ],
               "displayName":"Small"
            }
         }
      ]
   }
]
}
</pre></p>
<p><strong>注</strong>：为本地或专用环境创建服务代理程序时，必须在服务定义 JSON 文件的“tags”字段中指定 `customer_dedicated`。</p>
</li>
<li>在实现服务代理程序 API 后，请转至<strong>管理</strong> &gt; <strong>目录管理</strong>。</li>
<li>单击<strong>注册服务代理程序</strong>。</li>
<li>通过在以下字段中输入值来填写表单：<ul>
<li>服务代理程序名称</li>
<li>服务代理程序 URL</li>
<li>服务代理程序用户名</li>
<li>服务代理程序密码</li>
</ul>
</li>
<li>单击<strong>连接</strong>。</li>
<li>查看服务的信息，包括可用套餐、图标和服务描述。<br />
<p><strong>注</strong>：如果需要更改服务的目录信息，请更新服务代理程序，然后通过填写表单来再次启动注册过程。</p>
</li>
<li>单击<strong>注册</strong>。</li>
<li>选择启用服务的所有套餐，或只启用特定套餐。缺省情况下，会禁用所有套餐。</li>
<li>为所有组织或特定组织启用服务实例。</li>
</ol>

现在，可以在 {{site.data.keyword.Bluemix_notm}}“目录”的“定制服务”类别中查看您的服务。转至**管理 &gt; 目录管理**，然后选择目录中的磁贴。可以启用不同套餐，并随时编辑组织的套餐可视性。

## 管理组织
{: #oc_organizations}

可以通过创建和删除组织，添加或除去组织的管理员以及监视配额使用情况来为您的业务做出最佳决策。

单击**管理 &gt; 组织管理**。

可以展开并查看各个部分。您还可以审查和管理组织的配额计划。

### 创建组织

要创建新组织并添加管理员，请完成以下步骤：

1. 单击<strong>创建组织</strong>。
2. 输入组织的名称。
3. 输入要添加为管理员的人员的姓名或电子邮件。可以通过输入并选择多个姓名来添加多个管理员。
4. 单击<strong>创建组织</strong>以保存更改并创建组织。

### 创建空间

您可以在组织中创建空间；例如，*dev* 空间（作为开发环境）、*test* 空间（作为测试环境）和 *production* 空间（作为生产环境）。然后，可以将应用程序与空间相关联。要创建空间，请完成以下步骤：

1. 转至**帐户和支持**图标 ![“帐户和支持”图标](../admin/images/account_support.svg) &gt; **管理组织**页面。
2. 选择要向其添加空间的组织。
3. 单击**创建空间**。
4. 输入空间名称。
5. 单击**创建**。

### 配额监视

在“配额监视”部分中，可以展开该部分并查看以下信息：

- 环境内存使用情况。此部分详细描述了整个系统环境的内存使用情况。图表提供的信息包括已用系统内存量、系统内存总量、已用配额和分配的配额总量。以下术语列表定义了图表中显示的内存使用量的类型。

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

- 组织内存使用情况。此部分详细描述了组织级别的内存使用情况。可以查看配额限额总量和为每个组织部署的配额。该图表提供的信息按每个组织的最高内存使用量列出，缺省情况下，使用内存量最多的组织列在最前面。可以按**最高内存使用量**和**多余内存分配量**进行排序。

	<dl>
	<dt><strong>最高内存使用量</strong></dt>
	<dd>使用此选项可识别内存使用量最高的组织。
	按最高内存使用量排序可识别使用内存量最多的组织。此列表按部署的配额进行排序。</dd>
	<dt><strong>多余内存分配量</strong></dt>
	<dd>使用此选项可识别其配额计划大于需求的组织。	按多余内存分配量排序可识别在为组织分配的配额中所使用的内存量最低的组织。</dd>
	</dl>

### 调整配额计划

要更改组织的配额计划，请完成以下步骤：

<ol>
<li>在“组织内存使用情况”部分中，单击图表中要编辑的组织所对应的条形，或者从“组织列表”部分中选择组织的名称。</li>
<li>在“管理组织”页面上，可以更改配额计划，更改组织的名称，以及添加或除去管理员。<br />
<p><strong>注</strong>：如果所选的配额计划无法满足组织的当前使用量，那么您会收到一条消息。</p>
</li>
<li>要保存在“管理组织”页面上进行的任何更改，请单击<strong>保存</strong>。</li>
</ol>

### 通过组织列表管理组织

在“组织列表”部分中，可以查看 {{site.data.keyword.Bluemix_notm}} 环境中的所有组织，并可以通过单击组织名称，对各个组织分别执行操作。

- 要删除组织，请单击“操作”列中的**删除**图标 ![删除](images/icon_trash.svg)。
- 要查看组织的配额计划和使用情况，请在列表中单击组织的名称。在所选组织的**管理组织**页面上，可以查看以下使用情况信息：

  - 当前正在使用的服务数。
  - 当前正在使用的路径数。
  - 内存配额图，显示已用配额量和当前未使用的配额量。
  - 应用程序分配图，显示哪些应用程序包含在已用内存配额中。
  - 计量应用程序使用情况图，显示三个月的报告，内容是每个已部署应用程序使用的 GB-小时。可以选择**列表视图**来查看所有应用程序的数据，包括过去三个月中每个应用程序的内存分配和计量的 GB-小时使用量。

- 要编辑组织的名称，以及添加或除去管理员，请在列表中单击组织的名称，然后按照屏幕上的提示执行操作。

## 管理用户和许可权
{: #oc_useradmin}

您可以通过 LDAP 将公司用户注册表中的用户添加到 {{site.data.keyword.Bluemix_notm}} 实例。您可以添加单个用户或添加用户组，还可以查看用户许可权。如果分配给您的是 `admin` 许可权，那么您还可以设置和管理其他用户的许可权。单击**管理 &gt; 用户管理**。

“用户管理”页面显示本地或专用实例的所有用户。还会显示每个用户的许可权。许可权可以为以下值：无、`Admin`、`Catalog`、`Login`、`Reports` 和 `Users`。可以启用这些许可权，或者可以授予用户对该许可权的 `view` 或 `write` 访问权，如图标所示。有关每种类型的描述和图标说明，请参阅[许可权](index.html#permissions)。

### 处理用户

您可以搜索现有用户、除去用户以及单个或成组添加用户。从以下选项中进行选择：

* 查找用户。您可以使用**搜索**字段在表中查找用户。

* 添加单个用户。如果您拥有 `admin` 许可权或者具有 `write` 访问权的 `users` 许可权，那么可以添加用户。

  1. 要从 LDAP 目录添加单个用户，请单击**添加用户**。
  2. 在**搜索**字段中，输入用户的电子邮件地址，然后从填充的列表中选择相应用户。
  3. 接着，在**组织**字段中，通过输入组织名称并从填充的列表中选择相应组织来选择要向其添加用户的组织。
  4. 要向所选组织添加用户，请单击**添加用户**。

  **注**：添加操作成功后，该用户会添加到表中以供您查看和搜索。所添加的用户没有分配的许可权。

* 从 LDAP 目录添加用户组。

  1. 单击**添加用户组**。
  2. 在**搜索**字段中，输入要搜索的组名，然后从填充的列表中选择相应组名。
  3. 接着，在**组织**字段中，通过输入组织名称并从填充的列表中选择相应组织来选择要向其添加用户组的组织。
  4. 要向所选组织添加用户组，请单击**添加用户**。**注**：如果组中的用户数超过 50 个，那么会通过后台批处理作业添加这些组。添加操作成功后，即可在表中查看和搜索所添加的用户或组。所添加的用户没有分配的许可权。

* 通过导入包含用户标识、用户电子邮件地址和计划向其添加用户的组织来添加用户组。

  1. 单击**导入用户**。
  2. 单击**下载模板 (.CSV)**，以下载具有可以填充的必需列的电子表格，或者创建自己的电子表格并至少包含必需的列标题：**用户标识**、**电子邮件**和**组织**。
  3. 为必需列填写用户值。如果使用的不是 LDAP 目录，请将必需列和可选列标题（**名字**和**姓氏**）用于用户导入。
  4. 保存文件，然后单击**上传文件**。
 

  **注**：输入与用户注册表中使用的值相匹配的用户标识。电子表格中的列可以按任意顺序排列，只要您包含所有必需的列即可。如果导入成功，您会收到确认消息，声明所有用户都已添加。如果成功导入了一些用户，而另一些用户未成功导入，请查看错误消息，以对无法添加的用户执行操作。

* 除去用户。如果您拥有 `admin` 许可权或者具有 `write` 访问权的 `users` 许可权，那么可以除去用户。

    1. 找到用户，然后单击 ![删除](images/icon_trash.svg) 图标。
    2. 单击**除去**。

### 许可权
{: #permissions}

可以为用户分配以下许可权：

*表 6. 许可权*

| **用户许可权** | **描述** |       
|-----------------|-------------------|
| admin | 拥有 `admin` 许可权的用户可以编辑其他用户的许可权。 |
| Catalog | 可以为拥有 `catalog` 许可权的用户分配针对本地或专用实例中哪些服务可用执行 `view`（查看）或 `write`（写入，即修改）操作的访问权。 |  
| Login | 拥有 `login` 许可权的用户可以查看“管理”页面。没有此许可权，用户无法查看“管理”菜单选项。 |
| Reports | 可以为拥有 `reports` 许可权的用户分配针对安全报告执行 `view`（查看）或 `write`（写入，即修改）操作的访问权。 |
| Users | 可以为拥有 `users` 许可权的用户分配针对用户列表执行 `view`（查看）操作或针对用户执行 `write`（写入，即添加或除去）操作的访问权。此许可权不允许设置其他用户的许可权。|


可以启用这些许可权，或者可以授予用户对该许可权的 `view` 或 `write` 访问权，如以下图标所示：

* 许可权旁边的 ![“已启用”，用复选标记表示](images/icon_enabled.svg) 图标表示已启用。
* ![“查看”，用眼睛表示](images/icon_read.svg) 图标表示用户具有对该许可权的 `view`（只读）访问权。
* ![“写入”，用画笔表示](images/icon_write.svg) 图标表示用户具有对该许可权的 `write`（编辑、添加或除去）访问权。

编辑其他用户的许可权和组织需要您具有 `admin` 许可权。要编辑许可权，请找到用户，然后单击用户名。在**编辑用户**页面中，可以启用或禁用许可权：

* 从列表中选择**打开**，以启用许可权。
* 从列表中选择**读取**，以允许用户拥有对该许可权的 `view`（只读）访问权，或者选择**写入**，以允许用户拥有对该许可权的 `write`（编辑或添加和除去）访问权。
* 选择**关闭**，以禁用许可权。

要在组织中添加或除去用户，请从以下选项中进行选择：

* 要向组织添加用户，请从表中选择相应用户名以访问**编辑用户**屏幕。接着，使用搜索字段来查找组织，从列表中选择组织，然后单击**保存**。
* 要从组织中除去用户，请从表中选择相应用户名以访问**编辑用户**屏幕。接着，对要从中除去用户的组织，单击 ![除去](images/icon_remove.svg)，然后单击**保存**。


## 使用 Admin REST API 管理用户
{: #usingadminapi}

您可以使用 `Admin` REST API 为 {{site.data.keyword.Bluemix_notm}} 实例添加和除去用户。为了能够从命令行执行基本操作，提供了试验性 `Admin` REST API 端点和 JSON 响应。本信息的示例中的端点和 URL 可能会发生变化，也可能会临时通知停止使用。

下面是使用后续示例时所需的必备工具。也可以选择使用其他工具。
* cURL - 将 REST API 请求作为命令进行输入。cURL 是一个免费的实用程序，可用于通过命令行界面将 HTTP 请求发送到服务器并接收服务器响应。可以从 [cURL 下载站点](http://curl.haxx.se/download.html){: new_window}来下载 cURL。
* Python - 使用 Python 直观显示 JSON 工具的输出。此可选工具接受 JSON 文本作为输入，并提供易读输出。可以从 [Python 下载站点](https://www.python.org/downloads){: new_window}来下载 Python。

### 登录到管理控制台

运行任何 `Admin` API 请求之前，都必须登录到管理控制台。如果您拥有 `admin` 许可权或者具有 `write` 访问权的 `users` 许可权，那么可以添加或除去用户。必须拥有 `admin` 许可权，才能编辑其他用户的许可权。

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

### 列出组织
{: #listingorg}

添加用户时，必须指定组织。可以使用 `Admin` REST API 来列出所有组织。您必须拥有具有 `read` 访问权的 `users` 许可权，才能列出组织。要列出所有组织，请运行以下命令：

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

### 列出用户
{: #listingusr}

您可以使用 `Admin` REST API 来列出已注册的用户，以确定用户是否已添加到 {{site.data.keyword.Bluemix_notm}} 环境。您必须拥有具有 `read` 访问权的 `users` 许可权，才能列出已注册的用户。要列出所有用户，请运行以下命令：

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

### 添加用户

您可以使用 `Admin` REST API 将用户添加到 {{site.data.keyword.Bluemix_notm}} 实例。您必须拥有具有 `write` 访问权的 `users` 许可权，才能添加用户。

您可以添加一个用户或用户列表。可以将用户添加到单个组织或多个组织。要添加用户，必须提供以下信息：

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
<pre>
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
</pre>
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
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

### 除去用户

您可以使用 `Admin` REST API 从 {{site.data.keyword.Bluemix_notm}} 实例中除去用户。您必须拥有具有 `write` 访问权的 `users` 许可权，才能除去用户。

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
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}


## 定制服务 API
{: #servicebrokerapi}

有三个 API 可用于注册或创建新服务、更新服务和删除服务。

所有 API 都是相对于 <code>https://console.&lt;subdomain&gt;.bluemix.net/</code> 的。

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>此值是您本地或专用实例的名称。{{site.data.keyword.Bluemix}} 实例的子域名称已在上线时进行了分配。</dd>
</dl>

## 注册新服务

要注册新服务，请使用以下 API 和代码示例。

### 路径
{: #registerroute}

```
POST /codi/v1/serviceBrokers
```
{: screen}

### 请求
{: #registerrequest}

*表 7. 字段*

| **名称** | **描述** |
|-----------------|-------------------|
| name | 服务代理程序的名称。 |
| auth_username | 用于与服务代理程序连接的用户名。 |
| auth_password | 用于与服务代理程序连接的密码。 |
| broker_url | 用于连接服务代理程序的 URL。 |
| owningOrganization | 将服务列入白名单时要使用的初始组织。 |


#### 主体
{: #registerbody}

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### 头
{: #registerheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### 响应
{: #registerresponse}

#### 状态
{: #registerstatus}

```
201 Created
```
{: screen}

#### 主体
{: #registerbody2}

```
{
  "entity": {
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

## 更新服务

要更新服务，请使用以下 API 和代码示例。

### 路径
{: #updateroute}

`PUT /codi/v1/serviceBrokers`
{: screen}

### 请求
{: #updaterequest}

*表 8. 字段*

| **名称** | **描述** |
|-----------------|-------------------|
| name | 服务代理程序的名称。此名称是创建服务时使用的名称，无法更改。 |
| auth_username | 用于与服务代理程序连接的用户名。 |
| auth_password | 用于与服务代理程序连接的密码。 |
| broker_url | 用于连接服务代理程序的 URL。 |
| owningOrganization | 将服务列入白名单时要使用的初始组织。 |


#### 主体
{: #updatebody}

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### 头
{: #updateheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### 响应
{: #updateresponse}

#### 状态
{: #updatestatus}

```
201 Created
```
{: screen}

#### 主体
{: #updatebody2}

```
{
  "entity": {
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

## 删除服务

要删除服务，请使用以下 API 和代码示例。

*表 9. 参数*

| **名称** | **描述** |
|-----------------|-------------------|
| name | 服务代理程序的名称。此名称是创建服务时使用的名称，无法更改。 |


### 路径

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

### 请求
{: #deleterequest}

#### 头
{: #deleteheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### 响应
{: #deleteresponse}

#### 状态
{: #deletestatus}

```
204 No Content
```
{: screen}

## 使用 cf CLI 管理用户
{: #usingadmincli}

您可以将 Cloud Foundry 命令行界面与 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件一起使用来管理 {{site.data.keyword.Bluemix_notm}} 环境的用户。例如，可以从 LDAP 注册表添加用户。

开始之前，请安装 cf 命令行界面。{{site.data.keyword.Bluemix_notm}} 管理 CLI 插件需要 cf V6.11.2 或更高版本。[下载 Cloud Foundry 命令行界面](https://github.com/cloudfoundry/cli/releases){: new_window}

**限制：**Cygwin 不支持 Cloud Foundry 命令行界面。请在非 Cygwin 命令行窗口中使用 Cloud Foundry 命令行界面。

### 添加 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件

安装了 cf 命令行界面后，可以添加 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件。

**注**：如果先前安装了 {{site.data.keyword.Bluemix_notm}} 管理插件，那么可能需要卸载此插件，删除存储库，然后重新安装以获取最新更新。

完成以下步骤来添加存储库并安装该插件：

<ol>
<li>要添加 {{site.data.keyword.Bluemix_notm}} 管理插件存储库，请运行以下命令：<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
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

要查看命令的列表，请运行以下命令：

`cf plugins`
{: codeblock}

有关命令的其他帮助，请使用 `-help` 选项。

有关如何使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 管理](../cli/plugins/bluemix_admin/index.html)。
