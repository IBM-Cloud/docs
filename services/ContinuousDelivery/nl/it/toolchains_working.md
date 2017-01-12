---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestione delle toolchain
{: #toolchains_getting_started}

Ultimo aggiornamento: 17 novembre 2016
{: .last-updated}  

Una *toolchain* è una serie di integrazioni dello strumento che supporta le attività di operazioni, sviluppo e distribuzione. La potenza collettiva di una toolchain è superiore alla somma delle relative integrazioni dello strumento.
{: shortdesc}

Le toolchain sono disponibili negli ambienti pubblico e dedicato in {{site.data.keyword.Bluemix}}. Puoi creare una toolchain in due modi: utilizzando un template per creare una toolchain o creando una toolchain da un'applicazione. In {{site.data.keyword.Bluemix_notm}} pubblico, le toolchain sono disponibili solo nella regione degli Stati Uniti Sud.

##Introduzione alle toolchain: pubblico
{: #getting_started_public}

Ogni toolchain è associata a un'organizzazione (org) specifica e ogni utente che è membro di tale organizzazione può accedere alle toolchain associate. Prima di creare una toolchain, assicurati di lavorare nell'organizzazione in cui desideri creare la toolchain. L'organizzazione in cui stai attualmente lavorando è visualizzata nella barra dei menu. Per passare a un'altra organizzazione, fai clic sull'organizzazione nella barra dei menu e seleziona quella a cui vuoi passare.

###Creazione di una toolchain da un template   
{: #creating_a_toolchain_from_a_template}

Puoi utilizzare un template come punto di partenza per [creare una toolchain (il link si apre in una nuova finestra)](https://console.ng.bluemix.net/devops/create){: new_window} che includa una serie specifica di integrazioni dello strumento. Scopri come utilizzare i template da [IBM Bluemix Garage Method (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Accedi a [{{site.data.keyword.Bluemix_notm}} (il link si apre in una nuova finestra)](http://console.ng.bluemix.net){:new_window}. Si aprirà il Dashboard {{site.data.keyword.Bluemix_notm}} che mostra una panoramica dello spazio {{site.data.keyword.Bluemix_notm}} attivo per la tua organizzazione.
1. Dal menu hamburger, fai clic su **Servizi** e quindi su **DevOps**.
1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic su **Create a Toolchain**.
1. Nella pagina **Create a Toolchain**, fai clic su un template di toolchain.
1. Esamina il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain. Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra ogni integrazione dello strumento che fa parte della toolchain.
![Diagramma della toolchain](images/toolchain_diagram.png)

1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se vuoi utilizzare un nome diverso, modifica il nome della toolchain.  
1. Nella sezione Integrazioni configurabili, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Alcune delle integrazioni dello strumento non richiedono configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configurazione delle integrazioni dello strumento](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono create e attivate.
 * Se hai configurato l'integrazione dello strumento Sauce Labs, Sauce Labs viene impostato per aggiungere lavori alle pipeline ed eseguire i test.
 * Se hai configurato l'integrazione dello strumento PagerDuty, PagerDuty viene impostato per inviare notifiche di avviso al servizio che hai specificato.
 * Se hai configurato l'integrazione dello strumento Slack, Slack viene impostato per inviare notifiche sullo stato della distribuzione al canale che hai specificato.
 * Se hai configurato l'integrazione dello strumento GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.


###Creazione di una toolchain da un applicazione
{: #creating_a_toolchain_from_an_app}

Puoi creare una toolchain dalla tua applicazione. La toolchain può supportare varie attività continue come lo sviluppo, la distribuzione e il monitoraggio ed è associata alla tua applicazione. Ogni applicazione può essere associata con una toolchain. Quando esegui il push delle modifiche a un repository GitHub della toolchain, la pipeline automaticamente crea e distribuisce l'applicazione.  

1. Nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Abilita**. La tua applicazione è configurata per la distribuzione continua da un nuovo repository GitHub che viene popolato con il codice starter dell'applicazione.
1. Nella pagina di creazione della toolchain, rivedi il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain.
1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se vuoi utilizzare un nome diverso, modifica il nome della toolchain.
1. Nella sezione Integrazioni configurabili, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Alcune delle integrazioni dello strumento non richiedono configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configurazione delle integrazioni dello strumento](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono create e attivate.
 * Se hai configurato l'integrazione dello strumento Sauce Labs, Sauce Labs viene impostato per aggiungere lavori alle pipeline ed eseguire i test.
 * Se hai configurato l'integrazione dello strumento PagerDuty, PagerDuty viene impostato per inviare notifiche di avviso al servizio che hai specificato.
 * Se hai configurato l'integrazione dello strumento Slack, Slack viene impostato per inviare notifiche sullo stato della distribuzione al canale che hai specificato.
 * Se hai configurato l'integrazione dello strumento GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.


##Introduzione alle toolchain: dedicato
{: #getting_started_dedicated}

Ogni toolchain è associata a un'organizzazione specifica e ogni utente che è membro di tale organizzazione può accedere alle toolchain associate. Prima di creare una toolchain, fai clic sull'icona **{{site.data.keyword.avatar}}** nella barra dei menu per aprire il widget Account e supporto e visualizzare l'organizzazione in cui stai lavorando. Se tale organizzazione non è l'organizzazione dove desideri creare la toolchain, passa a un'altra organizzazione.

###Creazione di una toolchain da un template   
{: #creating_a_toolchain_from_a_template_dedicated}

Puoi utilizzare un template come punto di partenza nella creazione di una toolchain che includa una serie specifica di integrazioni dello strumento.

1. Nel dashboard {{site.data.keyword.Bluemix_notm}}, nella scheda **DEVOPS**, fai clic sul pulsante (+) per creare una toolchain.
1. Nella pagina **Create a Toolchain**, fai clic su un template di toolchain. 
1. Esamina il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain. Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra ogni integrazione dello strumento che fa parte della toolchain.
![Diagramma toolchain dedicato](images/toolchain_dedicated_diagram.png)

1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già hai una toolchain con lo stesso nome o se desideri utilizzare un nome differente, modifica il nome della toolchain.  
1. Nella sezione Integrazioni configurabili, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Alcune delle integrazioni dello strumento non richiedono configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configurazione delle integrazioni dello strumento](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono create e attivate.
 * Se hai configurato l'integrazione dello strumento PagerDuty, PagerDuty viene impostato per inviare notifiche di avviso al servizio che hai specificato.
 * Se hai configurato l'integrazione dello strumento Slack, Slack viene impostato per inviare notifiche sullo stato della distribuzione al canale che hai specificato.
 * Se hai configurato l'integrazione dello strumento GitHub Enterprise, il repository GitHub Enterprise di esempio viene clonato nel tuo account GitHub.


###Creazione di una toolchain da un applicazione
{: #creating_a_toolchain_from_an_app_dedicated}

Puoi creare una toolchain dalla tua applicazione. La toolchain può supportare varie attività continue come lo sviluppo, la distribuzione e il monitoraggio ed è associata alla tua applicazione. Ogni applicazione può essere associata con una toolchain. Quando esegui il push delle modifiche a un repository GitHub Enterprise della toolchain, la pipeline automaticamente crea e distribuisce l'applicazione.  

1. Nell'angolo in alto a destra della pagina di panoramica della tua applicazione, fai clic su **Add Toolchain**. La tua applicazione è configurata per la distribuzione continua da un nuovo repository GitHub Enterprise che viene popolato con il codice starter dell'applicazione.
1. Nella pagina di creazione della toolchain, rivedi il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain.
1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già hai una toolchain con lo stesso nome o se desideri utilizzare un nome differente, modifica il nome della toolchain.
1. Nella sezione Integrazioni configurabili, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Alcune delle integrazioni dello strumento non richiedono configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configurazione delle integrazioni dello strumento](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono create e attivate.
 * Se hai configurato l'integrazione dello strumento PagerDuty, PagerDuty viene impostato per inviare notifiche di avviso al servizio che hai specificato.
 * Se hai configurato l'integrazione dello strumento Slack, Slack viene impostato per inviare notifiche sullo stato della distribuzione al canale che hai specificato.
 * Se hai configurato l'integrazione dello strumento GitHub Enterprise, il repository GitHub Enterprise di esempio viene clonato nel tuo account GitHub.


##Visualizzazione di una toolchain
{: #viewing_a_toolchain}

Dopo aver configurato la toolchain e le sue integrazioni dello strumento, puoi visualizzare una rappresentazione visiva della toolchain.

* Se utilizzi {{site.data.keyword.Bluemix_notm}} pubblico, nella pagina **Toolchain** del dashboard DevOps, fai clic su una toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Fai quindi clic su **Panoramica**.  
   
* Se utilizzi {{site.data.keyword.Bluemix_notm}} dedicato, nel dashboard, fai clic sulla scheda **DEVOPS** e fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**.

* Per accedere all'integrazione dello strumento nella tua toolchain, fai clic sul tile dello strumento. 
 
 **Suggerimento**: se disponi di più di un repository GitHub o GitHub Enterprise, puoi avere più tile per la stessa integrazione dello strumento perché ogni repository è rappresentato dal proprio tile.


# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [Create and use your first toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Link correlati
{: #general}

* [Microservices toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method){:new_window}
