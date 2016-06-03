---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cloud Foundry (cf) 指令

*前次更新：2016 年 1 月 29 日*

您可以使用 Cloud Foundry (cf) 指令來管理應用程式。
{:shortdesc}

下列資訊會列出最常用來管理應用程式的 cf 指令。若要列出所有 cf 指令及其說明資訊，請使用 `cf help`。使用 `cf command_name -h` 可檢視特定指令的詳細說明資訊。

*附註：*如果您的網路在執行 cf 指令的主機與 Cloud Foundry API 端點之間包含 HTTP Proxy 伺服器，您必須藉由設定 `HTTP_PROXY` 環境變數來指定 Proxy 伺服器的主機名稱或 IP 位址。如需詳細資料，請參閱 [Using the cf CLI with an HTTP Proxy Server](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html)。

## cf api

顯示或指定 {{site.data.keyword.Bluemix_notm}} API 端點的 URL。
```
cf api BluemixServerURL
```
<dl>
<dt>BluemixServerURL</dt>
<dd>Bluemix API 端點的 URL，您在連接至 {{site.data.keyword.Bluemix_notm}} 時必須予以指定。這個 URL 通常是 https://api.{DomainName}。
如果您要顯示目前所使用 API 端點的 URL，則不需要針對 cf api 指令指定此參數。</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>停用 SSL 驗證處理程序。使用此參數可能導致安全問題。</dd>
<dt>*--unset*</dt>
<dd>移除所有 API 端點的連線資訊。</dd>
</dl>

## cf apps

列出您已部署在現行空間的所有應用程式。也會顯示每個應用程式的狀態。

假設您有一個應用程式的實例，則如果您的應用程式啟動，則會在 cf apps 指令回應的實例直欄中看到 1/1，如果您的應用程式關閉，則會看到 0/1。如果您看到指出應用程式實例狀態不明的 ?/1，則可以將應用程式 URL 複製到瀏覽器，以檢查應用程式是否有回應，或者您可以透過 `cf logs appname` 指令來讀取日誌尾端的內容，查看應用程式是否正在產生日誌內容。

## cf bind-service

將現有服務實例連結至您的應用程式。
```
cf bind-service appname service_instance
```

例如，如果您在現行組織及空間中有一個名為 `my_dataworks` 的服務實例，可以使用
`cf bind-service my_app my_dataworks` 將這個服務實例連結到您的應用程式。

<dl>
<dt>appname</dt>
<dd>應用程式的名稱。</dd>
<dt>service_instance</dt>
<dd>現有服務實例的名稱。</dd>
</dl>

## cf create-service

建立服務實例。
```
cf create-service service_name service_plan service_instance
```
例如，您可以使用 `cf create-service DataWorks free my_dataworks`，建立使用免費方案的 {{site.data.keyword.dataworks_short}} 服務實例。

<dl>
<dt>service_name</dt>
<dd>服務的名稱。</dd>
<dt>service_plan</dt>
<dd>服務方案的名稱。</dd>
<dt>service_instance</dt>
<dd>您要用於所建立之新服務實例的名稱。</dd>
</dl>

## cf create-space

建立空間。
```
cf create-space space_name
```
<dl>
<dt>space_name</dt>
<dd>空間的名稱。</dd>
<dt>*-o*</dt>
<dd>您要在其內建立空間的組織名稱。</dd>
<dt>*-q*</dt>
<dd>要指派給新建立空間的配額。如果未指定，則會自動指派一個預設配額。</dd>
</dl>

## cf delete

刪除現有應用程式。
```
cf delete appname
```
<dl>
<dt>appname</dt>
<dd>應用程式的名稱。<dd>
<dt>*-f*</dt>
<dd>強制刪除應用程式而不進行任何確認。這是選用性的參數。</dd>
<dt>*-r*</dt>
<dd>刪除與應用程式相關聯的所有網域名稱。這是選用性的參數。</dd>
</dl>

## cf delete-space

刪除空間。
```
cf delete-space space_name
```
<dl>
<dt>space_name</dt>
<dd>空間的名稱。</dd>
<dt>*-f*</dt>
<dd>強制刪除空間而不進行任何確認。這是選用性的參數。</dd>
*附註：*刪除空間是一項無法回復的作業。
</dl>

## cf events

顯示與應用程式相關的執行時期事件。
```
cf events appname
```
<dl>
<dt>appname</dt>
<dd>應用程式的名稱。</dd>
</dl>

## cf help

顯示所有 cf 指令的說明資訊，或是在使用 command_name 參數時顯示特定 cf 指令的說明資訊。
```
cf help command_name
```
<dl>
<dt>command_name</dt>
<dd>指令的名稱。如果您需要指令特有的說明資訊，可以使用此參數。</dd>
<dd>如果不指定此參數，則會顯示所有 cf 指令的說明資訊。</dd>
</dl>


## cf login

讓您登入 {{site.data.keyword.Bluemix_notm}}。
```
cf login
```
您可以在發出 cf login 指令時使用下列一個以上參數：
<dl>
<dt>*-a* https://api.{DomainName}</dt>
<dd>{{site.data.keyword.Bluemix_notm}} API 端點的 URL。這是選用性的參數。</dd>
<dt>*-u* user_name</dt>
<dd>您的使用者名稱。這是選用性的參數。</dd>
<dt>*-p* password</dt>
<dd>您的密碼。</dd>
<dd>*重要事項：*如果您在指令行介面上使用 *-p* 參數提供密碼，密碼可能會記錄在指令行歷程中。為了安全因素，請避免使用 -p 參數提供密碼。請改為在指令行介面提示您時再輸入密碼。</dd>
<dt>*-o* organization_name</dt>
<dd>您要登入的組織名稱。</dd>
<dt>*-s* space_name</dt>
<dd>您要登入的空間名稱。</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>停用 SSL 驗證處理程序。使用此參數可能導致安全問題。</dd>
</dl>

