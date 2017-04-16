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

# Einführung in Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB ist ursprünglich ein Ersatz für die verteilte Wide Column-Cassandra-Datenbank. ScyllaDB ist für eine bessere Ressourcennutzung, die zu einer zehnmal besseren Benchmarkleistung führen kann, in C++ geschrieben, nicht wie Cassandra in Java. ScyllaDB behält nicht nur die Kompatibilität mit Cassandra-Tools und Datendateien bei, sondern fügt auch Funktionen zur automatischen Leistungsoptimierung hinzu. Mithilfe von {{site.data.keyword.composeForScyllaDB_full}} werden die Funktionen von ScyllaDB dahingehend erweitert, dass die Verwaltung für Sie übernommen wird und Sie ein einfaches Bereitstellungssystem zur automatischen Skalierung für eine hohe Verfügbarkeit und Redundanz sowie automatisierte Backups angeboten bekommen.
{:shortdesc}

**Anmerkung:** {{site.data.keyword.composeForScyllaDB_full}} gewährt keinen Zugriff auf die Compose-Benutzerschnittstelle. Weitere Details finden Sie unter [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support).

Führen Sie zum Einstieg in {{site.data.keyword.composeForScyllaDB}} die folgenden Schritte aus:

1. [Erstellen Sie eine {{site.data.keyword.composeForScyllaDB}}-Instanz](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   Wenn Sie eine Instanz des Service erstellen, wählen Sie sowohl einen Namen für den Service als auch einen Namen für den Berechtigungsnachweis aus. Lassen Sie den Service ungebunden; Sie können später eine Anwendung mit Ihrem Service verbinden, indem Sie die Berechtigungsnachweise verwenden, die bei der Bereitstellung des Service angegeben wurden. Die verschiedenen Werte für die Berechtigungsnachweise sind im Abschnitt "Verfügbare Berechtigungsnachweise" aufgeführt.

2. Stellen Sie eine Verbindung zu Ihrem {{site.data.keyword.composeForScyllaDB}}-Service her.

   Um eine Anwendung mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden.

   Laden Sie die Beispielanwendung [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung der Bluemix-Konsole auf **App anzeigen**.

   Die Beispielanwendung veranschaulicht die Verwendung von Node.js zur Verbindung mit einem {{site.data.keyword.composeForScyllaDB}}-Service.


## Verfügbare Berechtigungsnachweise

Feldname|Beschreibung
----------|-----------
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `scylla`.
`uri_cli_1`|Eine alternative `cqlsh`-Shellbefehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`maps`|Eine ScyllaDB-Verbindungskarte, die die Informationen bereitstellt, die verschiedene Treiber zur Zuordnung interner IP-Adressen zu externen DNS-Namen einer ScyllaDB-Datenbank benötigen.
`name`|Der Name der Datenbankimplementierung.
`uri_cli`|Eine `cqlsh`-Shellbefehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`uri_direct_2`|Ein alternativer URI, der bei der Verbindungsherstellung zum Service verwendet werden kann. Format wie für `uri`.
`uri_direct_1`|Ein alternativer URI, der bei der Verbindungsherstellung zum Service verwendet werden kann. Format wie für `uri`.
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum geeigneten Server herstellt. Das Zertifikat ist base64-codiert.
`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.
`uri_cli_2`|Eine alternative `cqlsh`-Shellbefehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`uri`|Die bei der Herstellung einer Verbindung zum Service verwendete URI, die Folgendes enthält: Schema (`scylla:`), Kennwort, Hostname des Servers, Portnummer für die Verbindungsherstellung und Datenbankname.
{: caption="Table 1. {{site.data.keyword.composeForScyllaDB}} - Berechtigungsnachweise" caption-side="top"}


# Zugehörige Links
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose-Artikel](https://www.compose.com/articles/){:new_window}

## Lernprogramme und Beispiele
{: #samples}
* [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs){:new_window}

## Zugehörige Links
{: #general}
* [Compose-Hilfe](https://help.compose.com/docs){:new_window}
