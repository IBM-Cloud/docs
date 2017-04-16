---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurazione delle integrazioni dello strumento
{: #integrations}

Ultimo aggiornamento: 18 ottobre 2016
{: .last-updated}

Puoi configurare le integrazioni dello strumento che supportano le attività di operazioni, sviluppo e distribuzione mentre crei una toolchain o puoi aggiungere e configurare le integrazioni dello strumento per personalizzare una toolchain esistente.  
{:shortdesc}

**Importante**: in {{site.data.keyword.Bluemix_notm}} pubblico, le toolchain sono disponibili solo nella regione degli Stati Uniti Sud.

Le integrazioni dello strumento disponibili per aggiungere e configurare la tua toolchain sono diverse a seconda se stai utilizzando le toolchain in {{site.data.keyword.Bluemix_notm}} pubblico o {{site.data.keyword.Bluemix_notm}} dedicato. Se stai utilizzando le toolchain in {{site.data.keyword.Bluemix_notm}} dedicato, le integrazioni dello strumento disponibili dipendono dal modo in cui {{site.data.keyword.jazzhub_title}} è stato configurato nel tuo ambiente specifico.

*Tabella 1. Integrazioni dello strumento disponibili per le toolchain in {{site.data.keyword.Bluemix_notm}} pubblico e dedicato*

|Integrazione strumento |Disponibile in {{site.data.keyword.Bluemix_notm}} pubblico	|Disponibile in {{site.data.keyword.Bluemix_notm}} dedicato (dipendente dall'ambiente)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|Sì	   	|Sì  		|
|{{site.data.keyword.DRA_short}} 		|Sì		|No			|
|Eclipse Orion {{site.data.keyword.webide}}		|Sì		|Sì			|
|GitHub		|Sì		|Sì		|
|Dedicated GitHub Enterprise			|No		|Sì		|
|Altro strumento			|Sì		|Sì		|
|PagerDuty			|Sì		|Sì		|
|Sauce Labs		|Sì		|No		|
|Slack			|Sì		|Sì		|

**Suggerimento**: se desideri avviare lo sviluppo con il codice di origine in {{site.data.keyword.Bluemix_notm}} pubblico, configura l'integrazione dello strumento GitHub prima di configurare la {{site.data.keyword.deliverypipeline}}. Se desideri avviare lo sviluppo con il codice in {{site.data.keyword.Bluemix_notm}} dedicato, configura l'integrazione dello strumento {{site.data.keyword.ghe_short}} o l'integrazione dello strumento GitHub prima di configurare la {{site.data.keyword.deliverypipeline}}. 


## Configurazione della delivery pipeline
{: #deliverypipeline}

La {{site.data.keyword.deliverypipeline}} automatizza la distribuzione continua dei tuoi progetti tramite una sequenza di fasi che richiamano i lavori di input ed esecuzione, come le creazioni, le verifiche e le distribuzioni. 

Configura la {{site.data.keyword.deliverypipeline}} per automatizzare la distribuzione, la verifica e la creazione continua delle tue applicazioni: 

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Integrazioni configurabili, fai clic su **Delivery Pipeline**. A seconda del template che utilizzi, possono essere disponibili diversi campi. Rivedi i valori di campo predefiniti e se necessario, modifica queste impostazioni.
1. Se disponi di una toolchain in {{site.data.keyword.Bluemix_notm}} pubblico a cui stai aggiungendo questa integrazione dello strumento, nella pagina **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella tua pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. Se stai utilizzando una toolchain in {{site.data.keyword.Bluemix_notm}} dedicato, nel dashboard, fai clic sulla scheda **DEVOPS** e fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Delivery Pipeline**.
1. Specifica un nome per la tua nuova pipeline.
1. Se stai pianificando di utilizzare la tua pipeline per distribuire un'interfaccia utente, seleziona la casella di spunta **Applicazione visualizzabile**. Tutte le applicazioni create dalla tua pipeline vengono visualizzate nell'elenco **VIEW APP** nella pagina Integrazioni dello strumento della toolchain.
1. Fai clic su **Create Integration** per aggiungere la {{site.data.keyword.deliverypipeline}} alla tua toolchain.
1. Fai clic sul tile per la {{site.data.keyword.deliverypipeline}} per visualizzare la pipeline e configurarla. Per informazioni sulla configurazione di una pipeline, consulta [Building and deploying pipelines (il link si apre in una nuova finestra)](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Suggerimento**: se desideri attivare la pipeline quando esegui il push delle modifiche al tuo repository GitHub o {{site.data.keyword.ghe_short}} devi configurare GitHub o {{site.data.keyword.ghe_short}} per la tua toolchain prima di definire le fasi per la tua pipeline. Le fasi della pipeline necessitano di URL Git per i tuoi repository. Ogni fase della pipeline può far riferimento solo a uno dei repository GitHub o {{site.data.keyword.ghe_short}} associato con la tua toolchain. Per istruzioni su come configurare GitHub, consulta la sezione [Problemi GitHub e GitHub](#github). Per istruzioni su come configurare Dedicated GitHub Enterprise, consulta [Getting started with {{site.data.keyword.ghe_long}} (il link si apre in una nuova finestra)](../services/ghededicated/index.html){: new_window}.
  
1. Facoltativo: se stai utilizzando una toolchain in {{site.data.keyword.Bluemix_notm}} pubblico e desideri che Sauce Labs esegua delle verifiche sulla tua applicazione, configura la {{site.data.keyword.deliverypipeline}} per aggiungere un lavoro di verifica Sauce Labs. Per istruzioni sulla configurazione del lavoro di verifica, consulta la sezione [Configurazione di un lavoro di verifica Sauce Labs nella tua pipeline](#config_saucelabs).

### Configurazione di un lavoro di verifica Sauce Labs nella tua pipeline
{: #config_saucelabs}

Prima di configurare un lavoro di verifica Sauce Labs nella tua pipeline, devi disporre di una pipeline funzionante provvista di fasi per creare e distribuire la tua applicazione e devi configurare Sauce Labs per la tua toolchain. Per istruzioni sulla configurazione di Sauce Labs, consulta la sezione [Sauce Labs](#saucelabs).

Configura la {{site.data.keyword.deliverypipeline}} per aggiungere un lavoro di verifica Sauce Labs:

1. Se non disponi di una fase che distribuisce una versione di verifica della tua applicazione, creane una.
1. Nella fase, aggiungi un lavoro di verifica dopo il lavoro di distribuzione. Posizionando questi lavori nella stessa fase, essi possono accedere alla stessa serie di proprietà di ambiente.   
  ![Lavoro di verifica](images/toolchain_test_job.png) 

1. Configura la fase: 

  a. Nella scheda **PROPRIETÀ AMBIENTE**, crea tre proprietà: CF_APP_NAME, SAUCE_USERNAME e SAUCE_ACCESS_KEY.
  
  b. Immetti il nome utente e la chiave di accesso Sauce Labs. In questo modo esternalizzi questi valori così da poterli utilizzare nelle tue verifiche.
  
1. Configura il lavoro di distribuzione. Nel campo **Deploy Script**, includi questo comando: `export CF_APP_NAME="$CF_APP"`. Questo comando esporta il nome dell'applicazione come una proprietà di ambiente.
1. Configura il lavoro di verifica. I valori nella seguente immagine sono degli esempi. I campi **Istanza del servizio**, **Destinazione**, **Organizzazione** e **Spazio** vengono popolati con il nome utente, la regione, l'organizzazione e lo spazio Sauce Labs che stai utilizzando.  
![Configura lavoro](images/toolchain_configure_job.png)

  a. Per il tipo di verifica, seleziona **Sauce Labs**.
  
  b. Per il servizio dell'istanza, seleziona il nome utente Sauce Labs che hai utilizzato nella configurazione di Sauce Labs per la tua toolchain. 
  
   **Suggerimento**: per visualizzare il nome utente e la chiave di accesso che hai utilizzato nella configurazione di Sauce Labs per la tua toolchain, fai clic su **Configura**. 
  
  c. Nel campo **Test Execution Command**, immetti i comandi per installare le dipendenze necessarie per le tue verifiche e quindi eseguile. Ad esempio, per un'applicazione Node.js, devi immettere questi comandi:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Se desideri visualizzare i report di verifica nei log del lavoro di verifica, seleziona la casella di spunta **Enable Test Report** e imposta il pattern del file dei risultati della verifica su `test/*.xml`.
  
1. Fai clic su **SAVE**. Se la tua pipeline è in esecuzione, puoi eseguire le tue verifiche Sauce Labs.

Per ulteriori informazioni, consulta [Delivery Pipeline (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.


## Aggiunta di {{site.data.keyword.DRA_short}}
{: #dra}

{{site.data.keyword.DRA_full}} raccoglie e analizza i risultati dalle verifiche di unità, dalle verifiche funzionali e dagli strumenti di copertura del codice per determinare se il tuo codice soddisfa i criteri predefiniti nei gate specificati nel tuo processo di distribuzione. Se il tuo codice non soddisfa o supera i criteri, la distribuzione viene arrestata per prevenire che vengano rilasciati dei rischi. Puoi utilizzare {{site.data.keyword.DRA_short}} come una rete di sicurezza per il tuo ambiente di distribuzione continua o come modo per implementare e migliorare gli standard di qualità. 

 **Nota**: questa integrazione dello strumento è preconfigurata. Non richiede alcun parametro di configurazione e non puoi riconfigurarla.
 
Aggiungi {{site.data.keyword.DRA_short}} per mantenere e migliorare la qualità del tuo codice {{site.data.keyword.Bluemix_notm}} monitorando le tue distribuzioni per identificare i rischi prima che vangano rilasciati.

1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, nella pagina **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Deployment Risk Analytics**. 
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per {{site.data.keyword.DRA_short}} e quindi completa i primi passi: creazione dei criteri, connessione dei criteri alla pipeline ed esecuzione della pipeline. Per ulteriori informazioni, consulta [{{site.data.keyword.DRA_short}} (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.


## Aggiunta di Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} è un ambiente basato sul web integrato dove puoi creare, modificare, eseguire il debug e completare le attività di controllo dell'origine. Puoi spostare senza interruzioni dalla modifica per l'esecuzione, l'invio e la distribuzione. 

 **Nota**: questa integrazione dello strumento è preconfigurata. Non richiede alcun parametro di configurazione e non puoi riconfigurarla.
 
Aggiungi l'integrazione dello strumento Eclipse Orion {{site.data.keyword.webide}} per completare le attività di controllo dell'origine:

1. Se disponi di una toolchain in {{site.data.keyword.Bluemix_notm}} pubblico a cui stai aggiungendo questa integrazione dello strumento, nella pagina **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. Se stai utilizzando una toolchain in {{site.data.keyword.Bluemix_notm}} dedicato, nel dashboard, fai clic sulla scheda **DEVOPS** e fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**.
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Eclipse Orion Web IDE**. 
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per la nuova Eclipse Orion {{site.data.keyword.webide}}. Il tuo spazio di lavoro viene prepopolato con i repository GitHub o {{site.data.keyword.ghe_short}}. I repository associati con la tua toolchain corrente sono evidenziati.

Per ulteriori informazioni, consulta [Modifica del codice con l'IDE web Eclipse Orion {{site.data.keyword.webide}} (il link si apre in una nuova finestra)](../toolchains/web_ide.html){: new_window}.


## Configurazione di GitHub
{: #github}

GitHub è un servizio host basato sul web per i repository Git. Puoi avere sia copie locali che remote dei tuoi repository, ciò rende più semplice la collaborazione. 

Problemi GitHub è uno strumento di traccia che ti permette di lavorare sui tuoi piani in un solo posto. È integrato con il tuo repository di sviluppo in modo che puoi focalizzarti sulle attività importanti.

Configura GitHub per gestire il tuo codice di origine nel cloud:

1. Se stai configurando questa integrazione dello strumento mentre stai creando la toolchain, segui questi passi:

 a. Nella sezione Configurable, fai clic su **GitHub**. Se stai creando la toolchain in {{site.data.keyword.Bluemix_notm}} pubblico e non hai autorizzato {{site.data.keyword.Bluemix_notm}} ad accedere a GitHub, fai clic su **Autorizza** per andare al sito web GitHub. Se non disponi di una sessione GitHub attiva, ti viene richiesto di accedere. Fai clic su **Authorize Application** per consentire a {{site.data.keyword.Bluemix_notm}} di accedere al tuo account GitHub. Se disponi di una sessione GitHub attiva ma non hai immesso la tua password recentemente, ti potrebbe essere richiesto di immettere la tua password GitHub per la conferma.
 
 b. Rivedi le ubicazioni del repository di destinazione predefinite per i repository GitHub. Questi repository vengono clonati dai repository di esempio. Se necessario, modifica i nomi dei repository di destinazione.
 ![Ubicazioni del repository di destinazione predefinite](images/toolchain_github_config.png)
   
1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, nella pagina **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **GitHub**.
1. Se disponi di un repository GitHub e desideri utilizzarlo, digita l'URL. Per il tipo di repository, fai clic su **Link**.
1. Se desideri utilizzare un nuovo repository GitHub, immetti un nome per il repository GitHub, l'URL per il repository che stai clonando o dividendo e seleziona il tipo di repository: 

 a. Per creare un repository vuoto, fai clic su **New**. 
 
 b. Per creare una copia di un repository GitHub, fai clic su **Clone**.
 
 c. Per dividere un repository GitHub in modo che puoi contribuire alle modifiche tramite l'inserimento di richieste, fai clic su **Fork**.
 
1. Se desideri utilizzare Problemi GitHub per la traccia del problema, seleziona la casella di spunta **Enable GitHub Issues**.
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per il repository GitHub con cui vuoi lavorare. Si apre il sito web GitHub, dove puoi visualizzare i contenuti del repository.
 
  **Suggerimento**: puoi utilizzare gli strumenti di gestione del codice di origine integrati in Eclipse Orion {{site.data.keyword.webide}} per modificare il repository GitHub e distribuire un'applicazione dal tuo spazio di lavoro.

1. Se hai abilitato Problemi GitHub, fai clic sul tile per i problemi GitHub per aprirlo.

Per ulteriori informazioni, consulta [GitHub (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} e [GitHub Issues (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configurazione di Dedicated GitHub Enterprise
{: #configghe}

{{site.data.keyword.ghe_long}} è un servizio host basato sul web, in loco per i repository Git. Dedicated GitHub Enterprise è solo per i clienti {{site.data.keyword.Bluemix_notm}} dedicato. GitHub Issues è uno strumento di traccia che ti permette di lavorare sui tuoi piani in un solo posto. È integrato con il tuo repository di sviluppo in modo che puoi focalizzarti sulle attività importanti. Per ulteriori informazioni su Dedicated GitHub Enterprise e i problemi GitHub, consulta [Using Dedicated GitHub Enterprise (il link si apre in una nuova finestra)](../services/ghededicated/index.html){: new_window} and [GitHub Issues (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Puoi configurare {{site.data.keyword.ghe_short}} come una integrazione dello strumento nella tua toolchain in modo da poter gestire il codice di origine nella tua istanza [{{site.data.keyword.Bluemix_notm}} dedicato aziendale (il link si apre in una nuova finestra)](../dedicated/index.html#dedicated){: new_window}.

1. Se stai configurando questa integrazione dello strumento mentre stai creando la toolchain, segui questi passi:

 a. Prima di accedere a Dedicated GitHub Enterprise per la prima volta, chiedi all'amministratore di regione della tua azienda di aggiungere il tuo ID utente alla tua istanza {{site.data.keyword.Bluemix_notm}} dedicato dal registro utenti della tua azienda utilizzando LDAP. Per informazioni sulla configurazione del tuo account {{site.data.keyword.ghe_short}}, consulta [Using Dedicated GitHub Enterprise (il link si apre in una nuova finestra)](../services/ghededicated/index.html){: new_window}.
 
 b. Nella sezione Configurable, fai clic su **{{site.data.keyword.ghe_short}}**.    
 
 c. Controlla il nome predefinito per il nuovo repository {{site.data.keyword.ghe_short}}. Se necessario, modifica il nome del nuovo repository. La seguente immagine mostra un esempio di un repository clonato da un repository di esempio. Puoi utilizzare un repository esistente o nuovo. Per utilizzare un nuovo repository, puoi creare un repository vuoto, o biforcarne uno. 
 ![Ubicazioni del repository predefinite](images/toolchain_ghe_config.png)
   
1. Se disponi di una toolchain in {{site.data.keyword.Bluemix_notm}} pubblico a cui stai aggiungendo questa integrazione dello strumento, nella pagina **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella tua pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. Se stai utilizzando una toolchain in {{site.data.keyword.Bluemix_notm}} dedicato, nel dashboard, fai clic sulla scheda **DEVOPS** e fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**.
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **{{site.data.keyword.ghe_short}}**.
1. Se disponi di un repository {{site.data.keyword.ghe_short}} e desideri utilizzarlo, digitane l'URL. Per il tipo di repository, fai clic su **Existing**.
1. Se desideri utilizzare un nuovo repository {{site.data.keyword.ghe_short}}, immetti un nome per il repository, l'URL per il repository che stai clonando o dividendo e seleziona il tipo di repository: 

 a. Per creare un repository vuoto, fai clic su **New**. 
 
 b. Per creare una copia di un repository, fai clic su **Clone**.
 
 c. Per dividere un repository in modo che puoi contribuire alle modifiche tramite l'inserimento di richieste, fai clic su **Fork**.
 
1. Per utilizzare GitHub Issues per la traccia del problema, seleziona la casella di spunta **Enable GitHub Issues**.
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per il repository {{site.data.keyword.ghe_short}} con cui vuoi lavorare. Si apre la tua istanza [{{site.data.keyword.Bluemix_notm}} dedicato aziendale (il link si apre in una nuova finestra)](../dedicated/index.html#dedicated){: new_window}, dove puoi visualizzare i contenuti del repository.
 
  **Suggerimento**: puoi utilizzare gli strumenti di gestione del codice di origine integrati in Eclipse Orion {{site.data.keyword.webide}} per modificare il repository {{site.data.keyword.ghe_short}} e distribuire un'applicazione dal tuo spazio di lavoro.

1. Se hai abilitato Problemi GitHub, fai clic sul tile per GitHub Issues.

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## Configurazione di uno strumento personalizzato (altro strumento)
{: #othertool}

Se il tuo team utilizza uno strumento che non è incluso nell'elenco di integrazioni delle toolchain, puoi integrare uno strumento personalizzato. 

Configura uno strumento personalizzato in modo che funzioni con gli altri strumenti della tua toolchain e sia disponibile per il tuo team:
1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Integrazioni configurabili, fai clic su **Altro strumento**.

1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, nella pagina **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**.
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazioni strumento, fai clic su **Altro strumento**.
1. Immetti il nome dello strumento.
1. Seleziona la fase del ciclo di vita strettamente associata allo strumento. La scelta della fase del ciclo di vita determina sotto quale categoria viene elencato lo strumento nella pagina Integrazioni toolchain.
1. Aggiungi un URL icona. L'icona verrà visualizzata nella scheda dell'integrazione strumento.
1. Aggiungi un URL documentazione.
1. Specifica un nome per l'istanza dello strumento. Ad esempio: My Team Tool.
1. Aggiungi un URL istanza dello strumento. Facendo clic sulla scheda di integrazione strumento, si accede all'URL elencato per l'istanza dello strumento.
1. Aggiungi una descrizione dello strumento.
1. (Avanzate) Aggiungi ulteriori proprietà come necessario. Ad esempio, elenca eventuali informazioni o attributi richiesti per integrare il tuo strumento con gli altri strumenti della toolchain.  
1. Fai clic su **Create Integration**.

## Configurazione di PagerDuty
{: #pagerduty}

PagerDuty integra i dati da più sistemi di monitoraggio in un singola vista. Quando si verifica un problema, PagerDuty si assicura che venga inviata una notifica al membro del team più adatto a risolverlo in quel momento. Se il membro del team non risponde al problema, possono essere configurate delle escalation per instradare il problema agli ingegneri secondari o ai gestori delle operazioni.

Configura PagerDuty per inviare notifiche quando si verifica un problema nella fase della pipeline in modo che puoi risolvere i problemi più velocemente e ridurre il tempo di inattività:

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Integrazioni configurabili, fai clic su **PagerDuty**.
1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, nella pagina **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **PagerDuty**
1. Digita il nome del sito PagerDuty associato con il tuo account PagerDuty. Se non disponi di un account PagerDuty, [registrane uno (il link si apre in una nuova finestra)](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Digita la chiave di accesso API per il tuo account PagerDuty. Per istruzioni su come trovare una chiave, consulta [API Authentication (il link si apre in una nuova finestra)](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Digita il nome del tuo servizio PagerDuty.
1. Digita l'indirizzo email per il contatto PagerDuty primario.
1. Digita il numero di telefono del contatto PagerDuty primario.
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per PagerDuty per andare alla pagina pagerduty.com. Puoi visualizzare gli eventi associati al servizio PagerDuty che hai specificato quando hai configurato questa integrazione dello strumento per la tua toolchain. 

Per ulteriori informazioni, consulta [PagerDuty (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configurazione di Sauce Labs
{: #saucelabs}

Sauce Labs esegue verifiche di unità funzionali. Quando una suite di verifica Sauce Labs è configurata come un lavoro di verifica nella {{site.data.keyword.deliverypipeline}}, la suite di test può eseguire verifiche sulla tua applicazione mobile o web come parte di un processo di distribuzione continua. Queste verifiche possono fornire un controllo prezioso del flusso per i tuoi progetti, che funzionano come gate per prevenire la distribuzione di codice errato.

Configura Sauce Labs per eseguire verifiche funzionali automatizzate su più sistemi operativi e browser in modo che puoi emulare la modalità di utilizzo di un sito o di un'applicazione di un utente.

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Integrazioni configurabili, fai clic su **Sauce Labs**.
1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, nella pagina **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Sauce Labs**.
1. Digita il nome utente associato con il tuo account Sauce Labs. Puoi [trovare il tuo nome utente nel messaggio di benvenuto all'inizio della tua pagina account Sauce Labs (il link si apre in una nuova finestra)](https://saucelabs.com/account){: new_window}.
1. Digita la chiave di accesso per il tuo account Sauce Labs. Puoi [trovare la chiave nella tua pagina account Sauce Labs (il link si apre in una nuova finestra)](https://saucelabs.com/account){: new_window}.
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per Sauce Labs per andare alla pagina saucelabs.com e visualizzare l'attività di verifica per la toolchain.

 **Suggerimento**: se hai aggiunto un lavoro di verifica Sauce Labs alla {{site.data.keyword.deliverypipeline}}, puoi selezionare l'istanza del servizio.

Per ulteriori informazioni, consulta [Sauce Labs (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configurazione di Slack
{: #slack}

**Importante**: le notifiche pubblicate nei canali Slack pubblici sono visibili a chiunque nel team. Ricorda che sei responsabile del contenuto che pubblichi.

Slack è un sistema di notifica e messaggistica in tempo reale basato sul cloud. Slack fornisce chat persistente, che è un'alternativa più interattiva alla email per la collaborazione del team. Puoi comunicare con il tuo team su un canale dedicato o su una serie di canali direttamente correlati al tuo lavoro. Puoi inoltre condividere file e immagini tramite i canali o con messaggi diretti tra due o più persone. Le comunicazioni nei messaggi diretti e sui canali vengono conservate in modo che puoi ricercarle. 

Configura Slack per ricevere notifiche sulla tua toolchain dalle integrazioni delle strumento, come ad esempio le attività di distribuzione e verifica:

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Integrazioni configurabili, fai clic su **Slack**.
1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, nella pagina **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**.
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Slack**.
1. Digita il token di autenticazione API per il tuo account Slack. Devi utilizzare un token di accesso completo generato per l'autenticazione con Slack. Per istruzioni su come trovare il token, consulta [Slack authentication (il link si apre in una nuova finestra)](https://api.slack.com/web#authentication){: new_window}.
1. Digita il nome del canale Slack a cui desideri vengano inviate le notifiche. Se il canale che hai specificato non esiste, viene creato. Se il canale è stato archiviato, viene riattivato.
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per Slack. Puoi visualizzare tutte le attività per la tua toolchain nel canale Slack configurato.

Per ulteriori informazioni, consulta [Slack (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.








