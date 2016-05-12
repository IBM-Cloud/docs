---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} (bx) 指令
{: #bluemix_cli}

*前次更新：2016 年 4 月 15 日*

{{site.data.keyword.Bluemix_notm}} 指令行介面 (CLI) 提供一組依名稱空間分組的指令，讓使用者與 {{site.data.keyword.Bluemix_notm}} 互動。部分 {{site.data.keyword.Bluemix_notm}} 指令是現有指令的封套，其他則提供延伸功能供 {{site.data.keyword.Bluemix_notm}} 使用者使用。下列資訊列出 {{site.data.keyword.Bluemix_notm}} CLI 支援的所有指令，並包括其名稱、選項、使用情形、必要條件、說明及範例。
{:shortdesc}
 
**附註：***必要條件* 列出使用指令之前需要哪些動作。沒有必要動作的指令會列為**無**。否則，必要條件可能包括下列一個以上的動作：
<dl>
<dt>端點</dt>
<dd>必須透過 <code>bluemix api</code> 設定 API 端點後，才能使用此指令。</dd>
<dt>登入</dt>
<dd>需要使用 <code>bluemix login</code> 指令進行登入後，才能使用此指令。</dd>
<dt>目標</dt>
<dd>必須使用 <code>bluemix target</code> 指令來設定組織及空間後，才能使用此指令。</dd>
<dt>Docker</dt>
<dd>必須先安裝 Docker CLI (Docker)，才能執行此指令。</dd>
</dl>

您可以使用下列 {{site.data.keyword.Bluemix_notm}} 指令：

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
顯示 {{site.data.keyword.Bluemix_notm}} CLI 之第一層內建指令及所支援名稱空間的一般說明，或特定內建指令或名稱空間的說明。

```
bluemix help [COMMAND|NAMESPACE]
```

**必要條件**：無

**指令選項**：

*COMMAND*|*NAMESPACE*（選用）：顯示說明的指令或名稱空間。如果未指定，則會顯示 {{site.data.keyword.Bluemix_notm}} CLI 的一般說明。

**範例**：

顯示 {{site.data.keyword.Bluemix_notm}} CLI 的一般說明：

```
bluemix help
```

顯示 `info` 指令的說明：

```
bluemix help info
```

顯示 `ic` 名稱空間的說明：

```
bluemix help ic
```

或 

```
bluemix ic help
```

顯示 `ic` 名稱空間下 `group-create` 指令的說明：

```
bluemix ic help group-create
```


## bluemix api
{: #bluemix_api}
設定或檢視 {{site.data.keyword.Bluemix_notm}} API 端點。此指令會覆蓋 `cf api` 指令。

```
bluemix api [API_ENDPOINT][--unset]
```

**必要條件**：無

**指令選項**：

*API_ENDPOINT*（選用）：已設定目標的 API 端點，例如 https://api.ng.bluemix.net。 如果未同時指定 *API_ENDPOINT* 及 `--unset` 選項，則會顯示現行 API 端點。

`--unset`（選用）：移除 API 端點設定。

**範例**：

將 API 端點設為 api.ng.bluemix.net：

```
bluemix api api.ng.bluemix.net
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

登入使用者。此指令會覆蓋 `cf login` 指令。指令選項與 `cf login` 指令選項相同。

```
bluemix login [OPTIONS...]
```

**必要條件**：端點

**指令選項**：如需 `login` 指令支援之選項的相關資訊，請參閱用於管理應用程式之 cf 指令的 `cf login` 指令用法資訊。


## bluemix logout
{: #bluemix_logout}

登出使用者。此指令會覆蓋 `cf logout` 指令。

```
bluemix logout
```

**必要條件**：無


## bluemix target
{: #bluemix_target}


設定或檢視目標組織或空間。此指令會覆蓋 `cf target` 指令。

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**必要條件**：端點、登入

**指令選項**：

-o *ORG_NAME*（選用）：要設為目標的組織名稱。

-s *SPACE_NAME*（選用）：要設為目標的空間名稱。

如果既未指定 -o *ORG_NAME* 也未指定 -s *SPACE_NAME*，則會顯示現行組織及空間。

**範例**：

將現行組織設為 `MyOrg`，並將空間設為 `MySpace`：

```
bluemix target -o MyOrg -s MySpace
```

檢視現行組織及空間：

```
bluemix target
```


## bluemix info
{: #bluemix_info}

檢視基本 {{site.data.keyword.Bluemix_notm}} 資訊，包括現行地區、雲端控制器版本以及部分有用端點（例如用於登入及交換存取記號的端點）。

```
bluemix info
```

**必要條件**：端點


## bluemix config
{: #bluemix_config}


將預設值寫入配置檔。

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**必要條件**：無

**指令選項**：

--http-timeout *TIMEOUT_IN_SECONDS*：HTTP 要求的逾時值。預設值為 60 秒。

--trace true|false|*path/to/file*：追蹤對終端機或指定檔案的 HTTP 要求。

--color true|false：啟用或停用顏色輸出。依預設，會啟用顏色輸出。

--locale *LOCALE*：設定預設語言環境。如果 LOCALE 為 *CLEAR*，則會刪除先前的語言環境。

一次只能指定其中一個選項。

**範例**：

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


## bluemix list
{: #bluemix_list}

列出現行空間中的所有 cf 應用程式、儲存器、儲存器群組及 VM 群組。

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**必要條件**：端點、登入、目標

**指令選項**：

apps（選用）：只顯示應用程式資訊。

containers（選用）：只顯示儲存器資訊。

container-groups（選用）：只顯示儲存器群組資訊。

vm-groups（選用）：只顯示 VM 群組資訊。

一次只能指定 `apps`、`containers`、`container-groups` 或 `vm-groups` 的其中之一。如果未指定其中任一個，則會列出所有 cf 應用程式、儲存器、儲存器群組及 VM 群組。

**範例**：

列出所有 cf 應用程式：

```
bluemix list apps
```

列出所有儲存器實例：

```
bluemix list containers
```

列出所有應用程式、儲存器、儲存器群組及 VM 群組：

```
bluemix list
```


## bluemix scale
{: #bluemix_scale}

將 cf 應用程式或儲存器群組橫向縮減或橫向擴充至指定的實例計數、磁碟限額及記憶體大小。

**附註：**調整儲存器群組時，只能指定實例數。如果未指定選項，此指令會列出儲存器群組的現行實例計數，也會列出 cf 應用程式的磁碟限額及記憶體大小。

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT][-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**必要條件**：端點、登入、目標

**指令選項**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必要）：要調整的 cf 應用程式或儲存器群組的名稱。

-i *INSTANCE_COUNT*（選用）：要調整的 cf 應用程式或儲存器群組的新實例數。此選項是要調整之儲存器群組的唯一有效選項。

-k *DISK_QUOTA*（選用）：cf 應用程式的新磁碟配額。無法用於調整儲存器群組。

-m *MEMORY_SIZE*（選用）：cf 應用程式的新記憶體大小。無法用於調整儲存器群組。

**範例**：

顯示 `my-container-group` 的現行實例數：

```
bluemix scale my-container-group
```

將 `my-container-group` 調整為 2 個實例：

```
bluemix scale my-container-group -i 2
```

將 `my-java-app` 調整為 3 個實例、8G 磁碟限額，以及 1024M 記憶體大小：

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
{: #bluemix_curl}

對 {{site.data.keyword.Bluemix_notm}} 執行原始 HTTP 要求。依預設，*Content-Type* 會設為 *application/json*。此指令會將要求傳送至「{{site.data.keyword.Bluemix_notm}} 多雲端控制 Proxy」。如需支援的路徑，請參閱 [CloudFoundry API 文件](http://apidocs.cloudfoundry.org/){: new_window}中的 API 路徑定義。

```
bluemix curl PATH [OPTIONS...]
```

**必要條件**：端點、登入

**指令選項**：

*PATH*（必要）：資源的 URL 路徑。例如，/v2/apps。

*OPTIONS*（選用）：`bluemix curl` 指令所支援的選項與 `cf curl` 指令的選項相同。

**範例**：

檢視現行帳戶的所有組織的資訊：

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

列出所有組織

```
bluemix iam orgs [-r REGION --guid]
```

**必要條件**：端點、登入

**指令選項**：

*-r REGION*（選用）：顯示其組織資訊的地區。如果設為 'all'，則會列出所有地區中的所有組織。

*--guid*（選用）：顯示組織的 GUID。

**範例**：列出已顯示 GUID 的 `us-south` 地區中的所有組織

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

顯示所指定組織的資訊。

```
bluemix iam org ORG_NAME [--guid]
```

**必要條件**：端點、登入

**指令選項**：

*ORG_NAME*（必要）：組織的名稱。

*--guid*（選用）：顯示組織的 GUID。


**範例**：顯示已顯示 GUID 的 `IBM` 組織的資訊

```
bluemix iam org IBM --guid
```

## bluemix iam org-create
{: #bluemix_iam_org_create}

建立新的組織。只有帳戶擁有者才能執行此作業。

```
bluemix iam org-create ORG_NAME
```

**必要條件**：端點、登入

**指令選項**：

*ORG_NAME*（必要）：所建立的組織的名稱。

**範例**：建立名稱為 `IBM` 的組織。

```
bluemix iam org-create IBM
```


## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

將組織從現行地區抄寫到另一個地區。

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**必要條件**：端點、登入

**指令選項**：

*ORG_NAME*（必要）：要抄寫的現有組織的名稱。

*REGION_NAME*（必要）：管理所抄寫組織的地區的名稱。

**範例**：

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

**必要條件**：端點、登入

**指令選項**：

*OLD_ORG_NAME*（必要）：要重新命名的組織的舊名稱。

*NEW_ORG_NAME*（必要）：組織重新命名後的新名稱。


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

刪除現行區域中的指定組織。

```
bluemix iam org-delete ORG_NAME [-f --all]
```

**必要條件**：端點、登入

**指令選項**：

*ORG_NAME*（必要）：要刪除的現有組織的名稱。

*-f*（選用）：強制刪除，而不進行確認。

*--all*（選用）：刪除所有地區中的組織。


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


## bluemix iam account-users
{: #bluemix_iam_account_users}

顯示與帳戶相關聯的使用者。只有帳戶擁有者才能執行此作業。

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


邀請使用者加入已設定組織和空間角色的帳戶。只有帳戶擁有者才能執行此作業。

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

**必要條件**：端點、登入


**指令選項**：

*USER_NAME*（必要）：所邀請的使用者的名稱。

*ORG_NAME*（必要）：邀請此使用者加入的組織的名稱。

*ORG_ROLE*（必要）：邀請此使用者加入的組織角色的名稱。例如：

<dl>
<dt>OrgManager</dt>
<dd>此角色可以邀請和管理使用者、選取和變更方案，以及設定消費限制。</dd>
<dt>BillingManager</dt>
<dd>此角色可以建立和管理計費帳戶及付款資訊。</dd>
<dt>OrgAuditor</dt>
<dd>此角色具有組織資訊和報告的唯讀權。</dd>
</dl> 

*SPACE_NAME*（必要）：邀請此使用者加入的空間的名稱。

*SPACE_ROLE*（必要）：邀請此使用者加入的空間角色的名稱。例如：

<dl>
<dt>SpaceManager</dt>
<dd>此角色可以邀請和管理使用者，以及啟用給定空間的特性。</dd>
<dt>SpaceDeveloper</dt>
<dd>此角色可以建立和管理應用程式及服務，以及查看日誌和報告。</dd>
<dt>SpaceAuditor</dt>
<dd>此角色可以檢視空間的日誌、報告和設定。</dd>
</dl> 

**範例**：

以 `OrgManager` 角色，邀請使用者 `Mary` 加入組織 `IBM`，以及以 `SpaceAuditor` 角色加入空間 `Cloud`：

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

依角色顯示指定組織中的使用者。

```
bluemix iam org-users ORG_NAME [-a]
```

**必要條件**：端點、登入

**指令選項**：

*ORG_NAME*（必要）：組織的名稱。

*-a*（選用）：列出指定組織中的所有使用者，而不依角色進行分組。


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

將組織角色指派給使用者。只有組織管理員才能執行此作業。

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

**必要條件**：端點、登入

**指令選項**：

*USER_NAME*（必要）：所指派的使用者的名稱。

*ORG_NAME*（必要）：獲指派此使用者的組織的名稱。

*ORG_ROLE*（必要）：獲指派此使用者的組織角色的名稱。例如：

<dl>
<dt>OrgManager</dt>
<dd>此角色可以邀請和管理使用者、選取和變更方案，以及設定消費限制。</dd>
<dt>BillingManager</dt>
<dd>此角色可以建立和管理計費帳戶及付款資訊。</dd>
<dt>OrgAuditor</dt>
<dd>此角色具有組織資訊和報告的唯讀權。</dd>
</dl> 

**範例**：

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

**必要條件**：端點、登入

**指令選項**：

*USER_NAME*（必要）：所移除的使用者的名稱。

*ORG_NAME*（必要）：從中移除此使用者的組織的名稱。

*ORG_ROLE*（必要）：從中移除此使用者的組織角色的名稱。例如：

<dl>
<dt>OrgManager</dt>
<dd>此角色可以邀請和管理使用者、選取和變更方案，以及設定消費限制。</dd>
<dt>BillingManager</dt>
<dd>此角色可以建立和管理計費帳戶及付款資訊。</dd>
<dt>OrgAuditor</dt>
<dd>此角色具有組織資訊和報告的唯讀權。</dd>
</dl> 

**範例**：

以 `OrgManager` 角色，從組織 `IBM` 中移除使用者 `Mary`：

```
bluemix iam org-role-unset Mary IBM OrgManager
```


## bluemix iam space-users
{: #bluemix_iam_space_users}

依角色顯示指定空間中的使用者。

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

**必要條件**：端點、登入

**指令選項**：

*ORG_NAME*（必要）：組織的名稱

*SPACE_NAME*（必要）：空間的名稱。


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

將空間角色指派給使用者。只有空間管理員才能執行此作業。

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**必要條件**：端點、登入

**指令選項**：

*USER_NAME*（必要）：所指派的使用者的名稱。

*ORG_NAME*（必要）：獲指派此使用者的組織的名稱。

*SPACE_NAME*（必要）：獲指派此使用者的空間的名稱。

*SPACE_ROLE*（必要）：獲指派此使用者的空間角色的名稱。例如：

<dl>
<dt>SpaceManager</dt>
<dd>此角色可以邀請和管理使用者，以及啟用給定空間的特性。</dd>
<dt>SpaceDeveloper</dt>
<dd>此角色可以建立和管理應用程式及服務，以及查看日誌和報告。</dd>
<dt>SpaceAuditor</dt>
<dd>此角色可以檢視空間的日誌、報告和設定。</dd>
</dl> 


**範例**：

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

**必要條件**：端點、登入

**指令選項**：

*USER_NAME*（必要）：所移除的使用者的名稱。

*ORG_NAME*（必要）：從中移除此使用者的組織的名稱。

*SPACE_NAME*（必要）：從中移除此使用者的空間的名稱。

*SPACE_ROLE*（必要）：從中移除此使用者的空間角色的名稱。例如：

<dl>
<dt>SpaceManager</dt>
<dd>此角色可以邀請和管理使用者，以及啟用給定空間的特性。</dd>
<dt>SpaceDeveloper</dt>
<dd>此角色可以建立和管理應用程式及服務，以及查看日誌和報告。</dd>
<dt>SpaceAuditor</dt>
<dd>此角色可以檢視空間的日誌、報告和設定。</dd>
</dl> 

**範例**：

以 `SpaceManager` 角色，從組織 `IBM` 和空間 `Cloud` 中移除使用者 `Mary`：

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

此指令的函數及選項與 `cf push` 指令相同。


## bluemix app list
{: #bluemix_app_list}

此指令的函數及選項與 `cf apps` 指令相同。


## bluemix app show
{: #bluemix_app_show}

此指令的函數及選項與 `cf app` 指令相同。


## bluemix app scale
{: #bluemix_app_scale}

此指令的函數及選項與 `cf scale` 指令相同。


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


## bluemix app stack
{: #bluemix_app_stack}

此指令的函數及選項與 `cf stack` 指令相同。


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

此指令的函數及選項與 `cf create-app-manifest` 指令相同。


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

**必要條件**：端點、登入

**指令選項**：

-d（選用）：如果指定了 `-d` 選項，也會顯示每一個範本的說明。否則，只會顯示每一個範本的 ID 及名稱。


## bluemix catalog template
{: #bluemix_catalog_template}

檢視所指定樣板範本的詳細資訊。

```
bluemix catalog template TEMPLATE_ID
```

**必要條件**：端點、登入

**指令選項**：

*TEMPLATE_ID*（必要）：樣板範本的 ID。請使用 'bluemix templates' 來檢視所有範本的 ID。

**範例**：

檢視範本 `mobileBackendStarter` 的詳細資料：

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

以指定的 URL 及說明，建立根據所指定範本的 cf 應用程式。依預設，新的應用程式會自動啟動。

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**必要條件**：端點、登入、目標

**指令選項**：

*TEMPLATE_ID*（必要）：應用程式在建立時將根據的範本。使用 `bluemix templates` 來查看所有範本 ID。

*CF_APP_NAME*（必要）：要建立之 cf 應用程式的名稱。

-u *URL*（選用）：應用程式的路徑。如果未指定，{{site.data.keyword.Bluemix_notm}} 會自動根據應用程式名稱及預設網域來設定路徑。

-d *DESCRIPTION*（選用）：應用程式的說明。

--no-start（選用）：在建立應用程式之後，請不要將它自動啟動。如果未指定，應用程式會在建立之後自動啟動。

**範例**：

根據 `javaHelloWorld` 範本建立 cf 應用程式 `my-app`：

```
bluemix catalog template-run javaHelloWorld my-app
```

根據 `rubyHelloWorld` 範本建立應用程式 `my-ruby-app`，路徑為 `myrubyapp.ng.bluemix.net`，說明為 `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`：

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

根據 `pythonHelloWorld` 範本建立應用程式 `my-python-app`，不自動啟動：

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
{: #bluemix_network_regions}

檢視 {{site.data.keyword.Bluemix_notm}} 上所有地區的資訊。

```
bluemix network regions
```

**必要條件**：端點


## bluemix network region-set
{: #bluemix_network_region_set}

切換至指定的地區。此指令會自動將目標重設為新地區中相同的組織及空間（可能的話）。否則，指令會提示使用者選取新的組織及空間（如果使用者已登入的話）。API 端點會相應地變更。

```
bluemix network region-set REGION_NAME
```

**必要條件**：端點

**指令選項**：

*REGION_NAME*（必要）：要切換至的地區名稱。您可以使用 `bluemix network regions` 指令來查看所有地區名稱。

**範例**：

將現行地區設為 `eu-gb`：

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

此指令的函數及選項與 `cf routes` 指令相同。


## bluemix network route-check
{: #bluemix_network_route_check}

此指令的函數及選項與 `cf check-route` 指令相同。


## bluemix network route-map
{: #bluemix_network_route_map}

將路徑對映至具有所指定網域及主機名稱的現有 cf 應用程式或儲存器群組。

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**必要條件**：端點、登入、目標

**指令選項**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必要）：要使用路徑對映之 cf 應用程式或儲存器群組的名稱。

*DOMAIN*（必要）：路徑的網域。例如，mybluemix.net 或 ng.bluemix.net。 

-n *HOST_NAME*（選用）：路徑的主機名稱。如果未提供，則依預設會將主機名稱設為應用程式名稱或儲存器群組名稱。

**範例**：

使用指定的網域將路徑對映到 `my-app`：

```
bluemix network route-map my-app mybluemix.net
```

以指定的網域及主機名稱對映將路徑對映至 'my-container-group'：

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
{: #bluemix_network_route_unmap}

從現有的 cf 應用程式或儲存器群組中取消對映指定的路徑。

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**必要條件**：端點、登入、目標

**指令選項**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必要）：cf 應用程式或儲存器群組的名稱。

*DOMAIN*（必要）：路徑的網域（例如，mybluemix.net 或 ng.bluemix.net）。 

-n *HOST_NAME*（選用）：路徑的主機名稱。如果未提供，則依預設會將主機名稱設為應用程式名稱或儲存器群組名稱。

**範例**：

從 `my-app` 取消對映 `my-app.mybluemix.net`：

```
bluemix network route-unmap my-app mybluemix.net
```

從 `my-container-group` 取消對映 `abc.ng.bluexmix.net`：

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
{: #bluemix_network_route_create}

此指令的函數及選項與 `cf create-route` 指令相同。


## bluemix network route-delete
{: #bluemix_network_route_delete}

此指令的函數及選項與 `cf delete-route` 指令相同。


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

此指令的函數及選項與 `cf delete-orphaned-routes` 指令相同。


## bluemix network domains
{: #bluemix_network_domains}

此指令的函數及選項與 `cf domains` 指令相同。


## bluemix network domain-create
{: #bluemix_network_domain_create}

此指令的函數及選項與 `cf create-domain` 指令相同。


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

此指令的函數及選項與 `cf delete-domain` 指令相同。


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

此指令的函數及選項與 `cf create-shared-domain` 指令相同。


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

此指令的函數及選項與 `cf delete-shared-domain` 指令相同。


## bluemix security cert
{: #bluemix_security_cert}

列出網域的憑證資訊。

```
bluemix security cert DOMAIN_NAME
```

**必要條件**：端點、登入

**指令選項**：

*DOMAIN_NAME*（必要）：管理憑證的網域。

**範例**：

檢視網域 `ibmcxo-eventconnect.com` 的憑證資訊：

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

將憑證新增到現行組織中的指定網域。

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**必要條件**：端點、登入、目標

**指令選項**：

*DOMAIN*（必要）：將憑證新增到其中的網域。

-k *PRIVATE_KEY_FILE*（必要）：私密金鑰檔案路徑。

-c *CERT_FILE*（必要）：憑證檔案路徑。

-p *PASSWORD*（選用）：憑證的密碼。

-i *INTERMEDIATE_CERT_FILE*（選用）：中繼憑證檔案路徑。

--verify-client（選用）：是否啟用用戶端憑證驗證。

**範例**：

將憑證新增到網域 `ibmcxo-eventconnect.com`：

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
{: #bluemix_security_cert_remove}

從現行組織中的指定網域移除憑證。

```
bluemix security cert-remove DOMAIN [-f]
```

**必要條件**：端點、登入、目標

**指令選項**：

*DOMAIN*（必要）：要從中移除憑證的網域。

-f（選用）：強制刪除，而不進行確認。







## bluemix plugin repos
{: #bluemix_plugin_repos}

列出 {{site.data.keyword.Bluemix_notm}} CLI 中登錄的所有外掛程式儲存庫。

```
bluemix plugin repos
```

**必要條件**：無


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

將新的外掛程式儲存庫新增至 {{site.data.keyword.Bluemix_notm}} CLI。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**必要條件**：無

**指令選項**：

*REPO_NAME*（必要）：要新增之儲存庫的名稱。您可以為每一個儲存庫定義專屬名稱。

*REPO_URL*（必要）：要新增之儲存庫的 URL。儲存庫 URL 必須包含通訊協定（例如，http://plugins.ng.bluemix.net 而非 plugins.ng.bluemix.net）。http://plugins.ng.bluemix.net 是 {{site.data.keyword.Bluemix_notm}} CLI 的正式外掛程式儲存庫。

**範例**：

將 Bluemix CLI 的官方外掛程式儲存庫新增為 `bluemix-repo`：

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

從 {{site.data.keyword.Bluemix_notm}} CLI 中移除外掛程式儲存庫。

```
bluemix plugin repo-remove REPO_NAME
```

**必要條件**：無

**指令選項**：

*REPO_NAME*（必要）：要移除之儲存庫的名稱。

**範例**：

從 {{site.data.keyword.Bluemix_notm}} CLI 中移除 `bluemix-repo` 儲存庫：

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

列出所有已新增之儲存庫或特定儲存庫中所有可用的外掛程式。

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

**必要條件**：無

**指令選項**：

-r *REPO_NAME*（選用）：只列出指定儲存庫中的外掛程式。

**範例**：

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

**必要條件**：無


## bluemix plugin install
{: #bluemix_plugin_install}

從指定的路徑或儲存庫將特定版本的外掛程式安裝到 {{site.data.keyword.Bluemix_notm}} CLI 中。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**必要條件**：無

**指令選項**：

*PLUGIN_PATH*|*PLUGIN_NAME*（必要）：如果未指定 `-r *REPO_NAME*`，則會從指定的本端路徑或遠端 URL 安裝外掛程式。

-r *REPO_NAME*（選用）：外掛程式二進位檔所在儲存庫的名稱。-v *VERSION*（選用）：要安裝的外掛程式的版本。如果未提供，將安裝外掛程式的最新版本。只有從儲存庫安裝外掛程式時，此選項才有效。

**範例**：

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






## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

從 {{site.data.keyword.Bluemix_notm}} CLI 解除安裝指定的外掛程式。

```
bluemix plugin uninstall PLUGIN_NAME
```

**必要條件**：無

**指令選項**：

*PLUGIN_NAME*（必要）：要解除安裝之外掛程式的名稱。

**範例**：

解除安裝先前安裝的 `IBM-Containers` 外掛程式：

```
bluemix plugin uninstall IBM-Containers
```


## bluemix ic init
{: #bluemix_ic_init}

起始設定本端機器上的 containers 環境，以使用 IBM Containers 服務的完整功能。

```
bluemix ic init
```

**必要條件**：端點、登入、目標

**附註：**起始設定之前，請確定 PATH 環境變數中已安裝並配置 Docker CLI (Docker)。若要切換至其他地區，請使用 `bluemix region-set` 指令。 

**範例**：

切換至 `us-south` 地區：

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

控制執行中儲存器，或檢視其輸出。使用 `CTRL+C` 以結束並停止儲存器。此指令會呼叫 Docker CLI。如需相關資訊，請參閱 Docker 說明中的 [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} 指令。 

```
bluemix ic attach [--no-stdin][--sig-proxy] CONTAINER
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

--no-stdin（選用）：不包括標準輸入。

--sig-proxy（選用）：將所有接收到的信號 Proxy 到處理程序。預設值為 **true**。

*CONTAINER*（必要）：儲存器名稱或 ID。

**範例**：

下列範例顯示連接至儲存器 `my_container` 的要求：
```
bluemix ic attach my_container
```


## bluemix ic build
{: #bluemix_ic_build}

呼叫 IBM Containers 建置服務，以在本端或專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中建置 Docker 映像檔。此指令會呼叫 Docker CLI。如需相關資訊，請參閱 Docker 說明中的 [build](https://docs.docker.com/reference/commandline/build/){: new_window} 指令。 

```
bluemix ic build -t TAG|--tag TAG [--no-cache][-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

-t *TAG*|--tag *TAG*（必要）：要套用至所建立映像檔的儲存庫名稱。

--no-cache（選用）：建置映像檔時不要使用快取。預設值為 **false**。

-p|--pull（選用）：嘗試從登錄中取回基礎映像檔，即使已快取也是一樣。

-q|--quiet（選用）：抑制儲存器所產生的詳細輸出。預設值為 **false**。

*DOCKERFILE_LOCATION*（必要）：本端主機上 Dockerfile 及環境定義的路徑。

**範例**：

下列範例顯示建置名為 *myimage* 之映像檔的要求。Dockerfile 及其他要在建置中使用的構件，位於執行指令的同一目錄中。因為登錄及名稱空間隨附於映像檔名稱，所以映像檔會建置在您組織的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中。
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic create
{: #bluemix_ic_create}

在 {{site.data.keyword.Bluemix_notm}} 儲存庫中，建立新儲存器。此指令會覆蓋 `docker create` 指令。如需相關資訊，請參閱 Docker 說明中的 [create](https://docs.docker.com/reference/commandline/create/){: new_window} 指令。


## bluemix ic cpi
{: #bluemix_ic_cpi}

存取「Docker 中心」映像檔或本端登錄中的映像檔，並將映像檔複製到您的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫。

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

**必要條件**：端點、登入、目標

**指令選項**：

*SOURCE_IMAGE*（必要）：來源儲存庫及映像檔名稱。

*DESTINATION_IMAGE*（必要）：專用 {{site.data.keyword.Bluemix_notm}} 儲存庫 URL（包含名稱空間及目的地映像檔名稱）。映像檔的標記是選用性的。

**範例**：

將映像檔從來源儲存庫複製到專用儲存庫，並新增映像檔的標記：

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

將 `sinatra` 映像檔從 `training` 儲存庫複製到專用儲存庫 `registry.ng.bluemix.net/mynamespace`，並將映像檔命名為 `mysinatra`。請新增映像檔 `mysinatra` 的標記 `v1`。 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


在儲存器內執行指令。如需相關資訊，請參閱 Docker 說明中的 [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} 指令。

```
bluemix ic exec [-d|--detach][-it] [-u USER|--user USER] CONTAINER [CMD]
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

-d|--detach（選用）：在背景中執行指定的指令。

-it（選用）：互動模式。請持續顯示標準輸入。鍵入 'exit' 以結束。

-u *USER*|--user *USER*（選用）：使用者名稱。

*CONTAINER*（必要）：儲存器名稱或 ID。

*CMD*（選用）：要在指定的一或數個儲存器內執行的指令。

**範例**：

以互動模式，執行 `my_container` 儲存器內的 `bash` 指令：

```
bluemix ic exec -it my_container bash
```

執行 `my_container` 儲存器內的 `date` 指令：

```
bluemix ic exec my_container date
```


## bluemix ic groups
{: #bluemix_ic_groups}

列出組織的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中的儲存器群組。

```
bluemix ic groups
```

**必要條件**：端點、登入、目標


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

檢視在建立儲存器群組時針對它所指定的詳細資訊，例如環境變數、埠或記憶體。

```
bluemix ic group-inspect CONTAINER_GROUP
```

**必要條件**：端點、登入、目標

**指令選項**：

*CONTAINER_GROUP*（必要）：儲存器群組 ID 或名稱。

**範例**：

下列範例顯示檢查儲存器群組 `my_group` 的要求：
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

列出所指定儲存器群組的實例。

```
bluemix ic group-instances CONTAINER_GROUP
```

**必要條件**：端點、登入、目標

**指令選項**：

*CONTAINER_GROUP*（必要）：儲存器群組 ID 或名稱。

**範例**：

列出儲存器群組 `my_group` 的所有實例：
```
bluemix ic group-instances my_group
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

建立可擴充儲存器群組。

```
bluemix ic group-create [-p PORT|--publish port][-m MEMORY|--memory MEMORY] [-e ENV|--env ENV][-v VOLUME:CONTAINER_PATH] [--min MIN][--max MAX] [--desired DESIRED][--auto] [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] [--name NAME] IMAGE [CMD]
```

**必要條件**：端點、登入、目標

**指令選項**：

-m *MEMORY*|--memory *MEMORY*（選用）：指派給群組的記憶體限制 (MB)。從 CLI 建立儲存器群組時，每一個儲存器實例的預設值都是 `64` MB。從 {{site.data.keyword.Bluemix_notm}}「儀表板」建立儲存器群組時，每一個儲存器實例的預設值都是 `256` MB。接受值是 `64`、`256`、`512`、`1024` 及 `2048`。指派記憶體限制之後，即無法變更其值。

-e *ENV*|--env *ENV*（選用）：設定環境變數，其中 **ENV** 是 `key=value` 配對。個別列出多個索引鍵。如果包括引號，請用它們括住環境變數名稱及值。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。下表顯示一些您可以指定的常用環境變數：

|  環境變數                              |     說明                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 將服務連結至儲存器。使用 'CCS_BIND_APP' 環境變數，以將應用程式連結至儲存器。應用程式會連結至目標服務，並作為橋接器，以容許 {{site.data.keyword.Bluemix_notm}} 將您橋接器應用程式的 `VCAP_SERVICES` 資訊帶入執行中儲存器實例。如需建立橋接器應用程式的相關資訊，請參閱[將服務連結至儲存器](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}。 |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | 建立儲存器時，在其中新增 SSH 金鑰。從 {{site.data.keyword.Bluemix_notm}} 儀表板或從 CLI 建立儲存器時，您可以使用環境變數來新增 SSH 金鑰。如需 SSH 金鑰的相關資訊，請參閱[登入儲存器](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 新增要在儲存器中監視的日誌檔。包括含有日誌檔路徑的 `LOG_LOCATIONS` 環境變數。 |
*表 1. 常用環境變數*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  （選用）：以 `VolumeId:ContainerPath[:ro]` 格式指定詳細資料，將磁區連接至儲存器。

- *VOLUME*：磁區 ID 或名稱。
- *CONTAINER_PATH*：儲存器中磁區的絕對路徑。
- ro：選用。指定 'ro' 會使磁區變成唯讀，而不是預設的讀寫。

-p *PORT*|--publish *PORT*（選用）：公開 HTTP 資料流量的埠。群組中的儲存器必須接聽 HTTP 埠。無法提出 HTTPS 要求。若為儲存器群組，您無法包含多個埠。

在您指定埠時，即將應用程式設為可供「{{site.data.keyword.Bluemix_notm}} 負載平衡器」或相同 {{site.data.keyword.Bluemix_notm}} 空間中嘗試連接主機的儲存器使用。然後，{{site.data.keyword.Bluemix_notm}} 負載平衡器或儲存器可以使用此埠來連接相同 {{site.data.keyword.Bluemix_notm}} 空間中的主機和應用程式。如果在 Dockerfile 中針對您要使用的映像檔指定了埠，請包含該埠。

**提示：**

- 對於 IBM 認證的 Liberty Server 映像檔或此映像檔的已修改版本，請輸入埠 9080。
- 對於 IBM 認證的 Node.js 映像檔或此映像檔的已修改版本，請輸入埠 8000。

--min *MIN*（選用）：實例數下限。預設值為 **1**。如果設定實例數下限，則在建立儲存器群組之後，無法變更此值。

--max *MAX*（選用）：實例數上限。預設值為 **2**。如果設定實例數上限，則在建立儲存器群組之後，無法變更此值。

--desired *DESIRED*（選用）：所需的實例數。預設值為 **2**。

--auto（選用）：建立儲存器群組並啟用自動回復時，IBM Containers 會使用對所指派埠的 HTTP 要求，來檢查每一個實例的性能。

如果您未在兩個後續 90 秒間隔內收到來自儲存器實例的回應，則會移除實例，並將其取代為新的實例。如果儲存器回應，則不需要採取任何動作。此處理程序會不斷地重複。在 30 分鐘時間範圍期間，如果本身為群組成員的不同儲存器總數等於或超出觀察到的群組大小上限的 3 倍，則會永久停用儲存器群組的自動回復。若要重新啟用自動回復，您必須重建儲存器群組。

-n *HOST*|--hostname *HOST*（選用）：主機名稱，例如 'mycontainerhost'。主機與網域會合併，以構成完整公用路徑 URL，例如 'http://mycontainerhost.mybluemix.net'。在使用 'bluemix ic group-inspect' 指令檢閱儲存器群組的詳細資料時，主機與網域會一起列出，作為路徑。

-d *DOMAIN*|--domain *DOMAIN*（選用）：網域通常為 `.mybluemix.net`。主機與網域會合併，以構成完整公用路徑 URL，例如 `http://mycontainerhost.mybluemix.net`。在使用 `bluemix ic group-inspect` 指令檢閱儲存器群組的詳細資料時，主機與網域會一起列出，作為路徑。

--name *NAME*（必要）：指派群組的名稱。`-n` 已淘汰。

**提示：**儲存器名稱必須以字母開頭。名稱可以包括大寫字母、小寫字母、數字、句點 `.`、底線 `_` 或連字號 `-`。

*IMAGE*（必要）：要併入儲存器群組中每一個儲存器實例的映像檔。您可以在映像檔之後列出指令，但不能在映像檔之後放置任何選項。請在指定映像檔之前併入所有選項。

如果您使用組織專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中的映像檔，請以下列格式指定映像檔：`registry.ng.bluemix.net/NAMESPACE/IMAGE`。

如果您使用 IBM Containers 所提供的映像檔，請不要併入您組織的名稱空間。請以下列格式指定映像檔：`registry.ng.bluemix.net/IMAGE`。

*CMD*（選用）：傳遞給儲存器群組執行的指令及引數。這個指令必須是長時間執行的指令。請不要使用不會執行很久的短期指令（例如，**/bin/date**），因為短期指令可能會導致儲存器損毀。

**附註：**
- 指令及其引數必須在 `bluemix ic run` 指令行的結尾。
- 如果指令引數包括連字號 `-`（如前一個範例指令中的 `-c`），則指令前面必須有兩個連字號 `--`。



**範例**：

使用 IBM Containers 所提供的 `registry.ng.bluemix.net/ibmnode` 映像檔來建立儲存器群組 `my_container_group`，然後在該儲存器群組上執行 `ping localhost` 長時間執行指令：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

使用 IBM Containers 所提供的 `registry.ng.bluemix.net/ibmnode` 映像檔來建立儲存器群組 `my_container_group`，然後在該儲存器群組上執行 `tail -f /dev/null` 長時間執行指令：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

使用 `registry.ng.bluemix.net/ibmliberty` 映像檔，以建立已啟用自動回復的可擴充群組 `mygroup`。埠是 `9080`、主機名稱是 `mycontainerhost`、網域名稱是 `.mybluemix.net`。
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d .mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

更新儲存器群組。


```
bluemix ic group-update [--min MIN][--max MAX] [--desired DESIRED][--auto] CONTAINER_GROUP
```

**提示：**若要更新儲存器群組的主機名稱或網域，請使用 `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`。

**必要條件**：端點、登入、目標

**指令選項**：

--min *MIN*（選用）：實例數下限。預設值為 **1**。在設定實例數下限之後，無法變更此值。

--max *MAX*（選用）：實例數上限。預設值為 **2**。在設定實例數上限之後，無法變更此值。

--desired *DESIRED*（選用）：所需的實例數。預設值為 **2**。

**提示：**一次只能指定下列其中一個選項：`--min MIN`、`--max MAX` 或 `--desired DESIRED`。

--auto（選用）：透過啟用自動回復來自動重新啟動失敗的實例。

*CONTAINER_GROUP*（必要）：儲存器群組 ID 或名稱。

**範例**：

下列範例顯示更新儲存器群組 `my_group` 的要求：
```
bluemix ic group-update --max 5 my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

從組織的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中移除儲存器群組。

```
bluemix ic group-remove [-f|--force] CONTAINER_GROUP
```

**必要條件**：端點、登入、目標

**指令選項**：

-f|--force（選用）：強制移除執行中或失敗的儲存器。

*CONTAINER_GROUP*（必要）：儲存器群組 ID 或名稱。

**範例**：

下列範例顯示移除儲存器群組的要求，其中 `my_group` 是儲存器群組的名稱。
```
bluemix ic group-remove my_group
```


## bluemix ic images
{: #bluemix_ic_images}

檢視組織專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中所有可用映像檔的清單。如需相關資訊，請參閱 Docker 說明中的 [images](https://docs.docker.com/reference/commandline/images){: new_window} 指令。此清單包括映像檔 ID、建立日期及映像檔名稱。

```
bluemix ic images [-a|--all][--no-trunc] [-q|--quiet]
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

-a|--all（選用）：包括組織儲存庫中每一個映像檔的所有映像檔層，而不只是最新的層。

--no-trunc（選用）：不截斷輸出。

-q|--quiet（選用）：只顯示數值 ID。

**範例**：

下列範例顯示接收組織可用映像檔清單的要求：
```
bluemix ic images
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

檢視儲存器的相關資訊。如需相關資訊，請參閱 Docker 說明中的 [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} 指令。

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

*IMAGE*（必要）：指定映像檔名稱或 ID，以檢視特定映像檔的詳細資訊。

images（必要）：檢視儲存庫中所有映像檔的詳細資訊。

*CONTAINER*（必要）：指定儲存器名稱或 ID，以檢視特定儲存器的詳細資訊。

**提示：**一次只能指定下列其中一個選項：*IMAGE*、images 或 *CONTAINER*。 

**範例**：

下列範例顯示檢查名為 `proxy` 之儲存器的要求：
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

檢視一組資訊，說明儲存器雲端服務實例的狀態。這項資訊包括儲存器限制、儲存器用量、執行中的儲存器、記憶體限制、記憶體用量、浮動 IP 位址限制、浮動 IP 位址用量、CCS 主機 URL、登錄主機 URL 及除錯模式狀態。

```
bluemix ic info
```

**必要條件**：端點、登入、目標


## bluemix ic ips
{: #bluemix_ic_ips}

列出已登入使用者的可用浮動 IP 位址。這份清單包括 IP 位址以及 IP 位址所鏈結的儲存器 ID。如果 IP 位址未使用，則不會顯示儲存器 ID。

```
bluemix ic ips [-a|--all]
```

**必要條件**：端點、登入、目標

**指令選項**：

-a|--all（選用）：列出所有 IP 位址。依預設，只會傳回可用的 IP 位址。

**範例**：

下列範例顯示接收組織之所有 IP 位址（不論是否可用）清單的要求。
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
要求新的浮動 IP 位址。

```
bluemix ic ip-request
```

**必要條件**：端點、登入、目標


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

釋放儲存器雲端服務實例中的浮動 IP 位址。

```
bluemix ic ip-release IP_ADDRESS
```

**必要條件**：端點、登入、目標

**指令選項**：

*IP_ADDRESS*（必要）：要釋放的 IP 位址。


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

將可用的浮動 IP 位址連結至儲存器。

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

**必要條件**：端點、登入、目標

**指令選項**：

*IP_ADDRESS*（必要）：要連結的 IP 位址。

*CONTAINER*（必要）：要連結的儲存器 ID 或名稱。

**範例**：

下列範例顯示將 IP 位址 `192.123.12.12` 連結至儲存器 `proxy` 的要求：
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

取消浮動 IP 位址與其儲存器的連結。

公用 IP 位址是 IBM Containers 中的有限資源。因此，大約每週會從免費試用版使用者定期收回已配置給空間但未連結至儲存器的公用 IP 位址。不過，絕不會從隨收隨付制或訂閱客戶收回已解除連結的公用 IP 位址。

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

**必要條件**：端點、登入、目標

**指令選項**：

*IP_ADDRESS*（必要）：要取消連結的 IP 位址。

*CONTAINER*（必要）：要取消連結的儲存器 ID 或名稱。

**範例**：

下列範例顯示取消 IP 位址 `192.123.12.12` 與儲存器 `proxy` 的連結的要求：
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

停止儲存器中的執行中處理程序，而不停止儲存器。如需相關資訊，請參閱 Docker 說明中的 [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} 指令。

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

-s *CMD*|--signal *CMD*（選用）：將指令傳送給正在儲存器中執行的處理程序。

*CONTAINER*（必要）：儲存器 ID 或名稱。

**範例**：

下列範例顯示結束 (kill) 名為 `proxy` 之儲存器中處理程序的要求：
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

檢視所登入組織之專用 {{site.data.keyword.Bluemix_notm}} 映像檔儲存庫的名稱。

```
bluemix ic namespace-get
```

**必要條件**：端點、登入、目標


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

設定所登入組織之專用 {{site.data.keyword.Bluemix_notm}} 映像檔儲存庫的名稱。

*限制*：您不能在儲存庫名稱空間名稱中使用連字號 `-`。

```
bluemix ic namespace-set NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*NAME*（必要）：一次性函數，可設定您組織的儲存庫名稱空間（如果尚未設定的話）。在您設定名稱空間之後，請先透過 `bluemix ic init` 指令重新起始設定 IBM Containers，然後再繼續進行。


## bluemix ic pause
{: #pause}

暫停執行中儲存器內的所有處理程序。如需相關資訊，請參閱 Docker 說明中的 [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} 指令。若要停止儲存器，請參閱 [bluemix ic unpause](#unpause) 指令。

```
bluemix ic pause CONTAINER
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

*CONTAINER*（必要）：儲存器名稱或 ID。

**回應**：

- 已順利暫停儲存器。

- 儲存器雲端服務的指令失敗

 `{message}`
  
 其中 `{message}` 是相關的錯誤。
 
- 指令失敗 - 無法連接至儲存器雲端服務

**範例**：

下列範例顯示暫停名為 `proxy` 之儲存器的要求：
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

取消暫停執行中儲存器內的所有處理程序。如需相關資訊，請參閱 Docker 說明中的 [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} 指令。若要暫停儲存器，請參閱 [bluemix ic pause](#pause) 指令。

```
bluemix ic unpause CONTAINER
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

*CONTAINER*（必要）：儲存器名稱或 ID。

**回應**：

- 已順利取消暫停儲存器。

- 儲存器雲端服務的指令失敗 

 `{message}` 
 
 其中 `{message}` 是相關的錯誤。
 
- 指令失敗 - 無法連接至儲存器雲端服務

**範例**：

下列範例顯示取消暫停名為 `proxy` 之儲存器的要求：
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

列出儲存器的埠對映或特定對映。此指令會覆蓋 `docker port` 指令。如需相關資訊，請參閱 Docker 說明中的 [port](https://docs.docker.com/reference/commandline/port/){: new_window} 指令。


## bluemix ic ps
{: #bluemix_ic_ps}
檢視已登入使用者之名稱空間中的執行中儲存器清單。此指令預設只會顯示執行中儲存器。如需相關資訊，請參閱 Docker 說明中的 [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} 指令。

```
bluemix ic ps [-a|--all][-s|--size] [-l NUM|--limit NUM][-q|--quiet]
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

-a|--all（選用）：顯示所有儲存器（包括執行中及已停止）。

-s|--size（選用）：列出儲存器的大小。

-l *NUM*|--limit *NUM*（選用）：列出最近建立的儲存器，其中 *NUM* 是您要傳回的最近建立儲存器數目。

例如，如果您已依序建立儲存器 'node1' 到 'node5'，則指令 'bluemix ic ps --limit 2' 會傳回 node4 及 node5，因為它們是最後兩個建立的儲存器。

-q|--quiet（選用）：只顯示儲存器 ID。

**範例**：

下列範例顯示查看所有執行中及已停止儲存器的要求：
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

重新啟動儲存器。如需相關資訊，請參閱 Docker 說明中的 [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} 指令。

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

*CONTAINER*（必要）：儲存器名稱或 ID。

-t *SECS*|--time *SECS*（選用）：重新啟動儲存器之前所要等待的秒數。

**回應**：

- 已順利重新啟動儲存器。

- 儲存器雲端服務的指令失敗 

 `{message}` 
 
 其中 `{message}` 是相關的錯誤。
 
- 指令失敗 - 無法連接至儲存器雲端服務

**範例**：

下列範例顯示重新啟動名為 `proxy` 之儲存器的要求：
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

移除儲存器。如需相關資訊，請參閱 Docker 說明中的 [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} 指令。

```
bluemix ic rm [-f|--force] CONTAINER
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

-f|--force（選用）：強制移除執行中或失敗的儲存器。

*CONTAINER*（必要）：儲存器名稱或 ID。

**回應**：

- 已順利移除儲存器。

- 儲存器雲端服務的指令失敗 

 `{message}` 
 
 其中 `{message}` 是相關的錯誤。
 
- 指令失敗 - 無法連接至儲存器雲端服務。

**範例**：

下列範例顯示移除名為 `proxy` 之儲存器的要求：
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

移除已登入使用者之名稱空間中的映像檔。如需相關資訊，請參閱 Docker 說明中的 [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} 指令。

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

-R *REGISTRY*|--registry *REGISTRY*（選用）：變更登錄主機。預設值為使用您在 `bluemix ic init` 指令中指定的登錄。

*IMAGE*（必要）：您要移除之映像檔的名稱。如果映像檔名稱中未指定標籤，則預設會刪除標記為 `latest` 的映像檔。

**回應**：

- 已移除：`{IMAGE}`

 其中 `{IMAGE}` 是已移除之映像檔的名稱。
 
- 錯誤！未指定任何登錄主機。

- 映像檔移除失敗 - 無法連接至儲存器雲端登錄

- 儲存器雲端服務的指令失敗 

 `{message}`
 
 其中 `{message}` 是相關的錯誤。

**範例**：

下列範例顯示移除映像檔 `mynamespace/myimage:latest` 的要求：
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

在儲存器雲端服務中，從映像檔名稱啟動新的儲存器。如需相關資訊，請參閱 Docker 說明中的 [run](https://docs.docker.com/reference/commandline/run/){: new_window} 指令。



```
bluemix ic run [-p PORT|--publish PORT][-P] [-m MEMORY|--memory MEMORY][-e ENV|--env ENV] [-v VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS][-it] IMAGE [CMD [CMD ...]]
```
**附註：** 請確定已安裝 Cloud Foundry 指令工具，而且您具有 Cloud Foundry 記號。使用 'bluemix login' 及 'bluemix ic init' 的成功登入，會產生必要記號及憑證。 


**必要條件**：端點、登入、目標、Docker

**指令選項**：

-p *PORT*|--publish *PORT*（選用）：公開 HTTP 資料流量的埠。包括 Dockerfile 中針對您要使用之映像檔所指定的任何埠。您可以利用多個 `-p` 選項來包含多個埠。如果公用 IP 位址可供使用，則公開一個埠會自動將公用 IP 位址連結至儲存器。

如果空間中具有您要連結至儲存器的現有 IP 位址，您可以指定 IP 位址，而不用稍後再連結它。必須以下列格式指定 IP 位址：*&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt;*

如需要求空間之 IP 位址的相關資訊，請參閱 [bluemix ic ip-request](#ip_request) 指令。

在您指定埠時，即將應用程式設為可供「{{site.data.keyword.Bluemix_notm}} 負載平衡器」或相同 {{site.data.keyword.Bluemix_notm}} 空間中嘗試連接主機的儲存器使用。如果在 Dockerfile 中針對您要使用的映像檔指定了埠，請包含該埠。

**提示：**

- 對於 IBM 認證的 Liberty Server 映像檔或此映像檔的已修改版本，請輸入埠 9080。
- 對於 IBM 認證的 Node.js 映像檔或此映像檔的已修改版本，請輸入埠 8000。

-P（選用）：自動公開映像檔的 Dockerfile 中針對 HTTP 資料流量所指定的埠。

-m *MEMORY*|--memory *MEMORY*（選用）：指派給群組的記憶體限制 (MB)。從 CLI 建立儲存器群組時，每一個儲存器實例的預設值都是 '64' MB。從 {{site.data.keyword.Bluemix_notm}}「儀表板」建立儲存器群組時，每一個實例的預設值都是 `256` MB。接受值是 `64`、`256`、`512`、`1024` 及 `2048`。指派記憶體限制之後，即無法變更其值。

-e *ENV*|--env *ENV*（選用）：設定環境變數，其中 **ENV** 是 `key=value` 配對。個別列出多個索引鍵。如果您併入引號，請用它們括住環境變數名稱及值。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。下表顯示一些您可以指定的常用環境變數：

|      環境變數                          |   說明                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 將服務連結至儲存器。使用 'CCS_BIND_APP' 環境變數，以將應用程式連結至儲存器。應用程式會連結至目標服務，並作為橋接器，以容許 {{site.data.keyword.Bluemix_notm}} 將您橋接器應用程式的 `VCAP_SERVICES` 資訊帶入執行中儲存器實例。如需建立橋接器應用程式的相關資訊，請參閱[將服務連結至儲存器](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}。 |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | 建立儲存器時，在其中新增 SSH 金鑰。從 {{site.data.keyword.Bluemix_notm}} 儀表板或從 CLI 建立儲存器時，可以使用環境變數來新增 SSH 金鑰。如需 SSH 金鑰的相關資訊，請參閱[登入儲存器](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 新增要在儲存器中監視的日誌檔。包括含有日誌檔路徑的 `LOG_LOCATIONS` 環境變數。 |
*表 2. 常用環境變數*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  （選用）：以 `VolumeId:ContainerPath[:ro]` 格式指定詳細資料，將磁區連接至儲存器。

- *VOLUME*：磁區 ID 或名稱。
- *CONTAINER_PATH*：儲存器中磁區的絕對路徑。
- ro：選用。指定 'ro' 會使磁區變成唯讀，而不是預設的讀寫。

-n *NAME*|--name *NAME*（必要）：指派儲存器的名稱。

*提示：*儲存器名稱必須以字母開頭。名稱可以包括大寫字母、小寫字母、數字、句點 `.`、底線 `_` 或連字號 `-`。

--link *NAME*:*ALIAS*（選用）：想要某個儲存器與另一個執行中儲存器進行通訊時，即可使用主機名稱的別名予以定址。

-it（選用）：以互動模式執行儲存器。建立儲存器之後，請持續顯示標準輸入。鍵入 `exit` 以結束。

*IMAGE*（必要）：要併入儲存器的影像。您可以在映像檔之後列出指令，但不能在映像檔之後放置任何選項。請在指定映像檔之前併入所有選項。

如果您使用組織專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中的映像檔，請以下列格式指定映像檔：*registry.ng.bluemix.net/NAMESPACE/IMAGE*。

如果您使用 IBM Containers 所提供的映像檔，請以下列格式指定映像檔：*registry.ng.bluemix.net/IMAGE*。

*CMD*（選用）：傳遞給儲存器執行的指令及引數。這個指令必須是長時間執行的指令。請不要使用不會執行很久的短期指令（例如 `/bin/date`），因為短期指令可能會導致儲存器損毀。



**範例**：

在以 `registry.ng.bluemix.net/ibmnode` 映像檔為建置基礎的 `my_container` 儲存器上，執行 `sh -c "while true; do date; sleep 20; done"` 長時間執行指令。
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


使用 `my_namespace/nginx` 映像檔，來建立並啟動具有 `1024` MB 記憶體限制的儲存器 `proxy`，其中 `my_namespace` 是與已登入使用者相關聯的名稱空間。
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

使用 `my_namespace/blog` 映像檔來建立並啟動儲存器，並將認證傳遞為環境變數。`my_namespace` 是與已登入使用者相關聯的名稱空間。
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

使用 `my_namespace/blog` 映像檔，以在儲存器中新增磁區，其中 `my_namespace` 是與已登入使用者相關聯的名稱空間。
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

建立用來存取儲存器群組之網際網路資料流量的路徑。您可以使用此指令，建立新路徑或更新現有路徑。

```
bluemix ic route-map [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**必要條件**：端點、登入、目標

**指令選項**：

-n *HOST*|--hostname *HOST*（選用）：路徑的主機名稱。主機名稱是完整公用路徑 URL 的第一個部分（例如 URL `mycontainerhost.mybluemix.net` 中的 `mycontainerhost`）。

-d *DOMAIN*|--domain *DOMAIN*（選用）：路徑的網域名稱，即完整公用路徑 URL 的第二個部分。在大部分情況下，網域為 'mybluemix.net'。您也可以使用此參數來指定專用網域。

*CONTAINER_GROUP*（必要）：儲存器群組 ID 或名稱。

**範例**：

下列範例顯示對映稱為 'GROUP1' 之群組的路徑的要求，其中 'my_host' 是主機名稱，而 'organization.com' 是網域。
```
bluemix ic route-map -n my_host -d organization.com GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

建立用來存取儲存器群組之網際網路資料流量的路徑。您可以使用此指令，建立新路徑或更新現有路徑。

```
bluemix ic route-unmap [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**必要條件**：端點、登入、目標

**指令選項**：

-n *HOST*|--hostname *HOST*（選用）：路徑的主機名稱。

-d *DOMAIN*|--domain *DOMAIN*（選用）：路徑的網域名稱。

*CONTAINER_GROUP*（必要）：儲存器群組 ID 或名稱。

**範例**：

下列範例顯示取消對映稱為 'GROUP1' 之群組的路徑的要求，其中 'my_host' 是主機名稱，而 'organization.com' 是網域。
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic start
{: #ic_start}
啟動已停止的儲存器。如需相關資訊，請參閱 Docker 說明中的 [start](https://docs.docker.com/reference/commandline/start/){: new_window} 指令。若要停止儲存器，請參閱 [bluemix ic stop](#ic_stop) 指令。

```
bluemix ic start CONTAINER
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

*CONTAINER*（必要）：儲存器名稱或 ID。

**回應**：

- 已順利啟動儲存器。

- 儲存器雲端服務的指令失敗

 `{message}`
  
 其中 `{message}` 是相關的錯誤。
 
- 指令失敗 - 無法連接至儲存器雲端服務

**範例**：

下列範例顯示啟動名為 `proxy` 之儲存器的要求。
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
停止執行中的儲存器。如需相關資訊，請參閱 Docker 說明中的 [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} 指令。若要啟動儲存器，請參閱 [bluemix ic start](#ic_start) 指令。

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

*CONTAINER*（必要）：儲存器名稱或 ID。

-t *SECS*|--time *SECS*（選用）：結束 (kill) 儲存器之前所要等待的秒數。

**回應**：

- 已順利停止儲存器。

- 儲存器雲端服務的指令失敗

 `{message}`
  
 其中 `{message}` 是相關的錯誤。
 
- 指令失敗 - 無法連接至儲存器雲端服務

**範例**：

下列範例顯示停止名為 `proxy` 之儲存器的要求。
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

對於一個以上的儲存器，檢視即時使用情形統計資料。使用 `CTRL+C` 以結束。如需相關資訊，請參閱 Docker 說明中的 [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} 指令。

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

*CONTAINER*（必要）：儲存器名稱或 ID。

--no-stream（選用）：僅顯示最新結果，不包括它之前的任何資訊。

**範例**：

下列範例顯示最新儲存器統計資料的要求：
```
bluemix ic stats --no-stream my_container
```


## bluemix ic top
{: #bluemix_ic_top}

顯示正在儲存器中執行的處理程序。如需相關資訊，請參閱 Docker 說明中的 [top](https://docs.docker.com/reference/commandline/top/){: new_window} 指令。

```
bluemix ic top CONTAINER [CONTAINER]
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

*CONTAINER*（必要）：儲存器名稱或 ID。

**範例**：

下列範例顯示要在稱為 `my_container` 之儲存器中顯示處理程序的要求。
```
bluemix ic top my_container
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

列出磁區。

```
bluemix ic volumes
```

**必要條件**：端點、登入、目標


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

檢查磁區。

```
bluemix ic volume-inspect VOLUME_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*VOLUME_NAME*（必要）：磁區名稱。

**範例**：

下列範例是檢查磁區的要求，其中 `volume_name` 是磁區的名稱。
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

建立磁區。

```
bluemix ic volume-create VOLUME_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*VOLUME_NAME*（必要）：磁區名稱。名稱可以包含小寫字母、數字、底線 `_` 及連字號 `-`。

**範例**：

下列範例顯示建立磁區的要求。
```
bluemix ic volume-create volume_name 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

移除磁區。

```
bluemix ic volume-remove VOLUME_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*VOLUME_NAME*（必要）：磁區名稱。

**範例**：

下列範例顯示移除磁區的要求，其中 `volume_name` 是磁區的名稱。
```
bluemix ic volume-remove volume_name
```

## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

列出檔案系統。

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

建立新的檔案系統。

```
bluemix ic volume-fs-create FILE_SYSTEM_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*FILE_SYSTEM_NAME*（必要）：檔案系統名稱。名稱可以包含小寫字母、數字、底線 `_` 及連字號 `-`。

**範例**：

下列範例顯示建立檔案系統的要求。
```
bluemix ic volume-fs-create my_file_system 
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

移除檔案系統。

```
bluemix ic volume-fs-remove FILE_SYSTEM_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*FILE_SYSTEM_NAME*（必要）：檔案系統名稱。

**範例**：

下列範例顯示移除檔案系統的要求，其中 `my_file_system` 是檔案系統的名稱。
```
bluemix ic volume-fs-remove my_file_system
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

檢查檔案系統。

```
bluemix ic volume-fs-inspect FILE_SYSTEM_NAME
```

**必要條件**：端點、登入、目標

**指令選項**：

*FILE_SYSTEM_NAME*（必要）：檔案系統名稱。

**範例**：

下列範例是檢查檔案系統的要求，其中 `my_file_system` 是磁區的名稱。
```
bluemix ic volume-fs-inspect my_file_system
```
## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

列出所有檔案系統特性。

```
bluemix ic volume-fs-flavors
```

**必要條件**：端點、登入、目標

## bluemix ic wait
{: #bluemix_ic_wait}

結束儲存器，並顯示結束碼作為確認。如需相關資訊，請參閱 Docker 說明中的 [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} 指令。

```
bluemix ic wait CONTAINER [CONTAINER]
```

**必要條件**：端點、登入、目標、Docker

**指令選項**：

*CONTAINER*（必要）：儲存器名稱或 ID。

**範例**：

下列範例顯示結束稱為 `my_container` 之儲存器的要求：
```
bluemix ic wait my_container
```


## bluemix ic version
{: #bluemix_ic_version}

顯示 Docker 的版本。 

```
bluemix ic version
```

**必要條件**：Docker

若要查看 IBM Containers 的版本，請執行 `bluemix ic info`。如需相關資訊，請參閱 Docker 說明中的 [version](https://docs.docker.com/reference/commandline/version/){: new_window} 指令。
