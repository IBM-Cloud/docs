---

copyright:
  years: 2017
lastupdated: "2017-4-5"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilizzo delle pipeline composite (Sperimentale)
{: #deliverypipeline_create_composite}

Con la funzione delle pipeline composite per {{site.data.keyword.deliverypipeline}}, puoi gestire i processi di fornitura continua e di integrazione continua ripetibili per le applicazioni software correlate.
{:shortdesc}

Crea le pipeline composite per gestire le applicazioni in una toolchain. Se la tua toolchain contiene applicazioni distribuite da {{site.data.keyword.deliverypipeline}}, la toolchain si aggiorna dinamicamente quando aggiungi o rimuovi le delivery pipeline dalla toolchain. Puoi anche aggiungere le applicazioni da origini esterne alla pipeline composita.

## Creazione di una pipeline composita
{: #compositepipeline_create_for_toolchain}

1. Dal menu accanto al logo Bluemix, fai clic su **Services > DevOps**

1. Dal menu di navigazione di sinistra, fai clic su **Pipelines**.

2. Abilita la funzione delle pipeline composita facendo clic su **Learn more** e quindi su **Enable**. La pipeline composita viene abilitata per ogni utente, per cui solo i membri della tua organizzazione (org) che optano per la funzione sperimentale visualizzano le pipeline composite che crei.

2. Fai clic su **Create** > **Composite Pipeline**.

3. Immetti un nome per la pipeline composita. Puoi anche modificare la descrizione della pipeline.

4. Dall'elenco **Toolchain**, seleziona una toolchain.

    1. Per creare una toolchain e una pipeline composita vuote, seleziona **New**.

    2. Per creare una pipeline composita per una delle tue toolchain, selezionane il nome.

5. Se hai creato una toolchain vuota, seleziona **Add default environments**. Utilizza questi ambienti logici predefiniti per controllare l'esecuzione del processo tramite le pipeline composita.

6. Fai clic su **Crea**.

Le fasi che hai configurato vengono automaticamente associate allo spazio appropriato nella tua organizzazione e viene creato un piano di distribuzione per la pipeline composita.

Se hai creato una pipeline composita per una toolchain che contiene delivery pipeline, le applicazioni per tutte le pipeline nella toolchain vengono aggiunte alla pipeline composita. Le fasi che hai configurato nelle delivery pipeline vengono automaticamente associate agli spazi appropriati nella tua organizzazione e vengono visualizzati i loro stati.
Per visualizzare le stato di ogni lavoro in un'applicazione, espandila.

Viene inoltre creato un piano di distribuzione per la pipeline composita. Per impostazione predefinita, i lavori per tutte le applicazioni sono eseguiti in parallelo per uno spazio, ma puoi modificare l'ordine di distribuzione delle tue applicazioni nel piano.

Se hai creato una pipeline composita per una nuova toolchain, viene creato un piano di distribuzione da personalizzare.

![Espandi ogni applicazione per visualizzare ogni lavoro nella propria pipeline](images/composite_view.png "espandi ogni applicazione")

## Modifica del piano di distribuzione
{: #compositepipeline_modify_dp}

Per impostazione predefinita, viene creato un piano di distribuzione per una pipeline composita. Questo piano di distribuzione acquisisce tutte le informazioni sulle fasi in ogni Delivery Pipeline nella toolchain. Puoi visualizzare e modificare il piano di distribuzione per ogni fase.

Nella fase in cui desideri modificare il piano di distribuzione, fai clic sul menu e su **Deployment plan**.

![Apri il piano di distribuzione](images/open_deployment_plan.png "apri il piano di distribuzione")

Viene visualizzato l'elenco delle attività di distribuzione per il tuo ambiente.

![Piano di distribuzione predefinito per una pipeline composita che contiene tre pipeline individuali](images/composite_deploy_plan.png)

Per ulteriori informazioni sulla modifica del piano di distribuzione, consulta [Personalizzazione dei piani di distribuzione per le pipeline composite](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html).

## Modifica delle pipeline individuali
{: #compositepipeline_add_job}

Puoi modificare le pipeline individuali dalla pipeline composita.

1. Espandi l'applicazione.

2. Dal menu della fase, fai clic su **Configure**.

3. Aggiungi, modifica o elimina i lavori dalla fase. Per le istruzioni dettagliate, consulta [Aggiunta di un lavoro a una fase](pipeline_build_deploy.html#deliverypipeline_add_job).

## Esecuzione dei lavori in una pipeline composita
{: #compositepipeline_run_jobs}

Dopo aver espanso un'applicazione per visualizzarne i lavori, puoi eseguire manualmente tutti i lavori in una fase. Fai clic sull'icona **Deploy to *stage*** nello spazio per un'applicazione.

![Esecuzione di una fase in una sola applicazione](images/composite_run_stage.png)

Per eseguire tutti i lavori in tutte le applicazioni presenti in uno spazio, fai clic sull'icona **Deploy to *space*** nello spazio per la pipeline composita.

![Esecuzione di una fase in tutte le applicazioni](images/composite_run_space.png)

I lavori vengono eseguiti in base al piano di distribuzione del blueprint composito.

## Visualizzazione dei log
{: #compositepipeline_view_logs}

Per visualizzare i log di un lavoro, espandi l'applicazione che contiene il lavoro e fai clic su di esso.

## Utilizzo di IBM Bluemix DevOps Connect per l'integrazione con IBM UrbanCode Deploy
{: #compositepipeline_devops_connect}

IBM Bluemix DevOps Connect coordina la comunicazione tra la tua installazione di IBM&reg; UrbanCode&reg; Deploy in loco e {{site.data.keyword.contdelivery_short}}. Dopo aver installato DevOps Connect, puoi creare le integrazioni che puoi utilizzare per gestire le applicazioni IBM UrbanCode Deploy con le pipeline composite.

**Prerequisiti**

   * Per la registrazione a DevOps Connect, devi avere un ID IBM.

   * Assicurati che [Java&trade; Runtime Environment versione 8 aggiornamento 121 o successiva ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://java.com/en/download/){:new_window} sia presente nel sistema host e che la variabile di sistema PATH sia impostata sulla sua ubicazione.

   * Hai bisogno di un token di autorizzazione di gestione da IBM UrbanCode Deploy.

Per utilizzare DevOps Connect per l'integrazione con IBM UrbanCode Deploy, completa la seguente procedura:

1. Installa DevOps Connect e utilizzalo per integrare la tua organizzazione con IBM UrbanCode Deploy.

  1. In una pipeline composita, fai clic su **Add app**. Dall'elenco **Managed by**, seleziona **IBM UrbanCode Deploy**.

  1. Visualizza le fasi di integrazione. Se visualizzi un elenco di applicazioni, fai prima clic sull'icona delle informazioni (![Icona informazioni](/images/info.png)) da **Apps** e quindi fai clic su **Configure IBM UrbanCode Deploy for this organization**.

  1. Nella finestra Configure UrbanCode Deploy Integration, fai clic su **Download** per scaricare DevOps Connect. Posiziona il file JAR in un computer che ha accesso a IBM UrbanCode Deploy.

  1. Dalla finestra, copia lo script di installazione di DevOps Connect. Lo script contiene il comando per avviare DevOps Connect e le credenziali obbligatorie per identificare il tuo servizio {{site.data.keyword.contdelivery_short}}.

  1. Nel computer in cui hai posizionato DevOps Connect, apri una shell di comandi e incolla lo script copiato in essa.

  1. Esegui lo script. DevOps Connect visualizza i messaggi di avvio.

1. Registrazione a DevOps Connect.

  1.  Nel computer in cui hai posizionato DevOps Connect, utilizza un browser per aprire il dashboard DevOps Connect. L'URL predefinito è https://localhost:8443. Per modificare l'URL e per informazioni sulle opzioni di avvio, consulta la documentazione [DevOps Connect ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/urbancode/plugindoc/urbancode-sync/ibm-urbancode-sync-utility/1-2/){:new_window}.


1. Nella pagina "Sign-in to IBM", immetti il tuo ID IBM e la password e fai clic su **Sign In**. Accedi ogni volta che avvii DevOps Connect.

1. Con DevOps Connect, utilizza IBM UrbanCode Deploy per il plugin DevOps Connect per creare un'integrazione tra la tua organizzazione e IBM UrbanCode Deploy.

    1. Nella pagina Integrations, fai clic su **Add New**.

    1. Nel campo **Name**, immetti un nome per l'integrazione.

    1. Dall'elenco **Integration Type**, seleziona **IBM UrbanCode Deploy for DevOps Connect**.

    1. Nel campo **Server URI**, immetti l'URL pubblico del server IBM UrbanCode Deploy; ad esempio, `https://my_UCD.example.com:8443`.

    1. Nel campo **Authentication Token**, immetti o incolla il token di autenticazione che è stato generato da IBM UrbanCode Deploy.

    1. Nel campo **Admin User Email**, immetti il tuo indirizzo email.

    1. Per confermare che l'integrazione ha avuto esito positivo, fai clic su **Run Integration**. DevOps Connect si collega all'istanza IBM UrbanCode Deploy specificata nel campo **Server URI**. DevOps Connect è autorizzato dal token che è stato incollato nel campo **Authentication Token**.

    1. Fai clic su **Salva**.

Se la tua integrazione ha esito positivo, puoi aggiungere le applicazioni IBM UrbanCode Deploy alle tue pipeline composite. Per ulteriori informazioni, consulta [Aggiunta delle applicazioni da IBM UrbanCode Deploy](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_add_apps).


## Aggiunta delle applicazioni da IBM UrbanCode Deploy
{: #compositepipeline_add_apps}

Se sei membro di un'organizzazione che è stata integrata con IBM UrbanCode Deploy utilizzando DevOps Connect, puoi aggiungere le applicazioni a cui puoi accedere in IBM UrbanCode Deploy alla pipeline composita. Per le istruzioni di installazione, consulta [Utilizzo di IBM Bluemix DevOps Connect per l'integrazione con IBM UrbanCode Deploy](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_devops_connect).

Quando sei un membro di un'organizzazione collegata a IBM UrbanCode Deploy, puoi aggiungere le applicazioni UrbanCode Deploy alle pipeline composite, selezionare i processi dell'applicazione da includere nel piano di distribuzione e personalizzare la distribuzione delle applicazioni.

1. Dalla pipeline composita, fai clic su **Add app**.

2. Dall'elenco **Managed by**, seleziona **IBM UrbanCode Deploy**. Se hai recentemente integrato {{site.data.keyword.contdelivery_short}} con IBM UrbanCode Deploy, potresti dover aggiornare il tuo browser per visualizzare il tuo server.

3. Seleziona le applicazioni e fai clic su **Continue**. Vengono visualizzati tutti i processi dell'applicazione disponibili per le applicazioni IBM UrbanCode Deploy. Le voci per eseguire i processi che hai selezionato vengono aggiunte al piano di distribuzione.

4. Seleziona i processi dell'applicazione da utilizzare per le applicazioni. Utilizza le opzioni di ricerca e filtro per individuare i processi.

5. Fai clic su **Salva**. Ogni applicazione IBM UrbanCode Deploy che hai selezionato viene visualizzata come un'applicazione nella pipeline composita.

6. Associa gli ambienti dalle applicazioni IBM UrbanCode Deploy agli ambienti logici della pipeline composita:

    1. Dal menu accanto a un nome dell'ambiente logico, seleziona **Manage logical environments**.

    ![Selezione Gestione ambienti logici](images/composite_logical_env.png)

    2. Per ogni applicazione nella pipeline composita, seleziona gli ambienti che hai definito in IBM UrbanCode Deploy. I processi dell'applicazione che hai selezionato sono eseguiti solo negli ambienti da tale applicazione.

    3. Fai clic su **Salva**.

    4. Ripeti questi passi per ogni ambiente logico che utilizzi.
