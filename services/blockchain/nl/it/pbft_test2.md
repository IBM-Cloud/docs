---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Test di consenso 2: un singolo nodo Byzantine
{: #pbft_test2}

Ultimo aggiornamento: 4 agosto 2016
{: .last-updated}

Il test di consenso 2 testa il protocollo PBFT in uno scenario di rete in cui uno dei quattro nodi è Byzantine: un nodo è andato offline in modo arbitrario e simultaneo.
{:shortdesc}

Il protocollo PBFT garantisce che una rete blockchain con N peer continuerà a funzionare se non più di (N-1)/3 peer va offline in modo Byzantine (arbitrario e simultaneo). Il tuo ambiente blockchain Bluemix ha quattro peer; pertanto, se un peer si arresta in modo anomalo, la rete continua ad eseguire il consenso e accodare le transazioni al registro. L'applicazione della formula PBFT rivela che (4-1)/3 = 1 = numero di nodi Byzantine, quindi l'elaborazione della transazione sulla rete blockchain continua.

Completa la seguente procedura per testare PBFT su una rete a quattro nodi con un nodo Byzantine:
1.	Accedi con i tuoi ID utente e password di rete:  
    a.  Esegui POST a ***VP0 URL***/registrar  
    b.  Esegui il payload: {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}
    c.  Il peer restituisce il payload
2.  Verifica che la rete sia attiva e in esecuzione:  
    a.  Esegui una query di ciascun peer per la sua altezza del blockchain, specificando l'URL per ogni peer:  
    b   Esegui GET ***VP0 URL***/chain  
    c.  Il comando restituisce il payload:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
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
      "message":
      "IL_TUO_ID_CHAINCODE_RESTITUITO_QUI"
      },
      "id": 1
      }
      ```  
    d. La richiesta viene trasmessa a tutti e quattro i peer sulla rete. I peer eseguono il protocollo di consenso PBFT e concordano di eseguire questa richiesta e memorizzare il risultato nelle loro rispettive copie del registro.  
    e.  Nota: tutte le transazioni sono asincrone. Il payload di ritorno contiene un hash chaincode, che utilizzerai nei richiami di chaincode successivi.  
    f.  Il completamento della distribuzione dipende da fattori quali la velocità del processore e la latenza di rete.  
4.  Per scopi di test, simula il nodo Byzantine VP2 arrestandolo manualmente utilizzando il pulsante di arresto nell'interfaccia.  (**Nota**:  potrebbero volerci tra i 30 e i 60 secondi prima che la tua interfaccia mostri che VP2 è in uno stato di "Arrestato".
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
    d.  La richiesta viene di nuovo trasmessa a tutti e quattro i peer. I peer eseguono il protocollo di consenso PBFT e concordano di eseguire questa richiesta e memorizzare il risultato nelle loro rispettive copie del registro.
6.  La richiesta è anche asincrona. Dopo un breve intervallo, controlla che l'operazione di richiamo sia stata completata eseguendo una query del valore della variabile “a” sul chaincode:  
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
      "message": "999"
      },
      "id": 3
      }
      ```
7.  Come previsto, il valore di “a” è di 1 inferiore a quando il chaincode è stato originariamente distribuito.
8.  Puoi continuare a emettere ulteriori operazioni di richiamo e query. Il processo è lo stesso indicato nei passi precedenti.

(FINE del test di consenso 2)
