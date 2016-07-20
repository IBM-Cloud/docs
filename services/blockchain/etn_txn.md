---
 
copyright:
years: 2016
 
---
 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
 
 
# Testing blockchain networks
{: #etn_txn}
 
*Last updated: 19 July 2016*
{: .last-updated}

Use the tests laid forth in this section to affirm important security features and network availability.
{:shortdesc}

## Testing roles and transactions
{: #sdk}

The Node SDK module contains several unit tests that highlight security features such as privacy, confidentiality and unlinkability. Explore the unit tests located in the `/test/unit` directory to see code examples for registering and enrolling users, transferring assets, and managing assets with user roles and user attributes.  

* `registrar.js` - Demonstrates the enrollment of an "admin" user and designating that user as the chain `registrar`.  The test also shows the registration and enrollment of two additional users: "webAdmin" and "webUser".  During registration, "webAdmin" is given the authority to register members with the role of 'client', and "webUser" is not given any authority to register any additional members.  This is demonstrated in the test when "webAdmin" attempts to register and enroll an "auditor" and "validator"; and when "webUser" attempts to register and enroll "webUser2".  Both registration and enrollment attempts will fail.

"webAdmin" is registered and enrolled, and set as the chain `registrar`.  He successfully registers and enrolls "webUser":
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
 However, "webAdmin" fails to register and enroll "auditor", because he can only register and enroll members with the role of 'client':
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
 "webUser" attempts to register and enroll "webUser2".  This fails because he does not have the authority to enroll any members:
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
* `chain-tests.js` - Demonstrates the registration and enrollment of a test user by a chain `registrar` member.  The test also shows the ability of the test user to `deploy` a chaincode, `invoke` a chaincode function, and then `query` existing chaincode functions and state variables.  If the user attempts a query on a non-existing function or variable, an error will be generated.  

Test user constructs a deploy request with the following payload:
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
Test user triggers the deploy transaction:
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
Test user constructs a query request with the following payload:
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
Test user triggers the query transaction:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
The test passes, and he receives a successful response, because the chaincode function and state variables are valid:
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
The test user queries against a non-existing chaincode function with the following payload:
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
He triggers the query transaction:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
The test passes, and in doing so produces a failed response.  The failure response is generated because "BOGUS" is not a valid chaincode function:
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
* `asset-mgmt.js` - Demonstrates the enrollment of three users: Alice, Bob, and Charlie.   The test then demonstrates Alice deploying a chaincode and subsequently invoking it to assign an asset to Bob.  Bob then invokes the same chaincode to assign the same asset to Charlie, and a query is performed to confirm a successful asset transfer.  

Alice constructs the following payload to transfer an asset (Ferrari) to user Bob, who is represented by his user certificate - bobAppCert:
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
Alice triggers the invoke:
```js
var tx = alice.invoke(invokeRequest);
```
Bob constructs the following payload to transfer the Ferrari to user Charlie, who is represented by his user certificate - charlieAppCert:
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
Bob triggers the invoke:
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
The expected owner of the Ferrari is Charlie, represented in the code by charlieAppCert.  The query will produce a failed response if the query against "Ferrari" does not correspond to Charlie's encoded user certificate:
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
* `asset-mgmt-with-roles.js` - Expands on the transfer of ownership scenario demonstrated in the `asset-mgmt.js` example, by introducing roles and user attributes for three personas: Alice, Bob and assigner.  The assigner member invokes the chaincode to successfully transfer an asset to Alice, given his assigner attribute.  Alice, however, fails to successfully transfer the same asset to Bob, as she does not have the assigner attribute.  A query on the asset confirms the successful transfer by the asssigner member and a failed transfer by Alice. 

The "assigner" assigns Alice (designated by aliceCert) as the owner of an asset defined in the args parameter as "MyAsset":
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
Alice attempts to assign Bob as the owner of the asset.  This will fail because she has not been issued the member role of assigner in the membersrvc.yaml file:
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
