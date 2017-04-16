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

# Introduzione a Compose for MongoDB
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} utilizza l'aggregazione e l'indicizzazione e l'esecuzione di query potenti e un ampio supporto driver di MongoDB che è stato l'inizio dell'archiviazione dati JSON per molte nuove imprese e aziende. {{site.data.keyword.composeForMongoDB}} offre un sistema di distribuzione con ridimensionamento automatico facile da utilizzare. Offre disponibilità e ridondanza, backup no-stop in locale e automatizzati, strumenti di monitoraggio, integrazione nei sistemi di avviso, prestazioni delle viste di analisi e altro ancora, tutto con un'interfaccia utente semplice e ordinata.
{:shortdesc}

**Nota:** tutte le istanze del servizio Compose di cui è stato eseguito il provisioning prima del 14 settembre 2016 che sono ancora attive e che possono ancora essere utilizzate a cui si può fare direttamente accesso da [https://www.compose.com/](https://www.compose.com). È possibile accedere direttamente a tutte le istanze del servizio Compose di cui è stato eseguito il provisioning da questo punto in avanti ed è possibile utilizzarle nel tuo account Bluemix.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForMongoDB}}:

1. [Crea un'istanza {{site.data.keyword.composeForMongoDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/).

   Quando crei un'istanza del servizio, assicurati di scegliere un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio.  I vari valori delle credenziali sono elencati nella sezione *Credenziali disponibili*.

2. Collega il tuo servizio {{site.data.keyword.composeForMongoDB}}.

   Per collegare un'applicazione al tuo servizio, utilizza le credenziali create insieme al servizio. L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForMongoDB}}.

   Scarica l'applicazione di esempio [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli della tua applicazione in Bluemix, fai clic su **Visualizza applicazione**.


## Credenziali disponibili

Nome campo|Descrizione
----------|-----------
`uri`|L'URI da utilizzare durante il collegamento al servizio. `uri` include lo schema (`mongodb:`), il nome utente e la password amministratore, il nome host del server, il numero di porta a cui collegarsi, il nome del database e `?ssl=true` per abilitare le connessioni SSL.
`uri_cli`|Una riga di comando shell `mongo` che esegue il collegamento all'istanza del database.
`ca_certificate_base64`|Un certificato auto-firmato che viene utilizzato per confermare che un'applicazione sia collegata al server corretto. Il certificato si basa su codifica base64. Devi decodificare la chiave prima di utilizzarla, come mostrato nell'applicazione di esempio.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`db_type`|Il tipo di database offerto dal servizio: in questo caso, `mongodb`.
`name`|Il nome di distribuzione del database.
{: caption="Table 1. {{site.data.keyword.composeForMongoDB}} credentials" caption-side="top"}

# Link correlati
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Esercitazioni ed esempi
{: #samples}
* [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs){:new_window}

## Link correlati
{: #general}
* [Compose Help](https://help.compose.com/docs){:new_window}
