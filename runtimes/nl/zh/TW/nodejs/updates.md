---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# sdk-for-nodejs 建置套件的最新更新項目
{: #latest_updates}

*前次更新：2016 年 3 月 22 日*

sdk-for-nodejs 建置套件中的最新更新項目清單。
## 2016 年 4 月 29 日：已更新 Node.js 建置套件 v3.3-20160418-1749

這個版本的建置套件新增了 IBM SDK for Node.js 執行時期 0.10.44、0.12.13、4.4.1 及 4.4.2 版。預設值現在是 4.4.2。同時也移除了移除較舊的 IBM SDK for Node.js 執行時期版本。建置套件現在只包含最新的兩個版本 0.10.x、0.12.x，以及 4.x（目前為 0.10.43、0.10.44、0.12.12、0.12.13、4.4.1 及 4.4.2）。

針對 4.4.1 及 4.4.2，現在可以藉由為應用程式設定 `FIPS_MODE=true` 環境變數，使用與 FIPS 相容的執行時期版本。然後在編譯打包輸出中尋找 `FIPS_MODE`，以確認建置套件能辨識它。

更新的建置套件和新執行時期也包含下列安全漏洞的修正程式：
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

更新的建置套件也包含兩項錯誤的修正程式：
* 現在如果有符合所要求範圍的 IBM SDK for Node.js 建置可用，將一律使用 IBM SDK for Node.js 建置。先前只有針對 4.x 執行時期版本才是這種情況。
* 現在應用程式管理 inspector 檢查程式能與 4.x 執行時期版本搭配運作。

## 2016 年 3 月 18 日：已更新 Node.js 建置套件 v3.2-20160315-1257

這個版本的建置套件將預設 IBM SDK for Node.js 執行時期從 4.3.0 版移至 4.3.2 版。它也包括 IBM SDK for Node.js 0.10.43 版、0.12.12 版及 4.3.1 版。使用者應該使用這些最新的 Node.js 版本來取得數個安全漏洞的修正程式。

## 2016 年 3 月 4 日：已更新 Node.js 建置套件 v3.1-20160222-1123

這個版本的建置套件將預設 IBM SDK for Node.js 執行時期從 4.2.4 版移至 4.3.0 版。它也包括 IBM SDK for Node.js 0.10.42 版、0.12.10 版及 4.2.6 版。使用者應該使用這些最新的 Node.js 版本來取得數個安全漏洞的修正程式。

## 2016 年 2 月 4 日：已更新 Node.js 建置套件 v3.0-20160125-1224

此版本與 [Cloud Foundry 社群 Node.js](https://github.com/cloudfoundry/nodejs-buildpack) 建置套件完全同步。除了社群變更之外，特定預設值也有變更，並已最佳化來減少編譯打包時間，還有更新「應用程式管理」特性。

* 建置套件更新項目：

  * Node.js 4.2.4 版（IBM SDK for Node.js 第 4 版）現在是 Bluemix 上的預設執行時期，取代 0.12.9 版。如果您尚未針對應用程式指定特定版本，這可能造成您的應用程式會有不同的行為。若要瞭解如何指定 Bluemix 應用程式的 Node.js 版本，請參閱 [Node.js 執行時期](index.html)文件。

  * 依預設，NODE_ENV 現在是設為 *production*。這使得某些 node 相依關係會有不同的行為。例如，Express 架構將不再於 Web 瀏覽器中傳回失敗端點的堆疊追蹤，而只會顯示*內部伺服器錯誤*。當 NPM_CONFIG_PRODUCTION 設為 *true* 時，NPM 會將 NODE_ENV 設為 *production*，而這僅針對 npm 安裝階段中的子 Shell Script。這可讓使用者將應用程式執行時期的 NODE_ENV 設為其他值，例如 *development*。為了清楚說明，npm Script 會看到此訊息：**NODE_ENV=production**。

  * 已包括 Monitoring and Analytics 服務的錯誤修正程式。

* 快取更新項目：

  * 如果已停用快取 (NODE_MODULES_CACHE=false)，建置套件將不會嘗試快取任何模組/元件。先前此設定使得快取不會被取出，但它仍然會快取已安裝的模組供未來部署使用。現在，它既不會取出快取，也不會嘗試儲存任何快取。

  * 除了 node_modules 之外，依預設，還會快取 bower_components。

* 其他更新項目：

  * 針對遺漏相依關係如 gulp、bower 及 angular，已新增有用的警告。

  * 已使用建置套件版本資訊更新了 detect Script。

  * 已移除社群一開始產生的叢集建議 (WEB_CONCURRENCY)，因為在 Bluemix 上的記憶體判定不正確。


## 2015 年 12 月 16 日：已更新 Node.js 建置套件 v2.8-20151209-1403 和 v3.0beta-20151211-2041

這個版本的 Node.js 建置套件有兩個版本：2.8 版和 3.0 測試版。這兩個版本都包括下列變更：

Monitoring and Analytics 服務的錯誤修正程式
包含了 IBM SDK for Node.js 4.2.3.0 版、4.2.2.0 版、1.2.0.8 版及 1.2.0.7 版（分別根據社群 Node.js 4.2.3 版、4.2.2 版、0.12.9 版及 0.12.8 版）的快取執行時期
此外，在 3.0 測試版中，預設 Node.js 執行時期已變更為 4.2.3 版。

在 Bluemix 上，IBM Node.js 建置套件 3.0 測試版已發行為非預設建置套件，並以 Node.js 4.2.3 版作為預設執行時期。為確保應用程式和服務能夠在 Bluemix 上繼續運作，請以建置套件的測試版來推送應用程式。經過至少 30 天以後，第 3 版將成為預設建置套件。

若要以 3.0 測試版來推送應用程式，請執行下列動作：
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

如果您已在應用程式的 package.json 中配置特定版本的 Node.js，則預設執行時期的這項變更不會影響您的應用程式。請注意，您隨時都可以在 package.json 中使用 engines.node 項目，指定用來執行應用程式的 Node.js 版本，如[可用的版本](index.html#available_versions)中所述。

## 2015 年 11 月 23 日：已更新 Node.js 建置套件 v2.7-20151118-1003

在 2.7 中，我們包括了 IBM SDK for Node.js 4.2.1.0 版（根據 Node 4.2.1 版 LTS）。它還不是預設值，但是可以指定以供使用。請注意，這會取代先前可用的開放程式碼建置。我們也對服務延伸架構進行了一些較小的錯誤修正。

## 2015 年 10 月 19 日：已更新 Node.js 建置套件 v2.6.1-20151015-1326

Node.js 2.6.1 版引進了 [StrongPM 應用程式管理處理程式](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)的錯誤修正程式，以及更一致的 NPM 版本。

## 2015 年 10 月 15 日：已更新 Node.js 建置套件 v2.6-20151006-1309

這個版本的 Node.js 建置套件，其特性就是將 [StrongLoop Process Manager](https://strong-pm.io) 整合到「應用程式管理」特性。如需相關資訊，請參閱部落格文章 [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)。

## 2015 年 6 月 15 日：已更新 Node.js 建置套件 v2.0-20150608-1503

在這個版本中，我們的 Node.js 建置套件已與最新 [CF 社群 Node.js 建置套件](https://github.com/cloudfoundry/nodejs-buildpack)同步化，後者具有許多來自社群的新特性。
此外，我們也改良了 Node.js 建置套件中的「應用程式管理」特性，它能夠啟用如 Shell、node-inspector、Bluemix Live Sync 等公用程式。如需詳細資料，請參閱[應用程式管理](../../manageapps/app_mng.html)。

## 2015 年 5 月 5 日：已更新 Node.js 建置套件 v1.17-20150429-1033

* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 0.12.1 版](https://developer.ibm.com/node/sdk/)。
* 如果您的應用程式未在其 package.json 檔案中指定執行時期，則您的應用程式現在將開始使用 0.12.1 版而非 0.10.x 版。如果您需要使用舊版，請在 package.json 中指定 0.10.x 版，如下所示：

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* 0.12.1 版有已知的問題：
   * 使用 Bluemix Live Sync 提供的「除錯工具」特性時，「暫停」特性故障。
   * 在 0.12.x 版上，不支援用於 MQ Light 服務的 mqlight 模組

* 已解決多種安全漏洞：
  * 已修正 OpenSSL 中會影響 IBM SDK for Node.js 的漏洞。如需相關詳細資料，請參閱[安全公告](http://www-01.ibm.com/support/docview.wss?uid=swg21701494)。
  * 已修正 RC4 Stream Cipher 中會影響 IBM SDK for Node.js 的漏洞。如需相關詳細資料，請參閱[安全公告](http://www-01.ibm.com/support/docview.wss?uid=swg21882778)。

##  2015 年 4 月 2 日：已更新 Node.js 建置套件 v1.15-20150331-2231

* Node.js 建置套件現在包含三個新增特性，可以協助在 Bluemix 上進行快速開發，就像在桌上型電腦上一樣，而不必重新部署
  * 桌面同步：使任何 (Windows) 桌面樹狀結構與雲端型專案工作區同步
  * 即時編輯：您可以變更在 Bluemix 中執行的 Node.js 應用程式，並立刻在瀏覽器中測試它們。
  * 除錯：開啟 Shell 進入您的環境並進行除錯！您可以使用 Node Inspector 除錯器，動態地編輯程式碼、插入中斷點、逐步執行程式碼、重新啟動執行時期等等
  * 如需相關資訊，請參閱[應用程式管理](../../manageapps/app_mng.html#Utilities)。
* 我們已經加入來自 [Cloud Foundry 的 Node.js 建置套件](https://github.com/cloudfoundry/nodejs-buildpack)的最新變更。這附有由社群所提出的許多錯誤修正程式和改良功能。
* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 1.1.0.13 版](https://developer.ibm.com/node/sdk/)。

## 2015 年 1 月 5 日：已更新 Node.js 建置套件 v1.9.1-20141208-1221

* Node.js 建置套件現在包含動態日誌設定支援。如果應用程式是使用 log4js、bunyan 或 ibmbluemix 模組來記載，則開發人員可以使用此功能即時變更其應用程式的記載層次。
* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 0.10.33 版](https://developer.ibm.com/node/sdk/)。這包括 POODLE 問題的修正程式。

## 2014 年 10 月 23 日：已更新 Node.js 建置套件 v1.6-20141013-1736

* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 1.1.0.8 版](https://developer.ibm.com/node/sdk/)。這表示，當您為應用程式指定最新穩定的 Node.js 執行時期 0.10.32 版時，您會得到受完整支援的 IBM Node.js 執行時期。這個最新的 SDK 隨附了修正程式，可解決內嵌 qs 模組導致拒絕服務的問題。它也包含更新版本的 npm 模組，以及 http 和 url 模組中的其他改良功能。如需其他詳細資訊，請參閱 [0.10.32 版變更日誌](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog)。
* 建置套件也針對在部署期間新增不正確 index.html 檔案至客戶應用程式中的錯誤，包含解決錯誤的修正程式。

## 2014 年 9 月 30 日：已更新 Node.js 建置套件 v1.4-20140908-1746

* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 1.1.0.7 版](https://developer.ibm.com/node/sdk/)。這表示，當您為應用程式指定最新穩定的 Node.js 執行時期 0.10.31 版時，您會得到受完整支援的 IBM Node.js 執行時期。有了受完整支援的 Node.js 執行時期，客戶可以使用它作為基礎進行建置，並且知道他們可以依賴 IBM 產品一向具備的深度支援。
* 建置套件包含改良過的服務架構。具體而言，它在連結 Monitoring and Analytics 服務時運作情況更好，萬一發生失敗還可以提供額外的診斷資訊。

## 2014 年 8 月 28 日：已更新 Node.js 建置套件 v1.3-20140821-1143

* 現在，最新的 Node.js 建置套件隨附了 IBM SDK for Node.js 1.1.0.6 版。這表示，當您為應用程式指定最新穩定的 Node.js 執行時期 0.10.30 版時，您會得到受完整支援的 IBM Node.js 執行時期。這個執行時期可修正[第 8 版記憶體毀損漏洞](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow)。
* 建置套件也包括 Monitoring and Analytics 服務延伸的改良功能及錯誤修正程式，讓您可以透過該服務來診斷效能及錯誤狀況。

## 2014 年 7 月 29 日：已更新 Node.js 建置套件 v1.1-20140717-1447

現在，Node.js 建置套件隨附了 IBM SDK for Node.js 1.1.0.5 版。這表示，當您為應用程式指定最新穩定的 Node.js 執行時期 0.10.29 版時，您會得到受完整支援的 IBM Node.js 執行時期。如需進一步瞭解 IBM Node.js SDK，請查看[這裡](https://developer.ibm.com/node/sdk/)。

# 相關鏈結
## 一般
* [Node.js 執行時期](index.html)
