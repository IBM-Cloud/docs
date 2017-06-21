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

Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispielapp [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung mit einem {{site.data.keyword.composeForMySQL}}-Service mithilfe der Berechtigungsnachweise. 

Feldname|Beschreibung
----------|-----------
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `mysql`.
`name`|Der Name der Datenbankimplementierung.
`uri_cli`|Eine `mysql`-Shellbefehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum geeigneten Server herstellt. Das Zertifikat ist base64-codiert.
`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.
`uri`|Die bei der Herstellung einer Verbindung zum Service verwendete URI, die Folgendes enthält: Schema (`mysql:`), Benutzername und Kennwort des Administrators, Hostname des Servers sowie die Nummer des Ports, zu dem die Verbindung hergestellt werden soll, und der vhost-Name.
{: caption="Tabelle 1. Compose for MySQL - Berechtigungsnachweise" caption-side="top"}
