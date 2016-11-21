---

copyright:
  anni: 2016

---

{:new_window: target="\_blank"}

{:shortdesc: .shortdesc}


# Utilizzo dell'applicazione starter
*Ultimo aggiornamento: 15 settembre 2016*
{: .last-updated}

Crea applicazioni simulate nell'applicazione starter {{site.data.keyword.iotelectronics_full}}. Scopri come un produttore aziendale può monitorare le applicazioni connesse a {{site.data.keyword.iot_short_notm}}. Interagisci manualmente con l'applicazione simulata per attivare avvisi, notifiche e azioni.
{:shortdesc}


## Apertura dell'applicazione starter
{: #iot4e_openAppMain}

Poiché il metodo di apertura dell'applicazione starter varia leggermente a seconda della versione della console {{site.data.keyword.Bluemix_notm}} in uso, devi leggere le istruzioni per la versione appropriata.

Per determinare la versione che stai utilizzando, puoi controllare le seguenti opzioni:
  - [Nuovo {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp). Se stai utilizzando la nuova esperienza {{site.data.keyword.Bluemix_notm}}, l'opzione **Prova il nuovo Bluemix** *non* viene visualizzata nella sezione dell'intestazione.
  - [{{site.data.keyword.Bluemix_notm}} classico](#iot4e_openApp_c). Se stai utilizzando l'esperienza classica di {{site.data.keyword.Bluemix_notm}}, l'opzione **Prova il nuovo Bluemix** viene visualizzata nella sezione dell'intestazione.  

**Suggerimento:** per passare all'esperienza classica di {{site.data.keyword.Bluemix_notm}}, fai clic sul tuo nome utente nella sezione dell'intestazione, scorri verso il basso e fai clic su **Passa alla versione classica**. Per passare alla nuova esperienza {{site.data.keyword.Bluemix_notm}}, fai clic su **Prova il nuovo Bluemix** nella sezione dell'intestazione.

### Apertura dell'applicazione starter nella nuova esperienza {{site.data.keyword.Bluemix_notm}}.
{: #iot4e_openApp}
1. Nel dashboard {{site.data.keyword.Bluemix_notm}}, avvia la tua applicazione starter {{site.data.keyword.iotelectronics}} facendo clic sul tile relativo.

    ![{{site.data.keyword.iotelectronics}} nel dashboard, Nuova esperienza.](images/IoT4E_bm_dashboard.png "{{site.data.keyword.iotelectronics}} nel dashboard, Nuova esperienza")

2. Attendi che nell'intestazione venga visualizzato il messaggio di stato *La tua applicazione è in esecuzione* e dopo fai clic su **Visualizza applicazione** per visualizzare l'applicazione starter.  

    ![{{site.data.keyword.iotelectronics}} nel dashboard, Nuova esperienza.](images/IoT4E_view_app.png "{{site.data.keyword.iotelectronics}} nel dashboard, Nuova esperienza")

### Apertura dell'applicazione starter nell'esperienza classica di {{site.data.keyword.Bluemix_notm}}.
{: #iot4e_openApp_c}

1. Nel dashboard {{site.data.keyword.Bluemix_notm}}, avvia la tua applicazione starter {{site.data.keyword.iotelectronics}} facendo clic sul tile relativo.

    ![{{site.data.keyword.iotelectronics}} nel dashboard, Classico.](images/IoT4E_bm_dashboard_c.png "{{site.data.keyword.iotelectronics}} nel dashboard, Classico")

2. Attendi che nella sezione Integrità dell'applicazione venga visualizzato il messaggio di stato *La tua applicazione è in esecuzione*, quindi nella finestra principale, in base al nome dell'applicazione, fai clic sull'URL **Rotte** per visualizzare l'applicazione starter.  

    ![{{site.data.keyword.iotelectronics}} nel dashboard, Classico.](images/IoT4E_view_app_c.png "{{site.data.keyword.iotelectronics}} nel dashboard")

## Creazione di applicazioni simulate
{: #iot4eCreateAppliances}

Nelle applicazioni starter puoi creare e controllare le applicazioni simulate in qualità di produttore dell'applicazione o di consumatore. I dati relativi allo stato e agli eventi di tali applicazioni simulate vengono memorizzati e possono essere visualizzati in {{site.data.keyword.iot_full}}.

1. Seleziona una delle seguenti opzioni:
    - **Connetti e gestisci applicazioni simulate**, per creare applicazioni simulate come produttore dell'applicazione
    - **Controlla in remoto le tue applicazioni collegate**, per creare applicazioni simulate e connetterti con l'[applicazione mobile di esempio](iotelectronics_config_mobile.html) come proprietario dell'applicazione.

    ![{{site.data.keyword.iotelectronics}} esperienza starter](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} esperienza starter")

2. Vai alla sezione etichettata **Successivamente, scegli o aggiungi una nuova rondella simulata** e fai clic sull'icona +. Viene creata una nuova rondella.

    ![Aggiunta di una rondella.](images/IoT4E_add_washer.png "Aggiunta di una rondella")

3. Per visualizzare i dettagli della rondella, immettere  comandi e causare errori, fai clic su una rondella.

  ![Dettagli dello stato della rondella.](images/IoT4E_washer_control.png "Dettagli dello stato della rondella")


# Link correlati
{: #rellinks}

## Documentazione API
{: #api}
* [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## interessati
{: #general}

* [Documentazione {{site.data.keyword.iotelectronics}}](iotelectronics_overview.html)
* [Documentazione {{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
*  [Documentazione {{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [Documentazione {{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## Esempi
{: #samples}
* [Applicazione mobile di esempio](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
