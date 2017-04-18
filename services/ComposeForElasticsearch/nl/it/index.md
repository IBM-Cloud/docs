---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} unisce la potenza di un motore di ricerca di testo completo con la forza dell'indicizzazione di un database del documento JSON. Insieme creano uno strumento potente per l'analisi dei dati su grandi volumi di dati. Con Elasticsearch, la tua ricerca può essere effettuata con esattezza, lasciandoti cercare approfonditamente nei tuoi dataset le strette corrispondenze e le quasi corrispondenze che potrebbero essere mancanti.
{:shortdesc}

**Nota:** tutte le istanze del servizio Compose di cui è stato eseguito il provisioning prima del 14 settembre 2016 che sono ancora attive e che possono ancora essere utilizzate a cui si può fare direttamente accesso da [https://www.compose.com/](https://www.compose.com). È possibile accedere direttamente a tutte le istanze del servizio Compose di cui è stato eseguito il provisioning da questo punto in avanti ed è possibile utilizzarle nel tuo account Bluemix.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForElasticsearch}}:

1. [Crea un'istanza {{site.data.keyword.composeForElasticsearch}}](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/).

  Quando crei un'istanza del servizio, assicurati di scegliere un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio. I vari valori delle credenziali sono elencati nella sezione *Credenziali disponibili*.

2. Collega il tuo servizio {{site.data.keyword.composeForElasticsearch}}.

  Per collegare un'applicazione al tuo servizio, utilizza le credenziali create insieme al servizio. L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForElasticsearch}}.

  Scarica l'applicazione di esempio [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli della tua applicazione in Bluemix, fai clic su **Visualizza applicazione** per visualizzare il contenuto dell'indice *esempi*.

## Credenziali disponibili

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
{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} credentials" caption-side="top"}

**Nota:** due portali `haproxy` forniscono l'accesso al cluster Elasticsearch. Possono essere utilizzati sia `uri` che `uri_direct_1` per il collegamento al cluster. Nelle tue applicazioni, passa da `uri` a `uri_direct_1` per gestire le risposte agli errori di connessione.

# Link correlati
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Esercitazioni ed esempi
{: #samples}
* [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs){:new_window}

## Link correlati
{: #general}
* [Compose Help](https://help.compose.com/docs){:new_window}
