---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 管理 CLI
{: #bluemixadmincli}

*上次更新时间：2016 年 3 月 3 日*

您可以将 Cloud Foundry 命令行界面与 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件一起使用来管理 {{site.data.keyword.Bluemix_notm}} Local 或 {{site.data.keyword.Bluemix_notm}} Dedicated 环境的用户。例如，可以从 LDAP 注册表添加用户。如果要查看有关管理 {{site.data.keyword.Bluemix_notm}} Public 帐户的信息，请参阅[管理](../../../admin/adminpublic.html#administer)。

开始之前，请安装 cf 命令行界面。{{site.data.keyword.Bluemix_notm}} 管理 CLI 插件需要 cf V6.11.2 或更高版本。[下载 Cloud Foundry 命令行界面](https://github.com/cloudfoundry/cli/releases){: new_window}

**限制：**Cygwin 不支持 Cloud Foundry 命令行界面。请在非 Cygwin 命令行窗口中使用 Cloud Foundry 命令行界面。

## 添加 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件

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

## 使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件

您可以使用 {{site.data.keyword.Bluemix_notm}} 管理 CLI 插件来添加或除去用户、分配或取消分配组织中的用户，以及执行其他管理任务。要查看命令的列表，请运行以下命令：

```
cf plugins```
{: codeblock}

有关命令的其他帮助，请使用 `-help` 选项。

### 连接并登录到 {{site.data.keyword.Bluemix_notm}}

您必须连接并登录到（如果尚未这样做）管理 CLI 插件后，才能使用该插件来管理用户。

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

### 添加用户

您可以从 LDAP 注册表向 {{site.data.keyword.Bluemix_notm}} 环境添加用户。输入以下命令：

```
cf ba add-user <user_name> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP 注册表中用户的名称。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要向其添加用户的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：****ba add-user** 命令名较长，您还可以使用 **ba au** 作为其别名。

<!-- staging-only commands start. Live for interconnect -->

### 搜索用户

可以搜索用户。输入以下命令：

```
cf ba search-users <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>

</dl>

**提示：****ba search-users** 命令名较长，您还可以使用 **ba su** 作为其别名。

### 为用户设置许可权

可以为指定用户设置许可权。输入以下命令：

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**注**：一次只能设置一个许可权。

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">为用户设置许可权：Admin、Login、Catalog（read 或 write 访问权）、Reports（read 或 write 访问权）或 Users（read 或 write 访问权）。</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">对于 Catalog、Reports 或 Users 许可权，还必须将访问级别设置为 <code>read</code> 或 <code>write</code>。</dd>
</dl>

**提示：****ba set-permissions** 命令名较长，您还可以使用 **ba sp** 作为其别名。

<!-- staging-only commands end -->

### 除去用户

您可以通过输入以下命令从 {{site.data.keyword.Bluemix_notm}} 环境中除去用户：

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 中用户的名称。</dd>

</dl>

**提示：****ba remove-user** 命令名较长，您还可以使用 **ba ru** 作为其别名。

### 添加和删除组织

可以添加和删除组织。

* 要添加组织，请输入以下命令：

```
cf ba create-organization <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要添加的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">组织的管理员的用户名。</dd>
</dl>

**提示：****ba create-organization** 命令名较长，您还可以使用 **ba co** 作为其别名。

* 要删除组织，请输入以下命令：

```
cf ba delete-organization <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要删除的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：****ba delete-organization** 命令名较长，您还可以使用 **ba do** 作为其别名。

### 向组织分配用户

您可以将 {{site.data.keyword.Bluemix_notm}} 环境中的用户分配给特定组织。输入以下命令：

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
<dd class="pd">有关 {{site.data.keyword.Bluemix_notm}} 用户角色和描述的信息，请参阅[角色](../../../admin/adminpublic.html#orgsandspaces)。</dd>
</dl>

**提示：****ba set-org** 命令名较长，您还可以使用 **ba so** 作为其别名。

### 取消向组织分配用户

您可以取消将 {{site.data.keyword.Bluemix_notm}} 环境中的用户分配给特定组织。输入以下命令：

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
<dd class="pd">有关 {{site.data.keyword.Bluemix_notm}} 用户角色和描述的信息，请参阅[角色](../../../admin/adminpublic.html#orgsandspaces)。</dd>
</dl>

**提示：****ba unset-org** 命令名较长，您还可以使用 **ba uo** 作为其别名。

### 角色

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

可以为特定组织设置使用量配额。

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

### 添加、删除和检索报告

可以添加、删除和检索安全报告。
* 要添加报告，请输入以下命令：

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
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

**提示：****ba add-report** 命令名较长，您还可以使用 **ba ar** 作为其别名。

* 要删除报告，请输入以下命令：

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

* 要检索报告，请输入以下命令：

```
cf ba retrieve-report <category> <date> <name>
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

**提示：****ba retrieve-report** 命令名较长，您还可以使用 **ba rr** 作为其别名。

### 对所有组织启用和禁用服务

您可以针对所有组织启用或禁用在 {{site.data.keyword.Bluemix_notm}}“目录”中显示的某个服务。

* 要针对所有组织启用在 {{site.data.keyword.Bluemix_notm}}“目录”中显示的某个服务，请输入以下命令：

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要启用的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
</dl>

**提示：****ba enable-service-plan** 命令名较长，您还可以使用 **ba esp** 作为其别名。

* 要针对所有组织禁用在 {{site.data.keyword.Bluemix_notm}}“目录”中显示的某个服务，请输入以下命令：

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要禁用的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
</dl>

**提示：****ba disable-service-plan** 命令名较长，您还可以使用 **ba dsp** 作为其别名。

### 添加、除去和编辑组织的服务可视性

对于能够在 {{site.data.keyword.Bluemix_notm}}“目录”中查看特定服务的组织的列表，可以在其中添加或除去组织。您还可以编辑和替换特定组织可以在 {{site.data.keyword.Bluemix_notm}}“目录”中查看的服务列表。

* 要允许某个组织在 {{site.data.keyword.Bluemix_notm}}“目录”中查看特定服务，请输入以下命令：

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要为其添加可视性的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要添加到服务的可视性列表的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：****ba add-service-plan-visibility** 命令名较长，您还可以使用 **ba aspv** 作为其别名。

* 要在 {{site.data.keyword.Bluemix_notm}}“目录”中除去某个服务对组织的可视性，请输入以下命令：

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要除去其可视性的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要从中除去服务的可视性列表的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。</dd>
</dl>

**提示：****ba remove-service-plan-visibility** 命令名较长，您还可以使用 **ba rspv** 作为其别名。

* 要替换一个组织或多个组织的所有现有可视服务，请使用以下命令：

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**注：**此命令会将指定组织的现有可视服务替换为在命令中指定的服务。

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">要使其可视的服务的名称或 GUID。如果输入非唯一的服务名称，系统将提示您选择服务套餐。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">要为其添加可视性的 {{site.data.keyword.Bluemix_notm}} 组织的名称或 GUID。可以通过在命令中输入其他组织名称或 GUID，对多个组织启用服务可视性。</dd>
</dl>

**提示：****ba edit-service-plan-visibility** 命令名较长，您还可以使用 **ba espv** 作为其别名。

### 使用服务代理程序

使用以下命令可列出所有服务代理程序，添加或删除服务代理程序，或者更新服务代理程序。

* 可以通过输入以下命令来列出服务代理程序：

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

* 可以通过输入以下命令来添加服务代理程序，以便可将定制服务添加到 {{site.data.keyword.Bluemix_notm}}“目录”：

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

* 可以通过输入以下命令来删除服务代理程序，以从 {{site.data.keyword.Bluemix_notm}}“目录”中除去定制服务：

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">定制服务代理程序的名称或 GUID。</dd>
</dl>

**提示：****ba delete-service-broker** 命令名较长，您还可以使用 **ba dsb** 作为其别名。

* 可以通过输入以下命令来更新服务代理程序：

`cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>`
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
