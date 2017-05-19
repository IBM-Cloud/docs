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

# Credenziali disponibili
{: #available-credentials}

Per collegare un'applicazione al tuo servizio, utilizza le credenziali create insieme al servizio. L'applicazione di esempio [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForRedis}} utilizzando le credenziali.

Nome campo|Descrizione
----------|-----------
`uri`|L'URI da utilizzare quando esegui il collegamento al servizio, include lo schema (redis:), il nome utente e la password amministratore, il nome host del server e il numero di porta a cui collegarsi.
`uri_cli`|Una riga di comando `redis-cli` che esegue il collegamento all'istanza del database.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`db_type`|Il tipo di database offerto dal servizio; in questo caso `redis`.
`name`|Il nome di distribuzione del database.
{: caption="Tabella 1. Credenziali di Compose for Redis" caption-side="top"}
