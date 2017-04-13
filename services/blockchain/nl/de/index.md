---

copyright:
  years: 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung
{: #gettingstartedtemplate}

**ACHTUNG:** Lesen Sie vor der Verwendung eines IBM Blockchain on Bluemix-Plans unbedingt die technischen Angaben und Unterstützungsinformationen unter [Haftungsausschluss](needtoknow.html).
{:shortdesc}

## IBM Blockchain on Bluemix

Der {{site.data.keyword.blockchainfull}} on Bluemix&reg;-Service setzt sich aus drei Blockchain-Netzplänen zusammen. Der neuste Plan **High Security Business Network (HSBN) vNext Beta** basiert auf der Codebasis von Hyperledger Fabric v1.0 und nutzt eine modulare Architektur für die Bereitstellung neuer Funktionen. Mit IBM Blockchain on Bluemix-Plänen können Entwickler Chaincode-Anwendungen sofort schreiben und testen, ohne ein privates Blockchain-Netz entwerfen und konfigurieren zu müssen. Chaincode ist die treibende Kraft hinter dem sicheren und effizienten Austausch von Assets in Fabric-Blockchain-Netzen sowie der ständigen Aufzeichnung dieser Transaktionen im entsprechenden Konto.

## Angebotspläne

Neue IBM Blockchain on Bluemix-Subskribenten können sich jetzt beim **HSBN vNext Beta**-Plan registrieren. Dieses aktuelle Angebot basiert auf Hyperledger Fabric Version 1.0, das Sicherheit, Integrität, Skalierbarkeit und Leistung der nächsten Generation bereitstellt. In Tabelle 1 sind die Bluemix-Pläne beschrieben:

Tabelle 1: IBM Blockchain on Bluemix-Pläne  

| Bluemix Plan      | Status       | Verfügbar für neue Subskribenten  | Hyperledger Fabric Version
| ------------------------- |:--------------------------:|:-----:|:-----:|
| **HSBN vNext Beta** (1)   | Betaversion     | Ja |  v1.0 |
| HSBN (2) |  Allgemein verfügbar |  Ja |  v0.6 |
| Starter Developer (3)    | Betaversion     | Ja | v0.6 |

(1) Vom **High Security Business Network (HSBN) vNext Beta**-Plan wird ein einfacher Mechanismus für den Beitritt zu einer Bluemix-Organisation und für die Erstellung eines verteilten Blockchain-Netzes bereitgestellt.  
(2) Vom **High Security Business Network (HSBN) GA**-Plan wird eine Single-Tenant-LinuxONE on z Systems-Hochsicherheitsumgebung mit Codeisolation unter Verwendung von [IBM Secure Service Container](etn_ssc.html) bereitgestellt.  
(3) Vom **Starter Developer Beta**-Plan wird eine Multi-Tenant-Umgebung nur für die Entwicklung bereitgestellt.  

## Details zu Angebotsplänen

Tabelle 2 enthält einen detaillierten Vergleich der IBM Blockchain on Bluemix-Angebotspläne. Neue IBM Blockchain on Bluemix-Subskribenten müssen den **HSBN vNext Beta**-Plan auswählen. Der HSBN- und der Starter Developer-Plan stehen neuen Subskribenten nicht zur Verfügung, werden jedoch von IBM weiter unterstützt:

Tabelle 2: Details zu IBM Blockchain on Bluemix-Plänen  

| Bluemix-Plan:      | Starter Developer-Netz       | High Security Business Network       | High Security Business Network (HSBN) vNext Beta
| ------------------------- |:--------------------------:|:-----:|:-----:|
| Status:    | Betaversion     | Allgemein verfügbar | Betaversion |
| Zweck:  |  Entwicklung und Teststufen für Sicherheit, Leistung und Verfügbarkeit |  Simulation eines Unternehmensnetzes und Teststufen für Sicherheit, Leistung und Verfügbarkeit |  Einrichten eines Unternehmensnetzes mit Sicherheit, Leistung und Verfügbarkeit auf Produktionsebene |
| Knoten:    | 4 Peers + Zertifizierungsstelle     | 4 Peers + Zertifizierungsstelle | Dynamische Verwaltung von Netzkomponenten |
| Dashboard-Überwachung: | [Ja](ibmblockchainmonitor.html) | [Ja](ibmblockchainmonitor.html) | [Ja](v10_dashboard.html) |
| Umgebung:     | Gemeinsame Multi-Tenant | Isolierte Single-Tenant | Mehrere Isolationsstufen |

# Zugehörige Links
{: #rellinks}
## Lernprogramme und Beispiele
{: #samples}
* [IBM Marbles-Demo (GitHub)](https://github.com/IBM-Blockchain/marbles) - v0.6 & v1.0
* [IBM Wertpapaier-Demo (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme) - v0.6
* [IBM Autoleasing-Demo (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) - v0.6
* [Kunstauktion-Demo (Github)](https://github.com/ITPeople-Blockchain/auction) v0.6 - v1.0 (wird lokal ausgeführt)

## API-Referenz
{: #api}
* [Hyperledger Fabric-API (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC-SDK für Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## Zugehörige Links
{: #general}
* [Fabric-Code](https://github.com/hyperledger/fabric)
* [Fabric-Composer](https://fabric-composer.github.io/)
* [Dokumente zu Fabric v1.0](http://hyperledger-fabric.readthedocs.io/en/latest/)
* [Dokumente zu Fabric v0.6](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Neuerungen in Bluemix-Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
