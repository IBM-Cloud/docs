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


# 共識測試 3：兩個拜占庭節點
{: #pbft_test2}


「共識測試 3」會測試四個節點中有兩個為拜占庭的網路情境中的 PBFT 共識通訊協定：兩個節點以任意且同時的方式離線。
{:shortdesc}

如果不超過 (N-1)/3 個對等節點以拜占庭（任意且同時）方式離線，則 PBFT 通訊協定保證具有 N 個對等節點的區塊鏈網路將繼續運作。您的 Bluemix 區塊鏈網路有四個對等節點，因此，如果兩個對等節點損毀，則網路不會執行任何交易，或不會將任何區塊附加至分類帳。套用 PBFT 公式時顯示 (4-1)/3 = 1 < 拜占庭節點數目 (2)，因此交易處理會停止。

請完成下列步驟，以在具有兩個拜占庭節點的四個節點網路上測試 PBFT：
1.  使用網路使用者 ID 及密碼登入：  
    a.  對 ***VP0 URL***/registrar 執行 POST  
    b.  執行以下有效負載：{“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}  
     c.  對等節點傳回有效負載
2.  驗證網路已啟動且在執行：  
    a.  指定每一個對等節點的 URL，以查詢每一個對等節點的區塊鏈高度：  
    b.  執行 GET ***VP0 URL***/chain  
     c.  指令傳回以下有效負載：
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```
    d.  如果這是區塊鏈的第一個作業，則鏈結高度是 1，因為鏈結上的唯一區塊是初始區塊。鏈結高度會隨著交易附加至分類帳而增加。
3.  部署鏈碼：  
    a.  對 ***VP0 URL***/chaincode 執行 POST  
    b.  使用以下有效負載：  
      ```
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
     c.  對等節點傳回以下有效負載：
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "YOUR_CHAINCODE_ID"
      },
      "id": 1
      }
      ```
    d.  要求會傳輸至網路上的所有四個對等節點。對等節點會執行 PBFT 共識通訊協定、同意執行此要求，並將結果附加至其各自的分類帳副本。  
    e.  請注意，所有交易都是非同步的。傳回的有效負載只包含交易 ID，以在稍後查詢結果時使用。
4.  基於測試，請使用介面上的停止按鈕手動停止節點 VP2 及 VP3，模擬它們以拜占庭（任意且同時）方式離線。（**附註**：可能需要 30-60 秒，您的介面才會反映 VP2 及 VP3「已停止」。）
5.  在鏈碼上執行 invoke 作業：  
    a.  在此範例中，chaincode_example02 會將 1 個單位從 a 移至 b：  
    b.  使用以下有效負載，對 ***VP0 URL***/chaincode 執行 POST：
      ```
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
     c.  對等節點傳回以下有效負載：
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
      },
      "id": 2
      }
      ```
    d.  因為網路無法通過 f=(N-1)/3 PBFT 測試，所以會將 invoke 作業接受為輸入，但不會執行，也不會將任何項目附加至共用分類帳。
6.  查詢 "a" 變數的值，以驗證未執行 invoke 作業：  
    a.  使用以下有效負載，對 ***VP0 URL***/chaincode 執行 POST：
      ```
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
      "args": ["a"]
      }
      "secureContext": "***test\_user1***"
      },
      "id": 3
      }
      ```
    b.  對等節點傳回以下有效負載：
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "1000"
      },
      "id": 3
      }
      ```
     c.  請注意，"a" 的值會保持不變。

  （共識測試 3 結束）
