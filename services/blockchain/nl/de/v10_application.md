---

copyright:
  years: 2017
lastupdated: "2017-03-17"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Anwendungsentwicklung
{: #v10_dashboard}


Verwenden Sie den Beispiel-Chaincode 'marbles02' und die entsprechende JavaScript-App als Vorlage zum Erstellen Ihrer eigenen Geschäftslösung.
{:shortdesc}


Die App nutzt die Node.js-SDK-APIs für die Interaktion mit den bereitgestellten Netzkomponenten und gibt den Peer als Ziel für Transaktionsanforderungen an. Suchen Sie die API-Endpunkte für den Peer, die Zertifizierungsstelle und den Anordnungsservice für das Netz auf der Registerkarte **Serviceberechtigungsnachweise** in der Anzeige **Ressourcen** der Überwachung und speichern Sie diese Zeichenfolgen in einer Konfigurationsdatei als Teil der App. Beachten Sie jedoch, dass Sie bei der Auswahl zusätzlicher Peers im Netz als Ziel (dies ist der Fall, wenn Sie die Bewilligung eines Peers benötigen, der nicht Ihrer Organisation angehört) die korrekten API-Endpunkte für diese Peers abrufen müssen. Außerdem müssen Sie die Zertifikate der Zertifizierungsstelle für die andere Organisation speichern, um Antworten überprüfen zu können, die an Ihre Anwendung zurückgegeben werden. Diese Informationen werden in der Ansicht **Ressourcen** nicht angezeigt. Sie müssen sich daher an den entsprechenden Administrator der Bluemix-Organisation wenden und diese Daten mit einer externen Operation anfordern. Die URL des Anordnungsservice ist für das gesamte Netz gültig; Sie benötigen keinerlei mitgliedsspezifische Informationen für diese Komponente.  

Im [Marbles](https://github.com/IBM-Blockchain/marbles/tree/v3.0)-GitHub-Repository finden Sie den Quellcode und die entsprechenden Voraussetzungen. Befolgen Sie die Anweisungen in der Readme-Datei und aktivieren Sie Ihre App.  

Untersuchen Sie das [SDK-Repository](https://github.com/hyperledger/fabric-sdk-node), um probehalber einige durchgängige Test durchzuführen und sich so mit den APIs vertraut zu machen.
