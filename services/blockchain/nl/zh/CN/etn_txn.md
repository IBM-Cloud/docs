---

copyright:
  years: 2016
lastupdated: "2016-11-03"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 测试区块链网络
{: #etn_txn}


使用以下角色和交易测试来确定 IBM Blockchain 网络的安全性和可用性。可以使用“入门模板开发者”套餐或“高安全性业务网络”套餐来执行所有测试。
{:shortdesc}

## 测试角色和交易
{: #sdk}

Hyperledger Fabric V0.6 HFC SDK for Node.js 包含的单元测试着重于安全功能，例如隐私性、机密性和不可链接性。您可以在 https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/test/unit 上探索这些单元测试，以了解用于通过用户角色和用户属性注册和登记用户、转移资产以及管理资产的代码示例。提供了以下单元测试：

### registrar.js
registrar.js 测试将登记“admin”用户，并将该用户指定为区块链网络 `registrar`。此测试还将注册并登记额外的用户“webAdmin”和“webUser”。将授权“webAdmin”身份注册具有角色“client”的额外成员。但不会授权“webUser”身份来注册额外成员。“webAdmin”尝试注册并登记具有“auditor”（审计员）和“validator”（验证者）角色的用户，并且“webUser”尝试注册并登记“webUser2”时，这些尝试会失败。

以下屏幕快照显示了“webAdmin”已注册并登记，并已设置为链 `registrar`。“webAdmin”用户成功注册并登记了“webUser”：
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
但是，“webAdmin”未能将用户注册并登记为“auditor”，因为“webAdmin”身份仅有权注册并登记具有角色“client”的成员：
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
在以下屏幕快照中，“webUser”尝试注册并登记“webUser2”。该尝试失败，因为“webUser”身份无权登记成员：
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
### chain-tests.js
chain-test.js 测试将注册并登记测试用户，这由区块链网络 `registrar` 实现。此测试还将显示测试用户`部署`、`调用`和查询链代码的权限，以及查询状态变量的权限。测试用户尝试查询不存在的函数或变量时，会返回一条错误消息：  

测试用户使用以下有效内容构造部署请求：
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
测试用户触发部署交易：
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
测试用户使用以下有效内容构造查询请求：
```js
var queryRequest = {
        // Name (hash) required for query
        chaincodeID: testChaincodeID,
        // Function to trigger
        fcn: "query",
        // Existing state variable to retrieve
        args: ["a"]
    };
```
测试用户触发查询交易：
```js
var queryTx = test_user_Member1.query(queryRequest);
```
查询交易成功，因为链代码函数和状态变量有效：
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
测试用户使用以下有效内容，为不存在的链代码函数构造查询：
```js
 var queryRequest = {
        // Name (hash) required for query
        chaincodeID: testChaincodeID,
        // Function to trigger
        fcn: "BOGUS",
        // Existing state variable to retrieve
        args: ["a"]
    };
```
测试用户触发查询交易：
```js
var queryTx = test_user_Member1.query(queryRequest);
```
查询交易失败，因为 fcn: "BOGUS" 未指定有效的链代码函数：
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
asset-mgmt.js 测试将登记三个用户：Alice、Bob 和 Charlie。此测试还让 Alice 部署链代码，然后调用该链代码以向 Bob 分配资产。随后，Bob 调用相同的链代码以将相同资产转移给 Charlie。查询确认资产转移成功。

Alice 构造以下有效内容以将资产 (Ferrari) 转移给用户 Bob，Bob 由其登记证书 (eCert) bobAppCert 表示：
```js
var invokeRequest = {
        // Name (hash) required for invoke
        chaincodeID: testChaincodeID,
        // Function to trigger
        fcn: "assign",
        // Parameters for the invoke function
        args: ['Ferrari', bobAppCert.encode().toString('base64')],
        confidential: true,
        userCert: alicesCert
    };
```
Alice 触发调用以将资产分配给 Bob：
```js
var tx = alice.invoke(invokeRequest);
```
Bob 构造以下有效内容以将该资产转移给用户 Charlie，Charlie 由其 eCert（即 charlieAppCert）表示：
```js
var invokeRequest = {
        // Name (hash) required for invoke
        chaincodeID: testChaincodeID,
        // Function to trigger
        fcn: "transfer",
        // Parameters for the invoke function
        args: ['Ferrari', charlieAppCert.encode().toString('base64')],
        userCert: bobAppCert,
        confidential: true
    };
```
Bob 触发调用以将资产分配给 Charlie：
```js
var tx = bob.invoke(invokeRequest);
```
Alice 使用以下有效内容构造查询：
```js
var queryRequest = {
        // Name (hash) required for query
        chaincodeID: testChaincodeID,
        // Function to trigger
        fcn: "query",
        // Existing state variable to retrieve
        args: ["Ferrari"],
        confidential: true
    };
```
Alice 触发查询：
```js
var tx = alice.query(queryRequest);
```
期望的 Ferrari 所有者是 Charlie，在代码中由 charlieAppCert 表示。如果对“Ferrari”的查询与 Charlie 的已编码用户证书不对应，那么查询将生成失败的响应：
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
### asset-mgmt-with-roles.js
asset-mgmt-with-roles.js 测试通过引入 Alice、Bob 和 assigner 这三个人的角色和用户属性，扩展了 `asset-mgmt.js` 示例中的所有权转移场景。assigner 成员调用链代码，并成功将资产转移给 Alice。Alice 未能成功将该相同资产转移给 Bob，因为她并不拥有 assigner 属性。对资产的查询确认，assigner 成员的转移成功，而 Alice 的转移失败。

“assigner”将 Alice（由 aliceCert 指定）分配为资产所有者，这在自变量参数中定义为“MyAsset”：
```js
alice.getUserCert(["role", "account"], function (err, aliceCert) {
        if (err) fail(t, "Failed getting Application certificate for Alice.");
        assignOwner(assigner, aliceCert.encode().toString('base64'), function(err) {
            if (err) {
                t.fail("error: "+err.toString());
            } else {
                checkOwner(assigner, aliceAccount, function(err) {
                    if(err){
                        t.fail("error: "+err.toString());
                    } else {
                        t.pass("assign successful");
                    }
                });
            }
```
Alice 尝试将 Bob 分配为该资产的所有者。该尝试失败，因为在 membersrvc.yaml 文件中没有为 Alice 分配“assigner”角色：
```js
 bob.getUserCert(["role", "account"], function (err, bobCert) {
        if (err) fail(t, "Failed getting Application certificate for Alice.");
        assignOwner(alice, bobCert.encode().toString('base64'), function(err) {
            if (err) {
                t.fail("error: "+err.toString());
            } else {
                checkOwner(alice, bobAccount, function(err) {
                    if(err){
                        t.pass("assign successful");
                    } else {
                        err = new Error ("this user should not have been allowed to assign");
                        t.fail("error: "+err.toString());
                    }
                });
            }
```

### asset-mgmt-with-dynamic-roles
asset-mgmt-with-dynamic-roles.js 测试是 `asset-mgmt-with-roles.js` 的变体。上一个测试显示用户 Alice、Bob 和 assigner 被登记到网络中。但是，这些用户先前已经使用 membersrvc.yaml 中硬编码的属性进行过注册。换句话说，`chain.enroll` 函数已使这些用户通过 membersrvc.yaml 中自己的对应属性、亲缘关系和角色登录到网络；注册部分已经执行。  

在此测试中，我们将看到非重复用户（即，membersrvc.yaml 中尚不存在的用户）的注册和登记。动态注册和登记是通过回调 `registerAndEnroll` 函数来完成的，如此测试末尾所示：

```js
function registerAndEnroll(name, attrs, cb) {
    console.log("registerAndEnroll name=%s attrs=%j",name,attrs);
    var registrationRequest = {
         roles: [ 'client' ],
         enrollmentID: name,
         affiliation: "bank_a",
         attributes: attrs
    };
    chain.registerAndEnroll(registrationRequest,cb);
}
```

例如，我们看到 alice2 被使用以下两个非重复属性进行注册和登记：值为“client”的“role”和值为“aliceAccount”的“account”。

```js
console.log("enrolling alice2 ...");
         registerAndEnroll("alice2",[{name:'role',value:'client'},{name:'account',value:aliceAccount}], function(err,user) {
            if (err) return cb(err);
            alice = user;
```

此测试的其余部分与 `asset-mgmt-with-roles.js` 相同，其中 Alice 未能将 Bob 分配为资产的所有者。
