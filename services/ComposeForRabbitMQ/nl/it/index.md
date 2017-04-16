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

# Introduzione a {{site.data.keyword.composeForRabbitMQ}}
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ gestisce in modo asincrono i messaggi tra le tue applicazioni e i database, abilitando la separazione dei livelli dati e applicazione. RabbitMQ consente agli sviluppatori di instradare, tracciare ed eseguire query dei messaggi con livelli di persistenza personalizzabili, impostazioni di fornitura e pubblicazione confermata. Utilizzando {{site.data.keyword.composeForRabbitMQ_full}}, ottieni l'accesso all'interfaccia di gestione di facile utilizzo con un host per la gestione delle funzioni come il monitoraggio della distribuzione, il ridimensionamento facendo clic su un pulsante, la configurazione utente e l'accesso al file di log.
{:shortdesc}

**Nota:** tutte le istanze del servizio Compose di cui è stato eseguito il provisioning prima del 14 settembre 2016 che sono ancora attive e che possono ancora essere utilizzate a cui si può fare direttamente accesso da [https://www.compose.com/](https://www.compose.com). È possibile accedere direttamente a tutte le istanze del servizio Compose di cui è stato eseguito il provisioning da questo punto in avanti ed è possibile utilizzarle nel tuo account Bluemix.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForRabbitMQ}}.

1. [Crea un'istanza {{site.data.keyword.composeForRabbitMQ}}](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  Quando crei un'istanza del servizio, assicurati di scegliere un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio.  I vari valori delle credenziali sono elencati nella sezione *Credenziali disponibili*.

2. Collega il tuo servizio {{site.data.keyword.composeForRabbitMQ}}.

  Per collegare un'applicazione al tuo servizio, utilizza le credenziali create insieme al servizio. L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForRabbitMQ}}.

  Scarica l'applicazione di esempio [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli della tua applicazione in Bluemix, fai clic su **Visualizza applicazione**.

## Credenziali disponibili

Nome campo|Descrizione
----------|-----------
``uri``|L'URI da utilizzare durante il collegamento al servizio. Include lo schema (`amqps:), il nome utente e la password amministratore, il nome host del server, il numero di porta a cui collegarsi e il nome vhost.
`uri_direct_1`|Un URI alternativo da utilizzare durante il collegamento al servizio. Formato come l'`uri`.
`uri_admin`|Un URI in cui recarsi con un browser per accedere all'interfaccia di gestione del database. L'accesso richiede il nome utente e la password amministratore dal campo `uri`.
`uri_admin_1`|Un URI di gestione alternativo - consulta `uri_admin`.
`uri_admin_2`|Un URI di gestione alternativo - consulta `uri_admin`.
`uri_admin_3`|Un URI di gestione alternativo - consulta `uri_admin`.
`uri_admin_4`|Un URI di gestione alternativo - consulta `uri_admin`.
`ca_certificate_base64`|Un certificato auto-firmato che viene utilizzato per confermare che un'applicazione sia collegata al server corretto. Si basa su codifica base64. Devi decodificare la chiave prima di utilizzarla, come mostrato nell'applicazione di esempio.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`db_type`|Il tipo di database offerto dal servizio; in questo caso `rabbitmq`.
`name`|Il nome di distribuzione del database.
{: caption="Table 1. {{site.data.keyword.composeForRabbitMQ}} credentials" caption-side="top"}

# Link correlati
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Esercitazioni ed esempi
{: #samples}
[compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs){:new_window}

## Link correlati
{: #general}
* [Compose Help](https://help.compose.com/docs){:new_window}
