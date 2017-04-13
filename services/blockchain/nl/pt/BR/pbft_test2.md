---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Teste 2 de consenso: um nó bizantino
{: #pbft_test2}

Última atualização: 4 de agosto de 2016
{: .last-updated}

O Teste 2 de consenso testa o protocolo do PBFT em um cenário de rede no qual um dos quatro nós é bizantino: um nó ficou off-line de uma maneira arbitrária e simultânea.
{:shortdesc}

O protocolo do PBFT garante que uma rede de blockchain com N peers continuará a funcionar se não mais de (N-1)/3 peers ficarem off-line de uma maneira bizantina (arbitrária e simultânea). O seu ambiente
de blockchain do Bluemix tem quatro peers; portanto, se um peer travar, a rede continuará a executar consenso e a anexar transações no livro razão. Aplicar a fórmula do PBFT revela que (4-1)/3 = 1 = número de
nós bizantinos; portanto, o processamento de transações na rede de blockchain continuará.

Conclua as etapas a seguir para testar o PBFT em uma rede de quatro nós com um nó bizantino:
1.	Efetue login com seu ID do usuário e sua senha de rede:  
    a.  Execute POST para ***VP0 URL***/registrar  
    b.  Execute Carga útil: {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}
    c.  O peer retorna com a carga útil
2.  Verifique se a rede está funcionando:  
    a.  Consulte cada peer para obter sua altura de blockchain, especificando a URL para cada peer:  
    b   Execute GET ***VP0 URL***/chain  
    c.  O comando retorna a carga útil:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
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
      "message":
      "YOUR_CHAINCODE_ID_RETURNED_HERE"
      },
      "id": 1
      }
      ```  
    d. A solicitação é transmitida para todos os quatro peers na rede. Os peers executam o protocolo de consenso do PBFT e concordam em executar essa solicitação e armazenar o resultado em suas respectivas
cópias do livro razão.  
    e.  Observe que todas as transações são assíncronas. A carga útil de retorno contém um hash de chaincode, que você usará em chamadas de chaincode posteriores.  
    f.  A conclusão da implementação é dependente de fatores como velocidade do processador e latência de rede.  
4.  Para fins de teste, simule nó bizantino VP2 parando isso manualmente, usando o botão de parada na interface.  (**Nota**: pode levar entre 30 e 60 segundos antes que a sua
interface reflita que VP2 foi "Parado".)
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
    d.  A solicitação é transmitida novamente para todos os quatro peers. Os peers executam o protocolo de consenso do PBFT e concordam em executar essa solicitação e armazenar o resultado em suas respectivas cópias do livro razão.
6.  Essa solicitação também é assíncrona. Após um breve intervalo, verifique se a operação de chamada foi concluída, consultando o valor da variável “a” no chaincode:  
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
    b.  O peer retorna com a carga útil:
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
7.  Como esperado, o valor de “a” é 1 a menos do que quando o chaincode foi originalmente implementado.
8.  É possível continuar a emitir operações de chamada e consulta adicionais. O processo é o mesmo que nas etapas anteriores.

(END de Teste 2 de consenso)
