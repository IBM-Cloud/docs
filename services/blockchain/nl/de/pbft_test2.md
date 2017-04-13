---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Konsenstest 2: Ein Byzantine-Knoten
{: #pbft_test2}

Letzte Aktualisierung: 4. August 2016
{: .last-updated}

In Konsenstest 2 wird das PBFT-Protokoll in einem Netzszenario getestet, in dem einer der vier Knoten ein Byzantine-Knoten ist: ein Knoten wechselt arbiträr und gleichzeitig in den Offline-Modus.
{:shortdesc}

Vom PBFT-Protokoll wird sichergestellt, dass ein Blockchain-Netz mit N Peers weiterhin funktioniert, wenn nicht mehr als (N-1)/3 Peers in einem Byzantine-Knoten in den Offline-Modus wechseln (arbiträr und gleichzeitig). Da die Bluemix Blockchain-Umgebung aus vier Peers besteht, werden im Netz beim Absturz eines Peers weiterhin Konsens- und Anhängetransaktionen für das Hauptbuch ausgeführt. Bei Anwendung der PBFT-Formel ergibt sich, dass (4-1)/3 = 1 = Anzahl der Byzantine-Knoten ist; deswegen kann die Transaktionsverarbeitung im Blockchain-Netz fortgesetzt werden.

Führen Sie die folgenden Schritte aus, um PBFT in einem aus vier Knoten bestehenden Netz mit einem Byzantine-Knoten zu testen:
1.	Melden Sie sich am Netz mit Benutzer-ID und Kennwort an:  
    a.  Führen Sie POST für ***VP0 URL***/registrar aus.  
    b.  Führen Sie die Nutzdaten aus: {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”}
    c.  Vom Peer werden die Nutzdaten zurückgegeben.
2.  Stellen Sie sicher, dass das Netz betriebsbereit ist:  
    a.  Fragen Sie die Blockchain-Höhe jedes Peers ab und geben Sie die URL für jeden Peer an:  
    b   Führen Sie GET ***VP0 URL***/chain aus.  
    c.  Vom Befehl werden die Nutzdaten zurückgegeben:
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```  
    d.  Wenn das die erste Operation für Blockchain ist, beträgt die Chain-Höhe 1, weil der einzige Block in der Chain der Genesis-Block ist. Die Chain-Höhe nimmt zu, wenn Transaktionen an das Hauptbuch angehängt werden.
3.  Stellen Sie den Chaincode bereit:  
    a.  Führen Sie POST für ***VP0 URL***/chaincode aus.  
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
      "YOUR_CHAINCODE_ID_RETURNED_HERE"
      },
      "id": 1
      }
      ```  
    d.  Die Anforderung wird an alle vier Peers im Netz übertragen. Von den Peers wird das PBFT-Konsensprotokoll ausgeführt und der Ausführung dieser Anforderung zugestimmt; danach wird das Ergebnis für die jeweiligen Kopien des Hauptbuchs gespeichert.  
    e.  Beachten Sie, dass alle Transaktionen asynchron sind. Die zurückgegebenen Nutzdaten enthalten einen Chaincode-Hashwert, den Sie in späteren Chaincode-Aufrufen verwenden.  
    f.  Die Ausführung der Bereitstellung hängt von Faktoren wie Prozessorgeschwindigkeit und Netzlatenz ab.  
4.  Simulieren Sie zu Testzwecken den Byzantine-Knoten VP2, indem Sie ihn mithilfe der Stoppschaltfläche in der Schnittstelle manuell stoppen.  (**Hinweis**: Es kann 30 bis 60 Sekunden dauern, bis das Stoppen von VP2 in der Schnittstelle seinen Niederschlag findet.)
5.  Führen Sie für den Chaincode eine Aufrufoperation aus:  
    a.  Verschieben Sie für dieses Beispiel unter Verwendung von 'chaincode_example02' 1 Einheit von a nach b:  
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
6.  Auch diese Anforderung ist asynchron. Stellen Sie nach einem kurzen Intervall durch Abfragen des Werts für die Variable 'a' für den Chaincode sicher, dass die Aufrufoperation ausgeführt wurde:  
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
7.  Wie erwartet ist der Wert für 'a' 1 weniger als zu dem Zeitpunkt, an dem der Chaincode ursprünglich bereitgestellt wurde.
8.  Sie können mit dem Absetzen weiterer Aufruf- und Abfrageoperationen fortfahren. Der Prozess ist mit dem in den vorherigen Schritten identisch.

(ENDE von Konsenstest 2)
