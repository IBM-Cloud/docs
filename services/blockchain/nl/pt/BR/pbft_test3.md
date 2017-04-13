---

copyright:
  years: 2016
lastupdated: "2016-08-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Teste 3 de consenso: dois nós bizantinos
{: #pbft_test2}


O Teste 3 de consenso testa o protocolo de consenso do PBFT em um cenário de rede no qual dois dos quatro nós são bizantinos: dois nós ficaram off-line de uma maneira arbitrária e simultânea.
{:shortdesc}

O protocolo do PBFT garante que uma rede de blockchain com N peers continuará a funcionar se não mais de (N-1)/3 peers ficarem off-line de uma maneira bizantina (arbitrária e simultânea). A sua rede de
blockchain do bluemix tem quatro peers; portanto, se dois peers travarem, a rede NÃO irá executar nenhuma transação ou anexar qualquer bloco no livro razão. Aplicar a fórmula do PBFT revela que (4-1)/3 = 1 <
o número de nós bizantinos (2); portanto, o processamento de transações para.

Conclua as etapas a seguir para testar o PBFT em uma rede de quatro nós com dois nós bizantinos:
1.  Efetue login com seu ID do usuário e sua senha de rede:  
    a.  Execute POST para ***VP0 URL***/registrar  
    b.  Execute a Carga Útil {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}  
    c.  O peer retorna a carga útil
2.  Verifique se a rede está funcionando:  
    a.  Consulte cada peer para obter sua altura de blockchain, especificando a URL para cada peer:  
    b.  Execute GET ***VP0 URL***/chain  
    c.  O command retorna a carga útil:
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```
    d.  Se esta for a primeira operação com relação ao blockchain, a altura de cadeia será 1, porque o único bloco na cadeia é o bloco de gênesis. A altura de cadeia aumenta conforme as transações são
anexadas ao livro razão.
3.  Implementar chaincode:  
    a.  Execute POST para ***VP0 URL***/chaincode  
    b.  Com carga útil:  
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
    c.  O peer retorna a carga útil:
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
    d.  A solicitação é transmitida para todos os quatro peers na rede. Os peers executam o protocolo de consenso do PBFT e concordam em executar essa solicitação e anexar o resultado em suas respectivas
cópias do livro razão.  
    e.  Observe que todas as transações são assíncronas. A carga útil de retorno contém um identificador de transação apenas, que é possível usar posteriormente para consultar o resultado.
4.  Para fins de teste, simule nós VP2 e VP3 ficando off-line, de uma maneira bizantina (arbitrária e simultânea), parando-os manualmente com o botão de parada de interface.  (**Nota**:
pode levar entre 30 e 60 segundos antes que a sua interface reflita que VP2 e VP3 foram "Parados".)
5.  Execute uma operação de chamada no chaincode:  
    a.  Para esse exemplo, chaincode_example02 move 1 unidade de a para b:  
    b.  Execute POST para **URL de *VP0***/chaincode com carga útil:
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
   c.  O peer retorna a carga útil:
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
    d.  Como a rede falha no teste do PBFT f=(N-1)/3, a operação de chamada será aceita como entrada, mas não será executada e nada será anexado ao livro razão compartilhado.
6.  Verifique se a operação de chamada não foi executada, consultando o valor da variável “a”:  
    a.  Execute POST para **URL de *VP0***/chaincode com carga útil:
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
    b.  O peer retorna a carga útil:
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
    c.  Observe que o valor de “a” permanece inalterado.

  (END de Teste 3 de consenso)
