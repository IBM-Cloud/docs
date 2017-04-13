---

copyright:
  years: 2017
lastupdated: "2017-03-17"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 應用程式開發
{: #v10_dashboard}


使用 marbles02 範例鏈碼及對應的 javascript 應用程式，作為建立您自己的商業解決方案的範本。
{:shortdesc}


應用程式運用 Node.js SDK API 以與所佈建的網路元件互動，最後將目標設為具有交易要求的對等節點。請在「監視器」之**資源**畫面的**服務認證**標籤內，找出對等節點、「憑證管理中心」及網路「排序服務」的 API 端點，並將這些字串插入您應用程式隨附的配置檔中。不過，請注意，如果您要將目標設為網路中的其他對等節點（例如，需要非您組織所屬的對等節點的背書時），則需要取得這些對等節點的正確 API 端點。您也需要儲存其他組織的 CA 憑證，才能驗證傳回給應用程式的回應。此資訊未公開於**資源**視圖中，因此，您必須聯絡 Bluemix 組織的適當管理者，並在頻外作業中獲得此資料。排序服務 URL 通用於整個網路；您不需要此元件的任何成員特定資訊。  

如需原始碼及必要條件，請造訪[大理石](https://github.com/IBM-Blockchain/marbles/tree/v3.0) GitHub 儲存庫；請遵循 README，並啟動應用程式。  

請探索 [SDK 儲存庫](https://github.com/hyperledger/fabric-sdk-node)，以實驗端對端測試，更深入地瞭解 API。
