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

Um eine App mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Die Beispielapp [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung mit einem {{site.data.keyword.composeForElasticsearch}}-Service mithilfe der Berechtigungsnachweise. 

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
{: caption="Tabelle 1. Compose for Elasticsearch - Berechtigungsnachweise" caption-side="top"}

**Hinweis:** Zwei `haproxy`-Portale bieten Zugriff auf den Elasticsearch-Cluster. Sowohl `uri` als auch `uri_direct_1` können für die Verbindung zum Cluster verwendet werden. In Ihrer Anwendung wechseln Sie zwischen `uri` und `uri_direct_1`, um die Reaktionen auf Verbindungsfehler zu verwalten.
