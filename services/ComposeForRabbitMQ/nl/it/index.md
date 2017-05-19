---

copyright:
  years: 2016,2017
lastupdated: "2017-04-027"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a Compose for RabbitMQ
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ gestisce in modo asincrono i messaggi tra le tue applicazioni e i database, abilitando la separazione dei livelli dati e applicazione. RabbitMQ consente agli sviluppatori di instradare, tracciare ed eseguire query dei messaggi con livelli di persistenza personalizzabili, impostazioni di fornitura e pubblicazione confermata. Utilizzando {{site.data.keyword.composeForRabbitMQ_full}}, ottieni l'accesso all'interfaccia di gestione di facile utilizzo con un host per la gestione delle funzioni come il monitoraggio della distribuzione, il ridimensionamento facendo clic su un pulsante, la configurazione utente e l'accesso al file di log.
{:shortdesc}

**Nota:** tutte le istanze del servizio Compose di cui è stato eseguito il provisioning prima del 14 settembre 2016 che sono ancora attive e che possono ancora essere utilizzate a cui si può fare direttamente accesso da [https://www.compose.com/](https://www.compose.com). È possibile accedere direttamente a tutte le istanze del servizio Compose di cui è stato eseguito il provisioning da questo punto in avanti ed è possibile utilizzarle nel tuo account Bluemix.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForRabbitMQ}}.

1. [Crea un'istanza {{site.data.keyword.composeForRabbitMQ}}](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  Quando crei un'istanza del servizio, assicurati di scegliere un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio.  I vari valori delle credenziali sono elencati nella sezione *Credenziali disponibili*.

2. Collega il tuo servizio {{site.data.keyword.composeForRabbitMQ}}.

  Per collegare un'applicazione al tuo servizio, utilizza le [credenziali](./credentials.html) create insieme al servizio. L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForRabbitMQ}}.

  Scarica l'applicazione di esempio [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli della tua applicazione in Bluemix, fai clic su **Visualizza applicazione**.
