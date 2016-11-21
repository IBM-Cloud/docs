---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Prueba de consenso 1: Sin nodos bizantinos
{: #pbft_test1}
Última actualización: 4 de agosto de 2016
{: .last-updated}

La prueba de consenso 1 prueba el protocolo de consenso PBFT en un escenario de red de donde ninguno de los cuatro nodos son bizantinos: ninguno de los nodos han pasado a estar fuera de línea de forma arbitraria y simultánea.
{:shortdesc}

Después de iniciar la Red de desarrollador o la Red empresarial de alta seguridad, complete los siguientes pasos para probar PBFT sin nodos bizantinos:

(**Nota**:  Los fragmentos de código y las instrucciones hacen uso de varios valores simbólicos.  **VPO URL**, **"test_user1"**, **"test_user1_enrollSecret"** y **YOUR_CHAINCODE_ID** son simplemente marcadores de posición.  Acceda a los valores literales para las **Credenciales de servicio** y los **URL de VP** desde el separador **API** en la consola de red.  El valor de **YOUR_CHAINCODE_ID** aparecerá en el separador **Red** una vez que ha desplegado una pieza de código de encadenamiento a la red.  Además, los valores hash en las cargas útiles de respuesta JSON serán diferentes a estos ejemplos.)

1.	Inicie la sesión con el ID de usuario y contraseña de red:
    a.  Ejecute POST to ***VP0 URL***/registrar
    b.	Ejecute Payload {“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”}      c.	El igual devuelve la carga útil
2.	Verifique que la red está activa y en ejecución:
    a.	Busque en cada igual su altura de blockchain, especificando el URL para cada igual:
    b.  Ejecute GET ***VP0 URL***/chain
    c.  El igual devuelve la carga útil:
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d.	Si es la primera operación frente a blockchain, la altura de cadena es 1, porque el único bloque de la cadena es el bloque inicial. La altura de cadena aumenta a medida que se añaden las transacciones al libro mayor.
3.	Despliegue código de encadenamiento:
    a.	Ejecute POST to ***VP0 URL***/chaincode
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
       "52b0d803fc395b5e34d8d4a7cd69fb6aa00099b8fabed83504ac1c5d61a425aca5b3ad3bf96643ea4fdaac132c417c37b00f88fa800de7ece387d008a76d3586"
       },
       "id": 1
       }
       ```
    d. La solicitud se transmite a los cuatro iguales de la red. Los iguales ejecutan el protocolo de consenso PBFT y están de acuerdo en ejecutar esta solicitud y almacenar el resultado en sus respectivas copias del libro mayor.  
    e.	Tenga en cuenta que las transacciones son asíncronas. La carga útil de devolución contiene un hash de código de encadenamiento, que se utilizará en invocaciones de código de encadenamiento posteriores.
4.  Después de un breve intervalo, compruebe que se haya completado la solicitud de despliegue:
    a.  Busque en cada igual su altura de blockchain, especificando el URL para cada igual sucesivamente:
    b.  Ejecute GET ***VP0 URL***/chain
    c.  El mandato devuelve la carga útil:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
    d.  La finalización de la operación de despliegue depende de factores tales como la velocidad del procesador y la latencia de red.
5.  Ahora que ya desplegado el código de encadenamiento, puede invocar operaciones en el código de encadenamiento:
    a.  Utilizando chaincode_example02, mueva 1 unidad de a a b:
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
6.  La solicitud anterior es asíncrona. Después de un breve intervalo, compruebe que la operación de invocación se ha completado consultando el valor de la variable “a” en el código de encadenamiento:
    a.  POST to ***VP0 URL***/chaincode con carga útil:
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
      "message": "999"
      },
      "id": 3
      }
      ```
    c.  Tal como se esperaba, el valor de "a" es 1 menos que cuando el código de encadenamiento se desplegó originalmente.  Recuerde que el valor original asignado a "a" era 1.000 y el valor original asignado a "b" era 2.000.  La solicitud de invocación que ha desencadenado en el paso 5 resulta en que una unidad se transfiera de "a" a "b".
7.  Puede seguir emitiendo operaciones de invocación y consulta. El proceso es el mismo que en los pasos anteriores.

  (FIN de la prueba de consenso 1)
