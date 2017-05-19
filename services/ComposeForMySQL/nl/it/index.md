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

# Introduzione a Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Con un'ampia serie secondaria di ANSI SQL 99 e una vasta gamma delle relative estensioni, inclusi il documento JSON, la ricerca di testo completo e le viste aggiornabili, MySQL offre una ricca tavolozza per gli sviluppatori per progettare le loro applicazioni. Gli amministratori possono inoltre trovare un'ampia selezione di strumenti di gestione del database che possono utilizzare con MySQL. {{site.data.keyword.composeForMySQL_full}} permette a MySQL di estendere le funzionalità di MySQL a gestirle al tuo posto, offrendo un sistema di distribuzione con ridimensionamento automatico facile da utilizzare che distribuisce l'elevata disponibilità e la ridondanza e i backup automatizzati.
{:shortdesc}

**Nota:** {{site.data.keyword.composeForMySQL_full}} non fornisce accesso alla IU di Compose. Consulta [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) per ulteriori dettagli.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForMySQL}}:

1. [Crea un'istanza {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

   Quando crei un'istanza del servizio, scegli un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio.  I vari valori delle credenziali sono elencati nella sezione "Credenziali disponibili".

2. Collega il tuo servizio {{site.data.keyword.composeForMySQL}}.

  Per collegare un'applicazione al tuo servizio, utilizza le [credenziali](./credentials.html) create insieme al servizio. 

  Scarica l'applicazione di esempio [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli dell'applicazione nella console Bluemix, fai clic su **Visualizza applicazione**.

  L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForMySQL}}.
