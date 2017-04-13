---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Zusätzliche Tests
{: #etn_next}


Die folgenden Tests wurden in der Umgebung eines Unternehmensnetzes mit hohem Sicherheitsniveau durchgeführt (sofern nicht anders angegeben), um Chaincode-Funktionen, das Hauptbuch, lange Ausführungen, gleichzeitige Ausführungen und komplexe Transaktionen zu testen.  Die Knoten der Validatoren und Mitgliedschaftsservices wurden als VM-Gäste in einem Container für sichere Services unter dem Betriebssystem LinuxONE ausgeführt.  Die nachfolgend verwendeten Werte wurden auf Basis des Kundenfeedbacks ausgewählt und stellen keine Maximalwerte dar. (Hinweis: Manche dieser Tests werden in den Abschnitten [Node.js-SDK](etn_txn.html) und [Konsens und Verfügbarkeit testen](etn_pbft.html) wiederholt.)

{:shortdesc}

1. Chaincode-Funktion - Die Chaincode-Schnittstellen wurden ausgeführt, um sicherzustellen, dass die Transaktionen `Bereitstellen`, `Aufrufen` und `Abfragen` unter Verwendung der REST-API und Befehlszeilenschnittstelle ordnungsgemäß funktionieren. Sowohl REST-API als auch Befehlszeilenschnittstelle wurden zum Testen aller Endpunktfunktionen (einschließlich Block, Blockchain, Chaincode, Network, Registrar und Transactions) wie in der Protokollspezifikation von Hyperledger verwendet.
2. Hauptbuch - Die Erstellung von 20.000 Einträgen mit Nutzdaten von jeweils 1.000 Byte im Hauptbuch basierend auf unterschiedlichen Umgebungen. Die Tests bezogenen einen Client ein, auf dem seriell 20.000 Datensätze erstellt wurden.
3. Lange Ausführungen - Für diesen Test wurden Aufrufe, Chain-Höhe und Abfragen für mehrere Knoten über 72 Stunden mithilfe des Demo-Chaincodes von 'example02' verwendet.
4. Node.js-SDK - Das erweiterte Node.js-SDK wurde zum Registrieren und Eintragen von Benutzern und zum Ausführen von Bereitstellungen, Aufrufen und Abfragen für einen Peer im Entwicklungsmodus (Starten des Peers mit: `peer node start –peer -chaincodedev`) und im Netzmodus (Starten des Peers mit: `peer node start`) verwendet.
5. Gleichzeitige Basisausführungen - Dieser Test wurde durch Senden gleichzeitiger Aufrufe an jeden der vier Peers für eine Dauer von 10 Minuten und mit einer Nutzlast von jeweils 1.000 Byte, dem Messen der Chain-Höhe und dem Abfragen des Hauptbuchstatus ausgeführt.
6. Komplexe Transaktionen - Dieser Test umfasste das zufällige Abschicken einer Mischung aus Abfragen und Aufrufen mit unterschiedlicher Nutzdatengröße zwischen 10 KB und 500 KB an Peers für eine Dauer von 10 Minuten. Die Chain-Höhe und die Abfrage des globalen Status wurden gemessen, um die Synchronisation des gemeinsam genutzten Hauptbuchs im Netz bei den Peers im Netz sicherzustellen.
