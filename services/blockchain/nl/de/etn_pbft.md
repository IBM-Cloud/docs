---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Konsens und Verfügbarkeit testen
{: #etn_pbft}

Der Starter-Entwicklerplan und der Plan für ein Unternehmensnetz mit hohem Sicherheitsniveau ermöglichen das Testen des PBFT-Konsensprotokolls (PBFT - Practical Byzantine Fault Tolerance) in einem aus vier Knoten bestehenden Blockchain-Netz. Die folgenden Abschnitte enthalten allgemeine Details zum Konsens und spezielle Details zu PBFT. Sobald Sie zum Starten der Tests bereit sind, werden die PBFT-Testfälle bereitgestellt.  
{:shortdesc}  

## Was ist ein Konsens?

Der Konsens ist eine Methode zum Überprüfen der Reihenfolge der Anforderungen oder Transaktionen (Bereitstellen und Aufrufen) in einem Blockchain-Netz. Die korrekte Reihenfolge der Transaktionen ist von großer Bedeutung, weil viele Transaktionen von mindestens einer vorherigen Transaktion abhängen (Kontobelastungen hängen zum Beispiel oft von vorherigen Gutschriften ab).

In einem Blockchain-Netz gibt es keine zentrale Autorität, von der die Reihenfolge der Transaktionen festgelegt wird; stattdessen wird von vielen validierenden Knoten (oder Peers) im Netz ein Konsensprotokoll implementiert. Durch den Konsens wird sichergestellt, dass ein Quorum an Knoten der Reihenfolge zustimmt, in der die Transaktionen an das gemeinsam genutzte Hauptbuch angehängt werden. Da eventuelle Abweichungen in Bezug auf die vorgeschlagene Transaktionsreihenfolge so aufgelöst werden, garantiert der Konsens, dass alle Knoten in einem Blockchain-Netz unter Verwendung desselben Hauptbuchs betrieben werden. Der Konsens garantiert* also die Integrität und Konsistenz aller Transaktionen in einem Blockchain-Netz.

* Diese Garantie hängt von Variablen wie dem jeweils implementierten Konsensprotokoll und der Anzahl der Knoten im Blockchain-Netz ab. Im Rahmen beider Blockchain on Bluemix-Pläne wird das PBFT-Konsensprotokoll implementiert.  

<br>
## Was ist PBFT?

Practical Byzantine Fault Tolerance (PBFT) ist eine Version eines Konsensprotokolls. Die Aufgabe eines Konsensprotokolls besteht darin, die Reihenfolge der Transaktionen in einem Blockchain-Netz ungeachtet eventueller Risiken aufrecht zu erhalten. Ein solches Risiko ist das arbiträre gleichzeitige Fehlschlagen (ein Byzantine-Fehlertyp) mehrerer Netzknoten. Bei Verwendung von PBFT kann ein Blockchain-Netz aus (N) Knoten den Ausfall einer Anzahl von (f) Byzantine-Knoten überbrücken, wobei die Formel f = (N-1)/3 gilt. Anders ausgedrückt bedeutet dies, dass ein Minimum von 2\*f + 1 Knoten den Konsens für die Reihenfolge der Transaktionen erreicht, bevor sie an das gemeinsam genutzte Hauptbuch angehängt werden. Aus beiden Formeln lässt sich die Regel ableiten, dass die Konsistenz und Integrität der Daten in einem PBFT-Netz sichergestellt ist, wenn auf weniger als einem Drittel aller Netzknoten ein Byzantine-Fehler auftritt.  

<br>
## PBFT und Blockchain-Netz

Die PBFT-Regel 2\*f + 1 hat folgende Auswirkungen auf einen Starter-Entwicklerplan und einen Plan für ein Unternehmensnetz mit hohem Sicherheitsniveau:

1. Vom Netz kann maximal ein Byzantine-Knoten toleriert werden. Da jedes Netz aus N = 4 Knoten besteht, ergibt die Anwendung der Formel für die maximale Anzahl der tolerierten Byzantine-Knoten: f = (4-1)/3 = 1. Wenn zwei oder mehr Byzantine-Knoten vorhanden sind (f > 1), kann in einem aus 4 Knoten bestehenden PBFT-Netz nicht die Konsistenz bzw. Integrität des Hauptbuchs auf allen Knoten garantiert werden. (Zum Tolerieren von zwei Byzantine-Knoten wären im Vergleich dazu f = (7-1)/3 = 2 Knoten oder ein aus mindestens 7 Knoten bestehendes PBFT-Blockchain-Netz erforderlich.)
2. Wenn weniger als 2\*f + 1 Knoten online sind, wird das Anhängen an das Hauptbuch vom Netz beendet, weil die Konsistenz und Integrität der Daten von PBFT nicht auf allen Knoten sichergestellt werden kann. Das Anhängen (der Transaktionen) an das Hauptbuch wird im Netz wieder aufgenommen, wenn mindestens 2\*f + 1 Knoten online sind (im vorliegenden Fall drei oder vier Knoten).
3. Da nur ein Minimum von 2\*f + 1 Knoten den Konsens erreichen muss, bevor mit dem nächsten Transaktionsblock fortgefahren werden kann, liegt das Hauptbuch auf weiteren Knoten (jenseits von 2\*f + 1) vorübergehend zeitlich zurück. Diese Verzögerung bei der Synchronisierung des gemeinsamen Hauptbuchs auf allen Knoten ist eine unvermeidliche Einschränkung in jedem PBFT-Netz.
<br>

## Konsenstestfälle
Die folgenden Konsenstestfälle wurden von IBM überprüft und erfüllen die Standards der Netzverfügbarkeit für PBFT:

1. [PBFT-Tests ohne Byzantine-Knoten](pbft_test1.html). Während eines Konsensprozesses werden Transaktionen ausgeführt und an das Hauptbuch angehängt.
2. [Simulation eines Byzantine-Knotens](pbft_test2.html) durch Stoppen eines Knotens und fortgesetztem Senden von Transaktionen zum Bereitstellen, Aufrufen und Abfragen. Während eines PBFT-Konsensprozesses werden Transaktionen ausgeführt und an das Hauptbuch angehängt. Dieser Test wurde für jeden Knoten in einer Umgebung aus vier Knoten wiederholt.
3. [Simulation von zwei Byzantine-Knoten](pbft_test3.html) durch Stoppen von zwei Knoten und fortgesetztem Senden von Transaktionen zum Bereitstellen, Aufrufen und Abfragen. Da der PBFT-Konsens nicht erreicht werden kann, werden Transaktionen nicht ausgeführt oder an das Hauptbuch angehängt.
4. [Neustart eines gestoppten Knotens](pbft_test4.html), der im vorherigen Testfall (Test 3) gestoppt wurde. Während des PBFT-Konsensprozesses werden die Transaktionen wieder aufgenommen und an das Hauptbuch angehängt. Vom neu gestarteten Knoten wird sein Hauptbuch mit dem gemeinsam genutzten Hauptbuch synchronisiert.  

Achtung: Überprüfen Sie die folgenden Anmerkungen, bevor Sie mit den Konsenstests beginnen:

- In allen Konsenstests wird die REST-API zum Interagieren mit den Netzpeers verwendet.
- HTTP/2 wird als Kommunikationsprotokoll verwendet; in den Testfällen werden die URLs der Peers verwendet. Beispiel: 'VP0–api.dev.blockchain.ibm.com:80'. Die symbolischen Werte ***VP0, VP1, VP2 und VP3*** werden als Platzhalter für die URLs der Peer-Literale verwendet.
-  Verwenden Sie zum Anmelden an einem Peer die Berechtigungsnachweise, die beim Bereitstellen des Bluemix-Service angegeben wurden. In den Testfällen werden **test\_user1** und **test\_user1\_enrollSecret** jeweils als Werte für *enrollID* und *enrollSecret* verwendet.
-  Simulieren Sie Knotenausfälle durch das manuelle Stoppen und erneute Starten von Peers mit den Schaltflächen mit der Bezeichnung **Aktionen** in der Netzkonsole. In der nachfolgenden Abbildung 1 wird die Schaltfläche **Aktionen** in der Registerkarte **Netz** dargestellt:

![](images/stopstartpeer.png "Peers starten und stoppen")
*Abbildung 1. Peers starten und stoppen*

- In den Testfällen wird standardmäßig **chaincode_example02** von https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go/chaincode_example02 verwendet. Sie können jedoch auch Ihren eigenen Chaincode oder unter https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go verfügbare Chaincode-Beispiele verwenden.
- Anforderungen werden zur Verarbeitung in einer Transaktion zu einem Stapel zusammengefasst. Mithilfe des Zeitlimitwerts für den Stapel können Sie jedoch eine sofortige Verarbeitung sicherstellen; wenn Sie mindestens zwei Sekunden warten, bevor Sie die nächste Anforderung abschicken, wird die Transaktion sofort verarbeitet.
