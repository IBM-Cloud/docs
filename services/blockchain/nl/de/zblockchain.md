---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Blockchain on z
{: #zblockchain}
Letzte Aktualisierung: 8. Juli 2016
{: .last-updated}



Sie können den Blockchain-Service im zugeordneten Bluemix-Angebot mit z/OS verwenden, um private und sichere digitale Assets zu erstellen, die anschließend schnell und sicher in Netzen mit Berechtigungen gehandelt werden können.  *(Zusätzliche Information als Teil der Kurzbeschreibung)*
{:shortdesc}


* Rechtfertigt die Menge an Inhalt, dass dies ein eigener Abschnitt ist?  Oder belassen wir diesen Inhalt als eingebetteten Abschnitt in 'Informationen'?
* Der Inhalt besteht aus Informationen zu PBFT, Sicherheit, Leistung und Support.


## PBFT
{: #PBFT}

Practical Byzantine Fault Tolerance (PBFT) ist ein zukunftsträchtiges Konsensprotokoll, das in einer Bereitstellung als Plug-in integriert und konfiguriert werden kann. Das Paket `obcpbft` ist eine Implementierung des zukunftsträchtigen [PBFT](http://dl.acm.org/citation.cfm?id=571640 "PBFT")-Konsensprotokolls, von dem trotz eines Schwellenwerts der validierenden Elemente, die als *Byzantine* agieren, also auf eine unvorhersehbare Art böswillig oder fehlerhaft sind, ein Konsens zwischen validierenden Elementen bereitgestellt wird. In der Standardkonfiguration sind PBFT und Sieve zum Ausführen von mindestens *3t+1* Validatoren (Replikate) konzipiert, wobei bis zu *t* potenziell fehlerhafte Replikate (einschließlich böswilliger oder *Byzantine*-Replikate) toleriert werden. Weitere Informationen zu den PBFT-Kernfunktionen finden Sie im Abschnitt [Protocol Specification](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) des Hyperledger Projects der Linux Foundation. 

Im folgenden Video sehen Sie eine Vorschau: [![Vorschau](http://www.youtube.com/watch?v=EKa5Gh9whgU)(http://img.youtube.com/vi/EKa5Gh9whgU/0.jpg)]:

*(Angabe eines praktischen Grunds erforderlich, aus dem die Benutzer PBFT kennen müssen. Welche Rolle spielt PBFT beim Support von Blockchain on z und welche Beziehungen gibt es zu diesem Support.)*


### Unterstützte Fehlerfälle
{: #failure}

*Welche Fehlerfälle wir unterstützen und was wir hier nicht unterstützen.*

*(Mehr Details können Barry Mosakowski/Raleigh/IBM oder Tuan Dang/Raleigh/IBM bereitstellen.)*

### Verfügbarkeit des zugeordneten Angebots mit z/OS
{: #Availability}

*Verfügbarkeit und Erwartungen zu Verfügbarkeit auf der Basis der PBFT-Tests.*

*(Weitere Details erforderlich.)*

### Basisfunktionalität von PBFT überprüfen
{: #Test PBFT}

*(Infos von Gari. Wir brauchen weitere Details von Jason zum Ausführen und Testen der Schritte, einschließlich Screenshots.)*

Führen Sie die folgenden Schritte aus, um die PBFT-Basisfunktionalität zu überprüfen:

1. Übergeben Sie Transaktionen für mindestens einen Peer im Netz.
2. Stellen Sie sicher, dass mindestens *2f+1* (in diesem Fall 3) Peers denselben Status aufweisen. *(Wie soll das überprüft werden? Die Details für den Testfall sind erforderlich.)*

  *Beispiel bei Verwendung einer REST-API*
3. Klicken Sie im Dashboard auf die Schaltfläche zum Stoppen von Peer 4. *(Verwenden Sie die Funktion 'Peer stoppen' im Dashboard zum Stoppen von Peer 4. Ein Testfall zum Beschreiben der detaillierten Operation ist erforderlich.)*
4. Überprüfen Sie, ob die Verarbeitung im Netz fortgesetzt wird. *(Wie wird das überprüft?)*
5. Klicken Sie im Dashboard auf die Schaltfläche zum Stoppen von Peer 3.
6. Überprüfen Sie, ob die Verarbeitung im Netz gestoppt wird.
7. Klicken Sie im Dashboard auf die Schaltfläche zum erneuten Starten von Peer 3.

Wenn der Status von Peer 3 wieder auf dem aktuellen Stand ist und die Verarbeitung im Netz fortgesetzt wird, können Sie die PBFT-Basisfunktionen verwenden.

**Hinweise:**
* Nach dem Neustart von Peer 3 müssen Sie das Zeitlimit abwarten, bevor Sie für Peer 3 neue Transaktionen ausführen können.

* Transaktionen, die an aktive Peers gesendet werden, während die Verarbeitung im Netz gestoppt ist, werden gepuffert und nach der Wiederaufnahme der Verarbeitung im Netz ausgeführt.

## Umgebung für Blockchain on z
{: #z environment}

Stellen Sie zum Verwenden des Blockchain-Service im zugeordneten Bluemix-Angebot mit z/OS sicher, dass die Umgebung die folgenden Voraussetzungen erfüllt:

* Vier Peernetze, in denen PBFT mit Mitgliedschaftsservices ausgeführt wird. Weitere Informationen zu Mitgliedschaftsservices finden Sie im Abschnitt [Protocol Specification](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) des Hyperledger Projects der Linux Foundation. 
* Ein isoliertes Netz, in dem keine gemeinsam genutzten Computer und kein gemeinsam genutzter Hauptspeicher vorhanden ist.
* Isolierte Peers in dem Netz.
* Ein System, das von Cloudsystemadministratoren geschützt wird.

Von der Blockchain-Überwachung werden eine Übersicht über die Blockchain-Umgebung bereitgestellt und Details zum Netz abgerufen. Weitere Informationen zu Ihrer Blockchain-Umgebung und zu ihrer Überwachung finden Sie unter [Chaincode mit Blockchain-Überwachung verwalten](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) und [Beispielapps und Lernprogramme für Blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html).

## Sicherheit

*Sollten Sicherheitsinformationen besser nicht in der Dokumentation angegeben werden?*

## Leistung

*Sollten Leistungsinformationen besser nicht in der Dokumentation angegeben werden?*

## Kundenunterstützung abrufen

Gehen Sie gemäß dem Fehlerbehebungsprozess für IBM Bluemix vor, wenn Probleme mit dem Blockchain-Service auftreten, der dem Bluemix-Angebot mit z/OS zugeordnet ist. Weitere Informationen zum Anfordern von Hilfe finden Sie unter [Fehlerbehebung](https://new-console.ng.bluemix.net/docs/troubleshoot/troubleshoot.html).
