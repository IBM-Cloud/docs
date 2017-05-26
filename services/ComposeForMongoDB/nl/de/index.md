---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in Compose for MongoDB
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} verwendet die leistungsfähige Indexierung und Abfrage, die Aggregation und die breite Treiberunterstützung von MongoDB, die es zum gefragtesten JSON-Datenspeicher für viele Startup- und etablierte Unternehmen gemacht haben. {{site.data.keyword.composeForMongoDB}} bietet ein einfaches, selbstskalierendes Bereitstellungssystem. Es bietet hohe Verfügbarkeit und Redundanz, automatisierte und anforderungsbasierte dauerhaft aktive Sicherungsfunktionen, Überwachungstools, Integration in Warnsysteme, Ansichten für die Leistungsanalyse und vieles mehr, alles in einer übersichtlichen, leicht zu bedienenden Benutzerschnittstelle.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in {{site.data.keyword.composeForMongoDB}} die folgenden Schritte aus:

1. [Erstellen Sie eine {{site.data.keyword.composeForMongoDB}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/).

   Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden.  Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForMongoDB}}-Service her.

   Zur Herstellung einer Verbindung von einer App zu Ihrem Service verwenden Sie die [Berechtigungsnachweise](./credentials.html), die zusammen mit dem Service erstellt werden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForMongoDB}}-Service.

   Laden Sie die Beispiel-App [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**.
