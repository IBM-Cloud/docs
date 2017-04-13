---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 共識測試 1：沒有拜占庭節點
{: #pbft_test1}
前次更新：2016 年 8 月 4 日
{: .last-updated}

「共識測試 1」會測試四個節點都不是拜占庭的區塊鏈網路情境中的 PBFT 共識通訊協定：沒有任何節點以任意且同時的方式離線。
{:shortdesc}

啟動「開發人員網路」或「高安全性商業網路」之後，請完成下列步驟來測試沒有拜占庭節點的 PBFT：

（**附註**：程式碼 Snippet 及指令利用各種符號值。**VPO URL**、**"test_user1"**、**"test_user1_enrollSecret"** 及 **YOUR_CHAINCODE_ID** 都只是位置保留元。從網路主控台的 **API** 標籤中，存取**服務認證**及 **VP URL** 的文字值。將鏈碼部署至網路之後，**YOUR_CHAINCODE_ID** 的值會出現在**網路**標籤上。此外，JSON 回應有效負載中的雜湊值會與這些範例不同。）

1.	使用網路使用者 ID 及密碼登入：  
    a.  對 ***VP0 URL***/registrar 執行 POST  
    b.	執行以下有效負載：{“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”}  
    c.	對等節點傳回有效負載
2.	驗證網路已啟動且在執行：  
    a.	指定每一個對等節點的 URL，以查詢每一個對等節點的區塊鏈高度：  
    b.  執行 GET ***VP0 URL***/chain  
     c.  對等節點傳回以下有效負載：
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d.	如果這是區塊鏈的第一個作業，則鏈結高度是 1，因為鏈結上的唯一區塊是初始區塊。鏈結高度會隨著交易附加至分類帳而增加。
3.	部署鏈碼：  
    a.	對 ***VP0 URL***/chaincode 執行 POST  
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
       "52b0d803fc395b5e34d8d4a7cd69fb6aa00099b8fabed83504ac1c5d61a425aca5b3ad3bf96643ea4fdaac132c417c37b00f88fa800de7ece387d008a76d3586"
       },
       "id": 1
       }
       ```
    d. 要求會傳輸至網路上的所有四個對等節點。對等節點會執行 PBFT 共識通訊協定、同意執行此要求，並將結果儲存至其各自的分類帳副本。  
    e.	請注意，所有交易都是非同步的。傳回有效負載包含將用於稍後鏈碼呼叫的鏈碼雜湊。
4.  短暫間隔之後，請確認已完成 deploy 要求：  
    a.  依序指定每一個對等節點的 URL，以查詢每一個對等節點的區塊鏈高度：  
    b.  執行 GET ***VP0 URL***/chain  
     c.  指令傳回以下有效負載：
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
    d.  deploy 作業的完成取決於處理器速度及網路延遲之類的因素。
5.  既然您已部署鏈碼，就可以對鏈碼呼叫作業：  
    a.  使用 chaincode_example02，將 1 個單位從 a 移動至 b：  
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
6.  前一個要求是非同步的。短暫間隔之後，請從鏈碼查詢 "a" 變數的值，以確認已完成 invoke 作業：  
    a.  使用以下有效負載，POST 到 ***VP0 URL***/chaincode：
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
     c.  如預期，原始部署鏈碼時，"a" 的值等於或小於 1。請記住，指派給 "a" 的原始值為 1,000，而指派給 "b" 的原始值為 2,000。您在步驟 5 觸發的呼叫要求會導致正在將一個單位從 "a" 轉移給 "b"。
7.  您可以繼續發出 invoke 及 query 作業。此程序與先前的步驟相同。

  （共識測試 1 結束）
