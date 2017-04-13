---

copyright:
  years: 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用
{: #gettingstartedtemplate}

**注意：**使用任何 IBM Blockchain on Bluemix 方案之前，您必須閱讀[免責聲明](needtoknow.html)中的技術及支援資訊。
{:shortdesc}

## IBM Blockchain on Bluemix

{{site.data.keyword.blockchainfull}} on Bluemix&reg; 服務包含三個區塊鏈網路方案。**高安全性商業網路 (HSBN) vNext 測試版**這個最新方案是以 Hyperledger Fabric 1.0 版程式碼庫為建置基礎，並運用模組架構來提供新功能。IBM Blockchain on Bluemix 方案可讓開發人員立即撰寫及測試鏈碼應用程式，而不需要設計及配置專用區塊鏈網路。鏈碼是引擎，可在 Fabric 區塊鏈網路上進行安全且具效率的資產交換，並在分類帳上永久記錄這些交易。

## 供應項目方案

新的 IBM Blockchain on Bluemix 訂閱者現在可以登記於 **HSBN vNext 測試版**方案中。這個最新供應項目是以 Hyperledger Fabric 1.0 版為建置基礎，可提供新一代的安全、完整性、可擴充性及效能。表格 1 說明 Bluemix 方案：

表格 1：IBM Blockchain on Bluemix 方案  

| Bluemix 方案      | 狀態       | 可供新的訂閱者使用  | Hyperledger Fabric 版本
| ------------------------- |:--------------------------:|:-----:|:-----:|
| **HSBN vNext 測試版** (1)   | 測試版     | 是 |  1.0 版 |
| HSBN (2) |  GA 版 |  是 |  0.6 版 |
| 入門範本開發人員 (3)    | 測試版     | 是 | 0.6 版 |

(1) **高安全性商業網路 (HSBN) vNext 測試版**方案提供一種簡易機制，來加入 Bluemix 組織以及建置分散式區塊鏈網路。  
(2) **高安全性商業網路 (HSBN) GA** 方案透過使用 [IBM Secure Service Container](etn_ssc.html) 的程式碼隔離，提供高安全的單一承租戶 LinuxONE on z Systems 環境。  
(3)「入門範本開發人員測試版」方案提供僅限多方承租戶開發的環境。  

## 供應項目方案詳細資料

表格 2 提供 IBM Blockchain on Bluemix 供應項目方案的詳細比較。新的 IBM Blockchain on Bluemix 訂閱者必須選擇 **HSBN vNext 測試版**方案。新的訂閱者已不支援 HSBN 及「入門範本開發人員」方案，但 IBM 仍予以支援：

表格 2：IBM Blockchain on Bluemix 方案詳細資料  

| Bluemix 方案：      | 入門範本開發人員網路       | 高安全性商業網路       | 高安全性商業網路 (HSBN) vNext 測試版
| ------------------------- |:--------------------------:|:-----:|:-----:|
| 狀態：    | 測試版     | GA 版 | 測試版 |
| 用途：  |  安全、效能及可用性的開發及測試層次 |  模擬企業網路，以及安全、效能及可用性的測試層次 |  設定具有正式作業等級安全、效能及可用性的企業商業網路 |
| 節點：    | 4 個對等節點 + 憑證管理中心     | 4 個對等節點 + 憑證管理中心 | 網路元件的動態管理 |
| 儀表板監視器： | [是](ibmblockchainmonitor.html) | [是](ibmblockchainmonitor.html) | [是](v10_dashboard.html) |
| 環境：     | 共用多方承租戶 | 隔離的單一承租戶 | 多個隔離層次 |

# 相關鏈結
{: #rellinks}
## 指導教學及範例
{: #samples}
* [IBM 的大理石展示 (GitHub)](https://github.com/IBM-Blockchain/marbles) - 0.6 版 & 1.0 版
* [IBM 的商業票據展示 (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme) - 0.6 版
* [IBM 的租車展示 (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) - 0.6 版
* [藝術拍賣展示 (Github)](https://github.com/ITPeople-Blockchain/auction) 0.6 版 - 1.0 版（在本端執行）

## API 參考資料
{: #api}
* [Hyperledger Fabric API (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## 相關鏈結
{: #general}
* [網狀架構程式碼](https://github.com/hyperledger/fabric)
* [網狀架構編製器](https://fabric-composer.github.io/)
* [Fabric 1.0 版文件](http://hyperledger-fabric.readthedocs.io/en/latest/)
* [Fabric 0.6 版文件](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Bluemix 服務的新增功能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
