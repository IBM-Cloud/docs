---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Eliminazione di risorse in ambienti temporanei
{: #destroying}

Puoi utilizzare {{site.data.keyword.bplong}} per eliminare le tue risorse. Quando elimini le risorse, elimini il tuo ambiente e tutte le risorse associate.  
{:shortdesc}

**Avvertenza**: quando elimini le risorse, l'azione non può essere annullata. L'eliminazione delle risorse non è consigliata negli ambienti di produzione, ma potrebbe essere utile per gli ambienti temporanei come test o QA.

Prima di eliminare le tue risorse, considera le seguenti linee guida: 
* Assicurati che il traffico non sia diretto alle tue risorse.
* Assicurati di eseguire il backup di tutti i dati di cui potresti aver bisogno. 


## Eliminazione delle risorse con la GUI
{: #gui}

Puoi utilizzare il dashboard {{site.data.keyword.bpshort}} per avviare ed eliminare gli ambienti temporanei.
{:shortdesc}

1. Nel dashboard **{{site.data.keyword.bpshort}}**, seleziona la scheda **Ambienti**.

2. Fai clic sulla riga dell'ambiente specifico che desideri rimuovere. 

3. Nel menu delle opzioni, seleziona **Elimina risorse** o **Elimina ambiente**. Entrambe queste opzioni sono irreversibili. Per determinare quale opzione selezionare, considera se hai delle risorse attive.
  * Seleziona **Elimina risorse** se vuoi arrestare e rimuovere le risorse attive. Si consiglia di eseguire un piano prima dell'eliminazione per confermare se le risorse associate all'ambiente sono da rimuovere.
  * Seleziona **Elimina ambiente** se vuoi rimuovere la configurazione dell'ambiente dal servizio {{site.data.keyword.bpshort}}. Questa opzione viene generalmente utilizzata se l'ambiente non viene distribuito e non dispone di risorse attive. Se selezioni questa opzione con delle risorse attive, non puoi più utilizzare il servizio {{site.data.keyword.bpshort}} per tracciare o distribuire le modifiche al tuo ambiente. Le risorse attive devono essere gestite singolarmente, dai propri dashboard del servizio.
  
  Segui le istruzioni visualizzate sullo schermo per confermare la scelta. 


## Eliminazione delle risorse con la CLI
{: #cli}

Puoi utilizzare la CLI {{site.data.keyword.bpshort}} per avviare ed eliminare gli ambienti temporanei.
{:shortdesc}

1. Esegui il comando `destroy` per eliminare il tuo ambiente e le risorse.

  ```
  bx schematics action destroy --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
2. Facoltativo: esegui il comando `delete` se vuoi rimuovere la tua configurazione dal servizio.

  ```
  bx schematics environment delete --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Eliminazione delle risorse con l'API
{: #api}

Puoi utilizzare l'API {{site.data.keyword.bpshort}} per avviare ed eliminare gli ambienti temporanei.
{:shortdesc}

1. Esegui la chiamata `PUT v1/environments/<environment_ID>/destroy` per eliminare le tue risorse.

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. Facoltativo: esegui la chiamata `DELETE v1/environments/<environment_ID>` se vuoi rimuovere la tua configurazione dal servizio {{site.data.keyword.bpshort}}.

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
