---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Test di consenso 1: nessun nodo Byzantine
{: #pbft_test1}
Ultimo aggiornamento: 4 agosto 2016
{: .last-updated}

Il test di consenso 1 testa il protocollo di consenso PBFT in uno scenario di rete blockchain in cui nessuno dei quattro nodi è Byzantine: nessuno dei nodi è andato offline in un modo arbitrario e simultaneo.
{:shortdesc}

Dopo l'avvio di Developer Network o High Security Business Network, completa la seguente procedura per testare PBFT senza nodi Byzantine:

(**Nota**:  i frammenti di codice e le istruzioni utilizzano diversi valori simbolici.  **VPO URL**, **"utente_test1"**, **"utente_test1_enrollSecret"** e **IL_TUO_ID_CHAINCODE** sono semplicemente dei segnaposto.  Accedi ai valori letterali per le tue **Credenziali di servizio** e i tuoi **URL VP** dalla scheda **API** nella tua console di rete.  Il valore per **IL_TUO_ID_CHAINCODE** sarà visualizzato nella scheda **Rete** dopo che avrai distribuito una parte di chaincode alla rete.  Inoltre, i valori hash nei tuoi payload di risposta JSON saranno differenti da questi esempi).

1.	Accedi con i tuoi ID utente e password di rete:  
    a.  Esegui POST a ***VP0 URL***/registrar  
    b.	Esegui il payload {“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”}  
    c.	Il peer restituisce il payload
2.	Verifica che la rete sia attiva e in esecuzione:  
    a. Esegui una query di ciascun peer per la sua altezza del blockchain, specificando l'URL per ogni peer:  
    b.  Esegui GET ***VP0 URL***/chain  
    c.  Il peer restituisce il payload:
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d. Se questa è la prima operazione sul blockchain, l'altezza della catena è 1 perché il solo blocco nella catena è il blocco di genesi. L'altezza della catena aumenta man mano che le transazioni vengono accodate al registro.
3.	Distribuisci il chaincode:  
    a. Esegui POST a ***VP0 URL***/chaincode  
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
       "52b0d803fc395b5e34d8d4a7cd69fb6aa00099b8fabed83504ac1c5d61a425aca5b3ad3bf96643ea4fdaac132c417c37b00f88fa800de7ece387d008a76d3586"
       },
       "id": 1
       }
       ```
    d. La richiesta viene trasmessa a tutti e quattro i peer sulla rete. I peer eseguono il protocollo di consenso PBFT e concordano di eseguire questa richiesta e memorizzare il risultato nelle loro rispettive copie del registro.  
    e. Nota: tutte le transazioni sono asincrone. Il payload di ritorno contiene un hash chaincode, che utilizzerai nei richiami di chaincode successivi.
4.  Dopo un breve intervallo, controlla che la richiesta di distribuzione sia stata completata:  
    a.  Esegui una query di ciascun peer per la sua altezza del blockchain, specificando l'URL per ciascun peer per volta:  
    b.  Esegui GET ***VP0 URL***/chain  
    c.  Il comando restituisce il payload:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
    d.  Il completamento dell'operazione di distribuzione dipende da fattori quali la velocità del processore e la latenza di rete.
5.  Ora che hai distribuito il chaincode, puoi richiamare le operazioni su di esso:  
    a.  Utilizzando chaincode_example02, sposta 1 unità da a a b:  
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
6.  La richiesta precedente è asincrona. Dopo un breve intervallo, controlla che l'operazione di richiamo sia stata completata eseguendo una query del valore della variabile “a” dal chaincode:  
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
    c.  Come previsto, il valore di "a" è di 1 inferiore a quando il chaincode è stato originariamente distribuito.  Ricorda che il valore originario assegnato ad "a" era 1.000 e il valore originario assegnato a "b" era 2.000.  La richiesta di richiamo da te attivata nel passo 5 produce il trasferimento di una singola unità da "a" a "b".
7.  Puoi continuare a emettere operazioni di richiamo e query. Il processo è lo stesso indicato nei passi precedenti.

  (FINE del test di consenso 1)
