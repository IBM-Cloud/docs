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

Per collegare un'applicazione al tuo servizio, utilizza le credenziali create insieme al servizio. L'applicazione di esempio [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForElasticsearch}} utilizzando le credenziali.

Nome campo|Descrizione
----------|-----------
`uri`|L'URI da utilizzare durante il collegamento al servizio. Include lo schema (`https:`), il nome utente e la password amministratore, il nome host del server e il numero di porta a cui collegarsi.
`uri_direct_1`|Un URI alternativo da utilizzare durante il collegamento al servizio. Formato come l'`uri`.
`uri_health`|Un comando `curl` che richiede l'integrità del cluster dal primo haproxy.
`uri_health_1`|Un comando `curl` che richiede l'integrità del cluster dal secondo haproxy.
`ca_certificate_base64`|Un certificato auto-firmato che viene utilizzato per confermare che un'applicazione sia collegata al server corretto. Si basa su codifica base64. Devi decodificare la chiave prima di utilizzarla, come mostrato nell'applicazione di esempio.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`db_type`|Il tipo di database offerto dal servizio; in questo caso `elastic_search`.
`name`|Il nome di distribuzione del database.
{: caption="Tabella 1. Credenziali di Compose for Elasticsearch" caption-side="top"}

**Nota:** due portali `haproxy` forniscono l'accesso al cluster Elasticsearch. Possono essere utilizzati sia `uri` che `uri_direct_1` per il collegamento al cluster. Nelle tue applicazioni, passa da `uri` a `uri_direct_1` per gestire le risposte agli errori di connessione.
