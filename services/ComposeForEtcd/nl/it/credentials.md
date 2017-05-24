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

Per collegare un'applicazione al tuo servizio, utilizza le credenziali create insieme al servizio. L'applicazione di esempio [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForEtcd}} utilizzando le credenziali.

Nome campo|Descrizione
----------|-----------
`ca_certificate_base64`|Un certificato auto-firmato che viene utilizzato per confermare che un'applicazione sia collegata al server corretto. Il certificato si basa su codifica base64. Devi decodificare la chiave prima di utilizzarla, come mostrato nell'applicazione di esempio.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`db_type`|Il tipo di database offerto dal servizio; in questo caso `etcd`.
`name`|Il nome di distribuzione del database.
`uri`|L'URI da utilizzare durante il collegamento al servizio. `uri` include lo schema (`amqps:), il nome utente e la password amministratore, il nome host del server, il numero di porta a cui collegarsi e il nome `vhost.
{: caption="Tabella 1. Credenziali di Compose for etcd" caption-side="top"}
