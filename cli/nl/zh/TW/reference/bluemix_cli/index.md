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
 <caption>表 1. 一般 bluemix 指令</caption>
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
 <caption>表 2. 用來管理組織、空間和使用者的指令</caption>
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
 <caption>表 3. 用來管理 cf 應用程式的指令</caption>
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
 <caption>表 4. 用來管理 Bluemix 服務的指令</caption>
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
 <caption>表 5. 用來管理 Bluemix 型錄、外掛程式、帳單和安全設定的指令</caption>
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
 <caption>表 6. 用來管理網路設定的指令</caption>
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

從 `bluemix-repo` 儲存庫安裝最新版本的 `container-service` 外掛程式：

```
bluemix plugin install container-service -r bluemix-repo
```
從 `bluemix-repo` 儲存庫安裝版本為 `0.5.800` 的 `container-service` 外掛程式：
```
bluemix plugin install container-service -r bluemix-repo -v 0.1.217
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

解除安裝先前安裝的 `container-service` 外掛程式：

```
bluemix plugin uninstall container-service
```



# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

* [bx tool ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg)
