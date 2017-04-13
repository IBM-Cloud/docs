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


# Testo di consenso 3: due nodi Byzantine
{: #pbft_test2}


Il test di consenso 3 testa il protocollo di consenso PBFT in uno scenario di rete in cui due dei quattro nodi sono Byzantine: due nodi sono andati offline in modo arbitrario e simultaneo.
{:shortdesc}

Il protocollo PBFT garantisce che una rete blockchain con N peer continuerà a funzionare se non più di (N-1)/3 peer va offline in modo Byzantine (arbitrario e simultaneo). La tua rete blockchain bluemix ha quattro peer; quindi, se due peer si arrestano in modo anomalo, la rete NON eseguirà alcuna transazione o accoderà blocchi al registro. L'applicazione della formula PBFT rivela che (4-1)/3 = 1 < il numero di nodi Byzantine (2), quindi l'elaborazione della transazione viene arrestata.

Completa la seguente procedura per testare PBFT su una rete a quattro nodi con due nodi Byzantine:
1.  Accedi con i tuoi ID utente e password di rete:  
    a.  Esegui POST a ***VP0 URL***/registrar  
    b.  Esegui il payload {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}  
    c.  Il peer restituisce il payload
2.  Verifica che la rete sia attiva e in esecuzione:  
    a.  Esegui una query di ciascun peer per la sua altezza del blockchain, specificando l'URL per ogni peer:  
    b.  Esegui GET ***VP0 URL***/chain  
    c.  Il comando restituisce il payload:
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```
    d.  Se questa è la prima operazione sul blockchain, l'altezza della catena è 1 perché il solo blocco nella catena è il blocco di genesi. L'altezza della catena aumenta man mano che le transazioni vengono accodate al registro.
3.  Distribuisci il chaincode:  
    a.  Esegui POST a ***VP0 URL***/chaincode  
    b.  Con il payload:  
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
    c.  Il peer restituisce il payload:
      ```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "IL_TUO_ID_CHAINCODE"
      },
      "id": 1
      }
      ```
    d.  La richiesta viene trasmessa a tutti e quattro i peer sulla rete. I peer eseguono il protocollo di consenso PBFT e concordano di eseguire questa richiesta e accodare il risultato alle loro rispettive copie del registro.  
    e.  Nota: tutte le transazioni sono asincrone. Il payload di ritorno contiene solo un ID transazione, che puoi utilizzare successivamente per eseguire una query del risultato.
4.  Per scopi di test, simula un passaggio offline dei nodi VP2 e VP3, in modo Byzantine (arbitrario e simultaneo) arrestandoli manualmente con il pulsante di arresto dell'interfacci a.  (**Nota**:  potrebbero volerci tra i 30 e i 60 secondi prima che la tua interfaccia mostri che VP2 e VP3 sono in uno stato di "Arrestato".
5.  Esegui un'operazione di richiamo sul chaincode:  
    a.  Per questo esempio, chaincode_example02 sposta 1 unità da a a b:  
    b.  Esegui POST a ***VP0 URL***/chaincode con payload:
      ```
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
   c.  Il peer restituisce il payload:
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
    d.  Poiché la rete non supera il test PBFT f=(N-1)/3, l'operazione di richiamo viene accettata come input ma non viene eseguita e al registro condiviso non viene accodato nulla.
6.  Verifica la mancata esecuzione dell'operazione di richiamo eseguendo una query del valore della variabile “a”:  
    a.  Esegui POST a ***VP0 URL***/chaincode con payload:
      ```
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
      "args": ["a"]
      }
      “secureContext”: “***test\_user1***”
      },
      "id": 3
      }
      ```
    b.  Il peer restituisce il payload:
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
    c.  Nota: il valore di “a” rimane invariato.

  (FINE del test di consenso 3)
