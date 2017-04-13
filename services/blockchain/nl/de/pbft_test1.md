---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Konsenstest 1: Keine Byzantine-Knoten
{: #pbft_test1}
Letzte Aktualisierung: 4. August 2016
{: .last-updated}

In Konsenstest 1 wird das PBFT-Konsensprotokoll in einem Blockchain-Netzszenario getestet, in dem keiner der vier Knoten ein Byzantine-Knoten ist: kein Knoten hat arbiträr und gleichzeitig in den Offline-Modus gewechselt.
{:shortdesc}

Führen Sie nach dem Start des Entwicklernetzes oder des Unternehmensnetzes mit hohem Sicherheitsniveau die folgenden Schritte aus, um PBFT ohne Byzantine-Knoten zu testen:

(**Hinweis**: In den Code-Snippets und Anweisungen werden verschiedene symbolische Werte verwendet.  **VPO URL**, **"test_user1"**, **"test_user1_enrollSecret"** und **YOUR_CHAINCODE_ID** sind einfach Platzhalter.  Auf die Literalwerte für Ihre **Serviceberechtigungsnachweise** und **VP-URLs** können Sie in der Registerkarte **APIs** in der Netzkonsole zugreifen.  Der Wert für **YOUR_CHAINCODE_ID** wird in der Registerkarte **Netz** angezeigt, sobald Sie einen Teil eines Chaincodes im Netz bereitgestellt haben.  Außerdem weichen die Hashwerte in den JSON-Antwortnutzdaten von den Werten in diesen Beispielen ab.)

1.	Melden Sie sich am Netz mit Benutzer-ID und Kennwort an:  
    a.  Führen Sie POST für ***VP0 URL***/registrar aus.  
    b.	Führen Sie die Nutzdaten {“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”} aus.  
   c. Der Peer gibt die Nutzdaten zurück.
2.	Stellen Sie sicher, dass das Netz betriebsbereit ist:  
   a. Fragen Sie die Blockchain-Höhe jedes Peers ab und geben Sie die URL für jeden Peer an:  
    b.  Führen Sie GET ***VP0 URL***/chain aus.  
    c.  Vom Peer werden die Nutzdaten zurückgegeben:
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d.	Wenn das die erste Operation für Blockchain ist, beträgt die Chain-Höhe 1, weil der einzige Block in der Chain der Genesis-Block ist. Die Chain-Höhe nimmt zu, wenn Transaktionen an das Hauptbuch angehängt werden.
3.	Stellen Sie den Chaincode bereit:  
   a. Führen Sie POST für ***VP0 URL***/chaincode aus.  
    b.  Verwenden Sie folgende Nutzdaten:  
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
     c.  Vom Peer werden die Nutzdaten zurückgegeben:  
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
    d. Die Anforderung wird an alle vier Peers im Netz übertragen. Von den Peers wird das PBFT-Konsensprotokoll ausgeführt und der Ausführung dieser Anforderung zugestimmt; danach wird das Ergebnis für die jeweiligen Kopien des Hauptbuchs gespeichert.  
    e.	Beachten Sie, dass alle Transaktionen asynchron sind. Die zurückgegebenen Nutzdaten enthalten einen Chaincode-Hashwert, den Sie in späteren Chaincode-Aufrufen verwenden.
4.  Überprüfen Sie nach einem kurzen Intervall, ob die Bereitstellungsanforderung ausgeführt wurde:  
    a.  Fragen Sie die Blockchain-Höhe jedes Peers ab und geben Sie die URL für jeden Peer an:  
    b.  Führen Sie GET ***VP0 URL***/chain aus.  
    c.  Vom Befehl werden die Nutzdaten zurückgegeben:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
    d.  Die Ausführung der Bereitstellungsoperation hängt von Faktoren wie Prozessorgeschwindigkeit und Netzlatenz ab.
5.  Da Sie jetzt Chaincode bereitgestellt haben, können Sie Operationen für Chaincode aufrufen:  
    a.  Verschieben Sie unter Verwendung von 'chaincode_example02' 1 Einheit von a nach b:  
    b.  Führen Sie POST für ***VP0 URL***/chaincode mit Nutzdaten aus:
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
    c.  Vom Peer werden die Nutzdaten zurückgegeben:
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
    d.  Die Anforderung wird wieder an alle vier Peers übertragen. Von den Peers wird das PBFT-Konsensprotokoll ausgeführt und der Ausführung dieser Anforderung zugestimmt; danach wird das Ergebnis für die jeweiligen Kopien des Hauptbuchs gespeichert.
6.  Die vorherige Anforderung ist asynchron. Stellen Sie nach einem kurzen Intervall durch Abfragen des Werts für die Variable 'a' vom Chaincode sicher, dass die Aufrufoperation ausgeführt wurde:  
    a.  Führen Sie POST für ***VP0 URL***/chaincode mit Nutzdaten aus:
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
    b.  Vom Peer werden die Nutzdaten zurückgegeben:
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
    c.  Wie erwartet ist der Wert für 'a' 1 weniger als zu dem Zeitpunkt, an dem der Chaincode ursprünglich bereitgestellt wurde.  Hierbei ist zu beachten, dass 'a' als ursprünglicher Wert 1.000 und 'b' als ursprünglicher Wert 2.000 zugeordnet war.  Die Aufrufanforderung, die Sie in Schritt 5 ausgelöst haben, führte dazu, dass eine Einheit von 'a' nach 'b' übertragen wurde.
7.  Sie können mit dem Absetzen von Aufruf- und Abfrageoperationen fortfahren. Der Prozess ist mit dem in den vorherigen Schritten identisch.

  (ENDE von Konsenstest 1)
