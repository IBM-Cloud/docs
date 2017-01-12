---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione a {{site.data.keyword.contdelivery_short}}
{: #cd_getting_started}

Ultimo aggiornamento: 18 novembre 2016
{: .last-updated}  

Adotta un approccio DevOps utilizzando {{site.data.keyword.contdelivery_full}}, che include le toolchain che automatizzano la creazione e la distribuzione di applicazioni. Puoi iniziare creando una semplice toolchain di distribuzione che supporta le attività di sviluppo, distribuzione e operative.
{: shortdesc}

Dopo aver creato un'istanza di {{site.data.keyword.contdelivery_short}} selezionando il relativo tile di servizio dal catalogo {{site.data.keyword.Bluemix_notm}}, puoi scegliere in che modo iniziare a utilizzare il servizio.
 ![Pagina di benvenuto di Fornitura continua](images/cd_landing_page.png)

 * Per iniziare rapidamente e distribuire la tua applicazione utilizzando una pipeline automatizzata, nella sezione "Inizia con una pipeline", fai clic su **[Inizia qui](#starting_with_a_pipeline)**. Puoi aggiungere altri strumenti in seguito. 
 * Per creare e configurare una toolchain di fornitura continua da un template, nella sezione "Inizia da un template di toolchain", fai clic su **[Inizia qui](#starting_from_a_toolchain_template)**. La toolchain integra gli strumenti per la pianificazione, lo sviluppo, la distribuzione di pipeline e la gestione delle tue applicazioni. Puoi sempre aggiungere o rimuovere strumenti dalla toolchain.
 * Se hai già delle toolchain, nella sezione "Inizia da un template di toolchain", fai clic su **Visualizza le tue toolchain**. Per ulteriori informazioni sull'utilizzo delle toolchain, vedi [Utilizzo delle toolchain in Bluemix pubblico](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}.

##Inizia con una pipeline
{: #starting_with_a_pipeline}

Le pipeline automatizzano creazioni, distribuzioni e altro ancora. Per iniziare con una pipeline automatizzata, seleziona un template e fornisci la posizione del tuo repository GitHub.

Per [creare una pipeline (il link si apre in una nuova finestra)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} configurata per distribuire un'applicazione Cloud Foundry, completa la seguente procedura:

1. Fai clic su **Cloud Foundry**.
1. Se vuoi utilizzare un nome diverso per la pipeline, modifica il suo nome predefinito. Il nome della pipeline la identifica in {{site.data.keyword.Bluemix_notm}}. 
1. Se vuoi utilizzare un nome diverso per l'applicazione, modifica il suo nome predefinito. Il nome dell'applicazione la identifica in {{site.data.keyword.Bluemix_notm}}. Questo nome indica l'applicazione in cui distribuisce la pipeline. 
1. Se non hai una toolchain, ne viene creata una con un nome predefinito. Se vuoi utilizzare un nome diverso per la toolchain, modifica il suo nome. Le pipeline sono gestite dalle toolchain. Con la toolchain, puoi estendere le funzionalità della tua pipeline mediante l'integrazione con altri strumenti e servizi. 

 **Suggerimento**: le pipeline e le toolchain appartengono alle organizzazioni. Se fai parte di un'organizzazione che ha delle toolchain, puoi utilizzare tali toolchain anche se non sei stato tu a crearle.
 
1. Seleziona la toolchain che vuoi utilizzare o immetti un nome per la nuova toolchain da creare.
1. Fornisci la posizione del tuo repository GitHub.

 **Suggerimento**: se non hai autorizzato {{site.data.keyword.Bluemix_notm}} ad accedere a GitHub, ti verrà chiesto di fare clic su **Autorizza** per andare al sito Web GitHub. Se non disponi di una sessione GitHub attiva, ti viene richiesto di accedere. Fai clic su **Authorize Application** per consentire a {{site.data.keyword.Bluemix_notm}} di accedere al tuo account GitHub. Se disponi di una sessione GitHub attiva ma non hai immesso la tua password recentemente, ti potrebbe essere richiesto di immettere la tua password GitHub per la conferma.

   * Se disponi di un repository GitHub e desideri utilizzarlo, per il tipo di repository, seleziona **Link**. Cerca la posizione del repository o selezionane uno dall'elenco di repository disponibili.
   
   * Se vuoi creare un repository GitHub vuoto, per il tipo di repository, seleziona **Nuovo**. Immetti un nome per il repository.
   
   * Se vuoi creare un clone di un repository GitHub, per il tipo di repository, seleziona **Copia**. Cerca la posizione del repository o selezionane uno dall'elenco di repository disponibili.
   
   * Se vuoi biforcare un repository GitHub in modo da poter fornire le modifiche attraverso le richieste di importazione, seleziona **Fork**. Cerca la posizione del repository o selezionane uno dall'elenco di repository disponibili.
 
1. Fai clic su **Crea**. La pipeline viene creata, configurata e visualizzata nella pagina Panoramica della toolchain.
 ![Tile Pipeline](images/cd_pipeline.png)
 
Per creare una [pipeline vuota (il link si apre in una nuova finestra)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} senza alcuna fase preconfigurata:

1. Fai clic su **Personalizzato**.
1. Se vuoi utilizzare un nome diverso per la pipeline, modifica il suo nome predefinito. Il nome della pipeline la identifica in {{site.data.keyword.Bluemix_notm}}. 
1. Se non hai una toolchain, ne viene creata una con un nome predefinito. Se vuoi utilizzare un nome diverso per la toolchain, modifica il suo nome. Le pipeline sono gestite dalle toolchain. Con la toolchain, puoi estendere le funzionalità della tua pipeline mediante l'integrazione con altri strumenti e servizi.
1. Seleziona la toolchain che vuoi utilizzare o immetti un nome per la nuova toolchain da creare.
1. Fai clic su **Crea**. Viene creata una pipeline vuota che viene rappresentata in forma di tile nella pagina Panoramica della toolchain.

##Inizia da un template di toolchain
{: #starting_from_a_toolchain_template}

Per creare e configurare una toolchain di fornitura continua da un [template (il link si apre in una nuova finestra)](https://console.ng.bluemix.net/devops/create){: new_window}:

1. Nella pagina **Create a Toolchain**, fai clic su un template di toolchain.  
1. Esamina il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain. Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra ogni integrazione dello strumento che fa parte della toolchain.
 ![Diagramma_toolchain](images/toolchain_diagram.png)
1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se vuoi utilizzare un nome diverso, modifica il nome della toolchain.
1. Nella sezione Integrazioni configurabili, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Alcune delle integrazioni dello strumento non richiedono configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configurazione delle integrazioni dello strumento](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**. Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono create e attivate.
 * Se hai configurato l'integrazione dello strumento Sauce Labs, Sauce Labs viene impostato per aggiungere lavori alle pipeline ed eseguire i test.
 * Se hai configurato l'integrazione dello strumento PagerDuty, PagerDuty viene impostato per inviare notifiche di avviso al servizio che hai specificato. 
 * Se hai configurato l'integrazione dello strumento Slack, Slack viene impostato per inviare notifiche sullo stato della distribuzione al canale che hai specificato. 
 * Se hai configurato l'integrazione dello strumento GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub. 

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [Create and use your first toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}

## Link correlati
{: #general}

* [Microservices toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method){:new_window}
