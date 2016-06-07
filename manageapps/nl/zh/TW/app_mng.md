---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#管理 Liberty 及 Node.js 應用程式
{: #app_management}

*前次更新：2016 年 3 月 17 日*

「應用程式管理」是一組開發及除錯公用程式，可以針對您在 {{site.data.keyword.Bluemix}} 上的 Liberty 和 Node.js 應用程式啟用。
{:shortdesc}

##「應用程式管理」公用程式
{: #Utilities}

這些公用程式同時支援 Liberty 及 Node.js。

  1. *proxy*：作為應用程式與 {{site.data.keyword.Bluemix_notm}} 間之 Proxy 的最小應用程式管理。

    若已啟用，建置套件會啟動位在應用程式執行時期與儲存器之間的 Proxy 代理程式。*proxy* 公用程式會處理應用程式接收的所有要求。根據要求類型，它會執行「應用程式管理」動作，或將要求轉遞給應用程式。*proxy* 容許啟用大部分其他「應用程式管理」公用程式。透過啟用 *proxy*，即使應用程式損毀，您的應用程式儲存器還是會繼續運作。Proxy 代理程式也容許進行漸進式檔案更新，以啟用 Node.js 應用程式的「即時編輯」模式。
	
  2. *devconsole*：啟用可在下列 URL 存取的開發主控台公用程式：
    ```
    http://<yourappname>.mybluemix.net/bluemix-debug/manage
    ```
	
    使用開發主控台，使用者可以重新啟動、停止或暫停其應用程式。使用者也可以啟用或存取 shell 及 inspector 公用程式。

    devconsole 公用程式也會啟動 *proxy*。
	
  3. *hc*：「性能檢測中心」代理程式，可讓「性能檢測中心用戶端」監視您的應用程式。

    「性能檢測中心」支援透過使用 IBM Monitoring and Diagnostic Tools 來分析 Liberty 及 Node.js 應用程式的效能。如需相關資訊，請參閱 [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}。</p></li>
	
  4. *shell*：啟用可從 devconsole 公用程式或透過存取下列 URL 進行存取的 Web 型 Shell：
    ```
    http://<yourappname>.mybluemix.net/bluemix-debug/shell
    ```
	
    在您存取 shell 公用程式之後，即會顯示終端機視窗，在視窗中會以 Shell 方式連入應用程式。您可以執行一般 Shell 中所支援的所有作業，例如編輯檔案、檢查記憶體用量，或執行診斷指令。
	
    *shell* 公用程式也會啟動 *proxy*。

這些公用程式僅支援 Liberty。

  1. *debug*：讓 Liberty 應用程式轉換為除錯模式，並讓用戶端（例如 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}）建立與應用程式的遠端除錯階段作業。
  
   如需相關資訊，請參閱[遠端除錯](../manageapps/eclipsetools/eclipsetools.html#remotedebug)。
   
   *debug* 公用程式也會啟動 *proxy*。
   
  2. *jmx*：使用 {{site.data.keyword.Bluemix_notm}} 使用者認證，以讓「JMX REST 連接器」容許遠端 JMX 用戶端管理應用程式。
  
  如需配置 JMX 連接器的相關資訊，請參閱 [Configuring secure JMX connection to the Liberty profile](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}。
  
  *jmx* 公用程式不會啟動 proxy。

這些公用程式僅支援 Node.js。

  1. *inspector*：啟用可從 *devconsole* 公用程式或 *https://myApp.mybluemix.net/bluemix-debug/inspector* 存取的 Node Inspector 除錯器介面。
  
  inspector 處理程序是在應用程式儲存器中執行。使用此公用程式，可建立 CPU 使用率設定檔、新增岔斷點，以及對程式碼進行除錯，而這些作業都是應用程式在 {{site.data.keyword.Bluemix_notm}} 上執行時進行。如需 Node Inspector 模組的相關資訊，請參閱 [GitHub 上的 node-inspector](https://github.com/node-inspector/node-inspector){:new_window}。
  
  *inspector* 公用程式也會啟動 *proxy*。
  
  2. *strongpm*：啟用 [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window}，以使用 [StrongLoop Metrics、Profiling 及 Tracing](https://strongloop.com/node-js/devops-tools/){:new_window} 之類的公用程式來分析 Node.js 應用程式。
    
  *strongpm* 公用程式也會啟動 *proxy*。
  
  採取下列步驟，以使用 [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} 來配置 Node.js 應用程式。

    1. 配置 *strongpm* BlUEMIX_APP_MGMT_ENABLE 環境變數，然後重新編譯打包應用程式。
    
	```
    cf set-env <appname> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <appname>
    ```
	
    2. 從 Cloud Foundry 指令行中，新增應用程式的路徑，其中路徑裡的應用程式名稱後面附加了 "-pm"，例如 <appname>-pm.mybluemix.net。
    
	```
    cf map-route <appname> ng.bluemix.net -n <appname>-pm
    ```
	
    3. 在本端工作站上安裝 [StrongLoop npm 模組](https://www.npmjs.com/package/strongloop){:new_window}。
    
	```
    npm install -g strongloop
    ```
	
    4. 在 [StrongLoop 網站](https://strongloop.com/register/){:new_window}上建立帳戶。
    5. 在本端工作站上啟動 Arc，並使用您建立的帳戶登入。
    
	```
    slc arc
    ```
	
    6. 導覽至 Arc 內的「程序管理程式」視圖。將含有埠 80 的新建路徑輸入「程序管理程式」。按「啟動」按鈕。如需詳細資料，請參閱[有關使用 Arc 的完整文件](https://docs.strongloop.com/display){:new_window}。
	
  3. *trace*：如果您的應用程式使用 *log4js*、*ibmbluemix* 或 *bunyan* 記載模組，則會動態設定追蹤層次。
  
  **附註：**支援的相依關係版本：

    * log4js：(0.6.0 - 0.6.24)
    * bunyan：（1.0.0、1.0.1、1.1.0 - 1.1.3、1.2.0 - 1.2.3、1.3.0 - 1.3.5）
    * ibmbluemix：(1.0.0-20140707-1250)-(1.0.0-20150409-1328)
  
  移至 {{site.data.keyword.Bluemix_notm}} Web 主控台中的「實例詳細資料」頁面，然後選取**動作**以查看使用者介面。

  *trace* 公用程式不會啟動 *proxy*。

##如何配置應用程式管理
{: #configure}

若要啟用「應用程式管理」公用程式，請設定 *BLUEMIX_APP_MGMT_ENABLE* 環境變數，然後重新編譯打包您的應用程式。可以使用 "+" 區隔多個公用程式來啟用它們。

例如，若要啟用 devconsole 及 *shell* 公用程式，請執行下列指令：

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

設定環境變數之後，不要忘記重新編譯打包應用程式：

```
cf restage myApp
```

如果不想和應用程式一起安裝「應用程式管理」公用程式，請將 *BLUEMIX_APP_MGMT_INSTALL* 環境變數設為 'false'，然後重新編譯打包應用程式。

例如：

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

##限制
{: #restrictions}

* 「應用程式管理」僅支援單一實例應用程式。
* 使用「應用程式管理」對應用程式進行的變更是暫時性的，會在結束此模式之後遺失。此模式僅供暫時開發使用，而且基於效能原因，不是用來作為正式作業環境。
* 如果您在 manifest.yml 檔案 (command) 或 CF CLI (-c) 中設定啟動指令，則大部分「應用程式管理」公用程式不會運作。這些方法是建置套件置換，而且是啟動 Node.js 應用程式的反面模式 (anti-pattern)。若要獲得最佳的結果，請在 package.json 檔案或 Procfile 中設定啟動指令。

##Eclipse Tools 的開發模式
{: #devmode}

開發模式是 [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools) 的一項特性，它讓開發人員能夠在應用程式於雲端執行的同時，處理他們的應用程式。

在 {{site.data.keyword.Bluemix_notm}} 上處理應用程式時，開發人員可能感覺他們無法像在本端環境中那樣地執行正常的開發活動。為了處理此問題，Eclipse Tools
的開發模式讓您能夠在暫時性的安全工作區裡，在雲端工作。

Liberty 和 Node.js 應用程式都支援開發模式。為您的 Liberty 或 Node.js 應用程式啟用開發模式之後，便可以漸進式地更新應用程式檔案，而不必推送應用程式。您也可以建立與應用程式的除錯階段作業。Liberty
應用程式的開發模式就等同於啟用 debug 和 jmx 等「應用程式管理」公用程式。對於 Node.js 應用程式，則等同於啟用 *devconsole*、*inspector* 及 *shell* 公用程式。
