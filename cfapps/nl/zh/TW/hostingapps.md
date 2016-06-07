---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#在 {{site.data.keyword.Bluemix_notm}} 中管理應用程式

*前次更新：2016 年 5 月 9 日*

<!--The whole topic is staging only -->

使用 {{site.data.keyword.Bluemix}}，您可以建立應用程式，以及管理現有應用程式。
只要應用程式具有雲端功能，就可以將應用程式移轉至 {{site.data.keyword.Bluemix_notm}}。{{site.data.keyword.Bluemix_notm}} 提供各種讓您執行應用程式的方法，例如，Cloud Foundry、IBM Containers 及 Virtual Machines。

##使應用程式具有雲端功能
{: #cloud-readyapps}

具有雲端功能的應用程式，在設計及建置應用程式時便已遵循雲端平台原則。具有雲端功能的應用程式可以使用雲端平台所提供的功能。

如果在應用程式中觀察到下列所有原則，則應用程式具有雲端功能，而且可以移轉至 {{site.data.keyword.Bluemix_notm}}。
如果應用程式中違反原則，則通常可以修改應用程式以遵守原則。

* 不要直接根據特定拓蹼來撰寫應用程式。

  在非雲端環境中，應用程式可能會使用特定部署拓蹼。不過，雲端應用程式中的應用程式拓蹼可能會變更，因為具有雲端功能的應用程式及服務容許立即的可擴充性變更。可擴充性變更包括動態擴充及手動重新調整應用程式的實例數量。

  盡可能將應用程式建置為通用且無狀態，以避免應用程式受到可擴充性變更的影響。

* 不要假設本端檔案系統是永久的。

  因為隨時都可能在雲端上移動、刪除或複製應用程式實例，所以請不要依賴寫入至檔案系統的檔案。如果應用程式使用本端檔案系統作為常用資訊（包括應用程式日誌）的快取，則當實例關閉並在不同的位置或不同的 VM 重新啟動時，資訊便會遺失。

  您可以將資訊儲存至服務（例如 SQL 或 NoSQL 資料庫），而非本端檔案系統。在動態雲端環境中，也一定要讓日誌存在於存活時間比產生日誌的應用程式實例還要久的服務上。

* 不要在應用程式中儲存階段作業狀態。

  系統狀態是由資料庫及共用儲存體所定義，而非由每一個個別執行中應用程式實例所定義。任何種類的狀態性都會限制應用程式的可擴充性。請嘗試將階段作業狀態儲存在伺服器上的集中位置，讓階段作業狀態的影響降到最低。

  如果您無法完全刪除階段作業狀態，請將它推送到應用程式伺服器以外的高可用儲存庫。儲存庫包括 IBM WebSphere Extreme Scale、Redis 或 Memcached，或是外部資料庫。

* 不要使用特定基礎架構相依關係。

  這是具有數種呈現的一般原則。例如，請不要假設應用程式所使用的服務被配置了特定主機名稱或 IP 位址。因為可能在雲端環境中重新定位或重新產生服務，所以主機名稱及 IP 位址也可能會變更。

  將環境特有相依關係擷取成一組內容檔，可以有所改善，但仍然不足。最佳作法是使用外部服務登錄來解析服務端點，或將整個遞送功能委派給具有虛擬名稱的服務匯流排或負載平衡器。

* 不要在應用程式中使用基礎架構 API。

  如果您在應用程式中依賴特定的基礎架構 API，則變更基礎架構會十分具挑戰性，因為基礎架構 API 可能參照軟體堆疊中的許多不同層。

  您可以改為依賴現有開放程式碼或商業產品，並將 PaaS 解決方案保留在 PaaS 層，讓它們獨立在您的應用程式碼之外。

* 不要使用模糊通訊協定。

  請不要使用需要額外配置的模糊通訊協定進行備援。

  根據標準通訊協定的應用程式將配置項目委派給平台時會較具復原力。標準通訊協定包括 HTTP、SSL、標準資料庫、佇列作業及 Web 服務連線。

* 不要依賴 OS 特有特性

  如果您已使用 OS 特有的特性，則可以使用相容性程式庫（例如 Cygwin 及 Mono）來修正此問題。Cygwin 是一個相容性程式庫，可在 Windows 環境中提供一組 Linux 工具。Mono 是一個相容性程式庫，可在 Linux 中提供 Windows .NET 功能。

  請避免 OS 特有的相依關係；請改用中介軟體基礎架構或服務提供者所提供的服務。

* 不要手動安裝應用程式。

  您的應用程式可能會經常要視需求安裝在動態雲端環境上。安裝處理程序必須 Script 化且可靠，而且必須將配置資料從 Script 裡外部化 (externalize) 出來。

  最起碼要將應用程式安裝擷取為一組統一且與作業系統無關的 Script。請將應用程式安裝保持到最小並為可攜式，以適合不同的自動化技術。此外，也請將應用程式安裝所需的相依關係降到最少。

如需具有雲端功能的應用程式的相關資訊，請參閱 [The Twelve-Factor App](http://12factor.net/){:new_window}。

##移轉應用程式
{: #ht_hostapp}

您可以使用漸進式方式將應用程式移轉至 {{site.data.keyword.Bluemix_notm}}，而不是完整將應用程式轉移至雲端環境。您可以先移轉應用程式的某個部分，並使用 Cloud Integration 服務以連接至現有資料或記錄系統。

在您的雲端應用程式中，您可能需要存取後端資料或服務（例如，記錄系統）。在 {{site.data.keyword.Bluemix_notm}} 中，您可以使用 Secure Gateway 服務以在 {{site.data.keyword.Bluemix_notm}} 組織與企業後端網路之間建立安全通道。服務可讓 {{site.data.keyword.Bluemix_notm}} 上的應用程式存取後端網路的資料及服務。如需詳細資料，請參閱 [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}。

若要將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 以作為 Cloud Foundry 應用程式，請從 {{site.data.keyword.Bluemix_notm}}「型錄」中選取執行時期。此執行時期包含入門範本 Hello World 應用程式，您可以將它取代為自己的應用程式。如果您找不到提供您想要之執行時期的入門範本，則可以使用 -b 選項與 cf push 指令搭配，將自訂 Cloud Foundry 相容建置套件帶到 {{site.data.keyword.Bluemix_notm}}。如需詳細資料，請參閱[使用社群建置套件](../cfapps/byob.html)。

您可以使用 {{site.data.keyword.Bluemix_notm}} 所提供的下列工具及服務：

*表 1. {{site.data.keyword.Bluemix_notm}} 工具*

| 工具	| 方法 |
|:------|:--------|
|Cloud Foundry 指令行介面 (cf cli)	|在本端用戶端上管理您的程式碼，以及使用 Cloud Foundry 指令行介面，手動將應用程式推送至 {{site.data.keyword.Bluemix_notm}}。如需相關資訊，請參閱[上傳應用程式](../starters/upload_app.html)。|
|Eclipse	|在 Eclipse 中管理您的程式碼，並且使用 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} 來推送應用程式。|
|Git 整合	|在 GitHub 上管理您的程式碼，以及將 Git 整合至 {{site.data.keyword.Bluemix_notm}}。您可以與其他開發人員分工合作。確定程式碼中的變更時，會自動將您的應用程式部署至 {{site.data.keyword.Bluemix_notm}}。您不需要手動推送應用程式。|
|{{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline	|在 DevOps GitHub 儲存庫上管理您的程式碼，以及使用 DevOps Delivery Pipeline 將應用程式部署至 {{site.data.keyword.Bluemix_notm}}。|


如果 Cloud Foundry 平台不支援您的應用程式需求，您可以使用其他自訂的選項來使用已設定、配置及維護執行時期的儲存器或 VM。

##使用 cf cli 上傳應用程式
{: #ht_cfcli}

您可以在本端用戶端上管理您的程式碼，以及使用 Cloud Foundry 指令行介面，手動將應用程式上傳至 {{site.data.keyword.Bluemix_notm}}。如果您變更程式碼，則必須重新將應用程式推送至 {{site.data.keyword.Bluemix_notm}}，以執行更新過的程式碼。

請採取下列步驟來移轉應用程式：

<ol>
<li>安裝 Cloud Foundry 指令行介面。請確定使用最新版本的 cf 指令行介面。<ol>
<li>下載適用於您作業系統的安裝程式。</li>
<li>遵循工具精靈以安裝指令行。</li>
<li>使用下列指令來驗證 cf 指令行介面的版本：<pre>cf -v</pre></li>
</ol>
</li>

<li>選用項目：如果您要先指定並儲存部署詳細資料，再將應用程式推送至 {{site.data.keyword.Bluemix_notm}}，則可以採取下列步驟來新增應用程式資訊清單：
<ol>
<li>移至應用程式的工作目錄，並建立標題為 manifest.yml（預設名稱）的檔案。</li>
<li>在資訊清單檔中，指定部署詳細資料。下列範例顯示 Java™ 應用程式的資訊清單檔。
<pre class="pre codeblock"><code>applications:
- disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M</code></pre>
<p>如需可以在此檔案中使用之所支援選項的相關資訊，請參閱[應用程式資訊清單](../manageapps/depapps.html#appmanifest)。</p></li></ol>
</li>

<li>推送應用程式。您可以使用 cf push 指令來上傳應用程式。<ol>
<li>執行下列指令，以連接並登入 {{site.data.keyword.Bluemix_notm}}。請在提示時選取您的組織及空間。<pre>cf login -a https://api.ng.bluemix.net</pre></li>
<li>從您的應用程式目錄，輸入 cf push 指令與應用程式名稱。應用程式名稱在 {{site.data.keyword.Bluemix_notm}} 環境中必須是唯一的。<pre>cf push appname</pre></li>
<li>選用項目：如果您使用外部建置套件，則必須使用 -b 選項與 cf push 指令搭配。例如：
<pre>cf push appname -b buildpack_URL</pre>
<p>如需詳細資料，請參閱「使用社群建置套件」。</p>
</li></ol>
</li>

<li>選用項目：如果您變更應用程式，則必須重新輸入 cf push 指令來上傳那些變更。cf 指令行介面會使用您先前的選項以及對提示的回應，以一小段新的程式碼來更新應用程式的所有執行中實例。</li>
</ol>

**附註：**

* 使用 cf push 指令時，cf 指令行介面會將所有檔案及目錄從現行目錄複製到 {{site.data.keyword.Bluemix_notm}}。確定應用程式目錄中只有所需的檔案。
* 確定您的組織有足夠的記憶體可供應用程式的所有實例使用。若要檢視您組織的記憶體配額，請使用 cf org org_name。
* 如需 cf push 的相關資訊，請參閱 [cf 指令](../cli/reference/cfcommands/index.html)。

##移轉資料及使用服務
{: #ht_service}

將應用程式上傳至 {{site.data.keyword.Bluemix_notm}} 之後，請從 {{site.data.keyword.Bluemix_notm}}「型錄」選取您應用程式所連接的服務、建立服務實例、將實例連結至應用程式，然後重新啟動應用程式。

您應用程式的 VCAP_SERVICES 環境變數是 JSON 物件，而此物件包含如何與 {{site.data.keyword.Bluemix_notm}} 中的服務實例互動的相關資訊。此資訊包括服務實例名稱、認證，以及與服務實例的連線 URL。

若要在 {{site.data.keyword.Bluemix_notm}} 中執行程式碼，您必須新增程式碼邏輯，以剖析 VCAP_SERVICES 變數來取得服務連線的相關資訊。請修改應用程式，以透過環境變數來取得服務實例的動態指派主機及埠。下列範例顯示如何在 Ruby 應用程式中取得 Postgre SQL 服務實例的認證：

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)

        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```		
{:codeblock}

若要確定在修改 {{site.data.keyword.Bluemix_notm}} 的應用程式之後可以在本端環境中執行您的應用程式，請檢查 VCAP_SERVICES 環境變數是否存在（此環境變數是針對所有 {{site.data.keyword.Bluemix_notm}} Cloud Foundry 應用程式所設定）。


# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

* [IBM Containers](../containers/container_cli_ov.html)
* [Virtual Machines](../virtualmachines/vm_index.html)
* [開始使用 Delivery Pipeline](../services/DeliveryPipeline/index.html)
* [使用 IBM Eclipse Tools for Bluemix 來部署應用程式](../manageapps/eclipsetools/eclipsetools.html)
* [The Twelve-Factor App](http://12factor.net/){:new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}
