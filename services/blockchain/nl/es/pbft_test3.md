---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Prueba de consenso 3: Dos nodos bizantinos
{: #pbft_test2}

Última actualización: 4 de agosto de 2016
{: .last-updated}

La prueba de consenso 3 prueba el protocolo de consenso PBFT en un escenario de red donde dos de los cuatro nodos son bizantinos: dos nodos han pasado a estar fuera de línea de forma arbitraria y simultánea.
{:shortdesc}

El protocolo PBFT garantiza que una red de blockchain con N iguales continuará funcionando si no hay más de (N-1)/3 iguales que pasan a fuera de línea de una manera bizantina (arbitraria y simultánea). La red de blockchain de bluemix tiene cuatro iguales, de modo que si dos iguales se bloquean, la red no ejecutará ninguna transacción ni añadirá ningún bloque al libro mayor. La aplicación de la fórmula PBFT revela que (4-1)/3 = 1 < el número de nodos bizantinos (2), de modo que el proceso de transacción se detiene.

Complete los siguientes pasos para probar PBFT en una red de cuatro nodos con dos nodos bizantinos:
1.  Inicie la sesión con el ID de usuario y contraseña de red:
    a.  Ejecute POST to ***VP0 URL***/registrar
    b.  Ejecute Payload {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}
    c.  El igual devuelve la carga útil
2.  Verifique que la red está activa y en ejecución:
    a.  Busque en cada igual su altura de blockchain, especificando el URL para cada igual:
    b.  Ejecute GET ***VP0 URL***/chain
    c.  El mandato devuelve la carga útil:
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```
    d.  Si es la primera operación frente a blockchain, la altura de cadena es 1, porque el único bloque de la cadena es el bloque inicial. La altura de cadena aumenta a medida que se añaden las transacciones al libro mayor.
3.  Despliegue código de encadenamiento:
    a.  Ejecute POST to ***VP0 URL***/chaincode
    b.  Con carga útil:  
      ```
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
    c.  El igual devuelve la carga útil:
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "YOUR_CHAINCODE_ID"
      },
      "id": 1
      }
      ```
    d.  La solicitud se transmite a los cuatro iguales de la red. Los iguales ejecutan el protocolo de consenso PBFT y están de acuerdo en ejecutar esta solicitud y añade el resultado a sus respectivas copias del libro mayor.  
    e.  Tenga en cuenta que las transacciones son asíncronas. La carga útil de devolución contiene solamente un ID de transacción, que puede utilizar más adelante para consultar el resultado.
4.  Para fines de prueba, simule que los nodos VP2 y VP3 pasan a estar fuera de línea, de forma bizantina (arbitraria y simultánea), deteniéndolos manualmente con el botón de detención de la interfaz.  (**Nota**: Puede tardar entre 30 y 60 segundos antes de la interfaz refleje que VP2 y VP3 se han "Detenido".)
5.  Ejecute una operación de invocación en el código de encadenamiento:
    a.  Para este ejemplo, chaincode_example02 mueve 1 unidad de a a b:
    b.  Ejecute POST to ***VP0 URL***/chaincode con carga útil:
      ```
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
   c.  El igual devuelve la carga útil:
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
      },
      "id": 2
      }
      ```
    d.  Dado que la red falla en la prueba de PBFT f=(N-1)/3, la operación de invocación de acepta como entrada pero no se ejecuta y no se añade nada al libro mayor compartido.
6.  Verifique que la operación de invocación no se ha ejecutado, consultando el valor de la variable “a”:
    a.  Ejecute POST to ***VP0 URL***/chaincode con carga útil:
      ```
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
      "args": ["a"]
      }
      “secureContext”: “***test\_user1***”
      },
      "id": 3
      }
      ```
    b.  El igual devuelve la carga útil:
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "1000"
      },
      "id": 3
      }
      ```
    c.  Tenga en cuenta que el valor de “a” permanece sin cambios.

  (FIN de la prueba de consenso 3)
