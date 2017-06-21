---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Gestione di {{site.data.keyword.deliverypipeline}} {: #pipeline-working}

Per automatizzare le tue creazioni e le tue distribuzioni in {{site.data.keyword.Bluemix}}, utilizza {{site.data.keyword.deliverypipeline}} per {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Con {{site.data.keyword.deliverypipeline}}, puoi scegliere tra diversi tipi di build. Fornisci lo script
    di build e {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} lo esegue; non ha bisogno di impostare dei
    sistemi di build. Quindi, con un singolo clic, puoi distribuire automaticamente la tua applicazione a uno o più spazi {{site.data.keyword.Bluemix_notm}}, server Cloud Foundry pubblici o contenitori Docker su IBM Containers for {{site.data.keyword.Bluemix_notm}}.

I lavori di creazione compilano e impacchettano il codice sorgente della tua applicazione da repository Git. I lavori di creazione producono delle risorse utente distribuibili, quali file WAR o contenitori Docker per IBM Containers. Puoi
    inoltre eseguire delle verifiche di unità nella tua build automaticamente. Puoi impostare i tuoi lavori di creazione in modo che venga attivata una creazione ogni volta che si esegue il push del commit.

Un lavoro di distribuzione prende l'output da un lavoro di creazione e lo distribuisce a server IBM Containers o Cloud Foundry come {{site.data.keyword.Bluemix_notm}}.

Puoi eseguire la distribuzione a uno o più regioni e servizi. Ad esempio, puoi impostare il tuo {{site.data.keyword.deliverypipeline}} per utilizzare uno o più servizi, eseguire verifiche in una regione e distribuire in produzione in più regioni. Per ulteriori informazioni, consulta [Regioni](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}.

Se utilizzi più pipeline in una toolchain aperta, puoi creare una pipeline composita per gestire la distribuzione di tutte le pipeline da una sola ubicazione.

Esistono molti modi per creare una pipeline, incluso l'aggiunta di una pipeline a un'applicazione esistente e la creazione di una pipeline senza un'applicazione esistente. Se non disponi ancora di un servizio {{site.data.keyword.deliverypipeline}} nella tua organizzazione, puoi accedere al catalogo, fare clic su {{site.data.keyword.deliverypipeline}} e selezionare Crea.

Completa la seguente procedura per configurare una {{site.data.keyword.deliverypipeline}} per un'applicazione esistente:

1. Nel Dashboard dell'applicazione {{site.data.keyword.Bluemix_notm}}, fai clic sulla tua applicazione.
1. Dal menu nella barra dei menu {{site.data.keyword.Bluemix_notm}}, fai clic su **Servizi** e quindi su **DevOps**.
1. Fai clic su **Pipeline** e seleziona **Crea una pipeline**.

Per [creare una pipeline ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} configurata per distribuire un'applicazione Cloud Foundry, completa la seguente procedura:

1. Fai clic su **Cloud Foundry**.
1. Se vuoi utilizzare un nome diverso per la pipeline, modifica il suo nome predefinito.
1. Se vuoi utilizzare un nome diverso per l'applicazione, modifica il suo nome predefinito. Questo nome indica l'applicazione in cui distribuisce la pipeline.
1. Se non hai una toolchain, ne viene creata una con un nome predefinito. Se vuoi utilizzare un nome diverso per la toolchain, modifica il suo nome. Con la toolchain, puoi estendere le funzionalità della tua pipeline mediante l'integrazione con altri strumenti e servizi. Per ulteriori informazioni sulle toolchain, consulta [Gestione delle toolchain](/docs/services/ContinuousDelivery/toolchains_working.html){: new_window}.

 **Suggerimento**: le pipeline e le toolchain appartengono alle organizzazioni. Se fai parte di un'organizzazione che ha delle toolchain, puoi essere aggiunto al controllo dell'accesso per ogni toolchain associata. Dopo che sei stato aggiunto all'elenco del controllo dell'accesso per una toolchain, puoi utilizzare tale toolchain e tutte le pipeline associate, anche se non le hai create. Per ulteriori informazioni sul controllo dell'accesso alle toolchain, consulta [Gestione dell'accesso](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}.

1. Seleziona la toolchain che vuoi utilizzare o immetti un nome per la nuova toolchain da creare.
1. Seleziona il tuo provider Git.

 **Suggerimento**: se non hai autorizzato {{site.data.keyword.Bluemix_notm}} ad accedere a GitHub, ti verrà chiesto di fare clic su **Autorizza** per andare al sito Web GitHub. Se non disponi di una sessione GitHub attiva, ti viene richiesto di accedere. Fai clic su **Authorize Application** per consentire a {{site.data.keyword.Bluemix_notm}} di accedere al tuo account GitHub. Se disponi di una sessione GitHub attiva ma non hai immesso la tua password recentemente, ti potrebbe essere richiesto di immettere la tua password GitHub per la conferma.

   * Se disponi di un repository e desideri utilizzarlo, per il tipo di repository, seleziona **Link**. Cerca la posizione del repository o selezionane uno dall'elenco di repository disponibili.

   * Se vuoi creare un repository vuoto, per il tipo di repository, seleziona **Nuovo**. Immetti un nome per il repository.

   * Se vuoi creare un clone di un repository, per il tipo di repository, seleziona **Copia**. Cerca la posizione del repository o selezionane uno dall'elenco di repository disponibili.

   * Se vuoi biforcare un repository GitHub in modo da poter fornire le modifiche attraverso le richieste di importazione, seleziona **Fork**. Cerca la posizione del repository o selezionane uno dall'elenco di repository disponibili.

1. Seleziona un repository o immetti un URL del repository.
1. Fai clic su **Crea**. La pipeline viene creata, configurata e visualizzata nella pagina Panoramica della toolchain.
 ![Scheda pipeline](images/cd_pipeline.png)
1. Se hai creato una pipeline nella toolchain che contiene una pipeline composita, la nuova pipeline viene aggiunta alla pipeline composita. Modifica il piano di distribuzione per includere le attività di distribuzione per la nuova pipeline. Consulta [Creazione di attività Delivery Pipeline](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_pipelineCD){: new_window}.

Per creare una [pipeline vuota ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} senza alcuna fase preconfigurata:

1. Fai clic su **Personalizzato**.
1. Se vuoi utilizzare un nome diverso per la pipeline, modifica il suo nome predefinito.
1. Se non hai una toolchain, ne viene creata una con un nome predefinito. Se vuoi utilizzare un nome diverso per la toolchain, modifica il suo nome. Con la toolchain, puoi estendere le funzionalità della tua pipeline mediante l'integrazione con altri strumenti e servizi.
1. Seleziona la toolchain che vuoi utilizzare o immetti un nome per la nuova toolchain da creare.
1. Fai clic su **Crea**. Viene creata una pipeline vuota che viene rappresentata in forma di scheda nella pagina Panoramica della toolchain.

Da {{site.data.keyword.deliverypipeline}}, puoi modificare la tua configurazione, controllare lo stato delle creazioni, dell'applicazione distribuita e delle ultime distribuzioni, visualizzare i log più recenti e i dettagli di distribuzione oppure eliminare la tua pipeline.
