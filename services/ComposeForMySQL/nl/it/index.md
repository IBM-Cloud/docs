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

# Introduzione a Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Con un'ampia serie secondaria di ANSI SQL 99 e una vasta gamma delle relative estensioni, inclusi il documento JSON, la ricerca di test ocompleto e le viste aggiornabili, MySQL offre una ricca tavolozza per gli sviluppatori per progettare le loro applicazioni. Gli amministratori possono inoltre trovare un'ampia selezione di strumenti di gestione del database che possono utilizzare con MySQL. {{site.data.keyword.composeForMySQL_full}} permette a MySQL di estendere le funzionalità di MySQL a gestirle al tuo posto, offrendo un sistema di distribuzione con ridimensionamento automatico facile da utilizzare che distribuisce l'elevata disponibilità e la ridondanza e i backup automatizzati.
{:shortdesc}

**Nota:** {{site.data.keyword.composeForMySQL_full}} non fornisce accesso alla IU di Compose. Consulta [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) per ulteriori dettagli.

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.composeForMySQL}}:

1. [Crea un'istanza {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

   Quando crei un'istanza del servizio, scegli un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio.  I vari valori delle credenziali sono elencati nella sezione "Credenziali disponibili".

2. Collega il tuo servizio {{site.data.keyword.composeForMySQL}}.

  Per collegare un'applicazione al tuo servizio, utilizza le credenziali create insieme al servizio. 

  Scarica l'applicazione di esempio [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli dell'applicazione nella console Bluemix, fai clic su **Visualizza applicazione**.

  L'applicazione di esempio illustra come utilizzare Node.js per il collegamento a un servizio {{site.data.keyword.composeForMySQL}}. 


## Credenziali disponibili

Nome campo|Descrizione
----------|-----------
`db_type`|Il tipo di database offerto dal servizio, in questo caso `mysql`.
`name`|Il nome di distribuzione del database.
`uri_cli`|Una riga di comando shell `mysql` che esegue il collegamento all'istanza del database.
`ca_certificate_base64`|Un certificato auto-firmato che viene utilizzato per confermare che un'applicazione sia collegata al server corretto. Il certificato si basa su codifica base64.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`uri`|L'URI da utilizzare quando esegui il collegamento al servizio, include lo schema (`mysql:`), il nome utente e la password amministratore, il nome host del server e il numero di porta a cui collegarsi.
{: caption="Table 1. {{site.data.keyword.composeForMySQL}} credentials" caption-side="top"}


# Link correlati
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Compose Articles](https://www.compose.com/articles/){:new_window}

## Esercitazioni ed esempi
{: #samples}
* [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs){:new_window}

## Link correlati
{: #general}
* [Compose Help](https://help.compose.com/docs){:new_window}
