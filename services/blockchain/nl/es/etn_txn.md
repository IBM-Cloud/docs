---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Realización de pruebas en redes de blockchain
{: #etn_txn}
Última actualización: 07 de octubre de 2016
{: .last-updated}

Utilice las siguientes pruebas de roles y transacciones para confirmar la disponibilidad y seguridad de la red de IBM Blockchain. Todas las pruebas pueden llevarse a cabo utilizando el plan de desarrollador inicial o el plan de Red empresarial de alta seguridad.
{:shortdesc}

## Realización de pruebas de roles y transacciones
{: #sdk}

El SDK de Hyperledger Fabric v0.5 HFC para Node.js contiene pruebas de unidad que destacan las características de seguridad tales como privacidad, confidencialidad y capacidad de no asociación. Puede explorar estas pruebas de unidad en https://github.com/hyperledger/fabric/tree/master/sdk/node/test/unit para ver ejemplos de código para registrar e inscribir usuarios, transferir activos y gestionar activos con roles de usuario y atributos de usuario. Están disponibles las siguientes pruebas de unidad:

### registrar.js
La prueba registrar.js inscribe un usuario "admin" y designa ese usuario como el `registrador` de la red de blockchain. Esta prueba también registra e inscribe los usuarios adicionales "webAdmin" y "webUser". A la identidad "webAdmin" se le otorga autorización para registrar miembros adicionales con el rol de 'cliente'. A la identidad "webUser" no se le otorga autorización para registrar miembros adicionales. Cuando "webAdmin" intenta registrar e inscribir usuarios con los roles "auditor" y "validador", y cuando "webUser" intenta registrar e inscribir "webUser2", los intentos fallan.

La siguiente captura de pantalla muestra que "webAdmin" está registrado e inscrito, y establecido como el `registrador` de la cadena. El usuario "webAdmin" registra e inscribe satisfactoriamente "webUser":
```js
registerAndEnroll("webAdmin", "client", {roles:['client']}, chain, function(err,webAdmin) {
  if (err) return cb(err);
  chain.setRegistrar(webAdmin);
  registerAndEnroll("webUser", "client", null, chain, function(err, webUser) {
   if (err) return cb(err);
```
 Sin embargo, "webAdmin" no puede registrar ni inscribir a un usuario como "auditor", porque la identidad "webAdmin" solamente está autorizada a registrar e inscribir miembros con el rol de 'cliente':
```js
 registerAndEnroll("auditor", "auditor", null, chain, function(err, auditor) {
  if (!err) return cb(err);
  expect="webAdmin may not register member of type auditor";
  found = (err.toString()).match(expect);
  if (!(found==expect)) cb(err);
```
En la siguiente captura de pantalla, "webUser" intenta registrar e inscribir "webUser2". El intento falla porque la identidad "webUser" no tiene autorización para inscribir miembros:
```js
 chain.setRegistrar(webUser);
 registerAndEnroll("webUser2", "client", null, chain, function(err) {
  if (!err) return cb(Error("webUser should not be allowed to register a client"));
  expect="webUser may not register member of type client";
```
### chain-tests.js
La prueba chain-test.js registra e inscribe un usuario de prueba, tal como implementa el `registrador` de red de blockchain. Esta prueba también muestra la autorización del usuario de prueba para `desplegar`, `invocar` y consultar código de encadenamiento para consultar variables de estado. Cuando el usuario de prueba intenta consultar una función o variable no existente, se devuelve un mensaje de error:  

El usuario de prueba construye una solicitud de despliegue con la siguiente carga útil:
```js
  var deployRequest = {
    fcn: "init",
    args: ["a", initA, "b", initB]
  };
```
El usuario de prueba desencadena la transacción de despliegue:
```js
var deployTx = test_user_Member1.deploy(deployRequest);
```
El usuario de prueba construye una solicitud de consulta con la siguiente carga útil:
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
El usuario de prueba desencadena la transacción de consulta:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
La transacción de consulta se lleva a cabo satisfactoriamente porque la función de código de encadenamiento y las variables de estado son válidas:
```js
t.pass(util.format("Successfully queried existing chaincode state: request=%j, response=%j, value=%s", queryRequest, results, results.result.toString()));
```
El usuario de prueba construye una solicitud para una función de código de encadenamiento no existente con la siguiente carga útil:
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
El usuario de prueba desencadena la transacción de consulta:
```js
var queryTx = test_user_Member1.query(queryRequest);
```
La transacción de consulta falla porque fcn: "BOGUS" no especifica una función de código de encadenamiento válida.
```js
t.pass(util.format("Failed to query non-existing chaincode function: request=%j, error=%j",queryRequest,err));
```
### asset-mgmt.js
La prueba asset-mgmt.js incluye tres usuarios: Alice, Bob y Charlie. En esta prueba Alice también despliega código de encadenamiento y, a continuación, invoca el código de encadenamiento para asignar un activo a Bob. Bob invocará el mismo código de encadenamiento para transferir el mismo activo a Charlie. Una consulta confirma la transferencia de activos satisfactoria.

Alice construye la siguiente carga útil para transferir un activo (Ferrari) al usuario Bob, que está representado por su certificado de inscripción (eCert) bobAppCert:
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
Alice desencadena la invocación para asignar el activo a Bob:
```js
var tx = alice.invoke(invokeRequest);
```
Bob construye la siguiente carga útil para transferir el activo a Charlie, que está representado por este eCert charlieAppCert:
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
Bob desencadena la invocación para asignar el activo a Charlie:
```js
var tx = bob.invoke(invokeRequest);
```
Alice construye una consulta con la siguiente carga útil:
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
Alice desencadena la consulta:
```js
var tx = alice.query(queryRequest);
```
El propietario esperado del Ferrari es Charlie, representado en el código por charlieAppCert. La consulta generará una respuesta fallida si la consulta de "Ferrari" no corresponde al certificado de usuario codificado de Charlie:
```js
if (results.result != charlieAppCert.encode().toString('hex')) {
            fail(t, "Charlie is not the owner of the asset.")
        }
```
### asset-mgmt-with-roles.js
La prueba asset-mgmt-with-roles.js se amplía a la transferencia del escenario de propiedad en el ejemplo `asset-mgmt.js` introduciendo atributos de usuario y roles para tres personas: Alice, Bob y assigner. El miembro assigner invoca el código de encadenamiento y transfiere satisfactoriamente un activo a Alice. Alice no puede transferir satisfactoriamente el mismo activo a Bob, porque no es propietario del atributo assigner. Una consulta del activo confirma la transferencia satisfactoria realizada por el miembro assigner y una transferencia satisfactoria realizada por Alice.

El "assigner" asigna a Alice (designado por aliceCert) como la propietaria del activo, que se define en el parámetro args como "MyAsset":
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
Alice intenta asignar a Bob como el propietario del activo. El intento falla, porque no se ha emitido el rol de 'assigner' en el archivo membersrvc.yaml:
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
