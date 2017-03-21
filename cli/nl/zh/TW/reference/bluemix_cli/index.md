---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 {{site.data.keyword.Bluemix_notm}} CLI
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI 提供統一方式，可讓您使用指令行介面與應用程式、虛擬伺服器、容器以及其他服務互動。{{site.data.keyword.Bluemix_notm}} CLI 同時整合社群工具（例如 Cloud Foundry CLI、Docker CLI 及 OpenStack CLI），以及起始設定環境設定，讓您可以與不同的運算類型互動。

**限制**：Cygwin 不支援 {{site.data.keyword.Bluemix_notm}} CLI，因此請不要在 Cygwin 指令行視窗中使用 {{site.data.keyword.Bluemix_notm}} CLI。

**附註**：如果您的網路在執行 CLI 的主機與 {{site.data.keyword.Bluemix_notm}} 之間包含 HTTP Proxy 伺服器，則必須在 HTTP_PROXY 環境變數指定 Proxy 伺服器的主機名稱或 IP 位址。

## 安裝 {{site.data.keyword.Bluemix_notm}} CLI
{: #install_bluemix_cli}

安裝 {{site.data.keyword.Bluemix_notm}} CLI 之前，請安裝 [cf CLI ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}。

若為 Mac OS 及 Windows，請下載 [{{site.data.keyword.Bluemix_notm}} CLI 套件](/docs/cli/index.html#downloads)，然後執行安裝程式。

若為 Linux，請遵循下列步驟：

  1. 下載並解壓縮套件。例如：

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

  2. 移至 `Bluemix_CLI` 目錄，然後使用 root 許可權來執行 `./install_bluemix_cli` 指令。您可以使用 root 使用者身分執行此指令，或使用 `sudo` 指令來取得 root 許可權。例如：

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

您現在可以開始使用 {{site.data.keyword.Bluemix_notm}} CLI，或安裝其他外掛程式。

## 安裝外掛程式
{: #install_plug-in}

與 Cloud Foundry CLI 相似，{{site.data.keyword.Bluemix_notm}} CLI 支援外掛程式延伸架構以整合內建指令以外的其他指令。

若要從本端環境安裝外掛程式，請採取下列步驟：

  1. 下載外掛程式。例如：

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

  2. 對於 UNIX 型系統，您必須使用 `chmod` 指令，將下載的檔案設為可執行檔。例如：

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. 使用 `bluemix plugin install` 指令，以安裝外掛程式。例如：

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

若要從遠端伺服器安裝，請採取下列步驟：

  1. 使用 `bluemix plugin install` 指令，直接從遠端 URL 安裝外掛程式。例如：

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

您也可以從儲存庫安裝外掛程式。{{site.data.keyword.Bluemix_notm}} 的儲存庫可管理 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式及 Cloud Foundry CLI 外掛程式：

  * [Cloud Foundry CLI 外掛程式儲存庫 ](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg)，其管理 Cloud Foundry CLI 的外掛程式。
  * [{{site.data.keyword.Bluemix_notm}} CLI 外掛程式儲存庫 ](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg)，其管理 {{site.data.keyword.Bluemix_notm}} CLI 的專用外掛程式。

若要從儲存庫安裝，請採取下列步驟：

  1. 尋找儲存庫中的外掛程式。安裝 {{site.data.keyword.Bluemix_notm}} CLI 之後，預設會新增正式儲存庫 `Bluemix`。您可以使用 `bluemix plugin repo-plugins` 指令來列出 `Bluemix` 儲存庫中的外掛程式。例如：

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. 使用 `bluemix plugin install` 指令，從 `Bluemix` 儲存庫安裝外掛程式。例如：

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## 登入 {{site.data.keyword.Bluemix_notm}} CLI
{: #log_bmcli}

安裝 {{site.data.keyword.Bluemix_notm}} CLI 之後，即可使用 IBM ID 及密碼來登入 {{site.data.keyword.Bluemix_notm}}。例如：

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

您現在已準備好使用 {{site.data.keyword.Bluemix_notm}} 內建指令。例如，執行 `bluemix catalog templates` 指令來列出所有可用的 {{site.data.keyword.Bluemix_notm}} 樣板範本：

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

# {{site.data.keyword.Bluemix_notm}} (bx) 指令
{: #bluemix_cli}

版本：0.4.6

{{site.data.keyword.Bluemix_notm}} 指令行介面 (CLI) 提供一組依名稱空間分組的指令，讓使用者與 {{site.data.keyword.Bluemix_notm}} 互動。有些 {{site.data.keyword.Bluemix_notm}} 指令是現有 cf 指令的封套，有些則提供延伸功能供 {{site.data.keyword.Bluemix_notm}} 使用者使用。下列資訊列出 {{site.data.keyword.Bluemix_notm}} CLI 支援的指令，並包含其名稱、選項、用法、必要條件、說明及範例。
{:shortdesc}

**附註：***必要條件* 列出使用指令之前需要哪些動作。沒有必要動作的指令會列為**無**。否則，必要條件可能包括下列一個以上的動作：

<dl>
<dt>端點</dt>
<dd>必須透過 <code>bluemix api</code> 設定 API 端點後，才能使用此指令。</dd>
<dt>登入</dt>
<dd>需要使用 <code>bluemix login</code> 指令進行登入後，才能使用此指令。如果是使用聯合 ID 登入，請使用 '--sso' 選項以一次性密碼進行鑑別。</dd>
<dt>目標</dt>
<dd>必須使用 <code>bluemix target</code> 指令來設定組織及空間後，才能使用此指令。</dd>
<dt>Docker</dt>
<dd>必須先安裝 Docker CLI (Docker)，才能執行此指令。</dd>
</dl>

## bluemix 指令索引
{: #bx_commands_index}

請使用下表中的索引來參照常用的 bluemix 指令。

**附註：**您可以使用短格式的 bluemix 指令；例如，`bx api` 為 `bluemix api` 的短格式。


<table summary="一般 bluemix 指令。">
 <caption>表格 1. 一般 bluemix 指令</caption>
 <thead>
 <th colspan="5">一般 bluemix 指令</th>
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


<table summary="您可以用來管理組織、空間和使用者的 bluemix 指令。">
 <caption>表格 2. 用來管理組織、空間和使用者的指令</caption>
 <thead>
 <th colspan="5">用來管理組織、空間和使用者的指令</th>
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
 <td>[bluemix iam account-users
](index.html#bluemix_iam_account_users)</td>
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


<table summary="您可以用來管理 Cloud Foundry 應用程式的 bluemix 指令。">
 <caption>表格 3. 用來管理 cf 應用程式的指令</caption>
 <thead>
 <th colspan="5">用來管理 cf 應用程式的指令</th>
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


<table summary="您可以用來管理 Bluemix 服務的 bluemix 指令。">
 <caption>表格 4. 用來管理 Bluemix 服務的指令</caption>
 <thead>
 <th colspan="5">用來管理 Bluemix 服務的指令</th>
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


<table summary="您可以用來管理 Bluemix 型錄、外掛程式、帳單和安全設定的 bluemix 指令。">
 <caption>表格 5. 用來管理 Bluemix 型錄、外掛程式、帳單和安全設定的指令</caption>
 <thead>
 <th colspan="5">用來管理 Bluemix 型錄、外掛程式、帳單和安全設定的指令</th>
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


<table summary="您可以用來管理網路設定的 bluemix 指令。">
 <caption>表格 6. 用來管理網路設定的指令</caption>
 <thead>
 <th colspan="5">用來管理網路設定的指令</th>
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

<table summary="您可以用來在 Bluemix 上管理容器的 bluemix 指令。">
 <caption>表格 7. 用來在 Bluemix 上管理容器的指令</caption>
 <thead>
 <th colspan="5">用來在 Bluemix 上管理容器的指令</th>
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
顯示 {{site.data.keyword.Bluemix_notm}} CLI 之第一層內建指令及所支援名稱空間的一般說明，或特定內建指令或名稱空間的說明。

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：

   <dl>
   <dt>COMMAND|NAMESPACE（選用）</dt>
   <dd>顯示其說明的指令或名稱空間。如果未指定，則會顯示 {{site.data.keyword.Bluemix_notm}} CLI 的一般說明。</dd>
   </dl>



<strong>範例</strong>：

顯示 {{site.data.keyword.Bluemix_notm}} CLI 的一般說明：

```
bluemix help
```

顯示 `info` 指令的說明：

```
bluemix help info
```

顯示 `ic` 外掛程式的說明：

```
bluemix help ic
```

或

```
bluemix ic help
```

顯示 `ic` 外掛程式下 `group-create` 指令的說明：

```
bluemix ic help group-create
```


### bluemix api
{: #bluemix_api}
設定或檢視 {{site.data.keyword.Bluemix_notm}} API 端點。此指令會覆蓋 `cf api` 指令。

```
bluemix api [API_ENDPOINT] [--unset]
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：
   <dl>
   <dt>API_ENDPOINT（選用）</dt>
   <dd>設為目標的 API 端點，例如 `https://api.chinabluemix.net`。 如果未同時指定 *API_ENDPOINT* 及 `--unset` 選項，則會顯示現行 API 端點。</dd>
   <dt>--unset（選用）</dt>
   <dd>移除 API 端點設定。</dd>
    </dl>
<strong>範例</strong>：將 API 端點設為 api.chinabluemix.net：

```
bluemix api api.chinabluemix.net
```

檢視現行 API 端點：

```
bluemix api
```

取消設定 API 端點：

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

登入使用者。此指令會覆蓋 `cf login` 指令。指令選項與 `cf login` 指令選項相同。

```
bluemix login [OPTIONS...]
```

<strong>必要條件</strong>：端點

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>指令選項</strong>：如需 `login` 指令支援之選項的相關資訊，請參閱用於管理應用程式之 cf 指令的 `cf login` 指令用法資訊。

<strong>附註</strong>：如果是使用聯合 ID 登入，請使用 '--sso' 選項以一次性密碼進行鑑別。

### bluemix logout
{: #bluemix_logout}

登出使用者。此指令會覆蓋 `cf logout` 指令。

```
bluemix logout
```

<strong>必要條件</strong>：無


### bluemix target
{: #bluemix_target}


設定或檢視目標組織或空間。此指令會覆蓋 `cf target` 指令。

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>-o <i>ORG_NAME</i>（選用）</dt>
   <dd>要設為目標的組織名稱。</dd>
   <dt>-s <i>SPACE_NAME</i>（選用）</dt>
   <dd>要設為目標的空間名稱。</dd>
   </dl>
如果既未指定 -o *ORG_NAME* 也未指定 -s *SPACE_NAME*，則會顯示現行組織及空間。<strong>範例</strong>：將現行組織設為 `MyOrg`，並將空間設為 `MySpace`：

```
bluemix target -o MyOrg -s MySpace
```

檢視現行組織及空間：

```
bluemix target
```


### bluemix info
{: #bluemix_info}

檢視基本 {{site.data.keyword.Bluemix_notm}} 資訊，包括現行地區、雲端控制器版本以及部分有用端點（例如用於登入及交換存取記號的端點）。

```
bluemix info
```

<strong>必要條件</strong>：端點


### bluemix config
{: #bluemix_config}


將預設值寫入配置檔。

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：
   <dl>
   <dt>--http-timeout <i>TIMEOUT_IN_SECONDS</i></dt>
   <dd>用於 HTTP 要求的逾時值。預設值為 60 秒。</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>追蹤對終端機或指定檔案的 HTTP 要求。</dd>
   <dt>--color true|false</dt>
   <dd>啟用或停用顏色輸出。依預設，會啟用顏色輸出。</dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
   <dd>設定預設語言環境。如果 LOCALE 為 <i>CLEAR</i>，則會刪除先前的語言環境。</dd>
   <dt>--check-version true|false</dt>
   <dd>啟用或停用 CLI 版本檢查</dd>
   </dl>

一次只能指定其中一個選項。

<strong>範例</strong>：

將 HTTP 要求逾時值設為 30 秒：

```
bluemix config --http-timeout 30
```

啟用 HTTP 要求的追蹤輸出：

```
bluemix config --trace true
```

追蹤對指定檔案 */home/usera/my_trace* 的 HTTP 要求：

```
bluemix config --trace /home/usera/my_trace
```

停用顏色輸出：

```
bluemix config --color false
```

將語言環境設為 zh_Hans：

```
bluemix config --locale zh_Hans
```

清除語言環境設定：

```
bluemix config --locale CLEAR
```


### bluemix curl
{: #bluemix_curl}

對 {{site.data.keyword.Bluemix_notm}} 執行原始 HTTP 要求。依預設，*Content-Type* 會設為 *application/json*。此指令會將要求傳送至「{{site.data.keyword.Bluemix_notm}} 多雲端控制 Proxy」。如需支援的路徑，請參閱 [CloudFoundry API 文件 ](http://apidocs.cloudfoundry.org/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 中的 API 路徑定義。

```
bluemix curl PATH [OPTIONS...]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt><i>PATH</i>（必要）</dt>
   <dd>資源的 URL 路徑。例如，/v2/apps。</dd>
   <dt><i>OPTIONS</i>（選用）</dt>
   <dd>`bluemix curl` 指令所支援的選項與 `cf curl` 指令的選項相同。</dd>
   </dl>

<strong>範例</strong>：

檢視現行帳戶的所有組織的資訊：

```
bluemix curl /v2/organizations
```


### bluemix iam orgs
{: #bluemix_iam_orgs}

列出所有組織

```
bluemix iam orgs [-r REGION --guid]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>-r <i>REGION</i>（選用）</dt>
   <dd>顯示其組織資訊的地區。如果設為 'all'，則會列出所有地區中的所有組織。</dd>
   <dt>--guid（選用）</dt>
   <dd>顯示組織的 GUID。</dd>
   </dl>

<strong>範例</strong>：

列出 `us-south` 地區中的所有組織，並顯示 GUID

```
bluemix iam orgs -r us-south --guid
```

### bluemix iam org
{: #bluemix_iam_org}

顯示所指定組織的資訊。

```
bluemix iam org ORG_NAME [--guid]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>ORG_NAME（必要）</dt>
   <dd>組織的名稱。</dd>
   <dt>--guid（選用）</dt>
   <dd>顯示組織的 GUID。</dd>
   </dl>

<strong>範例</strong>：

顯示 `IBM` 組織的資訊，並顯示 GUID

```
bluemix iam org IBM --guid
```

### bluemix iam org-create
{: #bluemix_iam_org_create}

建立新的組織。只有帳戶擁有者才能執行此作業。

```
bluemix iam org-create ORG_NAME
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>ORG_NAME（必要）</dt>
   <dd>所要建立之組織的名稱。</dd>
   </dl>

<strong>範例</strong>：

建立名稱為 `IBM` 的組織。

```
bluemix iam org-create IBM
```


### bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

將組織從現行地區抄寫到另一個地區。

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>ORG_NAME（必要）</dt>
   <dd>要抄寫之現有組織的名稱。</dd>
   <dt>REGION_NAME（必要）</dt>
   <dd>管理所抄寫組織的地區名稱。</dd>
   </dl>

<strong>範例</strong>：

將組織 `myorg` 抄寫到地區 `eu-gb`：

```
bluemix iam org-replicate myorg eu-gb
```


### bluemix iam org-rename
{: #bluemix_iam_org_rename}

重新命名組織。只有組織管理員才能執行此作業。

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>OLD_ORG_NAME（必要）</dt>
   <dd>要重新命名之組織的舊名稱。</dd>
   <dt>NEW_ORG_NAME（必要）</dt>
   <dd>組織重新命名後的新名稱。</dd>
   </dl>

### bluemix iam org-delete
{: #bluemix_iam_org_delete}

刪除現行地區中的指定組織。

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>ORG_NAME（必要）</dt>
   <dd>要刪除之現有組織的名稱。</dd>
   <dt>-f（選用）</dt>
   <dd>強制刪除，而不確認。</dd>
   <dt>--all（選用）</dt>
   <dd>刪除所有地區中的組織。</dd>
   </dl>


### bluemix iam spaces
{: #bluemix_iam_spaces}

此指令的函數及選項與 `cf spaces` 指令相同。


### bluemix iam space
{: #bluemix_iam_space}

此指令的函數及選項與 `cf space` 指令相同。


### bluemix iam space-create
{: #bluemix_iam_space_create}

此指令的函數及選項與 `cf create-space` 指令相同。


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


此指令的函數及選項與 `cf rename-space` 指令相同。


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


此指令的函數及選項與 `cf delete-space` 指令相同。


### bluemix iam account-users
{: #bluemix_iam_account_users}

顯示與帳戶相關聯的使用者。只有帳戶擁有者才能執行此作業。

```
bluemix iam account-users
```

### bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}


邀請使用者加入已設定組織和空間角色的帳戶。只有帳戶擁有者才能執行此作業。

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>必要條件</strong>：端點、登入


<strong>指令選項</strong>：

   <dl>
   <dt>USER_NAME（必要）</dt>
   <dd>所邀請之使用者的名稱。</dd>
   <dt>ORG_NAME（必要）</dt>
   <dd>邀請此使用者加入之組織的名稱。</dd>
   <dt>ORG_ROLE（必要）</dt>
   <dd>邀請此使用者加入之組織角色的名稱。例如：
   <ul>
  <li>OrgManager：此角色可以邀請和管理使用者、選取和變更方案，以及設定消費限制。</li>
  <li>BillingManager：此角色可以建立和管理計費帳戶及付款資訊。</li>
  <li>OrgAuditor：此角色具有組織資訊和報告的唯讀權。</li>
  </ul> </dd>
   <dt>SPACE_NAME（必要）</dt>
   <dd>邀請此使用者加入之空間的名稱。</dd>
   <dt>SPACE_ROLE（必要）</dt>
   <dd>邀請此使用者加入之空間的名稱。邀請此使用者加入之空間角色的名稱。例如：
   <ul>
<li>SpaceManager：此角色可以邀請和管理使用者，以及啟用給定空間的特性。</li>
<li>SpaceDeveloper：此角色可以建立和管理應用程式及服務，以及查看日誌和報告。</li>
<li>SpaceAuditor：此角色可以檢視空間的日誌、報告和設定。</li>
</ul>
</dd>
</dl>

<strong>範例</strong>：

以 `OrgManager` 角色，邀請使用者 `Mary` 加入組織 `IBM`，以及以 `SpaceAuditor` 角色加入空間 `Cloud`：

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

重新傳送邀請給使用者（需要組織管理員或帳戶擁有者）
```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```


### bluemix iam org-users
{: #bluemix_iam_org_users}

依角色顯示指定組織中的使用者。

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>ORG_NAME（必要）</dt>
   <dd>組織的名稱。</dd>
   <dt>-a（選用）</dt>
   <dd>列出指定組織中的所有使用者，而不依角色分組。</dd>
    </dl>

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

將使用者新增到組織（需要組織管理員）。
```
 bluemix iam org-user-add USER_NAME ORG
```

### bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

從組織移除使用者（僅限組織管理員或使用者自己）
```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>指令選項</strong>：
  <dl>
   <dt>--force、-f</dt>
   <dd>強制刪除，而不確認。</dd>
 </dl>

### bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

將組織角色指派給使用者。只有組織管理員才能執行此作業。

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
  <dl>
   <dt>USER_NAME（必要）</dt>
   <dd>所指派之使用者的名稱。</dd>
   <dt>ORG_NAME（必要）</dt>
   <dd>獲指派此使用者之組織的名稱。</dd>
   <dt>ORG_ROLE（必要）</dt>
   <dd>獲指派此使用者之組織角色的名稱。例如：
   <ul>
   <li>OrgManager：此角色可以邀請和管理使用者、選取和變更方案，以及設定消費限制。</li>
   <li>BillingManager：此角色可以建立和管理計費帳戶及付款資訊。</li>
   <li>OrgAuditor：此角色具有組織資訊和報告的唯讀權。</li>
   </ul>
   </dd>
    </dl>

<strong>範例</strong>：

以 `OrgManager` 角色，將使用者 `Mary` 指派給組織 `IBM`：

```
bluemix iam org-role-set Mary IBM OrgManager
```


### bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

移除使用者的組織角色。只有組織管理員才能執行此作業。

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>USER_NAME（必要）</dt>
   <dd>所要移除之使用者的名稱。</dd>
   <dt>ORG_NAME（必要）</dt>
   <dd>從中移除此使用者之組織的名稱。</dd>
   <dt>ORG_ROLE（必要）</dt>
   <dd>從中移除此使用者之組織角色的名稱。例如：
   <ul>
   <li>OrgManager：此角色可以邀請和管理使用者、選取和變更方案，以及設定消費限制。</li>
   <li>BillingManager：此角色可以建立和管理計費帳戶及付款資訊。</li>
   <li>OrgAuditor：此角色具有組織資訊和報告的唯讀權。</li>
   </ul>
   </dd>
    </dl>

<strong>範例</strong>：

以 `OrgManager` 角色，從組織 `IBM` 移除使用者 `Mary`：

```
bluemix iam org-role-unset Mary IBM OrgManager
```


### bluemix iam space-users
{: #bluemix_iam_space_users}

依角色顯示指定空間中的使用者。

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>ORG_NAME（必要）</dt>
   <dd>組織的名稱。</dd>
   <dt>SPACE_NAME（必要）</dt>
   <dd>空間的名稱。</dd>
   </dl>


### bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

將空間角色指派給使用者。只有空間管理員才能執行此作業。

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：

   <dl>
   <dt>USER_NAME（必要）</dt>
   <dd>所指派之使用者的名稱。</dd>
   <dt>ORG_NAME（必要）</dt>
   <dd>獲指派此使用者之組織的名稱。</dd>
   <dt>SPACE_NAME（必要）</dt>
   <dd>獲指派此使用者之空間的名稱。</dd>
   <dt>SPACE_ROLE（必要）</dt>
   <dd>獲指派此使用者之空間角色的名稱。例如：
   <ul>
   <li>SpaceManager：此角色可以邀請和管理使用者，以及啟用給定空間的特性。</li>
   <li>SpaceDeveloper：此角色可以建立和管理應用程式及服務，以及查看日誌和報告。</li>
   <li>SpaceAuditor：此角色可以檢視空間的日誌、報告和設定。</li>
   </ul></dd>
    </dl>

<strong>範例</strong>：

以 `SpaceManager` 角色，將使用者 `Mary` 指派給組織 `IBM` 和空間 `Cloud`：

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

### bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

移除使用者的空間角色。只有空間管理員才能執行此作業。

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：

   <dl>
   <dt>USER_NAME（必要）</dt>
   <dd>所要移除之使用者的名稱。</dd>
   <dt>ORG_NAME（必要）</dt>
   <dd>從中移除此使用者之組織的名稱。</dd>
   <dt>SPACE_NAME（必要）</dt>
   <dd>從中移除此使用者之空間的名稱。</dd>
   <dt>SPACE_ROLE（必要）</dt>
   <dd>從中移除此使用者之空間角色的名稱。例如：
   <ul>
   <li>SpaceManager：此角色可以邀請和管理使用者，以及啟用給定空間的特性。</li>
   <li>SpaceDeveloper：此角色可以建立和管理應用程式及服務，以及查看日誌和報告。</li>
   <li>SpaceAuditor：此角色可以檢視空間的日誌、報告和設定。</li>
   </ul></dd>
    </dl>


<strong>範例</strong>：

以 `SpaceManager` 角色，從組織 `IBM` 和空間 `Cloud` 移除使用者 `Mary`：

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


### bluemix app push
{: #bluemix_app_push}

此指令的函數及選項與 `cf push` 指令相同。


### bluemix app list
{: #bluemix_app_list}

此指令的函數及選項與 `cf apps` 指令相同。


### bluemix app show
{: #bluemix_app_show}

此指令的函數及選項與 `cf app` 指令相同。


### bluemix app scale
{: #bluemix_app_scale}

此指令的函數及選項與 `cf scale` 指令相同。


### bluemix app delete
{: #bluemix_app_delete}

此指令的函數及選項與 `cf delete` 指令相同。


### bluemix app rename
{: #bluemix_app_rename}

此指令的函數及選項與 `cf rename` 指令相同。


### bluemix app start
{: #bluemix_app_start}

此指令的函數及選項與 `cf start` 指令相同。


### bluemix app stop
{: #bluemix_app_stop}

此指令的函數及選項與 `cf stop` 指令相同。


### bluemix app restart
{: #bluemix_app_restart}

此指令的函數及選項與 `cf restart` 指令相同。


### bluemix app restage
{: #bluemix_app_restage}


此指令的函數及選項與 `cf restage` 指令相同。


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


此指令的函數及選項與 `cf restart-app-instance` 指令相同。


### bluemix app events
{: #bluemix_app_events}

此指令的函數及選項與 `cf events` 指令相同。


### bluemix app files
{: #bluemix_app_files}

此指令的函數及選項與 `cf files` 指令相同。


### bluemix app logs
{: #bluemix_app_logs}

此指令的函數及選項與 `cf logs` 指令相同。


### bluemix app env
{: #bluemix_app_env}

此指令的函數及選項與 `cf env` 指令相同。


### bluemix app env-set
{: #bluemix_app_env_set}

此指令的函數及選項與 `cf set-env` 指令相同。


### bluemix app env-unset
{: #bluemix_app_env_unset}

此指令的函數及選項與 `cf unset-env` 指令相同。


### bluemix app stacks
{: #bluemix_app_stacks}

此指令的函數及選項與 `cf stacks` 指令相同。


### bluemix app stack
{: #bluemix_app_stack}

此指令的函數及選項與 `cf stack` 指令相同。


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

此指令的函數及選項與 `cf create-app-manifest` 指令相同。


### bluemix service offerings
{: #bluemix_service_offerings}


此指令的函數及選項與 `cf marketplace` 指令相同。


### bluemix service list
{: #bluemix_service_list}

此指令的函數及選項與 `cf services` 指令相同。


### bluemix service show
{: #bluemix_service_show}

此指令的函數及選項與 `cf service` 指令相同。


### bluemix service create
{: #bluemix_service_create}

此指令的函數及選項與 `cf create-service` 指令相同。


### bluemix service update
{: #bluemix_service_update}

此指令的函數及選項與 `cf update-service` 指令相同。


### bluemix service delete
{: #bluemix_service_delete}

此指令的函數及選項與 `cf delete-service` 指令相同。


### bluemix service rename
{: #bluemix_service_rename}

此指令的函數及選項與 `cf rename-service` 指令相同。


### bluemix service bind
{: #bluemix_service_bind}

此指令的函數及選項與 `cf bind-service` 指令相同。


### bluemix service unbind
{: #bluemix_service_unbind}

此指令的函數及選項與 `cf unbind-service` 指令相同。


### bluemix service key-create
{: #bluemix_service_key_create}

此指令的函數及選項與 `cf create-service-key` 指令相同。


### bluemix service key-delete
{: #bluemix_service_key_delete}

此指令的函數及選項與 `cf delete-service-key` 指令相同。


### bluemix service keys
{: #bluemix_service_keys}

此指令的函數及選項與 `cf service-keys` 指令相同。


### bluemix service key-show
{: #bluemix_service_key_show}

此指令的函數及選項與 `cf service-key` 指令相同。


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

此指令的函數及選項與 `cf create-user-provided-service` 指令相同。


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

此指令的函數及選項與 `cf update-user-provided-service` 指令相同。


### bluemix catalog templates
{: #bluemix_catalog_templates}

檢視 Bluemix 上的樣板範本。

```
bluemix catalog templates [-d]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：

   <dl>
   <dt>-d（選用）</dt>
   <dd>如果指定 <i>-d</i> 選項，也會顯示每個範本的說明。否則，只會顯示每一個範本的 ID 及名稱。</dd>
   </dl>


### bluemix catalog template
{: #bluemix_catalog_template}

檢視所指定樣板範本的詳細資訊。

```
bluemix catalog template TEMPLATE_ID
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>TEMPLATE_ID（必要）</dt>
   <dd>樣板範本的 ID。請使用 <i>bluemix templates</i> 來檢視所有範本的 ID。</dd>
   </dl>


<strong>範例</strong>：

檢視範本 `mobileBackendStarter` 的詳細資料：

```
bluemix catalog template mobileBackendStarter
```


### bluemix catalog template-run
{: #bluemix_catalog_template_run}

以指定的 URL 及說明，建立根據所指定範本的 cf 應用程式。依預設，新的應用程式會自動啟動。

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
   <dl>
   <dt>TEMPLATE_ID（必要）</dt>
   <dd>應用程式在建立時將根據的範本。使用 <i>bluemix templates</i> 來查看所有範本 ID。</dd>
   <dt>CF_APP_NAME（必要）</dt>
   <dd>要建立之 cf 應用程式的名稱。</dd>
   <dt>-u <i>URL</i>（選用）</dt>
   <dd>應用程式的路徑。如果未指定，Bluemix 會自動根據應用程式名稱及預設網域來設定路徑。</dd>
   <dt>-d <i>DESCRIPTION</i>（選用）</dt>
   <dd>應用程式的說明。</dd>
   <dt>--no-start（選用）</dt>
   <dd>建立應用程式之後，不要自動將它啟動。如果未指定，應用程式會在建立之後自動啟動。</dd>
   </dl>


<strong>範例</strong>：

根據 `javaHelloWorld` 範本建立 cf 應用程式 `my-app`：

```
bluemix catalog template-run javaHelloWorld my-app
```

根據 `rubyHelloWorld` 範本建立應用程式 `my-ruby-app`，路徑為 `myrubyapp.chinabluemix.net`，說明為 `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`：

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

根據 `pythonHelloWorld` 範本建立應用程式 `my-python-app`，不自動啟動：

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


### bluemix network regions
{: #bluemix_network_regions}

檢視 {{site.data.keyword.Bluemix_notm}} 上所有地區的資訊。

```
bluemix network regions
```

<strong>必要條件</strong>：端點


### bluemix network region-set
{: #bluemix_network_region_set}

切換至指定的地區。此指令會自動將目標重設為新地區中相同的組織及空間（可能的話）。否則，指令會提示使用者選取新的組織及空間（如果使用者已登入的話）。API 端點會相應地變更。

```
bluemix network region-set REGION_NAME
```

<strong>必要條件</strong>：端點

<strong>指令選項</strong>：

   <dl>
   <dt>REGION_NAME（必要）</dt>
   <dd>您要切換至的地區名稱。您可以使用 <i>bluemix network regions</i> 指令來查看所有地區名稱。</dd>
    </dl>

<strong>範例</strong>：

將現行地區設為 `eu-gb`：

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

此指令的函數及選項與 `cf routes` 指令相同。


### bluemix network route-check
{: #bluemix_network_route_check}

此指令的函數及選項與 `cf check-route` 指令相同。


### bluemix network route-map
{: #bluemix_network_route_map}

將路徑對映至具有所指定網域及主機名稱的現有 cf 應用程式或容器群組。

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME（必要）</dt>
   <dd>要與路徑對映之 cf 應用程式或容器群組的名稱。</dd>
   <dt>DOMAIN（必要）</dt>
   <dd>路徑的網域。例如，mychinabluemix.net 或 chinabluemix.net。</dd>
   <dt>-n <i>HOST_NAME</i>（選用）</dt>
   <dd>路徑的主機名稱。如果未提供，則依預設會將主機名稱設為應用程式名稱或容器群組名稱。</dd>
   </dl>

<strong>範例</strong>：

使用指定的網域將路徑對映到 `my-app`：

```
bluemix network route-map my-app mychinabluemix.net
```

以指定的網域及主機名稱對映將路徑對映至 'my-container-group'：

```
bluemix network route-map my-container-group chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

從現有的 cf 應用程式或容器群組中取消對映指定的路徑。

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME（必要）</dt>
   <dd>cf 應用程式或容器群組的名稱。</dd>
   <dt>DOMAIN（必要）</dt>
   <dd>路徑的網域（例如 mychinabluemix.net 或 chinabluemix.net）。</dd>
   <dt>-n <i>HOST_NAME</i>（選用）</dt>
   <dd>路徑的主機名稱。如果未提供，則依預設會將主機名稱設為應用程式名稱或容器群組名稱。</dd>
   </dl>

<strong>範例</strong>：

從 `my-app` 取消對映 `my-app.mychinabluemix.net`：

```
bluemix network route-unmap my-app mychianbluemix.net
```

從 `my-container-group` 取消對映 `abc.chinabluexmix.net`：

```
bluemix network route-unmap my-container-group chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

此指令的函數及選項與 `cf create-route` 指令相同。


### bluemix network route-delete
{: #bluemix_network_route_delete}

此指令的函數及選項與 `cf delete-route` 指令相同。


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

此指令的函數及選項與 `cf delete-orphaned-routes` 指令相同。


### bluemix network domains
{: #bluemix_network_domains}

此指令的函數及選項與 `cf domains` 指令相同。


### bluemix network domain-create
{: #bluemix_network_domain_create}

此指令的函數及選項與 `cf create-domain` 指令相同。


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

此指令的函數及選項與 `cf delete-domain` 指令相同。


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

此指令的函數及選項與 `cf create-shared-domain` 指令相同。


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

此指令的函數及選項與 `cf delete-shared-domain` 指令相同。



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

顯示帳戶的每月用量和費用。

```
bluemix bss account-usage [-d YYYY-MM] [--json]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：

<dl>
  <dt>-d MONTH_DATE（選用）</dt>
  <dd>顯示以 YYYY-MM 格式指定之月份和日期的資料。如果未指定，則會顯示現行月份的用量。</dd>
  <dt>--json（選用）</dt>
  <dd>以 JSON 格式顯示用量結果。</dd>
</dl>

<strong>範例</strong>：

顯示我的帳戶在 2016-06 的用量和費用報告：

```
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

顯示組織的每月用量詳細資料。只有組織的帳單管理員可以執行此作業。

```
bluemix bss org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：

<dl>
  <dt>ORG_NAME（必要）</dt>
  <dd>組織的名稱。</dd>
  <dt>-d MONTH_DATE（選用）</dt>
  <dd>顯示以 YYYY-MM 格式指定之月份和日期的資料。如果未指定，則會顯示現行月份的用量。</dd>
  <dt>-r REGION_NAME</dt>
  <dd>管理組織的地區名稱。如果設為 'all'，則會顯示組織在所有地區的用量。</dd>
  <dt>--json（選用）</dt>
  <dd>以 JSON 格式顯示用量結果。</dd>
</dl>



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

顯示我的帳戶中組織的每月用量摘要。

```
bluemix bss orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：

<dl>
  <dt>-d MONTH_DATE（選用）</dt>
  <dd>顯示以 YYYY-MM 格式指定之月份和日期的資料。如果未指定，則會顯示現行月份的用量。</dd>
  <dt>-r REGION_NAME</dt>
  <dd>管理組織的地區名稱。如果設為 'all'，則會顯示組織在所有地區的用量摘要。</dd>
  <dt>--json（選用）</dt>
  <dd>以 JSON 格式顯示用量結果。</dd>
</dl>



### bluemix security cert
{: #bluemix_security_cert}

列出網域的憑證資訊。

```
bluemix security cert DOMAIN_NAME
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：

   <dl>
   <dt>DOMAIN_NAME（必要）</dt>
   <dd>管理憑證的網域。</dd>
   </dl>



<strong>範例</strong>：

檢視網域 `ibmcxo-eventconnect.com` 的憑證資訊：

```
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

將憑證新增到現行組織中的指定網域。

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
   <dl>
   <dt>DOMAIN（必要）</dt>
   <dd>要新增憑證的網域。</dd>
   <dt>-k <i>PRIVATE_KEY_FILE</i>（必要）</dt>
   <dd>私密金鑰檔案路徑。</dd>
   <dt>-c <i>CERT_FILE</i>（必要）</dt>
   <dd>憑證檔案路徑。</dd>
   <dt>-p <i>PASSWORD</i>（選用）</dt>
   <dd>憑證的密碼。</dd>
   <dt>-i <i>INTERMEDIATE_CERT_FILE</i>（選用）</dt>
   <dd>中繼憑證檔案路徑。</dd>
   <dt>--verify-client（選用）</dt>
   <dd>是否啟用用戶端憑證驗證。</dd>
   </dl>


<strong>範例</strong>：

將憑證新增到網域 `ibmcxo-eventconnect.com`：

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

從現行組織中的指定網域移除憑證。

```
bluemix security cert-remove DOMAIN [-f]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>DOMAIN（必要）</dt>
   <dd>要從中移除憑證的網域。</dd>
   <dt>-f（選用）</dt>
   <dd>強制刪除，而不確認。</dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中登錄的所有外掛程式儲存庫。

```
bluemix plugin repos
```

<strong>必要條件</strong>：無


### bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

將新的外掛程式儲存庫新增至 {{site.data.keyword.Bluemix_notm}} CLI。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：

   <dl>
   <dt>REPO_NAME（必要）</dt>
   <dd>要新增之儲存庫的名稱。您可以自行為每一個儲存庫定義名稱。</dd>
   <dt>REPO_URL（必要）</dt>
   <dd>要新增之儲存庫的 URL。儲存庫 URL 必須包含通訊協定（例如，http://plugins.ng.bluemix.net 而非 plugins.ng.bluemix.net）。http://plugins.ng.bluemix.net 是 Bluemix CLI 的正式外掛程式儲存庫。</dd>
    </dl>


<strong>範例</strong>：

將 Bluemix CLI 的官方外掛程式儲存庫新增為 `bluemix-repo`：

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


### bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

從 {{site.data.keyword.Bluemix_notm}} CLI 移除外掛程式儲存庫。

```
bluemix plugin repo-remove REPO_NAME
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：
   <dl>
   <dt>REPO_NAME（必要）</dt>
   <dd>要移除之儲存庫的名稱。</dd>
   </dl>

<strong>範例</strong>：

從 {{site.data.keyword.Bluemix_notm}} CLI 移除 `bluemix-repo` 儲存庫：

```
bluemix plugin repo-remove bluemix-repo
```


### bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

列出所有已新增之儲存庫或特定儲存庫中所有可用的外掛程式。

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：

   <dl>
   <dt>-r <i>REPO_NAME</i>（選用）</dt>
   <dd>只列出指定儲存庫中的外掛程式。</dd>
   </dl>

<strong>範例</strong>：

列出所有已新增之儲存庫中的所有外掛程式：

```
bluemix plugin repo-plugins
```

列出 `bluemix-repo` 儲存庫中的所有外掛程式：

```
bluemix plugin repo-plugins -r bluemix-repo
```


### bluemix plugin list
{: #bluemix_plugin_list}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中的所有已安裝外掛程式。

```
bluemix plugin list
```

<strong>必要條件</strong>：無


### bluemix plugin install
{: #bluemix_plugin_install}

從指定的路徑或儲存庫將特定版本的外掛程式安裝到 {{site.data.keyword.Bluemix_notm}} CLI 中。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME（必要）</dt>
   <dd>如果未指定 -r <i>REPO_NAME</i>，則會從指定的本端路徑或遠端 URL 來安裝外掛程式。</dd>
   <dt>-r <i>REPO_NAME</i>（選用）</dt>
   <dd>外掛程式二進位檔所在儲存庫的名稱。</dd>
   <dt>-v <i>VERSION</i>（選用）</dt>
   <dd>要安裝之外掛程式的版本。如果未提供，將安裝外掛程式的最新版本。只有從儲存庫安裝外掛程式時，此選項才有效。</dd>
    </dl>

<strong>範例</strong>：

從本端檔案安裝外掛程式：

```
bluemix plugin install /downloads/new_plugin
```

從遠端 URL 安裝外掛程式：

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

從 `bluemix-repo` 儲存庫安裝最新版本的 `IBM-Containers` 外掛程式：

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
從 `bluemix-repo` 儲存庫安裝版本為 `0.5.800` 的 `IBM-Containers` 外掛程式：
```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```






### bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

從 {{site.data.keyword.Bluemix_notm}} CLI 解除安裝指定的外掛程式。

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：

   <dl>
   <dt>PLUGIN_NAME（必要）</dt>
   <dd>要解除安裝之外掛程式的名稱。</dd>
    </dl>

<strong>範例</strong>：

解除安裝先前安裝的 `IBM-Containers` 外掛程式：

```
bluemix plugin uninstall IBM-Containers
```


### bluemix ic attach
{: #bluemix_ic_attach}

控制執行中容器，或檢視其輸出。使用 `CTRL+C` 以結束並停止容器。此指令會呼叫 Docker CLI。如需相關資訊，請參閱 Docker 說明中的 [attach ](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>--no-stdin（選用）</dt>
   <dd>不要包含標準輸入。</dd>
   <dt>--sig-proxy（選用）</dt>
   <dd>將所有接收到的信號 Proxy 到處理程序。預設值為 <i>true</i>。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
    </dl>

<strong>範例</strong>：

下列範例顯示連接至容器 `my_container` 的要求：

```
bluemix ic attach my_container
```


### bluemix ic build
{: #bluemix_ic_build}

呼叫 IBM Containers 建置服務，以在本端或專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中建置 Docker 映像檔。此指令會呼叫 Docker CLI。如需相關資訊，請參閱 Docker 說明中的 [build ](https://docs.docker.com/engine/reference/commandline/build/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i>（必要）</dt>
   <dd>要套用至所建立映像檔的儲存庫名稱。</dd>
   <dt>--no-cache（選用）</dt>
   <dd>建置映像檔時不要使用快取。預設值為 <i>false</i>。</dd>
   <dt>--pull（選用）</dt>
   <dd>嘗試從登錄中取回基礎映像檔，即使已快取也一樣。</dd>
   <dt>-q|--quiet（選用）</dt>
   <dd>抑制容器所產生的詳細輸出。預設值為 <i>false</i>。</dd>
   <dt><i>DOCKERFILE_LOCATION</i>（必要）</dt>
   <dd>本端主機上 Dockerfile 及環境定義的路徑。</dd>
    </dl>

<strong>範例</strong>：

下列範例顯示建置名稱為 *myimage* 之映像檔的要求。Dockerfile 及其他要在建置中使用的構件，位於執行指令的同一目錄中。因為登錄及名稱空間隨附於映像檔名稱，所以映像檔會建置在您組織的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中。

```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


### bluemix ic cp
{: #bluemix_ic_cp}
在容器與本端檔案系統之間複製檔案或資料夾。此指令會呼叫 Docker CLI。如需相關資訊，請參閱 Docker 說明中的 [cp ](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。


### bluemix ic cpi
{: #bluemix_ic_cpi}

存取「Docker 中心」映像檔或本端登錄中的映像檔，並將映像檔複製到您的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫。

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
   <dl>
   <dt><i>SOURCE_IMAGE</i>（必要）</dt>
   <dd>來源儲存庫及映像檔名稱。</dd>
   <dt><i>DESTINATION_IMAGE</i>（必要）</dt>
   <dd>專用 {{site.data.keyword.Bluemix_notm}} 儲存庫 URL（包含名稱空間及目的地映像檔名稱）。映像檔的標記是選用性的。</dd>
   </dl>

<strong>範例</strong>：

將映像檔從來源儲存庫複製到專用儲存庫，並新增映像檔的標記：

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

將 `sinatra` 映像檔從 `training` 儲存庫複製到專用儲存庫 `registry.ng.bluemix.net/mynamespace`，並將映像檔命名為 `mysinatra`。請新增映像檔 `mysinatra` 的標記 `v1`。

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


### bluemix ic exec
{: #bluemix_ic_exec}

在容器內執行指令。如需相關資訊，請參閱 Docker 說明中的 [exec ](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-d|--detach（選用）</dt>
   <dd>在背景中執行指定的指令。</dd>
   <dt>-it（選用）</dt>
   <dd>互動模式。請持續顯示標準輸入。鍵入 <i>exit</i> 以結束。</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i>（選用）</dt>
   <dd>使用者名稱。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   <dt><i>CMD</i>（選用）</dt>
   <dd>要在一或數個指定容器內執行的指令。</dd>
   </dl>

<strong>範例</strong>：

以互動模式，執行 `my_container` 容器內的 `bash` 指令：

```
bluemix ic exec -it my_container bash
```

執行 `my_container` 容器內的 `date` 指令：

```
bluemix ic exec my_container date
```


### bluemix ic group-create
{: #bluemix_ic_group_create}

建立可擴充容器群組。

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRONMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
   <dl>
    <dt><i>IMAGE_NAME</i>（必要）</dt>
   <dd>要包含在容器群組中之每個容器實例的映像檔。您可以在映像檔之後列出指令，但不能在映像檔之後放置任何選項。請在指定映像檔之前併入所有選項。<br><br>如果您使用組織專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中的映像檔，請以下列格式指定映像檔：<i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>。<br><br>如果您使用 IBM Containers 所提供的映像檔，請不要併入您組織的名稱空間。請以下列格式指定映像檔：<i>registry.ng.bluemix.net/IMAGE</i>。</dd>
   <dt>--name <i>GROUP_NAME</i>（必要）</dt>
   <dd>將名稱指派給群組。<i>-n</i> 已淘汰。<br>
   <strong>提示：</strong>容器名稱必須以字母開頭。名稱可以包含大寫字母、小寫字母、數字、句點 .、底線 _ 或連字號 -。</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i>（選用）</dt>
   <dd>將記憶體限制指派給群組 (MB)。從 CLI 建立容器群組時，每一個容器實例的預設值都是 <i>64</i> MB。從 {{site.data.keyword.Bluemix_notm}}「儀表板」建立容器群組時，每一個容器實例的預設值都是 <i>256</i> MB。接受值是 <i>64</i>、<i>256</i>、<i>512</i>、<i>1024</i> 及 <i>2048</i>。指派記憶體限制之後，即無法變更其值。</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i>（選用）</dt>
   <dd>主機名稱，例如 <i>mycontainerhost</i>。主機與網域會結合，以構成完整公用路徑 URL，例如 <i>http://mycontainerhost.mybluemix.net</i>。在使用 <i>bluemix ic group-inspect</i> 指令檢閱容器群組的詳細資料時，主機與網域會一起列出，作為路徑。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>（選用）</dt>
   <dd>通常網域為 <i>.mybluemix.net</i>。主機與網域會結合，以構成完整公用路徑 URL，例如 <i>http://mycontainerhost.mybluemix.net</i>。在使用 <i>bluemix ic group-inspect</i> 指令檢閱容器群組的詳細資料時，主機與網域會一起列出，作為路徑。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i>（選用）</dt>
   <dd>設定環境變數。個別列出多個索引鍵。如果包含引號，請用它們括住環境變數名稱及值。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。下表顯示一些您可以指定的常用環境變數：</dd>
    </dl>


|  環境變數                              |     說明                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 將服務連結至容器。請使用 `CCS_BIND_APP` 環境變數，將應用程式連結至容器。應用程式會連結至目標服務，並作為橋接器，以容許 {{site.data.keyword.Bluemix_notm}} 將您橋接應用程式的 `VCAP_SERVICES` 資訊帶入執行中容器實例。|
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 若要將 Bluemix 服務直接連結至容器，而不使用橋接應用程式，請使用 CCS_BIND_SRV。此連結容許 Bluemix 將 VCAP_SERVICES 資訊注入執行中容器實例。若要列出多個 Bluemix 服務，請將它們併入為相同環境變數的一部分。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 新增要在容器中監視的日誌檔。包括含有日誌檔路徑的 `LOG_LOCATIONS` 環境變數。 |
{: caption="表 8. 常用環境變數" caption-side="top"}


 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i>（選用）</dt>
   <dd> 從檔案匯入環境變數，其中 ENVFILE 是本端目錄上檔案的路徑。檔案中的每一行都代表一個 key=value 配對。</dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro]（選用）</dt>
   <dd>以 <i>VolumeId:ContainerPath[:ro]</i> 格式指定詳細資料，將磁區連接至容器。
   <ul>
   <li><i>VOLUME</i>：磁區 ID 或名稱。</li>
   <li><i>CONTAINER_PATH</i>：容器中磁區的絕對路徑。</li>
   <li>ro：選用。指定 <i>ro</i> 會使磁區變成唯讀，而不是預設的讀寫。</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>（選用）</dt>
   <dd>公開 HTTP 資料流量的埠。群組中的容器必須接聽 HTTP 埠。無法提出 HTTPS 要求。若為容器群組，您無法包含多個埠。<br><br>在您指定埠時，即將應用程式設為可供「{{site.data.keyword.Bluemix_notm}} 負載平衡器」或相同 {{site.data.keyword.Bluemix_notm}} 空間中嘗試連接主機的容器使用。然後，{{site.data.keyword.Bluemix_notm}} 負載平衡器或容器可以使用此埠來連接相同 {{site.data.keyword.Bluemix_notm}} 空間中的主機和應用程式。如果在 Dockerfile 中針對您要使用的映像檔指定了埠，請包含該埠。<br>
   <strong>提示</strong>：<ul>
   <li>對於 IBM 認證的 Liberty Server 映像檔或此映像檔的已修改版本，請輸入埠 9080。</li>
   <li>對於 IBM 認證的 Node.js 映像檔或此映像檔的已修改版本，請輸入埠 8000。</li>
   </ul>
   </dd>
   <dt>-P（選用）</dt>
   <dd>發佈所有埠</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i>（選用）</dt>
   <dd>實例數下限。預設值為 1。如果設定實例數下限，則在建立容器群組之後，無法變更此值。</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i>（選用）</dt>
   <dd>實例數上限。預設值為 2。如果設定實例數上限，則在建立容器群組之後，無法變更此值。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i>（選用）</dt>
   <dd>您需要的實例數。預設值為 2。</dd>
   <dt>--auto（選用）</dt>
   <dd>建立容器群組並啟用自動回復後，IBM Containers 會對所指派的埠提出 HTTP 要求，以檢查每個實例的性能。<br>
如果您未在兩個後續 90 秒間隔內收到來自容器實例的回應，則會移除實例，並將其取代為新的實例。如果容器回應，則不需要採取任何動作。此處理程序會不斷地重複。在 30 分鐘時間範圍期間，如果本身為群組成員的不同容器總數等於或超出觀察到的群組大小上限的 3 倍，則會永久停用容器群組的自動回復。若要重新啟用自動回復，您必須重建容器群組。</dd>
  <dt>--anti（選用）</dt>
  <dd> 使用互斥，讓容器群組更高度可用。--anti 選項會強制將群組中的每個容器實例放在不同的實體運算節點上，這樣可減少群組中所有容器因硬體故障而損毀的機會。您可能無法搭配使用此選項與較大的群組大小，因為每一個 Bluemix 地區及組織可用來進行部署的運算節點集有限。如果您的部署失敗，請減少群組中的容器實例數，或移除 --anti 選項。</dd>
   <dt><i>CMD</i>（選用）</dt>
   <dd>傳遞給容器群組執行的指令及引數。這個指令必須是長時間執行的指令。請不要使用不會執行很久的短期指令（例如，<i>/bin/date</i>），因為短期指令可能會導致容器損毀。<br> <strong>附註：</strong> <ul>
   <li>指令及其引數必須在 <i>bluemix ic run</i> 指令行的結尾。</li>
   <li>如果指令引數包含連字號 -（如前一個範例指令中的 <i>-c</i>），則指令前面必須有兩個連字號 --。</li>
   </ul></dd>
   </dl>


<strong>範例</strong>：

使用 IBM Containers 所提供的 `registry.ng.bluemix.net/ibmnode` 映像檔來建立容器群組 `my_container_group`，然後在該容器群組上執行 `ping localhost` 長時間執行指令：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

使用 IBM Containers 所提供的 `registry.ng.bluemix.net/ibmnode` 映像檔來建立容器群組 `my_container_group`，然後在該容器群組上執行 `tail -f /dev/null` 長時間執行指令：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

使用 `registry.ng.bluemix.net/ibmliberty` 映像檔，以建立已啟用自動回復的可擴充群組 `mygroup`。埠是 `9080`、主機名稱是 `mycontainerhost`，而網域名稱是 `mybluemix.net`。
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


### bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

檢視在建立容器群組時針對它所指定的詳細資訊，例如環境變數、埠或記憶體。

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER_GROUP</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示檢查容器群組 `my_group` 的要求：

```
bluemix ic group-inspect my_group
```


### bluemix ic group-instances
{: #bluemix_ic_group_instances}

列出所指定容器群組的實例。

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER_GROUP</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

列出容器群組 `my_group` 的所有實例：

```
bluemix ic group-instances my_group
```


### bluemix ic group-remove
{: #bluemix_ic_group_remove}

從空間移除容器群組。

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-f|--force（選用）</dt>
   <dd>強制移除執行中或失敗的容器。</dd>
   <dt><i>GROUP_NAME</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示移除容器群組的要求，其中 `my_group` 是容器群組的名稱。

```
bluemix ic group-remove my_group
```


### bluemix ic group-update
{: #bluemix_ic_group_update}

更新容器群組。


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**提示：**若要更新容器群組的主機名稱或網域，請使用 `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`。

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
 <dl>
   <dt>--anti（選用）</dt>
   <dd>使用互斥，讓容器群組更高度可用。--anti 選項會強制將群組中的每個容器實例放在不同的實體運算節點上，這樣可減少群組中所有容器因硬體故障而損毀的機會。您可能無法搭配使用此選項與較大的群組大小，因為每一個 Bluemix 地區及組織可用來進行部署的運算節點集有限。如果您的部署失敗，請減少群組中的容器實例數，或移除 --anti 選項。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i>（選用）</dt>
   <dd>您需要的實例數。預設值為 <i>2</i>。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>（選用）</dt>
   <dd>設定環境變數。個別列出多個索引鍵。如果包含引號，請用它們括住環境變數名稱及值。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。</dd>
   <dt><i>GROUP_NAME</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示更新容器群組 `my_group` 的要求：

```
bluemix ic group-update --desired 5 my_group
```


### bluemix ic groups
{: #bluemix_ic_groups}

列出組織的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中的容器群組。

```
bluemix ic groups [-q]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
	<dl>
	<dt>-q（選用）</dt>
   	<dd>僅顯示群組 ID</dd>
	</dl>


### bluemix ic images
{: #bluemix_ic_images}

檢視組織專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中所有可用映像檔的清單。如需相關資訊，請參閱 Docker 說明中的 [images ](https://docs.docker.com/engine/reference/commandline/images){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。此清單包括映像檔 ID、建立日期及映像檔名稱。

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-a|--all（選用）</dt>
   <dd>包括組織儲存庫中每個映像檔的所有映像檔層，而不只是最新層。</dd>
   <dt>-f（選用）</dt>
   <dd>依提供的條件來過濾映像檔清單。</dd>
   <dt>--no-trunc（選用）</dt>
   <dd>不要截斷輸出。</dd>
   <dt>-q|--quiet（選用）</dt>
   <dd>只顯示數值 ID。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示接收組織可用映像檔清單的要求：

```
bluemix ic images
```


### bluemix ic info
{: #bluemix_ic_info}

檢視一組資訊，說明容器雲端服務實例的狀態。這項資訊包括容器限制、容器用量、執行中的容器、記憶體限制、記憶體用量、浮動 IP 位址限制、浮動 IP 位址用量、CCS 主機 URL、登錄主機 URL 及除錯模式狀態。

```
bluemix ic info
```

<strong>必要條件</strong>：端點、登入、目標


### bluemix ic init
{: #bluemix_ic_init}

起始設定本端機器上的 containers 環境，以使用 IBM Containers 服務的完整功能。

```
bluemix ic init
```

<strong>必要條件</strong>：端點、登入、目標

**附註：**起始設定之前，請確定 PATH 環境變數中已安裝並配置 Docker CLI (Docker)。若要切換至其他地區，請使用 `bluemix region-set` 指令。

<strong>範例</strong>：

切換至 `us-south` 地區：

```
bluemix region-set us-south
```


### bluemix ic inspect
{: #bluemix_ic_inspect}

檢視容器的相關資訊。如需相關資訊，請參閱 Docker 說明中的 [inspect](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} 指令。

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>IMAGE</i>（必要）</dt>
   <dd>指定映像檔名稱或 ID，以檢視特定映像檔的詳細資訊。</dd>
   <dt>images（必要）</dt>
   <dd>檢視儲存庫中所有映像檔的詳細資訊。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>指定容器名稱或 ID，以檢視特定容器的詳細資訊。</dd>
   </dl>

**提示：**一次只能指定 *IMAGE*、*images* 或 *CONTAINER* 其中一項。

<strong>範例</strong>：

下列範例顯示檢查名為 `proxy` 之容器的要求：

```
bluemix ic inspect proxy
```


### bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

將可用的浮動 IP 位址連結至容器。

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>IP_ADDRESS</i>（必要）</dt>
   <dd>要連結的 IP 位址。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>要連結的容器 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示將 IP 位址 `192.123.12.12` 連結至容器 `proxy` 的要求：

```
bluemix ic ip-bind 192.123.12.12 proxy
```


### bluemix ic ip-release
{: #bluemix_ic_ip_release}

釋放容器雲端服務實例中的浮動 IP 位址。

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>IP_ADDRESS</i>（必要）</dt>
   <dd>要釋放的 IP 位址。</dd>
   </dl>


### bluemix ic ip-request
{: #ip_request}
要求新的浮動 IP 位址。

```
bluemix ic ip-request [-q]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-q（選用）</dt>
   <dd>只列出 IP 位址，而不含連結至那些 IP 位址之容器的 ID。</dd>
   </dl>


### bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

取消浮動 IP 位址與其容器的連結。

公用 IP 位址是 IBM Containers 中的有限資源。因此，大約每週會從免費試用版使用者定期收回已配置給空間但未連結至容器的公用 IP 位址。不過，絕不會從隨收隨付制或訂閱客戶收回已解除連結的公用 IP 位址。

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>IP_ADDRESS</i>（必要）</dt>
   <dd>要取消連結的 IP 位址。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>要取消連結的容器 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示取消 IP 位址 `192.123.12.12` 與容器 `proxy` 的連結的要求：

```
bluemix ic ip-unbind 192.123.12.12 proxy
```


### bluemix ic ips
{: #bluemix_ic_ips}

列出已登入使用者的可用浮動 IP 位址。這份清單包括 IP 位址以及 IP 位址所鏈結的容器 ID。如果 IP 位址未使用，則不會顯示容器 ID。

```
bluemix ic ips [-q]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-q（選用）</dt>
   <dd>只列出 IP 位址，而不含連結至那些 IP 位址之容器的 ID。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示接收組織的所有 IP 位址清單的要求。
```
bluemix ic ips -q
```


### bluemix ic kill
{: #bluemix_ic_kill}

停止容器中的執行中處理程序，而不停止容器。如需相關資訊，請參閱 Docker 說明中的 [kill ](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i>（選用）</dt>
   <dd>將指令傳送給正在容器中執行的處理程序。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器 ID 或名稱。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示結束 (kill) 名為 `proxy` 之容器中處理程序的要求：

```
bluemix ic kill proxy
```


### bluemix ic logs
{: #bluemix_ic_logs}

顯示執行中容器的輸出或錯誤日誌。如需相關資訊，請參閱 Docker 說明中的 [logs ](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。
```
bluemix ic logs [OPTIONS] CONTAINER
```


### bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

檢視所登入組織之專用 {{site.data.keyword.Bluemix_notm}} 映像檔儲存庫的名稱。

```
bluemix ic namespace-get
```

<strong>必要條件</strong>：端點、登入、目標


### bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

設定所登入組織之專用 {{site.data.keyword.Bluemix_notm}} 映像檔儲存庫的名稱。

*限制*：您不能在儲存庫名稱空間名稱中使用連字號 `-`。

```
bluemix ic namespace-set NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>NAME</i>（必要）</dt>
   <dd>一次性函數，可設定組織的儲存庫名稱空間（如果尚未設定的話）。在您設定名稱空間之後，請先透過 `bluemix ic init` 指令重新起始設定 IBM Containers，然後再繼續進行。</dd>
   </dl>


### bluemix ic pause
{: #pause}

暫停執行中容器內的所有處理程序。如需相關資訊，請參閱 Docker 說明中的 [pause ](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。若要停止容器，請參閱 [bluemix ic unpause](#unpause) 指令。

```
bluemix ic pause CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：
   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>回應</strong>：

- 已順利暫停容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示暫停名為 `proxy` 之容器的要求：

```
bluemix ic pause proxy
```


### bluemix ic port
{: #bluemix_ic_port}

列出容器的埠對映或特定對映。此指令會覆蓋 `docker port` 指令。如需相關資訊，請參閱 Docker 說明中的 [port ](https://docs.docker.com/engine/reference/commandline/port/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。


### bluemix ic ps
{: #bluemix_ic_ps}
檢視已登入使用者之名稱空間中的執行中容器清單。此指令預設只會顯示執行中容器。如需相關資訊，請參閱 Docker 說明中的 [ps ](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-a|--all（選用）</dt>
   <dd>顯示所有容器（包括執行中及已停止）。</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i>（選用）</dt>
   <dd>搜尋具有特定環境變數值的容器。您可以依照檢查容器時 CLI 回應之 Env 區段中所列出的任何環境變數索引鍵或值來過濾容器。請將 SEARCH_CRITERIA 取代為您所尋找的索引鍵或值。您的搜尋準則不需要完全相符。</dd>
   <dt>-s|--size（選用）</dt>
   <dd>列出容器的大小。</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i>（選用）</dt>
   <dd>列出最近建立的容器，其中 <i>NUM</i> 是您要傳回的最新建立容器數目。<br><br> 例如，如果您已依序建立容器 <i>node1</i> 到 <i>node5</i>，則 <i>bluemix ic ps --limit 2</i> 指令會傳回 node4 和 node5，因為它們是最後建立的兩個容器。</dd>
   <dt>-q|--quiet（選用）</dt>
   <dd>只顯示容器 ID。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示查看所有執行中及已停止容器的要求：

```
bluemix ic ps -a
```


### bluemix ic rename
{: #bluemix_ic_rename}
重新命名容器。如需相關資訊，請參閱 Docker 說明中的 [rename ](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>必要條件</strong>：端點、登入、目標、Docker<strong>指令選項</strong>：

<dl>
   <dt><i>OLD_NAME</i>（必要）</dt>
   <dd>容器的舊名稱。</dd>
   <dt><i>NEW_NAME</i>（必要）</dt>
   <dd>容器的新名稱。</dd>
   </dl>


### bluemix ic reprovision
{: #bluemix_ic_reprovision}

在您已登入的 Bluemix 空間中，重建 IBM Containers 服務。會維護空間的原始配額。

<strong>重要事項</strong>：當您執行此指令時，此空間中您的單一容器及群組都不會移轉至重新佈建的空間，而且將會在移轉處理程序期間予以移除。

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>指令選項</strong>：<dl>
   <dt>--force|-f（選用）</dt>
   <dd>強制在 Bluemix 空間中重建 IBM Containers 服務。</dd>
   <dt><i>AVAILABILITY_ZONE</i>（選用）</dt>
   <dd>在其中部署容器的 IBM Containers 可用性區域的名稱。如果未指定任何可用性區域，則會使用針對地區所設定的預設可用性區域。</dd>
   </dl>


### bluemix ic restart
{: #bluemix_ic_restart}

重新啟動容器。如需相關資訊，請參閱 Docker 說明中的 [restart ](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i>（選用）</dt>
   <dd>重新啟動容器之前要等待的秒數。</dd>
   </dl>


<strong>回應</strong>：

- 已順利重新啟動容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示重新啟動名為 `proxy` 之容器的要求：

```
bluemix ic restart proxy
```


### bluemix ic rm
{: #bluemix_ic_rm}

移除容器。如需相關資訊，請參閱 Docker 說明中的 [rm ](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-f|--force（選用）</dt>
   <dd>強制移除執行中或失敗的容器。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>回應</strong>：

- 已順利移除容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務。

<strong>範例</strong>：

下列範例顯示移除名為 `proxy` 之容器的要求：

```
bluemix ic rm proxy
```


### bluemix ic rmi
{: #bluemix_ic_rmi}

移除已登入使用者之名稱空間中的映像檔。如需相關資訊，請參閱 Docker 說明中的 [rmi ](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i>（選用）</dt>
   <dd>變更登錄主機。預設值為使用您在 <i>bluemix ic init</i> 指令中指定的登錄。</dd>
   <dt><i>IMAGE</i>（必要）</dt>
   <dd>您要移除之映像檔的名稱。如果映像檔名稱中未指定標籤，則預設會刪除標記為 <i>latest</i> 的映像檔。</dd>
   </dl>

<strong>回應</strong>：

- 已移除：`{IMAGE}`

 其中 `{IMAGE}` 是已移除之映像檔的名稱。

- 錯誤！未指定任何登錄主機。

- 映像檔移除失敗 - 無法連接至容器雲端登錄

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

<strong>範例</strong>：

下列範例顯示移除映像檔 `mynamespace/myimage:latest` 的要求：

```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


### bluemix ic route-map
{: #bluemix_ic_route_map}

建立用來存取容器群組之網際網路資料流量的路徑。您可以使用此指令，建立新路徑或更新現有路徑。

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i>（選用）</dt>
   <dd>路徑的主機名稱。主機名稱是完整公用路徑 URL 的第一個部分（例如 URL <i>mycontainerhost.mybluemix.net</i> 中的 <i>mycontainerhost</i>）。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>（選用）</dt>
   <dd>路徑的網域名稱，即完整公用路徑 URL 的第二個部分。在大部分情況下，網域為 <i>mybluemix.net</i>。您也可以使用此參數來指定專用網域。</dd>
   <dt><i>CONTAINER_GROUP</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示對映稱為 `GROUP1` 之群組的路徑的要求，其中 `my_host` 是主機名稱，而 `mybluemix.net` 是網域。
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


### bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

建立用來存取容器群組之網際網路資料流量的路徑。您可以使用此指令，建立新路徑或更新現有路徑。

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i>（選用）</dt>
   <dd>路徑的主機名稱。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>（選用）</dt>
   <dd>路徑的網域名稱。</dd>
   <dt><i>CONTAINER_GROUP</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示取消對映名稱為 `GROUP1` 之群組的路徑的要求，其中 `my_host` 是主機名稱，而 `organization.com` 是網域。
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


### bluemix ic run
{: #bluemix_ic_run}

在容器雲端服務中，從映像檔名稱啟動新的容器。如需相關資訊，請參閱 Docker 說明中的 [run ](https://docs.docker.com/engine/reference/commandline/run/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**附註：**請確定已安裝 Cloud Foundry 指令工具，而且您有 Cloud Foundry 記號。使用 `bluemix login` 和 `bluemix ic init` 成功登入時，會產生必要的記號及憑證。

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>（選用）</dt>
   <dd>公開 HTTP 資料流量的埠。包括 Dockerfile 中針對您要使用之映像檔所指定的任何埠。您可以利用多個 <i>-p</i> 選項來包含多個埠。如果公用 IP 位址可供使用，則公開一個埠會自動將公用 IP 位址連結至容器。<br><br>如果空間中具有您要連結至容器的現有 IP 位址，您可以指定 IP 位址，而不用稍後再連結它。必須以下列格式指定 IP 位址：&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br><br>如需要求空間之 IP 位址的相關資訊，請參閱 <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a> 指令。<br><br>在您指定埠時，即將應用程式設為可供「{{site.data.keyword.Bluemix_notm}} 負載平衡器」或相同 {{site.data.keyword.Bluemix_notm}} 空間中嘗試連接主機的容器使用。如果在 Dockerfile 中針對您要使用的映像檔指定了埠，請包含該埠。<br><br><strong>提示：</strong><ul><li>對於 IBM 認證的 Liberty Server 映像檔或此映像檔的已修改版本，請輸入埠 9080。</li><li>對於 IBM 認證的 Node.js 映像檔或此映像檔的已修改版本，請輸入埠 8000。</li></ul></dd>
   <dt>-P（選用）</dt>
   <dd>自動公開映像檔的 Dockerfile 中針對 HTTP 資料流量所指定的埠。</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i>（選用）</dt>
   <dd>將記憶體限制指派給群組 (MB)。從 CLI 建立容器群組時，每個容器實例的預設值都是 64 MB。從「{{site.data.keyword.Bluemix_notm}} 儀表板」建立容器群組時，每個實例的預設值都是 256 MB。接受值為 64、256、512、1024 和 2048。指派記憶體限制之後，即無法變更其值。</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i>（選用）</dt>
   <dd>設定環境變數，其中 <i>ENV</i> 是 key=value 配對。個別列出多個索引鍵。如果您併入引號，請用它們括住環境變數名稱及值。例如：-e "key1=value1" -e "key2=value2" -e "key3=value3"。下表顯示一些您可以指定的常用環境變數：</dd>
   </dl>


|      環境變數                          |   說明                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 將服務連結至容器。請使用 `CCS_BIND_APP` 環境變數，將應用程式連結至容器。應用程式會連結至目標服務，並作為橋接器，以容許 {{site.data.keyword.Bluemix_notm}} 將您橋接應用程式的 `VCAP_SERVICES` 資訊帶入執行中容器實例。如需建立橋接應用程式的相關資訊，請參閱[將服務連結至容器](/docs/containers/container_integrations_binding.html){: new_window}。 |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 若要將 Bluemix 服務直接連結至容器，而不使用橋接應用程式，請使用 CCS_BIND_SRV。此連結容許 Bluemix 將 VCAP_SERVICES 資訊注入執行中容器實例。若要列出多個 Bluemix 服務，請將它們併入為相同環境變數的一部分。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 新增要在容器中監視的日誌檔。包括含有日誌檔路徑的 `LOG_LOCATIONS` 環境變數。 |
{: caption="表 9. 常用環境變數" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro]（選用）</dt>
   <dd>以 <i>VolumeId:ContainerPath[:ro]</i> 格式指定詳細資料，將磁區連接至容器。
   <ul>
   <li><i>VOLUME</i>：磁區 ID 或名稱。</li>
   <li><i>CONTAINER_PATH</i>：容器中磁區的絕對路徑。</li>
   <li>ro：選用。指定 <i>ro</i> 會使磁區變成唯讀，而不是預設的讀寫。</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i>（必要）</dt>
   <dd>將名稱指派給容器。<br> <strong>提示：</strong>容器名稱必須以字母開頭。名稱可以包含大寫字母、小寫字母、數字、句點 .、底線 _ 或連字號 -。</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i>（選用）</dt>
   <dd>每當您想要讓某個容器與另一個執行中的容器進行通訊時，可以使用主機名稱的別名來予以定址。</dd>
   <dt>-it（選用）</dt>
   <dd>以互動模式執行容器。建立容器之後，請持續顯示標準輸入。鍵入 <i>exit</i> 以結束。</dd>
   <dt><i>IMAGE</i>（必要）</dt>
   <dd>要併入容器中的映像檔。您可以在映像檔之後列出指令，但不能在映像檔之後放置任何選項。請在指定映像檔之前併入所有選項。請在指定映像檔之前併入所有選項。<br><br>如果您使用組織專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中的映像檔，請以下列格式指定映像檔：<i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>。<br><br>如果您使用 IBM Containers 所提供的映像檔，請以下列格式指定映像檔：<i>registry.ng.bluemix.net/IMAGE</i>。</dd>
   <dt><i>CMD</i>（選用）</dt>
   <dd>傳遞給容器群組執行的指令及引數。這個指令必須是長時間執行的指令。請不要使用不會執行很久的短期指令（例如，<i>/bin/date</i>），因為短期指令可能會導致容器損毀。</dd>
   </dl>


<strong>範例</strong>：

在以 `registry.ng.bluemix.net/ibmnode` 映像檔為建置基礎的 `my_container` 容器上，執行 `sh -c "while true; do date; sleep 20; done"` 長時間執行指令。

```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


使用 `my_namespace/nginx` 映像檔，來建立並啟動具有 `1024` MB 記憶體限制的容器 `proxy`，其中 `my_namespace` 是與已登入使用者相關聯的名稱空間。

```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

使用 `my_namespace/blog` 映像檔來建立並啟動容器，並將認證傳遞為環境變數。`my_namespace` 是與已登入使用者相關聯的名稱空間。

```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

使用 `my_namespace/blog` 映像檔，以在容器中新增磁區，其中 `my_namespace` 是與已登入使用者相關聯的名稱空間。

```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


### bluemix ic service-bind
{: #bluemix_ic_service-bind}

將服務新增至執行中的容器群組。此指令僅適用於容器群組。單一容器必須在執行 bluemix ic run 指令時連結服務。

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE 
```
<strong>指令選項</strong>：<dl>
   <dt><i>GROUP_NAME</i>（必要）</dt>
   <dd>群組 ID 或名稱。</dd>
   <dt><i>SERVICE_INSTANCE</i>（必要）</dt>
   <dd>要新增至容器群組的服務實例名稱。</dd>
   </dl>


### bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

從執行中的容器群組移除服務。此指令僅適用於容器群組。單一容器必須移除容器，並在沒有服務的情況下建立新的容器。

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE 
```
<strong>指令選項</strong>：<dl>
   <dt><i>GROUP_NAME</i>（必要）</dt>
   <dd>群組 ID 或名稱。</dd>
   <dt><i>SERVICE_INSTANCE</i>（必要）</dt>
   <dd>要新增至容器群組的服務實例名稱。</dd>
   </dl>


### bluemix ic start
{: #ic_start}
啟動已停止的容器。如需相關資訊，請參閱 Docker 說明中的 [start ](https://docs.docker.com/engine/reference/commandline/start/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。若要停止容器，請參閱 [bluemix ic stop](#ic_stop) 指令。

```
bluemix ic start CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>


<strong>回應</strong>：

- 已順利啟動容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示啟動名為 `proxy` 之容器的要求。

```
bluemix ic start proxy
```


### bluemix ic stats
{: #bluemix_ic_stats}

對於一個以上的容器，檢視即時用量統計資料。使用 `CTRL+C` 以結束。如需相關資訊，請參閱 Docker 說明中的 [stats](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} 指令。

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   <dt>--no-stream（選用）</dt>
   <dd>只顯示最新結果，而不包含它之前的任何資訊。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示最新容器統計資料的要求：

```
bluemix ic stats --no-stream my_container
```


### bluemix ic stop
{: #ic_stop}
停止執行中的容器。如需相關資訊，請參閱 Docker 說明中的 [stop ](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。若要啟動容器，請參閱 [bluemix ic start](#ic_start) 指令。

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i>（選用）</dt>
   <dd>結束 (kill) 容器之前要等待的秒數。</dd>
   </dl>

<strong>回應</strong>：

- 已順利停止容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示停止名為 `proxy` 之容器的要求。

```
bluemix ic stop proxy
```


### bluemix ic top
{: #bluemix_ic_top}

顯示正在容器中執行的處理程序。如需相關資訊，請參閱 Docker 說明中的 [top ](https://docs.docker.com/engine/reference/commandline/top/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示要在稱為 `my_container` 之容器中顯示處理程序的要求。

```
bluemix ic top my_container
```


### bluemix ic unpause
{: #unpause}

取消暫停執行中容器內的所有處理程序。如需相關資訊，請參閱 Docker 說明中的 [unpause ](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。若要暫停容器，請參閱 [bluemix ic pause](#pause) 指令。

```
bluemix ic unpause CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>回應</strong>：

- 已順利取消暫停容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示取消暫停名為 `proxy` 之容器的要求：

```
bluemix ic unpause proxy
```


### bluemix ic unprovision
{: #bluemix_ic_unprovision}

從您已登入的 Bluemix 空間刪除 IBM Containers 服務。

<strong>注意</strong>：當您執行此指令時，會遺失您的所有單一容器及容器群組。您的空間仍可在 Bluemix 中使用。若要重新開始使用 IBM Containers，您必須執行 `bluemix ic reprovision` 來重新佈建 IBM Containers 服務。

```
bluemix ic reprovision [--force|-f] 
```
<strong>指令選項</strong>：<dl>
   <dt>--force|-f（選用）</dt>
   <dd>強制從 Bluemix 空間刪除 IBM Containers 服務。</dd>
 </dl>


### bluemix ic version
{: #bluemix_ic_version}

顯示 Docker 的版本及 IBM Containers API。

```
bluemix ic version
```

<strong>必要條件</strong>：Docker

若要查看 IBM Containers 的版本，請執行 `bluemix ic info`。如需相關資訊，請參閱 Docker 說明中的 [version ](https://docs.docker.com/engine/reference/commandline/version/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。


### bluemix ic volume-create
{: #bluemix_ic_volume_create}

建立磁區。

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>FS_NAME</i>（選用）</dt>
   <dd>檔案共用名稱。如果沒有檔案共用可供使用，或未指定檔案共用，則會在空間的預設檔案共用上建置磁區。</dd>
   <dt><i>VOLUME_NAME</i>（必要）</dt>
   <dd>磁區名稱。名稱可以包含小寫字母、數字、底線 _ 及連字號 -。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示建立磁區的要求。

```
bluemix ic volume-create volume_name fileshare_name
```


### bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

列出檔案共用。

```
bluemix ic volume-fs
```


### bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

建立檔案共用。

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>FILE_SHARE_NAME</i>（必要）</dt>
   <dd>檔案共用名稱。名稱可以包含小寫字母、數字、底線 _ 及連字號 -。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示建立檔案共用的要求。
```
bluemix ic volume-fs-create my_file_share
```


### bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

列出所有檔案共用特性。

```
bluemix ic volume-fs-flavors
```

<strong>必要條件</strong>：端點、登入、目標


### bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

檢查檔案共用。

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

  <dl>
  <dt><i>FILE_SHARE_NAME</i>（必要）</dt>
   <dd>檔案共用名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例是檢查檔案共用的要求，其中 `my_file_share` 是檔案共用的名稱。
```
bluemix ic volume-fs-inspect my_file_share
```


### bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

移除檔案共用。

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>FILE_SHARE_NAME</i>（必要）</dt>
   <dd>檔案共用名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示移除檔案共用的要求，其中 `my_file_share` 是檔案共用的名稱。
```
bluemix ic volume-fs-remove my_file_share
```


### bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

檢查磁區。

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>VOLUME_NAME</i>（必要）</dt>
   <dd>磁區名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例是檢查磁區的要求，其中 `volume_name` 是磁區的名稱。

```
bluemix ic volume-inspect volume_name
```


### bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

移除磁區。

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>VOLUME_NAME</i>（必要）</dt>
   <dd>磁區名稱。</dd>
    </dl>

<strong>範例</strong>：

下列範例顯示移除磁區的要求，其中 `volume_name` 是磁區的名稱。

```
bluemix ic volume-remove volume_name
```


### bluemix ic volumes
{: #bluemix_ic_volumes}

列出磁區。

```
bluemix ic volumes
```

<strong>必要條件</strong>：端點、登入、目標


### bluemix ic wait
{: #bluemix_ic_wait}

結束容器，並顯示結束碼作為確認。如需相關資訊，請參閱 Docker 說明中的 [wait ](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg) 指令。

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示結束稱為 `my_container` 之容器的要求：

```
bluemix ic wait my_container
```


### bluemix ic wait-status
{: #bluemix_ic_wait_status}

等待單一容器或容器群組達到非暫時性狀態。在此等待時間，您的指令行不會返回，因此您無法輸入指令。只要容器達到非暫時性狀態，就會顯示 OK 訊息。若為單一容器，非暫時性狀態包括 Running、Shutdown、Crashed、Paused 或 Suspended。若為容器群組，非暫時性狀態包括 CREATE_COMPLETE、UPDATE_COMPLETE 或 FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示結束稱為 `my_container` 之容器的要求：

```
bluemix ic wait my_container
```



# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

* [bx tool ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg)
