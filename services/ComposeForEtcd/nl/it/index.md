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

# Introduzione a Compose for etcd
{: #getting-started-with-compose-for-etcd}

etcd è un archivio di valore-chiave che ospita i dati sempre corretti di cui hai bisogno per coordinare e gestire il tuo cluster server per la gestione della configurazione del server distribuito. etcd utilizza l'algoritmo coseno RAFT per assicurare la consistenza dei dati nel tuo cluster. Forza l'ordine in cui vengono eseguite le operazioni sui dati in modo che ogni nodo nel cluster arrivi allo stesso risultato con la stessa modalità. {{site.data.keyword.composeForEtcd_full}} aggiunge backup automatici dei tuoi dati di configurazione archiviati in etcd. Un'interfaccia di amministrazione intuitiva che ti permette di monitorare, ridimensionare e gestire la tua distribuzione con facilità.
{:shortdesc}

**Nota:** tutte le istanze del servizio Compose di cui è stato eseguito il provisioning prima del 14 settembre 2016 che sono ancora attive e che possono ancora essere utilizzate a cui si può fare direttamente accesso da [https://www.compose.com/](https://www.compose.com). È possibile accedere direttamente a tutte le istanze del servizio Compose di cui è stato eseguito il provisioning da questo punto in avanti ed è possibile utilizzarle nel tuo account Bluemix.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForEtcd}}.

1. [Crea un'istanza {{site.data.keyword.composeForEtcd}}](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/).

  Quando crei un'istanza del servizio, assicurati di scegliere un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio. I vari valori delle credenziali sono elencati nella sezione *Credenziali disponibili*.

2. Collega il tuo servizio {{site.data.keyword.composeForEtcd}}.

Per collegare un'applicazione al tuo servizio, utilizza le [credenziali](./credentials.html) create insieme al servizio. L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForEtcd}}.

Scarica l'applicazione di esempio [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli della tua applicazione in Bluemix, fai clic su **Visualizza applicazione** per visualizzare il contenuto degli *esempi*.
