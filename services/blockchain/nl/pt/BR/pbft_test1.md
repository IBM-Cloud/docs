---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Teste 1 de consenso: nenhum nó bizantino
{: #pbft_test1}
Última atualização: 4 de agosto de 2016
{: .last-updated}

O Teste 1 de consenso testa o protocolo de consenso do PBFT em um cenário de rede de blockchain no qual nenhum dos quatro nós são bizantinos: nenhum dos nó ficou off-line de uma maneira arbitrária e
simultânea.
{:shortdesc}

Após ativar o seu Developer Network ou High Security Business Network, conclua as etapas a seguir para testar PBFT sem nós bizantinos:

(**Nota**: os fragmentos de código e instruções fazem uso de vários valores simbólicos.  **URL de VPO**, **"test_user1"**,
**"test_user1_enrollSecret"** e **YOUR_CHAINCODE_ID** são simplesmente marcadores.  Acesse os valores literais para as suas **Credenciais de serviço**
e **URLs de VP** a partir da guia **APIs** em seu console de rede.  O valor para **YOUR_CHAINCODE_ID** aparecerá na guia
**Rede** logo que você tiver implementado uma parte de chaincode na rede.  Além disso, os valores do hash em suas cargas úteis de resposta de JSON serão diferentes desses exemplos.)

1.	Efetue login com seu ID do usuário e sua senha de rede:  
    a. Execute POST para ***VP0 URL***/registrar  
    b.	Execute a Carga Útil {“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”}  
    c.	O peer retorna a carga útil
2.	Verifique se a rede está funcionando:  
    a.	Consulte cada peer para obter sua altura de blockchain, especificando a URL para cada peer:  
    b.  Execute GET ***VP0 URL***/chain  
    c.  O peer retorna a carga útil:
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d.	Se esta for a primeira operação com relação ao blockchain, então, a altura de cadeia será 1, porque o único bloco na cadeia é o bloco de gênesis. A altura de cadeia aumenta conforme as transações são
anexadas ao livro razão.
3.	Implementar chaincode:  
    a.	Execute POST para ***VP0 URL***/chaincode  
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
       "52b0d803fc395b5e34d8d4a7cd69fb6aa00099b8fabed83504ac1c5d61a425aca5b3ad3bf96643ea4fdaac132c417c37b00f88fa800de7ece387d008a76d3586"
       },
       "id": 1
       }
       ```
    d. A solicitação é transmitida para todos os quatro peers na rede. Os peers executam o protocolo de consenso do PBFT e concordam em executar essa solicitação e armazenar o resultado em suas
respectivas cópias do livro razão.  
    e.	Observe que todas as transações são assíncronas. A carga útil de retorno contém um hash de chaincode, que você usará em chamadas de chaincode posteriores.
4.  Após um breve intervalo, verifique se a solicitação de implementação foi concluída:  
    a.  Consulte cada peer para obter sua altura de blockchain, especificando a URL para cada peer por sua vez:  
    b.  Execute GET ***VP0 URL***/chain  
    c.  O command retorna a carga útil:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
    d.  A conclusão da operação de implementação é dependente de fatores como velocidade do processador e latência de rede.
5.  Agora que você implementou o chaincode, é possível chamar operações no chaincode:  
    a.  Usando chaincode_example02, mova 1 unidade de a para b:  
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
6.  A solicitação anterior é assíncrona. Após um breve intervalo, verifique se a operação de chamada foi concluída consultando o valor da variável “a” no chaincode:  
    a.  POST para ***VP0 URL***/chaincode com carga útil:
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
      "message": "999"
      },
      "id": 3
      }
      ```
    c.  Como esperado, o valor de "a" é 1 a menos do que quando o chaincode foi originalmente implementado.  Lembre-se de que o valor original designado para "a" foi 1.000 e o valor original designado para "b"
foi 2.000.  A solicitação de chamada que você acionou na Etapa 5 resulta em uma unidade sendo transferida de "a" para "b".
7.  É possível continuar a emitir operações de chamada e consulta. O processo é o mesmo que nas etapas anteriores.

  (END de Teste 1 de consenso)
