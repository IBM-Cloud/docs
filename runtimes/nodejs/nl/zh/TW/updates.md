---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# SDK for Nodejs 建置套件的最新更新項目
{: #latest_updates}

sdk-for-nodejs 建置套件中的最新更新項目清單。

## 2017 年 3 月 10 日：已更新 Node.js 建置套件 3.11 版
這個版本的建置套件支援 IBM SDK for Node.js 運行環境版本：0.10.47、0.10.48、0.12.17、0.12.18、4.7.3、4.8.0、6.9.5 及 6.10.0。預設版本現在是 4.8.0。

除了新的運行環境之外，這個版本還會包含在使用 devconsole 使用者介面啟用 Shell 應用程式管理處理程式時所遇到的錯誤修正程式。此建置套件也會變更 Monitoring and Analytics 服務的自動配置運作方式。使用「免費」方案的應用程式無法再將記載功能新增至其應用程式，它現在已被 logmet 取代。

## 2017 年 1 月 20 日：已更新 Node.js 建置套件 3.10 版
這個版本的建置套件支援 IBM SDK for Node.js 運行環境版本：0.10.47、0.10.48、0.12.17、0.12.18、4.7.0、4.7.2、6.9.2 及 6.9.4。預設值現在是 4.7.2。

它包含錯誤的修正程式，該錯誤為不一定會呼叫 "npm start" 來啟動應用程式。

## 2016 年 11 月 17 日：已更新 Node.js 建置套件 3.9 版
這個版本的建置套件支援 IBM SDK for Node.js 運行環境版本：0.10.47、0.10.48、0.12.16、0.12.17、4.6.1、4.6.2、6.7.0 及 6.9.1。預設值現在是 4.6.2。

請注意，Node.js 第 6 版已在 2016 年 10 月 18 日升級至 LTS 狀態，而且很快會變成建置套件的預設運行環境。Node.js 0.10 版已在 2016 年 10 月 31 日到達使用期限，很快就不再內含在建置套件中。如需詳細資料，請參閱 [Node.js 版本長期支援及 SDK for Node.js 建置套件](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/)。

在這個版本中，已處理會影響追蹤及檢查程式「應用程式管理」處理程式的錯誤（當追蹤及檢查程式「應用程式管理」處理程式與 Node.js 第 6 版一起使用時）。如需 Node.js 第 6 版整合檢查程式功能後如何變更檢查程式處理程式的相關資訊，請參閱[管理 Liberty 及 Node.js 應用程式](/docs/manageapps/app_mng.html#inspector)。

## 2016 年 10 月 7 日：已更新 Node.js 建置套件 v3.8-20161006-1211
這個版本的建置套件支援 IBM SDK for Node.js 運行環境版本：0.10.46、0.10.47、0.12.15、0.12.16、4.5.0、4.6.0、6.6.0 及 6.7.0。預設值現在是 4.6.0。

除了新的運行環境之外，這個版本還包含建置套件錯誤修正程式。使用 Node.js 6.x 以及 v3.7-20160826-1101 版更新項目所提及的「開發模型」時的已知問題修正程式就是其中一個。這個版本同時還與 [Cloud Foundry Node.js 建置套件 v1.5.20](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.20) 同步。

## 2016 年 8 月 26 日：已更新 Node.js 建置套件 v3.7-20160826-1101
這個版本的建置套件支援 IBM SDK for Node.js 運行環境版本：0.10.45、0.10.46、0.12.14、0.12.15、4.4.7、4.5.0、6.2.2 和 6.4.0。預設值現在是 4.5.0。

這個版本包括錯誤修正程式（包括 [Cloud Foundry 的 Node.js 建置套件 1.5.18](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.18) 中的錯誤修正程式）。

這個版本不再支援 [Bluemix Node.js 建置套件 3.3 版 - FIPS 模式及其他項目](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/)中所發表的 strongpm「應用程式管理」處理程式。

請注意，使用 Node.js 6.x 及[開發模型](/docs/manageapps/app_mng.html#devmode)時，有一個已知問題。作為暫行解決方法，您將需要在啟用「開發模型」之後重新編譯打包您的應用程式，然後才能開始使用它。

## 2016 年 7 月 22 日：已更新 Node.js 建置套件 v3.6-20160715-0749
這個版本的建置套件支援 IBM SDK for Node.js 運行環境版本：0.10.45, 0.10.46、0.12.14、0.12.15、4.4.6、4.4.7、6.2.1 和 6.2.2。現在預設值為 4.4.7。

此版本包含已更新的「應用程式管理 Proxy」，可支援聯合登入。

其中包括下列安全漏洞的修正程式：
* [CVE-2016-1669](http://www-01.ibm.com/support/docview.wss?uid=swg21986383)

## 2016 年 6 月 22 日：已更新 Node.js 建置套件 v3.5-20160609-1608

這個版本的建置套件新增了 IBM SDK for Node.js 運行環境 4.4.5 及 6.2.0 版。預設為 4.4.5。

這個版本不再支援 [Bluemix Node.js 建置套件 3.3 版 - FIPS 模式及其他項目](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/)中所發表的舊運行環境版本。建置套件現在支援 0.10.44、0.10.45、0.12.13、0.12.14、4.4.4、4.4.5、6.1.0 及 6.2.0。

這個版本包括 [Cloud Foundry 的 Node.js 建置套件 1.5.14](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14) 中的錯誤修正程式。

## 2016 年 5 月 20 日：已更新 Node.js 建置套件 v3.4-20160518-1653

這個版本的建置套件新增了 IBM SDK for Node.js 運行環境 0.10.45、0.12.14、4.4.4、6.0.0 及 6.1.0 版。預設值現在是 4.4.4。

其中包括下列安全漏洞的修正程式：
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.openssl.org/news/secadv/20160503.txt)

請注意，npm 第 3 版及「應用程式管理」檢查程式公用程式有已知問題。npm 3.8.6 是 6.0.0 及 6.1.0 運行環境的預設值。如果您要使用 6.x 運行環境及檢查程式公用程式，則暫行解決方法是應該在 package.json 中指定 2.x npm 版本。

## 2016 年 4 月 29 日：已更新 Node.js 建置套件 v3.3-20160428-1409

這個版本的建置套件新增了 IBM SDK for Node.js 運行環境 0.10.44、0.12.13、4.4.0、4.4.1、4.4.2 及 4.4.3 版。預設值現在是 4.4.3。

對於 4.3.1 及以上版本，現在可以藉由為應用程式設定 `FIPS_MODE=true` 環境變數，使用已啟用 FIPS 功能的運行環境版本。

更新的建置套件和新運行環境也包含下列安全漏洞的修正程式：
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

更新的建置套件也包含數個錯誤的修正程式：
* 現在如果有符合所要求範圍的 IBM SDK for Node.js 建置可用，將一律使用 IBM SDK for Node.js 建置。先前只有針對 4.x 運行環境版本才是這種情況。
* 現在「應用程式管理」檢查程式公用程式將與 4.x 運行環境版本搭配運作。
* 已修正 strongpm「應用程式管理」公用程式中的回歸。

## 2016 年 3 月 18 日：已更新 Node.js 建置套件 v3.2-20160315-1257

這個版本的建置套件將預設 IBM SDK for Node.js 運行環境從 4.3.0 版移至 4.3.2 版。它也包括 IBM SDK for Node.js 0.10.43 版、0.12.12 版及 4.3.1 版。請使用這些最新的 Node.js 版本來取得數個安全漏洞的修正程式。

## 2016 年 3 月 4 日：已更新 Node.js 建置套件 v3.1-20160222-1123

這個版本的建置套件將預設 IBM SDK for Node.js 運行環境從 4.2.4 版移至 4.3.0 版。它也包括 IBM SDK for Node.js 0.10.42 版、0.12.10 版及 4.2.6 版。請使用這些最新的 Node.js 版本來取得數個安全漏洞的修正程式。

## 2016 年 2 月 4 日：已更新 Node.js 建置套件 v3.0-20160125-1224

此版本與 [Cloud Foundry 社群 Node.js](https://github.com/cloudfoundry/nodejs-buildpack) 建置套件完全同步。除了社群變更之外，也會修改特定預設值，並且進行最佳化來減少編譯打包時間，以及更新「應用程式管理」特性。

* 建置套件更新項目：

  * Node.js 4.2.4 版（IBM SDK for Node.js 第 4 版）現在是 Bluemix 上的預設運行環境，取代 0.12.9 版。如果未針對應用程式指定特定版本，這項變更可能會造成您的應用程式有不同的行為。若要瞭解如何指定 Bluemix 應用程式的 Node.js 版本，請參閱 [Node.js 運行環境](index.html)文件。

  * 依預設，NODE_ENV 現在是設為 *production*。這項變更使得某些 node 相依關係會有不同的行為。例如，Express 架構將不再於 Web 瀏覽器中傳回失敗端點的堆疊追蹤，而是顯示*內部伺服器錯誤*。當 NPM_CONFIG_PRODUCTION 設為 *true* 時，NPM 會將 NODE_ENV 設為 *production*，而這僅針對 npm 安裝階段中的子 Shell Script。這個功能可讓使用者將應用程式運行環境的 NODE_ENV 設為其他值，例如 *development*。為了清楚說明，npm Script 會看到此訊息：**NODE_ENV=production**。

  * 已包括 Monitoring and Analytics 服務的錯誤修正程式。

* 快取更新項目：

  * 如果已停用快取 (NODE_MODULES_CACHE=false)，建置套件將不會嘗試快取任何模組/元件。先前此設定使得快取不會被取出，但它仍然會快取已安裝的模組供未來部署使用。現在，它將不會取出快取，也不會嘗試儲存任何快取。

  * 除了 node_modules 之外，依預設，還會快取 bower_components。

* 其他更新項目：

  * 已新增 gulp、bower 及 angular 這類遺漏相依關係的有用警告。

  * 已使用建置套件版本資訊更新了 detect Script。

  * 已移除社群一開始產生的叢集建議 (WEB_CONCURRENCY)，因為在 Bluemix 上的記憶體判定不正確。


## 2015 年 12 月 16 日：已更新 Node.js 建置套件 v2.8-20151209-1403 及 v3.0beta-20151211-2041

這個版本的 Node.js 建置套件有兩個版本：2.8 版和 3.0 測試版。這兩個版本都包括下列變更：

Monitoring and Analytics 服務的錯誤修正程式
包含根據社群版本 Node.js 4.2.3 版、4.2.2 版、0.12.9 版及 0.12.8 版之 IBM SDK for Node.js 4.2.3.0 版、4.2.2.0 版、1.2.0.8 版及 1.2.0.7 版的快取運行環境。
此外，在 3.0 測試版中，預設 Node.js 運行環境已變更為 4.2.3 版。

在 Bluemix 上，IBM Node.js 建置套件 3.0 測試版現在已發行為非預設建置套件，並以 Node.js 4.2.3 版作為預設運行環境。為確保應用程式和服務能夠在 Bluemix 上繼續運作，請以建置套件的測試版來推送應用程式。經過至少 30 天以後，第 3 版將成為預設建置套件。

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

如果您已在應用程式的 package.json 中配置特定版本的 Node.js，則預設運行環境的這項變更不會影響您的應用程式。

**附註：**您隨時都可以在 package.json 中使用 engines.node 項目，指定用來執行應用程式的 Node.js 版本（如[可用的版本](index.html#available_versions)中所述）。

## 2015 年 11 月 23 日：已更新 Node.js 建置套件 v2.7-20151118-1003

在 2.7 中，包括 IBM SDK for Node.js 4.2.1.0 版（根據 Node 4.2.1 版 LTS）。它還不是預設值，但是可以指定以供使用。**附註：**這個版本會取代先前提供的開放程式碼建置。我們也對服務延伸架構進行了一些較小的錯誤修正。

## 2015 年 10 月 19 日：已更新 Node.js 建置套件 v2.6.1-20151015-1326

Node.js 2.6.1 版引進了 [StrongPM 應用程式管理處理程式](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)的錯誤修正程式，以及更一致的 NPM 版本。

## 2015 年 10 月 15 日：已更新 Node.js 建置套件 v2.6-20151006-1309

這個版本的 Node.js 建置套件，其特性就是將 [StrongLoop Process Manager ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://strong-pm.io) 整合至「應用程式管理」特性。如需相關資訊，請參閱部落格文章 [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)。

## 2015 年 6 月 15 日：已更新 Node.js 建置套件 v2.0-20150608-1503

在這個版本中，我們的 Node.js 建置套件已與最新 [CF 社群 Node.js 建置套件](https://github.com/cloudfoundry/nodejs-buildpack)同步化，後者具有許多來自社群的新特性。
此外，我們也改良了 Node.js 建置套件中的「應用程式管理」特性，它能夠啟用 Shell、node-inspector、Bluemix Live Sync 等這類公用程式。如需詳細資料，請參閱[應用程式管理](/docs/manageapps/app_mng.html)。

## 2015 年 5 月 5 日：已更新 Node.js 建置套件 v1.17-20150429-1033

* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 0.12.1 版](https://developer.ibm.com/node/sdk/)。
* 如果您的應用程式未在其 package.json 檔案中指定運行環境，則您的應用程式現在將開始使用 0.12.1 版而非 0.10.x 版。如果您需要使用舊版，請在 package.json 中指定 0.10.x 版，如下所示。

```
"engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* 0.12.1 版的已知問題：
   * 使用 Bluemix Live Sync 所提供的「除錯工具」特性時，「暫停」特性故障。
   * 在 0.12.x 版上，不支援用於 MQ Light 服務的 mqlight 模組。

* 已解決多種安全漏洞：
  * 已修正 OpenSSL 中會影響 IBM SDK for Node.js 的漏洞。如需相關詳細資料，請參閱[安全公告](http://www-01.ibm.com/support/docview.wss?uid=swg21701494)。
  * 已修正 RC4 Stream Cipher 中會影響 IBM SDK for Node.js 的漏洞。如需相關詳細資料，請參閱[安全公告](http://www-01.ibm.com/support/docview.wss?uid=swg21882778)。

##  2015 年 4 月 2 日：已更新 Node.js 建置套件 v1.15-20150331-2231

* Node.js 建置套件現在包含三個新增特性，可以協助在 Bluemix 上進行快速開發，就像在桌上型電腦上一樣，而不必重新部署
  * 桌面同步：使任何 (Windows) 桌面樹狀結構與雲端型專案工作區同步
  * 即時編輯：可讓您變更在 Bluemix 中執行的 Node.js 應用程式，並立刻在瀏覽器中測試它們。
  * 除錯：開啟 Shell 進入您的環境並進行除錯！您可以使用 Node Inspector 除錯器，動態地編輯程式碼、插入中斷點、逐步執行程式碼、重新啟動運行環境等等
  * 如需相關資訊，請參閱[應用程式管理](/docs/manageapps/app_mng.html#Utilities)。
* 我們已經加入來自 [Cloud Foundry 的 Node.js 建置套件](https://github.com/cloudfoundry/nodejs-buildpack)的最新變更。這項變更附有由社群所提出的許多錯誤修正程式和改良功能。
* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 1.1.0.13 版](https://developer.ibm.com/node/sdk/)。

## 2015 年 1 月 5 日：已更新 Node.js 建置套件 v1.9.1-20141208-1221

* Node.js 建置套件現在包含動態日誌設定支援。如果應用程式是使用 log4js、bunyan 或 ibmbluemix 模組來進行記載，則開發人員可以使用這項支援來動態變更其應用程式的記載層次。
* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 0.10.33 版](https://developer.ibm.com/node/sdk/)。這項更新包括 POODLE 問題的修正程式。

## 2014 年 10 月 23 日：已更新 Node.js 建置套件 v1.6-20141013-1736

* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 1.1.0.8 版](https://developer.ibm.com/node/sdk/)。這項更新表示，當您為應用程式指定最新穩定的 Node.js 運行環境 0.10.32 版時，您會得到完整支援的 IBM Node.js 運行環境。這個最新的 SDK 隨附了修正程式，可解決內嵌 qs 模組導致拒絕服務的問題。它也包含更新版本的 npm 模組，以及 http 和 url 模組中的其他改良功能。如需詳細資料，請參閱 [0.10.32 版變更日誌](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog)。
* 建置套件也針對在部署期間新增不正確 index.html 檔案至客戶應用程式中的錯誤，包含解決錯誤的修正程式。

## 2014 年 9 月 30 日：已更新 Node.js 建置套件 v1.4-20140908-1746

* 現在，Node.js 建置套件隨附了 [IBM SDK for Node.js 1.1.0.7 版](https://developer.ibm.com/node/sdk/)。這項更新表示，當您為應用程式指定最新穩定的 Node.js 運行環境 0.10.31 版時，您會得到完整支援的 IBM Node.js 運行環境。使用完整支援的 Node.js 運行環境，客戶就得到一致的支援體驗。
* 建置套件包含改良過的服務架構。具體而言，它在連結 Monitoring and Analytics 服務時運作情況更好，如果服務失敗還可以提供其他診斷資訊。

## 2014 年 8 月 28 日：已更新 Node.js 建置套件 v1.3-20140821-1143

* 現在，最新的 Node.js 建置套件隨附了 IBM SDK for Node.js 1.1.0.6 版。這項更新表示，當您為應用程式指定最新穩定的 Node.js 運行環境 0.10.30 版時，您會得到完整支援的 IBM Node.js 運行環境。這個運行環境可修正[第 8 版記憶體毀損漏洞 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow)。
* 建置套件也包括 Monitoring and Analytics 服務延伸的改良功能及錯誤修正程式，讓您可以透過該服務來診斷效能及錯誤狀況。

## 2014 年 7 月 29 日：已更新 Node.js 建置套件 v1.1-20140717-1447

現在，Node.js 建置套件隨附了 IBM SDK for Node.js 1.1.0.5 版。這項更新表示，當您為應用程式指定最新穩定的 Node.js 運行環境 0.10.29 版時，您會得到完整支援的 IBM Node.js 運行環境。請進一步瞭解 [IBM Node.js SDK](https://developer.ibm.com/node/sdk/)。

# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Node.js 運行環境](index.html)
