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

# Introduzione a Compose for RethinkDB
{: #getting-started-with-compose-for-rethinkdb}

{{site.data.keyword.composeForRethinkDB}} ti fornisce un documento basato su JSON, un database distribuito con una console di esplorazione e gestione integrata. RethinkDB utilizza il linguaggio di query ReQL, creato con il concatenamento della funzione e disponibile nelle librerie client per Java, JavaScript, Python e Ruby. Con ReQL, è possibile utilizzare le funzioni lato server RethinkDB come le query secondarie e le unioni distribuite tra i nodi del cluster. RethinkDB inoltre supporta gli indici secondari per una migliore lettura delle prestazioni di query. La funzione più potente di RethinkDB, changefeeds, consente a molte query ReQL di essere convertite in feed in tempo reale.
{:shortdesc}

**Nota:** tutte le istanze del servizio Compose di cui è stato eseguito il provisioning prima del 14 settembre 2016 che sono ancora attive e che possono ancora essere utilizzate a cui si può fare direttamente accesso da [https://www.compose.com/](https://www.compose.com). È possibile accedere direttamente a tutte le istanze del servizio Compose di cui è stato eseguito il provisioning da questo punto in avanti ed è possibile utilizzarle nel tuo account Bluemix.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForRethinkDB}}.

1. [Crea un'istanza {{site.data.keyword.composeForRethinkDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/).

  Quando crei un'istanza del servizio, assicurati di scegliere un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio. I vari valori delle credenziali sono elencati nella sezione *Credenziali disponibili*.

2. Collega il tuo servizio {{site.data.keyword.composeForRethinkDB}}.

   Per collegare un'applicazione al tuo servizio, utilizza le [credenziali](./credentials.html) create insieme al servizio. L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForRethinkDB}}.

   Scarica l'applicazione di esempio [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli della tua applicazione in Bluemix, fai clic su **Visualizza applicazione**.
