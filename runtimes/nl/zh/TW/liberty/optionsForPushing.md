---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 推送 Liberty 應用程式的選項
{: #options_for_pushing}

*前次更新：2016 年 3 月 23 日*

Liberty 伺服器在 Bluemix 中的行為受 Liberty 建置套件所控制。建置套件可以為特定的應用程式類別提供完整的執行時期環境。
它們對於在雲端之間提供可攜性以及對開放式雲端架構的貢獻而言很關鍵。Liberty 建置套件提供 WebSphere Liberty 儲存器，可以執行 Java EE 7 及 OSGi 應用程式。
它支援例如 Spring 的熱門架構，且包含了 IBM JRE。WebSphere Liberty 讓您能進行適合雲端的快速應用程式開發。Liberty 建置套件支援部署到單一 Liberty 伺服器的多個應用程式。當 Liberty 建置套件整合到 Bluemix 時，建置套件會確保連結服務的環境變數在 Liberty 伺服器中都顯示為配置變數。

您可以使用下列方法將 Liberty 應用程式部署至 Bluemix。

* 推送獨立式應用程式
* 推送伺服器目錄
* 推送包裝伺服器

重要事項：當您使用 Liberty 建置套件部署應用程式時，請至少指定 512M 作為應用程式的記憶體限制。如需相關資訊，請參閱[記憶體限制與 Liberty 建置套件](memoryLimits.html)。

## 獨立式應用程式
{: #stand_alone_apps}

獨立式應用程式（例如 WAR 檔或 EAR 檔）可部署至 Bluemix 中的 Liberty。

若要部署獨立式應用程式，請執行 cf push 指令並搭配 -p 參數，以指向您的 WAR 檔或 EAR 檔。
例如：

```
    $ cf push <yourappname> -p myapp.war
```
{: #codeblock}

部署獨立式應用程式之後，會為該應用程式提供預設的 Liberty 配置。預設配置會啟用下列 Liberty 特性：

* beanValidation-1.1
* [cdi-1.2](optionsForPushing.html#cdi12)
* ejbLite-3.2
* el-3.0
* jaxrs-2.0
* jdbc-4.1
* jndi-1.0
* jpa-2.1
* jsf-2.2
* jsonp-1.0
* jsp-2.3
* managedBeans-1.0
* servlet-3.1
* websocket-1.1
* icap:managementConnector-1.0
* appstate-1.0

這些特性對應於 Java EE 7 Web 設定檔特性。您可以透過設定 JBP_CONFIG_LIBERTY 環境變數來指定另一組 Liberty 特性。例如，若只要啟用 jsp-2.3 及 websocket-1.1 特性，請執行指令並重新編譯打包應用程式：

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: {features: [jsp-2.3, websocket-1.1]}"
```
{: #codeblock}

附註：若要取得最佳結果，請使用 JBP_CONFIG_LIBERTY 環境變數設定 Liberty 特性，或使用自訂 server.xml 檔案，將應用程式部署為[伺服器目錄](optionsForPushing.html#server_directory)或[包裝伺服器](optionsForPushing.html#packaged_server)。設定此環境變數可確保您的應用程式只使用它需要的特性，且不受建置套件預設 Liberty 特性集變更的影響。如果您需要提供特性集以外的額外 Liberty 配置，請使用[伺服器目錄](optionsForPushing.html#server_directory)或[包裝伺服器](optionsForPushing.html#packaged_server)選項來部署應用程式。

如果您已部署 WAR 檔，則可以在內嵌的 ibm-web-ext.xml 檔案中所設定的環境定義根目錄下存取 Web 應用程式。如果 ibm-web-ext.xml 檔案不存在，或未指定環境定義根目錄，則可以在根環境定義下存取應用程式。例如，
				

```
    http://<yourappname>.mybluemix.net/
```
{: #codeblock}

如果您已部署 EAR 檔，可在 EAR 部署描述子所定義的環境定義根目錄下，存取內嵌的 Web 應用程式。例如：

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

整個預設的 Liberty server.xml 配置檔如下：
```
    <server>
       <featureManager>
          <feature>beanValidation-1.1</feature>
          <feature>cdi-1.2</feature>
          <feature>ejbLite-3.2</feature>
          <feature>el-3.0</feature>
          <feature>jaxrs-2.0</feature>
          <feature>jdbc-4.1</feature>
          <feature>jndi-1.0</feature>
          <feature>jpa-2.1</feature>
          <feature>jsf-2.2</feature>
          <feature>jsonp-1.0</feature>
          <feature>jsp-2.3</feature>
          <feature>managedBeans-1.0</feature>
          <feature>servlet-3.1</feature>
          <feature>websocket-1.1</feature>
          <feature>icap:managementConnector-1.0</feature>
          <feature>appstate-1.0</feature>
       </featureManager>

       <application name='myapp' location='myapp.war' type='war' context-root='/'/>
       <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='${port}'/>
       <webContainer trustHostHeaderPort='true' extractHostHeaderPort='true'/>
       <include location='runtime-vars.xml'/>
       <logging logDirectory='${application.log.dir}' consoleLogLevel='INFO'/>
       <httpDispatcher enableWelcomePage='false'/>
       <applicationMonitor dropinsEnabled='false' updateTrigger='mbean'/>
       <config updateTrigger='mbean'/>
       <cdi12 enableImplicitBeanArchives='false'/>
       <appstate appName='myapp' markerPath='${home}/../.liberty.state'/>
    </server>
```
{: #codeblock}

### CDI 1.2
{: #cdi12}

由於效能的原因，只部署 WAR 和 EAR 檔時，依預設會停用 [CDI 1.2 隱含 Bean 保存檔掃描](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_cdi_behavior.html)。隱含 Bean 保存檔掃描可以使用 JBP_CONFIG_LIBERTY 環境變數加以啟用。例如：

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: { implicit_cdi: true }"
```    
{: #codeblock}

重要事項：為了讓環境變數的變更能夠生效，您必須重新編譯打包應用程式：

```
    $ cf restage myapp
```
{: #codeblock}

## 伺服器目錄
{: #server_directory}

在某些情況下，可能會需要與應用程式一起提供自訂 Liberty 伺服器配置。當您部署 WAR 檔或 EAR 檔，且預設 server.xml 檔案沒有您應用程式需要的特定設定時，則可能需要此自訂配置。

如果 Liberty 設定檔已安裝在您的工作站上，而且您已經使用應用程式建立 Liberty 伺服器，就可以將該目錄的內容推送至 Bluemix。例如，如果您的 Liberty 伺服器名稱為 defaultServer，請執行下列指令：

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer
```
{: #codeblock}

如果您的工作站上未安裝 Liberty 設定檔，您可以使用下列步驟，以您的應用程式來建立伺服器目錄：

1. 建立名稱為 defaultServer 的目錄。
2. 在 defaultServer 目錄中建立 apps 目錄。
3. 將您的 WAR 檔或 EAR 檔複製到 defaultServer/apps 目錄中。
4. 在 defaultServer 目錄中，建立含有下列範例內容的 server.xml 檔案。此外：
  * 請務必更新 application 元素的 location 或 type 屬性，以符合您應用程式的檔名和類型。
  * 此圖中的 server.xml 檔案顯示最小特性集。依據應用程式的需求，您可能必須調整特性集。

```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
        </featureManager>

        <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='8080' />

        <application name="myapp" context-root="/" type="war" location="myapp.war"/>
    </server>
```
{: #codeblock}

伺服器目錄備妥之後，您可以將它部署至 Bluemix。

```
    $ cf push <yourappname> -p defaultServer
```
{: #codeblock}

附註：已部署為該伺服器目錄一部分的 Web 應用程式，可在[環境定義根目錄（由 Liberty 設定檔決定）](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_dep_war.html?cp=SSAW57_8.5.5%2F1-3-11-0-5-6)下進行存取。例如：

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

## 包裝伺服器
{: #packaged_server}

您也可以將包裝伺服器檔案推送至 Bluemix。包裝伺服器檔案是使用 Liberty 的 server package 指令所建立。除了應用程式和配置檔之外，包裝伺服器檔案還可以包含應用程式所需的共用資源和 Liberty 使用者特性。

若要包裝 Liberty 伺服器，請從您的 Liberty 安裝目錄使用 ./bin/server package 指令。請指定伺服器名稱，並包含 '––include=usr' 選項。例如，如果您的 Liberty 伺服器為 defaultServer，請執行下列指令：

```
    $ wlp/bin/server package defaultServer --include=usr
```
{: #codeblock}

這個指令會在伺服器目錄中產生 serverName.zip 檔案。然後，您可以使用 cf push 指令，將該壓縮檔推送至 Bluemix。例如：

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer/defaultServer.zip
```
{: #codeblock}

附註：已部署為包裝伺服器一部分的 Web 應用程式，可在環境定義根目錄（由 Liberty 設定檔決定）下進行存取。

### server.xml 檔案的修改
{: #modifications_of_serverxml}

推送包裝伺服器或 Liberty 伺服器目錄時，Liberty 建置套件會偵測到您的應用程式所附的 server.xml 檔案。Liberty 建置套件會對 server.xml 檔案進行下列修改。

* 建置套件會確定在檔案中恰好有一個 httpEndpoint 元素。
* 建置套件會確定 httpEndpoint 元素中的 httpPort 屬性指向名稱為 ${port} 的系統變數。建置套件也會置換 host 屬性。
* 建置套件會將 logging 元素中的 logDirectory 屬性設為指向系統日誌目錄。
* 建置套件會確定 runtime-vars.xml 檔案與您的 server.xml 檔案進行邏輯合併。具體而言，建置套件會將 *&lt;include location="runtime-vars.xml" /&gt;* 這一行附加到 server.xml 檔案中。

### 可參照的變數
{: #referenceable_variables}

下列變數定義在 runtime-vars.xml 檔案中，並從推送的 server.xml 檔案進行參照。所有變數都區分大小寫。

* ${port}：Liberty 伺服器接聽所在的 HTTP 埠。
* ${vcap_console_port}：vcap 主控台執行所在的埠（通常與 ${port} 相同）。
* ${vcap_app_port}：應用程式伺服器接聽所在的埠（通常與 ${port} 相同）。
* ${vcap_console_ip}：vcap 主控台的 IP 位址（通常是 Liberty 伺服器接聽所在的 IP 位址）。
* ${application_name}：應用程式的名稱，如同使用 cf push 指令中的選項所定義。
* ${application_version}：此應用程式實例的版本，其格式為 UUID，例如 b687ea75-49f0-456e-b69d-e36e8a854caa。這個變數會隨著每次後續推送包含新程式碼或應用程式構件變更的應用程式而變更。
* ${host}：執行應用程式之 DEA 的 IP 位址（通常與 ${vcap_console_ip} 相同）。
* ${application_uris}：可以用來存取這個應用程式之端點 JSON 樣式陣列，例如：myapp.mydomain.com。
* ${start}：應用程式啟動的時間和日期，採用的格式類似 2013-08-22 10:10:18 -0400。

### 存取已連結服務的資訊
{: #accessing_info_of_bound_services}

當您想要將服務連結至應用程式時，在 Cloud Foundry 為應用程式設定的 [VCAP_SERVICES 環境變數](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html#VCAP-SERVICES)中會包含服務的相關資訊，例如連線認證。對於[自動配置的服務](autoConfig.html)，Liberty 建置套件會在 server.xml 檔案中產生或更新服務連結項目。服務連結項目的內容可能為下列其中一種格式：

* cloud.services.&lt;service-name&gt;.&lt;property&gt;，其說明服務的資訊，例如名稱、類型及方案。
* cloud.services.&lt;service-name&gt;.connection.&lt;property&gt;，其說明服務的連線資訊。

一般的資訊集如下所示：
* name：服務的名稱。例如，mysql-e3abd。
* label：所建立服務的類型。例如，mysql-5.5。
* plan：服務方案，如該方案的唯一 ID 所指示。例如，100。
* connection.name：連線的唯一 ID，其採用 UUID 的格式。例如，d01af3a5fabeb4d45bb321fe114d652ee。
* connection.hostname：執行服務之伺服器的主機名稱。例如，mysql-server.mydomain.com。
* connection.host：執行服務之伺服器的 IP 位址。例如，9.37.193.2。
* connection.port：服務接聽送入連線的埠。例如 3306、3307。
* connection.user：用來向服務鑑別此應用程式的使用者名稱。使用者名稱是由 Cloud Foundry 自動產生。例如：unHwANpjAG5wT。
* connection.username：connection.user 的別名。
* connection.password：用來向服務鑑別此應用程式的密碼。密碼是由 Cloud Foundry 自動產生。例如：pvyCY0YzX9pu5。

對於 Liberty 建置套件未自動配置的連結服務，應用程式需要自行管理後端資源的存取。

# 相關鏈結
## 一般
* [Liberty 執行時期](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
