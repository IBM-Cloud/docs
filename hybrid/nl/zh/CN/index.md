---


copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 管理 {{site.data.keyword.Bluemix_notm}} Local 和 {{site.data.keyword.Bluemix_notm}} Dedicated
{: #mng}

如果您具有 {{site.data.keyword.Bluemix}} Local 或 {{site.data.keyword.Bluemix_notm}} Dedicated 的管理员访问权，请转至**管理**页面来管理资源、监视配额使用情况、管理用户许可权、安排升级通知，以及查看安全报告和日志等。您可以通过创建空间并设置[用户角色和许可权](/docs/admin/index.html#oc_useradmin)来管理组织；请参阅[管理组织](/docs/admin/orgs_spaces.html)。
{:shortdesc}

{: #ld_table1}

| 我能执行哪些操作？ | 详细信息 |    
|----------------|---------|
|监视系统使用情况 | 单击**管理 &gt; 使用情况**。查看系统信息、监视 CPU 使用情况以及计划使用情况，以便做出最佳业务决策。请参阅[查看使用情况信息](/docs/admin/index.html#oc_resource)。|
|管理目录 | 单击**管理 &gt; 目录管理**可管理哪些服务对用户和组织可视。请参阅[管理目录](/docs/admin/index.html#oc_catalog)。|
|管理组织 | 单击**管理 &gt; 组织管理**可创建组织、监视组织配额以及基于需求快速做出决策。请参阅[管理组织](/docs/admin/index.html#oc_organizations)。|
|创建空间和分配用户角色 | 单击**帐户** &gt; **管理组织**以在组织内创建空间。添加用户并为用户分配组织和空间角色。请参阅[管理组织](/docs/admin/orgs_spaces.html)。 |
|对管理用户许可权进行管理 | 单击**管理 &gt; 用户管理**可添加用户、除去用户和调整用户许可权。请参阅[管理用户和许可权](/docs/admin/index.html#oc_useradmin)。 |
|查看报告和日志 | 单击**管理 &gt; 报告和日志**可查看针对您实例的安全报告和审计日志。请参阅[查看报告](/docs/admin/index.html#oc_report)。 |
|查看系统信息 | 单击**管理 &gt; 系统信息**可查看系统信息，例如暂挂维护更新数、实例的名称和版本、区域、API URL、CLI URL、LDAP 配置详细信息、组和用户映射、统计信息以及共享域。请参阅[查看系统信息](/docs/admin/index.html#oc_system)。 |
|扩展通知和设置通知预订 | 单击**管理 &gt; 系统信息 &gt; *Number* 个暂挂**。可以使用 Webhook 来与所选 Web 服务集成，以设置某个更新或事件的事件通知预订。请参阅[通知和通知预订](/docs/admin/index.html#oc_eventsubscription)。 |
{: caption="表 1. 用于管理 Bluemix Local 或 Dedicated 实例的管理任务" caption-side="top"}

<!-- staging only for WoW start -->

**提示**：{{site.data.keyword.Bluemix_notm}} 控制台中的“基础架构”仪表板仅在 {{site.data.keyword.Bluemix_notm}} Public 环境中的链接帐户中可用。


<!-- staging only for WoW end -->


## 通知和通知预订
{: #oc_eventsubscription}

您始终可以通过检查“状态”页面来了解环境的状态。当事件和安排的中断性维护更新事件发生时，会在“状态”页面上对这些事件进行报告。{{site.data.keyword.Bluemix_notm}} 还会向“管理”页面的“通知”区域发送有关事件（例如，安排或暂挂的维护更新）的通知。

### 通知

您可以查看有关您本地或专用环境的通知，以监视您环境的状态。复查下表以获取有关不同类型通知的信息以及每一个通知类型的发布位置。

{: #ld_table2}

| **事件类型** | **通知方法** |       
|-----------------|-------------------|
| 维护更新 | 要查看暂挂和完成的通知的完整列表和历史记录，请单击**管理 &gt; 系统信息** &gt; *数字* **个暂挂**。您还可以在“状态”页面上发出有关安排的中断性维护更新事件的警报。单击**支持** &gt; **状态**。您可以通过设置预订，向您选择的收件人发送电子邮件，来扩展通知功能。或者，您可以设置预订，使用 Webhook 将“管理”页面的通知与您选择的 Web Service 相集成。|
| 严重事件 | 您将在“状态”页面上获得有关严重事件的警报。单击**支持** &gt; **状态**。您可以通过设置通知预订，向您选择的收件人发送电子邮件，以扩展通知功能。或者，您可以设置预订，使用 Webhook 将“管理”页面的通知与您选择的 Web Service 相集成。  |  
| 阈值事件 | 您可以设置通知预订，以在环境中的组织配额、物理磁盘、物理内存、保留磁盘或保留内存达到阈值时，向您选择的收件人发送电子邮件。或者，您可以设置预订，使用 Webhook 将通知与您选择的 Web Service 相集成。  |  
| {{site.data.keyword.Bluemix_notm}} 状态 | 您始终可以在“状态”页面查看平台、服务和您的 {{site.data.keyword.Bluemix_notm}} 实例的最新状态。单击**支持** &gt; **状态**。  |
{: caption="表 2. 事件类型和通知方法" caption-side="top"}

### 设置通知预订
{: #seteventsub}

您可以使用通知预订来扩展发送到“管理”页面和“状态”页面的通知的功能。使用通知预订可设置定制电子邮件或使用 Webhook 与选择的工具相集成。
 * 如果选择电子邮件选项，那么通知将发送到指定的电子邮件地址。可以选择事件、维护更新或阈值的通知。这将发送初始电子邮件通知。随后，如果对事件进行了更改，那么每次进行更改后，都会再发送一条包含该更改的通知。  
 * 如果您选择 Webhook 选项，那么您的通知会直接路由到所选目标，例如电话号码（通过短信）。您可以定制通知类型，特别是维护更新、严重事件警报或阈值。还可以定制是接收新通知还是接收有关预订更改的通知，以及在每个通知的主体中包含哪些信息。

**注**：只有具有 Superuser 许可权 (`ops.admin`) 的用户才可以设置通知预订。

要从**通知预订**页面创建电子邮件或 Webhook 预订，请完成以下步骤：

1. 浏览到**通知预订**页面。转至**系统信息 &gt; 环境 &gt; 预订**。
2. 单击**添加预订**。
3. 填写通知预订表单。

  * 要创建有关维护更新或事件的电子邮件通知预订，请参阅[表 3](index.html#emailnotmaintinc) 中的信息。
  * 要创建有关阈值的电子邮件通知预订，请参阅[表 4](index.html#emailnottrhesh) 中的信息。
  * 要创建有关维护更新或事件的 Webhook 通知预订，请参阅[表 5](index.html#webhooknotsub) 中的信息。
  * 要创建有关阈值的 Webhook 通知预订，请参阅[表 6](index.html#webhooknotthresh) 中的信息。

4. 在您完成表单之后，可以从以下选项中进行选择：

  * 单击**保存**，以将预订保存到通知预订列表。
  * 单击**保存并测试**，以保存并测试通知。
  * 单击**保存并关闭**，以将预订保存到通知预订列表，然后返回上一页。

{: #emailnotmaintinc}

| **字段** | **描述** |
|-----------------|-------------------|
| 已启用 | 选择要启用电子邮件通知的选项。清除选项将禁用电子邮件通知。缺省情况下，会启用预订。 |
| 类型 | 选择**电子邮件**。 |
| 事件 | 选择要预订有关**维护**事件的通知还是**事件**的通知。 |
| 组合通知 | 选中该选项可将所有区域的事件通知组合到单个通知。此选项仅可用于事件。
 |
| 主题 | 输入电子邮件的主题行。这是必填字段。  |
| 主体 | 输入要在电子邮件中发送的消息体文本。您可以使用 IBM 有效内容值，向电子邮件通知填充相关信息。请参阅[维护和事件有效内容部分值](index.html#payload)表，以识别可以使用的值。使用基本 HTML 标记，来构建您的电子邮件。这是必填字段。 |
| 收件人 | 使用电子邮件通知收件人的逗号分隔列表，输入一个或多个电子邮件地址。展开“抄送”或“密件抄送”选项，将电子邮件抄送给其他人。这是必填字段。 |
| 描述 | 添加要创建的预订的唯一描述。 |
{: caption="表 3. 关于阈值的电子邮件通知预订的字段" caption-side="top"}


{: #emailnottrhesh}

| **字段** | **描述** |
|-----------------|-------------------|
| 已启用 | 选择要启用电子邮件通知的选项。清除选项将禁用电子邮件通知。缺省情况下，会启用预订。 |
| 类型 | 选择**电子邮件**。 |
| 事件 | 选择**阈值**。 |
| 阈值 | 选择要获取相关通知的阈值的类型：组织配额、物理磁盘、物理内存、保留磁盘或保留内存。 |
| 阈值方向 | 选择在超过设置的“跨越阈值时通知”值时希望数据移入的方向，即“升序”或“降序”。例如，如果“跨越阈值时通知”值为 50%，并且方向为“降序”，那么仅当使用量百分比从大于或等于 50% 变为小于 50% 时，才会向您发送通知。如果将方向设置为“升序”，那么当使用量百分比从小于 50% 变为大于 50% 时，会向您发送通知。|
| 超过 (%) 时通知 | 输入达到时发送通知的阈值百分比。如果在“阈值方向”字段中选择“升序”属性，那么当阈值高于此百分比时，会发送电子邮件通知。 |
| 低于 (%) 时通知 | 输入达到时发送通知的阈值百分比。如果在“阈值方向”字段中选择“降序”属性，那么当阈值低于此百分比时，会发送电子邮件通知。 |
| 描述 | 添加要创建的预订的唯一描述。 |
| 主题 | 输入电子邮件的主题行。这是必填字段。  |
| 消息体 | 输入要在电子邮件中发送的消息体文本。您可以使用 IBM 有效内容值，向电子邮件通知填充相关信息。请参阅[阈值有效内容部分值](index.html#threshpayload)表，以识别可以使用的值。使用基本 HTML 标记，来构建您的电子邮件。这是必填字段。 |
| 收件人 | 使用电子邮件通知收件人的逗号分隔列表，输入一个或多个电子邮件地址。展开“抄送”或“密件抄送”选项，将电子邮件抄送给其他人。这是必填字段。 |
{: caption="表 4. 关于维护更新或事件的电子邮件通知预订的字段" caption-side="top"}

阈值数据每 6 个小时收集一次。当值跨越设置的阈值时，只发送一次通知。如果选择“升序”，那么当值低于阈值，然后再次高于阈值时，才会发送新通知。同样，如果选择“降序”，那么仅当值高于设置的阈值，然后再次低于阈值时，才会向您发送通知。 

如果在达到阈值时不想等 6 小时再发送通知，那么在填完表单上的字段后，可以单击**保存并测试**以接收使用样本数据的测试通知。  

“组织配额”阈值通知仅包含在与该通知对应的 6 小时时间段内跨越指定阈值百分比的组织。不会包含在先前的 6 小时时间段内跨越阈值的组织，即便这些组织仍然高于或低于阈值。在确定是否应该发送组织配额通知时，会独立考虑构成组织配额的三个资源（保留内存、服务和路径）。例如，如果组织使用的保留内存量跨越组织配额的 50%，那么配置为值 50% 的“组织配额”阈值会导致发送通知。如果相同组织使用的服务数在将来某个时间点跨越组织配额的 50%，那么尽管使用的内存量保持不变，相同的“组织配额”阈值预订也将导致发送通知。

{: #webhooknotsub}

| **字段** | **描述** |
|-----------------|-------------------|
| 已启用 | 选中该选项可启用通知。清除该选项会禁用通知。缺省情况下，会启用预订。 |
| 类型 | 选择 **Webhook** |
| 事件 | 选择要预订有关**维护**事件的通知还是**事件**的通知。 |
| 授权 | 选择是否启用授权。选项为：**基本**或**无**。 |
| 用户名 | 如果选择**基本**授权，请输入您的 Web Service 的用户名。如果不想使用个人凭证，那么可以设置功能标识以专门用于 {{site.data.keyword.Bluemix_notm}}。 |
| 密码 | 如果选择**基本**授权，请输入您的 Web Service 的密码。 |
| 描述 | 添加要创建的预订的唯一描述。 |
| 新事件 | 选中此选项可启用新维护或事件的通知。清除该选项会禁用通知。 |
| 方法 | 选择 **GET**、**POST** 或 **PUT**。 |
| URL | 输入要连接到 Web Service 的 URL。 |
| 响应属性 | 此可选字段是属性名称，用于标识发送 POST 或 PUT 请求时 Web Service 创建的资源。如果为新事件提供响应属性，并且选择为事件更改创建预订，那么还必须为“事件更改”预订提供该响应属性。根据使用的 Web Service，可以将其指定为 URL 的一部分或指定为有效内容值。  |
| 有效内容 | 如果选择了 POST 或 PUT 方法，请输入特定于要使用的 Web Service 的属性，以及与属性成对的用于 IBM 通知的有效内容值。请参阅[维护和事件有效内容部分值](index.html#payload)表，以识别可以使用的值。如果未在此部分中输入信息，您会收到不含任何更多信息的通知。 |
| 事件更改 | 选中此选项可创建有关已对其创建预订的维护或事件的更改的通知预订。清除该选项会禁用通知。 |
| 使用新事件的值和有效内容 | 使用“新事件”部分中的“方法”、URL 和“有效内容”字段的内容。请注意，如果选中此选项，那么这些字段在“事件更改”部分中不可做进一步编辑。 |
| 方法 | 选择 **GET**、**POST** 或 **PUT**。 |
| URL | 输入要连接到 Web Service 的 URL。 |
| 有效内容 | 如果选择了 POST 或 PUT 方法，请输入特定于要使用的 Web Service 的属性，以及与属性成对的用于 IBM 通知的有效内容值。请参阅[维护和事件有效内容部分值](index.html#payload)表，以识别可以使用的值。如果未在此部分中输入信息，您会收到不含任何更多信息的通知。 |
| 组合通知 | 选中该选项可将所有区域的事件通知组合到单个通知。此选项仅可用于事件。
 |
{: caption="表 5. 关于维护或事件的 Webhook 通知预订的表单字段" caption-side="top"}


{: #webhooknotthresh}

| **字段** | **描述** |
|-----------------|-------------------|
| 已启用 | 选中该选项可启用通知。清除该选项会禁用通知。缺省情况下，会启用预订。 |
| 类型 | 选择 **Webhook**。 |
| 事件 | 选择**阈值**。 |
| 阈值 | 选择要获取相关通知的阈值的类型：组织配额、物理磁盘、物理内存、保留磁盘或保留内存。|
| 阈值方向 | 选择是要以“升序”还是“降序”查看阈值数据。  |
| 低于 (%) 时通知 | 如果选择**降序****阈值方向**，请输入达到时发送通知的阈值百分比。当阈值低于此百分比时，会发送 Webhook 通知。 |
| 超过 (%) 时通知 | 如果选择**升序****阈值方向**，请输入达到时发送通知的阈值百分比。当阈值高于此百分比时，会发送 Webhook 通知。 |
| 描述 | 添加要创建的预订的唯一描述。 |
| 授权 | 选择是否启用授权。选项为：**基本**或**无**。 |
| 用户名 | 如果选择基本授权，请输入您的 Web Service 的用户名。如果不想使用个人凭证，那么可以设置功能标识以专门用于 {{site.data.keyword.Bluemix_notm}}。 |
| 密码 | 如果选择基本授权，请输入您的 Web Service 的密码。 |
| 方法 | 选择 **GET**、**POST** 或 **PUT**。 |
| URL | 输入要连接到 Web Service 的 URL。 |
{: caption="表 6. 关于阈值的 Webhook 通知预订的表单字段" caption-side="top"}

阈值数据每 6 个小时收集一次。当值跨越设置的阈值时，只发送一次通知。如果选择“升序”，那么当值低于阈值，然后再次高于阈值时，才会发送新通知。同样，如果选择“降序”，那么仅当值高于设置的阈值，然后再次低于阈值时，才会再次向您发送通知。 

如果在达到阈值时不想等 6 小时再发送通知，在填完表单上的字段后，可以单击**保存并测试**以保存通知并使用样本数据来测试通知。

“组织配额”阈值通知仅包含在与该通知对应的 6 小时时间段内跨越指定阈值百分比的组织。不会包含在先前的 6 小时时间段内跨越阈值的组织，即便这些组织仍然高于/低于阈值。在确定是否应该发送组织配额通知时，会独立考虑构成组织配额的三个资源（保留内存、服务和路径）。例如，如果组织使用的保留内存量跨越组织配额的 50%，那么配置为值 50% 的“组织配额”阈值会导致发送通知。如果相同组织使用的服务数在将来某个时间点跨越组织配额的 50%，那么尽管使用的内存量保持不变，相同的“组织配额”阈值预订也将导致发送通知。

{: #payload}

| **IBM 值** | **描述** | **事件类型** |
|----------------|----------------|------------------------|
| {{content.category}} | 受影响的服务 | 事件 |
| {{content.disruption}} | 受影响的组件 | 维护更新 |
| {{content.message}} | 消息描述 |   维护更新和事件 |
| {{content.scheduleWindow.start}} | 安排的更新开始日期 | 维护更新 |
| {{content.scheduleWindow.end}} | 安排的更新结束时间 | 维护更新 |
| {{content.severity}} | 严重性分级 | 事件 |
| {{content.subCategoryName}} | 受影响的组件 | 事件 |
| {{content.title}} | 消息标题 | 维护更新和事件 |
| {{region}} | 受影响的区域 | 维护更新和事件 |
| {{status}} | 更新的状态 | 维护更新 |
| {{type}} | 更新或事件 | 维护更新和事件 |
{: caption="表 7. 维护和事件有效内容部分值" caption-side="top"}


{: #threshpayload}

| **IBM 值** | **描述** | **事件类型** |
|----------------|----------------|------------------------|
| {{content.org_quota}} | 组织配额阈值 | 阈值 |
| {{content.physical_disk}} | 物理磁盘阈值 | 阈值 |
| {{content.physical_memory}} | 物理内存阈值 | 阈值 |  
| {{content.reserved_disk}} | 保留磁盘阈值 | 阈值 |
| {{content.reserved_memory}} | 保留内存阈值 | 阈值 |
{: caption="表 8. 阈值有效内容部分值" caption-side="top"}

保存通知预订时，您会通过设置的方法接收通知。通知仍将在以下位置中进行发布：  
 * 在“状态”页面上发布事件
 * 在“状态”页面上发布安排的中断性维护更新事件
 * 在“管理”页面的“通知”区域中发布维护更新

可以选择任何保存的通知预订，查看最近的活动或按需要进行编辑。单击以展开任何最近活动条目来查看历史记录详细信息。

## 维护更新
{: #oc_schedulemaintenance}

如果您具有 Superuser 许可权 (`ops.admin`)，那么可以通过单击**管理 &gt; 系统信息 &gt; *数字* 个暂挂**来访问**系统更新**页面，从而查看安排的和暂挂的维护更新。环境中的所有用户都可以通过单击**支持** &gt; **状态**来查看安排的中断性维护更新事件。

**注**：请参阅以下[设置预先批准的维护时段](index.html#preapprovedmaintenance)部分，以开始进行操作。必须设置这些时段，IBM 才能安排对您环境的维护。

<dl>
<dt>非中断性更新</dt>
<dd>非中断性更新不会影响您的环境和正在运行的应用程序，也不会影响用户对您应用程序的访问。此更新类型不需要逐个批准更新，并将在“系统更新”页面中设置的预先批准的可用维护时段内应用。</dd>
<dt>中断性更新</dt>
<dd>中断性更新可能会影响您的环境、正在运行的应用程序，或影响用户对您应用程序的访问。必须安排并批准每个维护更新在分配的 21 天维护时段内执行。您可以选择建议的部署日期和时间（任何预先批准的时段的选项），也可以打开日历，选择三个特定时间和日期，供 IBM 在安排更新时选择使用。</dd>
</dl>


### 设置预先批准的维护时段
{: #preapprovedmaintenance}

非中断性维护更新安排在预先批准的时段内运行。缺省情况下，将为系统创建两个每周可用更新时段。这两个时段通常设置为每周六和每周日夜间重复执行。可以通过以下某种方式来更改缺省设置：
 * 通过选择其他日期和/或其他开始时间来编辑缺省更新时段
 * 创建更新时段，然后删除缺省更新时段

要保存更改，仍必须满足每周必需的最少时间。

您需要每周至少设置两天，并且一周至少设置 12 小时的可用小时数。例如，可以在不同的两天分别设置 6 小时时段，也可以在不同的三天分别设置 4 小时时段。为了确保这些时段有足够的时间来应用更新，每个时段的持续时间必须至少为 4 小时。  

**注**：只有具有 Superuser 许可权 (`ops.admin`) 的用户才可以安排和批准维护更新。

1. 转至**管理 &gt; 系统信息 &gt; *数字* 个暂挂 &gt; 管理可用性**。
2. 展开**管理可用更新时段**部分。
3. 单击**添加新时段** ![添加新时段](images/add-new.png)。
4. 通过选择时段的频率、持续时间和开始时间，设置第一个可用时段。
5. 可选：如果您想要将重现可用性时段设置为要安排部署的首先时间，请选择**标记为首选**。可能时，首选时段会提供高优先级。
6. 单击**提交**。
7. 重复此过程，直到满足每周时段数的最低需求。

### 设置不可用的维护时段
{: #blockpreapprovedmaintenance}

可以选择设置特定不可用更新时段，在这些时段内，环境不可进行非中断性维护更新。例如，可选择不希望应用任何维护的高流量周末或假期，以确保应用程序可供用户使用。

您需要每周至少设置两天，并且一周至少设置 12 小时的可用小时数。尝试创建不可用更新时段时，如果此新时段会使系统每周运行更新的时间少于最低必需时间，那么可能无法保存更改。在这种情况下，必须首先除去某些现有的不可用更新时段，或者添加更多可用更新时段后，才能保存新的不可用更新时段。有关更多信息，请参阅[设置预先批准的维护时段](index.html#preapprovedmaintenance)。

1. 转至**管理 &gt; 系统信息 &gt; *数字* 个暂挂 &gt; 管理可用性**。
2. 展开**管理不可用更新时段**部分。
3. 单击**添加新时段** ![添加新时段](images/add-new.png)。
4. 通过选择时段的频率、持续时间和开始时间，设置不可用时段。
5. 单击**提交**。

### 安排和批准更新
{: #scheduleandapprove}

设置了预先批准的维护时段后，非中断性更新将自动安排在这些时间内执行。无需您对这些类型的更新进行明确批准。然而，您可以查看每个维护更新的详细信息，包括要更新的内容、更新所需时间以及安排更新执行的时间。

要查看非中断性更新的详细信息，请完成以下步骤：

1. 转至**管理 &gt; 系统信息 &gt; *数字* 个暂挂**。
2. 确定**需要客户安排**设置为**否**的任何行。
3. 选择该更新所在的行以查看详细信息。

中断性更新可能会影响您的环境、正在运行的应用程序，或影响用户对您应用程序的访问。必须安排并批准每个维护更新在分配的 21 天维护时段内执行。您可以选择建议的部署日期和时间（任何预先批准的时段的选项），也可以打开日历，选择三个特定时间和日期，供 IBM 在安排更新时选择使用。

对于需要批准的中断性更新，请完成以下步骤：

1. 转至**管理 &gt; 系统信息 &gt; *数字* 个暂挂**。
2. 确定**需要客户安排**设置为**是**的任何行。
3. 选择该更新所在行，以查看更新的详细信息，包括更新描述、建议的更新日期和时间、受影响的组件以及更新的持续时间。
4. 选择**安排和批准**。
5. 从以下选项中进行选择：**建议的日期**、**替代日期**或**任何预先批准的时段**。如果选择**替代日期**，您可以打开日历，选择三个选项，供 IBM 从中进行选择。
6. 可选：从日历中所选替代日期的列表中，选择您要设置为部署首选日期的日期。每一个所选的日期都会针对安排部署的开发者标记为首选。IBM 会尝试在首选更新时段期间安排维护。
7. 完成时选择**提交**。

根据所选项，更新将安排在接受的建议日期内、某个预先批准的时段内或者某个所选特定日期和时间进行部署。当更新安排由 IBM 进行部署时，您会在**系统更新**页面上的更新详细信息中看到安排的日期。您只能在所安排的开始日期和时间之前还剩下一天（24 小时）时，才可以重新安排已经计划的部署。一旦您已重新安排了部署，您就无法再重新安排。


## 查看系统信息
{: #oc_system}

要查看系统信息，请单击**管理 &gt; 系统信息**。

可以查看包括暂挂系统更新、常规系统信息、API 和 CLI 信息以及 LDAP 配置详细信息在内的各个部分。

### 暂挂系统更新

在“更新”部分中，可以查看需要您执行操作的暂挂更新通知数。可能会看到两种类型的暂挂更新：

<dl>
<dt>非中断性更新</dt>
<dd>非中断性更新不会影响您的环境和正在运行的应用程序，也不会影响用户对您应用程序的访问。此更新类型不需要逐个批准更新。这些更新将在“系统更新”页面中设置的预先批准的可用维护时段内应用。</dd>
<dt>中断性更新</dt>
<dd>中断性更新可能会影响您的环境、正在运行的应用程序，或影响用户对您应用程序的访问。您可以安排并批准每个维护更新在分配的 21 天维护时段内执行，以确保更新不会在关键业务时间内应用。可以选择根据预先批准的更新时段建议的部署日期和时间，也可以另外选择两个时间和日期，供 IBM 在应用更新时选择使用。</dd>
</dl>

有关设置预先批准的维护时段以及设置特定的不可用维护日期的更多信息，请参阅[维护更新](index.html#oc_schedulemaintenance)。

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
- 组织内存配额使用情况，基于已用总内存配额分配的应用程序内存，以及特定组织每个应用程序的 GB-小时使用量视图。还可以在“组织管理”页面的**配额监视**部分中查看所有组织的配额使用情况。请参阅[组织管理](../admin/index.html#orgusage)。


### 资源使用情况
{: #resourceusage}

要查看资源使用情况信息，请单击**管理 &gt; 资源使用情况**。

在**资源使用情况**部分中，可以查看以下信息：

- 资源使用情况信息，例如可以保留的内存量和磁盘空间量、物理可用的内存量和磁盘空间量，以及实际保留的内存量和磁盘空间量与物理使用的内存量和磁盘空间量。您可以查看有关在所有 Droplet Execution Agent (DEA) 上平均 CPU 使用量的信息。有关内存、磁盘和 CPU 使用量的更详细信息，请参阅[内存、磁盘和 CPU 详细信息](index.html#resourceusagedetails)。
- 最近 6 小时或最近一天的网络使用情况信息（流入带宽和流出带宽）。显示的数据基于公用和专用网络的流入与流出流量总和。
- 最近 10 分钟、最近一小时和最近一天 {{site.data.keyword.Bluemix_notm}} 的平均响应时间。
- 最近 10 分钟、最近一小时或最近一天 {{site.data.keyword.Bluemix_notm}} 的平均每秒事务数。


#### 系统内存、磁盘和 CPU 详细信息
{: #resourceusagedetails}

在**资源使用情况**部分中，可以查看内存和磁盘的**保留**量和**物理**量的摘要。    
	<dl>
	<dt><strong>物理</strong></dt>
	<dd>为环境购买的内存量或磁盘空间量。</dd>
	<dt><strong>保留</strong></dt>
	<dd>可为环境中所有已部署和正在运行的应用程序保留的内存总量或磁盘空间总量。由于应用程序很少会使用为其保留的所有内存，因此物理值通常小于保留值。</dd>
	</dl>

除了图形表示法外，还可以查看环境使用的内存和磁盘空间的百分比。您也可以查看实际使用的保留量和物理量与可用的保留量和物理量的比较（以 GB 为单位）。

要查看按 DEA 列出的内存、磁盘或 CPU 使用情况，请单击**细目**。  

要查看一段时间内有关内存或磁盘的物理和保留使用量的更详细信息，请单击**历史记录**。可以将查看的时间范围指定为每周或每月。“历史使用情况”视图显示在所选时间内的内存或磁盘的使用情况图。  
	<dl>
	<dt><strong>保留限制</strong></dt>
	<dd>“保留限制”显示为水平虚线图，等于可为环境中运行的所有应用程序总体保留的内存或磁盘空间总量。</dd>
	<dt><strong>保留</strong></dt>
	<dd>“保留”面积图显示当前为环境中运行的所有应用程序总体保留的内存或磁盘空间。<p>要查看在特定时间点保留内存最多的组织，请将鼠标悬停在“保留”面积图上与该时间点关联的点上。然后，可以在显示的饼图中单击组织以查看有关该组织的更多信息。</p></dd>
	<dt><strong>物理限制</strong></dt>
	<dd>“物理限制”显示为水平虚线图，显示购买用于环境的物理内存或磁盘空间量。</dd>
	<dt><strong>物理</strong></dt>
	<dd>“物理”面积图显示实际使用的内存或磁盘空间量。</dd>
	</dl>
	
#### 服务使用量详细信息
{: #servicesresourceusage}

**服务**选项卡显示服务使用总量与专用服务的最大容量的比较情况。例如，如果您有专用 Cloudant 服务，并且使用了 1000 GB 容量中的 500 GB，那么会看到一个图形显示您已使用了总容量的 50%。该图形的颜色会根据您有多接近容量限制而变化。使用了容量的 70% 到 84% 时会显示黄色，使用量达到可用容量的 85% 或更高时会显示红色。

**注**：目前，服务使用量信息可能并非在所有环境中可用。此功能可用于 Cloudant、MessageHub、API Connect 和 Session Cache。


### 帐户使用情况
{: #accountusage}

可以查看您的帐户每月在专用或本地环境中的使用情况。可以使用这些数据，根据特定组织的使用量来确定相应费用。所有分配了具有**读**访问权的**用户**许可权的管理控制台用户，都可以查看帐户使用情况数据。此外，组织记帐管理员也可以查看其组织的帐户使用情况数据，即使没有为记帐管理员分配管理控制台**用户**许可权时也是如此。作为管理控制台管理员（Superuser 许可权），您可以通过单击**帐户** &gt; **管理组织**来为组织分配记帐管理员角色。

要查看帐户使用情况数据，请完成以下步骤：

<ol>
<li>单击<strong>帐户</strong> &gt; <strong>使用情况仪表板</strong>。</li>
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
<li>单击<strong>帐户</strong> &gt; <strong>使用情况仪表板</strong>。</li>
<li>单击 <strong>Public</strong>。</li>
<li>选择要查看其数据的组织。</li>
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

下表显示了为 {{site.data.keyword.Bluemix_notm}} Local 和 {{site.data.keyword.Bluemix_notm}} Dedicated 生成的安全报告的列表。大多数报告会每天生成。但是，加密和密钥管理事件报告是每月生成一次。所有报告都会在管理控制台中保留 90 天，以供您检索。在 90 天后，报告在 {{site.data.keyword.Bluemix_notm}} 中可根据请求脱机提供，这一时间为 9 个月。报告总计可供检索的时间最长为 1 年。


{: #ld_table9}

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
{: caption="表 9. 安全报告列表" caption-side="top"}

## 查看状态
{: #oc_status}

您可以查看 {{site.data.keyword.Bluemix_notm}} 环境的状态和管理控制台的状态。

### {{site.data.keyword.Bluemix_notm}} 环境状态

您可以使用 {{site.data.keyword.Bluemix_notm}}“状态”页面来监视 {{site.data.keyword.Bluemix_notm}} 实例的状态。单击**支持** &gt; **状态**。

“状态”页面是查找通知和公告的一个中心位置，从中可了解影响 {{site.data.keyword.Bluemix_notm}} 平台以及 {{site.data.keyword.Bluemix_notm}} 中主要服务的关键事件。您可以预订 RSS 订阅源来获取通知，这样就不必检查是否有通知。有关“状态”页面和设置 RSS 订阅源的更多信息，请参阅[查看 {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status)。

### 管理控制台状态

初始部署 {{site.data.keyword.Bluemix_notm}} 环境后，系统会对用于管理环境的组件自动完成验证检查。验证检查运行后，可以转至管理控制台的“验证检查”页面来检查组件的状态。要访问该页面，请转至 <code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>，其中 `<subdomain>` 是您的本地或专用实例的名称。

您可以随时运行验证，但必须登录才能选择用于运行验证的选项。如果在添加用户、编辑组织或管理服务时遇到故障，请运行此检查以确定是否有任何组件发生故障或断开连接。您可以开具支持凭单并填写检查中获得的信息，以快速解决问题。

## 管理目录
{: #oc_catalog}

您可以管理用户可以在 {{site.data.keyword.Bluemix_notm}}“目录”中可查看哪些 {{site.data.keyword.Bluemix_notm}} 服务。单击**管理 &gt; 目录管理**。

选择服务磁贴以编辑服务套餐可视性。要编辑可视性，请从以下选项中进行选择：

- 要显示隐藏的服务以使用户可在“目录”中进行查看，请选择**启用所有套餐**。
- 要隐藏服务以使用户无法在 {{site.data.keyword.Bluemix_notm}}“目录”中进行查看，请选择**禁用所有套餐**。
- 要控制单个套餐的可视性，请选择套餐名称，然后使用下拉菜单来选择**对所有组织启用**、**对所有组织禁用**或**对特定组织启用套餐**。

<!-- staging only start -->

您还可以基于开发者创建应用程序时的兼容性，管理可用 buildpack 的优先级顺序。

1. 转至**管理 &gt; 目录管理**
2. 转至**计算**部分。
3. 选择 **Buildpack 优先级**。
4. 选择您要在列表中划分较高或较低优先级的 buildpack 选项。
5. 在已选择选项的情况下，使用箭头在列表中移动选项。

<!-- staging only end -->

### 注册服务代理程序
{: #servicebrokerui}

如果您有一个服务要显示在 {{site.data.keyword.Bluemix_notm}}“目录”中，那么必须实现并注册[服务代理程序 ![外部链接图标](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window}。注册代理程序后，可以选择哪些组织可在本地或专用实例中访问该服务。

服务代理程序的使用方法根据其管理的服务数，或根据其是否已向 {{site.data.keyword.Bluemix_notm}} 注册而有所不同。

- 如果服务代理程序管理一个服务，那么在实现了[服务代理程序 API ![外部链接图标](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window} 之后，可以使用该用户界面来注册该服务代理程序。请参阅[注册管理一个服务的服务代理程序](index.html#registerbrokerui)。
- 如果服务代理程序管理多个服务，请将 cf CLI 与 [{{site.data.keyword.Bluemix_notm}} 管理 CLI](../cli/plugins/bluemix_admin/index.html) 插件（`ba` 子命令）一起使用，或者使用[定制服务 API](index.html#servicebrokerapi)。
- 如果服务代理程序已注册，但希望对其执行更新或删除操作，请将 cf CLI 与 [{{site.data.keyword.Bluemix_notm}} 管理 CLI](../cli/plugins/bluemix_admin/index.html) 插件（`ba` 子命令）一起使用，或者使用[定制服务 API](index.html#servicebrokerapi)。

#### 注册管理一个服务的服务代理程序
{: #registerbrokerui}

<!-- staging only start -->

查看以下信息并完成相应步骤来注册服务代理程序：

**开始之前**：<a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">实现 Cloud Foundry 服务代理程序 API <img src="../icons/launch-glyph.svg" alt="外部链接图标"></a> 以支持您的服务与 {{site.data.keyword.Bluemix_notm}} 之间的通信。服务代理程序 API 是由 {{site.data.keyword.Bluemix_notm}} 使用的一组 REST 端点。

要实现服务代理程序时，在 <code>GET /v2/catalog</code> 的 JSON 响应中，必须提供服务和服务套餐的定义，包括要显示的服务信息。例如，查看目录 (GET) 响应的以下样本 JSON：

```
{
"services":[
   {
      "bindable":true,
      "description":"Cool Service is an analytics and data warehousing solution.",
      "id":"cool-service-id",
      "name":"coolservice",
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
               "description":"Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data immediately with familiar tools."
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
```
{: codeblock}

以下各表可以帮助您填写 JSON 文件。


{: #ld_table10}

| **JSON 字段** | **描述** |
|-----------------|-----------------|
|bindable   | 布尔值，指示服务实例是否可以绑定到应用程序。  |
|描述 | 服务描述，使用 cf marketplace 命令时显示，或者将鼠标悬停在 {{site.data.keyword.Bluemix_notm}} 用户界面的“目录”中的相应服务图标上时显示。可以为描述添加单个语句或短语。 |
|name | 服务的名称，在 cf 命令行界面中显示。此名称必须在 {{site.data.keyword.Bluemix_notm}} 中唯一，并且必须使用小写字母且不能包含空格。向 {{site.data.keyword.Bluemix_notm}} 注册服务后，不能更改该服务的名称。 |
|id  | 服务的标识。此标识必须在 {{site.data.keyword.Bluemix_notm}} 中唯一，并且必须是 GUID（全局唯一标识）。向 {{site.data.keyword.Bluemix_notm}} 注册服务后，不能更改该服务的标识。 |
|metadata | 服务套餐元数据，在 {{site.data.keyword.Bluemix_notm}}“目录”和价格表中显示。metadata 字段是可选字段。可以指定 metadata 的更多字段。请参阅下表 [Metadata 字段](index.html#metadatafields)，以获取更多信息。 |
|plans | 一组服务套餐定义。请参阅下表 [Plan 字段](index.html#planfields)，以获取更多信息。 |
{: caption="表 10. JSON 字段" caption-side="top"}


{: #metadatafields}

| **Metadata 值** | **描述** |
|---------------------|-----------------|
|displayName          | 套餐的名称，在 {{site.data.keyword.Bluemix_notm}} 用户界面中显示。此名称会同时显示在“目录”中的服务详细信息页面上以及价格表上。套餐名称仅第一个字母大写。请勿使用“Default”作为缺省套餐名称；请改为使用“Standard”。 |
|providerDisplayName | 服务提供者的名称 |
|longDescription | 服务的详细描述。请考虑至少对详细描述使用两个语句。 |
|plans                | 一组服务套餐定义。plans 字段的每组条目都由以下字段组成：name、description、free、id 和 metadata。请参阅下表 [Plan 字段](index.html#planfields)，以获取更多信息。 |
|bullets | 为服务显示的一组字符串。可使用 bullets 来提供详细描述以及其他信息。bullets 字段必须至少包含两个 bullet 元素。每个 bullet 都包含 title 和 description 字段。 |
|imageUrl | 大型 PNG 图像（50 x 50 像素）的 URL。 |
|smallImageUrl | 小型 PNG 图像（24 x 24 像素）的 URL。 |
|mediumImageUrl | 中型 PNG 图像（32 x 32 像素）的 URL。 |
|featuredImageUrl | 特色图像的（64 x 64 像素）的 URL。 |
|documentationUrl | 有关服务的文档的 URL。 |
|termsUrl | 包含协议条款的 PDF 文件的 URL。 |
|media（可选） | 一组元素，用于显示在 {{site.data.keyword.Bluemix_notm}} 用户界面中介绍服务的视频和截屏。media 元素可以包含以下字段：type（image、youtube 或 video）、thumbnailUrl（media 元素的预览图像的 URL）、url（截屏或 YouTube 视频的 URL）、source（未在 YouTube 上托管的视频的来源。视频来源的“类型”必须受 HTML5 支持。对于 video，请包含“type”和“url”。）和 caption（media 元素的文字说明。文字说明有助于身有残疾的人员进行访问以了解 media 元素。）. |
|serviceKeysSupported | 布尔值，指示是否支持服务密钥 API。服务密钥 API 用于支持服务在 {{site.data.keyword.Bluemix_notm}} 外部使用。缺省值为 false。 |
|plan_updateable | 布尔值，指示服务是否支持更改套餐。缺省值为 false。 |
|embeddableDashboard（可选） | 此字段指示服务仪表板在 {{site.data.keyword.Bluemix_notm}} 用户界面中的显示方式。如果未指定此字段，仪表板将嵌入用户界面中，但限制为宽度不低于 960px，并且仪表板围绕 iFrame 有更多水平内边距。可以使用 true、false、drilldown 或 launch。对于此值，可以使用以下字段：true、false、drilldown 和 launch。  |
|notCreatable（可选） | 布尔值，指示是否可以通过 {{site.data.keyword.Bluemix_notm}} 用户界面和 cf 命令行界面创建服务实例。值为 true 表示无法通过 {{site.data.keyword.Bluemix_notm}} 用户界面或 cf 命令行界面创建服务实例。缺省值为 false。 |
|notCreatableMessage（可选） | 无法创建服务实例时，在 {{site.data.keyword.Bluemix_notm}} 用户界面中显示的消息。如果未指定此字段，那么将显示以下缺省消息：可用时进行通知，请确认您的电子邮件地址，或输入其他电子邮件地址。 |
|notCreatableRobotMessage（可选） | 在 {{site.data.keyword.Bluemix_notm}} 用户界面的服务详细信息页面中的对话气泡中显示的消息。此消息用于指示服务可能存在问题，或者指示导致服务不可用的其他原因。可以指定消息来说明原因。如果未指定此字段，那么将显示以下缺省消息：此服务当前不可用。 |
|apiReferenceUrl（可选） | iFrame 的 URL，位于“目录”中服务详细信息页面上的“API 引用”区域中。如果未用于“目录”中的服务详细信息页面，那么可以输入在“{{site.data.keyword.Bluemix_notm}} REST API 文档”微服务中注册服务时，分配给服务的“REST API 文档”的数字值。这将在服务仪表板中显示 REST API 文档。 |
|sdkDownloadUrl（可选） | 单击“下载 SDK”按钮时打开的 Web 页面的 URL。“下载 SDK”按钮位于“仪表板”中“应用程序概述”页面的服务磁贴上。Web 页面会在新的浏览器选项卡中打开。 |
|serviceMonitorApi    | 返回 JSON 数据的 API 的 URL，如以下示例中所示，用于报告服务运行状况。必须在服务元数据中具有 serviceMonitorApi 或 serviceMonitorApp。请参阅以下代码样本以获取示例。 |
|serviceMonitorApp    | 应用程序的 URL，该应用程序可部署到 {{site.data.keyword.Bluemix_notm}} 并绑定服务，以提供特定于服务状态的输出。应用程序返回的 JSON 数据格式必须与 serviceMonitorApi 相同。必须在服务元数据中具有 serviceMonitorApi 或 serviceMonitorApp。请参阅以下代码样本以获取示例。 |
{: caption="表 11. 元数据字段" caption-side="top"}


```
{
    "service": "servicename",
    "version": 1,
    "health": [
        {
            "plan": "starter",
            "status": 0,
            "serviceinput": "count(*) from healthcheck",
            "serviceoutput": "10…or error 1234 database not running",
            "responsetime": 4
        },
        {
            "plan": "enterprise",
            "status": 1,
            "serviceinput": "count(*)fromhealthcheck",
            "serviceoutput": "10…orerror1234databasenotrunning",
            "responsetime": 4
        }
    ]
}
```
{: pre}

以下示例显示了 GET /v2/catalog 的 JSON 响应如何映射到 {{site.data.keyword.Bluemix_notm}}“目录”中的服务详细信息页面：

![“目录”中的服务详细信息。](images/metadata.png "Bluemix“目录”的服务详细信息视图")


{: #planfields}

| **Plan 值** | **描述** |
|---------------------|-----------------|
|name       | 服务套餐的名称，在 cf 命令行界面中使用。例如，套餐名称显示在 cf marketplace 命令的输出中。套餐名称必须为小写字母且不能包含空格，并且必须在服务中唯一。  |
|描述       | 服务套餐的描述。在 {{site.data.keyword.Bluemix_notm}}“目录”中的服务详细信息页面上选择套餐后，会显示相应描述。 |
|free      | 布尔值，指示服务套餐是否免费。缺省值为 true。 |
|id       | 服务套餐的标识。标识必须唯一，并且必须为 GUID。  |
|metadata（可选）    | 服务套餐元数据，在 {{site.data.keyword.Bluemix_notm}}“目录”和价格表中显示。metadata 字段是可选字段。可以在 metadata 字段内指定以下字段：displayName, type（subscription、reservable 或 planDetails）、bullets、costs（unitId、unit 或 partNumber）和 paidOnly。请参阅下表 [Plan metadata 字段](index.html#planmetadata)，以获取更多信息。 |
{: caption="表 12. 套餐字段" caption-side="top"}


{: #planmetadata}

| **Plan metadata 值** | **描述** |
|------------------------|-----------------|
|displayName             | 套餐的名称，在 {{site.data.keyword.Bluemix_notm}} 用户界面中显示。此名称会同时显示在“目录”中的服务详细信息页面上以及价格表上。   |
|type                    | 套餐的类型。此字段可以使用以下值：subscription（预订套餐。缺省值为 false。）、reservable（可保留套餐。仅当套餐是预订套餐，即 plan.metadata.subscription 的值为 true 时，才使用此值。缺省值为 false。）或 planDetails（可用于套餐的资源的详细数量和描述。仅当套餐是可保留套餐，即 plan.metadata.reserveable 的值为 true 时，才使用此值。） |
|bullets                 | 可用于套餐的资源的描述。描述会显示在“目录”中服务详细信息页面上的**功能**列中以及价格表上。 |
|costs                   | 有关服务的成本信息，显示在“目录”中服务详细信息页面上的“价格”列中以及价格表上。每组条目都包含以下字段：unitId（单位标识。使用复数形式并且所有字母均大写。对于免费套餐，此字段是可选的。）、unit（用于计算服务费用的度量值。此字段的值在 {{site.data.keyword.Bluemix_notm}} 用户界面中用于表示费用度量值。）和 partNumber（记帐系统使用的 `part_number` 标识。对于免费套餐，此字段是可选的。）.   |
|paidOnly（可选）     | 布尔值，指示此服务套餐是否只可用于 {{site.data.keyword.Bluemix_notm}} 付费帐户。值为 **true** 表示此服务套餐只可用于付费帐户，不能添加到试用帐户。值为 **false** 表示此服务套餐可以添加到付费帐户和试用帐户。缺省值为 **false**。	  |
{: caption="表 13. 套餐元数据字段" caption-side="top"}

以下示例显示了 GET /v2/catalog 的 JSON 响应如何映射到 {{site.data.keyword.Bluemix_notm}}“目录”中的服务详细信息页面。具体而言，即上表中描述的 plan metadata 字段如何映射到用户界面：

![“目录”中的 plan metadata 详细信息。](images/plan_metadata.png "Bluemix“目录”plan metadata 值视图")


<!-- staging only end -->

<ol>
<li>在实现了服务代理程序 API 后，请转至<strong>管理</strong> &gt; <strong>目录管理</strong>。</li>
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

要创建组织并添加管理员，请完成以下步骤：

1. 单击<strong>创建组织</strong>。
2. 输入组织的名称。
3. 输入要添加为管理员的人员的姓名或电子邮件。可以通过输入并选择多个姓名来添加多个管理员。
4. 单击<strong>创建组织</strong>以保存更改并创建组织。

### 创建空间

您可以在组织中创建空间；例如，*dev* 空间（作为开发环境）、*test* 空间（作为测试环境）和 *production* 空间（作为生产环境）。然后，可以将应用程序与空间相关联。要创建空间，请完成以下步骤：

1. 在菜单栏中，单击**帐户** &gt; **管理组织**。
2. 选择要向其添加空间的组织。
3. 单击**创建空间**。
4. 输入空间名称。
5. 单击**创建**。

### 配额监视

可以展开**配额监视**部分来查看以下信息：

- 环境内存使用情况详细描述了整个系统环境的内存使用情况。图表显示了以下信息：
<ul>
<li>使用的物理内存和可用物理内存的限制</li>
<li>当前保留的内存配额和可以保留的内存的限制</li>
<li>组织的内存配额总量</li>
</ul>
图表中显示了以下类型的内存使用情况。

	<dl>
	<dt><strong>已用物理量</strong></dt>
	<dd>环境使用的物理内存量。</dd>
	<dt><strong>物理限制</strong></dt>
	<dd>环境可用的物理内存总量。</dd>
	<dt><strong>保留配额</strong></dt>
	<dd>在所有组织中为所有部署的应用程序保留的内存总和。保留的配额总和可能会超过环境的物理内存限制。例如，如果物理内存限制为 16 GB，您可能对总共 5 个不同应用程序分别保留 4 GB 的内存。因此，保留的配额会超过物理内存限制。但是，在许多情况下，这些应用程序可能不会使用单独为每个应用程序保留的所有配额。此外，所有应用程序可能也不会同时使用保留的所有内存配额。</dd>
	<dt><strong>保留限制</strong></dt>
	<dd>可以为环境中的所有应用程序保留的内存总量。</dd>
	<dt><strong>配额总量</strong></dt>
	<dd>在所有组织中分配的内存配额总量。</dd>
	</dl>
	**注**：数据每 4 小时自动刷新一次。如果要在页面上的数据自动更新之前刷新数据，请单击**重新计算**。

- 组织内存使用情况。此部分详细描述了组织级别的内存使用情况。可以查看每个组织的内存配额总量、为每个组织保留的配额和每个组织使用的物理内存。该图表提供的信息按每个组织的最高内存保留量列出，缺省情况下，保留内存量最多的组织列在最前面。可以按**最高内存使用量**和**多余内存分配量**进行排序。

	<dl>
	<dt><strong>最高内存使用量</strong></dt>
	<dd>使用此选项可识别内存保留量最高的组织。按最高内存使用量排序可识别保留内存量最多的组织。此列表按保留的配额进行排序。</dd>
	<dt><strong>多余内存分配量</strong></dt>
	<dd>使用此选项可识别其内存配额总量大于需求的组织。按多余内存分配量排序可识别在为组织分配的配额中所使用的内存量最低的组织。</dd>
	</dl>

### 管理配额
{: #manageorgquota}

配额表示在环境中创建组织时为其分配的资源限制。组织空间中的任何应用程序或服务都会使用一定的已分配的配额。要管理组织的配额，请完成以下步骤：

<ol>
<li>在“组织内存使用情况”部分中，单击图表中要编辑的组织所对应的条形，或者从“组织列表”部分中选择组织的名称。在“组织信息”页面中，可以重命名组织，也可以添加或除去管理员。
<p><strong>注</strong>：如果所选的配额计划无法满足组织的当前使用量，那么您会收到一条消息。</p></li>
<li>单击 <strong>Cloud Foundry</strong> 或 <strong>Containers</strong>。缺省情况下，会打开 Cloud Foundry 配额页面。
<ul>
<li>在 Cloud Foundry 页面中，可以选择套餐，并查看以下资源的配额详细信息：
<ul>
<li>服务</li>
<li>路径</li>
<li>内存配额</li>
<li>应用程序分配</li>
</ul>
</li>
<li>在 <strong>Containers</strong> 页面中，可以为以下字段分配值（值必须为整数）：
<dl class="parml">
<dt class="pt dlterm">映像限制</dt>
<dd class="pd">在专用注册表中可以拥有的最大容器映像数。容器映像是所创建的每一个容器的基础。映像通过 Dockerfile 创建，该文件为只读文件，用于保存操作系统、应用程序及其所有依赖项，并描述如何配置容器。映像在组织的所有成员之间共享。</dd>
<dt class="pt dlterm">缺省内存分配量</dt>
<dd>创建新空间时，自动分配的容器内存量。创建容器时，必须选择容器大小。该大小将确定容器可以在计算主机上使用的内存量，并计入容器内存限制。</dd>
<dt class="pt dlterm">最大内存分配量</dt>
<dd>可以在组织的所有空间中分配的最大容器内存量。</dd>
<dt class="pt dlterm">缺省浮动 IP 数</dt>
<dd>创建新空间时，自动分配的公共 IP 地址数。可以将公共 IP 地址绑定到单个容器和容器组，使其可以通过因特网访问。</dd>
<dt class="pt dlterm">最大浮动 IP 数</dt>
<dd>可以在组织的所有空间中分配的最大公共 IP 地址数。</dd>
</dl>
<strong>注</strong>：如果环境中尚无容器，或者如果在环境中尚未设置容器，那么您将收到错误消息。
<p>有关容器的更多信息，请参阅[关于 IBM Containers](/docs/containers/container_ov.html)。有关容器配额的更多信息，请参阅[配额和 Bluemix 帐户](/docs/containers/container_planning_org_ov.html#container_planning_quota)。</p>
<strong>注：</strong>在 {{site.data.keyword.Bluemix_notm}} 悉尼区域中无法使用容器。</li>
</ul>
<li>要保存在“管理组织”页面上进行的任何更改，请单击<strong>保存</strong>。</li>
</ol>


### 通过组织列表管理组织
{: #manageorgfrolis}

在“组织列表”部分中，可以查看 {{site.data.keyword.Bluemix_notm}} 环境中的所有组织，并可以通过单击组织名称，对各个组织分别执行操作。

- 要删除组织，请单击“操作”列中的**删除**图标 ![删除](images/icon_trash.svg)。
- 要查看组织的配额计划和使用情况，请在列表中单击组织的名称。在所选组织的**管理组织**页面上，可以查看以下使用情况信息：

  - 当前正在使用的服务数。
  - 当前正在使用的路径数。
  - 内存配额图，显示已用配额量和当前未使用的配额量。
  - 应用程序分配图，显示哪些应用程序包含在已用内存配额中。
  - 计量应用程序使用情况图，显示三个月的报告，内容是每个已部署应用程序使用的 GB-小时。可以选择**列表视图**来查看所有应用程序的数据，包括过去三个月中每个应用程序的内存分配和计量的 GB-小时使用量。

- 要编辑组织的名称，以及添加或除去管理员，请在列表中单击组织的名称，然后按照屏幕上的提示执行操作。
- 要查看有关所查看组织的特定用户的信息，请单击该用户名以显示“用户信息”。然后，可以单击组织名称返回以查看“组织信息”。 

## 管理用户和许可权
{: #oc_useradmin}

您可以添加单个用户或添加用户组。通常，可以通过轻量级目录访问协议 (LDAP)，从公司的用户注册表中，将用户添加到 {{site.data.keyword.Bluemix_notm}} 实例。您还可以查看用户许可权。如果分配给您的是 **Superuser** 许可权，那么您还可以设置和管理其他用户的许可权。单击**管理 &gt; 用户管理**。

“用户管理”页面显示本地或专用实例的所有用户。还会使用表中的图标显示每个用户的许可权。许可权可以为以下值：无、**Superuser**、**Basic Access**、**Catalog**、**Reports** 和 **Users**。
**Superuser** 和 **Basic Access** 许可权可以设置为**打开**或**关闭**，而其余的许可权则通过特定访问权类型进行启用或禁用，包括该许可权的 **Read** 或 **Write** 访问权，如图标所示。有关每种类型的描述和图标说明，请参阅[许可权](#permissions)。

### 处理用户
{: #workwithusers}

根据您对用户许可权具有 **Read** 还是 **Write** 访问权，您可以搜索现有的用户、除去用户，以及单个或成组添加用户。如果您具有 **Superuser** 许可权，那么您具有完全访问权，可完成环境中用户管理的任何任务。请复查以下用户管理任务和完成每一项任务所需的访问级别：

* 查找用户。如果您具有 **Read** 和 **Write** 访问权且您了解所有或部分用户名，那么您可以使用**搜索**字段，在表中查找用户。您还可以按用户的组织和许可权来过滤用户列表。要过滤用户列表，请完成以下步骤：
  <ol>
  <li>单击<strong>过滤器</strong>。</li>
  <li> 根据需要的过滤依据，单击<strong>组织</strong>或<strong>许可权</strong>。<dl>
	<dt><strong>组织</strong></dt>
	<dd>要按用户的组织过滤用户，请在<strong>组织</strong>字段中开始输入组织名称，并从列表中选择相应组织。然后，选择分配给该组织内用户的一个或多个角色。</dd>
	<dt><strong>许可权</strong></dt>
	<dd>要按用户的许可权过滤用户，请首先选择一个或多个用户的类型。例如，您可能希望查看所有 Superuser。对于除 <strong>Superuser</strong> 或 <strong>Basic Access</strong> 以外的其他许可权，还可以选择访问权类型，例如<strong>读</strong>或<strong>写</strong>。</dd>
	</dl></li>
  <li>单击<strong>应用</strong>。</li>
   </ol>

   “用户管理”窗口显示设置的过滤器以及通过指定过滤器过滤出的用户。然后，可以在过滤后的表中搜索用户。您还可以通过从指定过滤器的列表中除去过滤器选项来修改此列表。

* 添加单个用户。如果您拥有 **Superuser** 许可权或者具有 **Write** 访问权的 **Users** 许可权，那么可以添加用户。

  1. 要从 LDAP 目录添加单个用户，请单击**添加用户**。
  2. 在**搜索**字段中，输入用户的电子邮件地址，然后从填充的列表中选择相应用户。
  3. 接着，在**组织**字段中，通过输入组织名称并从填充的列表中选择相应组织来选择要向其添加用户的组织。
  4. 要向所选组织添加用户，请单击**添加用户**。

  **注**：添加操作成功后，该用户会添加到表中以供您查看和搜索。所添加的用户没有分配的许可权。

* 从 LDAP 目录添加用户组。如果您拥有 **Superuser** 许可权或者具有 **Write** 访问权的 **Users** 许可权，那么可以添加用户。

  1. 单击**添加用户组**。
  2. 在**搜索**字段中，输入要搜索的组名，然后从填充的列表中选择相应组名。
  3. 接着，在**组织**字段中，通过输入组织名称并从填充的列表中选择相应组织来选择要向其添加用户组的组织。
  4. 要向所选组织添加用户组，请单击**添加用户**。

  **注**：如果组中的用户数超过 50 个，那么会通过后台批处理作业添加这些组。添加操作成功后，即可在表中查看和搜索所添加的用户或组。所添加的用户没有分配的许可权。

* 通过导入包含用户标识、用户电子邮件地址和计划向其添加用户的组织来添加用户组。如果您拥有 **Superuser** 许可权或者具有 **Write** 访问权的 **Users** 许可权，那么可以添加用户。

**注**：输入与用户注册表中使用的值相匹配的用户标识。

  1. 单击**导入用户**。
  2. 单击**下载模板 (.CSV)**，以下载具有可以填充的必需列的电子表格，或者您可以创建自己的电子表格并包含必需的列标题：**用户标识**、**电子邮件**和**组织**。模板中还包含两个可选列：**名字**和**姓氏**。
  3. 为必需列填写用户值。如果使用的不是 LDAP 目录，请将必需列和可选列标题用于导入的用户。
  4. 保存文件，然后单击**上传文件**。

  **注**：电子表格中的列可以按任意顺序排列，只要您包含所有必需的列即可。如果导入成功，您会收到确认消息，声明所有用户都已添加。如果成功导入了一些用户，而另一些用户未成功导入，请查看错误消息，以对无法添加的用户执行操作。

* 除去用户。如果您拥有 **Superuser** 许可权或者具有 **Write** 访问权的 **Users** 许可权，那么可以从环境永久地除去用户。

    1. 找到用户，然后单击 ![删除](images/icon_trash.svg) 图标。
    2. 单击**除去**。

* 编辑用户所属的许可权和组织需要您具有 **Superuser** 许可权。要编辑用户的许可权，请找到该用户，然后单击用户名。在**编辑用户**页面中，可以启用或禁用许可权：

    * 从列表中选择**打开**，以启用 **Superuser** 或 **Basic Access** 许可权。
    * 从列表中选择**读取**，以允许用户拥有对该许可权的 **Read**（只读）访问权，或者选择**写入**，以允许用户拥有对该许可权的 **Write**（编辑或添加和除去）访问权。
    * 选择**关闭**，以禁用任何许可权。

    **注**：将 **Superuser** 许可权设置为**打开**可设置所有其他具有 **Write** 访问权的许可权。

* 要向特定组织添加用户或从中除去用户，您必须拥有 **Superuser** 许可权或具有 **Write** 访问权的 **Users** 许可权。

    1. 要向组织添加用户，请从表中选择相应用户名以访问**编辑用户**页面。接着，使用搜索字段来查找组织，从列表中选择组织，然后单击**保存**。
    2. 要从组织中除去用户，请从表中选择相应用户名以访问**编辑用户**页面。接着，对要从中除去用户的组织，单击 ![除去](images/icon_remove.svg)，然后单击**保存**。
    
* 要查看有关用户分配到的组织的信息，请单击组织名称以显示“组织信息”。然后，可以单击用户名返回以查看“用户信息”。 

### 许可权
{: #permissions}

可以为用户分配以下具有特定访问级别（读或写）的许可权，使用户可以在管理控制台中完成特定任务：


{: #ld_table14}

| **用户许可权** | **描述** |       
|-----------------|-------------------|
| Superuser | **Superuser** 许可权设置为**打开**的用户可以编辑其他用户的许可权。如果您打开该许可权，那么它会自动对所有其他许可权启用完全访问权。除了针对此表中每个许可权所概括的任务之外，它们还可以设置通知预订，以直接获取有关维护或事件的警报、安排维护、对控制台组件运行验证检查，以及为环境创建组织和空间。此许可权等同于管理控制台的管理员 (admin) 角色。  |
| Basic Access | **Basic Access** 许可权设置为**打开**的用户可以在 {{site.data.keyword.Bluemix_notm}} 用户界面查看“管理”页面选项。启用该许可权的用户可以访问[系统信息](#oc_system)和[资源使用情况](#oc_resource)磁贴。没有此许可权，用户无法查看或访问“管理”菜单选项。此许可权等同于管理控制台的管理员 (admin) 角色。此许可权等同于先前使用的管理控制台的登录许可权。 |
| 目录 | 可以为拥有 **Catalog** 许可权的用户分配 **Read** 或 **Write**（修改）的访问权，以指出本地或专用实例中哪些服务可用。Read 访问权允许用户访问“目录管理”磁贴，以查看可用的服务。Write 访问权允许用户访问[目录管理](#oc_catalog)磁贴，以查看服务、编辑服务的可视性、注册定制服务并控制 buildpack 优先级列表。 |  
| Reports | 可以为拥有 **Reports** 许可权的用户分配 **Read** 或 **Write**（修改）安全报告的访问权。Read 访问权允许用户访问“报告和日志”磁贴，以下载报告。Write 访问权允许用户查看[报告和日志](#oc_report)磁贴，以及使用 CLI 上传新报告，并创建新类别以供用户访问。 |
| Users | 可以为拥有 **Users** 许可权的用户分配针对用户列表执行 **Read**（查看）操作或针对用户执行 **Write**（添加或除去）操作的访问权。此许可权不允许为其他用户设置许可权。Write 访问权允许用户向环境添加新用户、从环境删除用户，并向环境内已经存在的组织添加现有用户。此外，**Write** 访问权允许用户添加新组织、删除组织并编辑组织内的用户。 |
{: caption="表 14. 许可权" caption-side="top"}

## 使用 REST API 
{: #auth_adminapi}

要使用 REST API 命令，您首先需要进行认证。要生成并支持会话，可以使用 cURL 命令来完成以下任务：

* [登录到管理控制台](#auth_loginapi) 
* [存储用户标识和密码](#auth_setuidpw)
* [存储 cookie](#auth_apistorecook)
* [复用 cookie](#auth_apireusecook)

### 登录到管理控制台
{: #auth_loginapi}

运行任何 `Admin` API 请求之前，都必须登录到管理控制台。 

要登录到管理控制台，可以在 `https://console.<region>.bluemix.net/login` 端点上使用基本访问认证。服务器会使用您的会话返回 cookie。您使用该 cookie 来执行所有管理控制台操作。

**注：**如果几个小时不使用会话，会话将变为无效。

要登录到管理控制台，请运行以下命令：

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">--user <em>user_id</em>:<em>password</em></dt>
<dd class="pd">接受用户标识和密码，并发送基本授权头。</dd>
<dt class="pt dlterm">-c <em>filename</em></dt>
<dd class="pd">将指定的用户标识和密码作为 cookie 存储在指定的文件中。</dd>
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">检索指定的用户标识和密码作为 cookie 放入指定的文件中。</dd>
<dt class="pt dlterm">--header</dt>
<dd class="pd">发送 Accept 头。</dd>
</dl>

以下示例显示了此命令的输出：
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

### 存储用户标识和密码
{: #auth_setuidpw}

您还可以存储用户标识和密码，这样就不必每次登录时都手动输入。要存储用户标识和密码以供复用，请使用以下 cURL 示例：

`curl -X GET -H "Authorization: Basic <redacted>" -H "Accept: application/json" "http://localhost:3000/login"`
{: codeblock}

要在单独的文件中设置登录信息，然后调用该文件，以便您不必为每个认证请求重新输入这些信息，请使用 cURL 命令提供的 `--netrc` 选项。

要将 `--netrc` 选项与 cURL 配合使用，请首先通过以下某种方式在用户的主目录中创建文件：
* 在 Unix 系统上，创建名为 .netrc 的文件 
* 在 Windows 系统上，创建名为 _netrc 的文件。 

在该文件中，输入以下信息：

`machine console.<region>.bluemix.net
login <id>
password <password>`
{: codeblock}

调用 cURL 命令时，添加以下自变量：`--netrc`。
<p>要使用位于其他目录中的 netrc 文件，请使用 `--netrc-file [file]` 选项，其中 `[file]` 是 netrc 文件的位置。</p>
</li>
</ol>


### 存储 cookie
{: #auth_apistorecook}

登录到管理控制台时，服务器会随会话返回 cookie。未来通过 API 调用使用管理控制台执行所有操作时，在登录过程中都需要该 cookie。可以存储 cookie 以供日后使用。

要在登录后存储 cookie，请使用 `-c` 选项，如以下 CURL 示例中所示：

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

### 复用 cookie
{: #auth_apireusecook}

要复用 cookie，请使用 `-b` 选项，后跟使用 `-c` 选项分配的 cookie 文件名，如以下 CURL 示例中所示：

`curl --user <user_id>:<password> -b ./cookies.txt`
{: codeblock}

## 使用 Admin REST API 管理用户

{: #usingadminapi}

您可以使用 `Admin` REST API 为 {{site.data.keyword.Bluemix_notm}} 实例添加和除去用户。为了能够从命令行执行基本操作，提供了试验性 `Admin` REST API 端点和 JSON 响应。本信息的示例中的端点和 URL 可能会发生变化，也可能会临时通知停止使用。

如果您拥有 **Superuser** 许可权或者具有 **Write** 访问权的 **Users** 许可权，那么可以添加或移除用户。必须拥有 **Superuser** 许可权，才能编辑其他用户的许可权。

虽然可以选择使用其他工具，但下面是使用后续示例时所需的必备工具：
* cURL - 将 REST API 请求作为命令进行输入。cURL 是一个免费的实用程序，可用于通过命令行界面将 HTTP 请求发送到服务器并接收服务器响应。可以从 [cURL 下载站点 ![外部链接图标](../icons/launch-glyph.svg)](http://curl.haxx.se/download.html){: new_window} 来下载 cURL。
* Python - 使用 Python 直观显示 JSON 工具的输出。此可选工具接受 JSON 文本作为输入，并提供易读输出。可以从 [Python 下载站点 ![外部链接图标](../icons/launch-glyph.svg)](https://www.python.org/downloads){: new_window} 来下载 Python。


### 列出组织
{: #listingorg}

添加用户时，必须指定组织。可以使用 `Admin` REST API 来列出所有组织。您必须拥有具有 **Read** 访问权的 **Users** 许可权，才能列出组织。要列出所有组织，请运行以下命令：

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">将先前使用 <samp class="ph codeph">-c</samp> 选项存储到文件中的用户标识和密码作为 cookie 传递到 HTTP 服务器。</dd>

</dl>

对于每个组织，结果会包含以下信息：
* `"guid"`：组织的 GUID
* `"name"`：组织的名称

以下示例显示了此命令的输出：
```
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

您可以使用 `Admin` REST API 来列出已注册的用户，以确定用户是否已添加到 {{site.data.keyword.Bluemix_notm}} 环境。您必须拥有具有 **Read** 访问权的 **Users** 许可权，才能列出已注册的用户。要列出所有用户，请运行以下命令：

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

您可以使用 `Admin` REST API 将用户添加到 {{site.data.keyword.Bluemix_notm}} 实例。您必须拥有具有 **Write** 访问权的 **Users** 许可权才能添加用户，或者具有管理控制台的 **Superuser** 许可权 (ops.admin)。此外，作为 Admin，您可以允许没有一般管理控制台 `user` 或 `superuser` 许可权的组织成员能够仅向其组织添加新用户。请使用以下 API 命令，为组织管理员提供此特定能力：

```
PUT console.<subdomain>.bluemix.net/codi/env_config/allow_managers?flag=<TRUE or FALSE>
```
{: screen}

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

您可以使用 `Admin` REST API 从 {{site.data.keyword.Bluemix_notm}} 实例中除去用户。您必须拥有具有 **Write** 访问权的 **Users** 许可权，才能除去用户。

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

## 用于度量值的 API（试验性）
{: #envappmetricsapi}

您可以使用三个试验性 API 来收集有关环境或应用程序的度量值。这些 API 会针对指定时间段内所请求的度量值返回一组数据点。

以下各部分中描述的度量值 API 可以从特定于区域的端点进行访问，例如： 

`https://console.<region>.bluemix.net/admin/metrics`
{: codeblock}

**注**：

1. 用户每小时最多可以对度量值发起 200 个 API 请求。
2. 每个 API 请求最多可返回 200 个数据点。如果有更多数据可用，将在响应中提供 URL，以用于装入下一组数据。
3. 每个 API 请求都需要用户至少具有对管理控制台的基本访问权。可能还需要其他许可权，如下面所指定。

## 收集有关环境的度量值 

您可以使用试验性环境 API 来收集指定时间段内的高级别环境信息。这将返回指定时间内的可用数据点。数据大约每小时记录一次。例如，如果请求 6 个小时的环境 CPU 数据，那么响应将包含请求 6 个小时内每个小时的 CPU 数据。


### 环境端点 

您可以使用以下端点来调用此 API 命令：`/api/v1/env`

**注**：访问这些端点需要以下某个许可权：**基本访问权**、**用户读许可权**、**用户写许可权**或**超级用户**

### 环境度量值查询参数

使用以下查询参数可以收集 CPU、磁盘、内存、网络、配额和应用程序的度量值：

<dl class="parml">
<dt class="pt dlterm">metric</dt>
<dd class="pd">以下一个或多个值，各值之间用逗号分隔：`memory`、`disk`、`cpu`、`network`、`quota` 和 `apps`。</dd>
<dt class="pt dlterm">startTime</dt>
<dd class="pd">开始返回数据的最早时间点。如果未指定 startTime，那么将包含最早的可用数据点。例如，要收集下午 2 点到 5 点的数据，请将 startTime 指定为 2 PM。</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">结束返回数据的最晚时间点。如果未指定 endTime，那么将使用最新的数据点。例如，要收集下午 2 点到 5 点的数据，请将 endTime 指定为 5 PM。</dd>
<dt class="pt dlterm">sort</dt>
<dd class="pd">数据的返回顺序。有效值为 `asc`（升序）和 `desc`（降序）。缺省值为降序，即首先返回最新的数据。</dd>
</dl>

以下示例使用查询参数来收集环境的度量值：

```
 curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/env?metric=cpu,network,disk,apps,memory
 ```
{: codeblock}


### 环境度量值数据格式

以下各部分提供了数据格式。

 * 要收集有关内存使用情况的数据记录，请使用以下数据格式：
 
```
{
  "sample_time": 1477494000000,
  "memory": {
    "total": {
      "physical": {
      "total_gb": 1728,
        "used": {
          "value_gb": 673.68,
          "percent": 38.99
        }
      },
    "allocated": {
      "reserved_gb": 3456,
        "total_allocated": {
          "value_gb": 2575.18,
          "percent": 74.51
        }
      },
    },
  	"cell": {
      "physical": {
      "total_gb": 864,
      "used": {
        "value_gb": 336.84,
        "percent": 38.99
      }
    },
    "allocated": {
      "reserved_gb": 1728,
      "total_allocated": {
        "value_gb": 1287.59,
        "percent": 74.51
      }
    },
    },
    "dea": {
      "physical": {
      "total_gb": 864,
      "used": {
        "value_gb": 336.84,
        "percent": 38.99
      }
    },
    "allocated": {
      "reserved_gb": 1728,
      "total_allocated": {
        "value_gb": 1287.59,
        "percent": 74.51
      }
    },
    },
    "memory_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "47"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "51"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "45"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "43"
      }
    ]
  }
}
```
{: screen}

 * 要收集有关磁盘使用情况的数据记录，请使用以下数据格式：
 
```
{
  "sample_time": 1477494000000,
  "disk": {
    "total": {
      "physical": {
      "total_gb": 16200,
        "used": {
          "value_gb": 1614,
          "percent": 9.96
        }
      },
    "allocated": {
      "reserved_gb": 32400,
        "total_allocated": {
          "value_gb": 3979,
          "percent": 12.28
        }
      },
    },
    "cell": {
      "physical": {
      "total_gb": 8100,
      "used": {
        "value_gb": 807,
        "percent": 9.96
      }
    },
    "allocated": {
      "reserved_gb": 16200,
      "total_allocated": {
        "value_gb": 1989.5,
        "percent": 12.28
      }
    },
    },
    "dea": {
      "physical": {
      "total_gb": 8100,
      "used": {
        "value_gb": 807,
        "percent": 9.96
      }
    },
    "allocated": {
      "reserved_gb": 16200,
      "total_allocated": {
        "value_gb": 1989.5,
        "percent": 12.28
      }
    },
    },
    "disk_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "13"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "14"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "13"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "12"
      }
    ]
  }
}
```
{: screen}

 * 要收集有关 CPU 使用情况的数据记录，请使用以下数据格式：
 
```
{
  "sample_time": 1477494000000,
  "cpu": {
    "total": {
      "average_percent_cpu_used": 14.725
    },
    "cell": {
      "average_percent_cpu_used": 19
    },
    "dea": {
      "average_percent_cpu_used": 10.45
    },
    "cpu_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "sys_percent": "8.4",
        "user_percent": "2.7",
        "wait_percent": "0.0"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "sys_percent": "7.4",
        "user_percent": "2.4",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/1",
        "type": "cell",
        "ip": "169.53.230.49",
        "sys_percent": "5.3",
        "user_percent": "1.9",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/2",
        "type": "cell",
        "ip": "169.44.109.231",
        "sys_percent": "8.2",
        "user_percent": "22.6",
        "wait_percent": "0.0"
      }
    ]
  }
}
```
{: screen}

 * 要收集有关网络的数据记录，请使用以下数据格式：
 
```
{
  "sample_time": 1477494000000,
  "network": {
    "datapower": {
    "response_times": [
      {
        "proxy": "custom_certificates",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "90",
        "one_minute_ms": "89",
        "ten_minutes_ms": "83",
        "one_hour_ms": "85",
        "one_day_ms": "95"
      }
      ],
        "transactions": [
      {
        "proxy": "custom_domains",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "697",
        "one_minute_ms": "747",
        "ten_minutes_ms": "802",
        "one_hour_ms": "794",
        "one_day_ms": "730"
      }
      ],
        "bandwidth": {
        "in_kbps": 10855,
        "out_kbps": 38090
      }
  }
}
```
{: screen}

* 要收集有关配额使用情况的数据记录，请使用以下数据格式：
 
```
{
  "sample_time": 1477494000000,
  "quota": {
    "reserved_memory": {
      "total_bytes": 33176474877952
    },
    "services": {
      "total": 111650
    },
    "routes": {
      "total": 1675000
    }
  }
}
```
{: screen}

* 要收集有关应用程序的数据记录，请使用以下数据格式：
 
```
{
  "sample_time": 1477494000000,
  "apps": {
    "count": 1406,
    "allocation": {
      "memory_gb": 571.8,
      "disk_gb": 1204
    }
  }
}
```
{: screen}

### 环境度量值响应格式

```
{
   docs: [],
   next_url:
}
```
{: screen}

## 收集有关组织的度量值

大约每小时为所有组织记录一次数据。对特定度量值的请求会返回指定时间段内每次数据采样中的所有组织的信息，信息按请求的度量值降序排列。例如，如果在具有 200 个应用程序的环境中请求 6 小时时间段内按内存列出的所有组织，将返回 1200 个记录，每次返回 200 个。

要减少在请求的时间段内每次数据采样返回的信息量，可以指定 count 选项。使用上面的示例并添加值为 5 的 count 选项时，将返回 30 个记录，这表示每次数据采样中按内存列出的排名前 5 位的组织。

### 组织端点 

您可以使用以下端点来调用此 API 命令：
* `/api/v1/org/memory/physical`
* `/api/v1/org/memory/reserved`
* `/api/v1/org/disk/physical`
* `/api/v1/org/disk/reserved`

**注**：访问这些端点需要以下某个许可权：**用户读许可权**、**用户写许可权**或**超级用户**

### 组织查询参数
 
使用以下查询参数可收集组织的度量值：

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">开始返回数据的最早时间点。如果未指定 startTime，那么将包含最早的可用数据点。例如，要收集下午 2 点到 5 点的数据，请将 startTime 指定为 2 PM。</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">结束返回数据的最晚时间点。如果未指定 endTime，那么将使用最新的数据点。例如，要收集下午 2 点到 5 点的数据，请将 endTime 指定为 5 PM。</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">每次数据采样中返回的记录数。
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">针对指定度量值返回的最小值。如果未指定 minValue，那么会返回所有值。例如，要使用至少 20000 字节的物理内存来收集组织，请将 minValue 指定为 20000。
</dd>
</dl>

以下示例收集有关组织的度量值：

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/org/memory/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}

### 组织响应格式

```
{
   docs: [],
   next_url:
}
```
{: screen}

返回的每个文档都表示在请求的时间点，在每次数据采样中针对某个组织所请求的度量值。

## 收集有关应用程序的度量值

所有应用程序的数据大约每小时记录一次。对特定度量值的请求会返回指定时间段内每次数据采样中的所有应用程序的信息，信息按请求的度量值降序排列。例如，在具有 200 个应用程序的环境中，请求 6 小时时间段内按 CPU 列出的所有应用程序，这样将返回 1200 个记录，每次返回 200 个。

要减少在请求的时间段内每次数据采样返回的信息量，可以指定 count 选项。使用上面的示例，并添加值为 5 的 count 选项时，将返回 30 个记录，这表示每次数据采样中按 CPU 列出的排名前 5 位的应用程序。

### 应用程序端点 

您可以使用以下端点来调用此 API 命令：
* `/api/v1/app/cpu/physical` 
* `/api/v1/app/memory/physical`
* `/api/v1/app/memory/reserved`
* `/api/v1/app/disk/physical`
* `/api/v1/app/disk/reserved`

**注**：访问这些端点需要以下某个许可权：**用户读许可权**、**用户写许可权**或**超级用户**

### 应用程序查询参数
 
使用以下查询参数可收集应用程序的度量值：

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">开始返回数据的最早时间点。如果未指定 startTime，那么将包含最早的可用数据点。例如，要收集下午 2 点到 5 点的数据，请将 startTime 指定为 2 PM。</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">结束返回数据的最晚时间点。如果未指定 endTime，那么将使用最新的数据点。例如，要收集下午 2 点到 5 点的数据，请将 endTime 指定为 5 PM。</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">每次数据采样中返回的记录数。
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">针对指定度量值返回的最小值。如果未指定 minValue，那么会返回所有值。例如，要使用最少 20000 字节的物理内存来收集应用程序，请将 minValue 指定为 20000。
</dd>
</dl>

以下示例收集应用程序的度量值：

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/app/cpu/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}


### 应用程序响应格式

```
{
   docs: [],
   next_url:
}
```
{: screen}

返回的每个文档都表示在每次数据采样中，在请求的时间点，所请求的应用程序的度量值。


## 定制服务 API
{: #servicebrokerapi}

有三个 API 可用于注册或创建服务、更新服务和删除服务。

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

{: #ld_table15}

| **名称** | **描述** |
|-----------------|-------------------|
| name | 服务代理程序的名称。 |
| auth_username | 用于与服务代理程序连接的用户名。 |
| auth_password | 用于与服务代理程序连接的密码。 |
| broker_url | 用于连接服务代理程序的 URL。 |
| owningOrganization | 将服务列入白名单时要使用的初始组织。 |
{: caption="表 15. 字段" caption-side="top"}

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
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
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

{: #ld_table16}

| **名称** | **描述** |
|-----------------|-------------------|
| name | 服务代理程序的名称。此名称是创建服务时使用的名称，无法更改。 |
| auth_username | 用于与服务代理程序连接的用户名。 |
| auth_password | 用于与服务代理程序连接的密码。 |
| broker_url | 用于连接服务代理程序的 URL。 |
| owningOrganization | 将服务列入白名单时要使用的初始组织。 |
{: caption="表 16. 请求" caption-side="top"}

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
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
}
```
{: screen}

## 删除服务

要删除服务，请使用以下 API 和代码示例。


{: #ld_table17}

| **名称** | **描述** |
|-----------------|-------------------|
| name | 服务代理程序的名称。此名称是创建服务时使用的名称，无法更改。 |
{: caption="表 17. 参数" caption-side="top"}

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

### 使用 cf CLI 管理用户
{: #usingadmincli}

您可以将 Cloud Foundry 命令行界面与 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件一起使用来管理 {{site.data.keyword.Bluemix_notm}} 环境的用户。必须为 Cloud Foundry CLI 下载此插件。

开始之前，请安装 cf 命令行界面。{{site.data.keyword.Bluemix_notm}} 管理 CLI 插件需要 cf V6.11.2 或更高版本。[下载 Cloud Foundry 命令行界面 ![外部链接图标](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}。

**限制：**Cygwin 不支持 Cloud Foundry 命令行界面。请在非 Cygwin 命令行窗口中使用 Cloud Foundry 命令行界面。

#### 添加 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件

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

要查看已安装插件中可用子命令的列表，请运行以下命令：

```
cf plugins
```
{: codeblock}

要查看 {{site.data.keyword.Bluemix_notm}} 管理插件的可用命令组的列表，请运行以下命令：

```
cf ba
```
{: codeblock}

有关命令的更多帮助，请使用 `-help` 选项。

有关如何使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 管理](../cli/plugins/bluemix_admin/index.html)。
