{:shortdesc: .shortdesc}

# bx 指令（用於與 {{site.data.keyword.Bluemix_notm}} 互動）
{: #bluemix_cli}

*前次更新：*2016 年 1 月 5 日

{{site.data.keyword.Bluemix}} 指令行介面 (CLI) 提供一組依名稱空間分組的指令，讓使用者與 {{site.data.keyword.Bluemix_notm}} 互動。部分 {{site.data.keyword.Bluemix_notm}} CLI 指令（稱為 bx 指令）是現有 cf 指令的封套，其他則是 {{site.data.keyword.Bluemix_notm}} 獨有的。下列資訊列出 {{site.data.keyword.Bluemix_notm}} CLI 支援的所有指令，並包括其名稱、選項、使用情形、必要條件、說明及範例。
{:shortdesc}
 
**附註：***必要條件*列出使用指令之前需要哪些動作。沒有必要動作的指令會列示為**無**。否則，必要條件可能包括下列一個以上的動作：
<dl>
<dt>端點</dt>
<dd>必須透過 <code>bluemix api</code> 設定 API 端點後，才能設定使用此指令。</dd>
<dt>Login</dt>
<dd>需要使用 <code>bluemix login</code> 指令進行登入後，才能使用此指令。</dd>
<dt>目標</dt>
<dd>必須使用 <code>bluemix target</code> 指令來設定組織及空間後，才能使用此指令。</dd>
</dl>

## bluemix help
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
設定或檢視 {{site.data.keyword.Bluemix_notm}} API 端點。此指令會覆蓋 `cf api` 指令。

```
bluemix api [API_ENDPOINT][--unset]
```

**必要條件**：無

**指令選項**：

*API_ENDPOINT*（選用）：已設定目標的 API 端點，例如 https://api.ng.bluemix.net。如果未同時指定 *API_ENDPOINT* 及 `--unset` 選項，則會顯示現行 API 端點。

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

將現行組織設為 `MyOrg`，並將空間設為 `MySpace`：

```
bluemix target -o MyOrg -s MySpace
```

檢視現行組織及空間：

```
bluemix target
```


## bluemix info
檢視基本 {{site.data.keyword.Bluemix_notm}} 資訊，包括現行地區、雲端控制器版本以及部分有用端點（例如用於登入及交換存取記號的端點）。

```
bluemix info
```

**必要條件**：端點





## bluemix regions
檢視 {{site.data.keyword.Bluemix_notm}} 上所有地區的資訊。

```
bluemix regions
```

**必要條件**：端點


## bluemix region-set
切換至指定的地區。此指令會自動將目標重設為新地區中相同的組織及空間（可能的話）。否則，指令會提示使用者選取新的組織及空間（如果使用者已登入的話）。API 端點會相應地變更。

```
bluemix region-set REGION_NAME
```

**必要條件**：端點

**指令選項**：

*REGION_NAME*（必要）：要切換至的地區名稱。您可以使用 `bluemix regions` 指令來查看所有地區名稱。

**範例**：

將現行地區設為 `eu-gb`：

```
bluemix region-set eu-gb
```



## bluemix config
將預設值寫入配置檔。

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**必要條件**：無

**指令選項**：

--http-timeout *TIMEOUT_IN_SECONDS*：HTTP 要求的逾時值。預設值是 60 秒。

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
對 {{site.data.keyword.Bluemix_notm}} 執行原始 HTTP 要求。依預設，*Content-Type* 會設為 *application/json*。此指令會對 {{site.data.keyword.Bluemix_notm}} 主控台伺服器（例如，https://console.ng.bluemix.net）傳送要求，而不是對 cf API 端點（例如，https://api.ng.bluemix.net）傳送要求。

```
bluemix curl PATH [OPTIONS...]
```

**必要條件**：端點、登入

**指令選項**：

*PATH*（必要）：資源的 URL 路徑。例如，/rest/v2/apps。

*OPTIONS*（選用）：`bluemix curl` 指令所支援的選項與 `cf curl` 指令的選項相同。

**範例**：

擷取所有樣板範本的資訊：

```
bluemix curl /rest/templates
```


## bluemix iam orgs
此指令的功能和選項與 `cf orgs` 指令的相同。不同的是，該指令還會顯示組織所在的地區。


## bluemix iam org
此指令的功能和選項與 `cf org` 指令的相同。不同的是，該指令會顯示組織所在的地區。


## bluemix iam org-create
此指令的函數及選項與 `cf create-org` 指令相同。





## bluemix iam org-replicate
將組織從現行地區抄寫到另一個地區。

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**必要條件**：端點、登入

**指令選項**：

*ORG_NAME*（必要）：要抄寫的現有組織的名稱。

*REGION_NAME*（必要）：管理所抄寫組織的地區的名稱。

**範例**：

將組織 `OE_Runtimes_Scaling` 抄寫到地區 `eu-gb`：

```
bluemix iam org-replicate OE_Runtimes_Scaling eu-gb
```














## bluemix iam org-rename
此指令的函數及選項與 `cf rename-org` 指令相同。


## bluemix iam org-delete
此指令的函數及選項與 `cf delete-org` 指令相同。


## bluemix iam spaces
此指令的函數及選項與 `cf spaces` 指令相同。


## bluemix iam space
此指令的函數及選項與 `cf space` 指令相同。


## bluemix iam space-create
此指令的函數及選項與 `cf create-space` 指令相同。


## bluemix iam space-rename
此指令的函數及選項與 `cf rename-space` 指令相同。


## bluemix iam space-delete
此指令的函數及選項與 `cf delete-space` 指令相同。


## bluemix iam user-create
此指令的函數及選項與 `cf create-user` 指令相同。


## bluemix iam user-delete
此指令的函數及選項與 `cf delete-user` 指令相同。


## bluemix iam org-users
此指令的函數及選項與 `cf org-users` 指令相同。


## bluemix iam org-role-set
此指令的函數及選項與 `cf set-org-role` 指令相同。


## bluemix iam org-role-unset
此指令的函數及選項與 `cf unset-org-role` 指令相同。


## bluemix iam space-users
此指令的函數及選項與 `cf space-users` 指令相同。


## bluemix iam space-role-set
此指令的函數及選項與 `cf set-space-role` 指令相同。


## bluemix iam space-role-unset
此指令的函數及選項與 `cf unset-space-role` 指令相同。


## bluemix catalog templates
檢視 Bluemix 上的樣板範本。

```
bluemix catalog templates [-d]
```

**必要條件**：端點、登入

**指令選項**：

-d（選用）：如果指定了 `-d` 選項，也會顯示每一個範本的說明。否則，只會顯示每一個範本的 ID 及名稱。


## bluemix catalog template-run
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




## bluemix catalog template-register

在 {{site.data.keyword.Bluemix_notm}} 上登錄新的樣板範本。

```
bluemix catalog template-register TEMPLATE_ID TEMPLATE_URL
```

**必要條件**：端點、登入

**指令選項**：

*TEMPLATE_ID*（必要）：新登錄的範本的 ID。

*TEMPLATE_URL*（必要）：管理新範本 meta 資料的 URL。

**範例**：

建立名為 `javaHelloWorld` 的範本：

```
bluemix catalog template-register javaHelloWorld http://javaHelloWorld.ng.bluemix.net/info
```

## bluemix catalog template-deregister

取消登錄現有的樣板範本。

```
bluemix catalog template-deregister TEMPLATE_ID [-f]
```

**必要條件**：端點、登入

**指令選項**：

*TEMPLATE_ID*（必要）：使用 `bluemix catalog templates` 可檢視所有範本 ID。

-f（選用）：強制取消登錄，而不進行確認。

**範例**：

取消登錄範本 `javaHelloWorld`，而不進行確認：

```
bluemix catalog template-deregister javaHelloWorld -f
```


## bluemix catalog template-registry
檢視 {{site.data.keyword.Bluemix_notm}} 範本登錄。

```
bluemix catalog template-registry
```

**必要條件**：端點









## bluemix catalog service-broker

檢視指定的服務分配管理系統資訊。

```
bluemix catalog service-broker SERVICE_BROKER_NAME
```

**必要條件**：端點、登入

**指令選項**：

*SERVICE_BROKER_NAME*（必要）：要造訪的服務分配管理系統的名稱。


## bluemix catalog service-broker-create
{: #bluemix_catalog_service_broker_create}
建立服務分配管理系統。

```
bluemix catalog service-broker-create SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE [--no-billing]
```

**必要條件**：端點、登入

**指令選項**：

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE*（必要）：用於說明要建立的新服務分配管理系統的 JSON。您可以使用 JSON 檔名，也可以直接使用 JSON 文字。

--no-billing（選用）：如果指定了此選項，則會對服務分配管理系統停用計費。 

**範例**：

使用 JSON 檔案建立服務分配管理系統：

```
bluemix catalog service-broker-create ./broker.json
```

使用 JSON 文字建立新的服務分配管理系統，而且不計費：

```
bluemix catalog service-broker-create '{"name":"test_broker", ...}' --no-billing
```

下列範例顯示服務分配管理系統 JSON 和所有必要欄位：

```
{
    "name": "my_broker",  // 服務分配管理系統的名稱
    "broker_url": "http://my_broker.ng.bluemix.net"  // 指向服務分配管理系統 meta 資料的 URL
    "auth_username": "username",
	"auth_password": "password",  // 用於造訪服務分配管理系統 URL 的使用者名稱和密碼。使用者名稱和密碼應透過 HTTP 基本授權傳送。
    "visibilities" : [
{"organization_name": "OE_Runtimes_Scaling"}
    ]
}
```


## bluemix catalog service-broker-update
更新現有的服務分配管理系統。

```
bluemix catalog service-broker-update ORIGINAL_BROKER_NAME SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE
```

**必要條件**：端點、登入

**指令選項**：

*ORIGINAL_BROKER_NAME*（必要）：要更新的服務分配管理系統的名稱。

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE*（必要）：用於說明服務分配管理系統的新 JSON。您可以使用 JSON 檔名，也可以直接使用 JSON 文字。

**範例**：

更新現有服務分配管理系統 `auto-scaling`：

```
bluemix catalog service-broker-update auto-scaling ./auto-scaling.json
```

如需服務分配管理系統 JSON 格式的詳細資料，請參閱 [bluemix catalog service-broker-create](#bluemix_catalog_service_broker_create)。


## bluemix catalog service-broker-delete

刪除指定的服務分配管理系統。

```
bluemix catalog service-broker-delete SERVICE_BROKER_NAME [-f]
```

**必要條件**：端點、登入

**指令選項**：

*SERVICE_BROKER_NAME*（必要）：要刪除的服務分配管理系統的名稱。

-f（選用）：強制刪除，而不進行確認。

**範例**：

刪除服務分配管理系統 `auto-scaling`，而不進行確認：

```
bluemix catalog service-broker-delete auto-scaling -f
```














## bluemix network routes
此指令的函數及選項與 `cf routes` 指令相同。


## bluemix network route-check
此指令的函數及選項與 `cf check-route` 指令相同。


## bluemix network route-map
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
此指令的函數及選項與 `cf create-route` 指令相同。


## bluemix network route-delete
此指令的函數及選項與 `cf delete-route` 指令相同。


## bluemix network orphaned-routes-delete
此指令的函數及選項與 `cf delete-orphaned-routes` 指令相同。


## bluemix network domains
此指令的函數及選項與 `cf domains` 指令相同。


## bluemix network domain-create
此指令的函數及選項與 `cf create-domain` 指令相同。


## bluemix network domain-delete
此指令的函數及選項與 `cf delete-domain` 指令相同。


## bluemix network shared-domain-create
此指令的函數及選項與 `cf create-shared-domain` 指令相同。


## bluemix network shared-domain-delete
此指令的函數及選項與 `cf delete-shared-domain` 指令相同。




## bluemix security cert

列出指定主機的憑證資訊。

```
bluemix security cert HOST_NAME
```

**必要條件**：端點、登入

**指令選項**：

*HOST_NAME*（必要）：管理憑證的伺服器的名稱。

**範例**：

檢視主機 `ibmcxo-eventconnect.com` 上的憑證：

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add

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
從現行組織中的指定網域移除憑證。

```
bluemix security cert-remove DOMAIN [-f]
```

**必要條件**：端點、登入、目標

**指令選項**：

*DOMAIN*（必要）：要從中移除憑證的網域。

-f（選用）：強制刪除，而不進行確認。








## bluemix plugin repos
列出 {{site.data.keyword.Bluemix_notm}} CLI 中登錄的所有外掛程式儲存庫。

```
bluemix plugin repos
```

**必要條件**：無


## bluemix plugin repo-add
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


## bluemix plugin repo-plugin-list
列出所有已新增之儲存庫或特定儲存庫中所有可用的外掛程式。

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**必要條件**：無

**指令選項**：

-r *REPO_NAME*（選用）：只列出指定儲存庫中的外掛程式。

**範例**：

列出所有已新增之儲存庫中的所有外掛程式：

```
bluemix plugin repo-plugin-list
```

列出 `bluemix-repo` 儲存庫中的所有外掛程式：

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
列出 {{site.data.keyword.Bluemix_notm}} CLI 中的所有已安裝外掛程式。

```
bluemix plugin list
```

**必要條件**：無


## bluemix plugin install
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
