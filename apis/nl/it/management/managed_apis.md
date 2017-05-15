---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Le mie API
{: #manage_api}

Utilizza la scheda **Visualizza API gestite** per visualizzare lo stato complessivo delle API che gestisci e di quelle precedentemente gestite ma che sono attualmente non esposte. Nella scheda **API condivise**, puoi visualizzare tutte le API che sono state condivise con la tua organizzazione {{site.data.keyword.Bluemix_notm}} attraverso la Gestione API o il servizio {{site.data.keyword.apiconnect_short}}.

Puoi visualizzare tutte le API da te gestite con Gestione API utilizzando il dashboard delle API. 

## Visualizzazione delle API gestite
{: #view_api}

Qui puoi visualizzare le API create per le azioni {{site.data.keyword.openwhisk_short}} e altre origini esterne.

1. Dal dashboard {{site.data.keyword.Bluemix_notm}}, seleziona l'icona **Menu** > **Servizi** > **API**.
2. Per selezionare la tua origine, fai clic su **Gestisci API**. Viene visualizzato un elenco delle API attualmente gestite. Tra i tipi di API sono inclusi i seguenti:
    * Endpoint definiti dall'utente - Queste voci sono le API all'esterno dell'ambiente {{site.data.keyword.Bluemix_notm}} e sono tracciate dal relativo endpoint URL. 
    * Applicazioni {{site.data.keyword.openwhisk_short}} - Queste voci sono le azioni {{site.data.keyword.openwhisk_short}} che vengono integrate all'interno di un'API.

Selezionare il nome di un'API per visualizzarne ulteriori dettagli.

## Creazione di API gestite
{: #create_mgd_api}

Puoi aggiungere un'API all'elenco senza lasciare l'elenco di API gestite selezionando **Crea API gestita**.

Dopo aver scelto se creare un'API {{site.data.keyword.openwhisk_short}} o un proxy API (esterna), immetti le informazioni per la nuova API.  

Questo è l'unico posto in cui puoi aggiungere un proxy API o API esterna. Un'API esterna non viene creata né memorizzata nello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}}. Puoi gestire un'API esterna specificando l'URL del suo endpoint esterno. Questo può risultare utile se stai provando la Gestione API per verificare se soddisfa le tue esigenze o se hai già delle API in esecuzione con URL esistenti che non vuoi interrompere. 

Vedi [Gestisci API](manage_apis.html) per ulteriori informazioni sulle impostazioni richieste per la creazione delle API.

## Utilizzo delle API condivise
{: #share_api}

Nella scheda **Esplora API condivise** puoi visualizzare le API che sono state create da altri utenti e condivise con te. Puoi anche creare delle chiavi API per le API associate alle azioni {{site.data.keyword.openwhisk_short}} e al servizio {{site.data.keyword.appconserviceshort}}.

1. Dal dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Menu** > **Servizi** > **API**.
2. Seleziona **Esplora API condivise** nel riquadro di navigazione. Qui vengono visualizzate tutte le API che puoi utilizzare.
3. Per utilizzare un'API, selezionala per aprire il relativo portale sviluppatori in cui puoi sottoscrivere un piano al fine di utilizzarlo. 
4. Dopo aver selezionato un'API da gestire, vedi [Gestisci API](manage_apis.html) per ulteriori informazioni su come completare le seguenti attività: 
    * Visualizzare l'utilizzo dell'API
    * Creare le chiavi API
    * Utilizzare l'Explorer API per visualizzare la documentazione e verificare l'API.
