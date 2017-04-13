---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 共識測試 2：一個拜占庭節點
{: #pbft_test2}

前次更新：2016 年 8 月 4 日
{: .last-updated}

「共識測試 2」會測試四個節點中有一個為拜占庭的網路情境中的 PBFT 通訊協定：一個節點以任意且同時的方式離線。
{:shortdesc}

PBFT 通訊協定保證，如果不超過 (N-1)/3 個對等節點以拜占庭（任意且同時）方式離線，則具有 N 個對等節點的區塊鏈網路將繼續運作。您的 Bluemix 區塊鏈環境有四個對等節點，因此，如果其中一個對等節點損毀，則網路將繼續執行共識，並將交易附加至分類帳。套用 PBFT 公式時顯示 (4-1)/3 = 1 = 拜占庭節點數目，因此區塊鏈網路上的交易處理會繼續。

請完成下列步驟，以在具有一個拜占庭節點的四節點網路上測試 PBFT：
1.	使用網路使用者 ID 及密碼登入：  
    a.  對 ***VP0 URL***/registrar 執行 POST  
    b.  執行以下有效負載：{"enrollId": "***test\_user1***", enrollSecret": "***test\_user1\_enrollSecret***"}
    c.  對等節點傳回有效負載
2.  驗證網路已啟動且在執行：  
    a.  指定每一個對等節點的 URL，以查詢每一個對等節點的區塊鏈高度：  
    b   執行 GET ***VP0 URL***/chain  
     c.  指令傳回以下有效負載：
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
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
      "message":
      "YOUR_CHAINCODE_ID_RETURNED_HERE"
      },
      "id": 1
      }
      ```  
    d. 要求會傳輸至網路上的所有四個對等節點。對等節點會執行 PBFT 共識通訊協定、同意執行此要求，並將結果儲存至其各自的分類帳副本。  
    e.  請注意，所有交易都是非同步的。傳回有效負載包含將用於稍後鏈碼呼叫的鏈碼雜湊。  
    f.  部署的完成取決於處理器速度及網路延遲之類的因素。  
4.  基於測試，請使用介面上的停止按鈕，手動停止拜占庭節點 VP2 進行模擬。（**附註**：可能需要 30-60 秒，您的介面才會反映 VP2「已停止」。）
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
    d.  要求會再次傳輸至所有四個對等節點。對等節點會執行 PBFT 共識通訊協定、同意執行此要求，並將結果儲存至其各自的分類帳副本。
6.  此要求也是非同步的。短暫間隔之後，請在鏈碼上查詢 "a" 變數的值，以確認已完成 invoke 作業：  
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
      "message": "999"
      },
      "id": 3
      }
      ```
7.  如預期，原始部署鏈碼時，"a" 的值等於或小於 1。
8.  您可以繼續發出其他 invoke 及 query 作業。此程序與先前的步驟相同。

（共識測試 2 結束）
