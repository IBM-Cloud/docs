---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# node.js 的離線模式
{: #offline_mode}

將 node.js 應用程式推送至 {{site.data.keyword.Bluemix}} 之後，SDK for Node.js 建置套件通常會從外部資源下載構件，例如 NPM 提供的 node 模組。在某些情況下，例如使用 [Bluemix 專用](/docs/dedicated/index.html#dedicated)和 [Bluemix 本端](/docs/local/index.html#local)時，您可能會希望不要依賴存取 Bluemix 的外部網站，或是希望對這些外部網站有更明確的控制。  
{: shortdesc}

下列是 node.js 建置套件可以存取的外部網站。在 [Bluemix 專用](/docs/dedicated/index.html#dedicated)和 [Bluemix 本端](/docs/local/index.html#local)環境中，需要將這些網站設定為*白名單*。

* http://nodejs.org/ 可用來確定可用的 node 引擎版本。
* https://s3pository.heroku.com 可用來擷取建置套件中沒有包含的 node 引擎版本。
*  https://www.npmjs.com/package/npm 和 https://semver.herokuapp.com 可用來擷取建置套件中沒有包含的 npm 版本。
* https://iojs.org 可用來擷取建置套件中沒有包含，或是 https://semver.herokuapp.com 沒有提供的舊版 node。
* https://registry.npmjs.org 可用來擷取 Express 之類的 node 模組。

若要盡量精簡白名單網站集，請將您的 node 應用程式配置為使用 SDK 中適用於 Node.js 建置套件的 node 引擎版本。請參閱[最新更新項目](./updates.html)，以取得建置套件中包含的 node 引擎版本。如果這麼做，則只需要 https://registry.npmjs.org 網站來下載 node 模組。

請注意，安裝新版本的 SDK for Node.js 建置套件之後，可用的 node 引擎版本集通常就會移至較新的版本。這樣可能會需要您重新配置 node 應用程式，以指定較新的 node 引擎版本。


## 離線應用程式
{: #offline_applications}

若不想要存取 `https://registry.npmjs.org`，您可以將應用程式需要的所有 node 模組包含在您的應用程式中。若要這麼做，請針對應用程式需要的所有模組執行 **npm install**，並將所產生的 *node_modules* 目錄包含在您推送的應用程式中。

請注意，您的相依關係可以有相依關係，然後這些相依關係還可以再有相依關係，一直延續下去，但是 package.json
只包含最上層相依關係。如果其中一個相依關係使用 package.json 中的範圍，而該檔案有發行新的版本，則 node_modules 目錄中的模組就會作廢。*Shrinkwrap* 可協助您鎖定所有相依關係版本，所以不會發生這種情形。若要使用 shrinkwrap，請從空的或乾淨的 node_modules 目錄開始進行，然後在專案的根目錄中執行：
0. npm install
1. npm dedupe
2. npm shrinkwrap

這樣可能會變更您的 *package.json*，並且在您的根目錄中新增 *npm-shrinkwrap.json*。每當您變更 *package.json* 檔案中的相依關係，就要重複 *dedupe* 和 *shringwrap* 步驟。

## 使用 Proxy
{: #working_with_proxy}

在像 [Bluemix 專用](/docs/dedicated/index.html#dedicated)和 [Bluemix 本端](/docs/local/index.html#local)這些環境中，可以配置 Proxy。如需詳細資訊，請參閱[使用 Proxy](/docs/manageapps/workingWithProxy.html)。
