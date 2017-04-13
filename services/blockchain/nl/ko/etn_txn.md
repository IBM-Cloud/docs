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


# 블록체인 네트워크 테스트
{: #etn_txn}


다음 역할 및 트랜잭션 테스트를 사용하여 IBM Blockchain 네트워크 보안 및 가용성을 확인할 수 있습니다. 모든 테스트는 스타터 개발자 플랜 또는 고급 보안 비즈니스 네트워크 플랜을 사용하여 수행될 수 있습니다.
{:shortdesc}

## 역할 및 트랜잭션 테스트
{: #sdk}

Hyperledger Fabric v0.6 HFC SDK for Node.js에는 개인정보 보호정책, 기밀성 및 비연결성 등의 보안 기능에 중점을 두는 단위 테스트가 포함되어 있습니다. https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/test/unit 페이지에서 이러한 단위 테스트를 탐색할 수 있으며 사용자 등록 및 등록접수, 자산 전송, 사용자 역할 및 사용자 속성으로 자산 관리 등과 같은 코드 예제를 확인할 수 있습니다. 다음의 단위 테스트를 사용할 수 있습니다. 

### registrar.js
registrar.js 테스트는 "admin" 사용자를 등록접수하며, 해당 사용자를 블록체인 네트워크 `registrar`로 지정합니다. 또한 이 테스트는 추가 사용자 "webAdmin" 및 "webUser"를 등록하고 등록접수합니다. "webAdmin" ID에는 '클라이언트' 역할로 추가 멤버를 등록하는 권한이 부여되어 있습니다. "webUser" ID에는 추가 멤버를 등록하는 권한이 부여되어 있지 않았습니다. "webAdmin"이 "감사자" 및 "유효성 검증자" 역할의 사용자를 등록하고 등록접수하려고 시도하고, "webUser"가 "webUser2"를 등록하고 등록접수하려고 시도하면 해당 시도가 실패합니다. 

다음 스크린샷은 "webAdmin"이 등록되고 등록접수되었으며 체인 `registrar`로서 설정되었음을 표시합니다. "webAdmin" 사용자는 "webUser"를 성공적으로 등록하고 등록접수합니다. 
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
그러나 "webAdmin" ID에는 '클라이언트' 역할의 멤버를 등록하고 등록접수하는 권한만 있으므로 "webAdmin"은 사용자를 "감사자"로 등록하고 등록접수하는 데 실패합니다.
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
다음 스크린샷에서 "webUser"는 "webUser2"를 등록하고 등록접수하려고 시도합니다. "webUser" ID에는 멤버를 등록접수할 권한이 없으므로 해당 시도는 실패합니다.
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
### chain-tests.js
블록체인 네트워크 `registrar`에서 구현한 대로, chain-test.js 테스트는 테스트 사용자를 등록하고 등록접수합니다. 이 테스트는 체인코드 배치, 호출 및 조회와 상태 변수 조회를 위한 테스트 사용자의 권한도 표시합니다. 존재하지 않는 함수 또는 변수를 테스트 사용자가 조회하려고 시도하면 오류 메시지가 리턴됩니다.   

테스트 사용자가 다음 페이로드로 배치 요청을 생성합니다. 
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
테스트 사용자가 배치 트랜잭션을 트리거합니다.
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
테스트 사용자가 다음 페이로드로 조회 요청을 생성합니다.
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
테스트 사용자가 조회 트랜잭션을 트리거합니다.
```js
var queryTx = test_user_Member1.query(queryRequest);
```
체인코드 함수 및 상태 변수가 유효하므로 조회 트랜잭션에 성공합니다.
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
테스트 사용자가 다음 페이로드로 존재하지 않는 체인코드 함수에 대한 조회를 생성합니다.
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
테스트 사용자가 조회 트랜잭션을 트리거합니다.
```js
var queryTx = test_user_Member1.query(queryRequest);
```
fcn: "BOGUS"가 올바른 체인코드 함수를 지정하지 않으므로 조회 트랜잭션이 실패합니다.
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
asset-mgmt.js 테스트는 세 사용자 Alice, Bob 및 Charlie를 등록접수합니다. 이 테스트에는 Alice 배치 체인코드도 있으며, 자산을 Bob에 지정하는 체인코드를 호출합니다. 그리고 Bob은 동일한 체인코드를 호출하여 동일한 자산을 Charlie에게 전송합니다. 조회가 성공적인 자산 전송을 확인합니다. 

Alice는 자신의 등록접수 인증서(eCert) bobAppCert로 표시되는 사용자 Bob에게 자산(Ferrari)을 전송하기 위해 다음 페이로드를 생성합니다. 
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
Alice는 자산을 Bob에게 지정하는 호출을 트리거합니다.
```js
var tx = alice.invoke(invokeRequest);
```
Bob은 자신의 eCert charlieAppCert로 표시되는 사용자 Charlie에게 자산을 전송하기 위해 다음 페이로드를 생성합니다.
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
Bob은 자산을 Charlie에게 지정하는 호출을 트리거합니다.
```js
var tx = bob.invoke(invokeRequest);
```
Alice는 다음 페이로드로 조회를 생성합니다.
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
Alice는 조회를 트리거합니다.
```js
var tx = alice.query(queryRequest);
```
Ferrari의 예상 소유자는 charlieAppCert로 코드에서 표시되는 Charlie입니다. "Ferrari"에 대한 조회가 Charlie의 인코딩된 사용자 인증서에 대응되지 않는 경우, 조회는 실패한 응답을 생성합니다.
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
### asset-mgmt-with-roles.js
asset-mgmt-with-roles.js 테스트는 세 사람(Alice, Bob 및 지정자)에 대한 역할 및 사용자 속성을 도입하여 `asset-mgmt.js` 예제의 소유권 전송 시나리오를 부연 설명합니다. 지정자 멤버는 체인코드를 호출하며 성공적으로 자산을 Alice에게 전송합니다. 지정자 속성을 보유하지 않으므로, Alice는 성공적으로 동일 자산을 Bob을 전송하는 데 실패합니다. 자산에 대한 조회는 지정자 멤버의 전송 성공과 Alice의 전송 실패를 확인합니다. 

"지정자"는 Alice(aliceCert로 지정됨)를 args 매개변수에서 "MyAsset"으로 정의되어 있는 자산의 소유자로 지정합니다. 
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
Alice는 Bob을 자산의 소유자로서 지정하려고 시도합니다. membersrvc.yaml 파일에서 '지정자' 역할이 발행되지 않았으므로, 이 시도는 실패합니다.
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
asset-mgmt-with-dynamic-roles.js 테스트는 `asset-mgmt-with-roles.js`의 변형입니다. 이전 테스트에서는 사용자 Alice, Bob 및 지정자가 네트워크에 등록접수됨을 표시합니다. 그러나 이러한 사용자는 membersrvc.yaml에 하드코드화된 속성으로 이전에 등록되었습니다. 다시 말하면, `chain.enroll` 함수는 이 사용자를 대응되는 속성, 소속 및 membersrvc.yaml의 역할로 네트워크에 로깅합니다. 등록 부분은 이미 발생했습니다.   

이 테스트에서는 고유 사용자(즉, membersrvc.yaml에 아직 없는 사용자)의 등록 및 등록접수가 표시됩니다. 동적 등록 및 등록접수는 이 테스트의 마지막에 표시된 대로 `registerAndEnroll` 함수의 콜백을 통해 수행됩니다. 

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

예를 들어, alice2가 두 개의 고유 속성('클라이언트" 값의 '역할" 및 'aliceAccount' 값의 '계정")으로 등록되고 등록접수됨을 볼 수 있습니다. 

```js
console.log("enrolling alice2 ...");
         registerAndEnroll("alice2",[{name:'role',value:'client'},{name:'account',value:aliceAccount}], function(err,user) {
            if (err) return cb(err);
            alice = user;
```

테스트의 나머지는 `asset-mgmt-with-roles.js`와 동일하며, Alice는 Bob을 자산의 소유자로 지정할 수 없습니다. 
