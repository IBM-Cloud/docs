---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 IBM {{site.data.keyword.blockchain}}
{: #gettingstartedtemplate}
前次更新：2016 年 10 月 13 日
{: .last-updated}

**注意：**使用「入門範本開發人員」方案（測試版）或「高安全性商業網路」方案（GA 版）之前，您必須閱讀[使用須知](needtoknow.html)中的技術及支援資訊。
<br><br>

## 供應項目方案狀態

「入門範本開發人員」方案是測試版，並提供多方承租戶開發環境。「高安全性商業網路」方案已在 2016 年 10 月 20 日正式發行（GA 版）。「高安全性商業網路」方案透過使用 [IBM Secure Service Container](etn_ssc.html) 的程式碼隔離，提供高安全的單一承租戶 LinuxONE on z 環境。
<br><br>

## IBM Blockchain on Bluemix

您只需要按一下按鈕，Bluemix&reg; 上的 {{site.data.keyword.blockchainfull}} 服務便能提供四個節點的開發及測試區塊鏈網路。開發人員可以立即開始撰寫應用程式以及部署鏈碼，而不必從頭開始建立區塊鏈網路。IBM Blockchain on Bluemix 服務是一個對等式且具有許可權的網路，它是以 Linux Foundation 之 Hyperledger Project 的 [Hyperledger Fabric 0.5 版](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)程式碼為建置基礎。
{:shortdesc}

區塊鏈網路用來安全且有效率地交換與追蹤數位資產，以及永久地在共用分類帳上記錄所有交易。如需區塊鏈的詳細資料，請參閱[關於區塊鏈](ibmblockchain_overview.html)主題。
<br><br>

## 選擇網路方案

您可以選擇兩個 IBM Blockchain on Bluemix 方案：**入門範本開發人員網路**或**高安全性商業網路**。請使用下面的比較圖表，來選擇正確的環境。

<!-- Commenting our for move to GA status jh 10/07/16
![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html). -->

| Bluemix 方案：      | 入門範本開發人員網路       | 高安全性商業網路
| ------------------------- |:--------------------------:|:-----:|
| 狀態：    | 測試版     | GA 版 |
| 用途：  |  安全、效能及可用性的開發及測試層次 |  模擬企業網路，以及安全、效能及可用性的測試層次 |
| 節點：    | 4 個節點 + 憑證管理中心     | 4 個節點 + 憑證管理中心 |
| [儀表板監視器：](ibmblockchainmonitor.html) | 是 | 是 |
| 機密交易： | 是 | 是 |
| [共識：](etn_pbft.html) | PBFT | PBFT |
| 環境：     | 共用多方承租戶 | 隔離的單一承租戶 |
| [IBM Secure Service Container：](etn_ssc.html) | 否 | 是 |

<br>
## 啟動網路方案

請使用下列步驟，來建立及部署區塊鏈網路的未連結服務實例。您的網路包括具有驗證節點和安全服務的開發環境，並且可讓您部署鏈碼、檢視日誌及建置應用程式：

1. 從 [{{site.data.keyword.blockchain}} 服務](https://console.ng.bluemix.net/catalog/services/blockchain/)頁面中，完成右窗格的**新增服務**表單：
  - **空間：**選取 **dev**。
  - **應用程式：**選取**維持不連結**，或是若要將服務連結至其中一個 Bluemix.org 應用程式，則**選取應用程式**。
  - **服務名稱：**輸入唯一名稱或值（例如 **Blockchain Test Net123**）。
  - **認證名稱：**保留預設值。
  - **選取的方案：**選擇**入門範本開發人員**或**高安全性**。
  - 按一下**建立**按鈕。
2.  您現在位於新服務的**服務儀表板**畫面上。您可以在這裡**管理**網路實例；按一下**啟動**，以使用區塊鏈監視器。
3.  區塊鏈監視器會顯示網路詳細資料、即時日誌、現行分類帳狀態、API 及鏈碼範本。儀表板可用來進行下列任何功能：
  - 存取網路對等節點的探索及 API 路徑。
  - 檢視任何執行中的鏈碼容器。
  - 檢視即時日誌，以及對鏈碼進行疑難排解。
  - 檢視分類帳的廣域狀態。
  - 存取 Swagger 使用者介面，以及透過 REST API 與網路互動。
  - 部署三個鏈碼範例的其中一個。


# 相關鏈結
{: #rellinks}
## 指導教學及範例
{: #samples}
* [IBM 的大理石展示 (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [IBM 的商業票據展示 (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [IBM 的租車展示 (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [藝術拍賣展示 (Github)](https://github.com/ITPeople-Blockchain/auction)

## API 參考資料
{: #api}
* [Swagger 使用者介面](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [Hyperledger Fabric API (GitHub)](https://github.com/hyperledger/fabric/tree/master/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/master/sdk/node)

## 相關鏈結
{: #general}
* [網狀架構程式碼](https://github.com/hyperledger/fabric)
* [白皮書](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [通訊協定規格及相關文件](https://github.com/hyperledger/fabric/tree/master/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [Bluemix 服務的新增功能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
