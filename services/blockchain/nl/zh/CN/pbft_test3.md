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


# 共识测试 3：两个拜占庭节点
{: #pbft_test2}


共识测试 3 在一个网络场景中测试 PBFT 共识协议，在此场景中，四个节点中有两个是拜占庭节点：两个节点以任意且并发方式脱机了。
{:shortdesc}

PBFT 协议保证对于具有 N 个同级的区块链网络，如果不超过 (N-1)/3 个同级以拜占庭（任意且并发）方式脱机，那么该网络将继续正常运行。您的 Bluemix 区块链网络有四个同级，所以如果两个同级崩溃，那么网络不会执行任何交易，也不会将任何区块附加到分类帐。应用 PBFT 公式得到的结果是 (4-1)/3 = 1 < 拜占庭节点数 (2)，所以交易处理将停止。

完成以下步骤以在有两个拜占庭节点的四节点网络上测试 PBFT：
1.  使用您的网络用户标识和密码登录：  
    a.  运行 POST 操作以发布到 ***VP0 URL***/registrar  
    b.  运行有效内容 {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}  
    c.  同级返回有效内容
2.  验证网络是否已启动并正在运行：  
    a.  查询每个同级的区块链高度，并指定每个同级的 URL：  
    b.  运行 GET ***VP0 URL***/chain  
    c.  该命令返回有效内容：
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```
    d.  如果这是对区块链执行的第一个操作，那么链高度为 1，因为链上唯一的区块就是创始区块。随着交易附加到分类帐，链高度会增加。
3.  部署链代码：  
    a.  运行 POST 操作以发布到 ***VP0 URL***/chaincode  
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
      "message": "YOUR_CHAINCODE_ID"
      },
      "id": 1
      }
      ```
    d.  请求会传输到网络上的所有四个同级。这些同级运行 PBFT 共识协议，同意执行此请求并将结果附加到其各自的分类帐副本。  
    e.  请注意，所有交易都是异步的。返回有效内容只包含交易标识，这可在以后查询结果时使用。
4.  出于测试目的，通过界面的“停止”按钮手动停止节点 VP2 和 VP3，以模拟这两个节点使用拜占庭（任意且并发）方式转为脱机。（**注**：可能需要 30-60 秒，界面才会反映出 VP2 和 VP3“已停止”。）
5.  在链代码上运行 invoke 操作：  
    a.  对于此示例，chaincode_example02 将 1 个单元从 a 移至 b：  
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
    d.  由于网络未通过 f=(N-1)/3 PBFT 测试，因此 invoke 操作会作为输入接受，但不会得到执行，并且不会有任何内容附加到共享分类帐。
6.  通过查询“a”变量的值，验证 invoke 操作是否未执行：  
    a.  运行 POST 操作以发布到 ***VP0 URL***/chaincode，有效内容如下：
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
      "message": "1000"
      },
      "id": 3
      }
      ```
    c.  请注意，“a”的值保持不变。

  （共识测试 3 结束）
