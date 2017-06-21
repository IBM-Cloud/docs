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

Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispielapp [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung mit einem {{site.data.keyword.composeForRedis}}-Service mithilfe der Berechtigungsnachweise. 

Feldname|Beschreibung
----------|-----------
`uri`|Der bei der Verbindungsherstellung zum Service zu verwendende URI, in dem Folgendes enthalten ist: das Schema (redis:), Benutzername und Kennwort des Administrators, der Hostname des Servers und die Nummer des Ports, zu dem die Verbindung hergestellt werden soll.
`uri_cli`|Eine `redis-cli`-Befehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `redis`.
`name`|Der Name der Datenbankimplementierung.
{: caption="Tabelle 1. Compose for Redis - Berechtigungsnachweise" caption-side="top"}
