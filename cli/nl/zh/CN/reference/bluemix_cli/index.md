---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI 入门
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI 提供了一种统一的方式，供您通过命令行界面与应用程序、虚拟服务器、容器和其他服务进行交互。{{site.data.keyword.Bluemix_notm}} CLI 还集成了多个社区工具，例如 Cloud Foundry CLI、Docker CLI 和 OpenStack CLI，并初始化了环境设置，以使您能够与不同的计算类型进行交互。

**限制**：Cygwin 不支持 {{site.data.keyword.Bluemix_notm}} CLI，因此请勿在 Cygwin 命令行窗口中使用 {{site.data.keyword.Bluemix_notm}} CLI。

**注**：如果您的网络中有 HTTP 代理服务器位于运行 CLI 的主机和 {{site.data.keyword.Bluemix_notm}} 之间，那么必须在 HTTP_PROXY 环境变量中指定该代理服务器的主机名或 IP 地址。

## 安装 {{site.data.keyword.Bluemix_notm}} CLI
{: #install_bluemix_cli}

安装 {{site.data.keyword.Bluemix_notm}} CLI 之前，请先安装 [cf CLI ![外部链接图标](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}。

对于 Mac OS 和 Windows，请下载 [{{site.data.keyword.Bluemix_notm}} CLI 包](/docs/cli/index.html#downloads)，并运行安装程序。

对于 Linux，请执行以下步骤：

  1. 下载包，并对其解压缩。例如：

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. 转至 `Bluemix_CLI` 目录，然后使用根权限运行 `./install_bluemix_cli` 命令。可以通过 root 用户身份运行此命令，也可以使用 `sudo` 命令来获取根权限。例如：

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

现在，可以开始使用 {{site.data.keyword.Bluemix_notm}} CLI 或安装其他插件。

## 安装插件
{: #install_plug-in}

与 Cloud Foundry CLI 一样，除了内置命令外，{{site.data.keyword.Bluemix_notm}} CLI 还支持通过插件扩展框架来集成其他命令。

要在本地环境中安装插件，请执行以下步骤：

  1. 下载插件。例如：

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. 对于类 UNIX 系统，必须使用 `chmod` 命令使下载的文件成为可执行文件。例如：

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. 使用 `bluemix plugin install` 命令安装插件。例如：

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

要从远程服务器进行安装，请执行以下步骤：

  1. 使用 `bluemix plugin install` 命令直接通过远程 URL 安装插件。例如：

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

您还可以从存储库安装插件。{{site.data.keyword.Bluemix_notm}} 具有用于托管 {{site.data.keyword.Bluemix_notm}} CLI 插件和 Cloud Foundry CLI 插件的存储库：

  * [Cloud Foundry CLI 插件存储库 ](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg)，用于托管 Cloud Foundry CLI 的插件。
  * [{{site.data.keyword.Bluemix_notm}} CLI 插件存储库 ](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg)，专门用于托管 {{site.data.keyword.Bluemix_notm}} CLI 的插件。

要从存储库进行安装，请执行以下步骤：

  1. 在存储库中找到插件。安装了 {{site.data.keyword.Bluemix_notm}} CLI 后，缺省情况下将添加官方存储库 `Bluemix`。可以使用 `bluemix plugin repo-plugins` 命令列出 `Bluemix` 存储库中的插件。例如：

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. 使用 `bluemix plugin install` 命令从 `Bluemix` 存储库安装插件。例如：

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## 登录到 {{site.data.keyword.Bluemix_notm}} CLI
{: #log_bmcli}

安装了 {{site.data.keyword.Bluemix_notm}} CLI 后，可以使用您的 IBM 标识和密码登录到 {{site.data.keyword.Bluemix_notm}}。例如：

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

现在，您已准备好使用 {{site.data.keyword.Bluemix_notm}} 内置命令。例如，运行 `bluemix catalog templates` 命令将列出所有可用的 {{site.data.keyword.Bluemix_notm}} 样板模板：

```
~$ bluemix catalog templates
Listing Bluemix boilerplate templates...

ID                      Name
pi-wdc-java-starter     Personality Insights Java Web Starter
xpages-starter          XPages Web Starter
mobileBackendStarter    Mobile Cloud
pi-wdc-nodejs-starter   Personality Insights Node.js Web Starter
mobileFirstPlatform     MobileFirst Services Starter
xspHelloWorld           IBM XPages
javacloudantbp          Java Cloudant Web Starter
```

# {{site.data.keyword.Bluemix_notm}} (bx) 命令
{: #bluemix_cli}

版本：0.4.6

{{site.data.keyword.Bluemix_notm}} 命令行界面 (CLI) 提供了一组按名称空间分组的命令，供用户用于与 {{site.data.keyword.Bluemix_notm}} 进行交互。一些 {{site.data.keyword.Bluemix_notm}} 命令是现有 cf 命令的包装程序，而另一些为 {{site.data.keyword.Bluemix_notm}} 用户提供了扩展功能。以下信息列出了 {{site.data.keyword.Bluemix_notm}} CLI 支持的命令，并包含命令名称、选项、用法、先决条件、描述和示例。
{:shortdesc}

**注：***先决条件*列出使用命令前必须执行的操作。没有任何先决条件操作的命令会列出**无**。否则，先决条件可能会包含以下一个或多个操作：

<dl>
<dt>端点</dt>
<dd>使用命令前，必须通过 <code>bluemix api</code> 设置 API 端点。</dd>
<dt>登录</dt>
<dd>使用此命令之前，必须使用 <code>bluemix login</code> 命令登录。如果使用联合标识登录，请使用“--sso”选项对一次性密码进行验证。</dd>
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
 <td>[bluemix help](index.html#bluemix_help)</td>
 <td>[bluemix api](index.html#bluemix_api)</td>
 <td>[bluemix_login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](index.html#bluemix_info) </td>
 <td>[bluemix config](index.html#bluemix_config)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
  </tbody>
 </table>


<table summary="可用于管理组织、空间和用户的 bluemix 命令">
 <caption>表 2. 用于管理组织、空间和用户的命令</caption>
 <thead>
 <th colspan="5">用于管理组织、空间和用户的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam account-users](index.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](index.html#bluemix_iam_account_users_delete)</td>
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account_user_invite)</td>
 <td>[bluemix iam account-user-reinvite](index.html#bluemix_iam_account_user_reinvite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-user-add](index.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](index.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 </tr>
 </tbody>
 </table>


<table summary="可用于管理 Cloud Foundry 应用程序的 bluemix 命令">
 <caption>表 3. 用于管理 cf 应用程序的命令</caption>
 <thead>
 <th colspan="5">用于管理 cf 应用程序的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 <td>[bluemix app list](index.html#bluemix_app_list)</td>
<td>[bluemix app show](index.html#bluemix_app_show)</td>
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 </tr>
 <tr>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 <td>[bluemix app start](index.html#bluemix_app_start)</td>
<td>[bluemix app stop](index.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 </tr>
 <tr>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 <td>[bluemix app events](index.html#bluemix_app_events)</td>
<td>[bluemix app files](index.html#bluemix_app_files)</td>
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 </tr>
 <tr>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset)</td>
<td>[bluemix app stacks](index.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
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
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](index.html#bluemix_service_list)</td>
 <td>[bluemix service show](index.html#bluemix_service_show)</td>
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](index.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](index.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
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
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](index.html#bluemix_catalog_template)</td>
<td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix bss account-usage](index.html#bluemix_bss_account_usage)</td>
 <td>[bluemix bss org-usage](index.html#bluemix_bss_org_usage)</td>
 <td>[bluemix bss orgs-usage-summary](index.html#bluemix_orgs_usage_summary)</td>
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td>
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 </tr>
 <tr>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td></td>
 <td></td>
 </tr>
  </tbody>
 </table>


<table summary="可用于管理网络设置的 bluemix 命令">
 <caption>表 6. 用于管理网络设置的命令</caption>
 <thead>
 <th colspan="5">用于管理网络设置的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td>
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td>
 </tr>
 <tr>
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td>
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td>
 </tr>
 <tr>
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td>
 <td></td>
 </tr>
  </tbody>
 </table>

<table summary="可用于在 Bluemix 上管理容器的 bluemix 命令">
 <caption>表 7. 用于在 Bluemix 上管理容器的命令</caption>
 <thead>
 <th colspan="5">用于在 Bluemix 上管理容器的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](index.html#bluemix_ic_service-bind)</td>
 <td>[bluemix ic service-unbind](index.html#bluemix_ic_service-unbind)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](index.html#unpause)</td>
 <td>[bluemix ic unprovision](index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


### bluemix help
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

显示 `ic` 插件的帮助：

```
bluemix help ic
```

或

```
bluemix ic help
```

显示 `ic` 插件下 `group-create` 命令的帮助：

```
bluemix ic help group-create
```


### bluemix api
{: #bluemix_api}
设置或查看 {{site.data.keyword.Bluemix_notm}} API 端点。此命令会对 `cf api` 命令打包。

```
bluemix api [API_ENDPOINT] [--unset]
```

<strong>先决条件</strong>：无

<strong>命令选项</strong>：
   <dl>
   <dt>API_ENDPOINT（可选）</dt>
   <dd>作为目标的 API 端点，例如 `https://api.chinabluemix.net`。如果未指定 *API_ENDPOINT* 和 `--unset` 选项，将显示当前 API 端点。</dd>
   <dt>--unset（可选）</dt>
   <dd>除去 API 端点设置。</dd>
    </dl>
<strong>示例</strong>：

将 API 端点设置为 api.chinabluemix.net：

```
bluemix api api.chinabluemix.net
```

查看当前 API 端点：

```
bluemix api
```

取消设置 API 端点：

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

用户登录。此命令会对 `cf login` 命令打包。命令选项与 `cf login` 命令选项相同。

```
bluemix login [OPTIONS...]
```

<strong>先决条件</strong>：端点

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>命令选项</strong>：
有关 `login` 命令支持的选项的信息，请参阅 `cf login` 命令用法信息，以了解用于管理应用程序的 cf 命令。

<strong>注</strong>：
如果使用联合标识登录，请使用“--sso”选项对一次性密码进行验证。

### bluemix logout
{: #bluemix_logout}

注销用户。此命令会对 `cf logout` 命令打包。

```
bluemix logout
```

<strong>先决条件</strong>：无


### bluemix target
{: #bluemix_target}


设置或查看目标组织或空间。此命令会对 `cf target` 命令打包。

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>先决条件</strong>：端点和登录

<strong>命令选项</strong>：
   <dl>
   <dt>-o <i>ORG_NAME</i>（可选）</dt>
   <dd>要作为目标的组织的名称。</dd>
   <dt>-s <i>SPACE_NAME</i>（可选）</dt>
   <dd>要作为目标的空间的名称。</dd>
   </dl>
如果 -o *ORG_NAME* 或 -s *SPACE_NAME* 均未指定，那么将显示当前组织和空间。
<strong>示例</strong>：

将当前组织设置为 `MyOrg`，将空间设置为 `MySpace`：

```
bluemix target -o MyOrg -s MySpace
```

查看当前组织和空间：

```
bluemix target
```


### bluemix info
{: #bluemix_info}

查看基本 {{site.data.keyword.Bluemix_notm}} 信息，包括当前区域、云控制器版本以及一些有用的端点，例如用于登录和交换访问令牌的端点。

```
bluemix info
```

<strong>先决条件</strong>：端点


### bluemix config
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


### bluemix curl
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


### bluemix iam orgs
{: #bluemix_iam_orgs}

列出所有组织

```
bluemix iam orgs [-r REGION --guid]
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

### bluemix iam org
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

### bluemix iam org-create
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


### bluemix iam org-replicate
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


### bluemix iam org-rename
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

### bluemix iam org-delete
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


### bluemix iam spaces
{: #bluemix_iam_spaces}

此命令的功能和选项与 `cf spaces` 命令的相同。


### bluemix iam space
{: #bluemix_iam_space}

此命令的功能和选项与 `cf space` 命令的相同。


### bluemix iam space-create
{: #bluemix_iam_space_create}

此命令的功能和选项与 `cf create-space` 命令的相同。


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


此命令的功能和选项与 `cf rename-space` 命令的相同。


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


此命令的功能和选项与 `cf delete-space` 命令的相同。


### bluemix iam account-users
{: #bluemix_iam_account_users}

显示与帐户关联的用户。此操作只能由帐户所有者执行。

```
bluemix iam account-users
```

### bluemix iam account-user-invite
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


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

向用户重新发送邀请（必须是组织管理员或帐户所有者）
```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```


### bluemix iam org-users
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

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

将用户添加到组织（需要组织管理员）。
```
 bluemix iam org-user-add USER_NAME ORG
```

### bluemix iam org-user-remove
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

### bluemix iam org-role-set
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


### bluemix iam org-role-unset
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


### bluemix iam space-users
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


### bluemix iam space-role-set
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

### bluemix iam space-role-unset
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


### bluemix app push
{: #bluemix_app_push}

此命令的功能和选项与 `cf push` 命令的相同。


### bluemix app list
{: #bluemix_app_list}

此命令的功能和选项与 `cf apps` 命令的相同。


### bluemix app show
{: #bluemix_app_show}

此命令的功能和选项与 `cf app` 命令的相同。


### bluemix app scale
{: #bluemix_app_scale}

此命令的功能和选项与 `cf scale` 命令的相同。


### bluemix app delete
{: #bluemix_app_delete}

此命令的功能和选项与 `cf delete` 命令的相同。


### bluemix app rename
{: #bluemix_app_rename}

此命令的功能和选项与 `cf rename` 命令的相同。


### bluemix app start
{: #bluemix_app_start}

此命令的功能和选项与 `cf start` 命令的相同。


### bluemix app stop
{: #bluemix_app_stop}

此命令的功能和选项与 `cf stop` 命令的相同。


### bluemix app restart
{: #bluemix_app_restart}

此命令的功能和选项与 `cf restart` 命令的相同。


### bluemix app restage
{: #bluemix_app_restage}


此命令的功能和选项与 `cf restage` 命令的相同。


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


此命令的功能和选项与 `cf restart-app-instance` 命令的相同。


### bluemix app events
{: #bluemix_app_events}

此命令的功能和选项与 `cf events` 命令的相同。


### bluemix app files
{: #bluemix_app_files}

此命令的功能和选项与 `cf files` 命令的相同。


### bluemix app logs
{: #bluemix_app_logs}

此命令的功能和选项与 `cf logs` 命令的相同。


### bluemix app env
{: #bluemix_app_env}

此命令的功能和选项与 `cf env` 命令的相同。


### bluemix app env-set
{: #bluemix_app_env_set}

此命令的功能和选项与 `cf set-env` 命令的相同。


### bluemix app env-unset
{: #bluemix_app_env_unset}

此命令的功能和选项与 `cf unset-env` 命令的相同。


### bluemix app stacks
{: #bluemix_app_stacks}

此命令的功能和选项与 `cf stacks` 命令的相同。


### bluemix app stack
{: #bluemix_app_stack}

此命令的功能和选项与 `cf stack` 命令的相同。


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

此命令的功能和选项与 `cf create-app-manifest` 命令的相同。


### bluemix service offerings
{: #bluemix_service_offerings}


此命令的功能和选项与 `cf marketplace` 命令的相同。


### bluemix service list
{: #bluemix_service_list}

此命令的功能和选项与 `cf services` 命令的相同。


### bluemix service show
{: #bluemix_service_show}

此命令的功能和选项与 `cf service` 命令的相同。


### bluemix service create
{: #bluemix_service_create}

此命令的功能和选项与 `cf create-service` 命令的相同。


### bluemix service update
{: #bluemix_service_update}

此命令的功能和选项与 `cf update-service` 命令的相同。


### bluemix service delete
{: #bluemix_service_delete}

此命令的功能和选项与 `cf delete-service` 命令的相同。


### bluemix service rename
{: #bluemix_service_rename}

此命令的功能和选项与 `cf rename-service` 命令的相同。


### bluemix service bind
{: #bluemix_service_bind}

此命令的功能和选项与 `cf bind-service` 命令的相同。


### bluemix service unbind
{: #bluemix_service_unbind}

此命令的功能和选项与 `cf unbind-service` 命令的相同。


### bluemix service key-create
{: #bluemix_service_key_create}

此命令的功能和选项与 `cf create-service-key` 命令的相同。


### bluemix service key-delete
{: #bluemix_service_key_delete}

此命令的功能和选项与 `cf delete-service-key` 命令的相同。


### bluemix service keys
{: #bluemix_service_keys}

此命令的功能和选项与 `cf service-keys` 命令的相同。


### bluemix service key-show
{: #bluemix_service_key_show}

此命令的功能和选项与 `cf service-key` 命令的相同。


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

此命令的功能和选项与 `cf create-user-provided-service` 命令的相同。


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

此命令的功能和选项与 `cf update-user-provided-service` 命令的相同。


### bluemix catalog templates
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


### bluemix catalog template
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


### bluemix catalog template-run
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


### bluemix network regions
{: #bluemix_network_regions}

查看 {{site.data.keyword.Bluemix_notm}} 上所有区域的信息。

```
bluemix network regions
```

<strong>先决条件</strong>：端点


### bluemix network region-set
{: #bluemix_network_region_set}

切换到指定的区域。此命令会自动重定向到新区域中的相同组织和空间（如果可能）。如果用户已登录，该命令会提示用户选择新的组织和空间。API 端点会相应地更改。

```
bluemix network region-set REGION_NAME
```

<strong>先决条件</strong>：端点

<strong>命令选项</strong>：

   <dl>
   <dt>REGION_NAME（必需）</dt>
   <dd>您要切换到的区域的名称。可以使用 <i>bluemix network regions</i> 命令来查看所有区域名称。</dd>
    </dl>

<strong>示例</strong>：

将当前区域设置为 `eu-gb`：

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

此命令的功能和选项与 `cf routes` 命令的相同。


### bluemix network route-check
{: #bluemix_network_route_check}

此命令的功能和选项与 `cf check-route` 命令的相同。


### bluemix network route-map
{: #bluemix_network_route_map}

将路径映射到具有指定域和主机名的现有 cf 应用程序或容器组。

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix network route-map my-app mychinabluemix.net
```

使用指定域和主机名将路径映射到“my-container-group”：

```
bluemix network route-map my-container-group chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

取消来自现有 cf 应用程序或容器组中的指定路径映射。

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix network route-unmap my-app mychianbluemix.net
```

从 `my-container-group` 取消 `abc.chinabluexmix.net` 的映射：

```
bluemix network route-unmap my-container-group chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

此命令的功能和选项与 `cf create-route` 命令的相同。


### bluemix network route-delete
{: #bluemix_network_route_delete}

此命令的功能和选项与 `cf delete-route` 命令的相同。


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

此命令的功能和选项与 `cf delete-orphaned-routes` 命令的相同。


### bluemix network domains
{: #bluemix_network_domains}

此命令的功能和选项与 `cf domains` 命令的相同。


### bluemix network domain-create
{: #bluemix_network_domain_create}

此命令的功能和选项与 `cf create-domain` 命令的相同。


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

此命令的功能和选项与 `cf delete-domain` 命令的相同。


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

此命令的功能和选项与 `cf create-shared-domain` 命令的相同。


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

此命令的功能和选项与 `cf delete-shared-domain` 命令的相同。



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

显示帐户的每月使用情况和成本。

```
bluemix bss account-usage [-d YYYY-MM] [--json]
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
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

显示组织的每月使用情况详细信息。此操作只能由组织的记帐管理员执行。

```
bluemix bss org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
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



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

显示我的帐户中组织的每月使用情况摘要。

```
bluemix bss orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
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



### bluemix security cert
{: #bluemix_security_cert}

列出域的证书信息。

```
bluemix security cert DOMAIN_NAME
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
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

将证书添加到当前组织中的指定域。

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
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
   <dt>--verify-client（可选）</dt>
   <dd>是否启用客户机证书验证。</dd>
   </dl>


<strong>示例</strong>：

将证书添加到域 `ibmcxo-eventconnect.com`：

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

从当前组织中的指定域除去证书。

```
bluemix security cert-remove DOMAIN [-f]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt>DOMAIN（必需）</dt>
   <dd>要从中除去证书的域。</dd>
   <dt>-f（可选）</dt>
   <dd>强制删除而不确认。</dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中注册的所有插件存储库。

```
bluemix plugin repos
```

<strong>先决条件</strong>：无


### bluemix plugin repo-add
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


### bluemix plugin repo-remove
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


### bluemix plugin repo-plugins
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


### bluemix plugin list
{: #bluemix_plugin_list}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中的所有已安装插件。

```
bluemix plugin list
```

<strong>先决条件</strong>：无


### bluemix plugin install
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






### bluemix plugin uninstall
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


### bluemix ic attach
{: #bluemix_ic_attach}

控制正在运行的容器或查看其输出。使用 `CTRL+C` 以退出并停止容器。此命令将调用 Docker CLI。有关更多信息，请参阅 Docker 帮助中的 [attach ](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt>--no-stdin（可选）</dt>
   <dd>不包含标准输入。</dd>
   <dt>--sig-proxy（可选）</dt>
   <dd>将所有接收到的信号通过代理传递到进程。缺省值为 <i>true</i>。</dd>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
    </dl>

<strong>示例</strong>：

以下示例显示用于连接到容器 `my_container` 的请求：

```
bluemix ic attach my_container
```


### bluemix ic build
{: #bluemix_ic_build}

调用 IBM Containers 构建服务，用于在本地或在专用 {{site.data.keyword.Bluemix_notm}} 存储库中构建 Docker 映像。此命令将调用 Docker CLI。有关更多信息，请参阅 Docker 帮助中的 [build ](https://docs.docker.com/engine/reference/commandline/build/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i>（必需）</dt>
   <dd>要应用到所创建映像的存储库名称。</dd>
   <dt>--no-cache（可选）</dt>
   <dd>在构建映像时不使用高速缓存。缺省值为 <i>false</i>。</dd>
   <dt>--pull（可选）</dt>
   <dd>尝试从注册表拉取基本映像（即使它已高速缓存）。</dd>
   <dt>-q|--quiet（可选）</dt>
   <dd>禁止显示容器生成的详细输出。缺省值为 <i>false</i>。</dd>
   <dt><i>DOCKERFILE_LOCATION</i>（必需）</dt>
   <dd>本地主机上 Dockerfile 和上下文的路径。</dd>
    </dl>

<strong>示例</strong>：

以下示例显示用于构建名为 *myimage* 的映像的请求。要在该构建中使用的 Dockerfile 和其他工件位于运行该命令的目录中。由于映像名称随附了注册表和名称空间，因此会在组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中构建映像。

```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


### bluemix ic cp
{: #bluemix_ic_cp}
在容器与本地文件系统之间复制文件或文件夹。此命令将调用 Docker CLI。有关更多信息，请参阅 Docker 帮助中的 [cp ](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。


### bluemix ic cpi
{: #bluemix_ic_cpi}

访问 Docker Hub 映像或本地注册表中的映像，然后将该映像复制到专用 {{site.data.keyword.Bluemix_notm}} 存储库。

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：
   <dl>
   <dt><i>SOURCE_IMAGE</i>（必需）</dt>
   <dd>源存储库和映像名称。</dd>
   <dt><i>DESTINATION_IMAGE</i>（必需）</dt>
   <dd>专用 {{site.data.keyword.Bluemix_notm}} 存储库 URL，其中包含名称空间和目标映像名称。映像的标记是可选的。</dd>
   </dl>

<strong>示例</strong>：

将映像从源存储库复制到专用存储库，然后为该映像添加标记：

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

将 `sinatra` 映像从 `training` 存储库复制到专用存储库 `registry.ng.bluemix.net/mynamespace`，然后将该映像命名为 `mysinatra`。为映像 `mysinatra` 添加标记 `v1`。

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


### bluemix ic exec
{: #bluemix_ic_exec}

在容器内执行命令。有关更多信息，请参阅 Docker 帮助中的 [exec ](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt>-d|--detach（可选）</dt>
   <dd>在后台运行指定的命令。</dd>
   <dt>-it（可选）</dt>
   <dd>交互方式。使标准输入保持显示。输入 <i>exit</i> 以退出。</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i>（可选）</dt>
   <dd>用户名。</dd>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   <dt><i>CMD</i>（可选）</dt>
   <dd>要在指定的一个或多个容器内执行的命令。</dd>
   </dl>

<strong>示例</strong>：

以交互方式在 `my_container` 容器内执行 `bash` 命令：

```
bluemix ic exec -it my_container bash
```

在 `my_container` 容器内执行 `date` 命令：

```
bluemix ic exec my_container date
```


### bluemix ic group-create
{: #bluemix_ic_group_create}

创建可扩展容器组。

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRONMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：
   <dl>
    <dt><i>IMAGE_NAME</i>（必需）</dt>
   <dd>要包含在容器组中的每个容器实例内的映像。可以在映像之后列出命令，但不要在映像之后放置任何选项。请在指定映像之前包含所有选项。<br><br>如果在组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中使用映像，请使用以下格式指定映像：<i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>。<br><br>如果使用 IBM Containers 提供的映像，请不要包含组织的名称空间。使用以下格式指定映像：<i>registry.ng.bluemix.net/IMAGE</i>。</dd>
   <dt>--name <i>GROUP_NAME</i>（必需）</dt>
   <dd>为组分配名称。不推荐使用 <i>-n</i>。<br>
   <strong>提示：</strong>容器名称必须以字母开头。名称可以包含大写字母、小写字母、数字、句点 .、下划线 _ 或连字符 -。</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i>（可选）</dt>
   <dd>为组分配内存限制 (MB)。在 CLI 中创建容器组时，每个容器实例的缺省值为 <i>64</i> MB。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中创建容器组时，每个容器实例的缺省值为 <i>256</i> MB。接受的值为 <i>64</i>、<i>256</i>、<i>512</i>、<i>1024</i> 和 <i>2048</i>。分配内存限制后，此值无法更改。</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i>（可选）</dt>
   <dd>主机名，如 <i>mycontainerhost</i>。主机和域组合在一起构成了完整的公共路径 URL，例如 <i>http://mycontainerhost.mybluemix.net</i>。使用 <i>bluemix ic group-inspect</i> 命令来查看容器组的详细信息时，主机和域会作为路径一起列出。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>（可选）</dt>
   <dd>通常，域为 <i>.mybluemix.net</i>。主机和域组合在一起构成了完整的公共路径 URL，例如 <i>http://mycontainerhost.mybluemix.net</i>。使用 <i>bluemix ic group-inspect</i> 命令来查看容器组的详细信息时，主机和域会作为路径一起列出。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i>（可选）</dt>
   <dd>设置环境变量。单独列出多个键。如果包含引号，请用引号将环境变量名称和值括起。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。下表显示了可以指定的一些常用环境变量：</dd>
    </dl>


|  环境变量                              |     描述                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 将服务绑定到容器。使用 `CCS_BIND_APP` 环境变量将应用程序绑定到容器。应用程序绑定到目标服务并用作网桥，以允许 {{site.data.keyword.Bluemix_notm}} 将网桥应用程序的 `VCAP_SERVICES` 信息放入正在运行的容器实例。|
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 要在不使用网桥应用程序的情况下将 Bluemix 服务直接绑定到容器，请使用 CCS_BIND_SRV。此绑定允许 Bluemix 将 VCAP_SERVICES 信息插入正在运行的容器实例中。要列出多个 Bluemix 服务，请将这些服务包含在同一环境变量中。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 添加要在容器中监视的日志文件。请包含 `LOG_LOCATIONS` 环境变量以及日志文件的路径。 |
{: caption="表 8. 常用环境变量" caption-side="top"}


 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i>（可选）</dt>
   <dd> 从文件导入环境变量，其中 ENVFILE 是本地目录上您文件的路径。文件中的每一行代表一个 key=value 对。</dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro]（可选）</dt>
   <dd>通过使用格式 <i>VolumeId:ContainerPath[:ro]</i> 指定详细信息来将卷连接到容器。
<ul>
   <li><i>VOLUME</i>：卷标识或名称。</li>
   <li><i>CONTAINER_PATH</i>：容器中卷的绝对路径。</li>
   <li>ro：可选。指定 <i>ro</i> 会将卷设为只读，而不是缺省的读/写。</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>（可选）</dt>
   <dd>公开用于 HTTP 流量的端口。组中的容器必须侦听该 HTTP 端口。无法发出 HTTPS 请求。对于容器组，不能包含多个端口。<br><br>指定端口时，您使应用程序可用于相同 {{site.data.keyword.Bluemix_notm}} 空间中正尝试联系主机的 {{site.data.keyword.Bluemix_notm}} 负载均衡器或容器。然后，{{site.data.keyword.Bluemix_notm}} 负载均衡器或容器可以使用该端口来访问同一 {{site.data.keyword.Bluemix_notm}} 空间中的主机和应用程序。如果在 Dockerfile 中为要使用的映像指定了端口，请包含该端口。<br>
   <strong>提示</strong>：<ul>
   <li>对于 IBM 认证的 Liberty Server 映像或此映像的修改版本，请输入端口 9080。</li>
   <li>对于 IBM 认证的 Node.js 映像或此映像的修改版本，请输入端口 8000。</li>
   </ul>
   </dd>
   <dt>-P（可选）</dt>
   <dd>发布所有端口</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i>（可选）</dt>
   <dd>最小实例数。缺省值为 1。如果设置了最小实例数，那么创建容器组后，无法更改此值。</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i>（可选）</dt>
   <dd>最大实例数。缺省值为 2。如果设置了最大实例数，那么创建容器组后，无法更改此值。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i>（可选）</dt>
   <dd>需要的实例数。缺省值为 2。</dd>
   <dt>--auto（可选）</dt>
   <dd>创建容器组并启用自动恢复后，IBM Containers 会通过向所分配的端口发送 HTTP 请求来检查每个实例的运行状况。<br>
在接下来的两个 90 秒的时间间隔内，如果没有收到来自某个容器实例的响应，那么会除去该实例并替换为新实例。如果该容器有响应，那么不会执行任何操作。此过程会持续重复。在 30 分钟的时段内，如果容器组中不同容器的总数等于或超过该容器组最大大小的 3 倍，那么会对该容器组永久禁用自动恢复。要重新启用自动恢复，必须重新创建容器组。</dd>
  <dt>--anti（可选）</dt>
  <dd> 使用反亲缘关系，可使您的容器组具有更高的可用性。--anti 选项强制将组中的每一个容器实例置于独立的物理计算节点上，这可降低因硬件故障而导致组中所有容器崩溃的几率。您可能无法对较大的组大小使用此选项，因为每一个 Bluemix 区域和组织在可用于部署的计算节点集方面存在限制。如果部署不成功，请减少组中的容器实例数或移除 --anti 选项。</dd>
   <dt><i>CMD</i>（可选）</dt>
   <dd>该命令和自变量会传递到容器组以便执行。此命令必须是长时间运行命令。不要使用不会运行很长时间的短时间运行命令（例如 <i>/bin/date</i>），因为短时间运行命令可能会导致容器崩溃。<br> <strong>注：</strong> <ul>
   <li>命令及其自变量必须位于 <i>bluemix ic run</i> 命令行的末尾。</li>
   <li>如果命令自变量包含连字符 -（如先前命令示例中的 <i>-c</i> 所示），那么必须在命令前面添加两个连字符 --。</li>
   </ul></dd>
   </dl>


<strong>示例</strong>：

使用 IBM Containers 提供的 `registry.ng.bluemix.net/ibmnode` 映像创建容器组 `my_container_group`，然后对该容器组运行长时间运行的命令 `ping localhost`：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

使用 IBM Containers 提供的 `registry.ng.bluemix.net/ibmnode` 映像创建容器组 `my_container_group`，然后对该容器组运行长时间运行的命令 `tail -f /dev/null`：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

使用 `registry.ng.bluemix.net/ibmliberty` 映像创建可扩展组 `mygroup`，并启用自动恢复。端口为 `9080`，主机名为 `mycontainerhost`，域名为 `mybluemix.net`。
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


### bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

查看在创建容器组时为其指定的详细信息，例如环境变量、端口或内存。

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER_GROUP</i>（必需）</dt>
   <dd>容器组标识或名称。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于检查容器组 `my_group` 的请求：

```
bluemix ic group-inspect my_group
```


### bluemix ic group-instances
{: #bluemix_ic_group_instances}

列出指定容器组的实例。

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER_GROUP</i>（必需）</dt>
   <dd>容器组标识或名称。</dd>
   </dl>

<strong>示例</strong>：

列出容器组 `my_group` 中的所有实例：

```
bluemix ic group-instances my_group
```


### bluemix ic group-remove
{: #bluemix_ic_group_remove}

从空间中除去容器组。

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt>-f|--force（可选）</dt>
   <dd>强制除去正在运行的或发生故障的容器。</dd>
   <dt><i>GROUP_NAME</i>（必需）</dt>
   <dd>容器组标识或名称。</dd>
   </dl>


<strong>示例</strong>：

以下示例显示用于除去容器组的请求，其中 `my_group` 是容器组的名称。

```
bluemix ic group-remove my_group
```


### bluemix ic group-update
{: #bluemix_ic_group_update}

更新容器组。


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**提示：**要更新容器组的主机名或域，请使用 `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`。

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：
 <dl>
   <dt>--anti（可选）</dt>
   <dd>使用反亲缘关系，可使您的容器组具有更高的可用性。--anti 选项强制将组中的每一个容器实例置于独立的物理计算节点上，这可降低因硬件故障而导致组中所有容器崩溃的几率。您可能无法对较大的组大小使用此选项，因为每一个 Bluemix 区域和组织在可用于部署的计算节点集方面存在限制。如果部署不成功，请减少组中的容器实例数或移除 --anti 选项。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i>（可选）</dt>
   <dd>需要的实例数。缺省值为 <i>2</i>。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>（可选）</dt>
   <dd>设置环境变量。单独列出多个键。如果包含引号，请用引号将环境变量名称和值括起。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。</dd>
   <dt><i>GROUP_NAME</i>（必需）</dt>
   <dd>容器组标识或名称。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于更新容器组 `my_group` 的请求：

```
bluemix ic group-update --desired 5 my_group
```


### bluemix ic groups
{: #bluemix_ic_groups}

列出组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中的容器组。

```
bluemix ic groups [-q]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：
	<dl>
	<dt>-q（可选）</dt>
   	<dd>仅显示组标识</dd>
	</dl>


### bluemix ic images
{: #bluemix_ic_images}

查看组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中所有可用映像的列表。有关更多信息，请参阅 Docker 帮助中的 [images ](https://docs.docker.com/engine/reference/commandline/images){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。此列表包含映像标识、创建日期和映像名称。

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt>-a|--all（可选）</dt>
   <dd>包含组织的存储库中每个映像的所有映像层，而不仅仅包含最近的层。</dd>
   <dt>-f（可选）</dt>
   <dd>按提供的条件过滤映像列表。</dd>
   <dt>--no-trunc（可选）</dt>
   <dd>不截断输出。</dd>
   <dt>-q|--quiet（可选）</dt>
   <dd>仅显示数字标识。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于接收组织的可用映像列表的请求：

```
bluemix ic images
```


### bluemix ic info
{: #bluemix_ic_info}

查看用于描述容器云服务实例状态的一组信息。该信息包括容器数限制、容器使用情况、正在运行的容器数、内存限制、内存使用情况、浮动 IP 地址限制、浮动 IP 地址使用情况、CCS 主机 URL、注册表主机 URL 和调试方式状态。

```
bluemix ic info
```

<strong>先决条件</strong>：端点、登录和目标


### bluemix ic init
{: #bluemix_ic_init}

初始化本地计算机上的容器环境，以使用 IBM Containers 服务的完整功能。

```
bluemix ic init
```

<strong>先决条件</strong>：端点、登录和目标

**注：**初始化之前，请确保 Docker CLI (docker) 已安装并在 PATH 环境变量中配置。要切换到其他区域，请使用 `bluemix region-set` 命令。

<strong>示例</strong>：

切换到 `us-south` 区域：

```
bluemix region-set us-south
```


### bluemix ic inspect
{: #bluemix_ic_inspect}

查看有关容器的信息。有关更多信息，请参阅 Docker 帮助中的 [inspect](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} 命令。

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt><i>IMAGE</i>（必需）</dt>
   <dd>通过指定映像名称或标识来查看有关特定映像的详细信息。</dd>
   <dt>images（必需）</dt>
   <dd>查看有关存储库中所有映像的详细信息。</dd>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>通过指定容器名称或标识来查看有关特定容器的详细信息。</dd>
   </dl>

**提示：**一次只能指定 *IMAGE*、*images* 或 *CONTAINER* 中的一个。

<strong>示例</strong>：

以下示例显示用于检查名为 `proxy` 的容器的请求：
```
bluemix ic inspect proxy
```


### bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

将可用浮动 IP 地址绑定到容器。

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>IP_ADDRESS</i>（必需）</dt>
   <dd>要绑定的 IP 地址。</dd>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>要绑定的容器标识或名称。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于将 IP 地址 `192.123.12.12` 绑定到容器 `proxy` 的请求：

```
bluemix ic ip-bind 192.123.12.12 proxy
```


### bluemix ic ip-release
{: #bluemix_ic_ip_release}

从容器云服务实例释放浮动 IP 地址。

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>IP_ADDRESS</i>（必需）</dt>
   <dd>要释放的 IP 地址。</dd>
   </dl>


### bluemix ic ip-request
{: #ip_request}
请求新的浮动 IP 地址。

```
bluemix ic ip-request [-q]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt>-q（可选）</dt>
   <dd>仅列出 IP 地址，而不列出绑定到那些 IP 地址的容器的标识。</dd>
   </dl>


### bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

将浮动 IP 地址从其容器取消绑定。

公共 IP 地址是 IBM Containers 中的有限资源。因此，对于免费试用版用户，如果有分配给空间的公共 IP 地址未绑定到容器，那么会大约每周回收一次这些公共 IP 地址。对于现买现付客户或预订客户，永远都不会回收这些未绑定的公共 IP 地址。

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>IP_ADDRESS</i>（必需）</dt>
   <dd>要取消绑定的 IP 地址。</dd>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>要取消绑定的容器标识或名称。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于取消 IP 地址 `192.123.12.12` 与容器 `proxy` 的绑定的请求：

```
bluemix ic ip-unbind 192.123.12.12 proxy
```


### bluemix ic ips
{: #bluemix_ic_ips}

列出已登录用户的可用浮动 IP 地址。列表包含 IP 地址以及这些 IP 地址链接到的容器标识。如果 IP 地址是未用过的，那么不会显示容器标识。

```
bluemix ic ips [-q]
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt>-q（可选）</dt>
   <dd>仅列出 IP 地址，而不列出绑定到那些 IP 地址的容器的标识。</dd>
   </dl>


<strong>示例</strong>：

以下示例显示用于接收组织的所有 IP 地址列表的请求。

```
bluemix ic ips -q
```


### bluemix ic kill
{: #bluemix_ic_kill}

停止容器中正在运行的进程而不停止容器。有关更多信息，请参阅 Docker 帮助中的 [kill ](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i>（可选）</dt>
   <dd>向正在容器中运行的进程发送命令。</dd>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器标识或名称。</dd>
   </dl>


<strong>示例</strong>：

以下示例显示用于终止容器 `proxy` 中的进程的请求：

```
bluemix ic kill proxy
```


### bluemix ic logs
{: #bluemix_ic_logs}

显示正在运行的容器的输出或错误日志。有关更多信息，请参阅 Docker 帮助中的 [logs ](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。
```
bluemix ic logs [OPTIONS] CONTAINER
```


### bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

查看您登录到的组织的专用 {{site.data.keyword.Bluemix_notm}} 映像存储库的名称。

```
bluemix ic namespace-get
```

<strong>先决条件</strong>：端点、登录和目标


### bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

设置您登录到的组织的专用 {{site.data.keyword.Bluemix_notm}} 映像存储库的名称。

*限制*：不能在存储库名称空间的名称中使用连字符 `-`。

```
bluemix ic namespace-set NAME
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>NAME</i>（必需）</dt>
   <dd>仅一次性功能，用于设置组织的存储库名称空间（如果尚未设置）。设置名称空间后，请通过 `bluemix ic init` 命令重新初始化 IBM Containers，然后再继续。</dd>
   </dl>


### bluemix ic pause
{: #pause}

暂停正在运行的容器内的所有进程。有关更多信息，请参阅 Docker 帮助中的 [pause ](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。要停止容器，请参阅 [bluemix ic unpause](#unpause) 命令。

```
bluemix ic pause CONTAINER
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：
   <dl>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   </dl>

<strong>响应</strong>：

- 已成功暂停容器。

- 针对容器云服务的命令失败

 `{message}`

 其中，`{message}` 是相关错误。

- 命令失败 - 无法连接到容器云服务

<strong>示例</strong>：

以下示例显示用于暂停名为 `proxy` 的容器的请求：

```
bluemix ic pause proxy
```


### bluemix ic port
{: #bluemix_ic_port}

列出容器的端口映射或特定映射。此命令会对 `docker port` 命令打包。有关更多信息，请参阅 Docker 帮助中的 [port ](https://docs.docker.com/engine/reference/commandline/port/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。


### bluemix ic ps
{: #bluemix_ic_ps}
查看正在已登录用户的名称空间中运行的容器的列表。缺省情况下，此命令仅显示正在运行的容器。有关更多信息，请参阅 Docker 帮助中的 [ps ](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt>-a|--all（可选）</dt>
   <dd>显示所有容器（包括正在运行和已停止的容器）。</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i>（可选）</dt>
   <dd>搜索具有特定环境变量值的容器。您可以按在检查容器时 CLI 响应的 Env 部分中列出的任何环境变量键或值来过滤容器。将 SEARCH_CRITERIA 替换为要查找的键或值。搜索条件无需是完全匹配的。</dd>
   <dt>-s|--size（可选）</dt>
   <dd>列出容器的大小。</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i>（可选）</dt>
   <dd>列出最新创建的容器，其中 <i>NUM</i> 是要返回的最新创建的容器数。<br><br> 例如，如果已按顺序创建了容器 <i>node1</i> 到 <i>node5</i>，那么命令 <i>bluemix ic ps --limit 2</i> 会返回 node4 和 node5，因为它们是最后创建的两个容器。</dd>
   <dt>-q|--quiet（可选）</dt>
   <dd>仅显示容器标识。</dd>
   </dl>


<strong>示例</strong>：

以下示例显示用于查看所有正在运行和已停止的容器的请求：

```
bluemix ic ps -a
```


### bluemix ic rename
{: #bluemix_ic_rename}
重命名容器。有关更多信息，请参阅 Docker 帮助中的 [rename ](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

<dl>
   <dt><i>OLD_NAME</i>（必需）</dt>
   <dd>容器的旧名称。</dd>
   <dt><i>NEW_NAME</i>（必需）</dt>
   <dd>容器的新名称。</dd>
   </dl>


### bluemix ic reprovision
{: #bluemix_ic_reprovision}

在登录的 Bluemix 空间中重新创建 IBM Containers 服务。空间的原始配额会保留。

<strong>重要事项</strong>：运行此命令时，此空间内的所有单个容器和组都不会迁移到重新供应的空间，且在迁移过程中将会除去。

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>命令选项</strong>：

<dl>
   <dt>--force|-f（可选）</dt>
   <dd>强制在 Bluemix 空间中重新创建 IBM Containers 服务。</dd>
   <dt><i>AVAILABILITY_ZONE</i>（可选）</dt>
   <dd>部署容器所在的 IBM Containers 可用性区域的名称。如果未指定可用性区域，那么将会使用针对区域设置的缺省可用性区域。</dd>
   </dl>


### bluemix ic restart
{: #bluemix_ic_restart}

重新启动容器。有关更多信息，请参阅 Docker 帮助中的 [restart ](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i>（可选）</dt>
   <dd>重新启动容器之前要等待的秒数。</dd>
   </dl>


<strong>响应</strong>：

- 已成功重新启动容器。

- 针对容器云服务的命令失败

 `{message}`

 其中，`{message}` 是相关错误。

- 命令失败 - 无法连接到容器云服务

<strong>示例</strong>：

以下示例显示用于重新启动名为 `proxy` 的容器的请求：

```
bluemix ic restart proxy
```


### bluemix ic rm
{: #bluemix_ic_rm}

除去容器。有关更多信息，请参阅 Docker 帮助中的 [rm ](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt>-f|--force（可选）</dt>
   <dd>强制除去正在运行的或发生故障的容器。</dd>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   </dl>

<strong>响应</strong>：

- 已成功除去容器。

- 针对容器云服务的命令失败

 `{message}`

 其中，`{message}` 是相关错误。

- 命令失败 - 无法连接到容器云服务。

<strong>示例</strong>：

以下示例显示用于除去名为 `proxy` 的容器的请求：

```
bluemix ic rm proxy
```


### bluemix ic rmi
{: #bluemix_ic_rmi}

从已登录用户的名称空间除去映像。有关更多信息，请参阅 Docker 帮助中的 [rmi ](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i>（可选）</dt>
   <dd>更改注册表主机。缺省行为是使用在 <i>bluemix ic init</i> 命令中指定的注册表。</dd>
   <dt><i>IMAGE</i>（必需）</dt>
   <dd>要除去的映像的名称。如果未在映像名称中指定标记，那么缺省情况下会删除标记为 <i>latest</i> 的映像。</dd>
   </dl>

<strong>响应</strong>：

- 已除去：`{IMAGE}`

 其中，`{IMAGE}` 是已除去映像的名称。

- 错误！未指定注册表主机。

- 除去映像失败 - 无法连接到容器云注册表

- 针对容器云服务的命令失败

 `{message}`

 其中，`{message}` 是相关错误。

<strong>示例</strong>：

以下示例显示用于除去映像 `mynamespace/myimage:latest` 的请求：

```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


### bluemix ic route-map
{: #bluemix_ic_route_map}

建立用于访问容器组的因特网传输路径。可以使用此命令来建立新路径或更新现有路径。

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i>（可选）</dt>
   <dd>路径的主机名。主机名是完整公共路径 URL 的第一部分，例如 URL <i>mycontainerhost.mybluemix.net</i> 中的 <i>mycontainerhost</i>。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>（可选）</dt>
   <dd>路径的域名，这是完整公共路径 URL 的第二部分。在大多数情况下，域为 <i>mybluemix.net</i>。您还可使用此参数来指定专用域。</dd>
   <dt><i>CONTAINER_GROUP</i>（必需）</dt>
   <dd>容器组标识或名称。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于映射组 `GROUP1` 的路径的请求，其中 `my_host` 是主机名，`mybluemix.net` 是域。
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


### bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

建立用于访问容器组的因特网传输路径。可以使用此命令来建立新路径或更新现有路径。

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i>（可选）</dt>
   <dd>路径的主机名。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>（可选）</dt>
   <dd>路径的域名。</dd>
   <dt><i>CONTAINER_GROUP</i>（必需）</dt>
   <dd>容器组标识或名称。</dd>
   </dl>

<strong>示例</strong>：

以下示例是用于取消映射组 `GROUP1` 的路径的请求，其中 `my_host` 是主机名，`organization.com` 是域。
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


### bluemix ic run
{: #bluemix_ic_run}

通过映像名称在容器云服务中启动新容器。有关更多信息，请参阅 Docker 帮助中的 [run ](https://docs.docker.com/engine/reference/commandline/run/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**注：**确保已安装 Cloud Foundry 命令工具，并且您具有 Cloud Foundry 令牌。使用 `bluemix login` 成功登录，然后使用 `bluemix ic init` 生成必需的令牌和证书。


<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>（可选）</dt>
   <dd>公开用于 HTTP 流量的端口。包含在 Dockerfile 中为要使用的映像指定的任何端口。可以使用多个 <i>-p</i> 选项包含多个端口。如果公共 IP 地址可用，那么公开端口会自动将公共 IP 地址绑定到容器。<br><br>如果空间中有要绑定到容器的现有 IP 地址，那么可以指定该 IP 地址，而不是以后绑定。IP 地址必须使用以下格式指定：&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br>。<br>有关请求空间的 IP 地址的更多信息，请参阅 <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a> 命令。<br><br>指定端口时，您将使应用程序可用于相同 {{site.data.keyword.Bluemix_notm}} 空间中正尝试联系主机的 {{site.data.keyword.Bluemix_notm}} 负载均衡器或容器。如果在 Dockerfile 中为要使用的映像指定了端口，请包含该端口。<br><br><strong>提示：</strong><ul><li>对于 IBM 认证的 Liberty Server 映像或此映像的修改版本，请输入端口 9080。</li><li>对于 IBM 认证的 Node.js 映像或此映像的修改版本，请输入端口 8000。</li></ul></dd>
   <dt>-P（可选）</dt>
   <dd>自动公开在映像的 Dockerfile 中为 HTTP 流量指定的端口。</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i>（可选）</dt>
   <dd>为组分配内存限制 (MB)。在 CLI 中创建容器组时，每个容器实例的缺省值为 64 MB。在 {{site.data.keyword.Bluemix_notm}}“仪表板”中创建容器组时，每个实例的缺省值为 256 MB。接受的值为 64、256、512、1024 和 2048。分配内存限制后，此值无法更改。</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i>（可选）</dt>
   <dd>设置环境变量，其中 <i>ENV</i> 是 key=value 对。单独列出多个键。如果包含引号，请用引号将环境变量名称和值括起。例如：-e "key1=value1" -e "key2=value2" -e "key3=value3"。下表显示了可以指定的一些常用环境变量：</dd>
   </dl>


|      环境变量                          |   描述                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 将服务绑定到容器。使用 `CCS_BIND_APP` 环境变量将应用程序绑定到容器。应用程序绑定到目标服务并用作网桥，以允许 {{site.data.keyword.Bluemix_notm}} 将网桥应用程序的 `VCAP_SERVICES` 信息放入正在运行的容器实例。有关创建网桥应用程序的更多信息，请参阅[将服务绑定到容器](/docs/containers/container_integrations_binding.html){: new_window}。 |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 要在不使用网桥应用程序的情况下将 Bluemix 服务直接绑定到容器，请使用 CCS_BIND_SRV。此绑定允许 Bluemix 将 VCAP_SERVICES 信息插入正在运行的容器实例中。要列出多个 Bluemix 服务，请将这些服务包含在同一环境变量中。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 添加要在容器中监视的日志文件。请包含 `LOG_LOCATIONS` 环境变量以及日志文件的路径。 |
{: caption="表 9. 常用环境变量" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro]（可选）</dt>
   <dd>通过使用格式 <i>VolumeId:ContainerPath[:ro]</i> 指定详细信息来将卷连接到容器。
<ul>
   <li><i>VOLUME</i>：卷标识或名称。</li>
   <li><i>CONTAINER_PATH</i>：容器中卷的绝对路径。</li>
   <li>ro：可选。指定 <i>ro</i> 会将卷设为只读，而不是缺省的读/写。</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i>（必需）</dt>
   <dd>为容器分配名称。<br> <strong>提示：</strong>容器名称必须以字母开头。名称可以包含大写字母、小写字母、数字、句点 .、下划线 _ 或连字符 -。</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i>（可选）</dt>
   <dd>每当您希望让某个容器与另一个正在运行的容器通信时，可以使用主机名的别名来指代该容器。</dd>
   <dt>-it（可选）</dt>
   <dd>以交互方式运行容器。创建容器后，使标准输入保持显示。输入 <i>exit</i> 以退出。</dd>
   <dt><i>IMAGE</i>（必需）</dt>
   <dd>要包含在容器中的映像。可以在映像之后列出命令，但不要在映像之后放置任何选项。请在指定映像之前包含所有选项。请在指定映像之前包含所有选项。<br><br>如果在组织的专用 {{site.data.keyword.Bluemix_notm}} 存储库中使用映像，请使用以下格式指定映像：<i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>。<br><br>如果使用 IBM Containers 提供的映像，请使用以下格式指定映像：<i>registry.ng.bluemix.net/IMAGE</i>。</dd>
   <dt><i>CMD</i>（可选）</dt>
   <dd>该命令和自变量会传递到容器组以便执行。此命令必须是长时间运行命令。不要使用不会运行很长时间的短时间运行命令（例如 <i>/bin/date</i>），因为短时间运行命令可能会导致容器崩溃。</dd>
   </dl>


<strong>示例</strong>：

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


### bluemix ic service-bind
{: #bluemix_ic_service-bind}

将服务添加到正在运行的容器组。此命令仅可用于容器组。单个容器必须将服务绑定为 bluemix ic run 命令的一部分。

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE 
```
<strong>命令选项</strong>：

   <dl>
   <dt><i>GROUP_NAME</i>（必需）</dt>
   <dd>组标识或名称。</dd>
   <dt><i>SERVICE_INSTANCE</i>（必需）</dt>
   <dd>要添加到容器组的服务实例的名称。</dd>
   </dl>


### bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

将服务从运行中容器组除去。此命令仅可用于容器组。单个容器必须除去容器并创建不带服务的新容器。

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE 
```
<strong>命令选项</strong>：

   <dl>
   <dt><i>GROUP_NAME</i>（必需）</dt>
   <dd>组标识或名称。</dd>
   <dt><i>SERVICE_INSTANCE</i>（必需）</dt>
   <dd>要添加到容器组的服务实例的名称。</dd>
   </dl>


### bluemix ic start
{: #ic_start}
启动已停止的容器。有关更多信息，请参阅 Docker 帮助中的 [start ](https://docs.docker.com/engine/reference/commandline/start/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。要停止容器，请参阅 [bluemix ic stop](#ic_stop) 命令。

```
bluemix ic start CONTAINER
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   </dl>


<strong>响应</strong>：

- 已成功启动容器。

- 针对容器云服务的命令失败

 `{message}`

 其中，`{message}` 是相关错误。

- 命令失败 - 无法连接到容器云服务

<strong>示例</strong>：

以下示例显示用于启动名为 `proxy` 的容器的请求：

```
bluemix ic start proxy
```


### bluemix ic stats
{: #bluemix_ic_stats}

对于一个或多个容器，请查看实时使用情况统计信息。使用 `CTRL+C` 以退出。有关更多信息，请参阅 Docker 帮助中的 [stats](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} 命令。

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   <dt>--no-stream（可选）</dt>
   <dd>仅显示最新结果，而不包含其之前的任何信息。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于获取有关容器的最近统计信息的请求：

```
bluemix ic stats --no-stream my_container
```


### bluemix ic stop
{: #ic_stop}
停止正在运行的容器。有关更多信息，请参阅 Docker 帮助中的 [stop ](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。要启动容器，请参阅 [bluemix ic start](#ic_start) 命令。

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i>（可选）</dt>
   <dd>终止容器之前要等待的秒数。</dd>
   </dl>

<strong>响应</strong>：

- 已成功停止容器。

- 针对容器云服务的命令失败

 `{message}`

 其中，`{message}` 是相关错误。

- 命令失败 - 无法连接到容器云服务

<strong>示例</strong>：

以下示例显示用于停止名为 `proxy` 的容器的请求。

```
bluemix ic stop proxy
```


### bluemix ic top
{: #bluemix_ic_top}

显示正在容器中运行的进程。有关更多信息，请参阅 Docker 帮助中的 [top ](https://docs.docker.com/engine/reference/commandline/top/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于显示名为 `my_container` 的容器中进程的请求。

```
bluemix ic top my_container
```


### bluemix ic unpause
{: #unpause}

取消暂停正在运行的容器内的所有进程。有关更多信息，请参阅 Docker 帮助中的 [unpause ](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。要暂停容器，请参阅 [bluemix ic pause](#pause) 命令。

```
bluemix ic unpause CONTAINER
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   </dl>

<strong>响应</strong>：

- 已成功取消暂停容器。

- 针对容器云服务的命令失败

 `{message}`

 其中，`{message}` 是相关错误。

- 命令失败 - 无法连接到容器云服务

<strong>示例</strong>：

以下示例显示用于取消暂停名为 `proxy` 的容器的请求：

```
bluemix ic unpause proxy
```


### bluemix ic unprovision
{: #bluemix_ic_unprovision}

在登录的 Bluemix 空间中删除 IBM Containers 服务。

<strong>注意</strong>：运行此命令后，所有单个容器和容器组都会丢失。您的空间在 Bluemix 中仍可用。要再次开始使用 IBM Containers，您必须运行 `bluemix ic reprovision` 以再次供应 IBM Containers 服务。

```
bluemix ic reprovision [--force|-f] 
```
<strong>命令选项</strong>：

<dl>
   <dt>--force|-f（可选）</dt>
   <dd>强制从 Bluemix 空间删除 IBM Containers 服务。</dd>
 </dl>


### bluemix ic version
{: #bluemix_ic_version}

显示 Docker 和 IBM Containers API 的版本。

```
bluemix ic version
```

<strong>先决条件</strong>：Docker

要查看 IBM Containers 的版本，请运行 `bluemix ic info`。有关更多信息，请参阅 Docker 帮助中的 [version ](https://docs.docker.com/engine/reference/commandline/version/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。


### bluemix ic volume-create
{: #bluemix_ic_volume_create}

创建卷。

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>FS_NAME</i>（可选）</dt>
   <dd>文件共享名称。如果没有文件共享可用或者未指定文件共享，那么卷将在空间的缺省文件共享上进行构建。</dd>
   <dt><i>VOLUME_NAME</i>（必需）</dt>
   <dd>卷名称。名称可以包含小写字母、数字、下划线 _ 和连字符 -。</dd>
   </dl>


<strong>示例</strong>：

以下示例显示用于创建卷的请求。

```
bluemix ic volume-create volume_name fileshare_name
```


### bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

列出文件共享。

```
bluemix ic volume-fs
```


### bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

创建文件共享。

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>FILE_SHARE_NAME</i>（必需）</dt>
   <dd>文件共享名称。名称可以包含小写字母、数字、下划线 _ 和连字符 -。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于创建文件共享的请求。
```
bluemix ic volume-fs-create my_file_share
```


### bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

列出所有文件共享类型模板。

```
bluemix ic volume-fs-flavors
```

<strong>先决条件</strong>：端点、登录和目标


### bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

检查文件共享。

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

  <dl>
  <dt><i>FILE_SHARE_NAME</i>（必需）</dt>
   <dd>文件共享名称。</dd>
   </dl>

<strong>示例</strong>：

以下示例是用于检查文件共享的请求，其中 `my_file_share` 是文件共享的名称。
```
bluemix ic volume-fs-inspect my_file_share
```


### bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

除去文件共享。

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>FILE_SHARE_NAME</i>（必需）</dt>
   <dd>文件共享名称。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于除去文件共享的请求，其中 `my_file_share` 是文件共享的名称。

```
bluemix ic volume-fs-remove my_file_share
```


### bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

检查卷。

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>VOLUME_NAME</i>（必需）</dt>
   <dd>卷名称。</dd>
   </dl>

<strong>示例</strong>：

以下示例是用于检查卷的请求，其中 `volume_name` 是卷的名称。

```
bluemix ic volume-inspect volume_name
```


### bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

除去卷。

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>先决条件</strong>：端点、登录和目标

<strong>命令选项</strong>：

   <dl>
   <dt><i>VOLUME_NAME</i>（必需）</dt>
   <dd>卷名称。</dd>
    </dl>

<strong>示例</strong>：

以下示例显示用于除去卷的请求，其中 `volume_name` 是卷的名称。

```
bluemix ic volume-remove volume_name
```


### bluemix ic volumes
{: #bluemix_ic_volumes}

列出卷。

```
bluemix ic volumes
```

<strong>先决条件</strong>：端点、登录和目标


### bluemix ic wait
{: #bluemix_ic_wait}

退出容器并显示退出代码以作为确认。有关更多信息，请参阅 Docker 帮助中的 [wait ](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg) 命令。

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于退出名为 `my_container` 的容器的请求：

```
bluemix ic wait my_container
```


### bluemix ic wait-status
{: #bluemix_ic_wait_status}

等待单个容器或容器组达到非瞬时状态。在此等待时间内，命令行不会返回任何内容，您也无法输入命令。当容器达到非瞬时状态后，会立即显示 OK 消息。对于单个容器，非瞬时状态包括 Running、Shutdown、Crashed、Paused 或 Suspended。对于容器组，非瞬时状态包括 CREATE_COMPLETE、UPDATE_COMPLETE 或 FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>先决条件</strong>：端点、登录、目标和 Docker

<strong>命令选项</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必需）</dt>
   <dd>容器名称或标识。</dd>
   </dl>

<strong>示例</strong>：

以下示例显示用于退出名为 `my_container` 的容器的请求：

```
bluemix ic wait my_container
```



# 相关链接
{: #rellinks}

## 相关链接
{: #general}

* [bx tool ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg)
