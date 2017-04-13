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


# 測試區塊鏈網路
{: #etn_txn}


使用下列角色及交易測試，以確認 IBM Blockchain 的網路安全及可用性。所有測試都可以使用「入門範本開發人員」方案或「高安全性商業網路」方案進行處理。
{:shortdesc}

## 測試角色及交易
{: #sdk}

Hyperledger Fabric 0.6 版 HFC SDK for Node.js 包含可強調安全特性（例如隱私權、機密性及不可鏈結性）的單元測試。您可以探索 https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/test/unit 上的這些單元測試，以查看用於登錄和登記使用者、轉移資產以及利用使用者角色和使用者屬性來管理資產的程式碼範例。下列是可用的單元測試：

### registrar.js
registrar.js 測試會登記 "admin" 使用者，並將該使用者指定為區塊鏈網路 `registrar`。此測試也會登錄及登記其他使用者 "webAdmin" 及 "webUser"。"webAdmin" 身分會獲授與登錄具有 'client' 角色之其他成員的權限。"webUser" 身分不會獲授與登錄其他成員的權限。若 "webAdmin" 嘗試登錄及登記具有 "auditor" 及 "validator" 角色的使用者，以及 "webUser" 嘗試登錄及登記 "webUser2"，則嘗試會失敗。

下列擷取畫面顯示已登錄及登記 "webAdmin"，並且設為鏈結 `registrar`。"webAdmin" 使用者已順利登錄及登記 "webUser"：
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
 不過，"webAdmin" 無法將使用者登錄及登記為 "auditor"，因為 "webAdmin" 身分僅獲授權登錄及登記具有 'client' 角色的成員：
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
在下列擷取畫面中，"webUser" 嘗試登錄及登記 "webUser2"。嘗試失敗，因為 "webUser" 身分沒有登記成員的權限：
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
### chain-tests.js
chain-test.js 測試會登錄及登記測試使用者，如區塊鏈網路 `registrar` 所實作。此測試也會顯示測試使用者部署、呼叫及查詢鏈碼的權限，以及查詢狀態變數的權限。測試使用者嘗試查詢不存在的函數或變數時，會傳回錯誤訊息：  

測試使用者使用下列有效負載建構 deploy 要求：
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
測試使用者觸發 deploy 交易：
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
測試使用者使用下列有效負載建構 query 要求：
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
測試使用者觸發 query 交易：
```js
var queryTx = test_user_Member1.query(queryRequest);
```
query 交易成功，因為鏈碼函數及狀態變數有效：
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
測試使用者使用下列有效負載建構對於不存在之鏈碼函數的查詢：
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
測試使用者觸發 query 交易：
```js
var queryTx = test_user_Member1.query(queryRequest);
```
query 交易失敗，因為 fcn: "BOGUS" 未指定有效的鏈碼函數：
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
asset-mgmt.js 測試登記三位使用者：Alice、Bob 及 Charlie。此測試也會讓 Alice 部署鏈碼，然後呼叫鏈碼將資產指派給 Bob。Bob 接著會呼叫相同的鏈碼，將相同的資產轉移給 Charlie。查詢會確認已成功轉移資產。

Alice 建構下列有效負載，以將資產 (Ferrari) 轉移給使用者 Bob，使用者 Bob 以他的登記憑證 (eCert) bobAppCert 表示：
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
Alice 觸發 invoke，以將資產指派給 Bob：
```js
var tx = alice.invoke(invokeRequest);
```
Bob 建構下列有效負載，以將資產轉移給使用者 Charlie，使用者 Charlie 以他的 eCert charlieAppCert 表示：
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
Bob 觸發 invoke，以將資產指派給 Charlie：
```js
var tx = bob.invoke(invokeRequest);
```
Alice 使用下列有效負載建構 query：
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
Alice 觸發 query：
```js
var tx = alice.query(queryRequest);
```
Ferrari 的預期擁有者是程式碼中以 charlieAppCert 表示的 Charlie。如果針對 "Ferrari" 的查詢未對應至 Charlie 的編碼使用者憑證，則查詢將產生失敗的回應：
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
### asset-mgmt-with-roles.js
asset-mgmt-with-roles.js 測試詳述 `asset-mgmt.js` 範例中的所有權轉移情境，方法是引進三位人員的角色及使用者屬性：Alice、Bob 及 assigner。assigner 成員呼叫 chaincode，並將資產順利轉移給 Alice。Alice 無法順利將相同的資產轉移給 Bob，因為她未擁有 assigner 屬性。對資產的查詢確認由 assigner 成員成功轉移，但 Alice 轉移失敗。

"assigner" 將 Alice（由 aliceCert 指定）指派為資產擁有者，這在 args 參數中定義為 "MyAsset"：
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
Alice 嘗試將 Bob 指派為資產擁有者。嘗試失敗，因為尚未在 membersrvc.yaml 檔案中將 'assigner' 角色發送給她：
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
asset-mgmt-with-dynamic-roles.js 測試是 `asset-mgmt-with-roles.js` 的變異。先前測試顯示正在將使用者 Alice、Bob 及 assigner 登記至網路。不過，先前已使用寫在 membersrvc.yaml 中的屬性來登錄這些使用者。換言之，`chain.enroll` 函數已使用這些使用者在 membersrvc.yaml 中的對應屬性、連結及角色，將他們登入網路；登錄部分已經發生過。  

在此測試中，我們看到登錄及登記唯一使用者（亦即，membersrvc.yaml 中還沒有該些使用者）。動態登錄及登記是透過回呼 `registerAndEnroll` 函數所完成，如這個測試的結尾所示：

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

例如，我們看到將使用兩個唯一屬性來登錄及登記 alice2：值為 'client' 的 'role'，及值為 'aliceAccount' 的 'account'。

```js
console.log("enrolling alice2 ...");
         registerAndEnroll("alice2",[{name:'role',value:'client'},{name:'account',value:aliceAccount}], function(err,user) {
            if (err) return cb(err);
            alice = user;
```

測試的其餘部分與 `asset-mgmt-with-roles.js` 相同，但 Alice 無法將 Bob 指派為資產擁有者。
