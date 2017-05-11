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

# API personali
{: #manage_api}

Utilizza la scheda **Visualizza API gestite** per visualizzare lo stato complessivo delle API da te gestite e quelle che hai gestito in precedenza ma che attualmente non sono esposte. Nella scheda **API condivise**, puoi visualizzare tutte le API che sono state condivise con la tua organizzazione {{site.data.keyword.Bluemix_notm}} tramite Gestione delle API oppure tramite il servizio {{site.data.keyword.apiconnect_short}}.

Puoi visualizzare tutte le API che gestisci con Gestione delle API insieme utilizzando il dashboard API. 

## Visualizzazione delle API gestite
{: #view_api}

Qui puoi visualizzare le API create per le azioni {{site.data.keyword.openwhisk_short}} e altre origini esterne.

1. Dal dashboard {{site.data.keyword.Bluemix_notm}}, seleziona l'icona **Menu** > **Servizi** > **API**.
2. Per selezionare la tua origine, fai clic su **Gestisci API**. Viene visualizzato un elenco delle API attualmente gestite. I tipi di API includono i seguenti:
    * Endpoint definiti dall'utente - queste voci sono le API esterne all'ambiente {{site.data.keyword.Bluemix_notm}} e rintracciate in base al loro endpoint URL. 
    * Applicazioni {{site.data.keyword.openwhisk_short}} - queste voci sono le azioni {{site.data.keyword.openwhisk_short}} incluse in una API.

Seleziona il nome di una API per visualizzare ulteriori dettagli a essa relativi.

## Creazione di API gestite
{: #create_mgd_api}

Puoi aggiungere una API all'elenco senza uscire dall'elenco di API gestite selezionando **Crea API gestita**.

Dopo aver selezionato se vuoi creare una API {{site.data.keyword.openwhisk_short}} o proxy API (esterna), immetti le informazioni per la tua nuova API.  

Questo è l'unico punto dove puoi aggiungere una proxy API o una API esterna. Una API esterna è una API che non viene creata o memorizzata nello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}}. Puoi gestire una API esterna specificando l'URL del suo endpoint esterno. Ciò è utile quando stai provando la gestione delle API per verificare se soddisfa le tue esigenze o quando già hai delle API in esecuzione con degli URL esistenti che non vuoi interrompere. 

Vedi [Gestire le API](manage_apis.html) per ulteriori informazioni sulle impostazioni richieste per creare delle API.

## Gestione delle API condivise
{: #share_api}

Nella scheda **Esplora API condivise**, puoi visualizzare le API che sono state create da altri utenti e condivise con te. Puoi anche creare delle chiavi API per le API associate alle azioni {{site.data.keyword.openwhisk_short}} e al servizio {{site.data.keyword.appconserviceshort}}.

1. Dal dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Menu** > **Servizi** > **API**.
2. Seleziona **Esplora API condivise** nella navigazione. Tutte le API da te utilizzate sono visualizzate qui.
3. Per utilizzare una API, selezionala per aprire il relativo portale per gli sviluppatori, dove puoi sottoscrivere piano al fine di utilizzarlo. 
4. Dopo che hai selezionato una API da gestire, vedi [Gestire le API](manage_apis.html) per ulteriori informazioni su come completare le seguenti attività: 
    * Visualizzare l'utilizzo delle API
    * Creare delle chiavi PI
    * Utilizzare Explorer API per visualizzare la documentazione e testare la API.
