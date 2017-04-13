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


# Blockchain-Netze testen
{: #etn_txn}


Verwenden Sie die folgenden Rollen- und Transaktionstests zum Sicherstellen der Sicherheit und Verfügbarkeit in einem IBM Blockchain-Netz. Alle Tests können sowohl mit dem Starter-Entwicklerplan als auch mit dem Plan für ein Unternehmensnetzwerk mit hohem Sicherheitsniveau durchgeführt werden.
{:shortdesc}

## Rollen und Transaktionen testen
{: #sdk}

Das Hyperledger Fabric v0.6-HFC-SDK für Node.js enthält Komponententests, in denen der Schwerpunkt auf Sicherheitsfunktionen wie Datenschutz, Vertraulichkeit und Nichtverlinkbarkeit liegt. Sie können diese Komponententests unter 'https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/test/unit' erkunden, um Codebeispiele zum Registrieren und Eintragen von Benutzern, Übertragen von Assets und Verwalten von Assets mit Benutzerrollen und Benutzerattributen anzuzeigen. Die folgenden Komponententests sind verfügbar:

### registrar.js
Im Verlauf des registrar.js-Tests wird der Benutzer "admin" eingetragen und als `registrar` (Registrator) für das Blockchain-Netz angegeben. Außerdem werden in diesem Test noch die Benutzer "webAdmin" und "webUser" registriert und eingetragen. Der Identität "webAdmin" wird die Berechtigung zum Registrieren weiterer Mitglieder mit der Rolle 'client' erteilt. Der Identität "webUser" wird nicht die Berechtigung zum Registrieren weiterer Mitglieder erteilt. Wenn "webAdmin" versucht, Benutzer mit den Rollen "auditor" und "validator" zu registrieren und einzutragen, und wenn "webUser" versucht, "webUser2" zu registrieren und einzutragen, schlagen diese Versuche fehl.

In den folgenden Screenshots wird dargestellt, dass "webAdmin" registriert und eingetragen und als `registrar` (Registrator) für die Chain festgelegt wurde. Der Benutzer "webAdmin" registriert den Benutzer "webUser" und trägt ihn ein:
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
 Das Registrieren und Eintragen eines Benutzers als "auditor" durch den Benutzer "webAdmin" schlägt jedoch fehl, weil die Identität "webAdmin" nur zum Registrieren und Eintragen von Mitgliedern mit der Rolle 'client' berechtigt ist:
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
Im folgenden Screenshot versucht der Benutzer "webUser", den Benutzer "webUser2" zu registrieren und einzutragen. Der Versuch schlägt fehl, weil die Identität "webUser" nicht über die Berechtigung zum Eintragen von Mitgliedern verfügt:
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
### chain-tests.js
Im Verlauf des chain-test.js-Tests wird ein Testbenutzer, wie vom `registrar` des Blockchain-Netzes implementiert, registriert und eingetragen. Außerdem wird in diesem Test die Berechtigung des Testbenutzers für die Transaktionen `deploy` und `invoke` sowie zum Abfragen des Chaincodes und der Statusvariablen beschrieben. Wenn er Testbenutzer versucht, eine nicht vorhandene Funktion oder Variable abzufragen, wird eine Fehlernachricht zurückgegeben:  

Der Testbenutzer erstellt eine Bereitstellungsanforderung mit den folgenden Nutzdaten:
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
Vom Testbenutzer wird die Bereitstellungstransaktion ausgelöst:
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
Der Testbenutzer erstellt eine Abfrageanforderung mit den folgenden Nutzdaten:
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
Vom Testbenutzer wird die Abfragetransaktion ausgelöst:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
Die Abfragetransaktion ist erfolgreich, weil die Chaincode-Funktion und die Statusvariablen gültig sind:
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
Der Testbenutzer erstellt eine Abfrageanforderung für eine nicht vorhandene Chaincode-Funktion mit den folgenden Nutzdaten:
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
Vom Testbenutzer wird die Abfragetransaktion ausgelöst:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
Die Abfragetransaktion schlägt wegen fcn fehl: Von "BOGUS" wird keine gültige Chaincode-Funktion angegeben:
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
Im Verlauf des asset-mgmt.js-Tests werden die drei Benutzer Alice, Bob und Charlie eingetragen. Außerdem stellt Alice in diesem Test Chaincode bereit und ruft den Chaincode anschließend auf, um Bob ein Asset zuzuweisen. Anschließend ruft Bob denselben Chaincode auf, um dasselbe Asset an Charlie zu übertragen. Eine Abfrage bestätigt den erfolgreichen Assettransfer.

Alice erstellt die folgenden Nutzdaten, um ein Asset (Ferrari) an den Benutzer Bob zu übertragen, der mithilfe seines Eintragungszertifikats (eCert) bobAppCert dargestellt wird:
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
Alice löst den Aufruf für die Zuweisung des Assets an Bob aus:
```js
var tx = alice.invoke(invokeRequest);
```
Bob erstellt die folgenden Nutzdaten, um das Asset an den Benutzer Charlie zu übertragen, der mithilfe seines eCert 'charlieAppCert' dargestellt wird:
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
Bob löst den Aufruf für die Zuweisung des Assets an Charlie aus:
```js
var tx = bob.invoke(invokeRequest);
```
Alice erstellt eine Abfrage mit den folgenden Nutzdaten:
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
Alice löst die Abfrage aus:
```js
var tx = alice.query(queryRequest);
```
Der erwartete Besitzer des Ferrari ist Charlie, im Code durch charlieAppCert dargestellt. Die Abfrage führt zu einer fehlgeschlagenen Antwort, wenn die Abfrage für "Ferrari" nicht mit dem entsprechend codierten Benutzerzertifikat von Charlie übereinstimmmt.
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
### asset-mgmt-with-roles.js
Im Test asset-mgmt-with-roles.js wird das Szenario für die Eigentumsübertragung aus Beispiel `asset-mgmt.js` durch das Einführen von Rollen und Benutzerattributen für die drei Teilnehmer Alice, Bob und eine zuweisende Person erweitert. Das zuweisende Mitglied ruft den Chaincode auf und überträgt ein Asset erfolgreich an Alice. Die erfolgreiche Übertragung desselben Assets an Bob schlägt fehl, weil sie nicht über das Zuweiserattribut verfügt. Eine Abfrage für das Asset bestätigt die erfolgreiche Übergabe durch das zuweisende Mitglied und eine fehlgeschlagene Übertragung durch Alice.

Der "Zuweiser" weist Alice (angegeben durch aliceCert) das Eigentum an einem Assets zu, das im Argumentparameter als "MyAsset" definiert ist:
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
Alice versucht, Bob das Eigentum am Asset zuzuweisen. Der Versuch schlägt fehl, weil ihr in der Datei 'membersrvc.yaml' nicht die Rolle eines "Zuweisers" zugeordnet wurde:
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
Der asset-mgmt-with-dynamic-roles.js-Test ist eine Variante des `asset-mgmt-with-roles.js`-Tests.  Im vorherigen Test waren die Benutzer Alice und Bob sowie ein zuweisendes Mitglied (Zuweiser) im Netz eingetragen.  Diese Benutzer waren jedoch vorher mit Attributen in der Datei 'membersrvc.yaml' registriert, die fest codiert waren.  Diese Benutzer wurden also von der Funktion `chain.enroll` im Netz mit ihren jeweiligen Attributen, thematischen Zusammenhängen und Rollen in der Datei 'membersrvc.yaml' angemeldet; die Registrierung war somit schon abgeschlossen.  

In diesem Test wird die Registrierung und Eintragung eindeutiger Benutzer beschrieben (also Benutzer, die noch nicht in der Datei 'membersrvc.yaml' enthalten sind). Die dynamische Registrierung und Eintragung wird durch ein Callback der Funktion `registerAndEnroll` (wie am Ende dieses Tests dargestellt) durchgeführt:

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

Im Beispiel wird "alice2" mit zwei eindeutigen Attributen registriert und eingetragen: einer Rolle mit dem Wert 'client' und einem Konto mit dem Wert 'aliceAccount'.

```js
console.log("enrolling alice2 ...");
         registerAndEnroll("alice2",[{name:'role',value:'client'},{name:'account',value:aliceAccount}], function(err,user) {
            if (err) return cb(err);
            alice = user;
```

Der restliche Teil des Tests ist mit dem `asset-mgmt-with-roles.js`-Test identisch, in dem die Zuweisung von Alice an Bob als Eigner des Assets fehlschlägt.
