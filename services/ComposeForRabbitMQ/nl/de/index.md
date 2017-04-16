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

# Einführung in {{site.data.keyword.composeForRabbitMQ}}
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ verarbeitet asynchron die Nachrichten zwischen Ihren Anwendungen und Datenbanken und ermöglicht damit die Trennung der Daten und Anwendungsebenen. Mit RabbitMQ haben Entwickler die Möglichkeit, Nachrichten mit anpassbaren Persistenzstufen, Bereitstellungseinstellungen und bestätigter Veröffentlichung weiterzuleiten, zu verfolgen und in die Warteschlange zu stellen. Durch die Verwendung von {{site.data.keyword.composeForRabbitMQ_full}} erhalten Sie Zugriff auf die leicht zu bedienende Verwaltungsschnittstelle mit einer Vielzahl von Verwaltungsfunktionen, wie z. B. Bereitstellungsüberwachung, Skalierung mit einem Mausklick, Benutzereinrichtung und Zugriff auf Protokolldateien.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in {{site.data.keyword.composeForRabbitMQ}} die folgenden Schritte aus.

1. [Erstellen Sie eine {{site.data.keyword.composeForRabbitMQ}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden.  Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForRabbitMQ}}-Service her.

  Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForRabbitMQ}}-Service.

  Laden Sie die Beispiel-App [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**.

## Verfügbare Berechtigungsnachweise

Feldname|Beschreibung
----------|-----------
``uri``|Der URI, der bei der Verbindungsherstellung zum Service verwendet werden soll. Enthält das Schema (`amqps:), Administrator-Benutzernamen und Kennwort, den Hostnamen des Servers, die Nummer des Ports, zu dem die Verbindung hergestellt werden soll, sowie den Namen des virtuellen Hosts.
`uri_direct_1`|Ein alternativer URI, der bei der Verbindungsherstellung zum Service verwendet werden kann. Format wie für `uri`.
`uri_admin`|Ein URI, der in einem Browser besucht werden sollte, um Zugriff auf die Verwaltungsschnittstelle der Datenbank zu erhalten. Für den Zugriff sind Benutzername und Kennwort des Administrators aus dem Feld `uri` erforderlich.
`uri_admin_1`|Ein alternativer Verwaltungs-URI, siehe `uri_admin`.
`uri_admin_2`|Ein alternativer Verwaltungs-URI, siehe `uri_admin`.
`uri_admin_3`|Ein alternativer Verwaltungs-URI, siehe `uri_admin`.
`uri_admin_4`|Ein alternativer Verwaltungs-URI, siehe `uri_admin`.
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum geeigneten Server herstellt. Dieses ist base64-codiert. Vor seiner Verwendung muss es decodiert werden, wie in der Beispielanwendung gezeigt.
`deployment_id`|Eine interne ID für den Service, wie in Compose erstellt.
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `rabbitmq`.
`name`|Der Name der Datenbankimplementierung.
{: caption="Table 1. {{site.data.keyword.composeForRabbitMQ}} - Berechtigungsnachweise" caption-side="top"}

# Zugehörige Links
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose-Artikel](https://www.compose.com/articles/){:new_window}

## Lernprogramme und Beispiele
{: #samples}
[compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs){:new_window}

## Zugehörige Links
{: #general}
* [Compose-Hilfe](https://help.compose.com/docs){:new_window}
