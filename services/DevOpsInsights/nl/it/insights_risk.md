---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Rischio per le distribuzioni
{: #gettingstarted}

{{site.data.keyword.DRA_short}} fornisce un gran numero di informazioni sulle tue distribuzioni, particolarmente a rischio. Puoi utilizzarlo per automatizzare la protezione della qualità nella tua delivery pipeline utilizzando politiche e gate. 
{:shortdesc}

Dopo aver aperto {{site.data.keyword.DRA_short}} dalla tua toolchain, fai clic su **Deployment Risk**. Da lì, puoi ottenere una panoramica delle applicazioni nei tuoi ambienti di produzione e di preparazione ed eseguire il drill down per comprendere la copertura del codice, le prestazioni del test e i report di sicurezza. I dashboard sono automaticamente popolati con le informazioni più recenti dai test {{site.data.keyword.DRA_short}} della tua pipeline.

## Informazioni su Deployment Risk
{: #about}

Puoi utilizzare Deployment Risk per applicare gli standard di qualità nella tua toolchain tramite politiche e gate. Le politiche comprendono le serie di regole; i gate applicano e politiche. Ad esempio, potresti creare una politica "Unit Testing and Test Coverage" che richiede che le le build rispettino gli standard di verifica dell'unità e di copertura del test. Successivamente aggiungi un gate che fa riferimento alla politica al tuo processo di fornitura continua. Le build che non soddisfano la politica vengono arrestate da questo gate. 

Deployment Risk utilizza {{site.data.keyword.deliverypipeline}}, che è parte di {{site.data.keyword.contdelivery_full}} e con i progetti Jenkins. Ad alto livello, le istruzioni per l'utilizzo di entrambi sono simili.  

Se si sta utilizzando {{site.data.keyword.deliverypipeline}}, procedi come segue:

1. [Crea le politiche e le regole](#policies_and_rules) per {{site.data.keyword.DRA_short}} da gestire.
2. [Prepara le fasi della tua pipeline](#integrate_pipeline) per l'integrazione con {{site.data.keyword.DRA_short}}.

3. [Crea o modifica i lavori di verifica](#configure_pipeline_jobs) nella pipeline che carica i risultati in {{site.data.keyword.DRA_short}}.
4. [Aggiungi i gate](#configure_pipeline_gates) alla pipeline che effettua le decisioni di promozione basate su quei risultati e sulle tue politiche.
5. Esegui la pipeline e [visualizza i risultati](#view_results).

Se stai utilizzando Jenkins, segui questa procedura:

1. [Crea le politiche e le regole](#policies_and_rules) per {{site.data.keyword.DRA_short}} da gestire.
2. [Installa e configura il plugin Jenkins](#integrate_jenkins).
3. [Crea i gate e i lavori di verifica come descritto nelle istruzioni del plugin](#integrate_jenkins). I test caricano i risultati in {{site.data.keyword.DRA_short}} per le analisi e i gate utilizzano questi risultati per effettuare decisioni di promozione.
4. Esegui il progetto e [visualizza i risultati](#view_results). 

Non importa come crei e distribuisci il tuo codice, i risultati sono gli stessi: le build che soddisfano gli standard saranno spostate oltre i gate Deployment Risk, mentre quelle che non li soddisfano saranno arrestate. 

## Prerequisiti
{: #prerequisites}

Deployment Risk richiede alcune configurazioni oltre a quelle descritte in [Introduzione a {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Per utilizzare Deployment Risk, hai bisogno di due cose:

* Una istanza di {{site.data.keyword.deliverypipeline}} o un progetto Jenkins
* I test che desideri utilizzare per valutare il tuo progetto

## Creazione di politiche e regole
{: #policies_and_rules}

Le politiche sono serie di regole che controllano i gate nella tua delivery pipeline. Se il tuo codice non soddisfa o supera una politica approvata in un gate particolare, la distribuzione viene arrestata per prevenire che vengano rilasciati dei rischi.

Definisci le politiche in {{site.data.keyword.DRA_short}}. Le politiche sono create nell'organizzazione (org) {{site.data.keyword.Bluemix_notm}} che contiene {{site.data.keyword.DRA_short}}. Tutte le applicazioni nella stessa organizzazione possono utilizzare la politica. 

### Creazione di politiche
{: #create_policies}

Per creare una politica:

1. Dal menu di navigazione di sinistra, fai clic su **Settings**.

2. Fai clic su **Policies**.

3. Fai clic su **Create Policy** e immetti quindi un nome e una descrizione per la nuova politica.

4. Fai clic su **Next**.

4. Aggiungi almeno una regola alla politica:
  1. Fai clic su **Add Rule to Policy**.
  2. Seleziona il tipo di regola.
  3. Immetti i dettagli e le condizioni per la regola.
  4. Fai clic su **Save**.

5. Quando ha terminato di aggiungere le regole alla politica, fai clic su **Complete**.

### Creazione di regole
{: #creating_rules}

Le regole definiscono i criteri che le tue politiche utilizzano per valutare un esito positivo o negativo. Potresti creare una politica "Unit Testing and Test Coverage" che contiene una regola di verifica dell'unità che richiede l'80% di esito positivo della verifica dell'unità e una regola di copertura del test che richiede il 100% di copertura di codice. Se aggiungi un gate che fa riferimento a questa regola in una pipeline, il gate previene a tutte le build che non soddisfano entrambe le regole di procedere. 

Puoi richiedere l'esito positivo indipendentemente se hai contrassegnato i test come critici. Per creare una regola, seleziona una politica e fai clic su **Add Rule to Policy**. 

#### Creazione delle regole del test di verifica funzionale
{: #criteria_fvt}

1. Immetti un descrizione e seleziona un formato.

2. Specifica la percentuale di scenari di test che deve essere superata per essere considerata con esito positivo.

3. Definisci ogni scenario di test che è critico.

4. Per monitorare le regressioni dello scenario di test, seleziona la casella di spunta **Monitor for test case regression**.

5. Fai clic su **Save**.


#### Creazione delle regole per la verifica di unità
{: #criteria_ut}

1. Immetti un descrizione e seleziona un formato.

2. Specifica la percentuale di scenari di test che deve essere superata per essere considerata con esito positivo.

3. Definisci ogni scenario di test che è critico.

4. Per monitorare le regressioni dello scenario di test, seleziona la casella di spunta **Monitor for test case regression**.

5. Fai clic su **Save**.


#### Creazione delle regole di copertura del codice
{: #criteria_codecoverage}

1. Immetti un descrizione e seleziona un formato.

2. Specifica la percentuale di copertura del codice necessaria per essere considerato con esito positivo.

3. Per monitorare le regressioni di copertura del codice, seleziona la casella di spunta **Monitor for test case regression**.

4. Fai clic su **Save**.

#### Creazione di regole di scansione sicura statica
{: #criteria_static}

Puoi integrare {{site.data.keyword.DRA_short}} con IBM Application Security on Cloud per eseguire le scansioni dell'applicazione dinamica e del codice statico. Per ulteriori informazioni su Application Security on Cloud, consulta [la documentazione ufficiale](/docs/services/ApplicationSecurityonCloud/index.html).

1. Immetti una descrizione.

2. Specifica i numeri massimi dei problemi di severità bassa, alta e media consentiti dalla regola. 

3. Fai clic su **Save**.

#### Creazione di regole di scansione sicura dinamica
{: #criteria_dynamic}

Puoi integrare {{site.data.keyword.DRA_short}} con {{site.data.keyword.appseccloudfull}} per eseguire le scansioni dell'applicazione dinamica. Per ulteriori informazioni su Application Security on Cloud, consulta [la documentazione ufficiale](/docs/services/ApplicationSecurityonCloud/index.html).

1. Immetti una descrizione.

2. Specifica i numeri massimi dei problemi di severità bassa, alta e media consentiti dalla regola. 

3. Fai clic su **Save**.

## Configurazione di {{site.data.keyword.deliverypipeline}} 
{: #configuration}

Dopo aver aggiunto {{site.data.keyword.DRA_short}} a una toolchain e aver definito le politiche che monitora, integralo con {{site.data.keyword.deliverypipeline}}. Per ulteriori informazioni sulle pipeline, consulta [la documentazione ufficiale](/docs/services/ContinuousDelivery/pipeline_working.html).

### Preparazione delle fasi della pipeline
{: #integrate_pipeline}

Per far analizzare a Deployment Risk il tuo progetto, devi definire le fasi di produzione e di preparazione nella tua pipeline. Definisci le fasi utilizzando le proprietà di ambiente di testo, che puoi trovare in ogni menu di configurazione della fase ![Icona configurazione fase pipeline](images/pipeline-stage-configuration-icon.png) in **Environment Properties**.

1. Nella fase di preparazione, imposta la proprietà `LOGICAL_ENV_NAME` su `STAGING`. 

2. Nella fase di produzione, imposta la proprietà `LOGICAL_ENV_NAME` su `PRODUCTION`. 

Puoi anche aggiungere le seguenti proprietà alle fasi che creano o distribuiscono la tua applicazione:

* `LOGICAL_APP_NAME`, che definisce il nome dell'applicazione nel dashboard.
* `BUILD_PREFIX`, che definisce il testo che precede le build della fase. Questo testo viene anche visualizzato nel dashboard. 

### Aggiunta di lavori di verifica
{: #configure_pipeline_jobs}

Integra {{site.data.keyword.DRA_short}} nella tua pipeline utilizzando due tipi di lavori di verifica: uno che carica i risultati in {{site.data.keyword.DRA_short}} per l'analisi e i gate che utilizzano questa analisi. 

Per prima cosa, aggiungi i lavori di tester avanzato alla tua pipeline per eseguire i test e caricare i risultati. 

**Nota:** se desideri aggiornare un lavoro di verifica per caricare i risultati in {{site.data.keyword.DRA_short}}, salvane la configurazione in un luogo apposito prima di procedere. Quindi, apri il menu di configurazione del lavoro e passa ala passo 3. 

1. Nella fase in cui desideri aggiungere il lavoro che carica i risultati, fai clic sull'icona **Configurazione fase** ![Icona configurazione fase della pipeline](images/pipeline-stage-configuration-icon.png). Fai clic su **Configura fase**.
2. Crea un lavoro di verifica ed immetti un nome per esso. 
3. Per il tipo di lavoro, seleziona **Advanced Tester**.
4. Riempi i campi **Test Command** e **Working Directory** come preferisci per una lavoro di verifica di una pipeline normale. 
5. Riempi i campi rimanenti per caricare i risultati del test per un tipo di test particolare. 

 1. Scegli il tipo di metrica che corrisponde a quella definita nella politica {{site.data.keyword.DRA_short}} che desideri utilizzare.
 2. Immetti un'ubicazione del file del risultato. Questa ubicazione è relativa alla directory di lavoro. 

6. Se desideri caricare i risultati per un secondo tipo di test, riempi i campi con il prefisso *Ulteriori*.
7. Fai clic su **Salva** per ritornare alla pipeline.

I valori per i campi **Tipo di metrica** e **Ubicazione del File di risultato** devono corrispondere al formato corretto:

<table><thead>
<tr>
<th>Tipo di metrica</th>
<th>Formati supportati</th>
</tr>
</thead><tbody>
<tr>
<td>Test di verifica funzionale</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Verifica di unità</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Copertura del codice</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

La figura 1 mostra un lavoro di test configurato per eseguire le verifiche di unità, per caricare i risultati nel formato Mocha e per caricare i risultati della copertura del codice nel formato Istanbul.

![Lavoro di caricamento DevOps Insights](images/insights_upload_job.png)
*Figura 1. Carica i risultati in DevOps Insights*

### Definizione dei gate
{: #configure_pipeline_gates}

I gate {{site.data.keyword.DRA_short}} verificano se i tuoi risultati di test soddisfano una politica definita. Se la politica non viene soddisfatta, il gate {{site.data.keyword.DRA_short}} ha un malfunzionamento per impostazione predefinita. Puoi inoltre configurare i gate per funzionare nella modalità advisory per consentire l'avanzamento della pipeline anche dopo un malfunzionamento.

Il dashboard Deployment Risk si basa sulla presenza di un gate dopo un lavoro di distribuzione di preparazione. Se desideri utilizzare il dashboard, assicurati di avere un gate dopo aver distribuito l'ambiente in fase di preparazione, ma prima di distribuire un ambiente di produzione.

Di solito, i gate sono posizionati prima della promozione della build nella tua pipeline. Queste ubicazioni sono ideali per controllare la qualità della build nelle tue politiche per assicurati che siano sicure da promuovere da un ambiente a un altro. Tuttavia, puoi posizionare i gate ovunque nella pipeline in cui desideri che venga controllato un criterio specifico. I gate che sono posizionati prima di distribuire un ambiente in fase di preparazione ancora utilizzeranno le politiche, ma non compariranno nel dashboard Deployment Risk.

1. Nella fase, fai clic sull'icona **Configurazione fase** ![Icona configurazione fase della pipeline](images/pipeline-stage-configuration-icon.png) e fai clic su **Configura fase**.
2. Fai clic su **Aggiungi lavoro**. Per il tipo di lavoro, seleziona **Test**.
3. Per il tipo di tester, seleziona **Gate {{site.data.keyword.DRA_short}}**.
4. Specifica il nome dell'ambiente. Assicurati che questo valore corrisponda al valore che è stato definito nelle tue [proprietà di ambiente](#toolchain_pipeline_props).
5. Immetti il nome della politica da controllare in questo gate.

 Questo nome deve corrispondere esattamente a uno dei nomi della politica che hai definito. Puoi specificare solo politiche definite nella stessa organizzazione {{site.data.keyword.Bluemix_notm}} della tua toolchain.

6. Facoltativo: per passare una funzione gate ella modalità advisory, annulla la spunta della casella **Arrestare l'esecuzione di questa fase se il lavoro non riesce**. Nella modalità advisory, {{site.data.keyword.DRA_short}} completa le stesse analisi della politica nel gate e genera i report, ma se incontra un malfunzionamento, la pipeline non viene arrestata.
7. Fai clic su **Salva** per ritornare alla pipeline.
8. Configura i gate per tutte le politiche {{site.data.keyword.DRA_short}} ripetendo questi passi.

![Lavoro Deployment Risk Mocha](images/insights_gate_job.png)
*Figura 2. Gate DevOps Insights*

Dopo aver configurato la tua pipeline, inizia ad utilizzare {{site.data.keyword.DRA_short}}. Per le istruzioni, consulta [Esecuzione della Delivery Pipeline](/docs/services/DevOpsInsights/pipeline_decision_reports.html#toolchain_reports).

## Configurazione di un progetto Jenkins
{: #integrate_jenkins}

Dopo aver aggiunto {{site.data.keyword.DRA_full}} a una toolchain aperta e definito le politiche che monitora, puoi integrarlo con il tuo progetto Jenkins. 

Il plugin IBM Cloud DevOps per Jenkins integra i progetti Jenkins con le toolchain. Una *toolchain* è una serie di integrazioni dello strumento che supporta le attività di operazioni, sviluppo e distribuzione. La potenza collettiva di una toolchain è superiore alla somma delle relative integrazioni dello strumento. Le toolchain aperte fanno parte del servizio {{site.data.keyword.contdelivery_full}}. Per ulteriori informazioni sul servizio {{site.data.keyword.contdelivery_short}}, consulta [la sua documentazione](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Dopo aver installato il plugin IBM Cloud DevOps, puoi pubblicare i risultati del test in {{site.data.keyword.DRA_short}}, aggiungere i gate di qualità automatizzati e tracciare il rischio di distribuzione. Puoi anche inviare notifiche del lavoro ad altri strumenti nella tua toolchain, come Slack e PagerDuty. Per aiutarti a tracciare le distribuzioni, la toolchain può aggiungere i messaggi di distribuzione ai commit Git e ai relativi problemi Git e JIRA. Puoi anche visualizzare le distribuzioni nella pagina delle connessioni della toolchain. 

Il plugin fornisce le azioni di post creazione e le CLI per supportare l'integrazione. {{site.data.keyword.DRA_short}} aggrega e analizza i risultati dagli strumenti di verifica di unità, di test funzionali, di copertura del codice, delle scansioni del codice di sicurezza statico per determinare se il tuo codice soddisfa le politiche predefinite nei gate nel tuo processo di distribuzione. Se il tuo codice non soddisfa o supera una politica, la distribuzione viene arrestata, per prevenire che vengano rilasciati dei rischi. Puoi utilizzare {{site.data.keyword.DRA_short}} come una rete di sicurezza per il tuo ambiente di fornitura continua, come un modo per implementare e migliorare gli standard nel tempo e come uno strumento di visualizzazione dei dati per aiutarti nella comprensione dello stato del tuo progetto.

### Prerequisiti
{: #jenkins_prerequisites}

Devi accedere a un server in esecuzione su un progetto Jenkins.

### Creazione di una toolchain
{: #jenkins_create}

Prima di poter integrare {{site.data.keyword.DRA_short}} con un progetto Jenkins, devi creare una toolchain. 

1. Per creare una toolchain, passa alla [Pagina Crea una toolchain](https://console.ng.bluemix.net/devops/create) e segui le istruzioni in tale pagina. 

2. Dopo aver creato la toolchain, aggiungi {{site.data.keyword.DRA_short}} ad essa. Per istruzioni, consulta la [documentazione {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

### Installazione del plugin
{: #jenkins_install}

Per prima cosa, scarica il plugin da {{site.data.keyword.DRA_short}}.  

1. Dalla pagina della panoramica della toolchain, fai clic su **DevOps Insights**.
2. Fai clic su **Settings**, quindi su **Jenkins Plugin Setup**.
3. Segui le istruzioni nella pagina per scaricare il plugin.

Quindi, nel tuo server Jenkins, installa il plugin.

1. Fai clic su **Manage Jenkins &gt; Manage Plugins** e sulla scheda **Advanced**.
2. Fai clic su **Choose File** e seleziona il file di installazione del plugin IBM Cloud DevOps. 
3. Fai clic su **Upload**.
4. Riavvia Jenkins e verifica che il plugin sia stato installato.

### Configurazione dei lavori Jenkins per il dashboard Deployment Risk
{: #jenkins_configure}

Dopo aver installato il plugin, puoi integrare {{site.data.keyword.DRA_short}} nel tuo progetto Jenkins. 

Segui questa procedura per utilizzare il dashboard e i gate di Deployment Risk con il tuo progetto.

1. Apri la configurazione di ogni lavoro di cui disponi, come una creazione, una verifica o una distribuzione.

2. Aggiungi un'azione di post creazione per il tipo corrispondente:

   * Per i lavori di creazione, utilizza **Publish build information to IBM Cloud DevOps**.
   
   * Per i lavori di verifica, utilizza **Publish test result to IBM Cloud DevOps**.
   
   * Per i lavori di distribuzione, utilizza **Publish deployment information to IBM Cloud DevOps**.
   
3. Completa i campi richiesti. Questi possono variare in base al tipo di lavoro. 

   * Dall'elenco **Credentials**, seleziona i tuoi ID e password {{site.data.keyword.Bluemix_notm}}. Se non sono salvati in Jenkins, fai clic su **Add** per aggiungerli e salvarli. Verifica la tua connessione con {{site.data.keyword.Bluemix_notm}} facendo clic su **Test Connection**.
   
   * Nel campo **Build Job Name**, specifica il tuo nome del lavoro di build esattamente come è in Jenkins. Se la build si verifica con il lavoro di verifica, lascia questo campo vuoto. Se il lavoro di build si verifica al di fuori di Jenkins, seleziona la casella di spunta **Builds are being done outside of Jenkins** e specifica il numero e l'URL di build.
   
   * Per l'ambiente, se le verifiche sono in esecuzione nella fase di build, seleziona solo l'ambiente di build. Se le verifiche sono in esecuzione nella fase di distribuzione, seleziona l'ambiente di distribuzione e secifica il nome dell'ambiente. Sono supportati due valori: `STAGING` e `PRODUCTION`.
   
   * Per il campo **Result File Location**, specifica l'ubicazione del file del risultato. Se il test non genera un file del risultato, lascia questo campo vuoto. Il plugin carica un file del risultato predefinito basato sullo stato del lavoro di verifica corrente.

   Queste immagini illustrano le configurazioni di esempio:
   
   ![Carica informazioni di build](images/Upload-Build-Info.png "Pubblica le informazioni di build su DRA")
   *Pubblica le informazioni di build*
   
   ![Carica il risultato del test](images/Upload-Test-Result.png "Pubblica il risultato del test su DRA")
   *Pubblica il risultato del test*
   
   ![Carica le informazioni di distribuzione](images/Upload-Deployment-Info.png "Pubblica le informazioni di distribuzione su DRA")
   *Pubblica le informazioni di distribuzione*

4. Se desideri utilizzare i gate della politica {{site.data.keyword.DRA_short}} per controllare un lavoro di distribuzione di downstream, aggiungi un'azione di post creazione, **IBM Cloud DevOps Gate**. Scegli una politica e specifica lo scopo dei risultati del test. Per consentire ai gate della politica di evitare le distribuzioni di downstream, seleziona la casella di spunta **Fail the build based on the policy rules**. La seguente immagine mostra una configurazione di esempio:

    ![Gate DevOps Insights](images/DRA-Gate.png "Gate DevOps Insights")

5. Esegui il tuo lavoro di creazione Jenkins.

6. Visualizza il dashboard Deployment Risk passando a [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops), selezionando la tua toolchain e facendo clic su **DevOps Insights**.

Il dashboard Deployment Risk si basa sulla presenza di un gate dopo un lavoro di distribuzione di preparazione. Se desideri utilizzare il dashboard, assicurati di avere un gate dopo aver distribuito l'ambiente in fase di preparazione, ma prima di distribuire un ambiente di produzione.
    
### Configurazione delle notifiche
{: #jenkins_notifications}

Puoi configurare i tuoi lavori Jenkins in modo da inviare notifiche agli strumenti come Slack o PagerDuty seguendo le istruzioni nei [Documenti Bluemix](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins).

Questo esempio mostra come configurare `ICD_WEBHOOK_URL` per le configurazioni del lavoro:
![Imposta il parametro ICD_WEBHOOK_URL](images/Set-Parameterized-Webhook.png "Imposta il webhook con parametri")

Questo esempio mostra come configurare le azioni di post creazione per le notifiche del lavoro:
![Azioni di post creazione per la notifica webhook](images/PostBuild-WebHookNotification.png "Configura la notifica webhook nelle azioni di post creazione")

## Visualizzazione dei risultati
{: #view_results}

Dopo aver eseguito una pipeline, {{site.data.keyword.DRA_short}} inizia a raccogliere e analizzare i risultati del test da essa per stabilire una linea di base. I dati di ogni successiva esecuzione sono raccolti e confrontati con i risultati precedenti. I gate di decisione utilizzano questi dati per determinare quando arrestare una distribuzione. 

Puoi visualizzare i dati della valutazione del gate e la tua distribuzione dal dashboard Deployment Risk. Per aprire il dashboard, apri {{site.data.keyword.DRA_short}} e dal manu laterale, fai clic su **Deployment Risk**.

Se stai utilizzando una {{site.data.keyword.contdelivery_short}} pipeline, puoi visualizzare i report di esecuzione del gate individuali dalla stessa pipeline. Per visualizzare il report di decisione per un gate dalla pipeline:

1. Nella fase che contiene il gate da verificare, fai clic su **Visualizza log e cronologia**.

2. Dal lavoro che contiene il gate, fai clic sul nome del gate.

3. Nella vista del log, individua il messaggio `Check {{site.data.keyword.DRA_short}} report here` e fai clic sul link per aprire il report.






