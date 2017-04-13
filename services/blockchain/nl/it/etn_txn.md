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


# Esecuzione di test di reti blockchain
{: #etn_txn}


Utilizza i seguenti test di transazioni e ruoli per confermare la sicurezza e la disponibilità di rete di IBM Blockchain. Tutti i test possono essere eseguiti utilizzando il piano Starter Developer oppure il piano High Security Business Network.
{:shortdesc}

## Esecuzione di test di ruoli e transazioni
{: #sdk}

L'HFC SDK per Node.js di Hyperledger Fabric v0.6 contiene i test d'unità che evidenziano le funzioni di sicurezza quali la privacy, la confidenzialità e la non collegabilità. Puoi esplorare questi test d'unità all'indirizzo https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/test/unit per visualizzare degli esempi di codice per la registrazione e il completamento della registrazione degli utenti, per il trasferimento di risorse e per la gestione di risorse con ruoli utente e attributi utente. Sono disponibili i seguenti test d'unità:

### registrar.js
Il test registrar.js registra un utente "admin" e lo indica come `registrar` (conservatore del registro) della rete blockchain. Questo test esegue anche la registrazione e il completamento della registrazione degli utenti aggiuntivi "webAdmin" e "webUser". All'identità "webAdmin" viene concessa l'autorizzazione a registrare ulteriori membri con il ruolo di 'client'. All'identità "webUser" non viene concessa l'autorizzazione a registrare ulteriori membri. Quando "webAdmin" prova ad eseguire la registrazione e il completamento della registrazione di utenti con i ruoli "auditor" e "validator" e quando "webUser" prova ad eseguire la registrazione e il completamento della registrazione di "webUser2", i tentativi hanno esito negativo.

Il seguente screenshot mostra che per "webAdmin" sono state eseguite la registrazione e il completamento della registrazione ed è stato impostato come `registrar` (conservatore del registro) della catena. L'utente "webAdmin" esegue correttamente la registrazione e il completamento della registrazione di "webUser":
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
 Tuttavia, "webAdmin" non riesce a registrare e a completare la registrazione di un utente come "auditor", perché l'identità "webAdmin" è autorizzata solo a registrare e completare la registrazioni di membri con il ruolo di 'client':
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin potrebbe non registrare il membro di tipo auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
Nel seguente screenshot, "webUser" prova a registrare e a completare la registrazione di "webUser2". Il tentativo non riesce perché l'identità "webUser" non dispone dell'autorizzazione per completare la registrazione di membri:
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("a webUser non dovrebbe essere consentito di registrare un client"));
  expect="webUser non può registrare un membro di tipo client";
```
### chain-tests.js
Il test chain-test.js registra e completa la registrazione di un utente del test, come implementato dal `registrar` della rete blockchain. Questo test mostra anche l'autorizzazione dell'utente del test ad eseguire distribuzioni (`deploy`), richiami (`invoke`) e query del chaincode e ad eseguire query delle variabili di stato. Quando l'utente del test prova ad eseguire una query di una funzione o di una variabile inesistente, viene restituito un messaggio di errore:  

L'utente del test crea una richiesta di distribuzione con il seguente payload:
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
L'utente del test attiva la transazione di distribuzione:
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
L'utente del test crea una richiesta di query con il seguente payload:
```js
var queryRequest = {
        // Nome (hash) richiesto per la query
        chaincodeID: testChaincodeID,
        // Funzione da attivare
        fcn: "query",
        // Variabile di stato esistente da richiamare
        args: ["a"]
    };
```
L'utente del test attiva la transazione di query:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
La transazione di query ha esito positivo perché la funzione chaincode e le variabili di stato sono valide:
```js
t.pass(util.format("Query dello stato del chaincode esistente eseguita con esito positivo: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
L'utente del test crea una query per una funzione chaincode inesistente con il seguente payload:
```js
 var queryRequest = {
        // Nome (hash) richiesto per la query
        chaincodeID: testChaincodeID,
        // Funzione da attivare
        fcn: "BOGUS",
        // Variabile di stato esistente da richiamare
        args: ["a"]
    };
```
L'utente del test attiva la transazione di query:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
La transazione di query ha esito negativo poiché fcn: "BOGUS" non specifica una funzione chaincode valida:
```js
t.pass(util.format("Impossibile eseguire la query della funzione chaincode inesistente: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
Il test asset-mgmt.js completa la registrazione di tre utenti: Alice, Bob e Charlie. Questo test vede anche Alice distribuire il chaincode e richiamarlo quindi per assegnare una risorsa a Bob. Bob richiama quindi lo stesso chaincode per trasferire la stessa risorsa a Charlie. Una query conferma quindi il corretto trasferimento della risorsa.

Alice crea il seguente payload per trasferire una risorsa (Ferrari) all'utente Bob, che è rappresentato dal suo certificato di registrazione completata (eCert) bobAppCert:
```js
var invokeRequest = {
        // Nome (hash) richiesto per richiamare
        chaincodeID: testChaincodeID,
        // Funzione da attivare
        fcn: "assign",
        // Parametri per la funzione di richiamo
        args: ['Ferrari', bobAppCert.encode().toString('base64')],
        confidential: true,
        userCert: alicesCert
    };
```
Alice attiva il richiamo per assegnare la risorsa a Bob:
```js
var tx = alice.invoke(invokeRequest);
```
Bob crea il seguente payload per trasferire la risorsa all'utente Charlie, che è rappresentato dal suo eCert charlieAppCert:
```js
var invokeRequest = {
        // Nome (hash) richiesto per richiamare
        chaincodeID: testChaincodeID,
        // Funzione da attivare
        fcn: "transfer",
        // Parametri per la funzione di richiamo
        args: ['Ferrari', charlieAppCert.encode().toString('base64')],
        userCert: bobAppCert,
        confidential: true
    };
```
Bob attiva il richiamo per assegnare la risorsa a Charlie:
```js
var tx = bob.invoke(invokeRequest);
```
Alice crea una query con il seguente payload:
```js
var queryRequest = {
        // Nome (hash) richiesto per eseguire la query
        chaincodeID: testChaincodeID,
        // Funzione da attivare
        fcn: "query",
        // Variabile di stato esistente da richiamare
        args: ["Ferrari"],
        confidential: true
    };
```
Alice attiva la query:
```js
var tx = alice.query(queryRequest);
```
Il proprietario previsto della Ferrari è Charlie, rappresentato nel codice da charlieAppCert. La query produrrà una risposta non riuscita se la query su "Ferrari" non corrisponde al certificato utente codificato di Charlie:
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie non è il proprietario della risorsa.")
        }
```
### asset-mgmt-with-roles.js
Il test asset-mgmt-with-roles.js sviluppa ulteriormente lo scenario di trasferimento di proprietà nell'esempio `asset-mgmt.js` introducendo i ruoli e gli attributi utente per tre persone: Alice, Bob e l'assegnatore. Il membro assegnatore richiama il chaincode e trasferisce correttamente una risorsa ad Alice. Alice non riesce a trasferire correttamente la stessa risorsa a Bob perché non possiede l'attributo di assegnatore. Una query sulla risorsa conferma il corretto trasferimento da parte del membro assegnatore e un trasferimento non riuscito da parte di Alice.

L'"assegnatore" assegna Alice (designata da aliceCert) come proprietaria di una risorsa, che è definita nel parametro args come "MyAsset":
```js
alice.getUserCert(["role", "account"], function (err, aliceCert) {
        if (err) fail(t, "Impossibile ottenere il certificato Application per Alice.");
        assignOwner(assigner, aliceCert.encode().toString('base64'), function(err) {
            if (err) {
                t.fail("errore: "+err.toString());
            } else {
                checkOwner(assigner, aliceAccount, function(err) {
                    if(err){
                        t.fail("errore: "+err.toString());
                    } else {
                        t.pass("assegnazione eseguita correttamente");
                    }
                });
            }
```
Alice prova ad assegnare Bob come proprietario della risorsa. Il tentativo non riesce perché non le è stato assegnato il ruolo di assegnatore (assigner) nel file membersrvc.yaml:
```js
 bob.getUserCert(["role", "account"], function (err, bobCert) {
        if (err) fail(t, "Impossibile ottenere il certificato Application per Alice.");
        assignOwner(alice, bobCert.encode().toString('base64'), function(err) {
            if (err) {
                t.fail("errore: "+err.toString());
            } else {
                checkOwner(alice, bobAccount, function(err) {
                    if(err){
                        t.pass("assegnazione eseguita correttamente");
                    } else {
                        err = new Error ("a questo utente non dovrebbe essere stata consentita l'assegnazione");
                        t.fail("errore: "+err.toString());
                    }
                });
            }
```

### asset-mgmt-with-dynamic-roles
Il test asset-mgmt-with-dynamic-roles.js è una variazione di `asset-mgmt-with-roles.js`.  Il test precedente mostra il completamento della registrazione degli utenti Alice, Bob e dell'assegnatore alla rete.  Tuttavia, tali utenti erano stati precedentemente registrati con gli attributi codificati (hardcoded) in membersrvc.yaml.  In altre parole, la funzione `chain.enroll` ha registrato questi utenti nella rete con i loro attributi, affiliazioni e ruoli corrispondenti da membersrvc.yaml; la parte di registrazione aveva già avuto luogo.  

In questo test, vediamo la registrazione e il completamento della registrazione di utenti univoci (ossia utenti non già presenti in membersrvc.yaml). La registrazione e il completamento della registrazione in modo dinamico vengono eseguiti tramite una richiamata della funzione `registerAndEnroll`, come si vede alla fine di questo test:

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

Ad esempio, vediamo che si sta eseguendo il completamento della registrazione di alice2 con due attributi univoci: un 'role' con il valore di 'client' e un 'account' con il valore di'aliceAccount'.

```js
console.log("completamento della registrazione di alice2 in corso ...");
         registerAndEnroll("alice2",[{name:'role',value:'client'},{name:'account',value:aliceAccount}], function(err,user) {
            if (err) return cb(err);
            alice = user;
```

Il resto del test è uguale a `asset-mgmt-with-roles.js`, e vede Alice che non riesce ad assegnare Bob come proprietario della risorsa.
