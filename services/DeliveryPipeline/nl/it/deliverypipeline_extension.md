---

copyright:
  years: 2015, 2016

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

# Estensione del servizio {{site.data.keyword.deliverypipeline}}
{: #deliverypipeline_extending}
Ultimo aggiornamento: 29 agosto 2016
{: .last-updated}

Puoi estendere le funzionalità del servizio {{site.data.keyword.deliverypipeline}} configurando i tuoi lavori in modo da utilizzare i servizi supportati. Ad esempio, i lavori di verifica possono eseguire delle scansioni di codice statico e i lavori di creazione possono globalizzare le stringhe.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->

Le seguenti attività descrivono come integrare gli strumenti selezionati con un Delivery Pipeline.

## Esecuzione delle scansioni di codice statico utilizzando la pipeline

{: #deliverypipeline_scan}

Desideri ricercare i problemi di sicurezza nel tuo codice prima di distribuirlo? Quando utilizzi IBM® Static Analyzer for Bluemix™ come parte della tua pipeline, puoi eseguire dei controlli automatizzati nei tuoi file binari di creazione `.war`, `.ear`, `.jar` o `.class` statici della tua applicazione Java™.

Una pipeline che utilizza il servizio Static Analyzer normalmente include tre fasi:

+ Una fase di build per generare i file di origine
+ Una fase di elaborazione che include tali lavori:
  + Un lavoro di creazione per eseguire il servizio Static Analyzer
  + Un lavoro di creazione per eseguire la creazione del contenitore
+ Una fase di distribuzione per distribuire il contenitore


### Creazione di una scansione di codice statico

Prima di iniziare, [riesamina i Termini di utilizzo per il servizio](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-6814-01).

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Crea una fase di elaborazione.

  a. Fai clic su **AGGIUNGI FASE**.

  b. Denomina la fase, ad esempio, `Elaborazione`.

  c. Per il tipo di input, seleziona **Risorse di build**.

  d. Per la fase e il lavoro, verifica i valori e aggiornali se necessario.

2. Nella fase di elaborazione, aggiungi un lavoro di creazione per eseguire la scansione del codice.

  a. Nella scheda **LAVORI**, fai clic su **AGGIUNGI LAVORO**.

  b. Per il tipo di lavoro, seleziona **Verifica**.

  c. Per il tipo di tester, seleziona **IBM Security Static Analyzer**.

  d. Per l'organizzazione e lo spazio, verifica i valori e aggiornali se necessario.

  e. Seleziona o deseleziona la casella di spunta **Configura il servizio e lo spazio per me** se necessario.

    * Se desideri che la pipeline verifichi il tuo spazio Bluemix per il servizio e che un'applicazione associ il servizio al contenitore, seleziona la casella di spunta. Se il servizio o l'applicazione associata non esistono, la pipeline aggiunge il piano gratuito del servizio al tuo spazio. L'applicazione associata che viene creata è denominata `pipeline_bridge_app`. Quindi, la pipeline utilizza le credenziali da pipeline_bridge_app per accedere ai servizi associati.

    * Se hai già configurato il servizio e l'applicazione è già associata nel tuo spazio Bluemix o se desideri [configurare questi requisiti manualmente](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), lascia la casella di spunta non selezionata.

  f. Nel campo **Minuti di attesa per il completamento dell'analisi**, immetti un valore compreso tra 0 e 59 minuti. Il valore predefinito è 5 minuti. Un URL al dashboard di Static Analyzer è presente nei log della console alla fine del lavoro.

     Se la scansione di Static Analyzer non viene completata entro il tempo specificato, il lavoro ha esito negativo. Tuttavia, l'analisi della scansione continua ad essere eseguita e puoi visualizzarla nel dashboard di Static Analyzer. Dopo che la scansione di Static Analyzer è stata completata, se riesegui il lavoro, la richiesta di scansione non viene reinviata e il lavoro della pipeline può essere completato. In alternativa, puoi configurare la pipeline in modo da non venir bloccata da un risultato della scansione positivo. Per le istruzioni, consulta la seguente fase.

  g. Seleziona o deseleziona la casella di spunta **Arrestare l'esecuzione di questa fase se il lavoro non riesce** a seconda di cosa desideri succeda se il lavoro non riesce o va in timeout. I lavori possono avere esito negativo quando le vulnerabilità sono elevate.

    * Se selezioni la casella di spunta e il lavoro ha esito negativo, i successivi lavori nella fase e le successive fasi non saranno eseguiti.

    * Se deselezioni la casella di spunta e il lavoro ha esito negativo, la fase continua senza bloccare i successivi lavori e fasi. Ad esempio, se sai che il report include molti problemi di elaborazione, puoi configurare la fase in modo che continui perché la scansione può durare a lungo. In questo scenario, potresti non voler arrestare il resto dei tuoi lavori e fasi solo perché la scansione impiega troppo tempo.

  h. Fai clic su **SALVA**.

3. Quando il lavoro termina, visualizza i risultati facendo clic su **Visualizza log e cronologia**. Se l'analisi ha esito positivo o va in timeout, viene visualizzato un URL nei risultati della scansione. Se lo stato della scansione è in attesa, attendi finché la scansione finisca per visualizzare i risultati completi.

4. Se hai bisogno di eseguire nuovamente la fase di elaborazione prima che termini l'analisi, puoi farlo. Tuttavia, nelle seguenti situazioni, non viene reinviata una nuova analisi e vengono utilizzati i precedenti risultati:
  * La fase di elaborazione è ancora in esecuzione quando hai avviato la nuova analisi
  * Una scansione è già stata inviata per la build
  * Non è ancora stata eseguita una nuova creazione dell'origine

5. Per avviare una nuova analisi, completa una delle seguenti fasi:
  * Esegui la fase di build che si inserisce nella fase di elaborazione e quindi esegui nuovamente la fase di elaborazione.
  * Apri l'URL per i risultati della scansione e fai clic sull'icona **Cestino**. Quindi, esegui nuovamente la fase di elaborazione.

Esempi di output della console:

**Scansione con esito positivo**
![Esempio di scansione con esito positivo](images/analyzer_success.png)

**Scansione in attesa**
![Esempio di scansione in attesa](images/analyzer_pending.png)

Per ulteriori informazioni sull'utilizzo del servizio Static Analyzer, [consulta i documenti del servizio Static Analyzer](https://console.ng.bluemix.net/docs/services/ApplicationSecurityonCloud/index.html).

<!--

## Globalizing strings by using the pipeline
{: #deliverypipeline_globalize}

You can translate strings automatically into other languages when you use the IBM Globalization Pipeline service with your pipeline. IBM Globalization Pipeline uses machine translation to translate your source files as part of the pipeline's build and deployment process.

You can also update the machine-translated strings within the globalization project. A translator or native speaker of the language can then review the machine-translated strings to ensure that they are of a high quality.

To see an example of a typical pipeline that uses the Globalization Pipeline service, watch this video:

<iframe width="640" height="360" src="https://www.youtube.com/embed/UToj7FIomCg?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

### Creating a globalization stage and job
Before you begin:

1. All English-translatable strings should be included in one or more `filename_en.properties` or `filename_en.json` files that all use the same name. For example: `messages_en.properties`.

2. If your messages are in `.json` files, remove the depth from the structure by removing any subkeys. To remove the subkeys, change instances of `{key: {subkey: value, subkey:value}}` to `{key:value, key:value}`.

To create the globalization stage and job:

1. Create a globalization stage.

  a. Click **ADD STAGE**.

  b. Name the stage; for example, `Globalization`.

  c. For the input type, select **SCM repository**.

2. In the globalization stage, add a job to translate the source files.

  a. On the **JOBS** tab, click **ADD JOB**.

  b. For the job type, select **Build**.

  c. For the builder type, select **IBM Globalization Pipeline**.

  d. For the organization and space, verify the values and update them if needed.

  e. In the **Source file name** field, type the name and extension of the `.properties` or `.json` input file. If you have files in different subdirectories, but they all have the same name, you need to type the file name once only. For example, if you have a `messages_en.properties` file in three directories, type `messages_en.properties` for the source file name, and all files with that name will be translated.

  f. Determine whether to select the **Set up service and space for me** check box.

    * If you want the pipeline to check your Bluemix space for the service and an app that binds the service to the container, select this check box. If the service or bound app does not exist, the pipeline adds the free plan of the service to your space for you. The bound app that is created is named `pipeline_bridge_app`. Then, the pipeline uses the credentials from pipeline_bridge_app to access the bound services.

    * If you configured the service and bound app in your Bluemix space already or if you want to [configure these requirements manually](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), leave this check box cleared.

  g. For the Globalization bundle prefix, enter a prefix for the bundle name, which is structured in this format: `<globalization_bundle_prefix>.path.to.source.file`. The pipeline job creates this Globalization bundle for you in the Globalization Pipeline service.

    **Tip:** Use the DevOps Services project name in the prefix so that the project can be identified easily in the Globalization Pipeline service.

  h. Click **SAVE**.

3. Create another stage to package your app. For the input of the job in this stage, use the IBM Globalization Pipeline job from the previous stage. Do not use the source as the input. The Globalization Pipeline job augments the source files with the machine-translated strings.

4. To ensure that the machine-translated content is included in the packaged app, create another stage to package the app in. For the input to that stage, include the Globalization Pipeline job.

The machine translated files are placed in the same directory as the source `.properties` or `.json` file. To view the files, click **Job > Artifacts**.

After the stage is completed, you can review the translated files from the console output. You can also direct translators to the files so that they can review the machine-translation output and provide revisions to improve quality. The revisions are stored in a Cloudant™ database and take precedence over any future machine translations of the same strings.

For more information about using the Globalization Pipeline service from the Bluemix Dashboard, [see the Globalization Pipeline service documentation](https://www.ng.bluemix.net/docs/services/GlobalizationPipeline/index.html).

-->

## Creazione di notifiche Slack per le build nella pipeline
{: #deliverypipeline_slack}

Puoi inviare le notifiche sui risultati di build per IBM Container Service, IBM Security Static Analyzer e IBM Globalization dal tuo Delivery Pipeline ai tuoi canali Slack.

Prima di iniziare, crea o copia un URL del webhook Slack:

1. Apri la pagina di integrazione Slack per il tuo team: `https://_project_name_.slack.com/services`
2. Nell'elenco di integrazioni, individua **WebHook in entrata** e fai clic su **Aggiungi**.
3. Seleziona un canale e fai clic su **Aggiungi integrazione di WebHook in entrata**.
4. Aggiungi un **URL del webhook** o copiane uno esistente.

Per ulteriori informazioni, [consulta Incoming WebHooks nella documentazione Slack](https://api.slack.com/incoming-webhooks).

Per creare le notifiche Slack:

1. Nella pipeline, apri la configurazione per una fase.
2. Nella scheda **PROPRIETÀ AMBIENTE**, fai clic su **AGGIUNGI PROPRIETÀ**.
3. Seleziona **Proprietà testo**.
4. Immetti un nome e un valore per la proprietà di ambiente. Ripeti i passi per creare più proprietà di ambiente.

  *Tabella 1. Proprietà dell'ambiente per la configurazione delle notifiche Slack*

  <table>
  <tr>
  <th>Nome</th>
  <th>Valore</th>
  <th>Descrizione</th>
  <tr/>
  <tr>
    <td><code>SLACK_WEBHOOK_PATH</code></td>
    <td>Un URL</td>
    <td>Obbligatorio. L'URL del webHook salvato nelle impostazioni per il tuo progetto Slack.</td>
  </tr>
  <tr>
    <td><code>SLACK_COLOR</code></td>
    <td>Puoi immettere uno dei seguenti valori:
      <ul><li><code>good</code></li>
      <li><code>warning</code></li>
      <li><code>danger</code></li>
      <li>Ogni colore esadecimale, come ad esempio #439FEO</li></ul></td>
    <td>Facoltativo. Il colore del bordo che viene visualizzato al lato del messaggio in Slack. I colori predefiniti sono il verde per i messaggi positivi, il rosso per i messaggi negativi e grigio per i messaggi informativi.</td>
  </tr>
  <tr>
    <td><code>NOTIFY_FILTER</code></td>
    <td>Per ricevere solo un sottoinsieme di tipi di messaggi, immetti uno dei seguenti valori:
      <ul>
      <li><code>good</code>: ottieni solo i messaggi informativi, positivi e sconosciuti. I messaggi negativi non vengono inviati.</li>
      <li><code>bad</code>: ricevi tutti i messaggi.</li>
      <li><code>info</code>: ricevi solo i messaggi informativi. I messaggi positivi, negativi e sconosciuti non vengono inviati.</li>
      <li><code>unknown</code>: ricevi tutti i messaggi.</li></ul>
      Esempio: se imposti <code>NOTIFY_FILTER = bad</code>, vengono visualizzate solo le notifiche di errore nel canale Slack.</td>
    <td>Facoltativo. Decidi quale tipo di messaggi per cui inviare le notifiche. Per impostazione predefinita, vengono inviati i messaggi positivi e negativi, ma non in messaggi informativi.
      <ul><li><code>good</code>: risultati di build positivi.</li>
      <li><code>bad</code>: risultati di build negativi.</li>
      <li><code>info</code>: messaggi informativi sul processo di build.</li>
      <li><code>unknown</code>: ai messaggi sconosciuti non viene assegnato un tipo.</li></ul></td>
   </table>

5. Fai clic su **Salva**.

6. Ripeti questi passi per inviare le notifiche Slack per altre fasi che includono i lavori di IBM Container Service, IBM Security Analyzer e IBM Globalization.

La notifica di build che viene visualizzata in Slack include un link al progetto dei servizi DevOps a alcune volte al dashboard del progetto. Per aprire questi link un utente Slack deve essere registrato ai servizi DevOps ed essere membro del progetto in cui è configurata la pipeline.

## Creazione di notifiche HipChat per le build nella pipeline
{: #deliverypipeline_hipchat}

Puoi inviare le notifiche sui risultati di build per IBM Container Service, IBM Security Static Analyzer e IBM Globalization dal tuo Delivery Pipeline alle tue sale HipChat.

Prima di iniziare, crea o copia un token HipChat esistente:

1. Vai alla pagina del tuo account HipChat per il tuo team: `https://_project_name_.hipchat.com/account/api`
2. Crea un nuovo token o utilizzane uno esistente.

Per creare le notifiche HipChat:

1. Nella pipeline, apri la configurazione per una fase.
2. Nella scheda **PROPRIETÀ AMBIENTE**, fai clic su **AGGIUNGI PROPRIETÀ**.
3. Seleziona **Proprietà testo**.
4. Immetti un nome e un valore per la proprietà di ambiente. Ripeti i passi per creare più proprietà di ambiente.

  *Tabella 2. Proprietà dell'ambiente per la configurazione delle notifiche HipChat*

  <table>
  <tr>
  <th>Nome</th>
  <th>Valore</th>
  <th>Descrizione</th>
  </tr>
  <tr>
    <td><code>HIP_CHAT_TOKEN</code></td>
    <td>Stringa alfanumerica</td>
    <td>Obbligatorio. Consulta "Prima di iniziare" per istruzioni sulla creazione o la copia di un token HipChat esistente.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_ROOM_NAME</code></td>
    <td>Nome sala</td>
    <td>Obbligatorio.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_COLOR</code></td>
    <td>Immetti uno dei seguenti valori:
      <ul><li><code>yellow</code></li>
      <li><code>red</code></li>
      <li><code>green</code></li>
      <li><code>purple</code></li>
      <li><code>gray</code></li>
      <li><code>random</code></li></ul>
    </td>
    <td>Facoltativo: specifica il colore di background e del bordo delle notifiche HipChat. Se imposti <code>HIP_CHAT_COLOR</code>, non hai bisogno di specificare il colore quando richiami lo script.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_COLOR</code></td>
    <td>Immetti uno dei seguenti valori:
      <ul><li><code>good</code></li>
      <li><code>danger</code></li>
      <li><code>info</code></li></ul>
    Questa variabile si applica sia ai colori di notifica HipChat che Clack. Se specifichi <code>NOTIFICATION_COLOR</code>, non dovrai specificare <code>HIP_CHAT_COLOR</code> o <code>SLACK_COLOR</code>.</td>
    <td>Facoltativo: specifica il colore di background e del bordo delle notifiche HipChat e Slack. Se imposti <code>NOTIFICATION_COLOR</code>, non hai bisogno di specificare il colore quando richiami lo script.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_LEVEL</code></td>
    <td>Immetti uno dei seguenti valori:
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul></td>
    <td>Facoltativo: Specifica il livello delle notifiche. Consulta <code>NOTIFICATION_FILTER</code> per ulteriori dettagli su come attivare le notifiche.</td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_FILTER</code></td>
    <td>Immetti uno dei seguenti valori:
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul>
    <td>Facoltativo: Specifica il livello di filtro delle notifiche. Le notifiche vengono inviate quando sono soddisfatti i seguenti parametri:
      <ul><li><code>NOTIFICATION_FILTER = good</code> e <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> o <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = info</code> e <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code>, <code>info</code> o <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = bad</code> e <code>NOTIFICATION_LEVEL = bad</code> o <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = unknown</code> e <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> o <code>unknown</code></li></ul></td>
    </tr>
  </table>

5. Fai clic su **Salva**.

6. Ripeti questi passi per inviare le notifiche HipChat per altre fasi che includono i lavori di IBM Container Service, IBM Security Static Analyzer e IBM Globalization.

## Utilizzo di Active Deploy per la distribuzione senza tempo di inattività nella pipeline
{: #deliverypipeline_activedeploy}

Puoi automatizzare la distribuzione continua delle tue applicazioni o gruppi di contenitori utilizzando il servizio IBM® Active Deploy service in Delivery Pipeline dei servizi DevOps di Bluemix®. Per ulteriori informazioni sulle istruzioni introduttive, [consulta la documentazione di Active Deploy](https://new-console.ng.bluemix.net/docs/services/ActiveDeploy/updatingapps.html#adpipeline).

## Creazione e distribuzione delle immagini del contenitore con la pipeline
{: #deliverypipeline_containers}

Puoi automatizzare le tue build dell'applicazione e le tue distribuzioni del contenitore a Bluemix® utilizzando IBM® Continuous Delivery Pipeline for Bluemix. Il servizio Delivery Pipeline nei servizi DevOps supporta:
  - La creazione di immagini Docker
  - La distribuzione di immagini nei contenitori a Bluemix

Per ulteriori informazioni sulle istruzioni introduttive, consulta [la panoramica su Delivery Pipeline e i contenitori](https://new-console.ng.bluemix.net/docs/containers/container_pipeline_ov.html#container_pipeline_ov).
