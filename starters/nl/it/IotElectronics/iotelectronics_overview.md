---

copyright:
  anni: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}

# Informazioni su {{site.data.keyword.iotelectronics}}
{: #iotelectronics_about}
*Ultimo aggiornamento: 19 settembre 2016*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} è un'istanza di produzione totalmente integrata IoT che permette alle tue applicazioni di comunicare e utilizzare i dati raccolti dalle tue applicazioni, sensori e gateway collegati.
{:shortdesc}

{{site.data.keyword.iotelectronics}} utilizza il servizio {{site.data.keyword.iot_full}} per collegare le tue applicazioni elettroniche smart con le applicazioni che sviluppi. Utilizza anche {{site.data.keyword.iot_short_notm}} per aiutarti nell'analizzare e comprendere i dati dalle tue applicazioni. Puoi stabilire delle regole per identificare delle condizioni che necessitano di attenzione e definire delle risposte automatizzate definite, come l'invio di email, l'esecuzione di un flusso di lavoro Node-RED o il collegamento ai servizi web.  

## Ricerca dello starter
{: #iot4eFindingStarter}
Puoi trovare lo starter {{site.data.keyword.iotelectronics}} nella sezione [Contenitori tipo](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/) del catalogo {{site.data.keyword.Bluemix_notm}}.  

## Cosa puoi fare con {{site.data.keyword.iotelectronics}}
{: #Features_iote}
Esplorare velocemente le funzioni della soluzione {{site.data.keyword.iotelectronics}} utilizzando dati e applicazioni simulate.

### Collegamento di applicazioni simulate
Crea applicazioni simulate e collegale alla piattaforma per visualizzare i dati live in streaming. Utilizza un'applicazione basata sul web per simulare come un'applicazione riceve i comandi ed esegue le operazioni. Imita malfunzionamenti per generare avvisi e notifiche. Ai fini della dimostrazione, vengono utilizzate delle rondelle per l'applicazione simulata all'interno dello starter {{site.data.keyword.iotelectronics}}. L'applicazione a cui scegli di connetterti può essere un qualsiasi tipo di dispositivo elettronico smart.  

### Prova un'applicazione mobile utente di esempio
Utilizza un telefono iOS per visualizzare come un proprietario dell'applicazione può interagire con l'applicazione. Invia comandi all'applicazione e ricevi aggiornamenti dall'applicazione utilizzando la piattaforma e {{site.data.keyword.Bluemix_notm}}. Imita malfunzionamenti di eventi e visualizza i risultati nell'applicazione mobile.

### Connetti le tue applicazioni elettroniche
Connetti le tue applicazioni al cloud in modo sicuro e inizia a personalizzare le tue applicazioni. Sono disponibili una serie di 'ricette' e esempi verificati che puoi modificare e utilizzare per prove di concetto, verifica e esperimenti.

## Cosa c'è nello starter {{site.data.keyword.iotelectronics}}
{: #whatsInStarter}
Il contenitore tipo starter distribuisce la soluzione {{site.data.keyword.iotelectronics}} integrata.  Tutti i componenti sono associati e distribuiti automaticamente per te. L'applicazione starter ti permette di esplorare velocemente le funzioni della soluzione utilizzando dati e applicazioni simulate. L'applicazione mobile di esempio ti mostra come un consumatore può registrare, ricevere avvisi e controllare un'applicazione collegata. Puoi utilizzare gli esempi come punti di partenza per la creazione e la raccolta di dati delle tue proprie applicazioni. I seguenti servizi e applicazioni sono inclusi nella soluzione:

![ Architettura {{site.data.keyword.iotelectronics}}. Questo diagramma è descritto nel testo principale dell'argomento.](images/IoT4E_architecture.svg "Architettura {{site.data.keyword.iotelectronics}}")

Lo starter {{site.data.keyword.iotelectronics}} utilizza il servizio e le API {{site.data.keyword.iotelectronics}} per connettersi con {{site.data.keyword.iot_short_notm}}. L'applicazione starter e l'applicazione mobile di esempio comunicano con il servizio {{site.data.keyword.iotelectronics}} e vengono connesse tra loro da {{site.data.keyword.amafull}}. I seguenti componenti sono inclusi nello starter:

**Il servizio {{site.data.keyword.iotelectronics}} ** supporta la registrazione e le notifiche di utenti e applicazioni.

**{{site.data.keyword.iot_full}}** permette alle tue applicazioni di comunicare e utilizzare i dati raccolti dalle tue applicazioni, sensori e gateway connessi.

<!-- **{{site.data.keyword.iotrtinsights_full}}** enables you to enrich and monitor data from your appliances, visualize what's happening now, and respond to emerging conditions by using automated actions. -->

**{{site.data.keyword.amafull}}** abilita gli utenti delle applicazioni mobili ad accedere utilizzando gli account social esistenti e verifica che le comunicazioni con i sistemi di backend siano sicure.

**{{site.data.keyword.sdk4nodefull}}** ti abilita a sviluppare, distribuire e ridimensionare le applicazioni JavaScript&reg; lato server e fornisce utilità, sicurezza e prestazioni avanzate.

L'**applicazione mobile di esempio** ti permette di visualizzare lo stato di un'applicazione simulata e di comunicare con tale applicazione utilizzando il tuo telefono iOS. Trova come ottenere l'applicazione mobile in [Utilizzo dell'applicazione mobile](iotelectronics_config_mobile.html).

# Link correlati
{: #rellinks}
## interessati
{: #general}
* [Documentazione {{site.data.keyword.iot_short}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html#gettingstartedtemplate)
* [Documentazione {{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/index.html)
* [Documentazione {{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)


## Documentazione API
{: #api}
*  [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)  
*  [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)
