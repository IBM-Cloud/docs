---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione alle toolchain (Beta)
{: #toolchains_getting_started}

Ultimo aggiornamento: 7 ottobre 2016
{: .last-updated}  

Le toolchain sono disponibili negli ambienti pubblico e dedicato in {{site.data.keyword.Bluemix}}. Puoi creare una toolchain in due modi: utilizzando un template per creare una toolchain o creando una toolchain da un'applicazione. In {{site.data.keyword.Bluemix_notm}} pubblico, le toolchain sono disponibili solo nella regione degli Stati Uniti Sud.
{: shortdesc}

##Introduzione alle toolchain: pubblico
{: #getting_started_public}

**Nota:** assicurati di lavorare nella Nuova esperienza Bluemix controllando il banner superiore.

 * Se vedi un messaggio che indica di provare il nuovo Bluemix, stai lavorando nell'esperienza classica di Bluemix. Fai clic sul link per aprire la Nuova esperienza Bluemix.
 * Se non vedi tale messaggio, stai già lavorando nella Nuova esperienza Bluemix. 

Ogni toolchain è associata a un'organizzazione (org) specifica e ogni utente che è membro di tale organizzazione può accedere alle toolchain associate. Prima di creare una toolchain, assicurati di lavorare nell'organizzazione in cui desideri creare la toolchain. L'organizzazione in cui stai attualmente lavorando è visualizzata nella barra dei menu. Per passare a un'altra organizzazione, fai clic sull'organizzazione nella barra dei menu e seleziona quella a cui vuoi passare.

###Creazione di una toolchain da un template   
{: #creating_a_toolchain_from_a_template}

Puoi utilizzare un template come punto di partenza nella creazione di una toolchain che includa una serie specifica di integrazioni dello strumento.

1. Se stai creando la tua prima toolchain, assicurati che tali toolchain siano abilitate nella tua organizzazione:
   1. Apri il dashboard DevOps e fai clic sulla pagina **Toolchain**.
   2. Se viene visualizzato il pulsante **Enable Toolchains**, fai clic su di esso e segui le istruzioni per creare la tua toolchain.
   3. Se non viene visualizzato il pulsante **Enable Toolchains**, le toolchain sono già abilitate. Continua con il passo 2.
1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic sul pulsante (+) per creare una toolchain.
1. Fai clic su un template toolchain. Ad esempio, per utilizzare un esempio di archivio online per creare una toolchain, fai clic su **Microservices toolchain**. 
1. Nella pagina di creazione della toolchain, rivedi il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain. Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra ogni integrazione dello strumento che fa parte della toolchain.
![Diagramma della toolchain](images/toolchain_diagram.png)

1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già hai una toolchain con lo stesso nome o se desideri utilizzare un nome differente, modifica il nome della toolchain.  
1. Nella sezione Integrazioni configurabili, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Le stesse integrazioni dello strumento non richiedono alcuna configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configuring tool integrations (il link si apre in una nuova finestra)](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Create**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono attivate.
 * Se hai configurato l'integrazione dello strumento Sauce Labs, l'integrazione Sauce Labs viene configurata per aggiungere lavori alle pipeline e per eseguire verifiche.
 * Se hai configurato l'integrazione dello strumento PagerDuty, l'integrazione PagerDuty viene configurata per inviare notifiche al canale configurato in Slack. Queste notifiche indicano quando si verifica un problema.
 * Se hai configurato l'integrazione dello strumento Slack, l'integrazione Slack viene configurata per inviare notifiche al canale configurato in Slack. Queste notifiche indicano l'avanzamento della distribuzione; ad esempio, `Connected with Project XYZ`, `Pipeline Configured` e `Stage 'build' started`.
 * Se hai configurato l'integrazione dello strumento GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.


###Creazione di una toolchain da un applicazione
{: #creating_a_toolchain_from_an_app}

Puoi creare una toolchain dalla tua applicazione. La toolchain può supportare il monitoraggio, la distribuzione e lo sviluppo continuo ed anche altro, e viene associata alla tua applicazione. Ogni applicazione può essere associata con una toolchain. Quando esegui il push delle modifiche a un repository GitHub della toolchain, la pipeline automaticamente crea e distribuisce l'applicazione.  

1. Se stai creando la tua prima toolchain, assicurati che tali toolchain siano abilitate nella tua organizzazione:
   1. Apri il dashboard DevOps e fai clic sulla pagina **Toolchain**.
   2. Se viene visualizzato il pulsante **Enable Toolchains**, fai clic su di esso e segui le istruzioni per creare la tua toolchain.
   3. Se non viene visualizzato il pulsante **Enable Toolchains**, le toolchain sono già abilitate. Continua con il passo 2.
1. Nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Abilita**. In alternativa, nella modalità classica di {{site.data.keyword.Bluemix_notm}}, nell'angolo in alto a destra della pagina della panoramica della tua applicazione, fai clic su **Add Toolchain**. La tua applicazione è configurata per la distribuzione continua da un nuovo repository GitHub che viene popolato con il codice starter dell'applicazione.
1. Nella pagina di creazione della toolchain, rivedi il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain.
1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già hai una toolchain con lo stesso nome o se desideri utilizzare un nome differente, modifica il nome della toolchain.
1. Nella sezione Integrazioni configurabili, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Le stesse integrazioni dello strumento non richiedono alcuna configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configuring tool integrations (il link si apre in una nuova finestra)](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Create**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono attivate.
 * Se hai configurato l'integrazione dello strumento Sauce Labs, l'integrazione Sauce Labs viene configurata per aggiungere lavori alle pipeline e per eseguire verifiche.
 * Se hai configurato l'integrazione dello strumento PagerDuty, l'integrazione PagerDuty viene configurata per inviare notifiche al canale configurato in Slack. Queste notifiche indicano quando si verifica un problema.
 * Se hai configurato l'integrazione dello strumento Slack, l'integrazione Slack viene configurata per inviare notifiche al canale configurato in Slack. Queste notifiche indicano l'avanzamento della distribuzione; ad esempio, `Connected with Project XYZ`, `Pipeline Configured` e `Stage 'build' started`.
 * Se hai configurato l'integrazione dello strumento GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.


##Introduzione alle toolchain: dedicato
{: #getting_started_dedicated}

Ogni toolchain è associata a un'organizzazione (org) specifica e ogni utente che è membro di tale organizzazione può accedere alle toolchain associate. Prima di creare una toolchain, fai clic sull'icona **{{site.data.keyword.avatar}}** ![Icona Avatar](../icons/i-avatar-icon.svg) nella barra del menu per aprire il widget Account e supporto e visualizza l'organizzazione con cui stai lavorando. Se tale organizzazione non è l'organizzazione dove desideri creare la toolchain, passa a un'altra organizzazione.

###Creazione di una toolchain da un template   
{: #creating_a_toolchain_from_a_template_dedicated}

Puoi utilizzare un template come punto di partenza nella creazione di una toolchain che includa una serie specifica di integrazioni dello strumento.

1. Se stai creando la tua prima toolchain, assicurati che tali toolchain siano abilitate nella tua organizzazione:
   1. Apri il dashboard DevOps e fai clic sulla scheda **Toolchains**.
   2. Se viene visualizzato il pulsante **Enable Toolchains**, fai clic su di esso e segui le istruzioni per creare la tua toolchain.
   3. Se non viene visualizzato il pulsante **Enable Toolchains**, le toolchain sono già abilitate. Continua con il passo 2.
1. Nel dashboard {{site.data.keyword.Bluemix_notm}}, nella scheda **DEVOPS**, fai clic sul pulsante (+) per creare una toolchain.
1. Fai clic su un template toolchain. Ad esempio, per creare una toolchain semplice per distribuire una nuova applicazione Cloud Foundry, fai clic su **Simple Cloud Foundry toolchain**. 
1. Nella pagina di creazione della toolchain, rivedi il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain. Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra ogni integrazione dello strumento che fa parte della toolchain.
![Diagramma toolchain dedicato](images/toolchain_dedicated_diagram.png)

1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già hai una toolchain con lo stesso nome o se desideri utilizzare un nome differente, modifica il nome della toolchain.  
1. Nella sezione Integrazioni configurabili, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Le stesse integrazioni dello strumento non richiedono alcuna configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configuring tool integrations (il link si apre in una nuova finestra)](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Create**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono attivate.
 * Se hai configurato l'integrazione dello strumento GitHub Enterprise, il repository GitHub Enterprise di esempio viene clonato nel tuo account GitHub.


###Creazione di una toolchain da un applicazione
{: #creating_a_toolchain_from_an_app_dedicated}

Puoi creare una toolchain dalla tua applicazione. La toolchain può supportare il monitoraggio, la distribuzione e lo sviluppo continuo ed anche altro, e viene associata alla tua applicazione. Ogni applicazione può essere associata con una toolchain. Quando esegui il push delle modifiche a un repository GitHub Enterprise della toolchain, la pipeline automaticamente crea e distribuisce l'applicazione.  

1. Se stai creando la tua prima toolchain, assicurati che tali toolchain siano abilitate nella tua organizzazione:
   1. Apri il dashboard DevOps e fai clic sulla scheda **Toolchains**.
   2. Se viene visualizzato il pulsante **Enable Toolchains**, fai clic su di esso e segui le istruzioni per creare la tua toolchain.
   3. Se non viene visualizzato il pulsante **Enable Toolchains**, le toolchain sono già abilitate. Continua con il passo 2.
1. Nell'angolo in alto a destra della pagina di panoramica della tua applicazione, fai clic su **Add Toolchain**. La tua applicazione è configurata per la distribuzione continua da un nuovo repository GitHub Enterprise che viene popolato con il codice starter dell'applicazione.
1. Nella pagina di creazione della toolchain, rivedi il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain.
1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già hai una toolchain con lo stesso nome o se desideri utilizzare un nome differente, modifica il nome della toolchain.
1. Nella sezione Integrazioni configurabili, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Le stesse integrazioni dello strumento non richiedono alcuna configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configuring tool integrations (il link si apre in una nuova finestra)](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Create**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono attivate.
 * Se hai configurato l'integrazione dello strumento GitHub Enterprise, il repository GitHub Enterprise di esempio viene clonato nel tuo account GitHub.


##Visualizzazione di una toolchain
{: #viewing_a_toolchain}

Dopo che la toolchain e tutte le integrazioni dello strumento sono state configurate, puoi visualizzare una rappresentazione grafica della toolchain nella pagina Integrazioni dello strumento.

* Se utilizzi {{site.data.keyword.Bluemix_notm}} pubblico, nella pagina **Toolchain** del dashboard DevOps, fai clic su una toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
   
* Se utilizzi {{site.data.keyword.Bluemix_notm}} dedicato, nel dashboard, fai clic sulla scheda **DEVOPS** e fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**.

* Per accedere all'integrazione dello strumento nella tua toolchain, fai clic sul tile dello strumento. 
 
 **Suggerimento**: se disponi di più di un repository GitHub o GitHub Enterprise, puoi avere più tile per la stessa integrazione dello strumento perché ogni repository è rappresentato dal proprio tile.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [Create an application with three microservices (Beta) (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Link correlati
{: #general}

* [Microservices toolchain (Beta) (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Beta) (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method){:new_window}
