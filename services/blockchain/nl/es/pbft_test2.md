---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Prueba de consenso 2: Un nodo bizantino
{: #pbft_test2}

Última actualización: 4 de agosto de 2016
{: .last-updated}

La prueba de consenso 2 prueba el protocolo PBFT en un escenario de red donde uno de los cuatro nodos es bizantino: un nodo ha pasado a estar fuera de línea de forma arbitraria y simultánea.
{:shortdesc}

El protocolo PBFT garantiza que una red de blockchain con N iguales continuará funcionando si no hay más de (N-1)/3 iguales que pasan a fuera de línea de una manera bizantina (arbitraria y simultánea). El entorno de blockchain de Bluemix tiene cuatro iguales, de modo que si uno se bloquea, la red seguirá ejecutando consenso y añadiendo transacciones al libro mayor. La aplicación de la fórmula PBFT se revela que (4-1)/3 = 1 = número de nodos bizantinos, de modo que el proceso de transacción de la red de blockchain continua.

Complete los siguientes pasos para probar PBFT en una red de cuatro nodos con un nodo bizantino:
1.	Inicie la sesión con el ID de usuario y contraseña de red:
    a.  Ejecute POST to ***VP0 URL***/registrar
    b.  Ejecute Payload: {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}
    c.  El igual se devuelve con la carga útil
2.  Verifique que la red está activa y en ejecución:
    a.  Busque en cada igual su altura de blockchain, especificando el URL para cada igual:
    b   Ejecute GET ***VP0 URL***/chain
    c.  El mandato devuelve la carga útil:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
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
      "message":
      "YOUR_CHAINCODE_ID_RETURNED_HERE"
      },
      "id": 1
      }
      ```  
    d. La solicitud se transmite a los cuatro iguales de la red. Los iguales ejecutan el protocolo de consenso PBFT y están de acuerdo en ejecutar esta solicitud y almacenar el resultado en sus respectivas copias del libro mayor.  
    e.  Tenga en cuenta que las transacciones son asíncronas. La carga útil de devolución contiene un hash de código de encadenamiento, que se utilizará en invocaciones de código de encadenamiento posteriores.  
    f.  La finalización del despliegue depende de factores tales como la velocidad del procesador y la latencia de red.  
4.  Para fines de prueba, simule un nodo bizantino VP2 deteniéndole manualmente, utilizando el botón de detención de la interfaz.  (**Nota**: Puede tardar entre 30 y 60 segundos antes de la interfaz refleje que VP2 se ha "Detenido".)
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
    d.  La solicitud se transmite de nuevo a los cuatro iguales. Los iguales ejecutan el protocolo de consenso PBFT y están de acuerdo en ejecutar esta solicitud y almacenar el resultado en sus respectivas copias del libro mayor.
6.  Esta solicitud también es asíncrona. Después de un breve intervalo, compruebe que la operación de invocación se ha completado, consultando el valor de la variable “a” en el código de encadenamiento:
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
    b.  El igual se devuelve con la carga útil:
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "999"
      },
      "id": 3
      }
      ```
7.  Tal como se esperaba, el valor de "a" es 1 menos que cuando el código de encadenamiento se desplegó originalmente.
8.  Puede seguir emitiendo operaciones de invocación y consulta adicionales. El proceso es el mismo que en los pasos anteriores.

(FIN de la prueba de consenso 2)
