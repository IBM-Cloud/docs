---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Testando redes de blockchain
{: #etn_txn}
Última atualização: 07 de outubro de 2016
{: .last-updated}

Use os testes de funções e transações a seguir para confirmar a segurança e disponibilidade de rede do IBM Blockchain. Todos os testes podem ser realizados usando o plano do Starter Developer ou o
plano do High Security Business Network.
{:shortdesc}

## Testando funções e transações
{: #sdk}

O Hyperledger Fabric v0.5 HFC SDK para Node.js contém testes de unidade que destacam recursos de segurança como privacidade, confidencialidade e incapacidade de vinculação. É possível explorar esses testes de unidade em https://github.com/hyperledger/fabric/tree/master/sdk/node/test/unit para ver exemplos de
código para registrar e inscrever usuários, transferir ativos e gerenciar ativos com funções de usuário e atributos do usuário. Os testes de unidade a seguir estão disponíveis:

### registrar.js
O teste de registrar.js inscreve um usuário "administrador" e designa esse usuário como o `registrar` de rede de blockchain. Esse teste também registra e inscreve os usuários adicionais
"webAdmin" e "webUser". A identidade "webAdmin" tem autoridade concedida para registrar membros adicionais com a função 'cliente'. A identidade "webUser" não tem autoridade concedida para registrar membros
adicionais. Quando o "webAdmin" tenta registrar e inscrever usuários com as funções "auditor" e "validador" e quando o "webUser" tenta registrar e inscrever o "webUser2", as tentativas falham.

A captura de tela a seguir mostra que "webAdmin" é registrado e inscrito e configurado como o `registrar` de cadeia. O usuário "webAdmin" registra e inscreve "webUser" com êxito:
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
 No entanto, "webAdmin" falha ao registrar e inscrever um usuário como "auditor", porque a identidade "webAdmin" é autorizada somente a registrar e inscrever membros com a função 'cliente':
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
Na captura de tela a seguir, o "webUser" tenta registrar e inscrever o "webUser2". A tentativa falha, porque a identidade "webUser" não tem autoridade para inscrever membros:
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
### chain-tests.js
O teste de chain-test.js registra e inscreve um usuário de teste, como implementado pelo `registrar` de rede de blockchain. Esse teste também mostra a autoridade do usuário para
`deploy`, `invoke` e consultar chaincode e para consultar variáveis de estado. Quando o usuário de teste tenta consultar uma função ou variável não existente, uma mensagem de
erro é retornada:  

O usuário de teste constrói uma solicitação de implementação com a carga útil a seguir:
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
O usuário de teste aciona a transação de implementação:
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
O usuário de teste constrói uma solicitação de consulta com a carga útil a seguir:
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
O usuário de teste aciona a transação de consulta:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
A transação de consulta é bem-sucedida, porque a função de chaincode e as variáveis de estado são válidas:
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
O usuário de teste constrói uma consulta para uma função de chaincode não existente, com a carga útil a seguir:
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
O usuário de teste aciona a transação de consulta:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
A transação de consulta falha pois: "BOGUS" não especifica uma função de chaincode válida:
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
O teste de asset-mgmt.js inscreve três usuários: Alice, Bob e Charlie. Esse teste também tem Alice implementando o chaincode e, em seguida, chamando o chaincode para atribuir um ativo para Bob. Bob,
então, chama o mesmo chaincode para transferir o mesmo ativo para Charlie. Uma consulta confirma a transferência de ativo bem-sucedida.

Alice constrói a carga útil a seguir para transferir um ativo (Ferrari) para o usuário Bob, que é representado por seu certificado de inscrição (eCert) bobAppCert:
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
Alice aciona a chamada para designar o ativo para Bob:
```js
var tx = alice.invoke(invokeRequest);
```
Bob constrói a carga útil a seguir para transferir o ativo para o usuário Charlie, que é representado por seu eCert charlieAppCert:
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
Bob aciona a chamada para designar o ativo para Charlie:
```js
var tx = bob.invoke(invokeRequest);
```
Alice constrói uma consulta com a carga útil a seguir:
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
Alice aciona a consulta:
```js
var tx = alice.query(queryRequest);
```
O proprietário esperado da Ferrari é Charlie, representado no código por charlieAppCert. A consulta produzirá uma resposta com falha se a consulta com relação à "Ferrari" não corresponder ao certificado de
usuário codificado do Charlie:
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
### asset-mgmt-with-roles.js
O teste de asset-mgmt-with-roles.js se expande na transferência de cenário de propriedade no exemplo de `asset-mgmt.js`, apresentando as funções e atributos do usuário para três
personagens: Alice, Bob e designador. O membro designador chama o chaincode e transfere com sucesso um ativo para Alice. Alice falha em transferir com êxito o mesmo ativo para Bob, porque ela não possui o
atributo de designador. Uma consulta no ativo confirma a transferência bem-sucedida pelo membro designador e uma transferência com falha por Alice.

O "designador" designa Alice (designada por aliceCert) como o proprietário de um ativo, que é definido no parâmetro args como "MyAsset":
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
Alice tenta designar Bob como o proprietário do ativo. A tentativa falha, porque a função de 'designador' não foi emitida para ela no arquivo membersrvc.yaml:
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

<!-- comment this one out until Hl v0.6 GAs
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

-->
