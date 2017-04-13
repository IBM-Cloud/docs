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


# ブロックチェーン・ネットワークのテスト
{: #etn_txn}


IBM Blockchain ネットワーク・セキュリティーと可用性を確認するには、次の役割とトランザクションのテストを使用します。テストはすべて、Starter Developer プランまたは High Security Business Network プランを使用して実行できます。
{:shortdesc}

## 役割とトランザクションのテスト
{: #sdk}

Node.js 用の Hyperledger Fabric v0.6 HFC SDK には、プライバシーや機密性、非連結性などのセキュリティー機能をハイライトする単体テストが含まれています。これらの単体テストは https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/test/unit で探すことができます。ここには、ユーザー役割やユーザー属性を使用してユーザーの登録とエンロールを行ったり、資産を移譲したり、資産を管理したりするコード・サンプルがあります。入手可能な単体テストは、次のとおりです。

### registrar.js
registrar.js テストは、"admin" ユーザーをエンロールし、そのユーザーをブロックチェーン・ネットワーク `registrar` として指定します。このテストは、追加のユーザー "webAdmin" や "webUser" も登録およびエンロールします。"webAdmin" の ID には、追加メンバーに 'client' の役割を登録する権限が付与されています。"webUser" の ID には、追加メンバーを登録する権限が付与されていません。"webAdmin" がユーザーに "auditor" や "validator" の役割を登録およびエンロールしようとしたり、"webUser" が "webUser2" を登録およびエンロールしようとしたりすると、その試行は失敗します。

以下のスクリーン・ショットは、"webAdmin" が登録およびエンロールされ、チェーン `registrar` として設定されることを示しています。"webAdmin" ユーザーは "webUser" を正常に登録およびエンロールします。
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
ただし、"webAdmin" は、ユーザーを "auditor" として登録およびエンロールすることができません。"webAdmin" の ID には、'client' の役割を持つメンバーだけを登録およびエンロールすることだけが許可されているからです。
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
以下のスクリーン・ショットでは、"webUser" は "webUser2" の登録とエンロールを試行しています。"webUser" の ID にはメンバーをエンロールする権限がないため、この試行は失敗します。
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
### chain-tests.js
ブロックチェーン・ネットワーク `registrar` によって実装されると、chain-test.js テストはテスト・ユーザーを登録およびエンロールします。また、このテストは、チェーンコードをデプロイしたり、呼び出したり、照会したり、状態変数を照会したりするためのテスト・ユーザーの権限を表示します。存在していない関数または変数の照会をテスト・ユーザーが試行すると、エラー・メッセージが返されます。  

テスト・ユーザーは、以下のペイロードでデプロイ要求を構成します。
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
テスト・ユーザーは、デプロイ・トランザクションをトリガーします。
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
テスト・ユーザーは、以下のペイロードで照会要求を構成します。
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
テスト・ユーザーは、照会トランザクションをトリガーします。
```js
var queryTx = test_user_Member1.query(queryRequest);
```
チェーンコード関数と状態変数が有効なので、照会トランザクションは成功します。
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
テスト・ユーザーは、以下のペイロードで、存在していないチェーンコード関数の照会を構成します。
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
テスト・ユーザーは、照会トランザクションをトリガーします。
```js
var queryTx = test_user_Member1.query(queryRequest);
```
fcn: "BOGUS" は有効なチェーン関数を指定していないので、照会トランザクションは失敗します。
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
asset-mgmt.js テストは、3 人のユーザー Alice、Bob、Charlie をエンロールします。このテストには Alice デプロイ・チェーンコードも含まれており、その後、資産を Bob に割り振るチェーンコードを呼び出します。その後、Bob は、同じチェーンコードを呼び出して、同じ資産を Charlie に移譲します。照会は、資産の移譲が成功したことを確認します。

Alice は、以下のペイロードを構成し、資産 (Ferrari) をユーザー Bob に移譲します。Bob は、登録証明書 (eCert) bobAppCert によって表されます。
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
Alice は、呼び出しをトリガーして、資産を Bob に割り当てます。
```js
var tx = alice.invoke(invokeRequest);
```
Bob は、以下のペイロードを構成し、資産をユーザー Charlie に移譲します。Charlie は、eCert charlieAppCert によって表されます。
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
Bob は、呼び出しをトリガーして、資産を Charlie に割り当てます。
```js
var tx = bob.invoke(invokeRequest);
```
Alice は、以下のペイロードで照会を構成します。
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
Alice は照会をトリガーします。
```js
var tx = alice.query(queryRequest);
```
Ferrari の予期される所有者は Charlie です。これは、コードで charlieAppCert によって表されます。"Ferrari" に対する照会が Charlie のエンコードされたユーザー証明書に対応しない場合、照会は失敗応答を生成します。
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
### asset-mgmt-with-roles.js
asset-mgmt-with-roles.js テストは、`asset-mgmt.js` の例の所有権の移譲シナリオを拡張したものです。Alice、Bob、割り当て者の 3 人に役割とユーザー属性が導入されています。割り当て者メンバーは、チェーンコードを呼び出し、資産を正常に Alice に移譲します。Alice には割り当て者属性がないため、同じ資産を Bob に正常に移譲できません。資産の照会は、割り当て者メンバーによる移譲の成功と、Alice による移譲の失敗を確認します。

"assigner" は Alice (aliceCert によって指定される) を資産の所有者として割り当てます。これは、args パラメーターで "MyAsset" として定義されます。
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
Alice は、Bob を資産の所有者として割り当てようとします。Alice には membersrvc.yaml ファイルで 'assigner' の役割が発行されていないので、この試行は失敗します。
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
asset-mgmt-with-dynamic-roles.js テストは、`asset-mgmt-with-roles.js` の変化形の 1 つです。前のテストでは、ユーザー Alice、Bob、および割り当て者がネットワークにエンロールされていました。しかし、これらのユーザーには membersrvc.yaml でハードコーディングされた属性が登録されていました。言い換えると、`chain.enroll` 関数は、これらのユーザーが membersrvc.yaml にあるその対応する属性、所属、役割でネットワークにログインするようにします。登録の部分は既に行われています。  

このテストでは、固有のユーザーの登録とエンロールが示されています (つまり、ユーザーは membersrvc.yaml にはまだ存在していません)。このテストの最後にあるように、動的な登録とエンロールが `registerAndEnroll` 関数のコールバックによって行われます。

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

例えば、ここでは alice2 が 2 つの固有の属性 ('role' は 'client' という値、'account' は 'aliceAccount' という値) で登録およびエンロールされています。

```js
console.log("enrolling alice2 ...");
         registerAndEnroll("alice2",[{name:'role',value:'client'},{name:'account',value:aliceAccount}], function(err,user) {
            if (err) return cb(err);
            alice = user;
```

テストの残りは `asset-mgmt-with-roles.js` と同じですが、Alice は Bob を資産の所有者として割り当てることができません。
