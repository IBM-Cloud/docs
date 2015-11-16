{:shortdesc: .shortdesc}

# bluemix 指令
{: #bluemix_cli}

*前次更新：*2015 年 10 月 19 日

Bluemix 指令行介面 (CLI) 提供一組依使用者的名稱空間分組的指令，可與 Bluemix 互動。部分 Bluemix CLI 指令是現有指令的封套，而其他則是 Bluemix 獨有的指令。以下資訊列出 Bluemix CLI 支援的所有指令，並包括其名稱、選項、用法、必要條件、說明，以及範例。
{:shortdesc}
 
**附註：***必要條件*列出使用指令之前需要哪些動作。沒有必要動作的指令會列示為**無**。否則，必要條件可能包括下列一個以上的動作：
<dl>
<dt>**端點**</dt>
<dd>必須透過 `bluemix api` 設定 API 端點後，才能設定使用此指令。</dd>
<dt>**登入**</dt>
<dd>需要使用 `bluemix login` 指令進行登入後，才能使用此指令。</dd>
<dt>**目標**</dt>
<dd>必須使用 `bluemix target` 指令來設定組織及空間後，才能使用此指令。</dd>
</dl>

## bluemix help
顯示 Bluemix CLI 的第一層內建指令及支援的名稱空間的一般說明，或是特定的內建指令或名稱空間的說明。

```
bluemix help [COMMAND|NAMESPACE]
```

**必要條件**：無

**指令選項**：

*COMMAND*|*NAMESPACE*（選用）：顯示說明的指令或名稱空間。如果未指定，則會顯示 Bluemix CLI 的一般說明。

**範例**：

顯示 Bluemix CLI 的一般說明：

```
bluemix help
```

顯示 `catalog` 名稱空間的說明：

```
bluemix help catalog
```

```
bluemix catalog help
```

顯示 `info` 指令的說明：

```
bluemix help info
```

顯示 `catalog` 名稱空間下 `templates` 指令的說明：

```
bluemix catalog help templates
```


## bluemix api
設定或檢視 Bluemix API 端點。此指令會覆蓋 `cf api` 指令。

```
bluemix api [API_ENDPOINT][--unset]
```

**必要條件**：無

**指令選項**：

*API_ENDPOINT*（選用）：已設定目標的 API 端點，例如 https://api.ng.bluemix.net。如果未同時指定 *API_ENDPOINT* 及 `–unset` 選項，則會顯示現行 API 端點。

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
登入使用者。此指令會覆蓋 `cf login` 指令。指令選項與 `cf login` 指令選項相同。

```
bluemix login [OPTIONS...]
```

**必要條件**：端點

**指令選項**：如需 `login` 指令支援之選項的相關資訊，請參閱用於管理應用程式之 cf 指令的 `cf login` 指令用法資訊。


## bluemix logout
登出使用者。此指令會覆蓋 `cf logout` 指令。

```
bluemix logout
```

**必要條件**：無


## bluemix target
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

將現行組織設為 'MyOrg'，並將空間設為 'MySpace'：

```
bluemix target -o MyOrg -s MySpace
```

檢視現行組織及空間：

```
bluemix target
```


## bluemix info
檢視基本 Bluemix 資訊，包括現行區域、雲端控制器版本，以及一些有用的端點，例如用於登入及交換存取記號的端點。

```
bluemix info
```

**必要條件**：端點


## bluemix list
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
將 cf 應用程式或儲存器群組橫向縮減或橫向擴充至指定的實例計數、磁碟限額及記憶體大小。

**附註：**只能指定一個實例數目，用於調整儲存器群組。如果未指定選項，此指令會列出儲存器群組的現行實例計數，也會列出 cf 應用程式的磁碟限額及記憶體大小。

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT] [-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**必要條件**：端點、登入、目標

**指令選項**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必要）：要調整之 cf 應用程式或儲存器群組的名稱。

-i *INSTANCE_COUNT*（選用）：要調整之 cf 應用程式或儲存器群組的新實例數目。此選項是要調整之儲存器群組的唯一有效選項。

-k *DISK_QUOTA*（選用）：cf 應用程式的新磁碟限額。無法用於調整儲存器群組。

-m *MEMORY_SIZE*（選用）：cf 應用程式的新記憶體大小。無法用於調整儲存器群組。

**範例**：

顯示 'my-container-group' 的現行實例數目：

```
bluemix scale my-container-group
```

將 'my-container-group' 調整為 2 個實例：

```
bluemix scale my-container-group -i 2
```

將 'my-java-app' 調整為 3 個實例、8G 磁碟限額，以及 1024M 記憶體大小：

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
對 Bluemix 執行原始 HTTP 要求。依預設，"Content-Type" 會設為 "application/json"。此指令會將要求傳送至 Bluemix 主控台伺服器（例如，https://console.ng.bluemix.net），而非 cf API 端點（例如，https://api.ng.bluemix.net）。

```
bluemix curl PATH [OPTIONS...]
```

**必要條件**：端點、登入

**指令選項**：

*PATH*（必要）：資源的 URL 路徑。例如，/rest/v2/apps。

*OPTIONS*（選用）：`bluemix curl` 指令支援的選項與 `cf curl` 指令支援的選項相同。

**範例**：

擷取所有樣板範本的資訊：

```
bluemix curl /rest/templates
```


## bluemix iam orgs
此指令具有與 `cf orgs` 指令相同的功能及選項。


## bluemix iam org
此指令具有與 `cf org` 指令相同的功能及選項。


## bluemix iam org-create
此指令具有與 `cf create-org` 指令相同的功能及選項。


## bluemix iam org-rename
此指令具有與 `cf rename-org` 指令相同的功能及選項。


## bluemix iam org-delete
此指令具有與 `cf delete-org` 指令相同的功能及選項。


## bluemix iam spaces
此指令具有與 `cf spaces` 指令相同的功能及選項。


## bluemix iam space
此指令具有與 `cf space` 指令相同的功能及選項。


## bluemix iam space-create
此指令具有與 `cf create-space` 指令相同的功能及選項。


## bluemix iam space-rename
此指令具有與 `cf rename-space` 指令相同的功能及選項。


## bluemix iam space-delete
此指令具有與 `cf delete-space` 指令相同的功能及選項。


## bluemix iam user-create
此指令具有與 `cf create-user` 指令相同的功能及選項。


## bluemix iam user-delete
此指令具有與 `cf delete-user` 指令相同的功能及選項。


## bluemix iam org-users
此指令具有與 `cf org-users` 指令相同的功能及選項。


## bluemix iam org-role-set
此指令具有與 `cf set-org-role` 指令相同的功能及選項。


## bluemix iam org-role-unset
此指令具有與 `cf unset-org-role` 指令相同的功能及選項。


## bluemix iam space-users
此指令具有與 `cf space-users` 指令相同的功能及選項。


## bluemix iam space-role-set
此指令具有與 `cf set-space-role` 指令相同的功能及選項。


## bluemix iam space-role-unset
此指令具有與 `cf unset-space-role` 指令相同的功能及選項。


## bluemix catalog templates
檢視 Bluemix 上的樣板範本。

```
bluemix catalog templates [-d]
```

**必要條件**：端點、登入

**指令選項**：

-d（選用）：如果指定了 '-d' 選項，也會顯示每一個範本的說明。否則，只會顯示每一個範本的 ID 及名稱。


## bluemix catalog template-run
以指定的 URL 及說明，建立根據所指定範本的 cf 應用程式。依預設，新的應用程式會自動啟動。

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**必要條件**：端點、登入、目標

**指令選項**：

*TEMPLATE_ID*（必要）：應用程式在建立時將根據的範本。請使用 'bluemix templates' 來查看所有範本的 ID。

*CF_APP_NAME*（必要）：要建立之 cf 應用程式的名稱。

-u *URL*（選用）：應用程式的路徑。如果未指定，Bluemix 會自動根據您的應用程式名稱及預設網域來設定路徑。

-d *DESCRIPTION*（選用）：應用程式的說明。

--no-start（選用）：在建立應用程式之後，請不要將它自動啟動。如果未指定，應用程式會在建立之後自動啟動。

**範例**：

根據 'javaHelloWorld' 範本建立 cf 應用程式 'my-app'：

```
bluemix catalog template-run javaHelloWorld my-app
```

根據 'rubyHelloWorld' 範本建立路徑為 'myrubyapp.ng.bluemix.net' 且說明為 'My first ruby app on Bluemix.' 的應用程式 'my-ruby-app'：

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on Bluemix."
```

根據 'pythonHelloWorld' 範本建立不會自動啟動的應用程式 'my-python-app'：

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
檢視 Bluemix 上所有區域的資訊。

```
bluemix network regions
```

**必要條件**：端點


## bluemix network region-set
切換至指定的區域。此指令會自動將目標重設為新區域中相同的組織及空間（可能的話），或提示使用者選取新的組織及空間（如果使用者已登入的話）。API 端點會相應地變更。

```
bluemix network region-set REGION_NAME
```

**必要條件**：端點

**指令選項**：

*REGION_NAME*（必要）：您要切換至的區域名稱。您可以使用 `bluemix regions` 指令來查看所有區域名稱。

**範例**：

將現行區域設為 'eu-gb'：

```
bluemix network region-set eu-gb
```


## bluemix network routes
此指令具有與 `cf routes` 指令相同的功能及選項。


## bluemix network route-check
此指令具有與 `cf check-route` 指令相同的功能及選項。


## bluemix network route-map
將路徑對映至具有所指定網域及主機名稱的現有 cf 應用程式或儲存器群組。

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**必要條件**：端點、登入、目標

**指令選項**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必要）：要與路徑對映之 cf 應用程式或儲存器群組的名稱。

*DOMAIN*（必要）：路徑的網域。例如，mybluemix.net 或 ng.bluemix.net。 

-n *HOST_NAME*（選用）：路徑的主機名稱。如果未提供，則依預設會將主機名稱設為應用程式名稱或儲存器群組名稱。

**範例**：

以指定的網域將路徑對映至 'my-app'：

```
bluemix network route-map my-app mybluemix.net
```

以指定的網域及主機名稱對映將路徑對映至 'my-container-group'：

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
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

從 'my-app' 中取消對映 'my-app.mybluemix.net'：

```
bluemix network route-unmap my-app mybluemix.net
```

從 'my-container-group' 中取消對映 'abc.ng.bluexmix.net'：

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
此指令具有與 `cf create-route` 指令相同的功能及選項。


## bluemix network route-delete
此指令具有與 `cf delete-route` 指令相同的功能及選項。


## bluemix network orphaned-routes-delete
此指令具有與 `cf delete-orphaned-routes` 指令相同的功能及選項。


## bluemix network domains
此指令具有與 `cf domains` 指令相同的功能及選項。


## bluemix network domain-create
此指令具有與 `cf create-domain` 指令相同的功能及選項。


## bluemix network domain-delete
此指令具有與 `cf delete-domain` 指令相同的功能及選項。


## bluemix network shared-domain-create
此指令具有與 `cf create-shared-domain` 指令相同的功能及選項。


## bluemix network shared-domain-delete
此指令具有與 `cf delete-shared-domain` 指令相同的功能及選項。


## bluemix plugin repos
列出所有登錄在 Bluemix CLI 的外掛程式儲存庫。

```
bluemix plugin repos
```

**必要條件**：無


## bluemix plugin repo-add
將外掛程式儲存庫新增至 Bluemix CLI。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**必要條件**：無

**指令選項**：

*REPO_NAME*（必要）：要新增的儲存庫名稱。您可以為每一個儲存庫定義專屬名稱。

*REPO_URL*（必要）：要新增之儲存庫的 URL。儲存庫 URL 必須包含通訊協定（例如，http://plugins.ng.bluemix.net 而非 plugins.ng.bluemix.net）。http://plugins.ng.bluemix.net 是 Bluemix CLI 的官方外掛程式儲存庫。

**範例**：

將 Bluemix CLI 的官方外掛程式儲存庫新增為 'bluemix-repo'：

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
從 Bluemix CLI 中移除外掛程式儲存庫。

```
bluemix plugin repo-remove REPO_NAME
```

**必要條件**：無

**指令選項**：

*REPO_NAME*（必要）：要移除的儲存庫名稱。

**範例**：

從 Bluemix CLI 中移除 'bluemix-repo' 儲存庫：

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
列出所有已新增之儲存庫或特定儲存庫中所有可用的外掛程式。

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**必要條件**：無

**指令選項**：

-r *REPO_NAME*（選用）：只列出所指定儲存庫中的外掛程式。

**範例**：

列出所有已新增之儲存庫中的所有外掛程式：

```
bluemix plugin repo-plugin-list
```

列出 'bluemix-repo' 儲存庫中的所有外掛程式：

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
列出 Bluemix CLI 中所有已安裝的外掛程式。

```
bluemix plugin list
```

**必要條件**：無


## bluemix plugin install
從指定的路徑或儲存庫將外掛程式安裝至 Bluemix CLI。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME]
```

**必要條件**：無

**指令選項**：

*PLUGIN_PATH*|*PLUGIN_NAME*（必要）：如果未指定 '-r *REPO_NAME*'，則會從指定的本端路徑或遠端 URL 安裝外掛程式。

-r *REPO_NAME*（選用）：外掛程式二進位檔所在的儲存庫名稱。

**範例**：

從本端檔案安裝外掛程式：

```
bluemix plugin install /downloads/new_plugin
```

從遠端 URL 安裝外掛程式：

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

從 'bluemix-repo' 儲存庫安裝 'IBM-Containers' 外掛程式：

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
從 Bluemix CLI 解除安裝指定的外掛程式。

```
bluemix plugin uninstall PLUGIN_NAME
```

**必要條件**：無

**指令選項**：

*PLUGIN_NAME*（必要）：要解除安裝的外掛程式名稱。

**範例**：

解除安裝先前已安裝的 'IBM-Containers' 外掛程式：

```
bluemix plugin uninstall IBM-Containers
```
