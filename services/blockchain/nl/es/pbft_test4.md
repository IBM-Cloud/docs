---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Prueba de consenso 4: Reiniciar un nodo bizantino
{: #pbft_test1}
Última actualización: 4 de agosto de 2016
{: .last-updated}

La prueba de consenso 4 prueba el protocolo PBFT en un escenario de red donde uno de los cuatro nodos ha vuelto a estar en línea después de ser bizantino: un nodo se reinicia después de pasar a estar fuera de línea de forma arbitraria y simultánea.

Un igual que fue bizantino anteriormente que ha vuelto a unirse a una red de blockchain detectará que su copia del libro mayor se retrasa en comparación con la de los otros iguales. El igual retrasado actualiza automáticamente su libro mayor copiando los bloques que faltan de un igual con el libro mayor actual; se hace referencia a este proceso como transferencia de estado.
{:shortdesc}

Tenga en cuenta que este caso de prueba requiere un gran número de operaciones de invocación. Los iguales se notifican entre sí de sus estados de libro mayor actuales enviando mensajes de *punto de comprobación* internos; el igual retrasado determina que está retrasado comprobando estos mensajes.

Complete los siguientes pasos para probar PBFT después de reiniciar un nodo bizantino:
1. Inicie la sesión con el ID de usuario y contraseña de red:
    a. Ejecute POST to ***VP0 URL***/registrar
    b. Ejecute Payload {“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”}
   c. El igual devuelve la carga útil
2. Verifique que la red está activa y en ejecución:
    a. Busque en cada igual su altura de blockchain, especificando el URL para cada igual:
    b. Ejecute **GET ***VP0 URL***/chain**
   c. El mandato devuelve la carga útil:  
```json
{
"currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
   d. Si es la primera operación frente a blockchain, la altura de cadena es 1, porque el único bloque de la cadena es el bloque inicial. La altura de la cadena aumenta a medida que se añaden transacciones al libro mayor.
3. Despliegue código de encadenamiento:
    a. Ejecute POST to ***VP0 URL***/chaincode
    b. Con carga útil:  
```json
 {
 "jsonrpc": "2.0",
 "method": "deploy",
 "params": {
 "type": 1,
 "chaincodeID":{
 "path":"github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02"
 },
 "ctorMsg": {
 "function":"init",
 "args": ["a", "1000", "b", "2000"]
 },
 "secureContext": "***test\_user1***"
 },
 "id": 1
 }
```
   c. El igual devuelve la carga útil:
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "YOUR_CHAINCODE_ID"
},
"id": 1
}
```
   d. La solicitud se transmite a los cuatro iguales de la red. Los iguales ejecutan el protocolo de consenso PBFT y están de acuerdo en ejecutar esta solicitud y almacenar el resultado en sus respectivas copias del libro mayor.  
   e. Todas las transacciones son asíncronas. La carga útil de devolución contiene un hash de código de encadenamiento, que se utilizará en invocaciones de código de encadenamiento posteriores. f. La finalización de la operación de despliegue depende de factores tales como la velocidad del procesador y la latencia de red.  
4. Para fines de prueba, simule que el igual VP2 pasa a estar fuera de línea de una forma bizantina (arbitraria y simultánea), deteniendo manualmente el nodo utilizando el botón de detención de la interfaz.
5. Ejecute una operación de invocación en el código de encadenamiento:
    a. Para este ejemplo, chaincode_example02 mueve 1 unidad de a a b:
    b. Ejecute POST to ***VP0 URL***/chaincode con carga útil:
```json
{
"jsonrpc": "2.0",
"method": "invoke",
"params": {
"type": 1,
"chaincodeID":{
"name":"YOUR_CHAINCODE_ID"
},
"ctorMsg": {
"function":"invoke",
"args": ["a", "b", "1"]
}
“secureContext”: “***test\_user1***”
},
"id": 2
}
```
  c. El igual devuelve la carga útil:
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
},
"id": 2
}
```
   d. La solicitud se transmite de nuevo a los cuatro iguales de la red. Los iguales ejecutan el protocolo de consenso PBFT y están de acuerdo en ejecutar esta solicitud y añade el resultado a sus respectivas copias del libro mayor.  
6. Esta solicitud también es asíncrona. Después de un breve intervalo, compruebe que la operación de invocación se ha completado:
    a. Ejecute POST to ***VP0 URL***/chaincode con carga útil:
```json
{
"jsonrpc": "2.0",
"method": "query",
"params": {
"type": 1,
"chaincodeID":{
"name":"YOUR_CHAINCODE_ID"
},
"ctorMsg": {
"function":"query",
"args":["a"]
}
“secureContext”: “***test\_user1***”
},
"id": 3
}
```
   b. El igual devuelve la carga útil:
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "999"
},
"id": 3
}
```
   c. Tal como se esperaba, el valor de "a" es 1 o menos.
7. Simule que el igual **VP2** vuelve a estar en línea reiniciándolo manualmente, utilizando el botón de inicio de la interfaz.
8. Envíe operaciones de invocación a VP0.
9. Consulte los valores de código de encadenamiento de “a” en los cuatro iguales. Todos los iguales devuelven el mismo valor para “a".  (**Nota**: La cantidad de tiempo que tarda el igual reiniciado (**VP2**) en ejecutar satisfactoriamente la función `stateTransfer` está sujeta a una variedad de parámetros.  Recuerde que PBFT solo requiere 2f + 1 iguales para llegar al consenso.  Por lo tanto, puede que sea necesario un gran número de invocaciones para que **VP2** "se ponga al día" debido al hecho de que no es necesario para el consenso en las circunstancias actuales.  Visite hyperledger/fabric [Especificación de protocolo](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1) en Hyperledger Project de Linux Foundation para obtener más información sobre esta implementación de consenso.)

(FIN de la prueba de consenso 4)
