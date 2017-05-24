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

# Einführung in Compose for RethinkDB
{: #getting-started-with-compose-for-rethinkdb}

{{site.data.keyword.composeForRethinkDB}} bietet Ihnen eine JSON-Dokument-basierte verteilte Datenbank mit integrierter Verwaltung und einer Untersuchungskonsole. RethinkDB verwendet die ReQL-Abfragesprache, die um Funktionsketten aufgebaut ist und in Clientbibliotheken für Java, JavaScript, Python und Ruby zur Verfügung steht. Mit ReQL besteht die Möglichkeit, serverseitige Funktionen von RethinkDB wie z. B. verteilte Joins und Unterabfragen über Clusterknoten hinweg zu verwenden. RethinkDB unterstützt außerdem sekundäre Indizes für eine bessere Lese-Abfrageleistung. Die leistungsfähigste Funktion von RethinkDB, Changefeeds, ermöglicht die Umwandlung vieler ReQL-Abfragen in Echtzeit-Feeds.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in {{site.data.keyword.composeForRethinkDB}} die folgenden Schritte aus.

1. [Erstellen Sie eine {{site.data.keyword.composeForRethinkDB}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/).

  Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden. Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForRethinkDB}}-Service her.

   Zur Herstellung einer Verbindung von einer App zu Ihrem Service verwenden Sie die [Berechtigungsnachweise](./credentials.html), die zusammen mit dem Service erstellt werden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForRethinkDB}}-Service.

   Laden Sie die Beispiel-App [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**.
