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

# Introduzione a Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB è un sostituto del database distribuito su colonna ampia Cassandra. ScyllaDB è scritto in C++, piuttosto che il Java di Cassandra, per un migliore utilizzo della risorsa che può dare un risultato 10 volte migliore nelle prestazioni nei riferimenti. In aggiunta per mantenere la compatibilità con i file di dati e lo strumento Cassandra, ScyllaDB aggiunge le funzionalità di ottimizzazione automatica. {{site.data.keyword.composeForScyllaDB_full}} estende le funzionalità di ScyllaDB a gestirle al tuo posto, offrendo un sistema di distribuzione con ridimensionamento automatico facile da utilizzare che distribuisce l'elevata disponibilità e la ridondanza e i backup automatizzati.
{:shortdesc}

**Nota:** {{site.data.keyword.composeForScyllaDB_full}} non fornisce accesso alla IU di Compose. Consulta [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) per ulteriori dettagli.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForScyllaDB}}:

1. [Crea un'istanza {{site.data.keyword.composeForScyllaDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   Quando crei un'istanza del servizio, scegli un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio. I vari valori delle credenziali sono elencati nella sezione "Credenziali disponibili".

2. Collega il tuo servizio {{site.data.keyword.composeForScyllaDB}}.

   Per collegare un'applicazione al tuo servizio, utilizza le [credenziali](./credentials.html) create insieme al servizio. 

   Scarica l'applicazione di esempio [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli dell'applicazione nella console Bluemix, fai clic su **Visualizza applicazione**.

   L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForScyllaDB}}.
