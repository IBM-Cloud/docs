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

# Einführung in {{site.data.keyword.composeForRedis}}
{: #getting-started-with-compose-for-redis}

Redis ist ein speicherinterner Open-Source-Schlüssel/Wert-Speicher. Die Werte in Redis können einfache Zeichenfolgen, Hashwerte, Listen und Gruppen oder leistungsfähige Bitmapdateien, HyperLOG-Protokolle und geografisch-räumliche Indizes sein. Redis eignet sich ideal als Anwendungscache oder als Datenspeicher für schnelle Antworten. {{site.data.keyword.composeForRedis_full}} bietet Ihnen eine Konfiguration, die für hohe Verfügbarkeit und persistente Plattenspeicherung voreingestellt ist, alles mit speziellen Sicherheitsfunktionen gesichert.
{:shortdesc}

**Hinweis:** Alle Compose-Serviceinstanzen, die vor dem 14. September 2016 bereitgestellt wurden und noch aktiv sind, können weiterhin verwendet werden und sind über [https://www.compose.com/](https://www.compose.com) zugänglich. Jede Compose-Serviceinstanz, die ab diesem Punkt bereitgestellt wird, ist direkt über Ihr Bluemix-Konto zugänglich und kann dort verwendet werden.

Führen Sie zum Einstieg in {{site.data.keyword.composeForRedis}} die folgenden Schritte aus.

1. [Erstellen Sie eine {{site.data.keyword.composeForRedis}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-redis/).

  Wenn Sie eine Instanz des Service erstellen, achten Sie darauf, sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis auszuwählen. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden. Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt *Verfügbare Berechtigungsnachweise* aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForRedis}}-Service her.

  Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispiel-App veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForRedis}}-Service.

  Laden Sie die Beispiel-App [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in Bluemix auf **App anzeigen**.

## Verfügbare Berechtigungsnachweise

Feldname|Beschreibung
----------|-----------
`uri`|Der bei der Verbindungsherstellung zum Service zu verwendende URI, in dem Folgendes enthalten ist: das Schema (redis:), Benutzername und Kennwort des Administrators, der Hostname des Servers und die Nummer des Ports, zu dem die Verbindung hergestellt werden soll.
`uri_cli`|Eine `redis-cli`-Befehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`deployment_id`|Eine interne ID für den Service, wie in Compose erstellt.
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `redis`.
`name`|Der Name der Datenbankimplementierung.
{: caption="Table 1. {{site.data.keyword.composeForRedis}} - Berechtigungsnachweise" caption-side="top"}

# Zugehörige Links
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose-Artikel](https://www.compose.com/articles/){:new_window}

## Lernprogramme und Beispiele
{: #samples}
* [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs){:new_window}

## Zugehörige Links
{: #general}
* [Compose-Hilfe](https://help.compose.com/docs){:new_window}
