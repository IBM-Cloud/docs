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


# Test di consenso 4: riavvio di un nodo Byzantine
{: #pbft_test1}


Il test di consenso 4 testa il protocollo PBFT in uno scenario di rete in cui uno dei quattro nodi è tornato online dopo essere stato Byzantine: un nodo viene riavviato dopo essere andato offline in modo arbitrario e simultaneo.

Un peer precedentemente Byzantine che si è poi unito nuovamente a una rete blockchain rileverà che la sua copia del registro è indietro rispetto a quello degli altri peer. Il peer in ritardo aggiorna automaticamente il suo registro copiando i blocchi mancanti da un peer con il registro corrente; questo processo viene indicato come trasferimento di stato.
{:shortdesc}

Nota: questo scenario di test richiede un ampio numero di operazioni di richiamo. I peer si segnalano reciprocamente gli stati correnti dei loro registri inviando dei messaggi di *checkpoint* interni: il peer in ritardo determina che è indietro controllando tali messaggi.

Completa la seguente procedura per testare PBFT dopo il riavvio di un singolo nodo Byzantine:
1. Accedi con i tuoi ID utente e password di rete:  
   a. Esegui POST a ***VP0 URL***/registrar  
   b. Esegui il payload {“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”}  
   c. Il peer restituisce il payload
2. Verifica che la rete sia attiva e in esecuzione:  
   a. Esegui una query di ciascun peer per la sua altezza del blockchain, specificando l'URL per ogni peer:  
   b. Esegui **GET ***VP0 URL***/chain**  
   c. Il comando restituisce il payload:  
```json
{
"currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
   d. Se questa è la prima operazione sul blockchain, l'altezza della catena è 1 perché il solo blocco nella catena è il blocco di genesi. L'altezza della catena aumenta man mano che accodi delle transazioni al registro.
3. Distribuisci il chaincode:  
   a. Esegui POST a ***VP0 URL***/chaincode  
   b. Con il payload:  
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
   c. Il peer restituisce il payload:
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "IL_TUO_ID_CHAINCODE"
},
"id": 1
}
```
   d. La richiesta viene trasmessa a tutti e quattro i peer sulla rete. I peer eseguono il protocollo di consenso PBFT e concordano di eseguire questa richiesta e memorizzare il risultato nelle loro rispettive copie del registro.  
   e. Tutte le transazioni sono asincrone. Il payload di ritorno contiene un hash chaincode, che utilizzerai nei richiami di chaincode successivi. f. Il completamento dell'operazione di distribuzione dipende da fattori quali la velocità del processore e la latenza di rete.  
4. Per scopi di test, simula che il peer VP2 va offline in modo Byzantine (arbitrario e simultaneo) arrestando manualmente il nodo utilizzando il pulsante di arresto dell'interfaccia.
5. Esegui un'operazione di richiamo sul chaincode:  
   a. Per questo esempio, chaincode_example02 sposta 1 unità da a a b:  
   b. Esegui POST a ***VP0 URL***/chaincode con il payload:
```json
{
"jsonrpc": "2.0",
"method": "invoke",
"params": {
"type": 1,
"chaincodeID":{
"name":"IL_TUO_ID_CHAINCODE"
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
  c. Il peer restituisce il payload:
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
   d. La richiesta viene nuovamente trasmessa a tutti e quattro i peer sulla rete. I peer eseguono il protocollo di consenso PBFT e concordano di eseguire questa richiesta e accodare il risultato alle loro rispettive copie del registro.  
6. La richiesta è anche asincrona. Dopo un breve intervallo, controlla che l'operazione di richiamo sia stata completata:  
   a. Esegui POST a ***VP0 URL***/chaincode with payload:
```json
{
"jsonrpc": "2.0",
"method": "query",
"params": {
"type": 1,
"chaincodeID":{
"name":"IL_TUO_ID_CHAINCODE"
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
   b. Il peer restituisce il payload:
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
   c. Come previsto, il valore di "a" è 1 o meno.
7. Simula che il peer **VP2** ritorna online riavviandolo manualmente, utilizzando il pulsante di avvio nell'interfaccia.
8. Invia le operazioni di richiamo a VP0.
9. Esegui una query dei valori chaincode di “a” su tutti e quattro i peer. Tutti i peer restituiscono lo stesso valore per “a".  (**Nota**: la quantità di tempo occorrente perché il peer riavviato (**VP2**) esegua correttamente la funzione `stateTransfer` è subordinata a una varietà di parametri.  Ricordati che PBFT richiede solo 2f + 1 peer per raggiungere il consenso.  Ci potrebbe pertanto volere un ampio numero di richiami perché **VP2** "recuperi", visto che non è richiesto per il consenso nelle attuali circostanze.  Visita [Protocol Specification](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1) di hyperledger/fabric dal progetto Hyperledger della Linux Foundation per ulteriori informazioni sull'implementazione di questo consenso).

(FINE del test di consenso 4)
