---



copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"


---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}


# Cloud Foundry (cf) 指令
{: #cf}

Cloud Foundry (cf) 指令行介面 (CLI) 提供一組管理應用程式的指令。下列資訊列出最常用來管理應用程式的 cf 指令，並且包括其名稱、選項、用法、必要條件、說明及範例。若要列出所有 cf 指令及關聯的說明資訊，請使用 `cf help`。使用 `cf command_name -h` 可檢視特定指令的詳細說明資訊。
{: shortdesc}

**附註**：如果您的網路在執行 cf 指令的主機與 Cloud Foundry API 端點之間包含 HTTP Proxy 伺服器，則必須設定 `HTTP_PROXY` 環境變數來指定 Proxy 伺服器的主機名稱或 IP 位址。如需詳細資料，請參閱 [Using the cf CLI with an HTTP Proxy Server ![外部鏈結圖示](../../../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html){: new_window}。


## Cloud Foundry CLI 指令索引
{: #CLIname_commands_index}

使用下表中的索引來參照常用的 Cloud Foundry 指令：

<table summary="按字母順序排序的一般 Cloud Foundry 指令，其鏈結提供指令的相關資訊">
 <caption>表 1. 一般 Cloud Foundry 指令</caption>
 <thead>
 <th colspan="6">一般 Cloud Foundry 指令</th>
 </thead>
 <tbody>
 <tr>
 <td>[api](/docs/cli/reference/cfcommands/index.html#cf_api)</td>
 <td>[help](/docs/cli/reference/cfcommands/index.html#cf_help)</td>
 <td>[login](/docs/cli/reference/cfcommands/index.html#cf_login)</td>
 <td>[stacks](/docs/cli/reference/cfcommands/index.html#cf_stacks)</td>
 <td>[target](/docs/cli/reference/cfcommands/index.html#cf_target)</td>
 <td>[-v ](/docs/cli/reference/cfcommands/index.html#cf_v)</td>
 </tr>
   </tbody>
 </table>


<table summary="按字母順序排序的指令，用於管理應用程式、空間及服務。每一個指令都有鏈結可提供指令的相關資訊。">
 <caption>表 2. 用來管理應用程式、空間及服務的指令</caption>
 <thead>
 <th colspan="5">用來管理應用程式、空間及服務的指令</th>
 </thead>
 <tbody>
 <tr>
 <td>[apps](/docs/cli/reference/cfcommands/index.html#cf_apps)</td>
 <td>[bind-service](/docs/cli/reference/cfcommands/index.html#cf_bind-service)</td>
 <td>[create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service)</td>
 <td>[create-space](/docs/cli/reference/cfcommands/index.html#cf_create-space)</td>
 <td>[delete](/docs/cli/reference/cfcommands/index.html#cf_delete)</td>
  </tr>
 <tr>
 <td>[delete-space](/docs/cli/reference/cfcommands/index.html#cf_delete-space)</td>
 <td>[events](/docs/cli/reference/cfcommands/index.html#cf_events)</td>
 <td>[logs](/docs/cli/reference/cfcommands/index.html#cf_logs)</td>
 <td>[marketplace](/docs/cli/reference/cfcommands/index.html#cf_marketplace)</td>
 <td>[push](/docs/cli/reference/cfcommands/index.html#cf_push)</td>
  </tr>
 <tr>
 <td>[scale](/docs/cli/reference/cfcommands/index.html#cf_scale)</td>
 <td>[services](/docs/cli/reference/cfcommands/index.html#cf_services)
 <td>[set-env](/docs/cli/reference/cfcommands/index.html#cf_set-env)</td>
 <td>[ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh)</td>
 <td>[stop](/docs/cli/reference/cfcommands/index.html#cf_stop)</td>
 </tr>
 </tbody>
 </table>

## cf api
{: #cf_api}

您可以使用此指令來顯示或指定 {{site.data.keyword.Bluemix_notm}} API 端點的 URL。

```
cf api [BluemixServerURL] [--skip-ssl-validation] [--unset]
```

<strong>必要條件</strong>：無。

<strong>指令選項</strong>：

   <dl>
   <dt>BluemixServerURL（選用）</dt>
   <dd>Bluemix API 端點的 URL，您在連接至 {{site.data.keyword.Bluemix_notm}} 時必須予以指定。這個 URL 通常是 `https://api.{DomainName}`。
   如果您要顯示目前所使用 API 端點的 URL，則不需要針對 cf api 指令指定此參數。</dd>
   <dt>* --skip-ssl-validation</dt>
   <dd>停用 SSL 驗證處理程序。使用此參數可能導致安全問題。</dd>
   <dt>* --unset</dt>
   <dd>移除所有 API 端點的連線資訊。</dd>
    </dl>

<strong>範例</strong>：

檢視現行 API 端點
```
cf api
```
{: codeblock}

移除與 api.ng.bluemix.net 之所有 API 端點的連線
```
cf api api.ng.bluemix.network --unset
```
{: codeblock}

停用 api.ng.bluemix.network 的 SSL 驗證處理程序
```
cf api api.ng.bluemix.network --skip-ssl-validation
```
{: codeblock}


## cf apps
{: #cf_apps}

列出您已部署在現行空間的所有應用程式。也會顯示每個應用程式的狀態。

假設您對某個應用程式有一個實例，則如果您的應用程式已啟動，則會在 cf apps 指令回應的實例直欄中看到 1/1，如果您的應用程式已關閉，則會看到 0/1。如果您看到指出應用程式實例狀態不明的 ?/1，則可以將應用程式 URL 複製到瀏覽器，以檢查應用程式是否有回應，也可以透過 `cf logs appname` 指令來讀取日誌尾端的內容，以查看應用程式是否正在產生日誌內容。

```
cf apps
```

<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`


## cf bind-service
{: #cf_bind-service}

將現有服務實例連結至您的應用程式。


```
cf bind-service appname service_instance
```

<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：

   <dl>
   <dt>appname（必要）</dt>
   <dd>應用程式的名稱。</dd>
   <dt>service_instance（必要）</dt>
   <dd>現有服務實例的名稱。</dd>
    </dl>

<strong>範例</strong>：

將 `my_dataworks` 服務實例連結至 `my_app` 應用程式。
```
cf bind-service my_app my_dataworks
```
{: codeblock}


## cf create-service
{: #cf_create-service}

建立服務實例

```
cf create-service service_name service_plan service_instance
```

<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：

   <dl>
   <dt>service_name（必要）</dt>
   <dd>服務的名稱。</dd>
   <dt>service_plan（必要）</dt>
   <dd>服務方案的名稱。</dd>
   <dt>service_instance（必要）</dt>
   <dd>您要用於所建立之新服務實例的名稱。</dd>
    </dl>

<strong>範例</strong>：

建立使用 `free` 方案的 {{site.data.keyword.dataworks_short}} 服務實例。
```
cf create-service DataWorks free my_dataworks
```
{: codeblock}


## cf create-space
{: #cf_create-space}

建立空間。


```
cf create-space space_name [-o] [-q]
```

<strong>必要條件</strong>：`cf api`、`cf login`

<strong>指令選項</strong>：

   <dl>
   <dt>space_name（必要）</dt>
   <dd>空間的名稱。</dd>
   <dt>*-o*（選用）</dt>
   <dd>您要在其內建立空間的組織名稱。</dd>
   <dt>*-q*（選用）</dt>
   <dd>要指派給新建立空間的配額。如果未指定，則會自動指派一個預設配額。</dd>
    </dl>

<strong>範例</strong>：

建立 new_space 空間
```
cf create-space new_space
```
{: codeblock}


## cf delete
{: #cf_delete}

刪除現有應用程式。


```
cf delete appname [-f] [-r]
```

<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：

   <dl>
   <dt>appname（必要）</dt>
   <dd>應用程式的名稱。</dd>
   <dt>*-f*（選用）</dt>
   <dd>強制刪除應用程式而不進行任何確認。</dd>
   <dt>*-r*（選用）</dt>
   <dd>刪除與應用程式相關聯的所有網域名稱。</dd>
    </dl>

<strong>範例</strong>：

刪除 `my_app` 應用程式（將需要確認）。
```
cf delete my_app
```
{: codeblock}

刪除 `my_app` 應用程式，不需要進行確認。
```
cf delete my_app -f
```
{: codeblock}

刪除 `my_app` 應用程式以及與 `my_app` 相關聯的所有網域名稱。
```
cf delete my_app -r
```
{: codeblock}

刪除 `my_app` 應用程式以及與 `my_app` 相關聯的所有網域名稱，不需要進行確認。
```
cf delete my_app -f -r
```
{: codeblock}


## cf delete-space
{: #cf_delete-space}

刪除空間。


```
cf delete-space space_name [-f]
```

<strong>必要條件</strong>：`cf api`、`cf login`

<strong>指令選項</strong>：

   <dl>
   <dt>space_name（必要）</dt>
   <dd>空間的名稱。</dd>
   <dt>*-f*（選用）</dt>
   <dd>強制刪除空間而不進行任何確認。</dd>
   *附註：*刪除空間是一項無法回復的作業。
</dl>

<strong>範例</strong>：

刪除 `my_app` 應用程式（將需要確認）。
```
cf delete my_app
```
{: codeblock}

刪除 `my_app` 應用程式，不需要進行確認。
```
cf delete my_app -f
```
{: codeblock}

刪除 `my_app` 應用程式以及與 `my_app` 相關聯的所有網域名稱。
```
cf delete my_app -r
```
{: codeblock}

刪除 `my_app` 應用程式以及與 `my_app` 相關聯的所有網域名稱，不需要進行確認。
```
cf delete my_app -f -r
```
{: codeblock}


## cf events
{: #cf_events}

顯示與應用程式相關的運行環境事件。

```
cf events [appname]
```

<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：

   <dl>
   <dt>appname</dt>
   <dd>應用程式的名稱。</dd>
   </dl>

<strong>範例</strong>：

顯示 `my_app` 應用程式的事件。
```
cf events my_app
```
{: codeblock}


## cf help
{: #cf_help}

顯示所有 cf 指令或特定 cf 指令的說明資訊。

```
cf help [command_name]
```

<strong>必要條件</strong>：無。

<strong>指令選項</strong>：

   <dl>
   <dt>command_name（選用）</dt>
   <dd>指令的名稱。</dd>
    </dl>

<strong>範例</strong>：

顯示所有 cf 指令的說明資訊。
```
cf help
```
{: codeblock}

顯示 events 指令的說明資訊。
```
cf help events
```
{: codeblock}


## cf login
{: #cf_login}

讓您登入 {{site.data.keyword.Bluemix_notm}}。


**附註**：如果您是使用[聯合 ID](/docs/admin/account.html#signup) 登入，則必須使用單一登入 (SSO) 參數來登入。

```
cf login [-a url] [-u user_name] [-p password] [-sso] [-o organization_name] [-s space_name] [--skip-ssl-validation]
```

<strong>必要條件</strong>：無。

<strong>指令選項</strong>：

<dl>
<dt>*-a* https://api.{DomainName}（選用）</dt>
<dd>{{site.data.keyword.Bluemix_notm}} API 端點的 URL。</dd>
<dt>*-u* user_name（選用）</dt>
<dd>您的使用者名稱。</dd>
<dt>*-p* password（選用）</dt>
<dd>您的密碼。</dd>
<dd>*重要事項：*如果您在指令行介面上使用 *-p* 參數提供密碼，密碼可能會記錄在指令行歷程中。為了安全因素，請避免使用 -p 參數提供密碼。請改為在指令行介面提示您時再輸入密碼。</dd>
<dt>*-sso*</dt>
<dd>以聯合 ID 登入時，必須使用單一登入選項 (SSO)。以 IBM ID 登入時，則不需要這麼做。如果您嘗試使用聯合 ID 來登入，而沒有指定 SSO 參數，系統會提示您將其包含在內。使用 SSO 參數時，系統會提示您在登入時輸入一次性密碼。</dd>
<dt>*-o* organization_name</dt>
<dd>您要登入的組織名稱。</dd>
<dt>*-s* space_name</dt>
<dd>您要登入的空間名稱。</dd>
<dt>*--skip-ssl-validation*（選用）</dt>
<dd>停用 SSL 驗證處理程序。使用此參數可能導致安全問題。</dd>
</dl>

*附註：*如果您在此指令的 *-p* 參數中提供密碼，您的密碼可能會記錄在 Shell 指令歷程檔案，且可能被本端作業系統的其他使用者看到。

<strong>範例</strong>：

登入 {{site.data.keyword.Bluemix_notm}}。
```
cf login
```
{: codeblock}

登入 {{site.data.keyword.Bluemix_notm}}，並使用已定義端點 `https://api.ng.bluemix.net`。
```
cf login -a https://api.ng.bluemix.net
```
{: codeblock}

登入 {{site.data.keyword.Bluemix_notm}}，並使用已定義端點 `https://api.ng.bluemix.net`、使用者名稱 `user_name` 且不指定密碼（這是基於安全原因）。
```
cf login -a https://api.ng.bluemix.net -u user_name
```
{: codeblock}

登入 {{site.data.keyword.Bluemix_notm}}，並使用已定義端點 `https://api.ng.bluemix.net`、使用者名稱 `user_name`、不指定密碼（這是基於安全原因）、組織名稱 `org_name`，以及空間名稱 `space_name`。
```
cf login -a https://api.ng.bluemix.net -u user_name -o org_name -s space_name
```
{: codeblock}


## cf logs
{: #cf_logs}

顯示應用程式的 STDOUT 及 STDERR 日誌串流。


```
cf logs appname [--recent]
```
<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：

<dl>
<dt>appname</dt>
<dd>應用程式的名稱。</dd>
<dt>*--recent*（選用）</dt>
<dd>擷取最近的日誌。</dd>
</dl>

<strong>範例</strong>：

顯示 `my_app` 應用程式的日誌串流。
```
cf logs my_app
```
{: codeblock}

顯示 `my_app` 應用程式的最近日誌串流。
```
cf logs my_app --recent
```
{: codeblock}


## cf marketplace
{: #cf_marketplace}

列出 Marketplace 中可用的所有服務。這個指令所列出的服務也會顯示在 {{site.data.keyword.Bluemix_notm}}「型錄」中。


```
cf marketplace
```
<strong>必要條件</strong>：`cf api`

<strong>指令選項</strong>：無。

<strong>範例</strong>：

列出 marketplace 中的所有服務
```
cf marketplace
```
{: codeblock}


## cf push
{: #cf_push}

將新的應用程式部署至 {{site.data.keyword.Bluemix_notm}}，或更新 {{site.data.keyword.Bluemix_notm}} 中的現有應用程式。

```
cf push appname [-b buildpack_name] [-c start_command] [-f manifest_path] [-i instance_number] [-k disk_limit] [-m memory_limit] [-n host_name] [-p app_path] [-s stack_name] [-t timeout_length] [--no-hostname] [--no-manifest] [--no-route] [--no-start] [--random-route]
```

<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：

<dl>
<dt>appname（必要）</dt>
<dd>應用程式的名稱。</dd>
<dt>*-b* buildpack_name（選用）</dt>
<dd>建置套件的名稱。buildpack_name 可以是依名稱（例如 liberty-for-java）、Git URL（例如 https://github.com/cloudfoundry/java-buildpack.git）或含分支或標記之 Git URL（例如，https://github.com/cloudfoundry/java-buildpack.git#v3.3.0 適用於 3.3.0 版標記）的自訂建置套件。</dd>
<dt>*-c* start_command（選用）</dt>
<dd>應用程式的啟動指令。若要使用預設的啟動指令，請針對這個選項指定空值。</dd>
<dt>*-f* manifest_path（選用）</dt>
<dd>資訊清單檔的路徑。預設資訊清單檔是您應用程式根目錄底下的 manifest.yml。</dd>
<dt>*-i* instance_number（選用）</dt>
<dd>實例數。</dd>
<dt>*-k* disk_limit（選用）</dt>
<dd>應用程式的磁碟限制。可能的值為 *256M*、*1024M* 或 *1G*。</dd>
<dt>*-m* memory_limit（選用）</dt>
<dd>應用程式的記憶體限制。可能的值為 *256M*、*1024M* 或 *1G*。</dd>
<dt>*-n* host_name（選用）</dt>
<dd>應用程式的主機名稱，例如 *my-subdomain*。</dd>
<dt>*-p* app_path（選用）</dt>
<dd>應用程式目錄或應用程式保存檔的路徑。</dd>
<dt>*-s* stack_name（選用）</dt>
<dd>要執行應用程式的堆疊。堆疊是預先建置的檔案系統（包括作業系統）。使用 `cf stacks`，以檢視 {{site.data.keyword.Bluemix_notm}} 中的可用堆疊。</dd>
<dt>*-t* timeout（選用）</dt>
<dd>應用程式啟動的時間上限（秒）。其他伺服器端的逾時可能會置換此值。</dd>
<dt>*--no-hostname*（選用）</dt>
<dd>將 {{site.data.keyword.Bluemix_notm}} 系統網域對映到此應用程式。</dd>
<dt>*--no-manifest*（選用）</dt>
<dd>忽略預設資訊清單檔。</dd>
<dt>*--no-route*（選用）</dt>
<dd>不要對映路徑至此應用程式。</dd>
<dt>*--no-start*（選用）</dt>
<dd>部署應用程式之後不要啟動應用程式。</dd>
<dt>*--random-route*（選用）</dt>
<dd>建立應用程式的隨機路徑。</dd>
</dl>

<strong>範例</strong>：

使用預設啟動指令，以啟動 `my_app` 應用程式。
```
cf push `my_app` -c null
```
{: codeblock}

使用執行 Script 檔 `run.sh` 的選項，以啟動 `my_app` 應用程式。
```
cf push `my_app` -c "bash ./<run.sh>"
```
{: codeblock}



## cf scale
{: #cf_scale}

顯示或變更應用程式的實例數目、磁碟空間限制及記憶體限制。


```
cf scale appname [-i instance_number] [-k disk_limit] [-m memory_limit] [-f]
```

<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：

<dl>
<dt>appname（必要）</dt>
<dd>應用程式的名稱。</dd>
<dt>*-i* instance_number（選用）</dt>
<dd>實例數。</dd>
<dt>*-k* disk_limit（選用）</dt>
<dd>應用程式的磁碟限制；可能的值為 `256M`、`1024M` 或 `1G`。</dd>
<dt>*-m* memory_limit（選用）</dt>
<dd>應用程式的記憶體限制；可能的值為 `256M`、`1024M` 或 `1G`。</dd>
<dt>*-f*（選用）</dt>
<dd>強制應用程式重新啟動而不提示。</dd>
</dl>

<strong>範例</strong>：

顯示 `my_app` 應用程式的實例數目、磁碟空間限制及記憶體限制。
```
cf scale my_app
```
{: codeblock}

將 `my_app` 應用程式的實例數目修改為 `1234`、將磁碟空間限制修改為 `1G`，並將記憶體限制修改為 `1G`。
```
cf scale appname -i 1234 -k 1G -m 1G
```
{: codeblock}


## cf services
{: #cf_services}

列出現行空間中可用的所有服務。


```
cf services
```
<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：無。

<strong>範例</strong>：

列出現行空間中的所有服務。
```
cf services
```
{: codeblock}


## cf set-env
{: #cf_set-env}

設定應用程式的環境變數

```
cf set-env appname var_name var_value
```
<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：

<dl>
<dt>appname（必要）</dt>
<dd>應用程式的名稱。</dd>
<dt>var_name（必要）</dt>
<dd>環境變數的名稱。</dd>
<dt>var_value（必要）</dt>
<dd>環境變數的值。</dd>
</dl>

<strong>範例</strong>：

針對 `my_app` 應用程式，設定值為 `123` 的 `variable_a` 環境變數。
```
cf set-env my_app variable_a 123
```
{: codeblock}


## cf ssh
{: #cf_ssh}

安全地存取應用程式容器。`cf ssh` 指令可以用來設定互動式 SSH 階段作業、執行遠端指令、傳送檔案，以及使用特定應用程式容器實例來設定埠轉遞。

```
cf ssh
```
<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

依預設，會啟用 Diego 應用程式的 SSH 存取。您可以使用 `cf ssh-enabled` 指令，驗證是否已啟用 SSH 存取，或是使用 `cf enable-ssh` 指令來啟用已停用的存取。 

<strong>指令選項</strong>：

<dl>
<dt>appname</dt>
<dd>應用程式的名稱。</dd>
<dt>-c</dt>
<dd>指定要執行的遠端指令。</dd>
<dt>-i</dt>
<dd>將特定應用程式實例設為目標。如果未指定，則會使用應用程式的第一個實例（索引為 0 的實例）。</dd>
<dt>-L</dt>
<dd>啟用本端埠轉遞，這會將機器上的輸出埠連結至應用程式 VM 上的輸入埠。</dd>
<dt>-N</dt>
<dd>不要執行遠端指令。</dd>
<dt>-t、-tt 或 -T</dt>
<dd>可讓您在 pseudo-tty 模式下執行 SSH 階段作業，而不是產生終端機行輸出。<dd>
</dl>

<strong>範例</strong>：

啟動與執行 `my_app` 應用程式之容器實例互動的 SSH 階段作業。
```
$ cf ssh my_app
```
{: codeblock}

在 `my_app` 應用程式容器實例上執行單一指令。
```
$ cf ssh my_app -c "ls -l"
```

從 `my_app` 應用程式容器實例傳送單一檔案。
```
$ cf ssh my_app -c "/bin/cat logs/messages.log" > messages.log
```

設定埠轉遞，將本端機器上的 7777 埠轉遞至 `my_app` 應用程式容器實例上的 8888 埠。
```
$ cf ssh -N -T -L 7777:localhost:8888 my_app

```

## cf stacks
{: #cf_stacks}

列出所有堆疊。堆疊是預先建置的檔案系統，包括可以執行應用程式的作業系統。


```
cf stacks
```
<strong>必要條件</strong>：`cf api`、`cf login`

<strong>指令選項</strong>：無。

<strong>範例</strong>：

列出所有堆疊。
```
cf stacks
```
{: codeblock}


## cf stop
{: #cf_stop}

停止應用程式

```
cf stop appname
```
<strong>必要條件</strong>：`cf api`、`cf login`、`cf target`

<strong>指令選項</strong>：

<dl>
<dt>appname（必要）</dt>
<dd>應用程式的名稱。</dd>
</dl>

<strong>範例</strong>：

停止 `my_app` 應用程式。
```
cf stop my_app
```
{: codeblock}


## cf target
{: #cf_target}

設定或檢視已設定為目標的組織或空間

```
cf target [-o org_name] [-s space_name]
```
<strong>必要條件</strong>：`cf api`、`cf login`

<strong>指令選項</strong>：

<dl>
<dt>-o *org_name*（選用）</dt>
<dd>空間所在組織的名稱。</dd>
<dt>-s *space_name*（選用）</dt>
<dd>空間的名稱。</dd>
</dl>

<strong>範例</strong>：

將目標設為 "my_org" 組織及 "my_space" 空間。
```
cf target -o my_org -s my_space
```
{: codeblock}


## cf -v
{: #cf_v}

顯示 cf 指令行介面的版本。


```
cf -v
```
<strong>必要條件</strong>：無。

<strong>指令選項</strong>：無。

<strong>範例</strong>：

顯示 cf 指令行介面的版本。
```
cf -v
```
{: codeblock}



# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

* [下載 Cloud Foundry CLI ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases)
{: new_window}
* [快速參照卡 - cf 指令 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/cf_cli_refcard.html)
{: new_window}
