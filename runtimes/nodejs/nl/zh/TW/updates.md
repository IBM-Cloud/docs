{:new_window: target="_blank"}
{:codeblock: .codeblock}

*前次更新：2016 年 1 月 18 日*

# Node.js 建置套件的最新更新項目
{: #latest_updates}

Node.js 建置套件中的最新更新項目清單。

## 2015 年 12 月 16 日：已更新 Node.js 建置套件 v2.8-20151209-1403 及 v3.0beta-20151211-2041

這版的 Node.js 建置套件隨附兩個版本：2.8 版及 3.0beta 版。這兩個版本都包括下列變更：

Monitoring and Analytics 服務的錯誤修正程式
包含 IBM SDK for Node.js 4.2.3.0 版、4.2.2.0 版、1.2.0.8 版及 1.2.0.7 版的已快取執行時期（分別根據社群 Node.js 4.2.3 版、4.2.2 版、0.12.9 版及 0.12.8 版）
此外，在 3.0beta 版中，預設的 Node.js 執行時期變更為 4.2.3 版。

在 Node.js 4.2.3 版為預設執行時期的 Bluemix 上，IBM Node.js Buildpack 3.0beta 版已發行為非預設建置套件。若要確定您的應用程式及服務將繼續在 Bluemix 上運作，請使用測試版的建置套件來推送應用程式。在 30 天或更長的時間之後，會將第 3 版設為預設建置套件。

若要使用 3.0beta 版來推送您的應用程式，請執行下列動作：
* 在 'cf push' 指令中使用 "-b" 選項：
```
 cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}
* 或者，在 manifest.yml 檔案中使用 "buildpack" 選項：
```
buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

如果您已在應用程式的 package.json 中配置特定版本的 Node.js，則預設執行時期的這項變更不會影響您的應用程式。請注意，在 package.json 中使用 engines.node 項目，一律可以指定 Node.js 版本來執行應用程式（如[可用的版本](index.html#available_versions)中所述）。

## 2015 年 11 月 23 日：已更新 Node.js 建置套件 2.7-20151118-1003 版

在 2.7 中，我們包括 4.2.1.0 版的 IBM SDK for Node.js（根據 Node 4.2.1 版 LTS）。
它還不是預設值，但是可以指定以供使用。請注意，這會取代先前可用的開放程式碼建置。我們也已對服務延伸架構進行一些較小的錯誤修正程式。

## 2015 年 10 月 19 日：已更新 Node.js 建置套件 v2.6.1-20151015-1326

Node.js 2.6.1 版引進 [StrongPM 應用程式管理處理程式](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)的錯誤修正程式，以及更一致的 NPM 版本。

## 2015 年 10 月 15 日：已更新 Node.js 建置套件 v2.6-20151006-1309

本版的 Node.js 建置套件特色為將 [StrongLoop Process Manager](https://strong-pm.io)
整合到「應用程式管理」特性。如需相關資訊，請參閱部落格文章 [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)。

## 2015 年 6 月 15 日：已更新 Node.js 建置套件 v2.0-20150608-1503

在本版中，我們的 Node.js 建置套件已和最新 [CF 社群
Node.js 建置套件](https://github.com/cloudfoundry/nodejs-buildpack)同步化，後者具有許多來自社群的新特性。此外，我們也改良了 Node.js 建置套件中的「應用程式管理」特性，它能夠啟用例如 shell、node-inspector、Bluemix Live Sync 等，以及更多其他公用程式。如需詳細資料，請參閱[應用程式管理](../../manageapps/app_mng.html)。

## 2015 年 5 月 5 日：已更新 Node.js 建置套件 v1.17-20150429-1033

* Node.js 建置套件現在伴隨 [IBM SDK for Node.js 0.12.1 版](https://developer.ibm.com/node/sdk/)。
* 如果您的應用程式未在其 package.json 檔中指定執行時期，則現在會使用 0.12.1 版啟動您的應用程式，而不使用 0.10.x 版。如果您需要使用舊版，請在 package.json 指定 0.10.x 版，如下所示：
```
   "engines": {
"node": "0.10.x"
}
```
{: codeblock}
* 0.12.1 版有已知的問題：
   * 使用 Bluemix Live Sync 提供的「除錯工具」特性時，「暫停」特性會岔斷。
   * 在 0.12.x 版上不支援用於 MQ Light 服務的 mqlight 模組

* 解決了各種安全漏洞：
  * 已修正 OpenSSL 中會影響 IBM SDK for Node.js 的漏洞。詳細資料提供於[安全性公告](http://www-01.ibm.com/support/docview.wss?uid=swg21701494)。
  * 已修正 RC4 Stream Cipher 中會影響 IBM SDK for Node.js 的漏洞。詳細資料提供於[安全性公告](http://www-01.ibm.com/support/docview.wss?uid=swg21882778)。

##  2015 年 4 月 2 日：已更新 Node.js 建置套件 v1.15-20150331-2231

* Node.js 建置套件現在包含三個新增特性，可以協助快速在 Bluemix 上和桌面一樣地進行開發，而不必重新部署
  * 桌面同步：將任何 (Windows) 桌面樹狀結構同步化到雲端型專案工作區
  * 即時編輯：您可以變更在 Bluemix 中執行的 Node.js 應用程式，並立刻在瀏覽器中測試它們。
  * 除錯：開啟 Shell 進入您的環境並進行除錯！您可以使用 Node Inspector 除錯器動態編輯程式碼、插入岔斷點、逐步執行程式碼、重新啟動執行時期，以及執行更多功能
  * 如需相關資訊，請參閱[應用程式管理](../../manageapps/app_mng.html#Utilities)。
* 我們已經加入來自 [Cloud Foundry 的 Node.js 建置套件](https://github.com/cloudfoundry/nodejs-buildpack)的最新變更。這伴隨由社群所做的許多錯誤修正程式和改良功能。
* Node.js 建置套件現在伴隨 [IBM SDK for Node.js 1.1.0.13 版](https://developer.ibm.com/node/sdk/)。

## 2015 年 1 月 5 日：已更新 Node.js 建置套件 v1.9.1-20141208-1221

* Node.js 建置套件現在包含動態日誌設定支援。使用此功能，開發人員可以即時變更應用程式的記載層次，如果應用程式使用 log4js、bunyan 或 ibmbluemix 模組來記載的話。
* Node.js 建置套件現在伴隨 [IBM SDK for Node.js 0.10.33 版](https://developer.ibm.com/node/sdk/)。這包括 POODLE 問題的修正程式。

## 2014 年 10 月 23 日：已更新 Node.js 建置套件 v1.6-20141013-1736

* Node.js 建置套件現在伴隨 [IBM SDK for Node.js 1.1.0.8 版](https://developer.ibm.com/node/sdk/)。這表示您將在指定應用程式的最新穩定 Node.js 執行時期 0.10.32 版時，取得完整支援的 IBM Node.js 執行時期。這個最新 SDK 伴隨內嵌 qs 模組的問題修正程式，此問題導致拒絕服務。它也包含更新版本的 npm 模組和 http 與 url 模組的其他改進功能。如需其他詳細資料，請參閱 [0.10.32 版變更日誌](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog)。
* 建置套件也包含錯誤的修正程式，該錯誤會在部署期間，在客戶的應用程式中新增不正確的 index.html 檔。

## 2014 年 9 月 30 日：已更新 Node.js 建置套件 v1.4-20140908-1746

* Node.js 建置套件現在伴隨 [IBM SDK for Node.js 1.1.0.7 版](https://developer.ibm.com/node/sdk/)。這表示您將在指定應用程式的最新穩定 Node.js 執行時期 0.10.31 版時，取得完整支援的 IBM Node.js 執行時期。使用完整支援的 Node.js 執行時期，客戶可以用它作為基礎進行建置，並且知道他們可以依賴和 IBM 產品一貫具備的深度支援。
* 建置套件包含改良的服務架構。明確地說，它在連結 Monitoring and Analytics 服務時運作較佳，且在發生失敗時提供額外的診斷資訊。

## 2014 年 8 月 28 日：已更新 Node.js 建置套件 v1.3-20140821-1143

* 最新的 Node.js 建置套件現在伴隨 IBM SDK for Node.js 1.1.0.6 版。這表示您將在指定應用程式的最新穩定 Node.js 執行時期 0.10.30 版時，取得完整支援的 IBM Node.js 執行時期。此執行時期修正[第 8 版記憶體毀損漏洞](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow)。
* 建置套件也包括 Monitoring and Analytics 服務延伸的增進功能及錯誤修正，讓您可以透過服務來診斷效能及錯誤狀況。

## 2014 年 7 月 29 日：已更新 Node.js 建置套件 v1.1-20140717-1447

Node.js 建置套件現在伴隨 IBM SDK for Node.js 1.1.0.5 版。這表示您將在指定應用程式的最新穩定 Node.js 執行時期 0.10.29 版時，取得完整支援的 IBM Node.js 執行時期。請參閱[這裡](https://developer.ibm.com/node/sdk/)以取得 IBM Node.js SDK 的相關資訊。
