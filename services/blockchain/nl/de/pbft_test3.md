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


# Konsenstest 3: Zwei Byzantine-Knoten
{: #pbft_test2}


In Konsenstest 3 wird das PBFT-Konsensprotokoll in einem Netzszenario getestet, in dem zwei Knoten Byzantine-Knoten sind: zwei Knoten sind arbiträr und gleichzeitig in den Offline-Modus gewechselt.
{:shortdesc}

Vom PBFT-Protokoll wird sichergestellt, dass ein Blockchain-Netz mit N Peers weiterhin funktioniert, wenn nicht mehr als (N-1)/3 Peers in einem Byzantine-Knoten in den Offline-Modus wechseln (arbiträr und gleichzeitig). Da das Bluemix Blockchain-Netz aus vier Peers besteht, werden im Netz beim Absturz von zwei Peers KEINE Transaktionen ausgeführt und KEINE Blöcke an das Hauptbuch angehängt. Bei Anwendung der PBFT-Formel ergibt sich, dass (4-1)/3 = 1 < Anzahl der Byzantine-Knoten (2) ist; deswegen wird die Transaktionsverarbeitung gestoppt.

Führen Sie die folgenden Schritte aus, um PBFT in einem aus vier Knoten bestehenden Netz mit zwei Byzantine-Knoten zu testen:
1.  Melden Sie sich am Netz mit Benutzer-ID und Kennwort an:  
    a.  Führen Sie POST für ***VP0 URL***/registrar aus.  
    b.  Führen Sie die Nutzdaten {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”} aus.  
    c.  Vom Peer werden die Nutzdaten zurückgegeben.
2.  Stellen Sie sicher, dass das Netz betriebsbereit ist:  
    a.  Fragen Sie die Blockchain-Höhe jedes Peers ab und geben Sie die URL für jeden Peer an:  
    b.  Führen Sie GET ***VP0 URL***/chain aus.  
    c.  Vom Befehl werden die Nutzdaten zurückgegeben:
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```
    d.  Wenn dies die erste Operation für Blockchain ist, beträgt die Chain-Höhe 1, weil der einzige Block in der Chain der Genesis-Block ist. Die Chain-Höhe nimmt zu, wenn Transaktionen an das Hauptbuch angehängt werden.
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
      "message": "YOUR_CHAINCODE_ID"
      },
      "id": 1
      }
      ```
    d.  Die Anforderung wird an alle vier Peers im Netz übertragen. Von den Peers wird das PBFT-Konsensprotokoll ausgeführt und der Ausführung dieser Anforderung sowie dem Anhängen des Ergebnisses an ihre jeweiligen Kopien des Hauptbuchs zugestimmt.  
    e.  Beachten Sie, dass alle Transaktionen asynchron sind. Die zurückgegebenen Nutzdaten enthalten nur eine Transaktions-ID, die Sie später zum Abfragen des Ergebnisses verwenden können.
4.  Simulieren Sie zu Testzwecken den Wechsel der Knoten VP2 und VP3 mithilfe der Byzantine-Methode (arbiträr und gleichzeitig) in den Offline-Modus; stoppen Sie die Knoten hierzu manuell in der Schnittstellen unter Verwendung der Stoppschaltfläche.  (**Hinweis**: Es kann 30 bis 60 Sekunden dauern, bis das Stoppen von VP2 und VP3 in der Schnittstelle seinen Niederschlag findet.)
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
    d.  Weil der PBFT-Test f = (N-1)/3 im Netz fehlschlägt, wird die Aufrufaktion zwar als Eingabe bestätigt, aber nicht ausgeführt; an das gemeinsam genutzte Hauptbuch wird nichts angehängt.
6.  Überprüfen Sie, ob die Aufrufoperation nicht ausgeführt wurde; fragen Sie hierzu den Wert für die Variable 'a' ab:  
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
      "message": "1000"
      },
      "id": 3
      }
      ```
    c.  Beachten Sie, dass der Wert für 'a' unverändert geblieben ist.

  (ENDE von Konsenstest 3)
