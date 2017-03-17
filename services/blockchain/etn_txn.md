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


# Testing blockchain networks
{: #etn_txn}


Use the following roles and transactions tests to confirm IBM Blockchain network security and availability. All tests can be conducted using the Starter Developer plan or the High Security Business Network plan.
{:shortdesc}

## Testing roles and transactions
{: #sdk}

The Hyperledger Fabric v0.6 HFC SDK for Node.js contains unit tests that highlight security features such as privacy, confidentiality and unlinkability. You can explore these unit tests at https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/test/unit to see code examples for registering and enrolling users, transferring assets, and managing assets with user roles and user attributes. The following unit tests are available:

### registrar.js
The registrar.js test enrolls an "admin" user and designates that user as the blockchain network `registrar`. This test also registers and enrolls the additional users "webAdmin" and "webUser". The "webAdmin" identity is granted authority to register additional members with the role of 'client'. The "webUser" identity is not granted authority to register  additional members. When "webAdmin" attempts to register and enroll users with the "auditor" and "validator" roles, and when "webUser" attempts to register and enroll "webUser2", the attempts fail.

The following screenshot shows that "webAdmin" is registered and enrolled, and set as the chain `registrar`. The "webAdmin" user successfully registers and enrolls "webUser":
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
 However, "webAdmin" fails to register and enroll a user as "auditor", because the "webAdmin" identity is only authorized to register and enroll members with the role of 'client':
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
In the following screenshot, "webUser" attempts to register and enroll "webUser2". The attempt fails, because the "webUser" identity not have authority to enroll members:
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
### chain-tests.js
The chain-test.js test registers and enrolls a test user, as implemented by the blockchain network `registrar`. This test also shows the test user's authority to `deploy`, `invoke`, and query chaincode, and to query state variables. When the test user attempts to query a non-existing function or variable, an error message is returned:  

The test user constructs a deploy request with the following payload:
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
The test user triggers the deploy transaction:
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
The test user constructs a query request with the following payload:
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
The test user triggers the query transaction:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
The query transaction succeeds, because the chaincode function and state variables are valid:
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
The test user constructs a query for a non-existing chaincode function, with the following payload:
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
The test user triggers the query transaction:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
The query transaction fails because fcn: "BOGUS" does not specify a valid chaincode function:
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
The asset-mgmt.js test enrolls three users: Alice, Bob, and Charlie. This test also has Alice deploy chaincode, and then invoke the chaincode to assign an asset to Bob. Bob then invokes the same chaincode to transfer the same asset to Charlie. A query confirms the successful asset transfer.

Alice constructs the following payload to transfer an asset (Ferrari) to user Bob, who is represented by his enrollment certificate (eCert) bobAppCert:
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
Alice triggers the invoke to assign the asset to Bob:
```js
var tx = alice.invoke(invokeRequest);
```
Bob constructs the following payload to transfer the asset to user Charlie, who is represented by his eCert charlieAppCert:
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
Bob triggers the invoke to assign the asset to Charlie:
```js
var tx = bob.invoke(invokeRequest);
```
Alice constructs a query with following payload:
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
Alice triggers the query:
```js
var tx = alice.query(queryRequest);
```
The expected owner of the Ferrari is Charlie, represented in the code by charlieAppCert. The query will produce a failed response if the query against "Ferrari" does not correspond to Charlie's encoded user certificate:
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
### asset-mgmt-with-roles.js
The asset-mgmt-with-roles.js test expands on the transfer of ownership scenario in the `asset-mgmt.js` example, by introducing roles and user attributes for three personas: Alice, Bob and assigner. The assigner member invokes the chaincode and successfully transfers an asset to Alice. Alice fails to successfully transfer the same asset to Bob, because she does not own the assigner attribute. A query on the asset confirms the successful transfer by the assigner member, and a failed transfer by Alice.

The "assigner" assigns Alice (designated by aliceCert) as the owner of an asset, which is defined in the args parameter as "MyAsset":
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
Alice attempts to assign Bob as the owner of the asset. The attempt fails, because she has not been issued the role of 'assigner' in the membersrvc.yaml file:
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
The asset-mgmt-with-dynamic-roles.js test is a variation of `asset-mgmt-with-roles.js`.  The prior test shows the users Alice, Bob, and assigner being enrolled to the network.  However, these users were previously registered with attributes hardcoded in the membersrvc.yaml.  In other words, the `chain.enroll` function logged these users into the network with their corresponding attributes, affiliations, and roles from the membersrvc.yaml; the registration portion had already occurred.  

In this test we see the registration and enrollment of unique users (i.e. users not already present in the membersrvc.yaml). The dynamic registration and enrollment is done through a callback of the `registerAndEnroll` function, as seen at the end of this test:

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

For example, we see alice2 being registered and enrolled with two unique attributes: a 'role' with the value of 'client' and an 'account' with the value of 'aliceAccount'.

```js
console.log("enrolling alice2 ...");
         registerAndEnroll("alice2",[{name:'role',value:'client'},{name:'account',value:aliceAccount}], function(err,user) {
            if (err) return cb(err);
            alice = user;
```

The remainder of the test is the same as `asset-mgmt-with-roles.js`, with Alice failing to assign Bob as the owner of the asset.
