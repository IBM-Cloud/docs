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


# Konsenstest 4: Einen Byzantine-Knoten erneut starten
{: #pbft_test1}


In Konsenstest 4 wird das PBFT-Protokoll in einem Netzszenario getestet, in dem einer der vier Knoten wieder in den Online-Modus wechselt, nachdem er im Byzantine-Modus war: ein Knoten wird erneut gestartet, nachdem er arbiträr und gleichzeitig in den Offline-Modus gewechselt ist.

Von einem früheren Byzantine-Peer, der wieder in ein Blockchain-Netz eingebunden wurde, wird festgestellt, dass seine Kopie des Hauptbuchs hinter denen der anderen Peers zurückliegt. Vom zurückliegenden Peer wird sein Hauptbuch automatisch durch Kopieren der fehlenden Blöcke von einem Peer mit aktuellem Hauptbuch aktualisiert; dieser Prozess wird als Statusübergabe bezeichnet.
{:shortdesc}

Beachten Sie, dass für diesen Testfall eine große Anzahl an Aufrufoperationen erforderlich sind. Die Peers benachrichtigen sich gegenseitig über ihren aktuellen Hauptbuchstatus durch Senden interner Nachrichten des Typs *checkpoint*; ein Peer mit nicht aktuellem Hauptbuch erkennt dies durch Überprüfen dieser Nachrichten.

Führen Sie die folgenden Schritte aus, um PBFT nach dem Neustart eines Byzantine-Knotens zu testen:
1. Melden Sie sich am Netz mit Benutzer-ID und Kennwort an:  
   a. Führen Sie POST für ***VP0 URL***/registrar aus.  
   b. Führen Sie die Nutzdaten {“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”} aus.  
   c. Der Peer gibt die Nutzdaten zurück.
2. Stellen Sie sicher, dass das Netz betriebsbereit ist:  
   a. Fragen Sie die Blockchain-Höhe jedes Peers ab und geben Sie die URL für jeden Peer an:  
   b. Führen Sie Run **GET ***VP0 URL***/chain** aus.  
   c. Vom Befehl werden die Nutzdaten zurückgegeben:  
```json
{
"currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
   d. Wenn das die erste Operation für Blockchain ist, beträgt die Chain-Höhe 1, weil der einzige Block in der Chain der Genesis-Block ist. Die Chain-Höhe nimmt zu, wenn Sie Transaktionen an das Hauptbuch anhängen.
3. Stellen Sie den Chaincode bereit:  
   a. Führen Sie POST für ***VP0 URL***/chaincode aus.  
   b. Verwenden Sie folgende Nutzdaten:  
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
   c. Der Peer gibt die Nutzdaten zurück:
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "YOUR_CHAINCODE_ID"
},
"id": 1
}
```
   d. Die Anforderung wird an alle vier Peers im Netz übertragen. Von den Peers wird das PBFT-Konsensprotokoll ausgeführt und der Ausführung dieser Anforderung zugestimmt; danach wird das Ergebnis für die jeweiligen Kopien des Hauptbuchs gespeichert.  
   e.	Alle Transaktionen sind asynchron. Die zurückgegebenen Nutzdaten enthalten einen Chaincode-Hashwert, den Sie in späteren Chaincode-Aufrufen verwenden. f. Die Ausführung der Bereitstellungsoperation hängt von Faktoren wie Prozessorgeschwindigkeit und Netzlatenz ab.  
4. Simulieren Sie zu Testzwecken den Wechsel von Peer VP2 in den Offline-Modus; verwenden Sie hierzu die Byzantine-Methode (arbiträr und gleichzeitig) und stoppen Sie den manuell Knoten über die Stoppschaltfläche der Schnittstelle.
5. Führen Sie für den Chaincode eine Aufrufoperation aus:  
   a. Verschieben Sie für dieses Beispiel unter Verwendung von 'chaincode_example02' 1 Einheit von a nach b:  
   b. Führen Sie POST für ***VP0 URL***/chaincode mit Nutzdaten aus:
```json
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
  c. Der Peer gibt die Nutzdaten zurück:
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
   d. Die Anforderung wird erneut an alle vier Peers im Netz übertragen. Von den Peers wird das PBFT-Konsensprotokoll ausgeführt und der Ausführung dieser Anforderung sowie dem Anhängen des Ergebnisses an ihre jeweiligen Kopien des Hauptbuchs zugestimmt.  
6. Auch diese Anforderung ist asynchron. Überprüfen Sie nach einem kurzen Intervall, ob die Aufrufoperation ausgeführt wurde:  
   a. Führen Sie POST für ***VP0 URL***/chaincode mit Nutzdaten aus:
```json
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
"args":["a"]
}
“secureContext”: “***test\_user1***”
},
"id": 3
}
```
   b. Der Peer gibt die Nutzdaten zurück:
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
   c. Wie erwartet beträgt der Wert für 'a' 1 oder weniger.
7. Simulieren den Wechsel von Peer **VP2** in den Online-Modus; starten Sie ihn hierzu manuell mithilfe der Startschaltfläche in der Schnittstelle.
8. Senden Sie Aufrufoperationen an VP0.
9. Fragen Sie die Chaincode-Werte von 'a' für alle vier Peers ab. Von allen Peers wird derselbe Wert für 'a' zurückgegeben.  (**Hinweis**: Wie lange es dauert, bis vom erneut gestartete Peer (**VP2**) erfolgreich die Funktion `stateTransfer` ausgeführt wird, hängt von einer Vielzahl an Parametern ab.  Bedenken Sie, dass für PBFT nur 2f + 1 Peers zum Erreichen eines Konsenses erforderlich ist.  Aus diesem Grund können zum Aufholen viele Aufrufe für **VP2** erforderlich sein, da dieser Knoten unter den aktuellen Umständen nicht für den Konsens erforderlich ist.  Weitere Informationen zu dieser Konsensimplementierung finden Sie unter [Protocol Specification](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1) von Hyperledger Fabric im Hyperledger Project der Linux Foundation.)

(ENDE von Konsenstest 4)
