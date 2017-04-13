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


# 共识测试 4：重新启动拜占庭节点
{: #pbft_test1}


共识测试 4 在一个网络场景中测试 PBFT 协议，在此场景中，四个节点之一在成为拜占庭节点后已恢复联机：一个节点在以任意且并发方式脱机后已重新启动。


先前成为拜占庭节点的一个同级后来重新联接了区块链网络，它将检测到其分类帐副本滞后于其他同级的分类帐副本。滞后的同级会通过从具有当前分类帐的同级复制缺少的区块来自动更新自己的分类帐；此过程称为状态转移。
{:shortdesc}

请注意，此测试用例需要大量 invoke 操作。同级通过发送内部*检查点*消息，相互通知其当前的分类帐状态；滞后的同级通过检查这些消息即可确定自己是否滞后。

完成以下步骤以在重新启动一个拜占庭节点后测试 PBFT：
1. 使用您的网络用户标识和密码登录：  
   a. 运行 POST 操作以发布到 ***VP0 URL***/registrar  
   b. 运行有效内容 {“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”}  
    c.	同级返回有效内容
2. 验证网络是否已启动并正在运行：  
    a.	查询每个同级的区块链高度，并指定每个同级的 URL：  
   b. 运行 **GET ***VP0 URL***/chain**  
   c. 命令返回有效内容：  
```json
{
"currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
   d.	如果这是对区块链执行的第一个操作，那么链高度为 1，因为链上唯一的区块就是创始区块。随着交易附加到分类帐，链高度会增加。
3. 部署链代码：  
    a.	运行 POST 操作以发布到 ***VP0 URL***/chaincode  
   b. 有效内容如下：  
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
   c. 同级返回有效内容：
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
   d. 请求会传输到网络上的所有四个同级。这些同级运行 PBFT 共识协议，同意执行此请求并将结果存储在其各自的分类帐副本上。  
   e.	所有交易都是异步的。返回有效内容包含链代码散列，您将在以后的链代码调用中使用。
   f. 部署操作的完成依赖于多种因素，例如处理器速度和网络等待时间。
  
4. 出于测试目的，通过界面的“停止”按钮手动停止同级 VP2，以模拟此节点使用拜占庭（任意且并发）方式转为脱机。
5. 在链代码上运行 invoke 操作：  
   a. 对于此示例，chaincode_example02 将 1 个单元从 a 移至 b：  
   b. 运行 POST 操作以发布到 ***VP0 URL***/chaincode，有效内容如下：
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
“secureContext”: “***test\_user1***”
},
"id": 2
}
```
  c. 同级返回有效内容：
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
   d. 请求会再次传输到网络上的所有四个同级。这些同级运行 PBFT 共识协议，同意执行此请求并将结果附加到其各自的分类帐副本。  
6. 此请求也是异步的。稍等片刻后，检查 invoke 操作是否已完成：  
   a. 运行 POST 操作以发布到 ***VP0 URL***/chaincode，有效内容如下：
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
“secureContext”: “***test\_user1***”
},
"id": 3
}
```
   b. 同级返回有效内容：
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
   c. 如预期那样，“a”的值小于或等于 1。
7. 通过使用界面中的“启动”按钮手动重新启动同级 **VP2**，以模拟此同级恢复联机。
8. 向 VP0 发送 invoke 操作。
9. 查询所有四个同级上“a”的链代码值。所有同级针对“a”返回的值均相同。（**注**：重新启动的同级 (**VP2**) 成功执行 `stateTransfer` 功能所需的时间长度根据多个参数而定。别忘了，PBFT 只需要 2f + 1 个同级即可达成共识。因此，**VP2** 可能需要执行大量 invoke 操作才能“赶上”，因为在当前情况下不需要 VP2 即可达成共识。请访问 Linux Foundation 的 Hyperledger 项目中的 hyperledger/fabric [协议规范](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1)，以获取有关此共识实现的更多信息。）

（共识测试 4 结束）
