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

# Einführung in Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} vereint die Leistung einer Engine für die Volltextsuche mit den Indexierungsfähigkeiten einer JSON-Dokument-Datenbank. Gemeinsam bilden sie ein leistungsfähiges Tool zur Analyse komplexer Daten bei großen Datenvolumen. Mit Elasticsearch kann Ihre Suche mit Genauigkeits-Scores bewertet werden, was es Ihnen ermöglicht, Ihren Datensatz nach diesen jeweils größten Übereinstimmungen und Beinahe-Treffern zu durchsuchen, die Sie sonst überspringen würden.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in {{site.data.keyword.composeForElasticsearch}} die folgenden Schritte aus:

1. [Erstellen Sie eine {{site.data.keyword.composeForElasticsearch}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/).

  Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden. Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForElasticsearch}}-Service her.

  Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForElasticsearch}}-Service.

  Laden Sie die Beispiel-App [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**, um den Inhalt des Index *examples* anzuzeigen.

## Verfügbare Berechtigungsnachweise

Feldname|Beschreibung
----------|-----------
`uri`|Der URI, der bei der Verbindungsherstellung zum Service verwendet werden soll. Enthält das Schema (`https:`), Administrator-Benutzernamen und Kennwort, den Hostnamen und die Nummer des Ports, zu dem die Verbindung hergestellt werden soll.
`uri_direct_1`|Ein alternativer URI, der bei der Verbindungsherstellung zum Service verwendet werden kann. Format wie für `uri`.
`uri_health`|Ein `curl`-Befehl, der vom ersten HAProxy Informationen zum Clusterstatus anfordert.
`uri_health_1`|Ein `curl`-Befehl, der vom zweiten HAProxy Informationen zum Clusterstatus anfordert.
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum geeigneten Server herstellt. Dieses ist base64-codiert. Vor seiner Verwendung muss es decodiert werden, wie in der Beispielanwendung gezeigt.
`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `elastic_search`.
`name`|Der Name der Datenbankimplementierung.
{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} - Berechtigungsnachweise" caption-side="top"}

**Hinweis:** Zwei `haproxy`-Portale bieten Zugriff auf den Elasticsearch-Cluster. Sowohl `uri` als auch `uri_direct_1` können für die Verbindung zum Cluster verwendet werden. In Ihrer Anwendung wechseln Sie zwischen `uri` und `uri_direct_1`, um die Reaktionen auf Verbindungsfehler zu verwalten.

# Zugehörige Links
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose-Artikel](https://www.compose.com/articles/){:new_window}

## Lernprogramme und Beispiele
{: #samples}
* [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs){:new_window}

## Zugehörige Links
{: #general}
* [Compose-Hilfe](https://help.compose.com/docs){:new_window}