*附註：*如果您在此指令的 *-p* 參數中提供密碼，您的密碼可能會記錄在 Shell 指令歷程檔案，且可能被本端作業系統的其他使用者看到。


## cf logs

顯示應用程式的 STDOUT 及 STDERR 日誌串流。
```
cf logs appname
```
<dl>
<dt>appname</dt>
<dd>應用程式的名稱。</dd>
<dt>*--recent*</dt>
<dd>擷取最近的日誌。</dd>
</dl>

## cf marketplace

列出 Marketplace 中可用的所有服務。這個指令所列出的服務也會顯示在 {{site.data.keyword.Bluemix_notm}}「型錄」中。
```
cf marketplace
```

## cf push

將新的應用程式部署至 Bluemix，或在 Bluemix 中更新現有的應用程式。
```
cf push appname 
```
<dl>
<dt>appname</dt>
<dd>應用程式的名稱。</dd>
<dt>*-b* buildpack_name</dt>
<dd>建置套件的名稱。buildpack_name 可以是依名稱或 Git URL 的自訂建置套件，例如，`my-buildpack` 或 `https://github.com/heroku/heroku-buildpack-play.git`。</dd>
<dt>*-c* start_command</dt>
<dd>應用程式的啟動指令。若要使用預設的啟動指令，請針對這個選項指定 null 值。例如：</dd>
<dd>```
cf push appname -c null
```</dd>
<dd>您也可以使用這個選項來執行 Script 檔。例如：
```
cf push appname -c "bash ./<run.sh>"
```</dd>
<dt>*-f* manifest_path</dt>
<dd>資訊清單檔的路徑。預設資訊清單檔是您應用程式根目錄底下的 manifest.yml。</dd>
<dt>*-i* instance_number</dt>
<dd>實例數。</dd>
<dt>*-k* disk_limit</dt>
<dd>應用程式的磁碟限制，例如 *256M*、*1024M* 或 *1G*。</dd>
<dt>*-m* memory_limit</dt>
<dd>應用程式的記憶體限制，例如 *256M*、*1024M* 或 *1G*。</dd>
<dt>*-n* host_name</dt>
<dd>應用程式的主機名稱，例如 *my-subdomain*。</dd>
<dt>*-p* app_path</dt>
<dd>應用程式目錄或應用程式保存檔的路徑。</dd>
<dt>*-t* timeout</dt>
<dd>應用程式啟動的時間上限（秒）。其他伺服器端的逾時可能會置換此值。</dd>
<dt>*-s* stackname</dt>
<dd>要執行應用程式的堆疊。堆疊是預先建置的檔案系統（包括作業系統）。使用 `cf stacks`，以檢視 {{site.data.keyword.Bluemix_notm}} 中的可用堆疊。</dd>
<dt>*--no-hostname*</dt>
<dd>將 Bluemix 系統網域對映到此應用程式。</dd>
<dt>*--no-manifest*</dt>
<dd>忽略預設資訊清單檔。</dd>
<dt>*--no-route*</dt>
<dd>不要對映路徑至此應用程式。</dd>
<dt>*--no-start*</dt>
<dd>部署應用程式之後不要啟動應用程式。</dd>
<dt>*--random-route*</dt>
<dd>建立應用程式的隨機路徑。</dd>
</dl>

## cf scale

顯示或變更應用程式的實例數目、磁碟空間限制及記憶體限制。
```
cf scale appname -i instance_number -k disk_limit -m memory_limit
```
<dl>
<dt>appname</dt>
<dd>應用程式的名稱。</dd>
<dt>*-i* instance_number</dt>
<dd>實例數。</dd>
<dt>*-k* disk_limit</dt>
<dd>應用程式的磁碟限制，例如 *256M*、*1024M* 或 *1G*。</dd>
<dt>*-m* memory_limit</dt>
<dd>應用程式的記憶體限制，例如 *256M*、*1024M* 或 *1G*。</dd>
<dt>*-f*</dt>
<dd>強制應用程式重新啟動而不提示。</dd>
</dl>

## cf services

列出現行空間中可用的所有服務。
```
cf services
```

## cf set-env

設定應用程式的環境變數。
```
cf set-env appname var_name var_value
```
<dl>
<dt>appname</dt>
<dd>應用程式的名稱。</dd>
<dt>var_name</dt>
<dd>環境變數的名稱。</dd>
<dt>var_value</dt>
<dd>環境變數的值。</dd>
</dl>

## cf stacks

列出所有堆疊。堆疊是預先建置的檔案系統，包括可以執行應用程式的作業系統。
```
cf stacks
```

## cf stop

停止應用程式。
```
cf stop appname
```
<dl>
<dt>appname</dt>
<dd>應用程式的名稱。</dd>
</dl>

## cf -v

顯示 cf 指令行介面的版本。
```
cf -v
```

# 相關鏈結
{: #rellinks}
## 一般 
{: #general}
* [快速參照卡 - cf 指令](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
