---

copyright:
  years: 2016
lastupdated: "2016-08-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 共識測試 4：重新啟動拜占庭節點
{: #pbft_test1}


「共識測試 4」會測試四個節點中有一個已在成為拜占庭之後重新上線的網路情境中的 PBFT 通訊協定：一個節點在以任意且同時的方式離線之後重新啟動。

重新加入區塊鏈網路的先前拜占庭對等節點將會偵測到其分類帳副本落後其他對等節點的副本。落後的對等節點會自動從具有現行分類帳的對等節點複製遺漏的區塊，以更新其分類帳；此程序稱為狀態轉移。
{:shortdesc}

請注意，此測試案例需要大量 invoke 作業。對等節點會透過傳送內部*檢查點* 訊息，來彼此通知其現行分類帳狀態；落後的對等節點會藉由檢查這些訊息而判斷出它落後了。

在重新啟動一個拜占庭節點之後，請完成下列步驟來測試 PBFT：
1. 使用網路使用者 ID 及密碼登入：  
   a. 對 ***VP0 URL***/registrar 執行 POST  
   b. 執行以下有效負載：{“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”}  
   c.	對等節點傳回有效負載
2. 驗證網路已啟動且在執行：  
   a.	指定每一個對等節點的 URL，以查詢每一個對等節點的區塊鏈高度：  
   b. 執行 **GET ***VP0 URL***/chain**  
   c. 指令傳回以下有效負載：  
```json
{
"currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
   d. 如果這是區塊鏈的第一個作業，則鏈結高度是 1，因為鏈結上的唯一區塊是初始區塊。鏈結高度會隨著您將交易附加至分類帳而增加。
3. 部署鏈碼：  
   a.	對 ***VP0 URL***/chaincode 執行 POST  
   b. 使用以下有效負載：  
```json
 {
 "jsonrpc": "2.0",
 "method": "deploy",
 "params": {
 "type": 1,
 "chaincodeID":{
 "path":"github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02"
 },
 "ctorMsg": {
 "function":"init",
 "args": ["a", "1000", "b", "2000"]
 },
 "secureContext": "***test\_user1***"
 },
 "id": 1
 }
```
   c. 對等節點傳回以下有效負載：
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "YOUR_CHAINCODE_ID"
},
"id": 1
}
```
   d. 要求會傳輸至網路上的所有四個對等節點。對等節點會執行 PBFT 共識通訊協定、同意執行此要求，並將結果儲存至其各自的分類帳副本。  
   e. 所有交易都是非同步的。傳回有效負載包含將用於稍後鏈碼呼叫的鏈碼雜湊。
   f. deploy 作業的完成取決於處理器速度及網路延遲之類的因素。
  
4. 基於測試，請使用介面上的停止按鈕手動停止節點，模擬對等節點 VP2 以拜占庭（任意且同時）方式離線。
5. 在鏈碼上執行 invoke 作業：  
   a. 在此範例中，chaincode_example02 會將 1 個單位從 a 移至 b：  
   b. 使用以下有效負載，對 ***VP0 URL***/chaincode 執行 POST：
```json
{
"jsonrpc": "2.0",
"method": "invoke",
"params": {
"type": 1,
"chaincodeID":{
"name":"YOUR_CHAINCODE_ID"
},
"ctorMsg": {
"function":"invoke",
"args": ["a", "b", "1"]
}
"secureContext": "***test\_user1***"
},
"id": 2
}
```
  c. 對等節點傳回以下有效負載：
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
},
"id": 2
}
```
   d. 要求會再次傳輸至網路上的所有四個對等節點。對等節點會執行 PBFT 共識通訊協定、同意執行此要求，並將結果附加至其各自的分類帳副本。  
6. 此要求也是非同步的。短暫間隔之後，請確認已完成 invoke 作業：  
   a. 使用以下有效負載，對 ***VP0 URL***/chaincode 執行 POST：
```json
{
"jsonrpc": "2.0",
"method": "query",
"params": {
"type": 1,
"chaincodeID":{
"name":"YOUR_CHAINCODE_ID"
},
"ctorMsg": {
"function":"query",
"args":["a"]
}
"secureContext": "***test\_user1***"
},
"id": 3
}
```
   b. 對等節點傳回以下有效負載：
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "999"
},
"id": 3
}
```
   c. 如預期，"a" 的值等於或小於 1。
7. 使用介面上的啟動按鈕，手動重新啟動對等節點 **VP2**，模擬其再次上線。
8. 將 invoke 作業傳送至 VP0。
9. 查詢所有四個對等節點上的鏈碼值 "a"。所有對等節點都會傳回相同值 "a"。（**附註**：重新啟動的對等節點 (**VP2**) 順利執行 `stateTransfer` 函數所需的時間量取決於各種參數。請記住，PBFT 只需要 2f + 1 個對等節點，就可以達到共識。因此，可能需要大量的 invoke 作業，**VP2** 才能「趕上進度」，因為現行情況中並不需要它即可達成共識。如需此共識實作的相關資訊，請造訪 Linux Foundation 之 Hyperledger Project 中的 hyperledger/fabric [通訊協定規格](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1)。）

（共識測試 4 結束）
