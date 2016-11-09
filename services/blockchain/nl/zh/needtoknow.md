---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 使用須知
{: #etn_overview}
前次更新：2016 年 10 月 13 日
{: .last-updated}

**注意：**您必須先檢閱下列資訊，然後才能使用任一 IBM Blockchain on Bluemix 方案：「入門範本開發人員（測試版）」或「高安全性商業網路（GA 版）」。
<br><br>

## IBM 支援聲明

IBM 在創新領域擁有歷史悠久的領導地位，並持續提供最新的 IBM Blockchain 供應項目。區塊鏈是一種快速發展的技術，預計會瓦解從金融到物流的一些產業。透過各種早期採用計劃，IBM 客戶及事業夥伴正在影響未來的區塊鏈方向。IBM Blockchain on Bluemix 即為這類程式。**如同所有的新技術一樣，IBM Blockchain on Bluemix 使用者應該準備好因應快速的基本變更**。  
{:shortdesc}

IBM Blockchain 後面的架構是 Linux Foundation 的 Hyperledger Project。Hyperledger Fabric 是正在積極發展的開放程式碼專案，目前處於*籌劃* 狀態。每一個開放程式碼社群的貢獻使得 Hyperledger Fabric 更為健全，但可能有採用挑戰。在*籌劃* 週期期間，用戶端可以使用 Hyperledger Fabric 0.5 版進行網路測試及模擬，但 **IBM 警告不要直接在 Hyperledger Fabric 0.5 版區塊鏈網路上執行有價值的金融資產**。  
<br>

## 開放程式碼聲明

IBM Blockchain on Bluemix（「入門範本開發人員」方案及「高安全性商業網路」方案）使用 Linux Foundation 的 Hyperledger Fabric 0.5 版開放程式碼。Hyperledger Project 成員（包括 IBM）會將程式碼提出至網狀架構，在此之後，社群會進行檢閱、調查及測試。
Hyperledger Fabric 0.5 版目前處於*籌劃* 狀態；以下提供*籌劃* 狀態及 Hyperledger Project 個生命週期的詳細資料：//github.com/hyperledger/hyperledger/wiki/Project-Lifecycle。
<br><br>

## 鏈碼支援聲明

IBM Blockchain 不支援[非唯一性鏈碼](ibmblockchain_tutorials.html#ndcc)，因為這會造成任何區塊鏈網路上資料一致性及完整性的風險。將新的鏈碼部署至 IBM Blockchain on Bluemix 網路之前，請檢閱[非唯一性鏈碼](ibmblockchain_tutorials.html#ndcc)的詳細資料。

除了[非唯一性鏈碼](ibmblockchain_tutorials.html#ndcc)之外，IBM Blockchain 網路也不支援下列編碼實務：

1. 搭配使用聯合陣列與反覆運算（順序在 Go 中已隨機化）。
2. 從 KVS 表格中讀取項目清單（不保證順序）。
3. 撰寫執行緒不安全的鏈碼（可以並行呼叫查詢及呼叫）。
4. 替換分類帳狀態變數在鏈碼中的通用記憶體或快取儲存空間。
5. 直接從鏈碼中存取外部服務（例如，資料庫）。
6. 使用可能會引入非唯一性（例如使用 "random" 或 "time"）的程式庫或廣域變數。
<br><br>

## 取得協助

如需 IBM Blockchain on Bluemix 網路的支援及協助，請參閱[取得支援](ibmblockchain_support.html)。
