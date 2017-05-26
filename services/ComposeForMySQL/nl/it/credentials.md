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

Per collegare un'applicazione al tuo servizio, utilizza le credenziali create insieme al servizio. L'applicazione di esempio [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForMySQL}} utilizzando le credenziali.

Nome campo|Descrizione
----------|-----------
`db_type`|Il tipo di database offerto dal servizio, in questo caso `mysql`.
`name`|Il nome di distribuzione del database.
`uri_cli`|Una riga di comando shell `mysql` che esegue il collegamento all'istanza del database.
`ca_certificate_base64`|Un certificato auto-firmato che viene utilizzato per confermare che un'applicazione sia collegata al server corretto. Il certificato si basa su codifica base64.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`uri`|L'URI da utilizzare quando esegui il collegamento al servizio, include lo schema (`mysql:`), il nome utente e la password amministratore, il nome host del server e il numero di porta a cui collegarsi.
{: caption="Tabella 1. Credenziali di Compose for MySQL" caption-side="top"}
