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


# Tests des réseaux de blockchain
{: #etn_txn}


Utilisez les tests de rôles et de transactions suivants afin de confirmer la sécurité et la disponibilité du réseau de blockchain IBM. Tous les tests peuvent être menés à l'aide du plan Starter Developer ou du plan High Security Business Network.
{:shortdesc}

## Tests des rôles et des transactions
{: #sdk}

Le logiciel SDK HFC Hyperledger Fabric v0.6 pour Node.js
comporte des tests unitaires qui mettent en avant des fonctions de
sécurité, telles que l'impossibilité de relier des transactions et la
confidentialité. Vous pouvez découvrir ces tests unitaires à
l'adresse
https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/test/unit,
avec des exemples de code pour l'enregistrement et l'inscription
d'utilisateurs, le transfert d'actifs, et la gestion d'actifs à
l'aide de rôles utilisateur et d'attributs utilisateur. Les tests unitaires suivants sont disponibles :

### registrar.js
Le test registrar.js inscrit un utilisateur "admin" et désigne cet utilisateur en tant que `registraire` du réseau de blockchain. Ce test enregistre et inscrit également les utilisateurs additionnels "webAdmin" et "webUser". Le droit d'enregistrer des membres supplémentaires avec le rôle de 'client' est accordé à l'identité "webAdmin". Ce droit n'est pas accordé à l'identité "webUser". Lorsque "webAdmin" essaie d'enregistrer et d'inscrire des utilisateurs avec les rôles "auditeur" et "valideur", et lorsque "webUser" essaie d'enregistrer et d'inscrire "webUser2", la tentative échoue.

La capture d'écran ci-après illustre "webAdmin" qui est enregistré et inscrit, et défini en tant que `registraire` de la chaîne. L'utilisateur "webAdmin" enregistre et inscrit "webUser" :
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
 Cependant, "webAdmin" ne parvient pas à enregistrer et à inscrire un utilisateur en tant que "auditeur", car l'identité "webAdmin" est uniquement autorisée à enregistrer et à inscrire des membres avec le rôle de 'client' :
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
Dans la capture d'écran ci-après, "webUser" essaie d'enregistrer et d'inscrire "webUser2". La tentative échoue, car l'identité "webUser" n'a pas le droit d'inscrire des membres :
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
### chain-tests.js
Le test chain-test.js enregistre et inscrit un utilisateur test, comme implémenté par le réseau de blockchain `registrar`. Ce test illustre également le droit de l'utilisateur à `déployer (deploy)`, `appeler (invoke)`, et interroger (query) le code blockchain, ainsi qu'à interroger les variables d'état. Lorsque l'utilisateur test essaie d'interroger une fonction ou une variable non existante, un message d'erreur est retourné :  

L'utilisateur test crée une demande de déploiement avec le contenu suivant :
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
L'utilisateur test déclenche la transaction deploy :
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
L'utilisateur test crée une demande de requête avec le contenu suivant :
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
L'utilisateur test déclenche la transaction query :
```js
var queryTx = test_user_Member1.query(queryRequest);
```
La transaction query aboutit, car la fonction de code blockchain et les variables d'état sont valides :
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
L'utilisateur test crée une requête pour une fonction de code blockchain non existante, avec le contenu suivant :
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
L'utilisateur test déclenche la transaction query :
```js
var queryTx = test_user_Member1.query(queryRequest);
```
La transaction query échoue car fcn: "BOGUS" n'indique pas une fonction de code blockchain valide :
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
Le test asset-mgmt.js inscrit trois utilisateurs : Alice, Bob et Charlie. Dans ce test également, Alice déploie du code blockchain, puis appelle ce code blockchain pour affecter un actif à Bob. Bob appelle ensuite le même code blockchain pour transférer le même actif à Charlie. Une requête confirme la réussite du transfert d'actif.

Alice construit le contenu suivant pour transférer un actif (Ferrari) à l'utilisateur Bob, qui est représenté par son certificat d'enregistrement (eCert) bobAppCert :
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
Alice déclenche l'appel pour affecter l'actif à Bob :
```js
var tx = alice.invoke(invokeRequest);
```
Bob construit le contenu suivant pour transférer l'actif à l'utilisateur Charlie, qui est représenté par son certificat eCert charlieAppCert :
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
Bob déclenche l'appel pour affecter l'actif à Charlie :
```js
var tx = bob.invoke(invokeRequest);
```
Alice construit une requête avec le contenu suivant :
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
Alice déclenche la requête :
```js
var tx = alice.query(queryRequest);
```
Le propriétaire prévu de la Ferrari est Charlie, représenté dans le code par charlieAppCert. La requête va produire une réponse en échec si la requête sur "Ferrari" ne correspond pas au certificat utilisateur codé de Charlie :
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
### asset-mgmt-with-roles.js
Le test asset-mgmt-with-roles.js se développe à partir du scénario de transfert de propriété dans l'exemple `asset-mgmt.js`, en introduisant des rôles et des attributs utilisateur pour trois personnes : Alice, Bob et un attributeur. Le membre attributeur appelle le code blockchain et transfère avec succès un actif à Alice. Alice ne parvient pas à transférer ce même actif à Bob, car elle ne possède pas l'attribut d'attributeur. Une requête sur l'actif confirme la réussite du transfert par le membre attributeur, et l'échec du transfert par Alice.

L'"attributeur" affecte Alice (désignée par le certificat aliceCert) en tant que propriétaire d'un actif, lequel est défini dans le paramètre args en tant que "MyAsset" :
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
Alice essaie d'affecter Bob en tant que propriétaire de l'actif. La tentative échoue, car elle n'a pas émis le rôle 'attributeur' dans le fichier membersrvc.yaml :
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
Le test asset-mgmt-with-dynamic-roles.js est une variante du
test `asset-mgmt-with-roles.js`.  Dans le test
précédent, les utilisateurs Alice, Bob et l'attributeur sont inscrits
sur le réseau.  Toutefois, ces utilisateurs étaient auparavant
enregistrés avec des attributs codés en dur dans le fichier
membersrvc.yaml.  En d'autres termes, la fonction
`chain.enroll` a consigné ces utilisateurs sur le
réseau avec les attributs, affiliations et rôles correspondants du
fichier membersrvc.yaml ; la partie enregistrement a donc déjà été
effectuée.  

Dans ce test, nous voyons l'enregistrement et l'inscription
d'utilisateurs uniques (c'est-à-dire d'utilisateurs qui ne sont pas
déjà présents dans le fichier membersrvc.yaml). L'enregistrement et
l'inscription dynamiques s'effectuent via un rappel de la fonction
`registerAndEnroll`, comme illustré à la fin de ce
test :

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

Par exemple, nous pouvons voir que alice2 est enregistrée puis
inscrite avec deux attributs uniques : un 'rôle' (role) avec la
valeur 'client' et un 'compte' (account) avec la valeur
'aliceAccount'.

```js
console.log("enrolling alice2 ...");
         registerAndEnroll("alice2",[{name:'role',value:'client'},{name:'account',value:aliceAccount}], function(err,user) {
            if (err) return cb(err);
            alice = user;
```

Le reste du test est identique à celui du test
`asset-mgmt-with-roles.js`, avec Alice qui ne
parvient pas à affecter Bob en tant que propriétaire de l'actif.
