---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in IBM {{site.data.keyword.blockchain}}
{: #gettingstartedtemplate}
Letzte Aktualisierung: 10. November 2016
{: .last-updated}

**ACHTUNG:** Lesen Sie vor Verwendung des Starter Developer-Plans (Betaversion) oder des High Security Business Network-Plans (allgemein verfügbar) unbedingt die technischen Angaben und Unterstützungsinformationen unter [Was Sie wissen müssen](needtoknow.html).
<br><br>

## Status der Pläne im Produktangebot

Der Starter Developer-Plan ist eine Betaversion und stellt eine Multi-Tenant-Entwicklungsumgebung bereit. Der High Security Business Network-Plan ist ein GA-Release. Vom High Security Business Network-Plan wird eine Single-Tenant-LinuxONE on z-Hochsicherheitsumgebung mit Codeisolation unter Verwendung von [IBM Secure Service Container](etn_ssc.html) bereitgestellt.
<br><br>

## IBM Blockchain on Bluemix

Der {{site.data.keyword.blockchainfull}}-Service in Bluemix&reg; stellt beim Klicken auf eine Schaltfläche folgende Auswahlmöglichkeiten zur Verfügung: zwei aus vier Knoten bestehende Blockchain-Netze zum Entwickeln und Testen. Anstatt ein Netz völlig neu erstellen zu müssen, können Entwickler unverzüglich mit dem Schreiben der Anwendungen und Bereitstellen von Chaincode beginnen. Der IBM Blockchain on Bluemix-Service ist ein genehmigtes Peer-to-Peer-Netz (mit Berechtigungen), das auf  [Hyperledger Fabric v0.6.1](https://github.com/hyperledger/fabric/tree/v0.6)-Code aus dem Hyperledger Project der Linux Foundation aufbaut.
{:shortdesc}

Blockchain-Netze werden zum sicheren und effizienten Austauschen und Verfolgen digitaler Assets sowie zum permanenten Aufzeichnen aller Transaktionen im Shared Ledger verwendet. Details zu Blockchain finden Sie im Abschnitt [Informationen zu Blockchain](ibmblockchain_overview.html).
<br><br>

## Netzplan auswählen

Sie haben die Wahl zwischen zwei IBM Blockchain on Bluemix-Plänen: Dem **Starter-Entwicklernetz** und dem **Unternehmensnetz mit hohem Sicherheitsniveau**. Welche Umgebung für Sie die richtig ist, können Sie aus dem folgenden Vergleichsdiagramm entnehmen.

<!-- Commenting our for move to GA status jh 10/07/16
![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html). -->

| Bluemix-Plan:      | Starter-Entwicklernetz       | Unternehmensnetz mit hohem Sicherheitsniveau
| ------------------------- |:--------------------------:|:-----:|
| Status:    | Betaversion     | Allgemein verfügbar |
| Zweck:  |  Entwicklung und Teststufen für Sicherheit, Leistung und Verfügbarkeit |  Simulation eines Unternehmensnetzes und Teststufen für Sicherheit, Leistung und Verfügbarkeit |
| Knoten:    | 4 Knoten + Zertifizierungsstelle     | 4 Knoten + Zertifizierungsstelle |
| [Dashboard-Überwachung:](ibmblockchainmonitor.html) | Ja | Ja |
| Vertrauliche Transaktionen | Ja | Ja |
| [Konsens:](etn_pbft.html) | PBFT | PBFT |
| Umgebung:     | Gemeinsame Multi-Tenant | Isolierte Single-Tenant |
| [IBM Secure Service Container:](etn_ssc.html) | Nein | Ja |

<br>
## Netzplan starten

Führen Sie die folgenden Schritte aus, um eine nicht gebundene Serviceinstanz des Blockchain-Netzes zu erstellen und bereitzustellen.  Das Netz umfasst eine Entwicklungsumgebung mit validierenden Knoten und einen Sicherheitsservice; es ermöglicht das Bereitstellen von Chaincode, Anzeigen von Protokollen und Erstellen von Anwendungen:

1. Füllen Sie auf der Seite [{{site.data.keyword.blockchain}}-Service](https://console.ng.bluemix.net/catalog/services/blockchain/) das Formular **Service hinzufügen** im rechten Teilfenster:
  - **Bereich:** Wählen Sie **dev** aus.
  - **App:** Wählen Sie entweder **Nicht binden** oder zum Binden des Service an eine der Bluemix.org-Anwendungen **Anwendung auswählen** aus.
  - **Servicename:** Geben Sie einen eindeutigen Namen oder Wert ein, zum Beispiel **Blockchain Test Net123**.
  - **Berechtigungsnachweisname:** Lassen Sie den Standardwert unverändert.
  - **Ausgewählter Plan:** Wählen Sie **Starter-Entwickler** oder **Hohes Sicherheitsniveau** aus.
  - Klicken Sie auf die Schaltfläche **Erstellen**.
2.  Sie befinden sich jetzt in der Anzeige **Service-Dashboard** für den neuen Service. In dieser Anzeige können Sie Ihre Instanz des Netzes **verwalten**; klicken Sie auf **STARTEN**, um die Blockchain-Überwachung zu verwenden.
3.  In der Blockchain-Überwachung werden Netzdetails, Live-Protokolle, der aktuelle Hauptbuchstatus, APIs und Chaincode-Vorlagen angezeigt. Im Dashboard können Sie die folgenden Funktionen verwenden:
  - Auf die Routen für Erkennung und APIs für Netzpeers zugreifen.
  - Aktive Chaincode-Container anzeigen.
  - Echtzeit-Protokolle anzeigen und Chaincode-Fehler beheben.
  - Globalen Status für das Hauptbuch anzeigen.
  - Auf Swagger-Benutzerschnittstelle zugreifen und mit Netz über REST-API interagieren.
  - Eines der drei Chaincode-Beispiele bereitstellen.


# Zugehörige Links
{: #rellinks}
## Lernprogramme und Beispiele
{: #samples}
* [IBM Marbles-Demo (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [IBM Wertpapier-Demo (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [IBM Autoleasing-Demo (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [Kunstauktion-Demo (Github)](https://github.com/ITPeople-Blockchain/auction)

## API-Referenz
{: #api}
* [Swagger-Benutzerschnittstelle](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [Hyperledger Fabric-API (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC-SDK für Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## Zugehörige Links
{: #general}
* [Fabric-Code](https://github.com/hyperledger/fabric)
* [Whitepaper](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [Protocol Specification & Zugehörige Dokumente](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [Neuerungen in Bluemix-Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
