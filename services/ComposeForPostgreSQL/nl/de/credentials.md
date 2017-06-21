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

Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispielapp [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung mit einem {{site.data.keyword.composeForPostgreSQL}}-Service mithilfe der Berechtigungsnachweise. 

Feldname|Beschreibung
----------|-----------
`uri`|Der URI, der bei der Verbindungsherstellung zum Service verwendet werden soll. Enthält das Schema (`postgres:`), Administrator-Benutzernamen und Kennwort, den Hostnamen des Servers, die Nummer des Ports, zu dem die Verbindung hergestellt werden soll, den Datenbanknamen sowie "?ssl=true" zur Ermöglichung von SSL-Verbindungen.
`uri_cli`|Eine `psql`-Shellbefehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum geeigneten Server herstellt. Dieses ist base64-codiert. Vor seiner Verwendung muss es decodiert werden, wie in der Beispielanwendung gezeigt.
`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `postgresql`.
`name`|Der Name der Datenbankimplementierung.
{: caption="Tabelle 1. Compose for PostgreSQL - Berechtigungsnachweise" caption-side="top"}
