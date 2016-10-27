---

copyright:
  anni: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione alle toolchain (sperimentale)
{: #toolchains_getting_started}

Ultimo aggiornamento: 17 agosto 2016
{: .last-updated}  

Le toolchain sono disponibili negli ambienti pubblico e dedicato in {{site.data.keyword.Bluemix}}. Puoi creare una toolchain in due modi: utilizzando un template o creandola da un'applicazione.
{: shortdesc}

**Importante**: questa funzionalità è sperimentale. Le toolchain potrebbero non essere stabili e potrebbero essere modificate secondo modalità non compatibili con le versioni precedenti. Non se ne consiglia l'utilizzo negli ambienti di produzione. In {{site.data.keyword.Bluemix_notm}} pubblico, le toolchain sono disponibili solo nella regione Stati Uniti Sud.


##Introduzione alle toolchain: pubblico
{: #getting_started_public}

Ogni toolchain è associata a una specifica organizzazione e qualsiasi utente membro di tale organizzazione può accedere alle toolchain associate. Prima di creare una toolchain, assicurati di trovarti nell'organizzazione in cui vuoi creare la toolchain. Per passare a un'altra organizzazione, fai clic sull'icona **{{site.data.keyword.avatar}}** ![icona Avatar](../icons/i-avatar-icon.svg) nella barra dei menu per aprire il widget Account e supporto.

###Creazione di una toolchain da un template   
{: #creating_a_toolchain_from_a_template}

Puoi utilizzare un template come punto di partenza per creare una toolchain che includa un insieme specifico di integrazioni dello strumento.

1. Se stai creando la tua prima toolchain, assicurati che le toolchain siano abilitate nella tua organizzazione:
   1. Apri il dashboard DevOps e fai clic sulla scheda **Toolchain**.
   2. Se viene visualizzato, fai clic sul pulsante **Abilita toolchain** e attieniti alle richieste che ti vengono presentate per creare la tua toolchain.
   3. Se il pulsante **Abilita toolchain** non viene visualizzato, le toolchain sono già abilitate. Continua al passo 2.
1. Nel dashboard DevOps, sulla scheda **Toolchain**, fai clic sul pulsante di aggiunta (+) per creare una toolchain.
1. Fai clic su un template di toolchain. Ad esempio, per utilizzare un negozio online di esempio per creare la toolchain, fai clic su **Toolchain microservizi**. 
1. Nella pagina di creazione delle toolchain, esamina il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella sua fase del ciclo di vita nella toolchain. Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra tutte le integrazioni dello strumento che fanno parte della toolchain.
![Diagramma Toolchain](images/toolchain_diagram.png)

1. Esamina le informazioni predefinite per le impostazioni della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già disponi di una toolchain con quel nome o se vuoi utilizzarne uno diverso, puoi modificare il nome della toolchain.   
1. Nella sezione Integrazioni configurabili, seleziona tutte le integrazioni dello strumento che vuoi configurare per la tua toolchain. Alcune integrazioni non richiedono alcuna configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, vedi [Configurazione di integrazioni dello strumento](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**.  Vengono eseguiti automaticamente diversi passi per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, vengono attivate le pipeline.
 * Se hai configurato l'integrazione dello strumento Sauce Labs, l'integrazione Sauce Labs viene configurata per aggiungere dei lavori alle pipeline ed eseguire dei test. 
 * Se hai configurato l'integrazione dello strumento PagerDuty, l'integrazione PagerDuty viene configurata per inviare notifiche al canale che hai configurato in Slack. Queste notifiche indicano quando si verifica un problema. 
 * Se hai configurato l'integrazione dello strumento Slack, l'integrazione Slack viene configurata per inviare notifiche al canale che hai configurato in Slack. Queste notifiche indicano l'avanzamento della distribuzione, ad esempio `Connesso con Progetto XYZ`, `Pipeline configurata` e `Fase 'build' avviata`.
 * Se hai configurato l'integrazione dello strumento GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.


###Creazione di una toolchain da un'applicazione
{: #creating_a_toolchain_from_an_app}

Puoi creare una toolchain dalla tua applicazione. La toolchain può supportare varie attività continue come lo sviluppo, la distribuzione e il monitoraggio ed è associata alla tua applicazione. Ogni applicazione può essere associata a una toolchain. Quando esegui il push delle modifiche al repository GitHub della toolchain, la pipeline crea e distribuisce automaticamente l'applicazione.  

1. Se stai creando la tua prima toolchain, assicurati che le toolchain siano abilitate nella tua organizzazione:
   1. Apri il dashboard DevOps e fai clic sulla scheda **Toolchain**.
   2. Se viene visualizzato, fai clic sul pulsante **Abilita toolchain** e attieniti alle richieste che ti vengono presentate per creare la tua toolchain.
   3. Se il pulsante **Abilita toolchain** non viene visualizzato, le toolchain sono già abilitate. Continua al passo 2.
1. Nella pagina Panoramica della tua applicazione, sul tile Fornitura continua, fai clic su **Aggiungi toolchain**. In alternativa, in {{site.data.keyword.Bluemix_notm}} Classic Experience, nell'angolo superiore destro della pagina Panoramica della tua applicazione, fai clic su  **Aggiungi toolchain**. La tua applicazione viene configurata per la fornitura continua da un nuovo repository GitHub che viene popolato con il codice starter dell'applicazione.
1. Nella pagina di creazione delle toolchain, esamina il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella sua fase del ciclo di vita nella toolchain. 
1. Esamina le informazioni predefinite per le impostazioni della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già disponi di una toolchain con quel nome o se vuoi utilizzarne uno diverso, puoi modificare il nome della toolchain. 
1. Nella sezione Integrazioni configurabili, seleziona tutte le integrazioni dello strumento che vuoi configurare per la tua toolchain. Alcune integrazioni non richiedono alcuna configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, vedi [Configurazione di integrazioni dello strumento](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**.  Vengono eseguiti automaticamente diversi passi per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, vengono attivate le pipeline.
 * Se hai configurato l'integrazione dello strumento Sauce Labs, l'integrazione Sauce Labs viene configurata per aggiungere dei lavori alle pipeline ed eseguire dei test. 
 * Se hai configurato l'integrazione dello strumento PagerDuty, l'integrazione PagerDuty viene configurata per inviare notifiche al canale che hai configurato in Slack. Queste notifiche indicano quando si verifica un problema. 
 * Se hai configurato l'integrazione dello strumento Slack, l'integrazione Slack viene configurata per inviare notifiche al canale che hai configurato in Slack. Queste notifiche indicano l'avanzamento della distribuzione, ad esempio `Connesso con Progetto XYZ`, `Pipeline configurata` e `Fase 'build' avviata`.
 * Se hai configurato l'integrazione dello strumento GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.


##Introduzione alle toolchain: dedicato
{: #getting_started_dedicated}

Ogni toolchain è associata a una specifica organizzazione e qualsiasi utente membro di tale organizzazione può accedere alle toolchain associate. Prima di creare una toolchain, fai clic sull'icona **{{site.data.keyword.avatar}}** ![icona Avatar](../icons/i-avatar-icon.svg) nella barra dei menu per aprire il widget Account e supporto e visualizzare l'organizzazione in cui stai lavorando. Se questa non è l'organizzazione in cui vuoi creare la toolchain, passa a un'altra organizzazione. 

###Creazione di una toolchain da un template   
{: #creating_a_toolchain_from_a_template_dedicated}

Puoi utilizzare un template come punto di partenza per creare una toolchain che includa un insieme specifico di integrazioni dello strumento.

1. Se stai creando la tua prima toolchain, assicurati che le toolchain siano abilitate nella tua organizzazione:
   1. Apri il dashboard DevOps e fai clic sulla scheda **Toolchain**.
   2. Se viene visualizzato, fai clic sul pulsante **Abilita toolchain** e attieniti alle richieste che ti vengono presentate per creare la tua toolchain.
   3. Se il pulsante **Abilita toolchain** non viene visualizzato, le toolchain sono già abilitate. Continua al passo 2.
1. Nel dashboard {{site.data.keyword.Bluemix_notm}}, sulla scheda **DEVOPS**, fai clic sul pulsante di aggiunta (+) per creare una toolchain.
1. Fai clic su un template di toolchain. Ad esempio, per creare una semplice toolchain per distribuire una nuova applicazione Cloud Foundry, fai clic su **Toolchain Cloud Foundry semplice**. 
1. Nella pagina di creazione delle toolchain, esamina il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella sua fase del ciclo di vita nella toolchain. Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra tutte le integrazioni dello strumento che fanno parte della toolchain.
![Diagramma toolchain dedicato](images/toolchain_dedicated_diagram.png)

1. Esamina le informazioni predefinite per le impostazioni della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già disponi di una toolchain con quel nome o se vuoi utilizzarne uno diverso, puoi modificare il nome della toolchain.   
1. Nella sezione Integrazioni configurabili, seleziona tutte le integrazioni dello strumento che vuoi configurare per la tua toolchain. Alcune integrazioni non richiedono alcuna configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, vedi [Configurazione di integrazioni dello strumento](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**.  Vengono eseguiti automaticamente diversi passi per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, vengono attivate le pipeline.
 * Se hai configurato l'integrazione dello strumento GitHub Enterprise, il repository GitHub Enterprise di esempio viene clonato nel tuo account GitHub Enterprise.


###Creazione di una toolchain da un'applicazione
{: #creating_a_toolchain_from_an_app_dedicated}

Puoi creare una toolchain dalla tua applicazione. La toolchain può supportare varie attività continue come lo sviluppo, la distribuzione e il monitoraggio ed è associata alla tua applicazione. Ogni applicazione può essere associata a una toolchain. Quando esegui il push delle modifiche al repository GitHub Enterprise della toolchain, la pipeline crea e distribuisce automaticamente l'applicazione.  

1. Se stai creando la tua prima toolchain, assicurati che le toolchain siano abilitate nella tua organizzazione:
   1. Apri il dashboard DevOps e fai clic sulla scheda **Toolchain**.
   2. Se viene visualizzato, fai clic sul pulsante **Abilita toolchain** e attieniti alle richieste che ti vengono presentate per creare la tua toolchain.
   3. Se il pulsante **Abilita toolchain** non viene visualizzato, le toolchain sono già abilitate. Continua al passo 2.
1. Nell'angolo superiore destro della pagina Panoramica della tua applicazione, fai clic su **Aggiungi toolchain**. La tua applicazione viene configurata per la fornitura continua da un nuovo repository GitHub Enterprise che viene popolato con il codice starter dell'applicazione.
1. Nella pagina di creazione delle toolchain, esamina il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella sua fase del ciclo di vita nella toolchain. 
1. Esamina le informazioni predefinite per le impostazioni della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix_notm}}. Se già disponi di una toolchain con quel nome o se vuoi utilizzarne uno diverso, puoi modificare il nome della toolchain. 
1. Nella sezione Integrazioni configurabili, seleziona tutte le integrazioni dello strumento che vuoi configurare per la tua toolchain. Alcune integrazioni non richiedono alcuna configurazione. Per informazioni sulla configurazione delle integrazioni dello strumento, vedi [Configurazione di integrazioni dello strumento](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Crea**.  Vengono eseguiti automaticamente diversi passi per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, vengono attivate le pipeline.
 * Se hai configurato l'integrazione dello strumento GitHub Enterprise, il repository GitHub Enterprise di esempio viene clonato nel tuo account GitHub Enterprise.


##Visualizzazione di una toolchain
{: #viewing_a_toolchain}

Dopo aver configurato la toolchain e relative integrazioni dello strumento, puoi visualizzare una rappresentazione visiva della toolchain nella pagina Integrazioni strumento.

* Se utilizzi {{site.data.keyword.Bluemix_notm}} pubblico, sulla scheda **Toolchain** del dashboard DevOps, fai clic su una toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**. 
   
* Se utilizzi {{site.data.keyword.Bluemix_notm}} dedicato, sulla scheda **DEVOPS** del dashboard, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nell'angolo superiore destro della pagina Panoramica dell'applicazione, fai clic su **Visualizza toolchain**. 

* Per accedere a un'integrazione dello strumento che si trova nella tua toolchain, fai clic sul tile dello strumento.  
 
 **Suggerimento**: se disponi di più di un repository GitHub o GitHub Enterprise, potresti avere più tile per la stessa integrazione dello strumento in quanto ogni repository è rappresentato dal suo proprio tile. 


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [Crea un'applicazione con tre microservizi](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Crea una toolchain da un template in {{site.data.keyword.Bluemix_notm}} dedicato (sperimentale)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Crea una toolchain da un'applicazione in {{site.data.keyword.Bluemix_notm}} dedicato (sperimentale)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Link correlati
{: #general}

* [Toolchain microservizi (sperimentale)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Toolchain semplice (sperimentale)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method](https://www.ibm.com/devops/method){:new_window}
