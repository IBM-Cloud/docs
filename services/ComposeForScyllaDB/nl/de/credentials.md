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

# Verfügbare Berechtigungsnachweise
{: #available-credentials}

Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispielapp [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung mit einem {{site.data.keyword.composeForScyllaDB}}-Service mithilfe der Berechtigungsnachweise. 

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
{: caption="Tabelle 1. Compose for ScyllaDB - Berechtigungsnachweise" caption-side="top"}
