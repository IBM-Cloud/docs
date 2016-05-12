---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} (bx) 命令
{: #bluemix_cli}

*上次更新时间：2016 年 4 月 15 日*

{{site.data.keyword.Bluemix_notm}} 命令行界面 (CLI) 提供了一组按名称空间分组的命令，供用户用于与 {{site.data.keyword.Bluemix_notm}} 进行交互。一些 {{site.data.keyword.Bluemix_notm}} 命令是现有 cf 命令的包装程序，而另一些为 {{site.data.keyword.Bluemix_notm}} 用户提供了扩展功能。以下信息列出了 {{site.data.keyword.Bluemix_notm}} CLI 支持的所有命令，并包含命令名称、选项、用法、先决条件、描述和示例。
{:shortdesc}
 
**注：***先决条件*列出使用命令前必须执行的操作。没有任何先决条件操作的命令会列出**无**。否则，先决条件可能会包含以下一个或多个操作：
<dl>
<dt>端点</dt>
<dd>使用命令前，必须通过 <code>bluemix api</code> 设置 API 端点。</dd>
<dt>登录</dt>
<dd>使用命令前，必须通过 <code>bluemix login</code> 命令登录。</dd>
<dt>目标</dt>
<dd>使用命令前，必须通过 <code>bluemix target</code> 命令设置组织和空间。</dd>
<dt>Docker</dt>
<dd>必须安装 Docker CLI (docker) 才能运行此命令。</dd>
</dl>

您可以使用以下 {{site.data.keyword.Bluemix_notm}} 命令：

 <table role="presentation"> 
 <tbody> 
 <tr> 
 <td>[bluemix help](index.html#bluemix_help)</td> 
 <td>[bluemix api](index.html#bluemix_api)</td> 
 <td>[bluemix login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr> 
 <tr> 
 <td> 
 [bluemix info](index.html#bluemix_info) </td> 
 <td>[bluemix config](index.html#bluemix_config)</td> 
 <td>[bluemix list](index.html#bluemix_list)</td>
 <td>[bluemix scale](index.html#bluemix_scale)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs) </td> 
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td> 
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete) </td> 
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td> 
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete) </td> 
 <td>[bluemix iam account-users](index.html#bluemix_iam_account-users)</td> 
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account-user-invite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset) </td> 
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td> 
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app list](index.html#bluemix_app_list) </td> 
 <td>[bluemix app show](index.html#bluemix_app_show)</td> 
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app start](index.html#bluemix_app_start) </td> 
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td> 
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app events](index.html#bluemix_app_events) </td> 
 <td>[bluemix app files](index.html#bluemix_app_files)</td> 
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset) </td> 
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td> 
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 </tr>
 
 <tr> 
 <td>[bluemix service list](index.html#bluemix_service_list) </td> 
 <td>[bluemix service show](index.html#bluemix_service_show)</td> 
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service rename](index.html#bluemix_service_rename) </td> 
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td> 
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service keys](index.html#bluemix_service_keys) </td> 
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td> 
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix catalog template](index.html#bluemix_catalog_template) </td> 
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td> 
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td> 
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td> 
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td> 
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td> 
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td> 
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td> 
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td> 
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td> 
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td> 
 <td>[bluemix ic init](index.html#bluemix_ic_init)</td> 
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic create](index.html#bluemix_ic_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td> 
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td> 
 <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td> 
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td> 
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
 <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic info](index.html#bluemix_ic_info)</td> 
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td> 
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td> 
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td> 
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic unpause](index.html#unpause)</td> 
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td> 
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td> 
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td> 
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic stop](index.html#ic_stop)</td> 
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td> 
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td> 
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td> 
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td> 
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td> 
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td> 
 </tr>
 
 <tr>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td> 
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
 </tr>
 
 
 </tbody> 
 </table> 

  

## bluemix help
{: #bluemix_help}
显示 {{site.data.keyword.Bluemix_notm}} CLI 第一级内置命令和受支持名称空间的一般帮助，或者显示特定内置命令或名称空间的帮助。

```
bluemix help [COMMAND|NAMESPACE]
```

**先决条件**：无

**命令选项**：

*命令*|*NAMESPACE*（可选）：显示其帮助信息的命令或名称空间。如果未指定，将显示 {{site.data.keyword.Bluemix_notm}} CLI 的一般帮助。

**示例**：

显示 {{site.data.keyword.Bluemix_notm}} CLI 的一般帮助：

```
bluemix help
```

显示 `info` 命令的帮助信息：

```
bluemix help info
```

显示 `ic` 名称空间的帮助：

```
bluemix help ic
```

或 

```
bluemix ic help
```

显示 `ic` 名称空间下 `group-create` 命令的帮助信息：

```
bluemix ic help group-create
```


## bluemix api
{: #bluemix_api}
设置或查看 {{site.data.keyword.Bluemix_notm}} API 端点。此命令会对 `cf api` 命令打包。

```
bluemix api [API_ENDPOINT][--unset]
```

**先决条件**：无

**命令选项**：

*API_ENDPOINT*（可选）：作为目标的 API 端点，例如 https://api.ng.bluemix.net。 如果未指定 *API_ENDPOINT* 和 `--unset` 选项，将显示当前 API 端点。

`--unset`（可选）：除去 API 端点设置。

**示例**：

将 API 端点设置为 api.ng.bluemix.net：

```
bluemix api api.ng.bluemix.net
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

用户登录。此命令会对 `cf login` 命令打包。命令选项与 `cf login` 命令选项相同。

```
bluemix login [OPTIONS...]
```

**先决条件**：端点

**命令选项**：
有关 `login` 命令支持的选项的信息，请参阅 `cf login` 命令用法信息，以了解用于管理应用程序的 cf 命令。


## bluemix logout
{: #bluemix_logout}

注销用户。此命令会对 `cf logout` 命令打包。

```
bluemix logout
```

**先决条件**：无


## bluemix target
{: #bluemix_target}


设置或查看目标组织或空间。此命令会对 `cf target` 命令打包。

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**先决条件**：端点和登录

**命令选项**：

-o *ORG_NAME*（可选）：要作为目标的组织的名称。

-s *SPACE_NAME*（可选）：要作为目标的空间的名称。

如果 -o *ORG_NAME* 或 -s *SPACE_NAME* 均未指定，那么将显示当前组织和空间。

**示例**：

将当前组织设置为 `MyOrg`，将空间设置为 `MySpace`：

```
bluemix target -o MyOrg -s MySpace
```

查看当前组织和空间：

```
bluemix target
```


## bluemix info
{: #bluemix_info}

查看基本 {{site.data.keyword.Bluemix_notm}} 信息，包括当前区域、云控制器版本以及一些有用的端点，例如用于登录和交换访问令牌的端点。

```
bluemix info
```

**先决条件**：端点


## bluemix config
{: #bluemix_config}


将缺省值写入配置文件。

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**先决条件**：无

**命令选项**：

--http-timeout *TIMEOUT_IN_SECONDS*：HTTP 请求的超时值。缺省值为 60 秒。

--trace true|false|*path/to/file*：跟踪对终端或指定文件的 HTTP 请求。

--color true|false：启用或禁用颜色输出。缺省情况下，会启用颜色输出。

--locale *LOCALE*：设置缺省语言环境。如果 LOCALE 为 *CLEAR*，那么将删除先前的语言环境。

一次只能指定其中一个选项。

**示例**：

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


## bluemix list
{: #bluemix_list}

列出当前空间中的所有应用程序、容器、容器组和 VM 组。

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**先决条件**：端点、登录和目标

**命令选项**：

apps（可选）：仅显示应用程序信息。

containers（可选）：仅显示容器信息。

container-groups（可选）：仅显示容器组信息。

vm-groups（可选）：仅显示 VM 组信息。

一次只能指定“apps”、“containers”、“container-groups”或“vm-groups”中的一项。如果未指定其中任何选项，那么将列出所有 cf 应用程序、容器、容器组和 VM 组。

**示例**：

列出所有 cf 应用程序：

```
bluemix list apps
```

列出所有容器实例：

```
bluemix list containers
```

列出所有应用程序、容器、容器组和 VM 组：

```
bluemix list
```


## bluemix scale
{: #bluemix_scale}

将 cf 应用程序或容器组向内扩展或向外扩展到指定的实例计数、磁盘配额和内存大小。

**注：**扩展容器组时，只能指定实例数。如果未指定任何选项，此命令将列出容器组的当前实例计数，以及 cf 应用程序的磁盘配额和内存大小。

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT][-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**先决条件**：端点、登录和目标

**命令选项**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必需）：要扩展的 cf 应用程序或容器组的名称。

-i *INSTANCE_COUNT*（可选）：要扩展的 cf 应用程序或容器组的新实例数。对于要扩展的容器组，此选项是唯一有效的选项。

-k *DISK_QUOTA*（可选）：cf 应用程序的新磁盘配额。对于扩展容器组无效。

-m *MEMORY_SIZE*（可选）：cf 应用程序的新内存大小。对于扩展容器组无效。

**示例**：

显示 `my-container-group` 的当前实例数：

```
bluemix scale my-container-group
```

将 `my-container-group` 扩展到 2 个实例：

```
bluemix scale my-container-group -i 2
```

将 `my-java-app` 扩展到 3 个实例、8G 磁盘配额和 1024M 内存大小：

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
{: #bluemix_curl}

执行针对 {{site.data.keyword.Bluemix_notm}} 的原始 HTTP 请求。缺省情况下，*Content-Type* 设置为 *application/json*。此命令会向 {{site.data.keyword.Bluemix_notm}} 多云控制代理发送请求。有关受支持的路径，请参阅 [Cloud Foundry API 文档](http://apidocs.cloudfoundry.org/){: new_window}中的 API 路径定义。

```
bluemix curl PATH [OPTIONS...]
```

**先决条件**：端点和登录

**命令选项**：

*PATH*（必需）：资源的 URL 路径。例如，/v2/apps。

*OPTIONS*（可选）：`bluemix curl` 命令支持的选项与 `cf curl` 命令支持的那些选项相同。

**示例**：

查看当前帐户的所有组织的信息：

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

列出所有组织

```
bluemix iam orgs [-r REGION --guid]
```

**先决条件**：端点和登录

**命令选项**：

*-r REGION*（可选）：显示其组织信息的区域。如果设置为“all”，将列出所有区域中的所有组织。

*--guid*（可选）：显示组织的 GUID。

**示例**：列出区域 `us-south` 中的所有组织并显示 GUID

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

显示指定组织的信息。

```
bluemix iam org ORG_NAME [--guid]
```

**先决条件**：端点和登录

**命令选项**：

*ORG_NAME*（必需）：组织的名称。

*--guid*（可选）：显示组织的 GUID。


**示例**：显示组织 `IBM` 的信息并显示 GUID

```
bluemix iam org IBM --guid
```

## bluemix iam org-create
{: #bluemix_iam_org_create}

创建新组织。此操作只能由帐户所有者执行。

```
bluemix iam org-create ORG_NAME
```

**先决条件**：端点和登录

**命令选项**：

*ORG_NAME*（必需）：要创建的组织的名称。

**示例**：创建名为 `IBM` 的组织。

```
bluemix iam org-create IBM
```


## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

将组织从当前区域复制到其他区域。

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**先决条件**：端点和登录

**命令选项**：

*ORG_NAME*（必需）：要复制的现有组织的名称。

*REGION_NAME*（必需）：托管所复制组织的区域的名称。

**示例**：

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

**先决条件**：端点和登录

**命令选项**：

*OLD_ORG_NAME*（必需）：要重命名的组织的旧名称。

*NEW_ORG_NAME*（必需）：组织要重命名为的新名称。


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

删除当前区域中的指定组织。

```
bluemix iam org-delete ORG_NAME [-f --all]
```

**先决条件**：端点和登录

**命令选项**：

*ORG_NAME*（必需）：要删除的现有组织的名称。

*-f*（可选）：强制删除，而不进行确认。

*--all*（可选）：从所有区域中删除该组织。


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


## bluemix iam account-users
{: #bluemix_iam_account_users}

显示与帐户关联的用户。此操作只能由帐户所有者执行。

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


邀请用户加入已设置组织和空间角色的帐户。此操作只能由帐户所有者执行。

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

**先决条件**：端点和登录


**命令选项**：

*USER_NAME*（必需）：要邀请的用户的名称。

*ORG_NAME*（必需）：要邀请此用户加入的组织的名称。

*ORG_ROLE*（必需）：要邀请此用户加入的组织角色的名称。例如：

<dl>
<dt>OrgManager</dt>
<dd>此角色可以邀请和管理用户，选择并更改套餐，以及设置花费限制。</dd>
<dt>BillingManager</dt>
<dd>此角色可以创建和管理缴费账户和付款信息。</dd>
<dt>OrgAuditor</dt>
<dd>此角色具有对组织信息和报告的只读访问权。</dd>
</dl> 

*SPACE_NAME*（必需）：要邀请此用户加入的空间的名称。

*SPACE_ROLE*（必需）：要邀请此用户加入的空间角色的名称。例如：

<dl>
<dt>SpaceManager</dt>
<dd>此角色可以邀请和管理用户，以及启用给定空间的功能。</dd>
<dt>SpaceDeveloper</dt>
<dd>此角色可以创建和管理应用程序与服务，以及查看日志和报告。</dd>
<dt>SpaceAuditor</dt>
<dd>此角色可以查看空间的日志、报告和设置。</dd>
</dl> 

**示例**：

邀请用户 `Mary` 以 `OrgManager` 角色加入组织 `IBM`，并以 `SpaceAuditor` 角色加入空间 `Cloud`：

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

按角色显示指定组织中的用户。

```
bluemix iam org-users ORG_NAME [-a]
```

**先决条件**：端点和登录

**命令选项**：

*ORG_NAME*（必需）：组织的名称。

*-a*（可选）：列出指定组织中的所有用户，但不按角色分组。


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

向用户分配组织角色。此操作只能由组织管理员执行。

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

**先决条件**：端点和登录

**命令选项**：

*USER_NAME*（必需）：要向其分配角色的用户的名称。

*ORG_NAME*（必需）：要将此用户分配到的组织的名称。

*ORG_ROLE*（必需）：要向此用户分配的组织角色的名称。例如：

<dl>
<dt>OrgManager</dt>
<dd>此角色可以邀请和管理用户，选择并更改套餐，以及设置花费限制。</dd>
<dt>BillingManager</dt>
<dd>此角色可以创建和管理缴费账户和付款信息。</dd>
<dt>OrgAuditor</dt>
<dd>此角色具有对组织信息和报告的只读访问权。</dd>
</dl> 

**示例**：

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

**先决条件**：端点和登录

**命令选项**：

*USER_NAME*（必需）：要除去的用户的名称。

*ORG_NAME*（必需）：要从中除去此用户的组织的名称。

*ORG_ROLE*（必需）：要从中除去此用户的组织角色的名称。例如：

<dl>
<dt>OrgManager</dt>
<dd>此角色可以邀请和管理用户，选择并更改套餐，以及设置花费限制。</dd>
<dt>BillingManager</dt>
<dd>此角色可以创建和管理缴费账户和付款信息。</dd>
<dt>OrgAuditor</dt>
<dd>此角色具有对组织信息和报告的只读访问权。</dd>
</dl> 

**示例**：

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

**先决条件**：端点和登录

**命令选项**：

*ORG_NAME*（必需）：组织的名称。

*SPACE_NAME*（必需）：空间的名称。


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

向用户分配空间角色。此操作只能由空间管理员执行。

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**先决条件**：端点和登录

**命令选项**：

*USER_NAME*（必需）：要向其分配角色的用户的名称。

*ORG_NAME*（必需）：要将此用户分配到的组织的名称。

*SPACE_NAME*（必需）：要将此用户分配到的空间的名称。

*SPACE_ROLE*（必需）：要向此用户分配的空间角色的名称。例如：

<dl>
<dt>SpaceManager</dt>
<dd>此角色可以邀请和管理用户，以及启用给定空间的功能。</dd>
<dt>SpaceDeveloper</dt>
<dd>此角色可以创建和管理应用程序与服务，以及查看日志和报告。</dd>
<dt>SpaceAuditor</dt>
<dd>此角色可以查看空间的日志、报告和设置。</dd>
</dl> 


**示例**：

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

**先决条件**：端点和登录

**命令选项**：

*USER_NAME*（必需）：要除去的用户的名称。

*ORG_NAME*（必需）：要从中除去此用户的组织的名称。

*SPACE_NAME*（必需）：要从中除去此用户的空间的名称。

*SPACE_ROLE*（必需）：要从中除去此用户的空间角色的名称。例如：

<dl>
<dt>SpaceManager</dt>
<dd>此角色可以邀请和管理用户，以及启用给定空间的功能。</dd>
<dt>SpaceDeveloper</dt>
<dd>此角色可以创建和管理应用程序与服务，以及查看日志和报告。</dd>
<dt>SpaceAuditor</dt>
<dd>此角色可以查看空间的日志、报告和设置。</dd>
</dl> 

**示例**：

从组织 `IBM` 和空间 `Cloud` 中除去用户 `Mary` 的 `SpaceManager` 角色：

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

此命令的功能和选项与 `cf push` 命令的相同。


## bluemix app list
{: #bluemix_app_list}

此命令的功能和选项与 `cf apps` 命令的相同。


## bluemix app show
{: #bluemix_app_show}

此命令的功能和选项与 `cf app` 命令的相同。


## bluemix app scale
{: #bluemix_app_scale}

此命令的功能和选项与 `cf scale` 命令的相同。


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


## bluemix app stack
{: #bluemix_app_stack}

此命令的功能和选项与 `cf stack` 命令的相同。


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

此命令的功能和选项与 `cf create-app-manifest` 命令的相同。


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

**先决条件**：端点和登录

**命令选项**：

-d（可选）：如果指定了 `-d` 选项，那么还会显示每个模板的描述。否则，只显示每个模板的标识和名称。


## bluemix catalog template
{: #bluemix_catalog_template}

查看指定样板模板的详细信息。

```
bluemix catalog template TEMPLATE_ID
```

**先决条件**：端点和登录

**命令选项**：

*TEMPLATE_ID*（必需）：样板模板的标识。使用“bluemix templates”可查看所有模板的标识。

**示例**：

查看模板 `mobileBackendStarter` 的详细信息：

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

使用指定 URL 和描述基于指定模板创建 cf 应用程序。缺省情况下，新应用程序将自动启动。

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**先决条件**：端点、登录和目标

**命令选项**：

*TEMPLATE_ID*（必需）：创建应用程序时所基于的模板。使用 `bluemix templates` 可查看所有模板的标识。

*CF_APP_NAME*（必需）：要创建的 cf 应用程序的名称。

-u *URL*（可选）：应用程序的路径。如果未指定，路径将由 {{site.data.keyword.Bluemix_notm}} 根据您的应用程序名称和缺省域自动设置。

-d *DESCRIPTION*（可选）：应用程序的描述。

--no-start（可选）：应用程序创建后不自动启动。如果未指定，应用程序创建后将自动启动。

**示例**：

基于 `javaHelloWorld` 模板创建 cf 应用程序 `my-app`：

```
bluemix catalog template-run javaHelloWorld my-app
```

基于 `rubyHelloWorld` 模板创建应用程序 `my-ruby-app`，路径为 `myrubyapp.ng.bluemix.net`，描述为 `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`：

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

基于 `pythonHelloWorld` 模板创建应用程序 `my-python-app`，不带自动启动：

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
{: #bluemix_network_regions}

查看 {{site.data.keyword.Bluemix_notm}} 上所有区域的信息。

```
bluemix network regions
```

**先决条件**：端点


## bluemix network region-set
{: #bluemix_network_region_set}

切换到指定的区域。此命令会自动重定向到新区域中的相同组织和空间（如果可能）。如果用户已登录，该命令会提示用户选择新的组织和空间。API 端点会相应地更改。

```
bluemix network region-set REGION_NAME
```

**先决条件**：端点

**命令选项**：

*REGION_NAME*（必需）：要切换到的区域的名称。可以使用 `bluemix network regions` 命令来查看所有区域名称。

**示例**：

将当前区域设置为 `eu-gb`：

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

此命令的功能和选项与 `cf routes` 命令的相同。


## bluemix network route-check
{: #bluemix_network_route_check}

此命令的功能和选项与 `cf check-route` 命令的相同。


## bluemix network route-map
{: #bluemix_network_route_map}

将路径映射到具有指定域和主机名的现有 cf 应用程序或容器组。

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**先决条件**：端点、登录和目标

**命令选项**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必需）：要与路径进行映射的 cf 应用程序或容器组的名称。

*DOMAIN*（必需）：路径的域。例如，mybluemix.net 或 ng.bluemix.net。 

-n *HOST_NAME*（可选）：路径的主机名。如果未提供，缺省情况下主机名将设置为应用程序名称或容器组名称。

**示例**：

使用指定的域将路径映射到 `my-app`：

```
bluemix network route-map my-app mybluemix.net
```

使用指定域和主机名将路径映射到“my-container-group”：

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
{: #bluemix_network_route_unmap}

取消来自现有 cf 应用程序或容器组中的指定路径映射。

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**先决条件**：端点、登录和目标

**命令选项**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必需）：cf 应用程序或容器组的名称。

*DOMAIN*（必需）：路径的域（例如，mybluemix.net 或 ng.bluemix.net）。 

-n *HOST_NAME*（可选）：路径的主机名。如果未提供，缺省情况下主机名将设置为应用程序名称或容器组名称。

**示例**：

从 `my-app` 取消 `my-app.mybluemix.net` 的映射：

```
bluemix network route-unmap my-app mybluemix.net
```

从 `my-container-group` 取消 `abc.ng.bluexmix.net` 的映射：

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
{: #bluemix_network_route_create}

此命令的功能和选项与 `cf create-route` 命令的相同。


## bluemix network route-delete
{: #bluemix_network_route_delete}

此命令的功能和选项与 `cf delete-route` 命令的相同。


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

此命令的功能和选项与 `cf delete-orphaned-routes` 命令的相同。


## bluemix network domains
{: #bluemix_network_domains}

此命令的功能和选项与 `cf domains` 命令的相同。


## bluemix network domain-create
{: #bluemix_network_domain_create}

此命令的功能和选项与 `cf create-domain` 命令的相同。


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

此命令的功能和选项与 `cf delete-domain` 命令的相同。


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

此命令的功能和选项与 `cf create-shared-domain` 命令的相同。


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

此命令的功能和选项与 `cf delete-shared-domain` 命令的相同。


## bluemix security cert
{: #bluemix_security_cert}

列出域的证书信息。

```
bluemix security cert DOMAIN_NAME
```

**先决条件**：端点和登录

**命令选项**：

*DOMAIN_NAME*（必需）：托管证书的域。

**示例**：

查看域 `ibmcxo-eventconnect.com` 的证书信息：

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

将证书添加到当前组织中的指定域。

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**先决条件**：端点、登录和目标

**命令选项**：

*DOMAIN*（必需）：将证书添加到其中的域。

-k *PRIVATE_KEY_FILE*（必需）：专用密钥文件路径。

-c *CERT_FILE*（必需）：证书文件路径。

-p *PASSWORD*（可选）：证书的密码。

-i *INTERMEDIATE_CERT_FILE*（可选）：中间证书文件路径。

--verify-client（可选）：是否启用客户机证书验证。

**示例**：

将证书添加到域 `ibmcxo-eventconnect.com`：

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
{: #bluemix_security_cert_remove}

从当前组织中的指定域除去证书。

```
bluemix security cert-remove DOMAIN [-f]
```

**先决条件**：端点、登录和目标

**命令选项**：

*DOMAIN*（必需）：要从中除去证书的域。

-f（可选）：强制删除，而不进行确认。







## bluemix plugin repos
{: #bluemix_plugin_repos}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中注册的所有插件存储库。

```
bluemix plugin repos
```

**先决条件**：无


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

将新的插件存储库添加到 {{site.data.keyword.Bluemix_notm}} CLI 中。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**先决条件**：无

**命令选项**：

*REPO_NAME*（必需）：要添加的存储库的名称。可以为每个存储库定义您自己的名称。

*REPO_URL*（必需）：要添加的存储库的 URL。存储库 URL 必须包含协议（例如，http://plugins.ng.bluemix.net，而不是 plugins.ng.bluemix.net）。http://plugins.ng.bluemix.net 是 {{site.data.keyword.Bluemix_notm}} CLI 的官方插件存储库。

**示例**：

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

**先决条件**：无

**命令选项**：

*REPO_NAME*（必需）：要除去的存储库的名称。

**示例**：

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

**先决条件**：无

**命令选项**：

-r *REPO_NAME*（可选）：仅列出指定存储库中的插件。

**示例**：

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

**先决条件**：无


## bluemix plugin install
{: #bluemix_plugin_install}

从指定的路径或存储库将特定版本的插件安装到 {{site.data.keyword.Bluemix_notm}} CLI 中。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**先决条件**：无

**命令选项**：

*PLUGIN_PATH*|*PLUGIN_NAME*（必需）：如果未指定 `-r *REPO_NAME*`，那么将从指定的本地路径或远程 URL 安装插件。

-r *REPO_NAME*（可选）：插件二进制文件所在的存储库的名称。
-v *VERSION*（可选）：要安装的插件的版本。如果未提供，将安装插件的最新版本。此选项仅对从存储库安装插件有效。

**示例**：

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






## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

从 {{site.data.keyword.Bluemix_notm}} CLI 中卸载指定的插件。

```
bluemix plugin uninstall PLUGIN_NAME
```

**先决条件**：无

**命令选项**：

*PLUGIN_NAME*（必需）：要卸载的插件的名称。

**示例**：

卸载先前安装的 `IBM-Containers` 插件：

```
bluemix plugin uninstall IBM-Containers
```


## bluemix ic init
{: #bluemix_ic_init}

初始化本地计算机上的容器环境，以使用 IBM Containers 服务的完整功能。

```
bluemix ic init
```

**先决条件**：端点、登录和目标

**注：**初始化之前，请确保 Docker CLI (docker) 已安装并在 PATH 环境变量中配置。要切换到其他区域，请使用 `bluemix region-set` 命令。 

**示例**：

切换到 `us-south` 区域：

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

控制正在运行的容器或查看其输出。使用 `CTRL+C` 以退出并停止容器。此命令将调用 Docker CLI。有关更多信息，请参阅 Docker 帮助中的 [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} 命令。 

```
bluemix ic attach [--no-stdin][--sig-proxy] CONTAINER
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

--no-stdin（可选）：不包含标准输入。

--sig-proxy（可选）：将所有接收到的信号通过代理传递到进程。缺省值为 **true**。

*CONTAINER*（必需）：容器名称或标识。

**示例**：

以下示例显示用于连接到容器 `my_container` 的请求：
```
bluemix ic attach my_container
```


## bluemix ic build
{: #bluemix_ic_build}

调用 IBM Containers 构建服务，用于在本地或在专用 {{site.data.keyword.Bluemix_notm}} 存储库中构建 Docker 映像。此命令将调用 Docker CLI。有关更多信息，请参阅 Docker 帮助中的 [build](https://docs.docker.com/reference/commandline/build/){: new_window} 命令。 

```
bluemix ic build -t TAG|--tag TAG [--no-cache][-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

-t *TAG*|--tag *TAG*（必需）：要应用到所创建映像的存储库名称。

--no-cache（可选）：在构建映像时不使用高速缓存。缺省值为 **false**。

-p|--pull（可选）：尝试从注册表拉取基本映像（即使它已高速缓存）。

-q|--quiet（可选）：禁止显示容器生成的详细输出。缺省值为 **false**。

*DOCKERFILE_LOCATION*（必需）：本地主机上 Dockerfile 和上下文的路径。

**示例**：

以下示例显示用于构建名为 *myimage* 的映像的请求。要在该构建中使用的 Dockerfile 和其他工件位于运行该命令的目录中。由于映像名称随附了注册表和名称空间，因此会在组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中构建映像。
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic create
{: #bluemix_ic_create}

在 {{site.data.keyword.Bluemix_notm}} 存储库中创建新容器。此命令会对 `docker create` 命令打包。有关更多信息，请参阅 Docker 帮助中的 [create](https://docs.docker.com/reference/commandline/create/){: new_window} 命令。


## bluemix ic cpi
{: #bluemix_ic_cpi}

访问 Docker Hub 映像或本地注册表中的映像，然后将该映像复制到专用 {{site.data.keyword.Bluemix_notm}} 存储库。

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

**先决条件**：端点、登录和目标

**命令选项**：

*SOURCE_IMAGE*（必需）：源存储库和映像名称。

*DESTINATION_IMAGE*（必需）：专用 {{site.data.keyword.Bluemix_notm}} 存储库 URL，其中包含名称空间和目标映像名称。映像的标记是可选的。

**示例**：

将映像从源存储库复制到专用存储库，然后为该映像添加标记：

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

将 `sinatra` 映像从 `training` 存储库复制到专用存储库 `registry.ng.bluemix.net/mynamespace`，然后将该映像命名为 `mysinatra`。为映像 `mysinatra` 添加标记 `v1`。 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


在容器内执行命令。有关更多信息，请参阅 Docker 帮助中的 [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} 命令。

```
bluemix ic exec [-d|--detach][-it] [-u USER|--user USER] CONTAINER [CMD]
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

-d|--detach（可选）：在后台运行指定的命令。

-it（可选）：交互方式。使标准输入保持显示。输入“exit”以退出。

-u *USER*|--user *USER*（可选）：用户名。

*CONTAINER*（必需）：容器名称或标识。

*CMD*（可选）：要在指定的一个或多个容器内执行的命令。

**示例**：

以交互方式在 `my_container` 容器内执行 `bash` 命令：

```
bluemix ic exec -it my_container bash
```

在 `my_container` 容器内执行 `date` 命令：

```
bluemix ic exec my_container date
```


## bluemix ic groups
{: #bluemix_ic_groups}

列出组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中的容器组。

```
bluemix ic groups
```

**先决条件**：端点、登录和目标


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

查看在创建容器组时为其指定的详细信息，例如环境变量、端口或内存。

```
bluemix ic group-inspect CONTAINER_GROUP
```

**先决条件**：端点、登录和目标

**命令选项**：

*CONTAINER_GROUP*（必需）：容器组标识或名称。

**示例**：

以下示例显示用于检查容器组 `my_group` 的请求：
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

列出指定容器组的实例。

```
bluemix ic group-instances CONTAINER_GROUP
```

**先决条件**：端点、登录和目标

**命令选项**：

*CONTAINER_GROUP*（必需）：容器组标识或名称。

**示例**：

列出容器组 `my_group` 中的所有实例：
```
bluemix ic group-instances my_group
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

创建可扩展容器组。

```
bluemix ic group-create [-p PORT|--publish port][-m MEMORY|--memory MEMORY] [-e ENV|--env ENV][-v VOLUME:CONTAINER_PATH] [--min MIN][--max MAX] [--desired DESIRED][--auto] [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] [--name NAME] IMAGE [CMD]
```

**先决条件**：端点、登录和目标

**命令选项**：

-m *MEMORY*|--memory *MEMORY*（可选）：为组分配内存限制 (MB)。在 CLI 中创建容器组时，每个容器实例的缺省值为 `64` MB。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中创建容器组时，每个容器实例的缺省值为 `256` MB。接受的值为 `64`、`256`、`512`、`1024` 和 `2048`。分配内存限制后，此值无法更改。

-e *ENV*|--env *ENV*（可选）：设置环境变量，其中 **ENV** 为“key=value”对。单独列出多个键。如果包含引号，请用引号将环境变量名称和值括起。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。下表显示了可以指定的一些常用环境变量：

|  环境变量                              |     描述                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 将服务绑定到容器。使用“CCS_BIND_APP”环境变量将应用程序绑定到容器。应用程序绑定到目标服务并用作网桥，以允许 {{site.data.keyword.Bluemix_notm}} 将网桥应用程序的 `VCAP_SERVICES` 信息放入正在运行的容器实例。有关创建网桥应用程序的更多信息，请参阅[将服务绑定到容器](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}。 |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | 创建容器时，向容器添加 SSH 密钥。在 {{site.data.keyword.Bluemix_notm}}“仪表板”或 CLI 中创建容器时，可以使用此环境变量来添加 SSH 密钥。有关 SSH 密钥的更多信息，请参阅[登录到容器](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 添加要在容器中监视的日志文件。请包含 `LOG_LOCATIONS` 环境变量以及日志文件的路径。 |
*表 1. 常用环境变量*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  （可选）：通过使用格式“VolumeId:ContainerPath[:ro]”指定详细信息来将卷连接到容器。

- *VOLUME*：卷标识或卷名。
- *CONTAINER_PATH*：容器中卷的绝对路径。
- ro：可选。指定“ro”会将卷设为只读，而不是缺省的读/写。

-p *PORT*|--publish *PORT*（可选）：公开用于 HTTP 流量的端口。组中的容器必须侦听该 HTTP 端口。无法发出 HTTPS 请求。对于容器组，不能包含多个端口。

指定端口时，您使应用程序可用于相同 {{site.data.keyword.Bluemix_notm}} 空间中正尝试联系主机的 {{site.data.keyword.Bluemix_notm}} 负载均衡器或容器。然后，{{site.data.keyword.Bluemix_notm}} 负载均衡器或容器可以使用该端口来访问同一 {{site.data.keyword.Bluemix_notm}} 空间中的主机和应用程序。如果在 Dockerfile 中为要使用的映像指定了端口，请包含该端口。

**提示：**

- 对于 IBM 认证的 Liberty Server 映像或此映像的修改版本，请输入端口 9080。
- 对于 IBM 认证的 Node.js 映像或此映像的修改版本，请输入端口 8000。

--min *MIN*（可选）：最小实例数。缺省值为 **1**。如果设置了最小实例数，那么创建容器组后，无法更改此值。

--max *MAX*（可选）：最大实例数。缺省值为 **2**。如果设置了最大实例数，那么创建容器组后，无法更改此值。

--desired *DESIRED*（可选）：需要的实例数。缺省值为 **2**。

--auto（可选）：创建容器组并启用自动恢复后，IBM Containers 会通过向所分配的端口发送 HTTP 请求来检查每个实例的运行状况。

在接下来的两个 90 秒的时间间隔内，如果没有收到来自某个容器实例的响应，那么会除去该实例并替换为新实例。如果该容器有响应，那么不会执行任何操作。此过程会持续重复。在 30 分钟的时段内，如果容器组中不同容器的总数等于或超过该容器组最大大小的 3 倍，那么会对该容器组永久禁用自动恢复。要重新启用自动恢复，必须重新创建容器组。

-n *HOST*|--hostname *HOST*（可选）：主机名，例如“mycontainerhost”。主机和域组合在一起构成了完整的公共路径 URL，例如“http://mycontainerhost.mybluemix.net”。使用“bluemix ic group-inspect”命令来复查容器组的详细信息时，主机和域会作为路径一起列出。

-d *DOMAIN*|--domain *DOMAIN*（可选）：通常，域为 `.mybluemix.net`。主机和域组合在一起构成了完整的公共路径 URL，例如 `http://mycontainerhost.mybluemix.net`。使用 `bluemix ic group-inspect` 命令来查看容器组的详细信息时，主机和域会作为路径一起列出。

--name *NAME*（必需）：为组分配名称。不推荐使用 `-n`。

**提示：**容器名称必须以字母开头。名称可以包含大写字母、小写字母、数字、句点 `.`、下划线 `_` 或连字符 `-`。

*IMAGE*（必需）：要包含在容器组中的每个容器实例内的映像。可以在映像之后列出命令，但不要在映像之后放置任何选项。请在指定映像之前包含所有选项。

如果在组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中使用映像，请使用以下格式指定映像：`registry.ng.bluemix.net/NAMESPACE/IMAGE`。

如果使用 IBM Containers 提供的映像，请不要包含组织的名称空间。使用以下格式指定映像：`registry.ng.bluemix.net/IMAGE`。

*CMD*（可选）：传递给容器组来执行的命令及相应自变量。此命令必须是长时间运行命令。不要使用不会运行很长时间的短时间运行命令（例如 **/bin/date**），因为短时间运行命令可能会导致容器崩溃。

**注：**
- 命令及其自变量必须位于 `bluemix ic run` 命令行的末尾。
- 如果命令自变量包含连字符 `-`（如先前命令示例中的 `-c` 所示），那么必须在命令前面添加两个连字符 `--`。



**示例**：

使用 IBM Containers 提供的 `registry.ng.bluemix.net/ibmnode` 映像创建容器组 `my_container_group`，然后对该容器组运行长时间运行的命令 `ping localhost`：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

使用 IBM Containers 提供的 `registry.ng.bluemix.net/ibmnode` 映像创建容器组 `my_container_group`，然后对该容器组运行长时间运行的命令 `tail -f /dev/null`：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

使用 `registry.ng.bluemix.net/ibmliberty` 映像创建可扩展组 `mygroup`，并启用自动恢复。端口为 `9080`，主机名为 `mycontainerhost`，域名为 `.mybluemix.net`。
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d .mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

更新容器组。


```
bluemix ic group-update [--min MIN][--max MAX] [--desired DESIRED][--auto] CONTAINER_GROUP
```

**提示：**要更新容器组的主机名或域，请使用 `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`。

**先决条件**：端点、登录和目标

**命令选项**：

--min *MIN*（可选）：最小实例数。缺省值为 **1**。设置了最小实例数后，无法更改此值。

--max *MAX*（可选）：最大实例数。缺省值为 **2**。设置了最大实例数后，无法更改此值。

--desired *DESIRED*（可选）：需要的实例数。缺省值为 **2**。

**提示：**一次只能指定 `--min MIN`、`--max MAX` 或 `--desired DESIRED` 选项中的一个。

--auto（可选）：通过启用自动恢复，自动重新启动发生故障的实例。

*CONTAINER_GROUP*（必需）：容器组标识或名称。

**示例**：

以下示例显示用于更新容器组 `my_group` 的请求：
```
bluemix ic group-update --max 5 my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

从组织专用 {{site.data.keyword.Bluemix_notm}} 存储库中除去容器组。

```
bluemix ic group-remove [-f|--force] CONTAINER_GROUP
```

**先决条件**：端点、登录和目标

**命令选项**：

-f|--force（可选）：强制除去正在运行的或发生故障的容器。

*CONTAINER_GROUP*（必需）：容器组标识或名称。

**示例**：

以下示例显示用于除去容器组的请求，其中 `my_group` 是容器组的名称。
```
bluemix ic group-remove my_group
```


## bluemix ic images
{: #bluemix_ic_images}

查看组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中所有可用映像的列表。有关更多信息，请参阅 Docker 帮助中的 [images](https://docs.docker.com/reference/commandline/images){: new_window} 命令。此列表包含映像标识、创建日期和映像名称。

```
bluemix ic images [-a|--all][--no-trunc] [-q|--quiet]
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

-a|--all（可选）：包含组织的存储库中每个映像的所有映像层，而不仅仅包含最近的层。

--no-trunc（可选）：不截断输出。

-q|--quiet（可选）：仅显示数字标识。

**示例**：

以下示例显示用于接收组织的可用映像列表的请求：
```
bluemix ic images
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

查看有关容器的信息。有关更多信息，请参阅 Docker 帮助中的 [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} 命令。

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

*IMAGE*（必需）：通过指定映像名称或标识来查看有关特定映像的详细信息。

images（必需）：查看有关存储库中所有映像的详细信息。

*CONTAINER*（必需）：通过指定容器名称或标识来查看有关特定容器的详细信息。

**提示：**一次只能指定 *IMAGE*、images 或 *CONTAINER* 中的一个。 

**示例**：

以下示例显示用于检查名为 `proxy` 的容器的请求：
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

查看用于描述容器云服务实例状态的一组信息。该信息包括容器数限制、容器使用情况、正在运行的容器数、内存限制、内存使用情况、浮动 IP 地址限制、浮动 IP 地址使用情况、CCS 主机 URL、注册表主机 URL 和调试方式状态。

```
bluemix ic info
```

**先决条件**：端点、登录和目标


## bluemix ic ips
{: #bluemix_ic_ips}

列出已登录用户的可用浮动 IP 地址。列表包含 IP 地址以及这些 IP 地址链接到的容器标识。如果 IP 地址是未用过的，那么不会显示容器标识。

```
bluemix ic ips [-a|--all]
```

**先决条件**：端点、登录和目标

**命令选项**：

-a|--all（可选）：列出所有 IP 地址。缺省情况下，仅返回可用 IP 地址。

**示例**：

以下示例显示用于接收组织的所有 IP 地址（无论是否可用）的列表的请求。
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
请求新的浮动 IP 地址。

```
bluemix ic ip-request
```

**先决条件**：端点、登录和目标


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

从容器云服务实例释放浮动 IP 地址。

```
bluemix ic ip-release IP_ADDRESS
```

**先决条件**：端点、登录和目标

**命令选项**：

*IP_ADDRESS*（必需）：要释放的 IP 地址。


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

将可用浮动 IP 地址绑定到容器。

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

**先决条件**：端点、登录和目标

**命令选项**：

*IP_ADDRESS*（必需）：要绑定的 IP 地址。

*CONTAINER*（必需）：要绑定的容器标识或名称。

**示例**：

以下示例显示用于将 IP 地址 `192.123.12.12` 绑定到容器 `proxy` 的请求：
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

将浮动 IP 地址从其容器取消绑定。

公共 IP 地址是 IBM Containers 中的有限资源。因此，对于免费试用版用户，如果有分配给空间的公共 IP 地址未绑定到容器，那么会大约每周回收一次这些公共 IP 地址。对于现买现付客户或预订客户，永远都不会回收这些未绑定的公共 IP 地址。

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

**先决条件**：端点、登录和目标

**命令选项**：

*IP_ADDRESS*（必需）：要取消绑定的 IP 地址。

*CONTAINER*（必需）：要取消绑定的容器标识或名称。

**示例**：

以下示例显示用于取消 IP 地址 `192.123.12.12` 与容器 `proxy` 的绑定的请求：
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

停止容器中正在运行的进程而不停止容器。有关更多信息，请参阅 Docker 帮助中的 [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} 命令。

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

-s *CMD*|--signal *CMD*（可选）：向正在容器中运行的进程发送命令。

*CONTAINER*（必需）：容器标识或名称。

**示例**：

以下示例显示用于终止容器 `proxy` 中的进程的请求：
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

查看您登录到的组织的专用 {{site.data.keyword.Bluemix_notm}} 映像存储库的名称。

```
bluemix ic namespace-get
```

**先决条件**：端点、登录和目标


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

设置您登录到的组织的专用 {{site.data.keyword.Bluemix_notm}} 映像存储库的名称。

*限制*：不能在存储库名称空间的名称中使用连字符 `-`。

```
bluemix ic namespace-set NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*NAME* （必需）：仅一次性功能，用于设置组织的存储库名称空间（如果尚未设置）。设置名称空间后，请通过 `bluemix ic init` 命令重新初始化 IBM Containers，然后再继续。


## bluemix ic pause
{: #pause}

暂停正在运行的容器内的所有进程。有关更多信息，请参阅 Docker 帮助中的 [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} 命令。要停止容器，请参阅 [bluemix ic unpause](#unpause) 命令。

```
bluemix ic pause CONTAINER
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

*CONTAINER*（必需）：容器名称或标识。

**响应**：

- 已成功暂停容器。

- 针对容器云服务的命令失败

 `{message}`
  
 其中，`{message}` 是相关错误。
 
- 命令失败 - 无法连接到容器云服务

**示例**：

以下示例显示用于暂停名为 `proxy` 的容器的请求：
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

取消暂停正在运行的容器内的所有进程。有关更多信息，请参阅 Docker 帮助中的 [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} 命令。要暂停容器，请参阅 [bluemix ic pause](#pause) 命令。

```
bluemix ic unpause CONTAINER
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

*CONTAINER*（必需）：容器名称或标识。

**响应**：

- 已成功取消暂停容器。

- 针对容器云服务的命令失败 

 `{message}` 
 
 其中，`{message}` 是相关错误。
 
- 命令失败 - 无法连接到容器云服务

**示例**：

以下示例显示用于取消暂停名为 `proxy` 的容器的请求：
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

列出容器的端口映射或特定映射。此命令会对 `docker port` 命令打包。有关更多信息，请参阅 Docker 帮助中的 [port](https://docs.docker.com/reference/commandline/port/){: new_window} 命令。


## bluemix ic ps
{: #bluemix_ic_ps}
查看正在已登录用户的名称空间中运行的容器的列表。缺省情况下，此命令仅显示正在运行的容器。有关更多信息，请参阅 Docker 帮助中的 [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} 命令。

```
bluemix ic ps [-a|--all][-s|--size] [-l NUM|--limit NUM][-q|--quiet]
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

-a|--all（可选）：显示所有容器（包括正在运行和已停止的容器）。

-s|--size（可选）：列出容器的大小。

-l *NUM*|--limit *NUM*（可选）：列出最新创建的容器，其中 *NUM* 是要返回的最新创建的容器数。

例如，如果已按顺序创建了容器“node1”到“node5”，那么命令“ice ps --limit 2”会返回 node4 和 node5，因为它们是最后创建的两个容器。

-q|--quiet（可选）：仅显示容器标识。

**示例**：

以下示例显示用于查看所有正在运行和已停止的容器的请求：
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

重新启动容器。有关更多信息，请参阅 Docker 帮助中的 [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} 命令。

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

*CONTAINER*（必需）：容器名称或标识。

-t *SECS*|--time *SECS*（可选）：重新启动容器之前要等待的秒数。

**响应**：

- 已成功重新启动容器。

- 针对容器云服务的命令失败 

 `{message}` 
 
 其中，`{message}` 是相关错误。
 
- 命令失败 - 无法连接到容器云服务

**示例**：

以下示例显示用于重新启动名为 `proxy` 的容器的请求：
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

除去容器。有关更多信息，请参阅 Docker 帮助中的 [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} 命令。

```
bluemix ic rm [-f|--force] CONTAINER
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

-f|--force（可选）：强制除去正在运行的或发生故障的容器。

*CONTAINER*（必需）：容器名称或标识。

**响应**：

- 已成功除去容器。

- 针对容器云服务的命令失败 

 `{message}` 
 
 其中，`{message}` 是相关错误。
 
- 命令失败 - 无法连接到容器云服务。

**示例**：

以下示例显示用于除去名为 `proxy` 的容器的请求：
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

从已登录用户的名称空间除去映像。有关更多信息，请参阅 Docker 帮助中的 [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} 命令。

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

-R *REGISTRY*|--registry *REGISTRY*（可选）：更改注册表主机。缺省行为是使用在 `bluemix ic init` 命令中指定的注册表。

*IMAGE*（必需）：要除去的映像的名称。如果未在映像名称中指定标记，那么缺省情况下会删除标记为 `latest` 的映像。

**响应**：

- 已除去：`{IMAGE}`

 其中，`{IMAGE}` 是已除去映像的名称。
 
- 错误！未指定注册表主机。

- 除去映像失败 - 无法连接到容器云注册表

- 针对容器云服务的命令失败 

 `{message}`
 
 其中，`{message}` 是相关错误。

**示例**：

以下示例显示用于除去映像 `mynamespace/myimage:latest` 的请求：
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

通过映像名称在容器云服务中启动新容器。有关更多信息，请参阅 Docker 帮助中的 [run](https://docs.docker.com/reference/commandline/run/){: new_window} 命令。



```
bluemix ic run [-p PORT|--publish PORT][-P] [-m MEMORY|--memory MEMORY][-e ENV|--env ENV] [-v VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS][-it] IMAGE [CMD [CMD ...]]
```
**注：** 确保已安装 Cloud Foundry 命令工具，并且您具有 Cloud Foundry 令牌。使用“bluemix login”成功登录，然后使用“bluemix ic init”生成必需的令牌和证书。 


**先决条件**：端点、登录、目标和 Docker

**命令选项**：

-p *PORT*|--publish *PORT*（可选）：公开用于 HTTP 流量的端口。包含在 Dockerfile 中为要使用的映像指定的任何端口。可以使用多个 `-p` 选项包含多个端口。如果公共 IP 地址可用，那么公开端口会自动将公共 IP 地址绑定到容器。

如果空间中有要绑定到容器的现有 IP 地址，那么可以指定该 IP 地址，而不是以后绑定。IP 地址必须使用以下格式指定：*&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt;*。

有关请求空间的 IP 地址的更多信息，请参阅 [bluemix ic ip-request](#ip_request) 命令。

指定端口时，您将使应用程序可用于相同 {{site.data.keyword.Bluemix_notm}} 空间中正尝试联系主机的 {{site.data.keyword.Bluemix_notm}} 负载均衡器或容器。如果在 Dockerfile 中为要使用的映像指定了端口，请包含该端口。

**提示：**

- 对于 IBM 认证的 Liberty Server 映像或此映像的修改版本，请输入端口 9080。
- 对于 IBM 认证的 Node.js 映像或此映像的修改版本，请输入端口 8000。

-P（可选）：自动公开在映像的 Dockerfile 中为 HTTP 流量指定的端口。

-m *MEMORY*|--memory *MEMORY*（可选）：为组分配内存限制 (MB)。在 CLI 中创建容器组时，每个容器实例的缺省值为“64”MB。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中创建容器组时，每个实例的缺省值为 `256` MB。接受的值为 `64`、`256`、`512`、`1024` 和 `2048`。分配内存限制后，此值无法更改。

-e *ENV*|--env *ENV*（可选）：设置环境变量，其中 **ENV** 为“key=value”对。单独列出多个键。如果包含引号，请用引号将环境变量名称和值括起。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。下表显示了可以指定的一些常用环境变量：

|      环境变量                          |   描述                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 将服务绑定到容器。使用“CCS_BIND_APP”环境变量将应用程序绑定到容器。应用程序绑定到目标服务并用作网桥，以允许 {{site.data.keyword.Bluemix_notm}} 将网桥应用程序的 `VCAP_SERVICES` 信息放入正在运行的容器实例。有关创建网桥应用程序的更多信息，请参阅[将服务绑定到容器](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}。 |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | 创建容器时，向容器添加 SSH 密钥。在 {{site.data.keyword.Bluemix_notm}} 仪表板或 CLI 中创建容器时，可以使用此环境变量来添加 SSH 密钥。有关 SSH 密钥的更多信息，请参阅[登录到容器](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 添加要在容器中监视的日志文件。请包含 `LOG_LOCATIONS` 环境变量以及日志文件的路径。 |
*表 2. 常用环境变量*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  （可选）：通过使用以下格式指定详细信息来将卷连接到容器：“VolumeId:ContainerPath[:ro]”。

- *VOLUME*：卷标识或卷名。
- *CONTAINER_PATH*：容器中卷的绝对路径。
- ro：可选。指定“ro”会将卷设为只读，而不是缺省的读/写。

-n *NAME*|--name *NAME*（必需）：为容器分配名称。

*提示：*容器名称必须以字母开头。名称可以包含大写字母、小写字母、数字、句点 `.`、下划线 `_` 或连字符 `-`。

--link *NAME*:*ALIAS*（可选）：每当您希望让某个容器与另一个正在运行的容器通信时，可以使用主机名的别名来指代该容器。

-it（可选）：以交互方式运行容器。创建容器后，使标准输入保持显示。输入 `exit` 以退出。

*IMAGE*（必需）：要包含在容器中的映像。可以在映像之后列出命令，但不要在映像之后放置任何选项。请在指定映像之前包含所有选项。

如果要在组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中使用映像，请使用以下格式指定映像：*registry.ng.bluemix.net/NAMESPACE/IMAGE*。

如果要使用 IBM Containers 提供的映像，请使用以下格式指定映像：*registry.ng.bluemix.net/IMAGE*。

*CMD*（可选）：传递给容器来执行的命令及相应自变量。此命令必须是长时间运行命令。不要使用不会运行很长时间的短时间运行命令（如 `/bin/date`），因为短时间运行命令可能会导致容器崩溃。



**示例**：

对基于 `registry.ng.bluemix.net/ibmnode` 映像构建的 `my_container` 容器，运行长时间运行的命令 `sh -c "while true;do date; sleep 20; done"`。
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


使用 `my_namespace/nginx` 映像创建并随后启动内存限制为 `1024` MB 的容器 `proxy`，其中 `my_namespace` 是与已登录用户关联的名称空间。
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

使用 `my_namespace/blog` 映像创建并随后启动容器，并将凭证作为环境变量传递。`my_namespace` 是与已登录用户关联的名称空间。
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

使用 `my_namespace/blog` 映像将卷添加到容器，其中 `my_namespace` 是与已登录用户关联的名称空间。
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

建立用于访问容器组的因特网传输路径。可以使用此命令来建立新路径或更新现有路径。

```
bluemix ic route-map [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**先决条件**：端点、登录和目标

**命令选项**：

-n *HOST*|--hostname *HOST*（可选）：路径的主机名。主机名是完整公共路径 URL 的第一部分，例如 URL `mycontainerhost.mybluemix.net` 中的 `mycontainerhost`。

-d *DOMAIN*|--domain *DOMAIN*（可选）：路径的域名，这是完整公共路径 URL 的第二部分。在大多数情况下，域为“mybluemix.net”。您还可使用此参数来指定专用域。

*CONTAINER_GROUP*（必需）：容器组标识或名称。

**示例**：

以下示例显示用于映射组“GROUP1”的路径的请求，其中“my_host”是主机名，“organization.com”是域。
```
bluemix ic route-map -n my_host -d organization.com GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

建立用于访问容器组的因特网传输路径。可以使用此命令来建立新路径或更新现有路径。

```
bluemix ic route-unmap [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**先决条件**：端点、登录和目标

**命令选项**：

-n *HOST*|--hostname *HOST*（可选）：路径的主机名。

-d *DOMAIN*|--domain *DOMAIN*（可选）：路径的域名。

*CONTAINER_GROUP*（必需）：容器组标识或名称。

**示例**：

以下示例显示用于取消映射组“GROUP1”的路径的请求，其中“my_host”是主机名，“organization.com”是域。
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic start
{: #ic_start}
启动已停止的容器。有关更多信息，请参阅 Docker 帮助中的 [start](https://docs.docker.com/reference/commandline/start/){: new_window} 命令。要停止容器，请参阅 [bluemix ic stop](#ic_stop) 命令。

```
bluemix ic start CONTAINER
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

*CONTAINER*（必需）：容器名称或标识。

**响应**：

- 已成功启动容器。

- 针对容器云服务的命令失败

 `{message}`
  
 其中，`{message}` 是相关错误。
 
- 命令失败 - 无法连接到容器云服务

**示例**：

以下示例显示用于启动名为 `proxy` 的容器的请求：
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
停止正在运行的容器。有关更多信息，请参阅 Docker 帮助中的 [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} 命令。要启动容器，请参阅 [bluemix ic start](#ic_start) 命令。

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

*CONTAINER*（必需）：容器名称或标识。

-t *SECS*|--time *SECS*（可选）：终止容器之前要等待的秒数。

**响应**：

- 已成功停止容器。

- 针对容器云服务的命令失败

 `{message}`
  
 其中，`{message}` 是相关错误。
 
- 命令失败 - 无法连接到容器云服务

**示例**：

以下示例显示用于停止名为 `proxy` 的容器的请求。
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

对于一个或多个容器，请查看实时使用情况统计信息。使用 `CTRL+C` 以退出。有关更多信息，请参阅 Docker 帮助中的 [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} 命令。

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

*CONTAINER*（必需）：容器名称或标识。

--no-stream（可选）：仅显示最新结果，而不包含其之前的任何信息。

**示例**：

以下示例显示用于获取有关容器的最近统计信息的请求：
```
bluemix ic stats --no-stream my_container
```


## bluemix ic top
{: #bluemix_ic_top}

显示正在容器中运行的进程。有关更多信息，请参阅 Docker 帮助中的 [top](https://docs.docker.com/reference/commandline/top/){: new_window} 命令。

```
bluemix ic top CONTAINER [CONTAINER]
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

*CONTAINER*（必需）：容器名称或标识。

**示例**：

以下示例显示用于显示名为 `my_container` 的容器中进程的请求。
```
bluemix ic top my_container
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

列出卷。

```
bluemix ic volumes
```

**先决条件**：端点、登录和目标


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

检查卷。

```
bluemix ic volume-inspect VOLUME_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*VOLUME_NAME*（必需）：卷名。

**示例**：

以下示例是用于检查卷的请求，其中 `volume_name` 是卷的名称。
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

创建卷。

```
bluemix ic volume-create VOLUME_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*VOLUME_NAME*（必需）：卷名。名称可以包含小写字母、数字、下划线 `_` 和连字符 `-`。

**示例**：

以下示例显示用于创建卷的请求。
```
bluemix ic volume-create volume_name 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

除去卷。

```
bluemix ic volume-remove VOLUME_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*VOLUME_NAME*（必需）：卷名。

**示例**：

以下示例显示用于除去卷的请求，其中 `volume_name` 是卷的名称。
```
bluemix ic volume-remove volume_name
```

## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

列出文件系统。

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

创建新文件系统。

```
bluemix ic volume-fs-create FILE_SYSTEM_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*FILE_SYSTEM_NAME*（必需）：文件系统名称。名称可以包含小写字母、数字、下划线 `_` 和连字符 `-`。

**示例**：

以下示例显示用于创建文件系统的请求。
```
bluemix ic volume-fs-create my_file_system 
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

除去文件系统。

```
bluemix ic volume-fs-remove FILE_SYSTEM_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*FILE_SYSTEM_NAME*（必需）：文件系统名称。

**示例**：

以下示例显示用于除去文件系统的请求，其中 `my_file_system` 是文件系统的名称。
```
bluemix ic volume-fs-remove my_file_system
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

检查文件系统。

```
bluemix ic volume-fs-inspect FILE_SYSTEM_NAME
```

**先决条件**：端点、登录和目标

**命令选项**：

*FILE_SYSTEM_NAME*（必需）：文件系统名称。

**示例**：

以下示例是用于检查文件系统的请求，其中 `my_file_system` 是文件系统的名称。
```
bluemix ic volume-fs-inspect my_file_system
```
## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

列出所有文件系统类型模板。

```
bluemix ic volume-fs-flavors
```

**先决条件**：端点、登录和目标

## bluemix ic wait
{: #bluemix_ic_wait}

退出容器并显示退出代码以作为确认。有关更多信息，请参阅 Docker 帮助中的 [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} 命令。

```
bluemix ic wait CONTAINER [CONTAINER]
```

**先决条件**：端点、登录、目标和 Docker

**命令选项**：

*CONTAINER*（必需）：容器名称或标识。

**示例**：

以下示例显示用于退出名为 `my_container` 的容器的请求：
```
bluemix ic wait my_container
```


## bluemix ic version
{: #bluemix_ic_version}

显示 Docker 的版本。 

```
bluemix ic version
```

**先决条件**：Docker

要查看 IBM Containers 的版本，请运行 `bluemix ic info`。有关更多信息，请参阅 Docker 帮助中的 [version](https://docs.docker.com/reference/commandline/version/){: new_window} 命令。
