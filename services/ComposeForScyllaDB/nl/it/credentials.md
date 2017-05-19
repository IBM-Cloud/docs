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

Per collegare un'applicazione al tuo servizio, utilizza le credenziali create insieme al servizio. L'applicazione di esempio [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForScyllaDB}} utilizzando le credenziali.

Nome campo|Descrizione
----------|-----------
`db_type`|Il tipo di database offerto dal servizio, in questo caso `scylla`.
`uri_cli_1`|Una riga di comando shell `cqlsh` alternativa che esegue il collegamento all'istanza del database.
`maps`|Un'associazione di connessione ScyllaDB che fornisce le informazioni necessarie ai vari driver per associare gli indirizzi IP interni con i nomi DNS esterni di un database ScyllaDB.
`name`|Il nome di distribuzione del database.
`uri_cli`|Una riga di comando shell `cqlsh` che esegue il collegamento all'istanza del database.
`uri_direct_2`|Un URI alternativo che può essere utilizzato per il collegamento al servizio. Formato come l'`uri`.
`uri_direct_1`|Un URI alternativo che può essere utilizzato per il collegamento al servizio. Formato come l'`uri`.
`ca_certificate_base64`|Un certificato auto-firmato che viene utilizzato per confermare che un'applicazione sia collegata al server corretto. Il certificato si basa su codifica base64.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`uri_cli_2`|Una riga di comando shell `cqlsh` alternativa che esegue il collegamento all'istanza del database.
`uri`|L'URI da utilizzare quando esegui il collegamento al servizio, include lo schema (`scylla:`), la password, il nome host del server, il numero di porta a cui collegarsi e il nome del database.
{: caption="Tabella 1. Credenziali di Compose for ScyllaDB" caption-side="top"}
