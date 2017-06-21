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

# Introduzione a Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} unisce la potenza di un motore di ricerca di testo completo con la forza dell'indicizzazione di un database del documento JSON. Insieme creano uno strumento potente per l'analisi dei dati su grandi volumi di dati. Con Elasticsearch, la tua ricerca può essere effettuata con esattezza, lasciandoti cercare approfonditamente nei tuoi dataset le strette corrispondenze e le quasi corrispondenze che potrebbero essere mancanti.
{:shortdesc}

**Nota:** tutte le istanze del servizio Compose di cui è stato eseguito il provisioning prima del 14 settembre 2016 che sono ancora attive e che possono ancora essere utilizzate a cui si può fare direttamente accesso da [https://www.compose.com/](https://www.compose.com). È possibile accedere direttamente a tutte le istanze del servizio Compose di cui è stato eseguito il provisioning da questo punto in avanti ed è possibile utilizzarle nel tuo account Bluemix.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForElasticsearch}}:

1. [Crea un'istanza {{site.data.keyword.composeForElasticsearch}}](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/).

  Quando crei un'istanza del servizio, assicurati di scegliere un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio. I vari valori delle credenziali sono elencati nella sezione *Credenziali disponibili*.

2. Collega il tuo servizio {{site.data.keyword.composeForElasticsearch}}.

  Per collegare un'applicazione al tuo servizio, utilizza le [credenziali](./credentials.html) create insieme al servizio. L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForElasticsearch}}.

  Scarica l'applicazione di esempio [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli della tua applicazione in Bluemix, fai clic su **Visualizza applicazione** per visualizzare il contenuto dell'indice *esempi*.
