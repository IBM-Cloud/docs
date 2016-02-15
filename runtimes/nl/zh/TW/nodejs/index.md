{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*前次更新：2016 年 1 月 12 日*

# Node.js 執行時期
{: #nodejs_runtime}

{{site.data.keyword.Bluemix}} 上的 Node.js 執行時期是採用 sdk-for-nodejs 建置套件的技術。
sdk-for-nodejs 建置套件為 Node.js 應用程式提供完整的執行時期環境。
{: shortdesc}

Node.js 建置套件用於應用程式在根目錄中包含 **package.json** 檔案時。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供一個 Node.js 入門範本應用程式。Node.js 入門範本應用程式是簡單的 Node.js 應用程式，您可以將它提供的範本用於您的應用程式。您可以用入門範本應用程式進行實驗，然後進行變更並推送到 Bluemix 環境。請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)，以取得使用入門範本應用程式的協助。

## Startup 指令
{: #starup_commmand}

為您的 Bluemix Node.js 應用程式指定啟動指令的建議方式，是使用 **Procfile** 或 **package.json** 檔。

請用以下格式在您的 **Procfile** 中指定啟動指令。在這裡，app.js 是應用程式的啟動 js Script。
```
web: node app.js
```
{: codeblock}

將 **Procfile** 儲存在應用程式的根目錄中。

如果 **Procfile** 不存在，IBM Bluemix Node.js 建置套件會檢查 **package.json** 檔案中的 scripts.start 項目。同樣地，在以下範例中，app.js 是應用程式的啟動 js Script。
```
{
  ...   
"scripts": {

    "start": "node app.js"
}
}
```
{: codeblock}

如果 **package.json** 中有啟動 Script 項目存在，則會自動產生 **Procfile**。自動產生的 **Procfile** 的內容如下：
```
web: npm start
```
{: codeblock}

如需 **Procfile** 及 **package.json** 檔案的相關資訊，請參閱 [Tips for Node.js Applications](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)。

## 在本端執行 Node.js 應用程式的提示
{: #hints}

請使用此資訊來協助在本端及在 Bluemix 上執行 Node.js 應用程式。

下列範例顯示 **js** 檔案的來源的一部分：
```
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

使用此程式碼，在 Bluemix 上執行應用程式時，VCAP_APP_HOST 及 VCAP_APP_PORT 環境變數會包含對 Bluemix 而言在內部，且應用程式接聽送入連線的主機及埠值。應用程式在本端執行時，不會定義 VCAP_APP_HOST 及 VCAP_APP_PORT，因此使用 **localhost** 作為主機，並使用 **3000** 作為埠號。以這種方式撰寫，您可以在本端執行應用程式來進行測試，以及在 Bluemix 上執行應用程式，而不需進行進一步變更。

## 應用程式管理
{{site.data.keyword.Bluemix}} 提供許多公用程式來管理 Node.js 應用程式及進行除錯。如需完整詳細資料，請參閱[應用程式管理](../../manageapps/app_mng.html)。

## 可用的版本
{: #available_versions}

{{site.data.keyword.Bluemix}} 提供所有[目前可用的 Node.js 執行時期](http://nodejs.org/dist/)。在其中，IBM 提供包含加強功能及錯誤修正程式的版本。如需相關資訊，請參閱 [Node.js 建置套件的最新更新項目](updates.html)。

IBM Node.js 建置套件會快取所有 IBM 執行時期版本。因此，如果您在應用程式中使用 IBM SDK for Node.js 執行時期，則將應用程式推送至 Bluemix 時會有更快速的應用程式效能。

使用 **package.json** 檔案中的 **engines** 區段的 **node** 參數，以指定要執行的 Node.js 執行時期版本。

如果需要指定非 Node.js 所搭配版本的 npm 版本，請使用 **package.json** 檔案中的 **engines** 區段的 **npm** 參數。  

請參閱下列範例：

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4"
     "npm": "2.11.3"
  }
}
```
{: codeblock}

您應該一律在 **package.json** 檔案中指定 node 版本。如果未指定，則會使用最新的 node 版本。

## 配置選項
{: #configuration_options}

### NPM Script
{: #npm_scripts}
NPM 提供 Scripting 機能，允許您執行 Script，包括 **preinstall** 和 **postinstall** Script，它們會在 node_modules 安裝之前和之後套用。如需完整詳細資料，請參閱 [npm-scripts](https://docs.npmjs.com/misc/scripts)。

### 快取操作方式
{: #cache_behavior}
{{site.data.keyword.Bluemix}} 為每個 node 應用程式維護一個快取目錄，它會在建置之間持續保存。快取會儲存已解析的相依關係，因此不會在每次部署應用程式時都下載並安裝。例如，假設 myapp 依賴 **express**。那麼第一次部署 myapp 時，會下載 **expess** 模組。在後續部署 myapp 時，會使用 **express** 的快取實例。

請使用 NODE_MODULES_CACHE 變數來判斷 Node 建置套件會使用還是忽略先前建置的快取。預設值是 true。若要停用快取，請將 NODE_MODULES_CACHE 設為 false，例如透過 cf 指令行：
```
cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

請注意，不會快取您應用程式所包含的 node_modules。

您可以在最上層 **package.json** 使用 **cacheDirectories** 陣列，以達到對於快取哪些模組的精細控制。**package.json** 中有 **cacheDirectories** 元素存在時，只會快取位於 **cacheDirectories** 陣列中的模組。在下列範例中，只會快取 node_modules 和 bower_components。
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

## Node.js 建置套件

Bluemix 提供多個版本的 Node.js 建置套件。
* IBM 所建立的 **sdk-for-nodejs** 建置套件，是用於 Bluemix 中 Node.js 應用程式的預設建置套件。
* **nodejs_buildpack** 是 Cloud Foundry 社群所提供的外部建置套件。

在 Bluemix 中，**sdk-for-nodejs** 建置套件的優先順序高於 **nodejs_buildpack**。如果您要使用 **nodejs_buildpack** 與應用程式搭配，而非 **sdk-for-nodejs** 建置套件，則必須使用 -b 選項與 **cf push** 指令搭配來指定建置套件。

一般而言，會提供現行 **sdk-for-nodejs** 建置套件和前一版本。若要查看所有可用的建置套件，請使用 **cf buildpacks** 指令。例如：
```
cf buildpacks
Getting buildpacks...

buildpack                      position          enabled          locked          filename	
   
...
sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}


## 相關鏈結
{: #related_links}
* [Node.js 建置套件的最新更新項目](updates.html)
* [應用程式管理](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
