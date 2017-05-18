---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Creazione delle toolchain
{: #toolchains_getting_started}

Una *toolchain* è una serie di integrazioni dello strumento che supporta le attività di operazioni, sviluppo e distribuzione. La potenza collettiva di una toolchain è superiore alla somma delle relative integrazioni dello strumento.
{: shortdesc}

Le toolchain aperte sono disponibili negli ambienti pubblico e dedicato in {{site.data.keyword.Bluemix}}. Puoi creare una toolchain in due modi: utilizzando un template o creandola da un'applicazione. 

Ogni toolchain è associata a un'organizzazione (org) specifica e ogni utente che è membro di tale organizzazione può essere aggiunto per accedere alle proprie toolchain associate. Per ulteriori informazioni sul controllo dell'accesso alle toolchain, consulta [Gestione dell'accesso](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}. Prima di creare una toolchain, assicurati di lavorare nell'organizzazione in cui desideri creare la toolchain. L'organizzazione con cui stai lavorando è visualizzata nella barra dei menu. Per passare a un'altra organizzazione, fai clic sull'organizzazione nella barra dei menu e seleziona quella a cui vuoi passare.


##Creazione di una toolchain da un template   
{: #creating_a_toolchain_from_a_template}

Puoi utilizzare un template come punto di partenza nella [creazione di una toolchain ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/create){: new_window} che includa una serie specifica di integrazioni dello strumento. Scopri come utilizzare i template da [IBM Cloud Garage Method ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Se utilizzi {{site.data.keyword.Bluemix_notm}} Pubblico, accedi a [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](http://console.ng.bluemix.net){:new_window}.
1. Se utilizzi {{site.data.keyword.Bluemix_notm}} Dedicato, accedi al tuo ambiente dedicato in {{site.data.keyword.Bluemix_notm}}.
1. Dal menu nella barra dei menu {{site.data.keyword.Bluemix_notm}}, fai clic su **Servizi** e quindi su **DevOps**.
1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic su **Create a Toolchain**.
1. Nella pagina **Create a Toolchain**, fai clic su un template di toolchain.
1. Esamina il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain.

 **Suggerimento**: alcuni modelli della toolchain dispongono di più istanze di un'integrazione dello strumento. Ad esempio, il modello della toolchain Microservizi su {{site.data.keyword.Bluemix_notm}} Pubblico contiene tre istanze di GitHub e tre di Delivery Pipeline, una per ognuno dei tre microservizi.

 Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra ogni integrazione dello strumento che fa parte della toolchain.
![Diagramma della toolchain](images/toolchain_diagram.png)

1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se vuoi utilizzare un nome diverso, modifica il nome della toolchain.  
1. Nella sezione Integrazioni dello strumento, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Alcune delle integrazioni dello strumento non richiedono configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configurazione delle integrazioni dello strumento](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**. Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain. Le integrazioni dello strumento configurate a seconda della toolchain selezionata e se stai utilizzando {{site.data.keyword.Bluemix_notm}} Pubblico o {{site.data.keyword.Bluemix_notm}} Dedicato. Ad esempio, quando crei una toolchain Microservizi in {{site.data.keyword.Bluemix_notm}} Pubblico, deve essere eseguita questa procedura:

 * La toolchain viene creata.
 * Se hai configurato Delivery Pipeline, le pipeline vengono create e attivate.
 * Se hai configurato Sauce Labs, la toolchain viene configurata per aggiungere i lavori di verifica Sauce Labs alle pipeline.
 * Se hai configurato PagerDuty, la toolchain viene configurata per inviare notifiche di avviso al servizio PagerDuty che hai specificato.
 * Se hai configurato Slack, la toolchain viene configurata per inviare notifiche sullo stato della distribuzione al canale Slack che hai specificato.
 * Se hai configurato un'integrazione dello strumento del codice di origine come GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.


##Creazione di una toolchain da un applicazione
{: #creating_a_toolchain_from_an_app}

Puoi creare una toolchain dalla tua applicazione. La toolchain può supportare varie attività continue come lo sviluppo, la distribuzione e il monitoraggio ed è associata alla tua applicazione. Ogni applicazione può essere associata con una toolchain. Quando esegui il push delle modifiche a un repository {{site.data.keyword.ghe_short}} o GitHub della toolchain, la pipeline automaticamente crea e distribuisce l'applicazione.  

1. Nella pagina della panoramica dell'applicazione, nella scheda di fornitura continua, fai clic su **Enable**. Se utilizzi {{site.data.keyword.Bluemix_notm}} Pubblico, la tua applicazione è configurata per la distribuzione continua da un nuovo repository GitHub che viene popolato con il codice starter dell'applicazione. Se utilizzi {{site.data.keyword.Bluemix_notm}} Dedicato, la tua applicazione è configurata per la distribuzione continua da un nuovo repository GitHub o {{site.data.keyword.ghe_short}} che viene popolato con il codice starter dell'applicazione.
1. Nella pagina di creazione della toolchain, rivedi il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain.
1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se vuoi utilizzare un nome diverso, modifica il nome della toolchain.
1. Nella sezione Integrazioni dello strumento, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Alcune delle integrazioni dello strumento non richiedono configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configurazione delle integrazioni dello strumento](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain. Le integrazioni dello strumento configurate a seconda della toolchain selezionata e se stai utilizzando {{site.data.keyword.Bluemix_notm}} Pubblico o {{site.data.keyword.Bluemix_notm}} Dedicato. Ad esempio, quando crei una toolchain da un'applicazione su {{site.data.keyword.Bluemix_notm}} Pubblico, devono essere eseguiti questi passi:

 * La toolchain viene creata.
 * Se hai configurato Delivery Pipeline, le pipeline vengono create e attivate.
 * Se hai configurato GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.


##Visualizzazione di una toolchain
{: #viewing_a_toolchain}

Dopo aver configurato la toolchain e le sue integrazioni dello strumento, puoi visualizzare una rappresentazione visiva della toolchain.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic sulla toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina della panoramica dell'applicazione, nella scheda di fornitura continua, fai clic su **View Toolchain**. Fai quindi clic su **Panoramica**.
2. Per accedere all'integrazione dello strumento nella tua toolchain, fai clic sullo strumento.

 **Suggerimento**: se disponi di più di un repository GitHub, {{site.data.keyword.ghe_short}} o Git, puoi avere più schede per la stessa integrazione dello strumento perché ogni repository è rappresentato dalla propria scheda. Se hai più di una pipeline, potresti avere più schede per la stessa integrazione dello strumento perché ogni pipeline è rappresentata dalla propria scheda. Ad esempio, quando crei una toolchain Microservizi, ognuno dei tre microservizi ha il proprio repository GitHub, {{site.data.keyword.ghe_short}} o Git e la propria pipeline.
