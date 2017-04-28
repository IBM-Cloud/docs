---

copyright:
  years: 2017
lastupdated: "2017-04-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 疑難排解
{: #ts}

記載 {{site.data.keyword.dev_cli_notm}} 的部分已知問題及其暫行解決方法。
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## 已知問題
{: #knownissues}

下列各節說明已知問題及可能的解決方法。


### 在建立具有非行動型樣的專案時發生主機名稱採用錯誤
{: #hostname}

如果您使用 {{site.data.keyword.dev_cli_short}} 以從「Web 應用程式」、BFF 或 Microservice 型樣建立專案，則可能會看到下列錯誤：

```
The hostname <myHostname> is taken.
```
{: codeblock}


#### 原因
{: #hostname-cause}
   
此錯誤是由於登入記號過期所造成。


#### 解決方法
{: #hostname-resolution}

請重新登入。

```
bx login
```
{: codeblock}


### {{site.data.keyword.dev_cli_short}} 的一般性失敗
{: #general}

如果您使用 {{site.data.keyword.dev_cli_short}} 來建立、刪除、列出或編寫指令，則可能會看到下列錯誤：

```
Failed to <command> project.
```
{: codeblock}


#### 原因
{: #general-cause}
   
此錯誤是由於登入記號過期所造成。


#### 解決方法
{: #general-resolution}

請重新登入。

```
bx login
```
{: codeblock}


### 新增 {{site.data.keyword.objectstorageshort}} 功能時發生服務分配管理系統錯誤
{: #os}

如果您使用 {{site.data.keyword.dev_cli_short}} 來建立具有 {{site.data.keyword.objectstorageshort}} 功能的兩個專案，則可能會看到下列錯誤：

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}


#### 原因
{: #os-cause}
   
此錯誤是 {{site.data.keyword.objectstorageshort}} 服務只提供一個「免費 {{site.data.keyword.objectstorageshort}}」方案實例所造成。


#### 解決方法
{: #os-resolution}

系統會提示您選擇不同方案來避免此錯誤。


### 在建立專案期間取得程式碼失敗
{: #code}

如果您使用 {{site.data.keyword.dev_cli_short}} 來建立專案，則可能會看到下列錯誤：
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### 原因
{: #code-cause}

此錯誤是由於內部逾時所造成。
	

#### 解決方法
{: #code-resolution}

您可以使用下列一種方式來取得程式碼：

* 使用 CLI 來執行下列指令：

   ```
bx dev code <your-project-name>
	```
   {: codeblock}

   請將 `<your-project-name>` 取代為建立專案期間所指定的專案名稱。

* 使用 {{site.data.keyword.dev_console}}。

	1. 在 {{site.data.keyword.dev_console}} 中選取[專案 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://console.{DomainName}/developer/projects)，然後按一下**取得程式碼**。

	2. 按一下**產生程式碼**。

	3. 產生程式碼之後，請按一下**下載程式碼**。


### 針對 Node.js 專案執行 `bx dev run` 時發生錯誤
{: #node}

如果您是針對 Node.js Web 或 BFF 專案搭配執行 `bx dev run` 與 {{site.data.keyword.dev_cli_short}}，則可能會看到下列錯誤：

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### 原因
{: #node-cause}
   
此錯誤是將 `appmetrics` 模組安裝在不同的架構上所造成。安裝在某個架構上的原生 npm 模組，無法在另一個架構上運作。包括的 Docker 映像檔是以 Linux Kernel 為依據。


#### 解決方法
{: #node-resolution}

刪除 `node_modules` 資料夾，並再次執行 `bx dev run`。


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## 取得協助及支援
{: #gettinghelp}

如果您有 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 或 {{site.data.keyword.dev_cli_notm}} 的問題或疑問，可以搜尋資訊或透過討論區提問來取得協助。您也可以開啟支援問題單。

在討論區提問時，請標記您的問題，讓 {{site.data.keyword.Bluemix_notm}} 開發團隊可以看到它。

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

如果您有使用 {{site.data.keyword.dev_console}} 或 {{site.data.keyword.dev_cli_notm}} 開發或部署應用程式的技術問題，請執行下列動作：

* 將問題張貼在 [Stack Overflow ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix)，並且使用 `bluemix-dev-services` 及 `ibm-bluemix` 來標記您的問題。
* 將問題張貼在 `bluemix-dev-services` 通道中的 [Slack ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://ibm-cloud-tech.slack.com/) 上。請馬上[註冊 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://ibm.biz/IBMCloudNativeSlack)。


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

如需使用討論區的詳細資料，請參閱[取得協助 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/support/index.html#getting-help)。

如需開啟 {{site.data.keyword.IBM}} 支援問題單或是支援層次及問題單嚴重性的相關資訊，請參閱[與支援中心聯絡 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/support/index.html#contacting-support)。

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

