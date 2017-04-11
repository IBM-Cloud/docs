---

copyright:

  years: 2015, 2017

lastupdated: "2017-02-20"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 管理 CLI
{: #bluemixadmincli}


您可以将 Cloud Foundry 命令行界面与 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件一起使用来管理 {{site.data.keyword.Bluemix_notm}} Local 或 {{site.data.keyword.Bluemix_notm}} Dedicated 环境。例如，可以从 LDAP 注册表添加用户。如果要查看有关管理 {{site.data.keyword.Bluemix_notm}} Public 帐户的信息，请参阅[管理](/docs/admin/adminpublic.html#administer)。

开始之前，请安装 cf 命令行界面。{{site.data.keyword.Bluemix_notm}} 管理 CLI 插件需要 cf V6.11.2 或更高版本。[下载 Cloud Foundry 命令行界面 ![外部链接图标](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}

**限制：**Cygwin 不支持 Cloud Foundry 命令行界面。请在非 Cygwin 命令行窗口中使用 Cloud Foundry 命令行界面。

**注**：{{site.data.keyword.Bluemix_notm}} 管理 CLI 仅用于 {{site.data.keyword.Bluemix_notm}} Local 和 {{site.data.keyword.Bluemix_notm}} Dedicated 环境。{{site.data.keyword.Bluemix_notm}} Public 不支持该管理 CLI。

## 添加 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件

安装了 cf 命令行界面后，可以添加 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件。

**注**：如果先前安装了 {{site.data.keyword.Bluemix_notm}} 管理插件，那么可能需要卸载此插件，删除存储库，然后重新安装以获取最新更新。

完成以下步骤来添加存储库并安装该插件：

<ol>
<li>要添加 {{site.data.keyword.Bluemix_notm}} 管理插件存储库，请运行以下命令：<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin http://plugins.ng.bluemix.net
</code><br/><br/>
</li>
<li>要安装 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件，请运行以下命令：<br/><br/>
<code>
cf install-plugin BluemixAdminCLI -r BluemixAdmin
</code>
</li>
</ol>

如果需要卸载插件，那么可以使用以下命令，然后可以添加更新的存储库并安装最新的插件：

* 卸载插件：`cf uninstall-plugin BluemixAdminCLI`
* 除去插件存储库：`cf remove-plugin-repo BluemixAdmin`


## 使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件

您可以使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件来添加或除去用户、向组织分配或取消分配用户，以及执行其他管理任务。

要查看命令的列表，请运行以下命令：

```
cf plugins
```
{: codeblock}

有关命令的其他帮助，请使用 `-help` 选项。

### 连接并登录到 {{site.data.keyword.Bluemix_notm}}

您必须进行连接并登录（如果尚未这样做）后，才能使用管理 CLI 插件。

<ol>
<li>要连接到 {{site.data.keyword.Bluemix_notm}} API 端点，请运行以下命令：<br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 实例的 URL 的子域。<br />
</dd>
</dl>
<p>您可以查看管理控制台的“资源和信息”页面，以获取正确的 URL。此 URL 显示在“API 信息”部分的 **API URL** 字段中。</p>
</li>
<li>使用以下命令登录到 {{site.data.keyword.Bluemix_notm}}：<br/><br/>
<code>
cf login
</code>
</li>
</ol>

## 管理用户
{: #admin_users}

### 添加用户
{: #admin_add_user}

要将用户从环境的用户注册表添加到 {{site.data.keyword.Bluemix_notm}} 环境，请使用以下命令：

```
cf ba add-user <user_name> <organization> <first_name> <last_name>
```
{: codeblock}

**注**：要向特定组织添加用户，您必须是拥有 **users.write** 许可权（或 **Superuser** 许可权）的**管理员**。如果您是组织管理员，那么您还能够通过 Superuser 来运行 **enable-managers-add-users** 命令，以向组织添加用户。有关更多信息，请参阅[允许管理员添加用户](index.html#clius_emau)。

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP 注册表中用户的名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其添加用户的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;first_name&gt;</dt>
<dd class="pd">要添加到组织的用户的名字。</dd>
<dt class="pt dlterm">&lt;last_name&gt;</dt>
<dd class="pd">要添加到组织的用户的姓氏。</dd>
</dl>

**提示：****ba add-user** 命令名较长，您还可以使用 **ba au** 作为其别名。

<!-- staging-only commands start. Live for interconnect -->

### 搜索用户
{: #admin_search_user}

要搜索用户，请使用以下命令搭配可选的搜索过滤参数（name、permission、organization 和 role）：

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name_value&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>
<dt class="pt dlterm">&lt;permission_value&gt;</dt>
<dd class="pd">分配给用户的许可权。例如，superuser、basic、catalog、user 和 reports。有关分配的用户许可权的更多信息，请参阅[许可权](/docs/admin/index.html#permissions)。不能将此参数与 organization 参数用于同一查询中。</dd>
<dt class="pt dlterm">&lt;organization_value&gt;</dt>
<dd class="pd">用户所属的组织名称。不能将此参数与 permission 参数用于同一查询中。</dd>
<dt class="pt dlterm">&lt;role_value&gt;</dt>
<dd class="pd">分配给用户的组织角色。例如，组织的管理员、记帐管理员或审计员。使用此参数时必须指定组织。有关角色的更多信息，请参阅[用户角色](/docs/admin/users_roles.html#userrolesinfo)。</dd>

</dl>

**提示：****ba search-users** 命令名较长，您还可以使用 **ba su** 作为其别名。

### 为用户设置许可权
{: #admin_setperm_user}

要为指定用户设置许可权，请使用以下命令：

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**注**：一次只能设置一个许可权。

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">为用户设置许可权：Admin（可用的替代项为 Superuser）、Login（可用替代项为 Basic）、Catalog（read 或 write 访问权）、Reports（read 或 write 访问权）或 Users（read 或 write 访问权）。</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">对于 Catalog、Reports 或 Users 许可权，还必须将访问级别设置为 <code>read</code> 或 <code>write</code>。</dd>
</dl>

**提示：****ba set-permissions** 命令名较长，您还可以使用 **ba sp** 作为其别名。

<!-- staging-only commands end -->

### 除去用户
{: #admin_remov_user}

要从 {{site.data.keyword.Bluemix_notm}} 环境除去用户，请使用以下命令：

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>

</dl>

**提示：****ba remove-user** 命令名较长，您还可以使用 **ba ru** 作为其别名。

### 允许管理员添加用户
{: #clius_emau}

如果您在 {{site.data.keyword.Bluemix_notm}} 环境中有 **Superuser** 许可权，那么可以允许组织管理员向其管理的组织添加用户。要使管理员能够添加用户，请使用以下命令：

```
cf ba enable-managers-add-users
```
{: codeblock}

**提示：****ba enable-managers-add-users** 命令名较长，您还可以使用 **ba emau** 作为其别名。

### 禁止管理员添加用户
{: #clius_dmau}

如果在 {{site.data.keyword.Bluemix_notm}} 环境中已允许组织管理员通过 **enable-managers-add-users** 命令向其管理的组织添加用户，并且您有 **Superuser** 许可权，那么可以除去此设置。要禁止管理员添加用户，请使用以下命令：

```
cf ba disable-managers-add-users
```
{: codeblock}

**提示：****ba disable-managers-add-users** 命令名较长，您还可以使用 **ba dmau** 作为其别名。

## 管理组织
{: #admin_orgs}

### 添加组织
{: #admin_add_org}

要添加组织，请使用以下命令：

```
cf ba create-org <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要添加的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">组织的管理员的用户名。</dd>
</dl>

**提示：****ba create-org** 命令名较长，您还可以使用 **ba co** 作为其别名。

### 删除组织
{: #admin_delete_org}

要删除组织，请使用以下命令：

```
cf ba delete-org <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要删除的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：****ba delete-org** 命令名较长，您还可以使用 **ba do** 作为其别名。

### 向组织分配用户
{: #admin_ass_user_org}

要将 {{site.data.keyword.Bluemix_notm}} 环境中的用户分配给特定组织，请使用以下命令：

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其分配用户的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">有关 {{site.data.keyword.Bluemix_notm}} 用户角色和描述的信息，请参阅[角色](/docs/admin/users_roles.html)。</dd>
</dl>

**提示：****ba set-org** 命令名较长，您还可以使用 **ba so** 作为其别名。

### 从组织中取消分配用户
{: #admin_unass_user_org}

要将 {{site.data.keyword.Bluemix_notm}} 环境中的用户取消分配给特定组织，请使用以下命令：

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其分配用户的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">有关 {{site.data.keyword.Bluemix_notm}} 用户角色和描述的信息，请参阅[分配角色](/docs/admin/users_roles.html)。</dd>
</dl>

**提示：****ba unset-org** 命令名较长，您还可以使用 **ba uo** 作为其别名。

#### 分配角色

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">组织管理员。组织管理员有权执行以下操作：<ul>
<li>在组织内创建或删除空间。</li>
<li>邀请用户加入组织并管理用户。</li>
<li>管理组织的域。</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">记帐管理员。记帐管理员可以查看组织的运行时和服务使用情况信息。</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">组织审计员。组织审计员可以查看空间中的应用程序和服务内容。</dd>
</dl>

### 设置组织的配额
{: #admin_set_org_quota}

要为特定组织设置使用量配额，请使用以下命令：

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要为其设置配额的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">组织的配额计划。</dd>
</dl>

**提示：****ba set-quota** 命令名较长，您还可以使用 **ba sq** 作为其别名。


### 查找组织的容器配额
{: #admin_find_containquotas}

要查找组织的容器配额，请使用以下命令：

```
cf bluemix-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Bluemix 中组织的名称或标识。此参数是必需的。</dd>
</dl>

**提示：****bluemix-admin containers-quota** 命令名较长，您还可以使用 **ba cq** 作为其别名。

### 设置组织的容器配额
{: #admin_set_containquotas}

要设置组织中容器的配额，请使用以下命令并至少包含其中一个选项：

```
cf bluemix-admin set-containers-quota <organization> <options>
```
{: codeblock}

**注**：您可以包含多个选项，但必须至少包含一个选项。

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Bluemix 中组织的名称或标识。此参数是必需的。</dd>
<dt class="pt dlterm">&lt;options&gt;</dt>
<dd class="pd">包含以下一个或多个选项，其中值必须为整数：<ul>
<li>floating-ips-max &lt;value&gt;</li>
<li>floating-ips-space-default &lt;value&gt;</li>
<li>memory-max &lt;value&gt;</li>
<li>memory-space-default &lt;value&gt;</li>
<li>image-limit &lt;value&gt;</li>
</ul>
</dd>
</dl>

**提示：**对于较长的选项名称，您还可以使用以下短名称作为其别名：
<dl class="parml">
<dt class="pt dlterm">floating-ips-max &lt;value&gt;</dt>
<dd class="pd"><strong>fim</strong></dd>
<dt class="pt dlterm">floating-ips-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>fisd</strong></dd>
<dt class="pt dlterm">memory-max &lt;value&gt;</dt>
<dd class="pd"><strong>mm</strong></dd>
<dt class="pt dlterm">memory-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>msd</strong></dd>
<dt class="pt dlterm">image-limit &lt;value&gt;</dt>
<dd class="pd"><strong>il</strong></dd>
</dl>

（可选）可以提供一个在有效 JSON 对象中包含特定配置参数的文件。如果使用 **-file** 选项，那么会优先使用此选项并忽略其他选项。要提供文件，而不设置选项，请使用以下命令：

```
cf bluemix-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

JSON 文件的格式应该如以下示例中所示：

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

**提示：****bluemix-admin set-containers-quota** 命令名较长，您还可以使用 **ba scq** 作为其别名。

## 管理空间
{: #admin_spaces}

### 向组织添加空间

要在组织中添加空间，请使用以下命令：

```
cf bluemix-admin create-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其添加空间的组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">要在组织中创建的空间的名称。</dd>
</dl>

**提示：****ba create-space** 命令名较长，您还可以使用 **ba cs** 作为其别名。

### 从组织中删除空间

要从组织中除去空间，请使用以下命令：

```
cf bluemix-admin delete-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要从中除去空间的组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">要从组织中除去的空间的名称。</dd>
</dl>

**提示：****ba delete-space** 命令名较长，您还可以使用 **ba cs** 作为其别名。

### 向空间添加具有角色的用户

要在空间中创建具有指定角色的用户，请使用以下命令：

```
cf bluemix-admin set-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其添加用户的组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">要向其添加用户的空间的名称。</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">要添加的用户的名称。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">要分配的用户角色。值可以为 Manager（管理员）、Developer（开发者）或 Auditor（审计员）。有关空间中的 {{site.data.keyword.Bluemix_notm}} 用户角色和描述的信息，请参阅[分配角色](/docs/admin/users_roles.html)。</dd>
</dl>

**提示：****ba set-space** 命令名较长，您还可以使用 **ba ss** 作为其别名。


### 除去空间中用户的角色 

要除去空间中用户的角色，请使用以下命令：

```
cf bluemix-admin unset-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其添加用户的组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">要向其添加用户的空间的名称。</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">要添加的用户的名称。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">要分配的用户角色。值可以为 Manager（管理员）、Developer（开发者）或 Auditor（审计员）。有关空间中的 {{site.data.keyword.Bluemix_notm}} 用户角色和描述的信息，请参阅[分配角色](/docs/admin/users_roles.html)。</dd>
</dl>

**提示：****ba unset-space** 命令名较长，您还可以使用 **ba us** 作为其别名。

## 管理目录
{: #admin_catalog}

### 对所有组织启用服务
{: #admin_ena_service_org}

要针对所有组织启用在 {{site.data.keyword.Bluemix_notm}}“目录”中显示的某个服务，请使用以下命令：

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。</dd>
</dl>

**提示：****ba enable-service-plan** 命令名较长，您还可以使用 **ba esp** 作为其别名。

### 对所有组织禁用服务
{: #admin_dis_service_org}

要针对所有组织禁用在 {{site.data.keyword.Bluemix_notm}}“目录”中显示的某个服务，请使用以下命令：

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。</dd>
</dl>

**提示：****ba disable-service-plan** 命令名较长，您还可以使用 **ba dsp** 作为其别名。

### 添加组织的服务可视性
{: #admin_addvis_service_org}

对于能够在 {{site.data.keyword.Bluemix_notm}}“目录”中查看特定服务的组织的列表，可以在其中添加组织。要允许某个组织在 {{site.data.keyword.Bluemix_notm}}“目录”中查看特定服务，请使用以下命令：

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要添加到服务的可视性列表的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：****ba add-service-plan-visibility** 命令名较长，您还可以使用 **ba aspv** 作为其别名。

### 除去组织的服务可视性
{: #admin_remvis_service_org}

对于能够在 {{site.data.keyword.Bluemix_notm}}“目录”中查看特定服务的组织的列表，可以在其中除去组织。要在 {{site.data.keyword.Bluemix_notm}}“目录”中对组织除去某个服务的可视性，请使用以下命令：

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要从服务的可视性列表中除去的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：****ba remove-service-plan-visibility** 命令名较长，您还可以使用 **ba rspv** 作为其别名。

### 编辑组织的服务可视性
{: #admin_editvis_service_org}

您可以编辑和替换特定组织可以在 {{site.data.keyword.Bluemix_notm}}“目录”中查看的服务列表。要替换一个组织或多个组织的所有现有可视服务，请使用以下命令：

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**注：**此命令会将指定组织的现有可视服务替换为在命令中指定的服务。

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要启用的服务套餐的名称或 GUID。如果输入非唯一的服务套餐名称（例如“Standard”或“Basic”），那么系统将提示您选择服务套餐。要识别服务套餐名称，请从主页选择服务类别，然后选择**添加**，以查看该类别的服务。单击服务名称以打开详细视图，然后您可以查看可用于该服务的服务套餐名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要为其添加可视性的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。可以通过在命令中输入更多组织名称或 GUID，对多个组织启用服务可视性。</dd>
</dl>

**提示：****ba edit-service-plan-visibility** 命令名较长，您还可以使用 **ba espv** 作为其别名。

## 管理报告
{: #admin_add_report}

### 添加报告
{: #admin_add_report}

要添加安全报告，请使用以下命令：

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

**注**：如果您具有报告许可权的写访问权，那么您可以使用用户接受的任何格式，创建新类别并添加报告。输入 `category` 参数的新类别名称，或者添加新报告到现有类别。

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

**提示：****ba add-report** 命令名较长，您还可以使用 **ba ar** 作为其别名。

### 删除报告
{: #admin_del_report}

要删除安全报告，请使用以下命令：

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">报告的类别。如果名称中有空格，请使用引号将名称括起。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">报告日期，格式为 <samp class="ph codeph">YYYYMMDD</samp>。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">报告的名称。</dd>
</dl>

**提示：****ba delete-report** 命令名较长，您还可以使用 **ba dr** 作为其别名。

### 检索报告
{: #admin_retr_report}

要检索安全报告，请使用以下命令：

```
cf ba retrieve-report <search>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;search&gt;</dt>
<dd class="pd">报告的文件名。如果名称中有空格，请使用引号将名称括起。</dd>
</dl>

**提示：****ba retrieve-report** 命令名较长，您还可以使用 **ba rr** 作为其别名。

## 查看资源度量值信息
{: #cliresourceusage}

您可以查看资源度量值信息，包括内存、磁盘和 CPU 使用情况。可以查看可用物理资源和保留资源的摘要，以及物理资源和保留资源使用情况的摘要。此外，还可以查看 Droplet Execution Agent (DEA) 和单元（Diego 体系结构）使用情况数据以及内存和磁盘的历史使用情况。缺省情况下，将按降序显示每周内存和磁盘使用情况的历史数据。要查看资源度量值信息，请使用以下命令：

```
cf ba resource-metrics <monthly> <weekly>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;monthly&gt;</dt>
<dd class="pd">一次查看一个月的内存和磁盘空间历史数据。</dd>
<dt class="pt dlterm">&lt;weekly&gt;</dt>
<dd class="pd">一次查看一周的内存和磁盘空间历史数据。这是缺省值。</dd>
</dl>

**提示：****ba resource-metrics** 命令名较长，您还可以使用 **ba rsm** 作为其别名。


## 管理服务代理程序
{: #admin_servbro}

### 列出服务代理程序
{: #clilistservbro}

要列出所有服务代理程序，请使用以下命令：

```
cf ba service-brokers <broker_name>
```
{: codeblock}

**注**：要列出所有服务代理程序，请输入不带 `broker_name` 参数的命令。

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">可选：定制服务代理程序的名称。如果要获取特定服务代理程序的信息，请使用此参数。</dd>
</dl>

**提示：****ba service-brokers** 命令名较长，您还可以使用 **ba sb** 作为其别名。

### 添加服务代理程序
{: #cliaddservbro}

要添加服务代理程序，以便可以将定制服务添加到 {{site.data.keyword.Bluemix_notm}}“目录”，请使用以下命令：

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">定制服务代理程序的名称。</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">有权访问服务代理程序的帐户的用户名。</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">有权访问服务代理程序的帐户的密码。</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">服务代理程序的 URL。</dd>
</dl>

**提示：****ba add-service-broker** 命令名较长，您还可以使用 **ba asb** 作为其别名。

### 删除服务代理程序
{: #clidelservbro}

要删除服务代理程序，以从 {{site.data.keyword.Bluemix_notm}}“目录”中除去定制服务，请使用以下命令：

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">定制服务代理程序的名称或 GUID。</dd>
</dl>

**提示：****ba delete-service-broker** 命令名较长，您还可以使用 **ba dsb** 作为其别名。

### 更新服务代理程序
{: #cliupdservbro}

要更新服务代理程序，请使用以下命令：

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">定制服务代理程序的名称。</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">有权访问服务代理程序的帐户的用户名。</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">有权访问服务代理程序的帐户的密码。</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">服务代理程序的 URL。</dd>
</dl>

**提示：****ba update-service-broker** 命令名较长，您还可以使用 **ba usb** 作为其别名。


## 管理应用程序安全组
{: #admin_secgro}

要使用应用程序安全组 (ASG)，您必须是具有本地或专用环境完全访问权的管理员。对于命令的目标组织，环境的所有用户都可以列出可用的 ASG。但是，要创建、更新或绑定 AGS，您必须是 {{site.data.keyword.Bluemix_notm}} 环境的管理员。

ASG 的功能类似虚拟防火墙，可控制 {{site.data.keyword.Bluemix_notm}} 环境中应用程序的出站流量。每一个 ASG 都包含一个规则列表，允许与外部网络相互进行特定流量传输和通信。您可以将一个或多个 ASG 绑定到特定安全组集（例如，用于应用全局访问的组集），或者绑定到 {{site.data.keyword.Bluemix_notm}} 环境中某个组织内的空间。

{{site.data.keyword.Bluemix_notm}} 最初设置时其对外部网络的所有访问都受到限制。当您将两个 IBM 创建的安全组 `public_networks` 和 `dns` 绑定到缺省 Cloud Foundry 安全组集时，这两个安全组会启用对外部网络的全局访问。Cloud Foundry 中用于应用全局访问的两个安全组为 **Default Staging** 和 **Default Running** 组集。这两个组集会应用允许向所有正在运行的应用程序或所有正在编译打包的应用程序进行流量传输的规则。如果您不想绑定到这两个安全组集，那么您可以从 Cloud Foundry 组集取消绑定，然后将安全组绑定到特定空间。有关更多信息，请参阅[绑定应用程序安全组 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}。

**注**：以下可使您使用安全组的命令基于 Cloud Foundry V1.6。有关更多信息（包括必填和可选字段），请参阅有关[创建应用程序安全组 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window} 的 Cloud Foundry 信息。

### 列出安全组
{: #clilissecgro}

* 要列出所有安全组，请使用以下命令：

```
cf ba security-groups
```
{: codeblock}

**提示：****ba security-groups** 命令名较长，您还可以使用 **ba sgs** 作为其别名。

* 要显示特定安全组的详细信息，请使用以下命令：

```
cf ba security-groups <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**提示：**具有 `security-group` 参数的 **ba security-groups** 命令名较长，您还可以使用 **ba sg** 作为其别名。


### 创建安全组
{: #clicreasecgro}

有关创建安全组和用于定义出局流量的规则的更多信息，请参阅[创建应用程序安全组 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}。

要创建安全组，请使用以下命令：

```
cf ba create-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

您创建的每一个安全组其名称前都添加了 `adminconsole_` 前缀，用于与 IBM 创建的安全组加以区分。

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
<dt class="pt dlterm">&lt;Path to rules file&gt;</dt>
<dd class="pd">规则文件的绝对或相对路径</dd>
</dl>

**提示：****ba create-security-group** 命令名较长，您还可以使用 **ba csg** 作为其别名。

### 更新安全组
{: #cliupdsecgro}

要更新安全组，请使用以下命令：

```
cf ba update-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
<dt class="pt dlterm">&lt;Path to rules file&gt;</dt>
<dd class="pd">规则文件的绝对或相对路径</dd>
</dl>

**提示：****ba update-security-group** 命令名较长，您还可以使用 **ba usg** 作为其别名。

### 删除安全组
{: #clidelsecgro}

要删除安全组，请使用以下命令：

```
cf ba delete-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**提示：****ba delete-security-group** 命令名较长，您还可以使用 **ba dsg** 作为其别名。


### 绑定安全组
{: #clibindsecgro}

有关绑定安全组的更多信息，请参阅[绑定应用程序安全组 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}。

* 要绑定 Default Staging 安全组集，请使用以下命令：

```
cf ba bind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**提示：****ba bind-staging-security-group** 命令名较长，您还可以使用 **ba bssg** 作为其别名。

* 要绑定 Default Running 安全组集，请使用以下命令：

```
cf ba bind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**提示：****ba bind-running-security-group** 命令名较长，您还可以使用 **ba brsg** 作为其别名。

* 要将安全组绑定到空间，请使用以下命令：

```
cf ba bind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
<dt class="pt dlterm">&lt;Org&gt;</dt>
<dd class="pd">安全组绑定到的组织的名称</dd>
<dt class="pt dlterm">&lt;Space&gt;</dt>
<dd class="pd">安全组绑定到的组织内空间的名称</dd>
</dl>

**提示：****ba bind-security-group** 命令名较长，您还可以使用 **ba bsg** 作为其别名。

### 取消绑定安全组
{: #cliunbindsecgro}

有关取消绑定安全组的更多信息，请参阅[取消绑定应用程序安全组 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window}。

* 要取消绑定 Default Staging 安全组集，请使用以下命令：

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**提示：****ba unbind-staging-security-group** 命令名较长，您还可以使用 **ba ussg** 作为其别名。

* 要取消绑定 Default Running 安全组集，请使用以下命令：

```
cf ba unbind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
</dl>

**提示：****ba bind-running-security-group** 命令名较长，您还可以使用 **ba brsg** 作为其别名。

* 要将安全组取消绑定到空间，请使用以下命令：

```
cf ba unbind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">安全组的名称</dd>
<dt class="pt dlterm">&lt;Org&gt;</dt>
<dd class="pd">安全组绑定到的组织的名称</dd>
<dt class="pt dlterm">&lt;Space&gt;</dt>
<dd class="pd">安全组绑定到的组织内空间的名称</dd>
</dl>

**提示：****ba unbind-staging-security-group** 命令名较长，您还可以使用 **ba usg** 作为其别名。

## 管理 buildpack
{: #admin_buildpack}

### 列出 buildpack
{: #clilistbuildpack}

如果您有应用程序目录写许可权，那么可以列出 buildpack。要列出所有 buildpack 或查看特定 buildpack，请使用以下命令：

```
cf ba buildpacks <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">可选参数，用于指定要查看的特定 buildpack。</dd>
</dl>

**提示：****ba buildpacks** 命令名较长，您还可以使用 **ba lb** 作为其别名。

### 创建并上传 buildpack
{: #clicreupbuildpack}

如果您有应用程序目录写许可权，那么可以创建并上传 buildpack。可以上传文件类型为 .zip 的任何压缩文件。要上传 buildpack，请使用以下命令：

```
cf ba create-buildpack <buildpack_name> <file_path> <position>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">要上传的 buildpack 的名称。</dd>
<dt class="pt dlterm">&lt;file_path&gt;</dt>
<dd class="pd">buildpack 压缩文件的路径。</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">在 buildpack 自动检测期间检查 buildpack 的顺序。</dd>
</dl>

**提示：****ba create-buildpack** 命令名较长，您还可以使用 **ba cb** 作为其别名。

### 更新 buildpack
{: #cliupdabuildpack}

如果您有应用程序目录写许可权，那么可以更新现有 buildpack。要更新 buildpack，请使用以下命令：

```
cf ba update-buildpack <buildpack_name> <position> <enabled> <locked>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">要更新的 buildpack 的名称。</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">在 buildpack 自动检测期间检查 buildpack 的顺序。</dd>
<dt class="pt dlterm">&lt;enabled&gt;</dt>
<dd class="pd">指示 buildpack 是否用于编译打包。</dd>
<dt class="pt dlterm">&lt;locked&gt;</dt>
<dd class="pd">指示 buildpack 是否已锁定以阻止更新。</dd>
</dl>

**提示：****ba update-buildpack** 命令名较长，您还可以使用 **ba ub** 作为其别名。

### 删除 buildpack
{: #clidelbuildpack}

如果您有应用程序目录写许可权，那么可以删除现有 buildpack。要删除 buildpack，请使用以下命令：

```
cf ba delete-buildpack <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">要删除的 buildpack 的名称。</dd>
</dl>

**提示：****ba delete-buildpack** 命令名较长，您还可以使用 **ba db** 作为其别名。
