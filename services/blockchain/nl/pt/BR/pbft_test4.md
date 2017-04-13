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


# Teste 4 de consenso: reiniciar um nó bizantino
{: #pbft_test1}


O Teste 4 de consenso testa o protocolo do PBFT em um cenário de rede no qual um dos quatro nós voltou on-line depois de ser bizantino: um nó é reiniciado após ficar off-line de uma maneira arbitrária e
simultânea.

Um peer anteriormente bizantino que, desde então, se uniu novamente a uma rede de blockchain detectará que sua cópia do livro razão se atrasa disso dos outros peers. O peer atrasado
atualiza automaticamente o seu livro razão copiando blocos ausentes de um peer com o livro razão atual; esse processo é referido como transferência de estado.
{:shortdesc}

Observe que esse caso de teste requer um grande número de operações de chamada. Os peers notificam um ao outro sobre os estados de seu livro razão atual enviando mensagens internas de
*ponto de verificação*; o peer atrasado determina que ele está se atrasando verificando essas mensagens.

Conclua as etapas a seguir para testar o PBFT após reiniciar um nó bizantino:
1. Efetue login com seu ID do usuário e sua senha de rede:  
   a. Execute POST para ***VP0 URL***/registrar  
   b. Execute a Carga Útil {“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”}  
    c.	O peer retorna a carga útil
2. Verifique se a rede está funcionando:  
    a.	Consulte cada peer para obter sua altura de blockchain, especificando a URL para cada peer:  
   b. Execute **GET ***VP0 URL***/chain**  
   c. O comando retorna a carga útil:  
```json {
"currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
   d. Se esta for a primeira operação com relação ao blockchain, a altura de cadeia será 1, porque o único bloco na cadeia é o bloco de gênesis. A altura de cadeia aumentará conforme você anexa transações ao
livro razão.
3. Implementar chaincode:  
    a.	Execute POST para ***VP0 URL***/chaincode  
   b. Com a carga útil:  
```json {
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
   c. O peer retorna a carga útil:
```json {
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "YOUR_CHAINCODE_ID"
},
"id": 1
}
```
   d. A solicitação é transmitida para todos os quatro peers na rede. Os peers executam o protocolo de consenso do PBFT e concordam em executar essa solicitação e armazenar o resultado em suas respectivas
cópias do livro razão.  
   e. Todas as transações são assíncronas. A carga útil de retorno contém um hash de chaincode, que você usará em chamadas de chaincode posteriores. f. A conclusão da implementação é dependente de fatores como velocidade do processador e latência de rede.  
4. Para fins de teste, simule nós VP2 ficando off-line, de uma maneira bizantina (arbitrária e simultânea), parando o nó manualmente usando o botão de parada de interface.
5. Execute uma operação de chamada no chaincode:  
   a. Para este exemplo, chaincode_example02 move 1 unidade de a para b:  
   b. Execute POST para ***VP0 URL***/chaincode com carga útil:
```json {
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
  c. O peer retorna a carga útil:
```json {
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
},
"id": 2
}
```
   d. A solicitação é novamente transmitida para todos os quatro peers na rede. Os peers executam o protocolo de consenso do PBFT e concordam em executar essa solicitação e anexar o resultado em suas
respectivas cópias do livro razão.  
6. Essa solicitação também é assíncrona. Após um breve intervalo, verifique se a operação de chamada foi concluída:  
   a. Execute POST para ***VP0 URL***/chaincode com carga útil:
```json {
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
   b. O peer retorna a carga útil:
```json {
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "999"
},
"id": 3
}
```
   c. Como esperado, o valor de "a" é 1 ou menos.
7. Simule o peer **VP2** voltando on-line reiniciando-o manualmente, usando o botão de início na interface.
8. Envie operações de chamada para VP0.
9. Consulte os valores chaincode de “a” em todos os quatro peers. Todos os peers retornam o mesmo valor para “a".  (**Nota**: a quantia de tempo para o peer reiniciado
(**VP2**) para executar com êxito a função `stateTransfer` é contingente de uma variedade de parâmetros.  Lembre-se de que o PBFT requer apenas 2f + 1 peers para chegar a
um consenso.  Portanto, pode ser necessário um grande número de chamadas **VP2** para "recuperar o atraso" devido ao fato de que isso não é necessário para um consenso nas circunstâncias
atuais.  Visite o hyperledger/fabric [Especificação de Protocolo](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1) do Hyperledger Project da Linux Foundation para obter mais informações sobre esta implementação de consenso.)

(END de Teste 4 de consenso)
