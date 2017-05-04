---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 配置選項
{: #configuration_options}
{: shortdesc}

有各種選項可用於配置 sdk-for-nodejs 建置套件。

## NPM Script
{: #npm_scripts}
NPM 提供 Scripting 機能讓您執行 Script，包括安裝 node_modules 之前及之後所套用的 **preinstall** 及 **postinstall** Script。如需完整詳細資料，請參閱 [npm-scripts ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.npmjs.com/misc/scripts)。

## 快取行為
{: #cache_behavior}
{{site.data.keyword.Bluemix}} 會為每個 node 應用程式維護一個快取目錄，它會在兩次建置之間持續保存。快取會儲存已解析的相依關係，因此不必每次部署應用程式時都進行下載及安裝。例如，假設 myapp 依賴 **express**。然後，第一次部署 myapp 時，即會下載 **express** 模組。後續部署 myapp 時，則會使用 **express** 的快取實例。預設行為是快取 NPM 安裝的所有 node_modules 以及 bower 安裝的 bower_components。

使用 NODE_MODULES_CACHE 變數，以決定 Node 建置套件會使用還是忽略先前建置的快取。預設值為 true。若要停用快取，則將 NODE_MODULES_CACHE 設為 false，例如透過 cf 指令行：

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
