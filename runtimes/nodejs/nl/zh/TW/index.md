---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}

{{site.data.keyword.Bluemix}} 上的 Node.js 運行環境是採用 sdk-for-nodejs 建置套件的技術。
sdk-for-nodejs 建置套件為 Node.js 應用程式提供完整的運行環境。
{: shortdesc}

當應用程式的根目錄包含 **package.json** 檔案時，會使用 sdk-for-nodejs 建置套件。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Node.js 入門範本應用程式。Node.js 入門範本應用程式是簡單的 Node.js 應用程式，提供可以讓您用於應用程式的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 Bluemix 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](/docs/cfapps/starter_app_usage.html)。

## Startup 指令
{: #starup_commmand}

為您的 Bluemix Node.js 應用程式指定 start 指令的建議方式，是使用 **Procfile** 或 **package.json** 檔案。

請使用下列格式在 **Procfile** 中指定 startup 指令。這裡的 app.js 是應用程式的 startup JS Script。

```
web: node app.js
```
{: codeblock}

將 **Procfile** 儲存在應用程式的根目錄中。

如果 **Procfile** 不存在，IBM Bluemix Node.js 建置套件會檢查 **package.json** 檔案中是否有 scripts.start 項目。同樣地，在以下範例中，app.js 是應用程式的 startup JS Script。

```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

如果 **package.json** 中有 start Script 項目存在，則會自動產生 **Procfile**。自動產生的 **Procfile** 內容如下：

```
    web: npm start
```
{: codeblock}

如需 **Procfile** 和 **package.json** 檔案的相關資訊，請參閱 [Node.js 應用程式的提示](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)。

## 在本端執行 Node.js 應用程式的提示
{: #hints}

使用此資訊，以協助在本端和 Bluemix 上執行 Node.js 應用程式。

下列範例顯示 **js** 檔案的部分原始碼：

```
var port = (process.env.PORT || 3000);
```
{: codeblock}

使用此程式碼，當應用程式在 Bluemix 上執行時，PORT 環境變數包含的埠值是 Bluemix 的內部值，應用程式藉此來接聽送入的連線。當應用程式在本端執行時，不會定義 PORT，因此會使用 **3000** 作為埠號。透過此撰寫方式，您可以在本端（若是進行測試）以及在 Bluemix 上執行應用程式，而不必做進一步的變更。

## 離線模式
{: #offline_mode}

請參閱[離線模式](offlineMode.html)，以瞭解如何控制建置套件對外部網站的存取。 

## 應用程式管理
{{site.data.keyword.Bluemix}} 提供若干公用程式來管理 Node.js 應用程式及進行除錯。如需完整的詳細資料，請參閱[應用程式管理](/docs/manageapps/app_mng.html)。

## 可用的版本
{: #available_versions}

{{site.data.keyword.Bluemix}} 提供所有[目前可用的 Node.js 運行環境](http://nodejs.org/dist/)。IBM 在其中一些提供了包含加強功能和錯誤修正程式的版本。如需相關資訊，請參閱 [Node.js 建置套件的最新更新項目](/docs/runtimes/nodejs/updates.html)。

IBM Node.js 建置套件會快取 IBM 運行環境版本。因此，如果您在應用程式中使用 IBM SDK for Node.js 運行環境，當應用程式推送至 Bluemix 時，即可提升應用程式效能。

請在 **package.json** 檔案的 **engines** 區段中使用 **node** 參數，指定您要執行的 Node.js 運行環境版本。

如果您需要指定非 Node.js 組合版本的 npm 版本，請在 **package.json** 檔案的 **engines** 區段中使用 **npm** 參數。  

請參閱下列範例：

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

node 版本應該一律指定在 **package.json** 檔案中。如果未指定，將使用最新的 node 版本。

## 配置選項
{: #configuration_options}

### NPM Script
{: #npm_scripts}
NPM 提供 Scripting 機能讓您執行 Script，包括安裝 node_modules 之前及之後所套用的 **preinstall** 及 **postinstall** Script。如需完整詳細資料，請參閱 [npm-scripts](https://docs.npmjs.com/misc/scripts)。

### 快取行為
{: #cache_behavior}
{{site.data.keyword.Bluemix}} 會為每個 node 應用程式維護一個快取目錄，它會在兩次建置之間持續保存。快取會儲存已解析的相依關係，因此不必每次部署應用程式時都進行下載及安裝。例如，假設 myapp 依賴 **express**。然後，第一次部署 myapp 時，即會下載 **express** 模組。後續部署 myapp 時，則會使用 **express** 的快取實例。預設行為是快取 NPM 安裝的所有 node_modules 以及 bower 安裝的 bower_components。

使用 NODE_MODULES_CACHE 變數，以決定 Node 建置套件會使用還是忽略先前建置的快取。預設值是 true。若要停用快取，則將 NODE_MODULES_CACHE 設為 false，例如透過 cf 指令行：

```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

請注意，不會快取應用程式中所包含的 node_modules。

您可以在最上層 **package.json** 中使用 **cacheDirectories** 陣列，來達到要快取哪些模組的精細控制。當 **cacheDirectories** 元素出現在 **package.json** 中時，只會快取位於 **cacheDirectories** 陣列中的那些模組。在下列範例中，只會快取 node_modules 和 bower_components。

```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### FIPS 模式
{: #fips_mode}

Nodejs 建置套件 v3.2-20160315-1257 版以及更新版本支援 [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards)。若要使用已啟用 FIPS 功能的 node 引擎，請將環境變數 FIPS_MODE 設為 true。
例如：

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

請務必瞭解，當 FIPS_MODE 為 true 時，部分 node 模組可能會無法運作。例如，**使用 [MD5](https://en.wikipedia.org/wiki/MD5) 的 node 模組將會失敗**（例如 [Express](http://expressjs.com/)）。對於 Express，在 Expess 應用程式中將 [etag](http://expressjs.com/en/api.html) 設為 false 可能有助於暫時解決此問題。例如，您可以在程式碼中執行下列動作：

```
    app.set('etag', false);
```
{: codeblock}
如需相關資訊，請參閱這則 [Stack Overflow 貼文](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)。**附註**：*未* 同時支援[應用程式管理](/docs/manageapps/app_mng.html)及 FIPS_MODE。如果設定 BLUEMIX_APP_MGMT_ENABLE 環境變數，而且 FIPS_MODE 環境變數設為 true，將無法編譯打包應用程式。

有各種方法可檢查 FIPS_MODE 的狀態：
<ul>
<li> 您可以檢查應用程式的 staging_task.log 中是否有與下列類似的訊息：    

  <pre>
  正在從快取中安裝已啟用 FIPS 功能的 IBM SDK for Node.js (4.4.3)
  </pre>
  {: codeblock}

這則訊息指出已啟用 FIPS 功能的 node.js 引擎正在執行中，但 FIPS 不一定要正在執行
</li>

<li> 您可以檢查 **process.versions.openssl** 的值。例如：

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

如果 SSL 版本包含 "fips"，則使用中的 SSL 版本支援 FIPS。  
</li>

<li> 若為 node.js 第 6 版及更高版本，您可以在與下面類似的程式碼中檢查 crypto.fips 所傳回的值：

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

如果傳回的值是 1，則表示正在使用 FIPS。請注意，若為第 6 版之前的 node.js 版本，crypto.fips 將傳回*未定義*。
</li>
</ul>

#### Nodejs 第 4 版
{: #nodejs_v4_fips}

下表說明 node.js 第 4 版在使用 FIPS 時的行為：

|                 | 結果          |
| :-------------- | :------------ |
|FIPS_MODE=true   |成功 (1)    |
|FIPS_MODE !=true |成功 (2)    |

* 成功 (1)
  * FIPS 正在使用中。
  * staging_task.log 將包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值將包含 "fips"。
* 成功 (2)
  * FIPS 目前*不* 在使用中。
  * staging_task.log *不* 會包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值*不* 會包含 "fips"。

#### Nodejs 第 6 版
{: #nodejs_v6_fips}

若要以 FIPS 模式與 Node.js 第 6 版搭配執行，則除了設定 **FIPS_MODE=true** 之外，您還必須在 start 指令中包括 **--enable-fips**，如下列範例中所示：
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

下表說明 node.js 第 6 版在使用 FIPS 時的行為。

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |成功 (1)    |成功 (2)      |
|FIPS_MODE !=true |失敗 (3)    |成功 (4)      |

* 成功 (1)
  * FIPS 正在使用中。
  * staging_task.log 將包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值將包含 "fips"。
  * crypto.fips 將傳回 1，指出 FIPS 正在使用中。
* 成功 (2)
  * FIPS 目前*不* 在使用中。
  * staging_task.log 將包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值將包含 "fips"。
  * crypto.fips 將傳回 0，指出 FIPS 目前*不* 在使用中。
* 失敗 (3)
  * FIPS 目前*不* 在使用中。
  * staging_task.log *不* 會包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * 編譯打包將會失敗，訊息為「ERR node：選項錯誤：--enable-fips」。
* 成功 (4)
  * FIPS 目前*不* 在使用中。
  * staging_task.log *不* 會包括*正在安裝已啟用 FIPS 功能的 IBM SDK for Node.js* 訊息。
  * process.versions.openssl 所傳回的值*不* 會包含 "fips"。
  * crypto.fips 將傳回 0，指出 FIPS 目前*不* 在使用中。


## Node.js 建置套件

Bluemix 提供多個版本的 Node.js 建置套件。
* IBM 建立的 **sdk-for-nodejs** 建置套件是用於 Bluemix 中之 Node.js 應用程式的預設建置套件。
* **nodejs_buildpack** 是 Cloud Foundry 社群所提供的社群建置套件。

在 Bluemix 中，**sdk-for-nodejs** 建置套件的優先順序高於 **nodejs_buildpack**。如果您想要對應用程式使用 **nodejs_buildpack** 而非 **sdk-for-nodejs** 建置套件，您必須指定您的建置套件，例如，使用 -b 選項來搭配 **cf push** 指令。

一般而言，可以使用現行 **sdk-for-nodejs** 建置套件和前一版的版本。若要查看所有可用的建置套件，請使用 **cf buildpacks** 指令。例如：
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                                 position   enabled   locked   filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip</pre>
{: codeblock}

# 相關鏈結
{: #rellinks}
## 一般
{: #general}
* [Node.js 建置套件的最新更新項目](/docs/runtimes/nodejs/updates.html)
* [應用程式管理](/docs/manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
