---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in {{site.data.keyword.composeForRethinkDB}}
{: #getting-started-with-compose-for-rethinkdb}

{{site.data.keyword.composeForRethinkDB}} bietet Ihnen eine JSON-Dokument-basierte verteilte Datenbank mit integrierter Verwaltung und einer Untersuchungskonsole. RethinkDB verwendet die ReQL-Abfragesprache, die um Funktionsketten aufgebaut ist und in Clientbibliotheken für Java, JavaScript, Python und Ruby zur Verfügung steht. Mit ReQL besteht die Möglichkeit, serverseitige Funktionen von RethinkDB wie z. B. verteilte Joins und Unterabfragen über Clusterknoten hinweg zu verwenden. RethinkDB unterstützt außerdem sekundäre Indizes für eine bessere Lese-Abfrageleistung. Die leistungsfähigste Funktion von RethinkDB, Changefeeds, ermöglicht die Umwandlung vieler ReQL-Abfragen in Echtzeit-Feeds.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in {{site.data.keyword.composeForRethinkDB}} die folgenden Schritte aus.

1. [Erstellen Sie eine {{site.data.keyword.composeForRethinkDB}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/).

  Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden. Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForRethinkDB}}-Service her.

   Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForRethinkDB}}-Service.

   Laden Sie die Beispiel-App [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**.

## Verfügbare Berechtigungsnachweise

Feldname|Beschreibung
----------|-----------
`uri`|Der URI, der bei der Verbindungsherstellung zum Service verwendet werden soll. Enthält das Schema (rethinkdb:), Benutzernamen und Kennwort des Administrators, den Hostnamen des Servers sowie die Nummer des Ports, zu dem die Verbindung hergestellt werden soll.
`uri_admin`|Ein URI, der in einem Browser besucht werden sollte, um Zugriff auf die Verwaltungsschnittstelle der Datenbank zu erhalten. Für den Zugriff sind Benutzername und Kennwort des Administrators aus dem Feld `uri` erforderlich.
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum geeigneten Server herstellt. Dieses ist base64-codiert. Vor seiner Verwendung muss es decodiert werden, wie in der Beispielanwendung gezeigt.
`deployment_id`|Eine interne ID für den Service, wie in Compose erstellt.
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `rethink`.
`name`|Der Name der Datenbankimplementierung.
{: caption="Table 1. {{site.data.keyword.composeForRethinkDB}} - Berechtigungsnachweise" caption-side="top"}

# Zugehörige Links
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose-Artikel](https://www.compose.com/articles/){:new_window}

## Lernprogramme und Beispiele
{: #samples}
* [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs){:new_window}

## Zugehörige Links
{: #general}
* [Compose-Hilfe](https://help.compose.com/docs){:new_window}
