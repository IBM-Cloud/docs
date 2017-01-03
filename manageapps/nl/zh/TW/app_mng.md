---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#管理 Liberty 及 Node.js 應用程式
{: #app_management}


「應用程式管理」是一組開發及除錯公用程式，可以針對您在 {{site.data.keyword.Bluemix}} 上的 Liberty 和 Node.js 應用程式啟用。
{:shortdesc}

## 「應用程式管理」公用程式
{: #Utilities}

### 這些公用程式同時支援 Liberty 及 Node.js
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

*proxy* 提供您應用程式與 {{site.data.keyword.Bluemix_notm}} 之間的最低應用程式管理。

若已啟用，建置套件會啟動位在應用程式運行環境與容器之間的 Proxy 代理程式。*proxy* 公用程式會處理應用程式接收的所有要求。根據要求類型，它會執行「應用程式管理」動作，或將要求轉遞給應用程式。*proxy* 容許啟用大部分其他「應用程式管理」公用程式。透過啟用 *proxy*，即使應用程式損毀，您的應用程式容器還是會繼續運作。Proxy 代理程式也容許進行漸進式檔案更新，以啟用 Node.js 應用程式的「即時編輯」模式。

#### devconsole
{: #devconsole}

您可在下列 URL 存取 (*devconsole*) 開發主控台公用程式：
```
http://<yourappname>.mybluemix.net/bluemix-debug/manage
    ```

使用開發主控台，使用者可以重新啟動、停止或暫停其應用程式。使用者也可以啟用或存取 shell 及 inspector 公用程式。

針對 Node 6.3.0 版或以上版本，開發主控台提供您應用程式的重新啟動按鈕，以及對 shell 公用程式的存取。如需相關資訊，請參閱 *inspector* 討論。

devconsole 公用程式也會啟動 *proxy*。

#### hc
{: #hc}

「(*hc*) 性能檢測中心」代理程式可讓「性能檢測中心」用戶端監視您的應用程式。

「性能檢測中心」支援透過使用 IBM Monitoring and Diagnostic Tools 來分析 Liberty 及 Node.js 應用程式的效能。如需相關資訊，請參閱 [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}。</p></li>

#### shell
{: #shell}

*shell* 公用程式可啟用 Web 型 Shell。它可以從 *devconsole* 公用程式或透過存取下列 URL 來進行存取：

```
http://<yourappname>.mybluemix.net/bluemix-debug/shell
    ```

在您存取 *shell* 公用程式之後，即會顯示終端機視窗，在視窗中會以 Shell 方式連入應用程式。您可以執行一般 Shell 中所支援的所有作業，例如編輯檔案、檢查記憶體用量，或執行診斷指令。

*shell* 公用程式也會啟動 *proxy*。

### 這些公用程式僅支援 Liberty
{: #liberty_utilities}

#### debug
{: #debug}

*debug* 公用程式可讓 Liberty 應用程式進入除錯模式，並讓用戶端（例如 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}）建立與應用程式的遠端除錯階段作業。

如需相關資訊，請參閱[遠端除錯](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug)。

*debug* 公用程式也會啟動 *proxy*。

#### jmx
{: #jmx}

*jmx* 公用程式可使用 {{site.data.keyword.Bluemix_notm}} 使用者認證，讓「JMX REST 連接器」容許遠端 JMX 用戶端管理應用程式。

如需配置 JMX 連接器的相關資訊，請參閱 [Configuring secure JMX connection to the Liberty profile](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}。

*jmx* 公用程式不會啟動 proxy。

### 這些公用程式僅支援 Node.js
{: #node_utilities}

#### inspector
{: #inspector}

針對 Node.js 6.3.0 之前的版本，*inspector* 啟用可從 *devconsole* 公用程式或 *https://myApp.mybluemix.net/bluemix-debug/inspector* 存取的 Node Inspector 除錯器介面。

*inspector* 處理程序是在應用程式容器中執行。使用此公用程式，可建立 CPU 用量設定檔、新增岔斷點，以及對程式碼進行除錯，而這些作業都是應用程式在 {{site.data.keyword.Bluemix_notm}} 上執行時進行。如需 Node Inspector 模組的相關資訊，請參閱 [GitHub 上的 node-inspector](https://github.com/node-inspector/node-inspector){:new_window}。

*inspector* 公用程式也會啟動 *proxy*。

針對 Node.js 6.3.0 版及以上版本，*inspector* 會使用 [Inspector Integration for Node.js 第 8 版](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}。在您應用程式的日誌中，您會尋找可用來將 Chrome DevTools 附加至您應用程式的 URL。日誌訊息類似於下列內容：

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node-hc --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

在此情境中，*devconsole* 將**不**會顯示 *inspector* 的鏈結，因為 URL 不存在。

在此情境中，*proxy* 不會將資料流量遞送至 *inspector*。您需要建立與您應用程式的 SSH 通道，Chrome DevTools URL 才能運作。若要建立 SSH 通道，請透過與下列類似的方式來使用 'cf ssh' 指令：

```
  cf ssh -N -T -L <port>:127.0.0.1:<hostport> <appName>
```

在此指令中，*hostport* 應該是「接聽埠 xxxx 的除錯器」日誌訊息中的埠值，而 *port* 是從中發出 "cf ssh" 指令的系統上的任何可用埠。

#### trace
{: #trace}

*trace* 公用程式可讓您在應用程式使用 *log4js*、*ibmbluemix* 或 *bunyan* 記載模組時動態設定追蹤層次。

**附註：**支援的相依關係版本：
* log4js：(0.6.0 - 0.6.24)
* bunyan：（1.0.0、1.0.1、1.1.0 - 1.1.3、1.2.0 - 1.2.3、1.3.0 - 1.3.5）
* ibmbluemix：(1.0.0-20140707-1250)-(1.0.0-20150409-1328)

移至 {{site.data.keyword.Bluemix_notm}} Web 主控台中的「實例詳細資料」頁面，然後選取**動作**以查看使用者介面。

使用 "-b buildpack" 選項啟動應用程式時，無法使用 *trace* 公用程式。

*trace* 公用程式不會啟動 *proxy*。

##  如何配置應用程式管理
{: #configure}

若要啟用「應用程式管理」公用程式，請設定 *BLUEMIX_APP_MGMT_ENABLE* 環境變數，然後重新編譯打包您的應用程式。可以使用 "+" 區隔多個公用程式來啟用它們。

例如，若要啟用 *devconsole* 及 *shell* 公用程式，請執行下列指令：

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

設定環境變數之後，請重新編譯打包應用程式：

```
cf restage myApp
```

如果不想和應用程式一起安裝「應用程式管理」公用程式，請將 *BLUEMIX_APP_MGMT_INSTALL* 環境變數設為 'false'，然後重新編譯打包應用程式。

例如：

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

## 限制
{: #restrictions}

* 「應用程式管理」僅支援單一實例應用程式。
* 使用「應用程式管理」對應用程式進行的變更是暫時性的，會在結束此模式之後遺失。此模式僅供暫時開發使用，而且基於效能原因，不是用來作為正式作業環境。
* 如果您在 manifest.yml 檔案 (command) 或 CF CLI (-c) 中設定啟動指令，則大部分「應用程式管理」公用程式不會運作。這些方法是建置套件置換，而且是啟動 Node.js 應用程式的反面模式 (anti-pattern)。若要獲得最佳的結果，請在 package.json 檔案或 Procfile 中設定啟動指令。

## Eclipse Tools 的開發模式
{: #devmode}

開發模式是 [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) 的一項特性，它讓開發人員能夠在他們的應用程式於雲端執行的同時，處理這些應用程式。

在 {{site.data.keyword.Bluemix_notm}} 上處理應用程式時，開發人員可能感覺他們無法像在本端環境中那樣地執行正常的開發活動。為了處理此問題，Eclipse Tools
的開發模式讓您能夠在暫時性的安全工作區裡，在雲端工作。

Liberty 和 Node.js 應用程式都支援開發模式。為您的 Liberty 或 Node.js 應用程式啟用開發模式之後，便可以漸進式地更新應用程式檔案，而不必推送應用程式。您也可以建立與應用程式的除錯階段作業。Liberty
應用程式的開發模式就等同於啟用 debug 和 jmx 等「應用程式管理」公用程式。對於 Node.js 應用程式，則等同於啟用 *devconsole*、*inspector* 及 *shell* 公用程式。
