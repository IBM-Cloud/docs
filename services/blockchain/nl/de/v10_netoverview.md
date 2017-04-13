---

copyright:
  years: 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HSBN vNext Beta-Netz - Übersicht
{: #v10_netoverview}


Der HSBN vNext Beta-Service nutzt Hyperledger Fabric v1.0 zur Bereitstellung eines sicheren und genehmigten Blockchain-Netzes, in dem authentifizierte Mitglieder leicht Assets definieren und die Geschäftslösungen für deren Änderung und Austausch erstellen können.
{:shortdesc}

Dieser Service **vereinfacht in hohem Maße** den ansonsten mühsamen Prozess, ein Bootstrapping für ein Blockchain-Netz durchzuführen. Wir stellen das Framework und die Tools zum Einladen von Mitgliedern, Aggregieren verschiedener Materialien zur kryptografischen Identität, Festlegen von Governanceregeln usw bereit. Diese komplizierten Prozesse können so intuitiv und mühelos durchgeführt werden. Innerhalb weniger Minuten können Sie ein voll funktionsfähiges Netz mit hohem Sicherheitsniveau mit Kanälen, Richtlinien und verschiedenen Geschäftslogiken generieren.  

Die **hohe Verfügbarkeit** der integralen Komponenten des Netzes (Peers, Anordnungsservice, Zertifizierungsstelle, Chaincode) eliminiert die lähmenden Effekten, die durch Single Points of Failure entstehen können. Eine integrierte Dashboard-Überwachung sorgt für eine einfache Verwaltung dieser Komponenten und stellt einen leistungsfähigen Mechanismus für die Visualisierung von Assets und Smart Contracts bereit.

Die **Modularität** der Hyperledger Fabric v1.0-Architektur und die klare Trennung von Netzrollen liefert eine Infrastruktur, die eine hohe Skalierbarkeit und leistungsfähige Berechnungen ermöglicht.  

Die Überprüfungen und Ausgleichungen, die während des Lebenszyklus einer Transaktion auftreten, führen zu konsistenten und vollständig überprüften Ergebnissen und die Konten bleiben während der Implementierung des gängigen Gossip-Protokolls durchgehend synchron. Die Identitäts- und Zugriffssteuerung wird ohne großen Aufwand mit **sign/verify**-Operationen durchgesetzt, die fortlaufend im Netz durchgeführt werden.  

Mit **Governance-Tools** können Mitglieder die kritischen Geschäftsregeln für ihr Netz verwalten. Beispielsweise können Sie eine Richtlinie implementieren, die festlegt, wie viele Mitglieder eines Netzes dem Beitritt eines neuen Mitglieds zustimmen müssen. Oder es gibt ein Asset, das von jedem Teilnehmer gebilligt werden muss, damit eine Änderung vorgenommen werden kann. Governanceregeln sind eine grundlegende Notwendigkeit für alle Unternehmensnetze und können häufig sehr umfangreich sein. Governance-Tools (z. B. Richtlinieneditoren) vereinfachen diesen Prozess in hohem Maße.

Der Service wird in einer **extrem sicheren und isolierten** Umgebung ohne externen Zugriff (einschließlich Rootzugriff) auf Netzkomponenten ausgeführt. Daten werden bei der Ausführung und im Ruhezustand verschlüsselt und der für Hardwaresicherheitsmodule verfügbare Support sorgt dafür, dass digitale Schlüssel in Übereinstimmung mit branchenspezifischen Vorschriften geschützt werden. Für Netzinteraktionen wird ein **dedizierter Compute**-Service bereitgestellt, wodurch die Leistung und der Datenschutz optimiert werden. Hashing, Operationen zum Signieren/Verifizieren und die Kommunikation zwischen Komponenten werden dank erweiterter Verschlüsselungsimplementierungen beschleunigt.

**Abbildung 1** zeigt ein Beispiel eines bereitgestellten Blockchain-Netzes bestehend aus vier Mitgliedern (wobei jedes Mitglied zwei Peers besitzt), einer Zertifizierungsstelle, die für das Verteilen kryptografischer Identitätsmaterialien zuständig ist, und einem Anordnungsservice, der Richtlinien und Netzteilnehmer definiert. Der blaue Kanal enthält alle vier Mitglieder, während der gelbe Kanal auf die Mitglieder 2, 3 und 4 beschränkt ist:

![Blockchain-Netz](images/blockchain_network.png "Blockchain-Beispielnetz")

*Abbildung 2. Ein Blockchain-Beispielnetz bestehend aus vier Mitgliedern, die Kanäle zum Isolieren von Daten nutzen*

Umfassende Informationen zu allen Hyperledger Fabric v1.0-Features und Funktionen finden Sie in der entsprechenden Dokumentation zum vollständigen Release unter 'http://hyperledger-fabric.readthedocs.io/en/latest/'.
