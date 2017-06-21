---



copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} (bx) 命令
{: #bluemix_cli}

版本：0.5.2

{{site.data.keyword.Bluemix_notm}} 命令行界面 (CLI) 提供了一组按名称空间分组的命令，供用户用于与 {{site.data.keyword.Bluemix_notm}} 进行交互。一些 {{site.data.keyword.Bluemix_notm}} 命令是现有 cf 命令的包装程序，而另一些为 {{site.data.keyword.Bluemix_notm}} 用户提供了扩展功能。以下信息列出了 {{site.data.keyword.Bluemix_notm}} CLI 支持的命令，并包含命令名称、选项、用法、先决条件、描述和示例。
{:shortdesc}

**注：***先决条件*列出使用命令前必须执行的操作。没有任何先决条件操作的命令会列出**无**。否则，先决条件可能会包含以下一个或多个操作：

<dl>
<dt>端点</dt>
<dd>使用命令前，必须通过 <code>bluemix api</code> 设置 API 端点。</dd>
<dt>登录</dt>
<dd>使用此命令之前，必须使用 <code>bluemix login</code> 命令登录。如果使用联合标识登录，请使用“--sso”选项通过一次性密码进行认证，或者使用“--apikey”通过 API 密钥进行认证。转至 {{site.data.keyword.Bluemix_notm}} 控制台的**管理** &gt; **安全性** &gt; **Bluemix API 密钥**以创建 API 密钥。
</dd>
<dt>目标</dt>
<dd>使用命令前，必须通过 <code>bluemix target</code> 命令设置组织和空间。</dd>
<dt>Docker</dt>
<dd>必须安装 Docker CLI (docker) 才能运行此命令。</dd>
</dl>

## bluemix 命令索引
{: #bx_commands_index}

使用下表中的索引可查看常用 bluemix 命令：

**注：**可以使用 Bluemix 命令的短格式；例如，`bx api` 是 `bluemix api` 的短格式。



<table summary="常规 bluemix 命令。">
 <caption>表 1. 常规 bluemix 命令</caption>
 <thead>
 <th colspan="5">常规 bluemix 命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix help](bx_cli.html#bluemix_help)</td>
 <td>[bluemix api](bx_cli.html#bluemix_api)</td>
 <td>[bluemix login](bx_cli.html#bluemix_login)</td>
 <td>[bluemix logout](bx_cli.html#bluemix_logout)</td>
 <td>[bluemix target](bx_cli.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](bx_cli.html#bluemix_info) </td>
 <td>[bluemix regions](bx_cli.html#bluemix_regions) </td>
 <td>[bluemix config](bx_cli.html#bluemix_config)</td>
 <td>[bluemix curl](bx_cli.html#bluemix_curl)</td>
 <td>[bluemix update](bx_cli.html#bluemix_update)</td>
 </tr>
 </tbody>
 </table>

<table summary="可用于管理帐户、组织、空间、角色和 API 密钥的 Bluemix 命令。">
<caption>表 2. 用于管理帐户、组织、空间、角色和 API 密钥的命令</caption>
 <thead>
 <th colspan="5">用于管理帐户、组织、空间、角色和 API 密钥的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](bx_cli.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](bx_cli.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](bx_cli.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](bx_cli.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](bx_cli.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](bx_cli.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](bx_cli.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](bx_cli.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](bx_cli.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](bx_cli.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](bx_cli.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam org-users](bx_cli.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-user-add](bx_cli.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](bx_cli.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-roles](bx_cli.html#bluemix_iam_org_roles)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-role-set](bx_cli.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](bx_cli.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](bx_cli.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-roles](bx_cli.html#bluemix_iam_space_roles)</td>
 <td>[bluemix iam space-role-set](bx_cli.html#bluemix_iam_space_role_set)</td>
</tr>
 <tr>
 <td>[bluemix iam space-role-unset](bx_cli.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix iam accounts](bx_cli.html#bluemix_iam_accounts)</td>
 <td>[bluemix iam org-account](bx_cli.html#bluemix_iam_org_account)</td>
 <td>[bluemix iam account-users](bx_cli.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](bx_cli.html#bluemix_iam_account_users_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam account-user-invite](bx_cli.html#bluemix_iam_account_user_invite)</td>
  <td>[bluemix iam account-user-reinvite](bx_cli.html#bluemix_iam_account_user_reinvite)</td>
  <td>[bluemix iam api-keys](bx_cli.html#bluemix_iam_api_keys)</td>
  <td>[bluemix iam api-key-create](bx_cli.html#bluemix_iam_api_key_create)</td>
  <td>[bluemix iam api-key-delete](bx_cli.html#bluemix_iam_api_key_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam api-key-update](bx_cli.html#bluemix_iam_api_key_update)</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
 </tr>
 </tbody>
 </table>

<table summary="可用于管理 CF 应用程序及与应用程序相关的域、路径和证书的 Bluemix 命令。">
<caption>表 3. 用于管理 CF 应用程序及与应用程序相关的域、路径和证书的命令</caption>
 <thead>
 <th colspan="5">用于管理 CF 应用程序及与应用程序相关的域、路径和证书的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](bx_cli.html#bluemix_app_push)</td>
 <td>[bluemix app list](bx_cli.html#bluemix_app_list)</td>
<td>[bluemix app show](bx_cli.html#bluemix_app_show)</td>
 <td>[bluemix app delete](bx_cli.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](bx_cli.html#bluemix_app_rename)</td>
 </tr>
 <tr>
 <td>[bluemix app start](bx_cli.html#bluemix_app_start)</td>
<td>[bluemix app stop](bx_cli.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](bx_cli.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](bx_cli.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](bx_cli.html#bluemix_app_instance_restart)</td>
 </tr>
 <tr>
 <td>[bluemix app events](bx_cli.html#bluemix_app_events)</td>
<td>[bluemix app files](bx_cli.html#bluemix_app_files)</td>
 <td>[bluemix app logs](bx_cli.html#bluemix_app_logs)</td>
 <td>[bluemix app env](bx_cli.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](bx_cli.html#bluemix_app_env_set)</td>
 </tr>
 <tr>
 <td>[bluemix app env-unset](bx_cli.html#bluemix_app_env_unset)</td>
<td>[bluemix app stacks](bx_cli.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack-show](bx_cli.html#bluemix_app_stack_show)</td>
 <td>[bluemix app manifest-create](bx_cli.html#bluemix_app_manifest_create)</td>
 <td>[bluemix app domain-cert](bx_cli.html#bluemix_app_domain_cert)</td>
 </tr>
 <tr>
  <td>[bluemix app domain-cert-add](bx_cli.html#bluemix_app_domain_cert_add)</td>
  <td>[bluemix app domain-cert-remove](bx_cli.html#bluemix_app_domain_cert_remove)</td>
  <td>[bluemix app domains](bx_cli.html#bluemix_app_domains)</td>
  <td>[bluemix app domain-create](bx_cli.html#bluemix_app_domain_create)</td>
  <td>[bluemix app domain-delete](bx_cli.html#bluemix_app_domain_delete)</td>
 </tr>
 <tr>
  <td>[bluemix app shared-domain-create](bx_cli.html#bluemix_app_shared_domain_create)</td>
  <td>[bluemix app shared-domain-delete](bx_cli.html#bluemix_app_shared_domain_delete)</td>
  <td>[bluemix app routes](bx_cli.html#bluemix_app_routes)</td>
  <td>[bluemix app route-check](bx_cli.html#bluemix_app_route_check)</td>
  <td>[bluemix app route-map](bx_cli.html#bluemix_app_route_map)</td>
 </tr>
 <tr>
  <td>[bluemix app route-unmap](bx_cli.html#bluemix_app_route_unmap)</td>
  <td>[bluemix app route-create](bx_cli.html#bluemix_app_route_create)</td>
  <td>[bluemix app route-delete](bx_cli.html#bluemix_app_route_delete)</td>
  <td>[bluemix app orphaned-routes-delete](bx_cli.html#bluemix_app_orphaned_routes_delete)</td>
  <td></td>
 </tr>
  </tbody>
 </table>

<table summary="可用于管理 Bluemix 服务的 bluemix 命令">
 <caption>表 4. 用于管理 Bluemix 服务的命令</caption>
 <thead>
 <th colspan="5">用于管理 Bluemix 服务的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix service offerings](bx_cli.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](bx_cli.html#bluemix_service_list)</td>
 <td>[bluemix service show](bx_cli.html#bluemix_service_show)</td>
 <td>[bluemix service create](bx_cli.html#bluemix_service_create)</td>
 <td>[bluemix service update](bx_cli.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](bx_cli.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](bx_cli.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](bx_cli.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](bx_cli.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](bx_cli.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](bx_cli.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](bx_cli.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](bx_cli.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](bx_cli.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](bx_cli.html#bluemix_service_user_provided_update)</td>
 </tr>
  </tbody>
 </table>

<table summary="可用于管理 Bluemix 目录、插件、帐单和安全设置的 bluemix 命令">
<caption>表 5. 用于管理 Bluemix 目录、插件、帐单和安全设置的命令</caption>
 <thead>
 <th colspan="5">用于管理 Bluemix 目录、插件、帐单和安全设置的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix catalog templates](bx_cli.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](bx_cli.html#bluemix_catalog_template)</td>
<td>[bluemix catalog template-run](bx_cli.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](bx_cli.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](bx_cli.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](bx_cli.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](bx_cli.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](bx_cli.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](bx_cli.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](bx_cli.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix plugin update](bx_cli.html#bluemix_plugin_update)</td>
 <td>[bluemix billing account-usage](bx_cli.html#bluemix_billing_account_usage)</td>
 <td>[bluemix billing org-usage](bx_cli.html#bluemix_billing_org_usage)</td>
 <td>[bluemix billing orgs-usage-summary](bx_cli.html#bluemix_billing_orgs_usage_summary)</td>
 <td></td>
 </tr>
 </tbody>
 </table>
 
## bluemix help
{: #bluemix_help}
显示 {{site.data.keyword.Bluemix_notm}} CLI 第一级内置命令和受支持名称空间的一般帮助，或者显示特定内置命令或名称空间的帮助。

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>COMMAND|NAMESPACE（可选）</dt>
   <dd>显示其帮助信息的命令或名称空间。如果未指定，将显示 {{site.data.keyword.Bluemix_notm}} CLI 的一般帮助。</dd>
   </dl>



<strong>示例</strong>：

显示 {{site.data.keyword.Bluemix_notm}} CLI 的一般帮助：

```
bluemix help
```

显示 `info` 命令的帮助：

```
bluemix help info
```



## bluemix api
{: #bluemix_api}
设置或查看 {{site.data.keyword.Bluemix_notm}} API 端点。

```
bluemix api [API_ENDPOINT] [--unset] [--skip-ssl-validation]
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：
   <dl>
   <dt>API_ENDPOINT（可选）</dt>
   <dd>作为目标的 API 端点，例如 `https://api.chinabluemix.net`。如果未指定 *API_ENDPOINT* 和 `--unset` 选项，将显示当前 API 端点。</dd>
   <dt>--unset（可选）</dt>
   <dd>除去 API 端点设置。</dd>
   <dt>--skip-ssl-validation（可选）</dt>
   <dd>绕过 HTTP 请求的 SSL 验证。</dd>
   </dl>
<strong>示例</strong>：

将 API 端点设置为 api.chinabluemix.net：

```
bluemix api api.chinabluemix.net
```

```
bluemix api https://api.chinabluemix.net --skip-ssl-validation
```

查看当前 API 端点：

```
bluemix api
```

取消设置 API 端点：

```
bluemix api --unset
```


## bluemix login
{: #bluemix_login}

用户登录。 

```
bluemix login [OPTIONS...]
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：
<dl>
  <dt>-a <i>API_ENDPOINT</i>（可选）</dt>
  <dd> API 端点（例如：api.ng.bluemix.net）</dd>
  <dt> --apikey <i>API_KEY 或 @API_KEY_FILE_PATH</i>
  <dd> API 密钥内容或用 @ 指示的 API 密钥文件路径</dd>
  <dt> --sso（可选）</dt>
  <dd> 使用一次性密码登录</dd>
  <dt> -u <i>USERNAME</i>（可选）</dt>
  <dd> 用户名</dd>
  <dt> -p <i>PASSWORD</i>（可选）</dt>
  <dd> 密码</dd>
  <dt> -c <i>ACCOUNT_ID</i>（可选）</dt>
  <dd> 目标帐户的标识</dd>
  <dt> -o <i>ORG_NAME</i>（可选）</dt>
  <dd> 目标组织的名称</dd>
  <dt> -s <i>SPACE_NAME</i>（可选）</dt>
  <dd> 目标空间的名称</dd>
  <dt> --skip-ssl-validation（可选）</dt>
  <dd> 绕过 HTTP 请求的 SSL 验证。建议不要使用此选项。</dd>
</dl>

<strong>示例</strong>：

交互式登录：

```
bluemix login
```

使用用户名和密码登录，并设置目标帐户、组织和空间：

```
bluemix login -u username -p password -c MyAccountID -o MyOrg -s MySpace
```

使用一次性密码登录，并设置目标帐户、组织和空间

```
bluemix login --sso -c MyAccountID -o MyOrg -s MySpace
```

使用 API 密钥登录并设置目标：

* API 密钥具有关联的帐户

```
bluemix login --apikey api-key-string -o MyOrg -s MySpace
```

```
bluemix login --apikey @filename -o MyOrg -s MySpace
```

* API 密钥没有关联的帐户

```
bluemix login --apikey api-key-string -c MyAccountID -o MyOrg -s MySpace
```

```
bluemix login --apikey @fileName -c MyAccountID -o MyOrg -s MySpace
```

<strong>注：</strong>如果 API 密钥具有关联的帐户，那么不允许切换到其他帐户。


## bluemix logout
{: #bluemix_logout}

注销用户。

```
bluemix logout
```

<strong>先决条件</strong>：无


## bluemix target
{: #bluemix_target}


设置或查看目标帐户、区域、组织或空间。

```
bluemix target [-c ACCOUNT_ID] [-r REGION] [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>-c <i>ACCOUNT_ID</i>（可选）</dt>
   <dd>要作为目标的帐户的标识。</dd>
   <dt>-r <i>REGION</i>（可选）</dt>
   <dd>要切换到的目标区域。</dd>
   <dt>-o <i>ORG_NAME</i>（可选）</dt>
   <dd>要作为目标的组织的名称。</dd>
   <dt>-s <i>SPACE_NAME</i>（可选）</dt>
   <dd>要作为目标的空间的名称。</dd>
   </dl>
如果未指定任何选项，那么将显示当前帐户、区域、组织和空间。
<strong>示例</strong>：

设置当前帐户、组织和空间

```
bluemix target -c MyAccountID -o MyOrg -s MySpace
```

切换到新区域

```
bluemix target -r eu-gb
```

查看当前帐户、区域、组织和空间：

```
bluemix target
```


## bluemix info
{: #bluemix_info}

查看基本 {{site.data.keyword.Bluemix_notm}} 信息，包括当前区域、云控制器版本以及一些有用的端点，例如用于登录和交换访问令牌的端点。

```
bluemix info
```

<strong>先决条件</strong>：端点


## bluemix config
{: #bluemix_config}


将缺省值写入配置文件。

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：
   <dl>
   <dt>--http-timeout <i>TIMEOUT_IN_SECONDS</i></dt>
   <dd>HTTP 请求的超时值。缺省值为 60 秒。</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>跟踪对终端或指定文件的 HTTP 请求。</dd>
   <dt>--color true|false</dt>
   <dd>启用或禁用颜色输出。缺省情况下，会启用颜色输出。</dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
   <dd>设置缺省语言环境。如果 LOCALE 为 <i>CLEAR</i>，将删除先前的语言环境。</dd>
   <dt>--check-version true|false</dt>
   <dd>启用或禁用 CLI 版本检查。</dd>
   </dl>

一次只能指定其中一个选项。

<strong>示例</strong>：

将 HTTP 请求超时设置为 30 秒：

```
bluemix config --http-timeout 30
```

启用 HTTP 请求的跟踪输出：

```
bluemix config --trace true
```

跟踪对指定文件 */home/usera/my_trace* 的 HTTP 请求：

```
bluemix config --trace /home/usera/my_trace
```

禁用颜色输出：

```
bluemix config --color false
```

将语言环境设置为 zh_Hans：

```
bluemix config --locale zh_Hans
```

清除语言环境设置：

```
bluemix config --locale CLEAR
```


## bluemix curl
{: #bluemix_curl}

执行针对 {{site.data.keyword.Bluemix_notm}} 的原始 HTTP 请求。缺省情况下，*Content-Type* 设置为 *application/json*。此命令会向 {{site.data.keyword.Bluemix_notm}} 多云控制代理发送请求。有关受支持的路径，请参阅 [Cloud Foundry API 文档 ](http://apidocs.cloudfoundry.org/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 中的 API 路径定义。

```
bluemix curl PATH [OPTIONS...]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt><i>PATH</i>（必需）</dt>
   <dd>资源的 URL 路径。例如，/v2/apps。</dd>
   <dt><i>OPTIONS</i>（可选）</dt>
   <dd>`bluemix curl` 命令支持的选项与 `cf curl` 命令支持的那些选项相同。</dd>
   </dl>

<strong>示例</strong>：

查看当前帐户的所有组织的信息：

```
bluemix curl /v2/organizations
```

## bluemix update
{: #bluemix_update}

将 CLI 更新到最新版本

```
bluemix update
```

<strong>先决条件</strong>：无

## bluemix regions
{: #bluemix_regions}

查看 {{site.data.keyword.Bluemix_notm}} 上所有区域的信息。

```
bluemix regions
```

<strong>先决条件</strong>：端点


## bluemix iam orgs
{: #bluemix_iam_orgs}

列出所有组织

```
bluemix iam orgs [-r REGION] [--guid]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>-r <i>REGION</i>（可选）</dt>
   <dd>显示其组织信息的区域。如果设置为“all”，将列出所有区域中的所有组织。</dd>
   <dt>--guid（可选）</dt>
   <dd>显示组织的 GUID。</dd>
   </dl>

<strong>示例</strong>：

列出区域 `us-south` 中的所有组织并显示 GUID

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

显示指定组织的信息。

```
bluemix iam org ORG_NAME [--guid]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>ORG_NAME（必需）</dt>
   <dd>组织的名称。</dd>
   <dt>--guid（可选）</dt>
   <dd>显示组织的 GUID。</dd>
   </dl>

<strong>示例</strong>：

显示组织 `IBM` 的信息并显示 GUID

```
bluemix iam org IBM --guid
```


## bluemix iam org-create
{: #bluemix_iam_org_create}

创建新组织。此操作只能由帐户所有者执行。

```
bluemix iam org-create ORG_NAME
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>ORG_NAME（必需）</dt>
   <dd>要创建的组织的名称。</dd>
   </dl>

<strong>示例</strong>：

创建名为 `IBM` 的组织。

```
bluemix iam org-create IBM
```

## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

将组织从当前区域复制到其他区域。

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>ORG_NAME（必需）</dt>
   <dd>要复制的现有组织的名称。</dd>
   <dt>REGION_NAME（必需）</dt>
   <dd>托管所复制组织的区域的名称。</dd>
   </dl>

<strong>示例</strong>：

将组织 `myorg` 复制到区域 `eu-gb`：

```
bluemix iam org-replicate myorg eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

重命名组织。此操作只能由组织管理员执行。

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>OLD_ORG_NAME（必需）</dt>
   <dd>要重命名的组织的旧名称。</dd>
   <dt>NEW_ORG_NAME（必需）</dt>
   <dd>组织要重命名为的新名称。</dd>
   </dl>

## bluemix iam org-delete
{: #bluemix_iam_org_delete}

删除当前区域中的指定组织。

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>ORG_NAME（必需）</dt>
   <dd>要删除的现有组织的名称。</dd>
   <dt>-f（可选）</dt>
   <dd>强制删除而不确认。</dd>
   <dt>--all（可选）</dt>
   <dd>从所有区域删除组织。</dd>
   </dl>


## bluemix iam spaces
{: #bluemix_iam_spaces}

此命令的功能和选项与 `cf spaces` 命令的相同。


## bluemix iam space
{: #bluemix_iam_space}

此命令的功能和选项与 `cf space` 命令的相同。


## bluemix iam space-create
{: #bluemix_iam_space_create}

此命令的功能和选项与 `cf create-space` 命令的相同。


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


此命令的功能和选项与 `cf rename-space` 命令的相同。


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


此命令的功能和选项与 `cf delete-space` 命令的相同。

## bluemix iam org-users
{: #bluemix_iam_org_users}

按角色显示指定组织中的用户。

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
<dl>
<dt>ORG_NAME（必需）</dt>
<dd>组织的名称。</dd>
<dt>-a（可选）</dt>
<dd>列出指定组织中的所有用户，但不按角色分组。</dd>
</dl>

## bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

将用户添加到组织（需要组织管理员）。

```
 bluemix iam org-user-add USER_NAME ORG
```

## bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

从组织移除用户（仅限组织管理员或用户自己）

```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>命令选项</strong>：
<dl>
<dt>--force, -f</dt>
<dd>强制删除而不确认。</dd>
</dl>

## bluemix iam org-roles
{: #bluemix_iam_org_roles}

获取当前用户的所有组织角色

```
bluemix iam org-roles
```

<strong>先决条件</strong>：端点和登录

## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

向用户分配组织角色。此操作只能由组织管理员执行。

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
  <dl>
   <dt>USER_NAME（必需）</dt>
   <dd>要分配的用户的名称。</dd>
   <dt>ORG_NAME（必需）</dt>
   <dd>要将此用户分配到的组织的名称。</dd>
   <dt>ORG_ROLE（必需）</dt>
   <dd>要将此用户分配到的组织角色的名称。例如：
<ul>
   <li>OrgManager：此角色可以邀请和管理用户，选择并更改套餐，以及设置花费限制。</li>
   <li>BillingManager：此角色可以创建和管理缴费帐户和付款信息。</li>
   <li>OrgAuditor：此角色具有对组织信息和报告的只读访问权。</li>
   </ul>
   </dd>
  </dl>

<strong>示例</strong>：

将用户 `Mary` 以 `OrgManager` 角色分配给组织 `IBM`：

```
bluemix iam org-role-set Mary IBM OrgManager
```


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

除去用户的组织角色。此操作只能由组织管理员执行。

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>USER_NAME（必需）</dt>
   <dd>要除去的用户的名称。</dd>
   <dt>ORG_NAME（必需）</dt>
   <dd>要将此用户从中除去的组织的名称。</dd>
   <dt>ORG_ROLE（必需）</dt>
   <dd>要将此用户从中除去的组织角色的名称。例如：
<ul>
   <li>OrgManager：此角色可以邀请和管理用户，选择并更改套餐，以及设置花费限制。</li>
   <li>BillingManager：此角色可以创建和管理缴费帐户和付款信息。</li>
   <li>OrgAuditor：此角色具有对组织信息和报告的只读访问权。</li>
   </ul>
   </dd>
    </dl>

<strong>示例</strong>：

从组织 `IBM` 中除去用户 `Mary` 的 `OrgManager` 角色：

```
bluemix iam org-role-unset Mary IBM OrgManager
```

## bluemix iam space-users
{: #bluemix_iam_space_users}

按角色显示指定空间中的用户。

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>ORG_NAME（必需）</dt>
   <dd>组织的名称。</dd>
   <dt>SPACE_NAME（必需）</dt>
   <dd>空间的名称。</dd>
   </dl>


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

向用户分配空间角色。此操作只能由空间管理员执行。

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：

   <dl>
   <dt>USER_NAME（必需）</dt>
   <dd>要分配的用户的名称。</dd>
   <dt>ORG_NAME（必需）</dt>
   <dd>要将此用户分配到的组织的名称。</dd>
   <dt>SPACE_NAME（必需）</dt>
   <dd>要将此用户分配到的空间的名称。</dd>
   <dt>SPACE_ROLE（必需）</dt>
   <dd>要将此用户分配到的空间角色的名称。例如：
<ul>
   <li>SpaceManager：此角色可以邀请和管理用户，以及启用给定空间的功能。</li>
   <li>SpaceDeveloper：此角色可以创建和管理应用程序与服务，以及查看日志和报告。</li>
   <li>SpaceAuditor：此角色可以查看空间的日志、报告和设置。</li>
   </ul></dd>
    </dl>

<strong>示例</strong>：

将用户 `Mary` 以 `SpaceManager` 角色分配给组织 `IBM` 和空间 `Cloud`：

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

除去用户的空间角色。此操作只能由空间管理员执行。

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：

   <dl>
   <dt>USER_NAME（必需）</dt>
   <dd>要除去的用户的名称。</dd>
   <dt>ORG_NAME（必需）</dt>
   <dd>要将此用户从中除去的组织的名称。</dd>
   <dt>SPACE_NAME（必需）</dt>
   <dd>要将此用户从中除去的空间的名称。</dd>
   <dt>SPACE_ROLE（必需）</dt>
   <dd>要将此用户从中除去的空间角色的名称。例如：
<ul>
   <li>SpaceManager：此角色可以邀请和管理用户，以及启用给定空间的功能。</li>
   <li>SpaceDeveloper：此角色可以创建和管理应用程序与服务，以及查看日志和报告。</li>
   <li>SpaceAuditor：此角色可以查看空间的日志、报告和设置。</li>
   </ul></dd>
    </dl>


<strong>示例</strong>：

从组织 `IBM` 和空间 `Cloud` 中除去用户 `Mary` 的 `SpaceManager` 角色：

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```

## bluemix iam accounts
{: #bluemix_iam_accounts}

列出当前用户的所有帐户

```
bluemix iam accounts
```

<strong>先决条件</strong>：端点和登录


## bluemix iam org-account
{: #bluemix_iam_org_account}

显示指定组织的帐户（需要组织用户）

```
bluemix iam org-account ORG_NAME [--guid]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
<dl>
  <dt>--guid（可选）</dt>
  <dd>仅显示帐户标识</dd>
</dl>


## bluemix iam account-users
{: #bluemix_iam_account_users}

显示与帐户关联的用户。此操作只能由帐户所有者执行。

```
bluemix iam account-users
```

## bluemix iam account-user-delete
{: #bluemix_iam_account_user_delete}

从当前帐户中删除用户（仅帐户所有者）

```
bluemix iam account-user-delete USERNAME [-f]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
<dl>
<dt>USERNAME（必需）</dt>
<dd>用户名</dd>
<dt>--force, -f（可选）</dt>
<dd>强制删除而不确认。</dd>
</dl>

## bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}

邀请用户加入已设置组织和空间角色的帐户。此操作只能由帐户所有者执行。

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
<dl>
   <dt>USER_NAME（必需）</dt>
   <dd>要邀请的用户的名称。</dd>
   <dt>ORG_NAME（必需）</dt>
   <dd>要邀请此用户加入的组织的名称。</dd>
   <dt>ORG_ROLE（必需）</dt>
   <dd>要邀请此用户加入的组织角色的名称。例如：
<ul>
  <li>OrgManager：此角色可以邀请和管理用户，选择并更改套餐，以及设置花费限制。</li>
  <li>BillingManager：此角色可以创建和管理缴费帐户和付款信息。</li>
  <li>OrgAuditor：此角色具有对组织信息和报告的只读访问权。</li>
  </ul> </dd>
   <dt>SPACE_NAME（必需）</dt>
   <dd>要邀请此用户加入的空间的名称。</dd>
   <dt>SPACE_ROLE（必需）</dt>
   <dd>要邀请此用户加入的空间的名称。要邀请此用户加入的空间角色的名称。例如：
<ul>
<li>SpaceManager：此角色可以邀请和管理用户，以及启用给定空间的功能。</li>
<li>SpaceDeveloper：此角色可以创建和管理应用程序与服务，以及查看日志和报告。</li>
<li>SpaceAuditor：此角色可以查看空间的日志、报告和设置。</li>
</ul>
</dd>
</dl>

<strong>示例</strong>：

邀请用户 `Mary` 以 `OrgManager` 角色加入组织 `IBM`，并以 `SpaceAuditor` 角色加入空间 `Cloud`：

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

向用户重新发送邀请（必须是组织管理员或帐户所有者）

```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```

## bluemix iam api-keys
{: #bluemix_iam api_keys}

列出所有 Bluemix 平台 API 密钥

```
bluemix iam api-keys
```

<strong>先决条件</strong>：端点和登录

## bluemix iam api-key-create
{: #bluemix_iam_api_key_create}

创建新的 Bluemix 平台 API 密钥

```
bluemix iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
<dl>
<dt>NAME（必需）</dt>
<dd>要创建的 API 密钥的名称。</dd>
<dt>-d <i>DESCRIPTION</i>（可选）</dt>
<dd>API 密钥的描述</dd>
<dt>-f, -- file <i>FILE</i></dt>
<dd>将 API 密钥信息保存到指定的文件。如果未设置，将显示 JSON 内容。</dd>
</dl>

<strong>示例</strong>：

创建 API 密钥并将其保存到文件

```
bluemix iam api-key-create MyKey -d "this is my API key" -f key_file
```

## bluemix iam api-key-update
{: #bluemix_iam_api_key_update}

更新 Bluemix 平台 API 密钥

```
bluemix iam api-key-update NAME [-n NAME] [-d DESCRIPTION]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
<dl>
<dt>NAME（必需）</dt>
<dd>要更新的 API 密钥的旧名称。</dd>
<dt>-n <i>NAME</i>（可选）</dt>
<dd>API 密钥的新名称</dd>
<dt>-d <i>DESCRIPTION</i>（可选）</dt>
<dd>API 密钥的新描述</dd>
</dl>

<strong>示例</strong>：

更新 API 密钥的描述：

```
bluemix iam api-key-update MyKey -d "the new description of my key"
```

## bluemix api-key-delete
{: #bluemix_api_key_delete}

删除 Bluemix 平台 API 密钥

```
bluemix iam api-key-delete NAME [-f]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
<dl>
<dt>NAME（必需）</dt>
<dd>要删除的 API 密钥的名称。</dd>
<dt>-f（可选）</dt>
<dd>强制删除而不确认。</dd>
</dl>


## bluemix app push
{: #bluemix_app_push}

此命令的功能和选项与 `cf push` 命令的相同。


## bluemix app list
{: #bluemix_app_list}

此命令的功能和选项与 `cf apps` 命令的相同。


## bluemix app show
{: #bluemix_app_show}

此命令的功能和选项与 `cf app` 命令的相同。


## bluemix app delete
{: #bluemix_app_delete}

此命令的功能和选项与 `cf delete` 命令的相同。


## bluemix app rename
{: #bluemix_app_rename}

此命令的功能和选项与 `cf rename` 命令的相同。


## bluemix app start
{: #bluemix_app_start}

此命令的功能和选项与 `cf start` 命令的相同。


## bluemix app stop
{: #bluemix_app_stop}

此命令的功能和选项与 `cf stop` 命令的相同。


## bluemix app restart
{: #bluemix_app_restart}

此命令的功能和选项与 `cf restart` 命令的相同。


## bluemix app restage
{: #bluemix_app_restage}


此命令的功能和选项与 `cf restage` 命令的相同。


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


此命令的功能和选项与 `cf restart-app-instance` 命令的相同。


## bluemix app events
{: #bluemix_app_events}

此命令的功能和选项与 `cf events` 命令的相同。


## bluemix app files
{: #bluemix_app_files}

此命令的功能和选项与 `cf files` 命令的相同。


## bluemix app logs
{: #bluemix_app_logs}

此命令的功能和选项与 `cf logs` 命令的相同。


## bluemix app env
{: #bluemix_app_env}

此命令的功能和选项与 `cf env` 命令的相同。


## bluemix app env-set
{: #bluemix_app_env_set}

此命令的功能和选项与 `cf set-env` 命令的相同。


## bluemix app env-unset
{: #bluemix_app_env_unset}

此命令的功能和选项与 `cf unset-env` 命令的相同。


## bluemix app stacks
{: #bluemix_app_stacks}

此命令的功能和选项与 `cf stacks` 命令的相同。


## bluemix app stack-show
{: #bluemix_app_stack_show}

此命令的功能和选项与 `cf stack` 命令的相同。


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

此命令的功能和选项与 `cf create-app-manifest` 命令的相同。

## bluemix app domain-cert 
{: #bluemix_app_domain_cert}

列出域的证书信息。

```
bluemix app domain-cert DOMAIN_NAME
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
<dl>
<dt>DOMAIN_NAME（必需）</dt>
<dd>托管证书的域。</dd>
</dl>


<strong>示例</strong>：

查看域 `ibmcxo-eventconnect.com` 的证书信息：

```
bluemix app domain-cert ibmcxo-eventconnect.com
```

## bluemix app domain-cert-add
{: #bluemix_app_domain_cert_add}

将证书添加到当前组织中的指定域。

```
bluemix app domain-cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [-t TRUST_STORE_FILE]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：
   <dl>
   <dt>DOMAIN（必需）</dt>
   <dd>将证书添加到其中的域。</dd>
   <dt>-k <i>PRIVATE_KEY_FILE</i>（必需）</dt>
   <dd>专用密钥文件路径。</dd>
   <dt>-c <i>CERT_FILE</i>（必需）</dt>
   <dd>证书文件路径。</dd>
   <dt>-p <i>PASSWORD</i>（可选）</dt>
   <dd>证书的密码。</dd>
   <dt>-i <i>INTERMEDIATE_CERT_FILE</i>（可选）</dt>
   <dd>中间证书文件路径。</dd>
   <dt>-t <i>TRUST_STORE_FILE</i>（可选）</dt>
   <dd>信任库文件。</dd>
   </dl>


<strong>示例</strong>：

将证书添加到域 `ibmcxo-eventconnect.com`：

```
bluemix app domain-cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```

## bluemix app domain-cert-remove
{: #bluemix_app_domain_cert_remove}

从当前组织中的指定域除去证书。

```
bluemix app domain-cert-remove DOMAIN [-f]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt>DOMAIN（必需）</dt>
   <dd>要从中除去证书的域。</dd>
   <dt>-f（可选）</dt>
   <dd>强制删除而不确认。</dd>
   </dl>

## bluemix app domains
{: #bluemix_app_domains}

此命令的功能和选项与 `cf domains` 命令的相同。


## bluemix app domain-create
{: #bluemix_app_domain_create}

此命令的功能和选项与 `cf create-domain` 命令的相同。


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

此命令的功能和选项与 `cf delete-domain` 命令的相同。


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

此命令的功能和选项与 `cf create-shared-domain` 命令的相同。


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

此命令的功能和选项与 `cf delete-shared-domain` 命令的相同。

## bluemix app routes
{: #bluemix_app_routes}

此命令的功能和选项与 `cf routes` 命令的相同。


## bluemix app route-check
{: #bluemix_app_route_check}

此命令的功能和选项与 `cf check-route` 命令的相同。


## bluemix app route-map
{: #bluemix_app_route_map}

将路径映射到具有指定域和主机名的现有 cf 应用程序或容器组。

```
bluemix app route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME（必需）</dt>
   <dd>要使用路径映射到的 cf 应用程序或容器组的名称。</dd>
   <dt>DOMAIN（必需）</dt>
   <dd>路径的域。例如，mychinabluemix.net 或 chinabluemix.net。</dd>
   <dt>-n <i>HOST_NAME</i>（可选）</dt>
   <dd>路径的主机名。如果未提供，缺省情况下主机名将设置为应用程序名称或容器组名称。</dd>
   </dl>

<strong>示例</strong>：

使用指定的域将路径映射到 `my-app`：

```
bluemix app route-map my-app mychinabluemix.net
```

使用指定域和主机名将路径映射到“my-container-group”：

```
bluemix app route-map my-container-group chinabluemix.net -n abc
```


## bluemix app route-unmap
{: #bluemix_app_route_unmap}

取消来自现有 cf 应用程序或容器组中的指定路径映射。

```
bluemix app route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME（必需）</dt>
   <dd>cf 应用程序或容器组的名称。</dd>
   <dt>DOMAIN（必需）</dt>
   <dd>路径的域（例如，mychinabluemix.net 或 chinabluemix.net）。</dd>
   <dt>-n <i>HOST_NAME</i>（可选）</dt>
   <dd>路径的主机名。如果未提供，缺省情况下主机名将设置为应用程序名称或容器组名称。</dd>
   </dl>

<strong>示例</strong>：

从 `my-app` 取消 `my-app.mychinabluemix.net` 的映射：

```
bluemix app route-unmap my-app mychianbluemix.net
```

从 `my-container-group` 取消 `abc.chinabluexmix.net` 的映射：

```
bluemix app route-unmap my-container-group chinabluemix.net -n abc
```


## bluemix app route-create
{: #bluemix_app_route_create}

此命令的功能和选项与 `cf create-route` 命令的相同。


## bluemix app route-delete
{: #bluemix_app_route_delete}

此命令的功能和选项与 `cf delete-route` 命令的相同。


## bluemix app orphaned-routes-delete
{: #bluemix_app_orphaned_routes_delete}

此命令的功能和选项与 `cf delete-orphaned-routes` 命令的相同。


## bluemix app domains
{: #bluemix_app_domains}

此命令的功能和选项与 `cf domains` 命令的相同。


## bluemix app domain-create
{: #bluemix_app_domain_create}

此命令的功能和选项与 `cf create-domain` 命令的相同。


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

此命令的功能和选项与 `cf delete-domain` 命令的相同。


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

此命令的功能和选项与 `cf create-shared-domain` 命令的相同。


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

此命令的功能和选项与 `cf delete-shared-domain` 命令的相同。


## bluemix service offerings
{: #bluemix_service_offerings}


此命令的功能和选项与 `cf marketplace` 命令的相同。


## bluemix service list
{: #bluemix_service_list}

此命令的功能和选项与 `cf services` 命令的相同。


## bluemix service show
{: #bluemix_service_show}

此命令的功能和选项与 `cf service` 命令的相同。


## bluemix service create
{: #bluemix_service_create}

此命令的功能和选项与 `cf create-service` 命令的相同。


## bluemix service update
{: #bluemix_service_update}

此命令的功能和选项与 `cf update-service` 命令的相同。


## bluemix service delete
{: #bluemix_service_delete}

此命令的功能和选项与 `cf delete-service` 命令的相同。


## bluemix service rename
{: #bluemix_service_rename}

此命令的功能和选项与 `cf rename-service` 命令的相同。


## bluemix service bind
{: #bluemix_service_bind}

此命令的功能和选项与 `cf bind-service` 命令的相同。


## bluemix service unbind
{: #bluemix_service_unbind}

此命令的功能和选项与 `cf unbind-service` 命令的相同。


## bluemix service key-create
{: #bluemix_service_key_create}

此命令的功能和选项与 `cf create-service-key` 命令的相同。


## bluemix service key-delete
{: #bluemix_service_key_delete}

此命令的功能和选项与 `cf delete-service-key` 命令的相同。


## bluemix service keys
{: #bluemix_service_keys}

此命令的功能和选项与 `cf service-keys` 命令的相同。


## bluemix service key-show
{: #bluemix_service_key_show}

此命令的功能和选项与 `cf service-key` 命令的相同。


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

此命令的功能和选项与 `cf create-user-provided-service` 命令的相同。


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

此命令的功能和选项与 `cf update-user-provided-service` 命令的相同。


## bluemix catalog templates
{: #bluemix_catalog_templates}

查看 Bluemix 上的样板模板。

```
bluemix catalog templates [-d]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：

   <dl>
   <dt>-d（可选）</dt>
   <dd>如果指定了 <i>-d</i> 选项，那么还会显示每个模板的描述。否则，只显示每个模板的标识和名称。</dd>
   </dl>


## bluemix catalog template
{: #bluemix_catalog_template}

查看指定样板模板的详细信息。

```
bluemix catalog template TEMPLATE_ID
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>TEMPLATE_ID（必需）</dt>
   <dd>样板模板的标识。使用 <i>bluemix templates</i> 可查看所有模板的标识。</dd>
   </dl>


<strong>示例</strong>：

查看模板 `mobileBackendStarter` 的详细信息：

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

使用指定 URL 和描述基于指定模板创建 cf 应用程序。缺省情况下，新应用程序将自动启动。

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：
   <dl>
   <dt>TEMPLATE_ID（必需）</dt>
   <dd>创建应用程序时将基于的模板。使用 <i>bluemix templates</i> 可查看所有模板的标识。</dd>
   <dt>CF_APP_NAME（必需）</dt>
   <dd>要创建的 cf 应用程序的名称。</dd>
   <dt>-u <i>URL</i>（可选）</dt>
   <dd>应用程序的路径。如果未指定，Bluemix 将基于应用程序名称和缺省域自动设置路径。</dd>
   <dt>-d <i>DESCRIPTION</i>（可选）</dt>
   <dd>应用程序的描述。</dd>
   <dt>--no-start（可选）</dt>
   <dd>应用程序创建后不自动启动。如果未指定，应用程序创建后将自动启动。</dd>
   </dl>


<strong>示例</strong>：

基于 `javaHelloWorld` 模板创建 cf 应用程序 `my-app`：

```
bluemix catalog template-run javaHelloWorld my-app
```

基于 `rubyHelloWorld` 模板创建应用程序 `my-ruby-app`，路径为 `myrubyapp.chinabluemix.net`，描述为 `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`：

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

基于 `pythonHelloWorld` 模板创建应用程序 `my-python-app`，不带自动启动：

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```

## bluemix billing account-usage
{: #bluemix_billing_account_usage}

显示帐户的每月使用情况和成本。

```
bluemix billing account-usage [-d YYYY-MM] [--json]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：

<dl>
  <dt>-d MONTH_DATE（可选）</dt>
  <dd>显示使用 YYYY-MM 格式指定的月份和日期的数据。如果未指定，那么会显示当月的使用情况。</dd>
  <dt>--json（可选）</dt>
  <dd>以 JSON 格式显示使用情况结果。</dd>
</dl>

<strong>示例</strong>：

显示 2016 年 6 月我的帐户的使用情况和成本报告：

```
bluemix billing account-usage -d 2016-06
```

## bluemix billing org-usage
{: #bluemix_billing_org_usage}

显示组织的每月使用情况详细信息。此操作只能由组织的记帐管理员执行。

```
bluemix billing org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：

<dl>
  <dt>ORG_NAME（必需）</dt>
  <dd>组织的名称。</dd>
  <dt>-d MONTH_DATE（可选）</dt>
  <dd>显示使用 YYYY-MM 格式指定的月份和日期的数据。如果未指定，那么会显示当月的使用情况。</dd>
  <dt>-r REGION_NAME</dt>
  <dd>托管组织的区域名称。如果设置为“all”，那么会显示所有区域中的组织使用情况。</dd>
  <dt>--json（可选）</dt>
  <dd>以 JSON 格式显示使用情况结果。</dd>
</dl>



## bluemix billing orgs-usage-summary
{: #bluemix_billing_orgs_usage_summary}

显示我的帐户中组织的每月使用情况摘要。

```
bluemix billing orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：

<dl>
  <dt>-d MONTH_DATE（可选）</dt>
  <dd>显示使用 YYYY-MM 格式指定的月份和日期的数据。如果未指定，那么会显示当月的使用情况。</dd>
  <dt>-r REGION_NAME</dt>
  <dd>托管组织的区域的名称。如果设置为“all”，那么会显示所有区域中组织的使用情况摘要。</dd>
  <dt>--json（可选）</dt>
  <dd>以 JSON 格式显示使用情况结果。</dd>
</dl>


## bluemix plugin repos
{: #bluemix_plugin_repos}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中注册的所有插件存储库。

```
bluemix plugin repos
```

<strong>先决条件</strong>：无


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

将新的插件存储库添加到 {{site.data.keyword.Bluemix_notm}} CLI 中。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>REPO_NAME（必需）</dt>
   <dd>要添加的存储库的名称。可以为每个存储库定义您自己的名称。</dd>
   <dt>REPO_URL（必需）</dt>
   <dd>要添加的存储库的 URL。存储库 URL 必须包含协议（例如，http://plugins.ng.bluemix.net，而不是 plugins.ng.bluemix.net）。http://plugins.ng.bluemix.net 是 Bluemix CLI 的官方插件存储库。</dd>
    </dl>


<strong>示例</strong>：

将 Bluemix CLI 的官方插件存储库添加为 `bluemix-repo`：

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

从 {{site.data.keyword.Bluemix_notm}} CLI 中除去插件存储库。

```
bluemix plugin repo-remove REPO_NAME
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：
   <dl>
   <dt>REPO_NAME（必需）</dt>
   <dd>要除去的存储库的名称。</dd>
   </dl>

<strong>示例</strong>：

从 {{site.data.keyword.Bluemix_notm}} CLI 中除去 `bluemix-repo` 存储库：

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

列出所有添加的存储库或特定存储库中的所有可用插件。

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>-r <i>REPO_NAME</i>（可选）</dt>
   <dd>仅列出指定存储库中的插件。</dd>
   </dl>

<strong>示例</strong>：

列出所有添加的存储库中的所有插件：

```
bluemix plugin repo-plugins
```

列出 `bluemix-repo` 存储库中的所有插件：

```
bluemix plugin repo-plugins -r bluemix-repo
```


## bluemix plugin list
{: #bluemix_plugin_list}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中的所有已安装插件。

```
bluemix plugin list
```

<strong>先决条件</strong>：无


## bluemix plugin install
{: #bluemix_plugin_install}

从指定的路径或存储库将特定版本的插件安装到 {{site.data.keyword.Bluemix_notm}} CLI 中。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME（必需）</dt>
   <dd>如果未指定 -r <i>REPO_NAME</i>，那么将从指定的本地路径或远程 URL 安装插件。</dd>
   <dt>-r <i>REPO_NAME</i>（可选）</dt>
   <dd>插件二进制文件所在的存储库的名称。</dd>
   <dt>-v <i>VERSION</i>（可选）</dt>
   <dd>要安装的插件的版本。如果未提供，将安装插件的最新版本。此选项仅对从存储库安装插件有效。</dd>
    </dl>

<strong>示例</strong>：

从本地文件安装插件：

```
bluemix plugin install /downloads/new_plugin
```

从远程 URL 安装插件：

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

从 `bluemix-repo` 存储库安装最新版本的 `IBM-Containers` 插件：

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
从 `bluemix-repo` 存储库安装版本为 `0.5.800` 的 `IBM-Containers` 插件：

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```

## bluemix plugin update
{: #bluemix_plugin_update}

升级存储库中的插件

```
bluemix plugin update -r REPO_NAME [PLUGIN NAME [-v VERSION]]
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：
<dl>
 <dt>-r REPO_NAME（必需）</dt>
 <dd>插件二进制文件所在的存储库的名称。</dd>
 <dt><i>PLUGIN_NAME</i>（可选）</dt>
 <dd>如果未指定，将列出给定存储库中可供更新的所有插件以供选择。</dd>
 <dt>-v <i>VERSION</i>（可选）</dt>
 <dd>要更新到的插件版本。如果未提供，那么将插件更新到最新可用版本。</dd>
</dl>

<strong>示例</strong>：

检查插件存储库“My-Repo”中所有可用的升级：

```
bluemix plugin update -r My-Repo
```

将存储库“My-Repo”中的插件“plugin-echo”升级到最新版本：

```
bluemix plugin update -r My-Repo plugin-echo
```

将存储库“My-Repo”中的插件“plugin-echo”升级到版本“1.0.1”：

```
bluemix plugin update -r My-Repo plugin-echo -v 1.0.1
```

## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

从 {{site.data.keyword.Bluemix_notm}} CLI 中卸载指定的插件。

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：

   <dl>
   <dt>PLUGIN_NAME（必需）</dt>
   <dd>要卸载的插件的名称。</dd>
    </dl>

<strong>示例</strong>：

卸载先前安装的 `IBM-Containers` 插件：

```
bluemix plugin uninstall IBM-Containers
```
