---

copyright:
  years: 2017
lastupdated: "2017-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 免責聲明
{: #etn_overview}

**注意：**您必須先檢閱下列資訊，才能使用任何 IBM Blockchain on Bluemix 方案。

## IBM 支援聲明

IBM 在創新領域擁有歷史悠久的領導地位，並持續提供 IBM Blockchain on Bluemix 供應項目方案。區塊鏈是一種快速發展的技術，預計會瓦解從金融到供應鏈到物流的若干產業。透過各種早期採用計劃，IBM 客戶及事業夥伴已主動將區塊鏈推進為產業解決方案。IBM Blockchain on Bluemix 即為這類程式。**如同所有新技術一樣，IBM Blockchain on Bluemix 使用者應該注意因應快速基本變更的可能性**。  
{:shortdesc}

IBM Blockchain 背後的基礎架構是 Linux Foundation 的 Hyperledger Fabric 專案。Fabric 目前處於*作用中* 狀態，並且持續進行開發。每一個開放程式碼社群的貢獻都可以改善 Hyperledger Fabric，但可能會通過挑戰。在*作用中* 專案週期期間，用戶端可以使用 Hyperledger Fabric 1.0 版進行網路測試及模擬。**IBM 警告不要直接在任何 Hyperledger Fabric 區塊鏈網路上定義或交換金融資產或任何有價值的資產**。  

## 開放程式碼聲明

**高安全性商業網路 (HSBN) vNext 測試版**方案是以 Linux Foundation 的 Hyperledger Fabric 1.0 版開放程式碼為建置基礎。「入門範本開發人員」及「高安全性商業網路 (HSBN)」方案是以 Hyperledger Fabric 0.6 版程式碼為建置基礎。Hyperledger Project 成員（包括 IBM）會持續提出原始碼，在此之後，社群會進行檢閱、調查及測試。Hyperledger Fabric 1.0 版目前處於*作用中* 狀態；以下網址提供*作用中* 狀態及 Hyperledger Project 生命週期的詳細資料：https://wiki.hyperledger.org/community/project-lifecycle。  

## 鏈碼支援聲明

IBM Blockchain 網路「不」支援下列編碼實務：

1. 搭配使用聯合陣列與反覆運算（順序在 Go 中已隨機化）。
2. 從 KVS 表格中讀取項目清單（不保證順序）。
3. 撰寫執行緒不安全的鏈碼（可以並行呼叫查詢及呼叫）。
4. 替換分類帳狀態變數在鏈碼中的通用記憶體或快取儲存空間。
5. 直接從鏈碼中存取外部服務（例如，資料庫）。
6. 使用可能會引入非唯一性（例如使用 "random" 或 "time"）的程式庫或廣域變數。
7. 使用 GetRows 進行反覆運算。  

此外，HSBN 及「入門範本」方案（Hyperledger Fabric 0.6 版）不支援非唯一性鏈碼，因為這會造成資料一致性及完整性的風險；如需詳細資料，請參閱[非唯一性鏈碼](nondeterministic.html)。
