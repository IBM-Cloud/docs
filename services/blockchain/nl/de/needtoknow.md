---

copyright:
  years: 2017
lastupdated: "2017-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Haftungsausschluss
{: #etn_overview}

**ACHTUNG:** Sie müssen die folgenden Informationen überprüfen, bevor Sie einen Plan für IBM Blockchain on Bluemix verwenden können.

## IBM Support-Aussage

IBM ist seit langem führend in der Innovation und setzt dies mit den Angebotsplänen von IBM Blockchain on Bluemix fort. Die sich schnell weiterentwickelnde Blockchain-Technologie wird in einer Reihe von Branchen von der Finanzwirtschaft über Lieferketten bis hin zur Logistik zu durchgreifenden Änderungen führen. Durch verschiedene Early-Adoption-Programme haben IBM Kunden und Business Partner aktiv Blockchain als eine Branchenlösung vorangetrieben. IBM Blockchain on Bluemix ist eines dieser Programme. **Wie bei jeder neuen Technologie sollten sich Benutzer von IBM Blockchain on Bluemix einer raschen Abfolge von grundlegenden Änderungen bewusst sein**.  
{:shortdesc}

IBM Blockchain stützt sich auf die Architektur des Hyperledger Fabric Projects der Linux Foundation. Fabric befindet sich gegenwärtig im Stadium *Active* und wird ständig weiterentwickelt. Jeder Beitrag der Open-Source-Community verbessert Hyperledger Fabric, kann jedoch im Hinblick auf die Akzeptanz eine Herausforderung darstellen. Während Fabric den Projektzyklus *Active* durchläuft, können Clients Hyperledger Fabric Version 1.0 für Netztests und -simulationen verwenden. **IBM warnt vor dem direkten Definieren oder Austauschen von Finanzanlagen oder anderen Assets in einem Blockchain-Netz**.  

## Open-Source-Aussage

Der **High Security Business Network (HSBN) vNext Beta**-Plan basiert auf dem Open-Source-Code von Hyperledger Fabric Version 1.0 der Linux Foundation. Der Starter Developer- und der High Security Business Network-Plan (HSBN) basieren auf dem Code von Hyperledger Fabric Version 0.6. Hyperledger Project-Mitglieder, einschließlich IBM, tragen weiterhin zum Quellcode bei; danach wird er von der Community überprüft, untersucht und getestet.
Hyperledger Fabric Version 1.0 befindet sich gegenwärtig im Stadium *Active*; Details zu diesem Stadium sowie zum Lebenszyklus des Hyperledger Projects sind unter 'https://wiki.hyperledger.org/community/project-lifecycle' verfügbar.  

## Support-Aussage für Chaincode

Die folgenden Programmierpraktiken werden in IBM Blockchain-Netzen NICHT unterstützt:

1. Verwendung von assoziativen Feldgruppen mit Iteration (Reihenfolge ist in Go randomisiert).
2. Lesen einer Liste von Einträgen aus einer KVS-Tabelle (Reihenfolge ist nicht garantiert).
3. Schreiben von nicht threadsicherem Chaincode (Abfrage und Aufruf können parallel erfolgen).
4. Ersetzen von globalem Hauptspeicher oder Cachespeicher für Hauptbuchstatusvariablen im Chaincode.
5. Direkter Zugriff auf externe Services wie Datenbanken aus dem Chaincode.
6. Verwendung von Bibliotheken oder globalen Variablen, die zu Nichtdeterminismus führen könnten (z. B. "random" oder "time").
7. Iteration mit GetRows.  

Zudem wird vom HSBN- und vom Starter-Plan (Hyperledger Fabric v0.6) nicht deterministischer Chaincode nicht unterstützt, der für die Datenkonsistenz und Integrität ein Risiko darstellt; Details hierzu finden Sie im Abschnitt zu [nicht deterministischem Chaincode](nondeterministic.html).
