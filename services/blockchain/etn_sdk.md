---
 
copyright:
years: 2016
 
---
 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
 
 
# Enhanced Node.js SDK
{: #etn_sdk}
 
*Last updated: 13 July 2016*
{: .last-updated}

The enhanced Node.js SDK allows application developers to build Node.js applications that can interact with an existing blockchain.  These include the abilities to:
{:shortdesc}

* Securely register and enroll users. A web application adminstrator with `registrar` authority can dynamically register and enroll other users who have already authenticated to the web application. 
* Issue transactions to the blockchain - deploy, invoke, and query.  These transactions are anonymous and unlinkable. 
* Store sensitive private keys and certificates in any location of your choice, such as a database.  This requires implementing a simple key-value store interface. 
 
The client SDK provides APIs through which an application can interact with a Hyperledger blockchain, and those APIs are designed to support two pluggable components.

1. Pluggable key value store that is used to retrieve and store keys associated with a member. For example, call the `chain.setKeyValStore()` method to override the default file-based key value store implementation.
2. Pluggable member service that is used to register and enroll members. For example, call the `chain.setMemberServices()` method to override the default implementation in `MemberServices`.


You can include the SDK in your Node.js app in one of the following ways:
*  offline: You need to copy the files from the Hyperledger source tree: https://github.com/hyperledger/fabric/tree/master/sdk/node/lib into the `/lib` directory of the Node.js app.  Subsequently include it with the following code snippet:
```js
var hlc = require("./lib/hlc");
```

* npm:  Install the SDK from npm with the first snippet, then include it with the second code snippet:
```
npm install hfc -g
```

```js
var hlc = require('hlc');
```

## Web Application
The following example demonstrates a basic web application.  It shows how to register and enroll an identity, and how to use that identity to deploy, invoke and query.  For the full example, with commented out documentation, visit the [SDK README](https://github.com/hyperledger/fabric/blob/master/sdk/node/README.md#learn-by-example). 

From your service dashboard, click your **Service Credentials** tab to access the VCAP data for your peers, certificate authority and users.  Use the code snippets below to bind your peers and users to an application.  For example, to bind your Certificate Authority to this application you use the "ca" URL which can be accessed within your **Service Credentials** tab, and implement the following:  *(Note: This is a sample "ca" URL, yours will not be the same)*.

```js
chain.setMemberServicesUrl("grpc://904bd229-5a3e-407f-8a5d-819dc6205e16_ca-api.stage.blockchain.ibm.com:30303")
```

Explore the remainder of the application to see member enrollment, issuing of transaction requests, and other SDK capabilities.

```js
// Include the package from npm:
var hlc = require('hlc');

// Create a client chain.
var chain = hlc.newChain("targetChain");

// Configure the KeyValStore which is used to store sensitive keys
// as so it is important to secure this storage.
chain.setKeyValStore( hlc.newFileKeyValStore('/tmp/keyValStore') );

// Set the URL for member services
chain.setMemberServicesUrl("grpc://localhost:50051");

// Add a peer's URL
chain.addPeer("grpc://localhost:30303");

// Enroll "WebAppAdmin" which is already registered because it is
// listed in fabric/membersrvc/membersrvc.yaml with it's one time password.
chain.enroll("WebAppAdmin", "DJY27pEnl16d", function(err, webAppAdmin) {
   if (err) return console.log("ERROR: failed to register %s: %s",err);
   // Set this user as the chain's registrar which is authorized to register other users.
   chain.setRegistrar(webAppAdmin);
   // Begin listening for web app requests
   listenForUserRequests();
});

// Main web app function to listen for and handle requests
function listenForUserRequests() {
   for (;;) {
      // WebApp-specific logic goes here to await the next request.
      // ...
      // Assume that we received a request from an authenticated user
      // 'userName', and determined that we need to invoke the chaincode
      // with 'chaincodeID' and function named 'fcn' with arguments 'args'.
      handleUserRequest(userName,chaincodeID,fcn,args);
   }
}

// Handle a user request
function handleUserRequest(userName, chaincodeID, fcn, args) {
   // Register and enroll this user.
   var registrationRequest = {
        enrollmentID: userName,
        // Customize account & affiliation
        account: "bank_a",
        affiliation: "00001"
   };
   chain.registerAndEnroll( registrationRequest, function(err, user) {
      if (err) return console.log("ERROR: %s",err);
      // Issue an invoke request
      var invokeRequest = {
        // Name (hash) required for invoke
        chaincodeID: chaincodeID,
        // Function to trigger
        fcn: fcn,
        // Parameters for the invoke function
        args: args
     };
     // Invoke the request from the user object.
     var tx = user.invoke(invokeRequest);
     // Listen for the 'submitted' event
     tx.on('submitted', function(results) {
        console.log("submitted invoke: %j",results);
     });
     // Listen for the 'complete' event.
     tx.on('complete', function(results) {
        console.log("completed invoke: %j",results;
     });
     // Listen for the 'error' event.
     tx.on('error', function(err) {
        console.log("error on invoke: %j",err);
     });
   });
}
``` 


## Public and Private Keys
{: #keys}

The Hyperledger fabric makes use of Certificate Authorities and the underlying concepts of public and private keys as mechanisms to address security requirements for businesses operating on a shared blockchain.  These include: identity management, role management, and transactional privacy; and these can be fully controlled through the client SDK.

User and transactional privacy concerns are managed through the implementation of a PKI (Public Key Infrastructure) framework.  The PKI consists of various certificate authorites, and manages the generation, distribution and revocation of keys and digital certificates.  The basic tenets of the Hyperledger fabric's PKI are explained below.  For the complete technical specifications on PKI and Membership Services, see the security section in the Hyperledger fabric [protocol specification](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md).  

1. A user is registered through a Registration Authority (RA), which validates the identity of a user requesting to participate in the blockchain.  This can be done dynamically by a user with `registrar` authority, or manually by editing the membersrvc.yaml file.  Upon registration, the RA provides a set of enrollment credentials - `<enrollID>` and `<enrollPWD>`.  
2. The user then sends an enrollment request to the Enrollment Certificate Authority.  This payload contains the user's registration credentials, along with with the user's public key.  The ECA subsequently signs the certificate with his private key and produces what is know as a message digest.  The message digest is a cryptographic hash generated through the SHA3 hashing algorithm.   The returned certificate is referred to as an eCert.  They are static and long-term and can be either visible or invisible to transactions. 
3. In order to transact on the network, the user also needs transaction certificates (tCerts).  The user submits a certificate request with his `<enrollID>` to the Transaction Certificate Authority for a batch of tCerts.  The TCA communicates with the ECA and validates that the supplied `<enrollID>` has been issued a valid eCert.  After validation, the user is supplied with a batch of tCerts and a KeyDF_Key (Key Derivation Function Key).  The KDF_Key allows for the user to derive his private keys.  While the single KeyDF_Key is used for each tCert in the batch, the ensuing private key that is generated is unique to each tCert.  A client must have a supply of tCerts in order to transact, and furthermore he must be able to sign the transaction payload with the decrypted private key.  Only then is a transaction forwarded to validators for consensus.  A tCert is short-term and specific to each transaction.  A client is also able to control features of the tCerts, such as batch size and attributes, through an API.  


