---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione a Fornitura continua
{: #cd_getting_started}

Adotta un approccio DevOps utilizzando {{site.data.keyword.contdelivery_full}}, che include le toolchain aperte che automatizzano la creazione e la distribuzione di applicazioni. Puoi iniziare creando una semplice toolchain di distribuzione che supporta le attività di sviluppo, distribuzione e operative.
{: shortdesc}

Dopo aver creato un'istanza di {{site.data.keyword.contdelivery_short}} selezionandola dal catalogo {{site.data.keyword.Bluemix_notm}}, puoi scegliere in che modo iniziare a utilizzare il servizio.
 ![Pagina di benvenuto di Fornitura continua](images/cd_landing_page.png)

 * Per iniziare rapidamente e distribuire la tua applicazione utilizzando una pipeline automatizzata, nella sezione "Inizia con una pipeline", fai clic su **[Inizia qui](#starting_with_a_pipeline)**. Puoi aggiungere altri strumenti in seguito.
 * Per creare e configurare una toolchain di fornitura continua da un template, nella sezione "Inizia da un template di toolchain", fai clic su **[Inizia qui](#starting_from_a_toolchain_template)**. La toolchain integra gli strumenti per la pianificazione, lo sviluppo, la distribuzione di pipeline e la gestione delle tue applicazioni. Puoi sempre aggiungere o rimuovere strumenti dalla toolchain.
 * Se hai già delle toolchain, nella sezione "Inizia da un template di toolchain", fai clic su **Visualizza le tue toolchain**. Per ulteriori informazioni sull'utilizzo delle toolchain, vedi [Gestione delle toolchain](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}.

**Suggerimento**: le pipeline sono gestite dalle toolchain. Puoi aggiungere una pipeline a una toolchain esistente. Se crei una pipeline e non hai alcuna toolchain esistente, sarà creata automaticamente una toolchain con un nome predefinito. Con la toolchain, puoi espandere le funzionalità della tua pipeline mediante l'integrazione con altri strumenti e servizi. 

##Inizia con una pipeline
{: #starting_with_a_pipeline}

Le pipeline automatizzano creazioni, distribuzioni e altro ancora. Per iniziare con una pipeline automatizzata, seleziona un template e fornisci la posizione del tuo repository GitHub.

Per [creare una pipeline ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){:new_window} configurata per distribuire un'applicazione Cloud Foundry, completa la seguente procedura:

1. Fai clic su **Cloud Foundry**.
1. Se vuoi utilizzare un nome diverso per la pipeline, modifica il suo nome predefinito. Il nome della pipeline la identifica in {{site.data.keyword.Bluemix_notm}}.
1. Se vuoi utilizzare un nome diverso per l'applicazione, modifica il suo nome predefinito. Il nome dell'applicazione la identifica in {{site.data.keyword.Bluemix_notm}}. Questo nome indica l'applicazione in cui distribuisce la pipeline.
1. Se non hai una toolchain, ne viene creata una con un nome predefinito. Se vuoi utilizzare un nome diverso per la toolchain, modifica il suo nome. Le pipeline sono gestite dalle toolchain. Con la toolchain, puoi estendere le funzionalità della tua pipeline mediante l'integrazione con altri strumenti e servizi.

 **Suggerimento**: le pipeline e le toolchain appartengono alle organizzazioni. Se fai parte di un'organizzazione che ha delle toolchain, puoi utilizzare tali toolchain anche se non sei stato tu a crearle.

1. Seleziona la toolchain che vuoi utilizzare o immetti un nome per la nuova toolchain da creare.
1. Seleziona il tuo provider Git.

 **Suggerimento**: se non hai autorizzato {{site.data.keyword.Bluemix_notm}} ad accedere a GitHub, ti verrà chiesto di fare clic su **Autorizza** per andare al sito Web GitHub. Se non disponi di una sessione GitHub attiva, ti viene richiesto di accedere. Fai clic su **Authorize Application** per consentire a {{site.data.keyword.Bluemix_notm}} di accedere al tuo account GitHub. Se disponi di una sessione GitHub attiva ma non hai immesso la tua password recentemente, ti potrebbe essere richiesto di immettere la tua password GitHub per la conferma.

 Non sei autorizzato ad accedere al repository {{site.data.keyword.ghe_short}}, qualcuno che dispone dei privilegi da amministratore per il repository deve aggiungerti. Per istruzioni sull'autorizzazione con {{site.data.keyword.Bluemix_notm}} Dedicato per {{site.data.keyword.ghe_short}}, consulta [Introduzione a {{site.data.keyword.Bluemix_notm}} Dedicato per {{site.data.keyword.ghe_short}}](/docs/services/ghededicated/index.html){: new_window}. Se devi essere autorizzato con la tua propria versione gestita di {{site.data.keyword.ghe_short}}, segui le procedure interne.

   * Se disponi di un repository e desideri utilizzarlo, per il tipo di repository, seleziona **Link**. Cerca la posizione del repository o selezionane uno dall'elenco di repository disponibili.

   * Se vuoi creare un repository vuoto, per il tipo di repository, seleziona **Nuovo**. Immetti un nome per il repository.

   * Se vuoi creare un clone di un repository, per il tipo di repository, seleziona **Copia**. Cerca la posizione del repository o selezionane uno dall'elenco di repository disponibili.

   * Se vuoi biforcare un repository GitHub in modo da poter fornire le modifiche attraverso le richieste di importazione, seleziona **Fork**. Cerca la posizione del repository o selezionane uno dall'elenco di repository disponibili.

1. Seleziona un repository o immetti un URL del repository.
1. Fai clic su **Crea**. La pipeline viene creata, configurata e visualizzata nella pagina Panoramica della toolchain.
 ![Scheda pipeline](images/cd_pipeline.png)

Per creare una [pipeline vuota ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} senza alcuna fase preconfigurata:

1. Fai clic su **Personalizzato**.
1. Se vuoi utilizzare un nome diverso per la pipeline, modifica il suo nome predefinito. Il nome della pipeline la identifica in {{site.data.keyword.Bluemix_notm}}.
1. Se non hai una toolchain, ne viene creata una con un nome predefinito. Se vuoi utilizzare un nome diverso per la toolchain, modifica il suo nome. Le pipeline sono gestite dalle toolchain. Con la toolchain, puoi estendere le funzionalità della tua pipeline mediante l'integrazione con altri strumenti e servizi.
1. Seleziona la toolchain che vuoi utilizzare o immetti un nome per la nuova toolchain da creare.
1. Fai clic su **Crea**. Viene creata una pipeline vuota che viene rappresentata in forma di scheda nella pagina Panoramica della toolchain. 

##Inizia da un template di toolchain
{: #starting_from_a_toolchain_template}

Per creare e configurare una toolchain di fornitura continua da un [template ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/create){: new_window}:

1. Nella pagina **Create a Toolchain**, fai clic su un template di toolchain.  
1. Esamina il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain.

 **Suggerimento**: alcuni modelli della toolchain dispongono di più istanze di un'integrazione dello strumento. Ad esempio, il modello della toolchain Microservizi su {{site.data.keyword.Bluemix_notm}} Pubblico contiene tre istanze di GitHub e tre di Delivery Pipeline, una per ognuno dei tre microservizi.

 Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra ogni integrazione dello strumento che fa parte della toolchain.
 ![Diagramma_toolchain](images/toolchain_diagram.png)
1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se vuoi utilizzare un nome diverso, modifica il nome della toolchain.
1. Nella sezione Integrazioni dello strumento, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Alcune delle integrazioni dello strumento non richiedono configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configurazione delle integrazioni dello strumento](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**. Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain. Le integrazioni dello strumento configurate a seconda della toolchain selezionata e se stai utilizzando {{site.data.keyword.Bluemix_notm}} Pubblico o {{site.data.keyword.Bluemix_notm}} Dedicato. Ad esempio, quando crei una toolchain Microservizi in {{site.data.keyword.Bluemix_notm}} Pubblico, deve essere eseguita questa procedura:

 * La toolchain viene creata.
 * Se hai configurato Delivery Pipeline, le pipeline vengono create ed eseguite.
 * Se hai configurato Sauce Labs, la toolchain viene configurata per aggiungere i lavori di verifica Sauce Labs alle pipeline.
 * Se hai configurato PagerDuty, la toolchain viene configurata per inviare notifiche di avviso al servizio PagerDuty che hai specificato.
 * Se hai configurato Slack, la toolchain viene configurata per inviare notifiche sullo stato della distribuzione al canale Slack che hai specificato.
 * Se hai configurato un'integrazione dello strumento del codice di origine come GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.
