---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione alle toolchain (sperimentale)
{: #toolchains_getting_started}

*Ultimo aggiornamento: 8 giugno 2016*
{: .last-updated}  

Una toolchain è una serie di integrazioni dello strumento che supporta le attività di operazioni, sviluppo e distribuzione. La potenza collettiva di una toolchain è superiore alla somma delle relative integrazioni dello strumento.
{: shortdesc}

Puoi creare una toolchain in due modi: utilizzando un template per creare una toolchain o creando una toolchain da un'applicazione. A seconda della toolchain o del template che utilizzi, la toolchain può includere un repository (repo) GitHub che viene popolato con il codice starter dell'applicazione e una delivery pipeline preconfigurata. Quando esegui il push delle modifiche a un repository GitHub della toolchain, la delivery pipeline automaticamente crea e distribuisce l'applicazione a {{site.data.keyword.Bluemix}}.

Come punto di partenza, puoi utilizzare un template toolchain per creare una toolchain che dispone di una serie di integrazioni dello strumento o una toolchain vuota a cui puoi aggiungere le integrazioni dello strumento.

**Importante**: questa funzionalità è sperimentale. Le toolchain potrebbero non essere stabili e potrebbero venire modificate in modi che le rendono non compatibili con le versioni precedenti. Non sono raccomandate per l'utilizzo in ambienti di produzione. Per utilizzare le toolchain, devi effettuare una [richiesta di accesso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} monouso. Le toolchain sono disponibili solo nella regione degli Stati Uniti Sud.


##Creazione di una toolchain da un template   
{: #creating_a_toolchain_from_a_template}

Dopo che la tua richiesta di accesso alla toolchain è stata approvata, puoi utilizzare un template come punto di partenza nella creazione di una toolchain che includa una serie specifica di integrazioni dello strumento.

1. Nel dashboard DevOps, nella scheda **Toolchains**, fai clic su **Create a Toolchain** per creare la tua prima toolchain. Se già disponi di una toolchain, fai clic sul pulsante di aggiunta (+) per creare un'altra toolchain.
1. Fai clic su un template toolchain. Ad esempio, per utilizzare un esempio di archivio online per creare una toolchain, fai clic su **Microservices Toolchain**. 
1. Nella pagina di creazione della toolchain, rivedi il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain. Il diagramma nella seguente immagine è un esempio. Quando crei una toolchain, il diagramma mostra ogni integrazione dello strumento che fa parte della toolchain.
![Diagramma della toolchain](images/toolchain_diagram.png)

1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix}}. Se già hai una toolchain con lo stesso nome o se desideri utilizzare un nome differente, modifica il nome della toolchain.  
1. Nella sezione Configurable Integrations, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configuring tool integrations](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Create**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono attivate.
 * Se hai configurato l'integrazione dello strumento Sauce Labs, l'integrazione Sauce Labs viene configurata per aggiungere lavori alle pipeline e per eseguire verifiche.
 * Se hai configurato l'integrazione dello strumento PagerDuty, l'integrazione PagerDuty viene configurata per inviare notifiche al canale configurato in Slack. Queste notifiche indicano quando si verifica un problema.
 * Se hai configurato l'integrazione dello strumento Slack, l'integrazione Slack viene configurata per inviare notifiche al canale configurato in Slack. Queste notifiche indicano l'avanzamento della distribuzione; ad esempio, `Connected with Project XYZ`, `Pipeline Configured` e `Stage 'build' started`.
 * Se hai configurato l'integrazione dello strumento GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.


##Creazione di una toolchain da un applicazione
{: #creating_a_toolchain_from_an_app}

Dopo che la tua richiesta di accesso alla toolchain è stata approvata, puoi creare una toolchain dalla tua applicazione. La toolchain può supportare il monitoraggio, la distribuzione e lo sviluppo continuo ed anche altro, e viene associata alla tua applicazione. Ogni applicazione può essere associata con una toolchain. Quando esegui il push delle modifiche a un repository GitHub della toolchain, la pipeline automaticamente crea e distribuisce l'applicazione.  

1. Nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Add Toolchain**. In alternativa, in Bluemix Classic Experience, fai clic su **ADD GIT**. La tua applicazione è configurata per la distribuzione continua da un nuovo repository GitHub che viene popolato con il codice starter dell'applicazione.
1. Nella pagina di creazione della toolchain, rivedi il diagramma della toolchain che stai per creare. Il diagramma mostra ogni integrazione dello strumento nella fase del suo ciclo di vita nella toolchain. 
1. Rivedi le informazioni predefinite per la configurazione della toolchain. Il nome della toolchain la identifica in {{site.data.keyword.Bluemix}}. Se già hai una toolchain con lo stesso nome o se desideri utilizzare un nome differente, modifica il nome della toolchain.
1. Nella sezione Configurable Integrations, seleziona ogni integrazione dello strumento che desideri configurare per la tua toolchain. Per informazioni sulla configurazione delle integrazioni dello strumento, consulta [Configuring tool integrations](../toolchains/toolchains_integrations.html){: new_window}.
1. Fai clic su **Create**.  Diversi passi vengono eseguiti automaticamente per configurare la tua toolchain:

 * La toolchain viene creata.
 * Se hai configurato l'integrazione dello strumento Delivery Pipeline, le pipeline vengono attivate.
 * Se hai configurato l'integrazione dello strumento Sauce Labs, l'integrazione Sauce Labs viene configurata per aggiungere lavori alle pipeline e per eseguire verifiche.
 * Se hai configurato l'integrazione dello strumento PagerDuty, l'integrazione PagerDuty viene configurata per inviare notifiche al canale configurato in Slack. Queste notifiche indicano quando si verifica un problema.
 * Se hai configurato l'integrazione dello strumento Slack, l'integrazione Slack viene configurata per inviare notifiche al canale configurato in Slack. Queste notifiche indicano l'avanzamento della distribuzione; ad esempio, `Connected with Project XYZ`, `Pipeline Configured` e `Stage 'build' started`.
 * Se hai configurato l'integrazione dello strumento GitHub, il repository GitHub di esempio viene clonato nel tuo account GitHub.

 
##Visualizzazione di una toolchain
{: #viewing_a_toolchain}

Dopo che la toolchain e tutte le integrazioni dello strumento sono state configurate, puoi visualizzare una rappresentazione grafica della toolchain nella pagina Integrazioni dello strumento.

1. Nel Dashboard DevOps, nella scheda **Toolchains**, fai clic su una toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain** e quindi su **Integrazioni dello strumento**.
1. Controlla la pagina per visualizzare una rappresentazione grafica della toolchain.
1. Per accedere all'integrazione dello strumento nella tua toolchain, fai clic sul tile dello strumento. 
 
 **Suggerimento**: se disponi di più di un repository GitHub, puoi avere più tile per la stessa integrazione dello strumento perché ogni repository necessita della propria pipeline.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Link correlati 
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [Create an application with three microservices](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}

## Link correlati 
{: #general}

* [Microservices toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM&reg; Bluemix&reg; Garage Method](https://www.ibm.com/devops/method){:new_window}
