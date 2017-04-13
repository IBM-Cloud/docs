---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 共识测试 1：无拜占庭节点
{: #pbft_test1}
上次更新时间：2016 年 8 月 4 日
{: .last-updated}

共识测试 1 在一个区块链网络场景中测试 PBFT 共识协议，在此场景中，四个节点均不是拜占庭节点：所有节点都未曾以任意且并发方式脱机。
{:shortdesc}

启动“开发者网络”或“高安全性业务网络”后，完成以下步骤来测试没有拜占庭节点的 PBFT：

（**注**：代码片段和指令使用了各种符号值。**VPO URL**、**"test_user1"**、**"test_user1_enrollSecret"** 和 **YOUR_CHAINCODE_ID** 只是占位符。在网络控制台上，访问 **API** 选项卡中**服务凭证**和 **VP URL** 的字面值。一旦将一段链代码部署到网络，**YOUR_CHAINCODE_ID** 的值就会显示在**网络**选项卡上。此外，JSON 响应有效内容中的散列值将与这些示例中的不同。）

1.	使用您的网络用户标识和密码登录：  
    a.  运行 POST 操作以发布到 ***VP0 URL***/registrar  
    b.	运行有效内容 {“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”}  
    c.	同级返回有效内容
2.	验证网络是否已启动并正在运行：  
    a.	查询每个同级的区块链高度，并指定每个同级的 URL：  
    b.  运行 GET ***VP0 URL***/chain  
    c.  同级返回有效内容：
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d.	如果这是对区块链执行的第一个操作，那么链高度为 1，因为链上唯一的区块就是创始区块。随着交易附加到分类帐，链高度会增加。
3.	部署链代码：  
    a.	运行 POST 操作以发布到 ***VP0 URL***/chaincode  
    b.  有效内容如下：  
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
     c.  同级返回有效内容：  
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
    d. 请求会传输到网络上的所有四个同级。这些同级运行 PBFT 共识协议，同意执行此请求并将结果存储在其各自的分类帐副本上。  
    e.	请注意，所有交易都是异步的。返回有效内容包含链代码散列，您将在以后的链代码调用中使用。
4.  稍等片刻后，检查部署请求是否已完成：  
    a.  查询每个同级的区块链高度，并依次指定每个同级的 URL：  
    b.  运行 GET ***VP0 URL***/chain  
    c.  该命令返回有效内容：
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
    d.  部署操作的完成依赖于多种因素，例如处理器速度和网络等待时间。
5.  现在您已部署链代码，可以在链代码上调用操作：  
    a.  使用 chaincode_example02，将 1 个单元从 a 移至 b：  
    b.  运行 POST 操作以发布到 ***VP0 URL***/chaincode，有效内容如下：
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
      “secureContext”: “***test\_user1***”
      },
      "id": 2
      }
      ```
    c.  同级返回有效内容：
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
    d.  请求会再次传输到所有四个同级。这些同级运行 PBFT 共识协议，同意执行此请求并将结果存储在其各自的分类帐副本上。
6.  先前的请求是异步的。稍等片刻后，通过查询链代码中“a”变量的值来检查 invoke 操作是否已完成：  
    a.  执行 POST 操作以发布到 ***VP0 URL***/chaincode，有效内容如下：
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
      “secureContext”: “***test\_user1***”
      },
      "id": 3
      }
      ```   
    b.  同级返回有效内容：
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
    c.  如预期那样，“a”的值比最初部署链代码时的值小 1。别忘了，分配给“a”的原始值为 1,000，分配给“b”的原始值为 2,000。在步骤 5 中触发的调用请求导致一个单元从“a”传输到“b”。
7.  可以继续发出 invoke 和 query 操作。该过程与先前的步骤相同。

  （共识测试 1 结束）
