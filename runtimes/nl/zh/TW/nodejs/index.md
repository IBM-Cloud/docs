---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}
*前次更新：2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} 上的 Node.js 執行時期是採用 sdk-for-nodejs 建置套件的技術。
sdk-for-nodejs 建置套件為 Node.js 應用程式提供完整的執行時期環境。
{: shortdesc}

當應用程式的根目錄包含 **package.json** 檔案時，會使用 sdk-for-nodejs 建置套件。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Node.js 入門範本應用程式。Node.js 入門範本應用程式是簡單的 Node.js 應用程式，它提供一個可以讓您用於應用程式的範本。您可以實驗入門範本應用程式，並進行及推送對 Bluemix 環境的變更。使用入門範本應用程式時如需協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## Startup 指令
{: #starup_commmand}

為您的 Bluemix Node.js 應用程式指定 start 指令的建議方式，是使用 **Procfile** 或 **package.json** 檔案。

請使用下列格式指定 **Procfile** 中的 startup 指令。這裡的 app.js 是應用程式的 startup js Script。
```
web: node app.js
```
{: codeblock}

將 **Procfile** 儲存在應用程式的根目錄中。

如果 **Procfile** 不存在，IBM Bluemix Node.js 建置套件會檢查 **package.json** 檔案中是否有 scripts.start 項目。同樣地，在以下範例中，app.js 是應用程式的 startup js Script。
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

下列範例顯示 **js** 檔案的原始碼的一部分：
```
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

透過此程式碼，當應用程式在 Bluemix 上執行時，VCAP_APP_HOST 及 VCAP_APP_PORT 環境變數包含的主機和埠值是 Bluemix 的內部值，應用程式即藉此來接聽送入的連線。當應用程式在本端執行時，並未定義 VCAP_APP_HOST 及 VCAP_APP_PORT，因此會使用 **localhost** 作為主機並使用 **3000** 作為埠號。透過此編寫方式，您可以在本端執行應用程式來進行測試，並且在 Bluemix 上執行而不必做進一步的變更。

## 應用程式管理
{{site.data.keyword.Bluemix}} 提供若干公用程式來管理 Node.js 應用程式及進行除錯。如需完整的詳細資料，請參閱[應用程式管理](../../manageapps/app_mng.html)。

## 可用的版本
{: #available_versions}

{{site.data.keyword.Bluemix}} 提供所有[目前可用的 Node.js 執行時期](http://nodejs.org/dist/)。IBM 在其中一些提供了包含加強功能和錯誤修正程式的版本。如需相關資訊，請參閱 [Node.js 建置套件的最新更新項目](../../runtimes/nodejs/updates.html)。

IBM Node.js 建置套件會快取所有 IBM 執行時期版本。因此，如果您在應用程式中使用 IBM SDK for Node.js 執行時期，當應用程式推送至 Bluemix 時，您會有更快的應用程式效能。

請在 **package.json** 檔案的 **engines** 區段中使用 **node** 參數，指定您要執行的 Node.js 執行時期的版本。

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

節點版本應該一律指定在 **package.json** 檔案中。如果未指定，將使用最新的節點版本。

## 配置選項
{: #configuration_options}

### NPM Script
{: #npm_scripts}
NPM 提供 Scripting 功能讓您執行 Script，包括安裝 node_modules 之前及之後所套用的 **preinstall** 及 **postinstall** Script。如需完整詳細資料，請參閱 [npm-scripts](https://docs.npmjs.com/misc/scripts)。

### 快取行為
{: #cache_behavior}
{{site.data.keyword.Bluemix}} 為每個節點應用程式維護一個快取目錄，它會在兩次建置之間持續保存。快取會儲存已解析的相依關係，因此每次部署應用程式時不會下載及安裝它們。例如，假設 myapp 相依於 **express**。那麼，第一次部署 myapp 時，會下載 **expess** 模組。在 myapp 的後續部署上，則會使用 **express** 的快取實例。預設行為是快取 NPM 安裝的所有 node_modules 以及 bower 安裝的 bower_components。

使用 NODE_MODULES_CACHE 變數，以決定 Node 建置套件會使用還是忽略先前建置中的快取。預設值是 true。若要停用快取，則將 NODE_MODULES_CACHE 設為 false，例如透過 cf 指令行：
```
cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

請注意，不會快取應用程式中所包含的 node_modules。

您可以使用最上層 **package.json** 中的 **cacheDirectories** 陣列，來達到要快取哪些模組的精細控制。當 **cacheDirectories** 元素出現在 **package.json** 中時，只會快取位於 **cacheDirectories** 陣列中的那些模組。在下列範例中，只會快取 node_modules 和 bower_components。
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

## Node.js 建置套件

Bluemix 提供 Node.js 建置套件的多個版本。
* IBM 建立的 **sdk-for-nodejs** 建置套件是用於 Bluemix 中的 Node.js 應用程式的預設建置套件。
* **nodejs_buildpack** 是 Cloud Foundry 社群所提供的外部建置套件。

在 Bluemix 中，**sdk-for-nodejs** 建置套件的優先順序高於 **nodejs_buildpack**。如果您想要對應用程式使用 **nodejs_buildpack** 而非 **sdk-for-nodejs** 建置套件，您必須指定您的建置套件，例如，使用 -b 選項來搭配 **cf push** 指令。

一般而言，現行 **sdk-for-nodejs** 建置套件和前一版的版本可供使用。若要查看所有可用的建置套件，請使用 **cf buildpacks** 指令。例如：
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                                 position   enabled   locked   filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
</pre>
{: codeblock}

# 相關鏈結
## 一般
* [Node.js 建置套件的最新更新項目](../../runtimes/nodejs/updates.html)
* [應用程式管理](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
