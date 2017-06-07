---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione delle chiavi API
{: #manapikey}

Una chiave API è un codice che viene trasmesso dai programmi informatici che richiamano un'interfaccia di programmazione delle applicazioni (API) per identificare il programma chiamante, il suo sviluppatore o il suo utente nel sito Web. Le chiavi API vengono utilizzate per tracciare e controllare l'utilizzo dell'API, ad esempio per prevenire l'uso dannoso o l'abuso dell'API (come definito probabilmente dai termini di servizio). La chiave API spesso funge da identificativo univoco e da token segreto per l'autenticazione e generalmente dispone di una serie di diritti di accesso nell'API ad essa associata. Le chiavi API possono essere basate sul sistema UUID (universally unique identifier) per garantire che siano univoche per ogni utente.

In qualità di utente {{site.data.keyword.Bluemix_notm}}, potresti voler utilizzare una chiave API quando abiliti un programma o uno script senza distribuire la tua password allo script. Un vantaggio di utilizzare una chiave API può essere che un utente o un'organizzazione può creare più chiavi API per programmi diversi e le chiavi API possono essere eliminate in modo indipendente se compromesse senza interferire con altre chiavi API o con l'utente. Inoltre, come [utente federato](/docs/admin/adminpublic.html#federatedid), puoi utilizzare una chiave API per eseguire l'accesso. Per ulteriori informazioni sull'utilizzo di una chiave API per l'accesso, vedi la documentazione per il comando [ `bluemix login` della CLI {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login) e il [comando `cf login` della CLI cf](/docs/cli/reference/cfcommands/index.html#cf_login).

Puoi gestire le tue chiavi API {{site.data.keyword.Bluemix_notm}} dalla finestra Chiavi API Bluemix. Vai a **Gestisci** &gt; **Sicurezza** &gt; **Chiavi API Bluemix** per visualizzare un elenco delle chiavi API con descrizioni e date. Da questa pagina puoi creare, modificare o eliminare le chiavi API.

Per creare una chiave API:

1. Vai a **Gestisci** &gt; **Sicurezza** &gt; **Chiavi API Bluemix**.
2. Fai clic su **Crea chiave API**.
3. Immetti un nome e una descrizione per la tua chiave API.
4. Fai clic su **Crea chiave API**.
5. Infine, fai clic su **Mostra** per visualizzare la chiave API e per copiarla e salvarla per un uso successivo oppure fai clic su **Scarica chiave API**.

**Nota**: la chiave API è disponibile per la visualizzazione o il download solo durante la fase di creazione. Se la chiave API viene persa, dovrai crearne una nuova.

Per modificare una chiave API:

1. Vai a **Gestisci** &gt; **Sicurezza** &gt; **Chiavi API Bluemix**.
2. Dal menu **Azioni** di una chiave API elencata nella tabella, fai clic su **Modifica nome e descrizione** 
3. Aggiorna le informazioni per la tua chiave API.
4. Fai clic su **Aggiorna chiave API**.

Per eliminare una chiave API: 

1. Vai a **Gestisci** &gt; **Sicurezza** &gt; **Chiavi API Bluemix**.
2. Dal menu **Azioni** di una chiave API elencata nella tabella, fai clic su **Elimina**.
3. Conferma infine l'eliminazione facendo clic su **Elimina chiave**.

Puoi anche utilizzare la CLI {{site.data.keyword.Bluemix_notm}} per gestire le tue chiavi API attraverso l'elenco, la creazione, l'aggiornamento o l'eliminazione delle chiavi. Per ulteriori informazioni, consulta la sezione relativa al comando [`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam).

