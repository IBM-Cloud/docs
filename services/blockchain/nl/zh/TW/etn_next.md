---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 其他測試
{: #etn_next}


除非特別註明，否則已在「高安全性商業網路」環境中執行下列測試，以測試鏈碼函數、分類帳、長期執行、並行性及複合交易。在 LinuxONE OS 的安全服務容器內，已使用 VM 來賓身分執行驗證者及成員資格服務節點。下面使用的值是根據客戶輸入來選擇，因此不會誤會為最大值。（附註：在 [Node.js SDK](etn_txn.html) 及[測試共識及可用性](etn_pbft.html)小節中會重複其中部分測試。）

{:shortdesc}

1. 鏈碼函數 - 已執行鏈碼介面，確保 `Deploy`、`Invoke` 及 `Query` 交易能使用 REST API 及 CLI 正確運作。如「Hyperledger 通訊協定規格」中所述，已利用 REST API 及 CLI 來測試所有端點函數，包括 Block、Blockchain、Chaincode、Network、Registrar 及 Transactions。
2. 分類帳 - 根據不同的驅動環境，在分類帳中建立 20,000 筆 1K 有效負載的記錄。這些測試包括一個以序列化方式建立 20,000 筆記錄的用戶端。
3. 長期執行 - 此測試的進行，是使用 example02 展示鏈碼，在多個節點中傳送 invoke、鏈結高度及 query 達 72 個小時。
4. Node.js SDK - 使用了加強 Node.js SDK 來登錄及登記使用者，以及在處於開發模式的對等節點（使用 `peer node start –peer -chaincodedev` 啟動對等節點）及在處於網路模式的對等節點（使用 `peer node start` 啟動對等節點）上執行 deploy、invoke 和 query。
5. 基本並行 - 此測試的進行，是在 10 分鐘的期間內，以 1KB 有效負載傳送並行 invoke 給所有四個對等節點，並且測量鏈結高度以及查詢分類帳狀態。
6. 複合交易 - 此測試的進行，是在 10 分鐘的期間內，隨機混合將範圍從 10k 到 500K 之各種有效負載大小的 query 及 invoke 提交至對等節點。會測量鏈結高度及廣域狀態的查詢，以確保共用分類帳跨網路對等節點進行同步化。
