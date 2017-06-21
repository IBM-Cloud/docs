---



copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} (bx) 指令
{: #bluemix_cli}

版本：0.5.2

{{site.data.keyword.Bluemix_notm}} 指令行介面 (CLI) 提供一組依名稱空間分組的指令，讓使用者與 {{site.data.keyword.Bluemix_notm}} 互動。有些 {{site.data.keyword.Bluemix_notm}} 指令是現有 cf 指令的封套，有些則提供延伸功能供 {{site.data.keyword.Bluemix_notm}} 使用者使用。下列資訊列出 {{site.data.keyword.Bluemix_notm}} CLI 支援的指令，並包含其名稱、選項、用法、必要條件、說明及範例。
{:shortdesc}

**附註：***必要條件* 列出使用指令之前需要哪些動作。沒有必要動作的指令會列為**無**。否則，必要條件可能包括下列一個以上的動作：

<dl>
<dt>端點</dt>
<dd>必須透過 <code>bluemix api</code> 設定 API 端點後，才能使用此指令。</dd>
<dt>登入</dt>
<dd>需要使用 <code>bluemix login</code> 指令進行登入後，才能使用此指令。如果是使用聯合 ID 登入，請使用 '--sso' 選項以一次性密碼進行鑑別，或使用 '--apikey' 以 API 金鑰進行鑑別。移至 {{site.data.keyword.Bluemix_notm}} 主控台**管理** &gt; **安全** &gt; **Bluemix API 金鑰**，以建立 API 金鑰。
</dd>
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

<table summary="您可以用來管理帳戶、組織、空間、角色及 API 金鑰的 bluemix 指令。">
<caption>表 2. 用來管理帳戶、組織、空間、角色及 API 金鑰的指令</caption>
 <thead>
 <th colspan="5">用來管理帳戶、組織、空間、角色及 API 金鑰的指令</th>
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
 <td>[bluemix iam account-users
](bx_cli.html#bluemix_iam_account_users)</td>
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

<table summary="您可以用來管理 cf 應用程式及應用程式相關網域、路徑和憑證的 bluemix 指令。">
<caption>表 3. 用來管理 cf 應用程式及應用程式相關網域、路徑和憑證的指令</caption>
 <thead>
 <th colspan="5">用來管理 cf 應用程式及應用程式相關網域、路徑和憑證的指令</th>
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

<table summary="您可以用來管理 Bluemix 服務的 bluemix 指令。">
 <caption>表 4. 用來管理 Bluemix 服務的指令</caption>
 <thead>
 <th colspan="5">用來管理 Bluemix 服務的指令</th>
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

<table summary="您可以用來管理 Bluemix 型錄、外掛程式、帳單和安全設定的 bluemix 指令。">
 <caption>表 5. 用來管理 Bluemix 型錄、外掛程式、帳單和安全設定的指令</caption>
 <thead>
 <th colspan="5">用來管理 Bluemix 型錄、外掛程式、帳單和安全設定的指令</th>
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



## bluemix api
{: #bluemix_api}
設定或檢視 {{site.data.keyword.Bluemix_notm}} API 端點。

```
bluemix api [API_ENDPOINT] [--unset] [--skip-ssl-validation]
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：
   <dl>
   <dt>API_ENDPOINT（選用）</dt>
   <dd>設為目標的 API 端點，例如 `https://api.chinabluemix.net`。 如果未同時指定 *API_ENDPOINT* 及 `--unset` 選項，則會顯示現行 API 端點。</dd>
   <dt>--unset（選用）</dt>
   <dd>移除 API 端點設定。</dd>
   <dt>--skip-ssl-validation（選用）</dt>
   <dd>略過 HTTP 要求的 SSL 驗證。</dd>
   </dl>
<strong>範例</strong>：將 API 端點設為 api.chinabluemix.net：

```
bluemix api api.chinabluemix.net
```

```
bluemix api https://api.chinabluemix.net --skip-ssl-validation
```

檢視現行 API 端點：

```
bluemix api
```

取消設定 API 端點：

```
bluemix api --unset
```


## bluemix login
{: #bluemix_login}

登入使用者。 

```
bluemix login [OPTIONS...]
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：
<dl>
  <dt>-a <i>API_ENDPOINT</i>（選用）</dt>
  <dd> API 端點（例如：api.ng.bluemix.net）</dd>
  <dt> --apikey <i>API_KEY 或 @API_KEY_FILE_PATH</i>
  <dd> API 金鑰內容，或透過 @ 指出的 API 金鑰檔案的路徑</dd>
  <dt> --sso（選用）</dt>
  <dd> 使用一次性密碼進行登入</dd>
  <dt> -u <i>USERNAME</i>（選用）</dt>
  <dd> 使用者名稱</dd>
  <dt> -p <i>PASSWORD</i>（選用）</dt>
  <dd> 密碼</dd>
  <dt> -c <i>ACCOUNT_ID</i>（選用）</dt>
  <dd> 目標帳戶的 ID</dd>
  <dt> -o <i>ORG_NAME</i>（選用）</dt>
  <dd> 目標組織的名稱</dd>
  <dt> -s <i>SPACE_NAME</i>（選用）</dt>
  <dd> 目標空間的名稱</dd>
  <dt> --skip-ssl-validation（選用）</dt>
  <dd> 略過 HTTP 要求的 SSL 驗證。不建議使用這個選項。</dd>
</dl>

<strong>範例</strong>：

互動式登入：

```
bluemix login
```

以使用者名稱及密碼登入，並設定目標帳戶、組織及空間：

```
bluemix login -u username -p password -c MyAccountID -o MyOrg -s MySpace
```

以一次性密碼登入，並設定目標帳戶、組織及空間：

```
bluemix login --sso -c MyAccountID -o MyOrg -s MySpace
```

以 API 金鑰登入，並設定目標：

* API 金鑰具有關聯的帳戶

```
bluemix login --apikey api-key-string -o MyOrg -s MySpace
```

```
bluemix login --apikey @filename -o MyOrg -s MySpace
```

* API 金鑰沒有關聯的帳戶

```
bluemix login --apikey api-key-string -c MyAccountID -o MyOrg -s MySpace
```

```
bluemix login --apikey @fileName -c MyAccountID -o MyOrg -s MySpace
```

<strong>附註：</strong>如果 API 金鑰具有關聯的帳戶，則不容許切換至另一個帳戶。


## bluemix logout
{: #bluemix_logout}

登出使用者。

```
bluemix logout
```

<strong>必要條件</strong>：無


## bluemix target
{: #bluemix_target}


設定或檢視目標帳戶、地區、組織或空間。

```
bluemix target [-c ACCOUNT_ID] [-r REGION] [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
   <dl>
   <dt>-c <i>ACCOUNT_ID</i>（選用）</dt>
   <dd>要設為目標的帳戶 ID。</dd>
   <dt>-r <i>REGION</i>（選用）</dt>
   <dd>要切換至的目標地區。</dd>
   <dt>-o <i>ORG_NAME</i>（選用）</dt>
   <dd>要設為目標的組織名稱。</dd>
   <dt>-s <i>SPACE_NAME</i>（選用）</dt>
   <dd>要設為目標的空間名稱。</dd>
   </dl>
如果未指定選項，則會顯示現行帳戶、地區、組織及空間。

<strong>範例</strong>：

設定現行帳戶、組織及空間

```
bluemix target -c MyAccountID -o MyOrg -s MySpace
```

切換至新的地區

```
bluemix target -r eu-gb
```

檢視現行帳戶、地區、組織及空間：

```
bluemix target
```


## bluemix info
{: #bluemix_info}

檢視基本 {{site.data.keyword.Bluemix_notm}} 資訊，包括現行地區、雲端控制器版本以及部分有用端點（例如用於登入及交換存取記號的端點）。

```
bluemix info
```

<strong>必要條件</strong>：端點


## bluemix config
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


## bluemix curl
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

## bluemix update
{: #bluemix_update}

將 CLI 更新至最新版本

```
bluemix update
```

<strong>必要條件</strong>：無

## bluemix regions
{: #bluemix_regions}

檢視 {{site.data.keyword.Bluemix_notm}} 上所有地區的資訊。

```
bluemix regions
```

<strong>必要條件</strong>：端點


## bluemix iam orgs
{: #bluemix_iam_orgs}

列出所有組織

```
bluemix iam orgs [-r REGION] [--guid]
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

## bluemix iam org
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


## bluemix iam org-create
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

## bluemix iam org-replicate
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


## bluemix iam org-rename
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

## bluemix iam org-delete
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


## bluemix iam spaces
{: #bluemix_iam_spaces}

此指令的函數及選項與 `cf spaces` 指令相同。


## bluemix iam space
{: #bluemix_iam_space}

此指令的函數及選項與 `cf space` 指令相同。


## bluemix iam space-create
{: #bluemix_iam_space_create}

此指令的函數及選項與 `cf create-space` 指令相同。


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


此指令的函數及選項與 `cf rename-space` 指令相同。


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


此指令的函數及選項與 `cf delete-space` 指令相同。

## bluemix iam org-users
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

## bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

將使用者新增到組織（需要組織管理員）。

```
 bluemix iam org-user-add USER_NAME ORG
```

## bluemix iam org-user-remove
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

## bluemix iam org-roles
{: #bluemix_iam_org_roles}

取得現行使用者的所有組織角色

```
bluemix iam org-roles
```

<strong>必要條件</strong>：端點、登入

## bluemix iam org-role-set
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


## bluemix iam org-role-unset
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

## bluemix iam space-users
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


## bluemix iam space-role-set
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

## bluemix iam space-role-unset
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

## bluemix iam accounts
{: #bluemix_iam_accounts}

列出現行使用者的所有帳戶

```
bluemix iam accounts
```

<strong>必要條件</strong>：端點、登入


## bluemix iam org-account
{: #bluemix_iam_org_account}

顯示所指定組織的帳戶（需要組織使用者）

```
bluemix iam org-account ORG_NAME [--guid]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
<dl>
  <dt>--guid（選用）</dt>
  <dd>僅顯示帳戶 ID</dd>
</dl>


## bluemix iam account-users
{: #bluemix_iam_account_users}

顯示與帳戶相關聯的使用者。只有帳戶擁有者才能執行此作業。

```
bluemix iam account-users
```

## bluemix iam account-user-delete
{: #bluemix_iam_account_user_delete}

從現行帳戶刪除使用者（僅限帳戶擁有者）

```
bluemix iam account-user-delete USERNAME [-f]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
<dl>
<dt>USERNAME（必要）</dt>
<dd>使用者名稱</dd>
<dt>--force、-f（選用）</dt>
<dd>強制刪除，而不確認。</dd>
</dl>

## bluemix iam account-user-invite
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

## bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

重新傳送邀請給使用者（需要組織管理員或帳戶擁有者）

```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```

## bluemix iam api-keys
{: #bluemix_iam api_keys}

列出所有 Bluemix 平台 API 金鑰

```
bluemix iam api-keys
```

<strong>必要條件</strong>：端點、登入

## bluemix iam api-key-create
{: #bluemix_iam_api_key_create}

建立新的 Bluemix 平台 API 金鑰

```
bluemix iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
<dl>
<dt>NAME（必要）</dt>
<dd>要建立之 API 金鑰的名稱。</dd>
<dt>-d <i>DESCRIPTION</i>（選用）</dt>
<dd>API 金鑰的說明</dd>
<dt>-f、-- file <i>FILE</i></dt>
<dd>將 API 金鑰資訊儲存至指定的檔案。如果未設定，則會顯示 JSON 內容。</dd>
</dl>

<strong>範例</strong>：

建立 API 金鑰，並儲存至檔案

```
bluemix iam api-key-create MyKey -d "this is my API key" -f key_file
```

## bluemix iam api-key-update
{: #bluemix_iam_api_key_update}

更新 Bluemix 平台 API 金鑰

```
bluemix iam api-key-update NAME [-n NAME] [-d DESCRIPTION]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
<dl>
<dt>NAME（必要）</dt>
<dd>要更新之 API 金鑰的舊名稱。</dd>
<dt>-n <i>NAME</i>（選用）</dt>
<dd>API 金鑰的新名稱</dd>
<dt>-d <i>DESCRIPTION</i>（選用）</dt>
<dd>API 金鑰的新說明</dd>
</dl>

<strong>範例</strong>：

更新 API 金鑰的說明：

```
bluemix iam api-key-update MyKey -d "the new description of my key"
```

## bluemix api-key-delete
{: #bluemix_api_key_delete}

刪除 Bluemix 平台 API 金鑰

```
bluemix iam api-key-delete NAME [-f]
```

<strong>必要條件</strong>：端點、登入

<strong>指令選項</strong>：
<dl>
<dt>NAME（必要）</dt>
<dd>要刪除之 API 金鑰的名稱。</dd>
<dt>-f（選用）</dt>
<dd>強制刪除，而不確認。</dd>
</dl>


## bluemix app push
{: #bluemix_app_push}

此指令的函數及選項與 `cf push` 指令相同。


## bluemix app list
{: #bluemix_app_list}

此指令的函數及選項與 `cf apps` 指令相同。


## bluemix app show
{: #bluemix_app_show}

此指令的函數及選項與 `cf app` 指令相同。


## bluemix app delete
{: #bluemix_app_delete}

此指令的函數及選項與 `cf delete` 指令相同。


## bluemix app rename
{: #bluemix_app_rename}

此指令的函數及選項與 `cf rename` 指令相同。


## bluemix app start
{: #bluemix_app_start}

此指令的函數及選項與 `cf start` 指令相同。


## bluemix app stop
{: #bluemix_app_stop}

此指令的函數及選項與 `cf stop` 指令相同。


## bluemix app restart
{: #bluemix_app_restart}

此指令的函數及選項與 `cf restart` 指令相同。


## bluemix app restage
{: #bluemix_app_restage}


此指令的函數及選項與 `cf restage` 指令相同。


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


此指令的函數及選項與 `cf restart-app-instance` 指令相同。


## bluemix app events
{: #bluemix_app_events}

此指令的函數及選項與 `cf events` 指令相同。


## bluemix app files
{: #bluemix_app_files}

此指令的函數及選項與 `cf files` 指令相同。


## bluemix app logs
{: #bluemix_app_logs}

此指令的函數及選項與 `cf logs` 指令相同。


## bluemix app env
{: #bluemix_app_env}

此指令的函數及選項與 `cf env` 指令相同。


## bluemix app env-set
{: #bluemix_app_env_set}

此指令的函數及選項與 `cf set-env` 指令相同。


## bluemix app env-unset
{: #bluemix_app_env_unset}

此指令的函數及選項與 `cf unset-env` 指令相同。


## bluemix app stacks
{: #bluemix_app_stacks}

此指令的函數及選項與 `cf stacks` 指令相同。


## bluemix app stack-show
{: #bluemix_app_stack_show}

此指令的函數及選項與 `cf stack` 指令相同。


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

此指令的函數及選項與 `cf create-app-manifest` 指令相同。

## bluemix app domain-cert 
{: #bluemix_app_domain_cert}

列出網域的憑證資訊。

```
bluemix app domain-cert DOMAIN_NAME
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
bluemix app domain-cert ibmcxo-eventconnect.com
```

## bluemix app domain-cert-add
{: #bluemix_app_domain_cert_add}

將憑證新增到現行組織中的指定網域。

```
bluemix app domain-cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [-t TRUST_STORE_FILE]
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
   <dt>-t <i>TRUST_STORE_FILE</i>（選用）</dt>
   <dd>信任儲存庫檔案。</dd>
   </dl>


<strong>範例</strong>：

將憑證新增到網域 `ibmcxo-eventconnect.com`：

```
bluemix app domain-cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```

## bluemix app domain-cert-remove
{: #bluemix_app_domain_cert_remove}

從現行組織中的指定網域移除憑證。

```
bluemix app domain-cert-remove DOMAIN [-f]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>DOMAIN（必要）</dt>
   <dd>要從中移除憑證的網域。</dd>
   <dt>-f（選用）</dt>
   <dd>強制刪除，而不確認。</dd>
   </dl>

## bluemix app domains
{: #bluemix_app_domains}

此指令的函數及選項與 `cf domains` 指令相同。


## bluemix app domain-create
{: #bluemix_app_domain_create}

此指令的函數及選項與 `cf create-domain` 指令相同。


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

此指令的函數及選項與 `cf delete-domain` 指令相同。


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

此指令的函數及選項與 `cf create-shared-domain` 指令相同。


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

此指令的函數及選項與 `cf delete-shared-domain` 指令相同。

## bluemix app routes
{: #bluemix_app_routes}

此指令的函數及選項與 `cf routes` 指令相同。


## bluemix app route-check
{: #bluemix_app_route_check}

此指令的函數及選項與 `cf check-route` 指令相同。


## bluemix app route-map
{: #bluemix_app_route_map}

將路徑對映至具有所指定網域及主機名稱的現有 cf 應用程式或容器群組。

```
bluemix app route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix app route-map my-app mychinabluemix.net
```

以指定的網域及主機名稱對映將路徑對映至 'my-container-group'：

```
bluemix app route-map my-container-group chinabluemix.net -n abc
```


## bluemix app route-unmap
{: #bluemix_app_route_unmap}

從現有的 cf 應用程式或容器群組中取消對映指定的路徑。

```
bluemix app route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix app route-unmap my-app mychianbluemix.net
```

從 `my-container-group` 取消對映 `abc.chinabluexmix.net`：

```
bluemix app route-unmap my-container-group chinabluemix.net -n abc
```


## bluemix app route-create
{: #bluemix_app_route_create}

此指令的函數及選項與 `cf create-route` 指令相同。


## bluemix app route-delete
{: #bluemix_app_route_delete}

此指令的函數及選項與 `cf delete-route` 指令相同。


## bluemix app orphaned-routes-delete
{: #bluemix_app_orphaned_routes_delete}

此指令的函數及選項與 `cf delete-orphaned-routes` 指令相同。


## bluemix app domains
{: #bluemix_app_domains}

此指令的函數及選項與 `cf domains` 指令相同。


## bluemix app domain-create
{: #bluemix_app_domain_create}

此指令的函數及選項與 `cf create-domain` 指令相同。


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

此指令的函數及選項與 `cf delete-domain` 指令相同。


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

此指令的函數及選項與 `cf create-shared-domain` 指令相同。


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

此指令的函數及選項與 `cf delete-shared-domain` 指令相同。


## bluemix service offerings
{: #bluemix_service_offerings}


此指令的函數及選項與 `cf marketplace` 指令相同。


## bluemix service list
{: #bluemix_service_list}

此指令的函數及選項與 `cf services` 指令相同。


## bluemix service show
{: #bluemix_service_show}

此指令的函數及選項與 `cf service` 指令相同。


## bluemix service create
{: #bluemix_service_create}

此指令的函數及選項與 `cf create-service` 指令相同。


## bluemix service update
{: #bluemix_service_update}

此指令的函數及選項與 `cf update-service` 指令相同。


## bluemix service delete
{: #bluemix_service_delete}

此指令的函數及選項與 `cf delete-service` 指令相同。


## bluemix service rename
{: #bluemix_service_rename}

此指令的函數及選項與 `cf rename-service` 指令相同。


## bluemix service bind
{: #bluemix_service_bind}

此指令的函數及選項與 `cf bind-service` 指令相同。


## bluemix service unbind
{: #bluemix_service_unbind}

此指令的函數及選項與 `cf unbind-service` 指令相同。


## bluemix service key-create
{: #bluemix_service_key_create}

此指令的函數及選項與 `cf create-service-key` 指令相同。


## bluemix service key-delete
{: #bluemix_service_key_delete}

此指令的函數及選項與 `cf delete-service-key` 指令相同。


## bluemix service keys
{: #bluemix_service_keys}

此指令的函數及選項與 `cf service-keys` 指令相同。


## bluemix service key-show
{: #bluemix_service_key_show}

此指令的函數及選項與 `cf service-key` 指令相同。


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

此指令的函數及選項與 `cf create-user-provided-service` 指令相同。


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

此指令的函數及選項與 `cf update-user-provided-service` 指令相同。


## bluemix catalog templates
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


## bluemix catalog template
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


## bluemix catalog template-run
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

## bluemix billing account-usage
{: #bluemix_billing_account_usage}

顯示帳戶的每月用量和費用。

```
bluemix billing account-usage [-d YYYY-MM] [--json]
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
bluemix billing account-usage -d 2016-06
```

## bluemix billing org-usage
{: #bluemix_billing_org_usage}

顯示組織的每月用量詳細資料。只有組織的帳單管理員可以執行此作業。

```
bluemix billing org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
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



## bluemix billing orgs-usage-summary
{: #bluemix_billing_orgs_usage_summary}

顯示我的帳戶中組織的每月用量摘要。

```
bluemix billing orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
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


## bluemix plugin repos
{: #bluemix_plugin_repos}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中登錄的所有外掛程式儲存庫。

```
bluemix plugin repos
```

<strong>必要條件</strong>：無


## bluemix plugin repo-add
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


## bluemix plugin repo-remove
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


## bluemix plugin repo-plugins
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


## bluemix plugin list
{: #bluemix_plugin_list}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中的所有已安裝外掛程式。

```
bluemix plugin list
```

<strong>必要條件</strong>：無


## bluemix plugin install
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

## bluemix plugin update
{: #bluemix_plugin_update}

從儲存庫升級外掛程式

```
bluemix plugin update -r REPO_NAME [PLUGIN NAME [-v VERSION]]
```

<strong>必要條件</strong>：無

<strong>指令選項</strong>：
<dl>
 <dt>-r REPO_NAME（必要）</dt>
 <dd>外掛程式二進位檔所在儲存庫的名稱。</dd>
 <dt><i>PLUGIN_NAME</i>（選用）</dt>
 <dd>如果未指定，則會列出給定儲存庫中可用於更新的所有外掛程式，以供選取。</dd>
 <dt>-v <i>VERSION</i>（選用）</dt>
 <dd>要更新至之目標外掛程式的版本。如果未提供，請將外掛程式更新至最新的可用版本。</dd>
</dl>

<strong>範例</strong>：

檢查外掛程式儲存庫 "My-Repo" 中的所有可用升級：

```
bluemix plugin update -r My-Repo
```

將儲存庫 "My-Repo" 中的外掛程式 "plugin-echo" 升級至最新版本：

```
bluemix plugin update -r My-Repo plugin-echo
```

將儲存庫 "My-Repo" 中的外掛程式 "plugin-echo" 更新為 "1.0.1" 版：

```
bluemix plugin update -r My-Repo plugin-echo -v 1.0.1
```

## bluemix plugin uninstall
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
