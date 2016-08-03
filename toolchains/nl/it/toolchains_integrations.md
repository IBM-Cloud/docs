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

*Ultimo aggiornamento: 17 giugno 2016*
{: .last-updated}

Puoi configurare le integrazioni dello strumento che supportano le attività di operazioni, sviluppo e distribuzione mentre crei una toolchain o puoi aggiungere e configurare le integrazioni dello strumento per personalizzare una toolchain esistente.  
{:shortdesc}

**Importante**: questa funzionalità è sperimentale. Le toolchain potrebbero non essere stabili e potrebbero venire modificate in modi che le rendono non compatibili con le versioni precedenti. Non sono raccomandate per l'utilizzo in ambienti di produzione. Per utilizzare le toolchain, devi effettuare una [richiesta di accesso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} monouso. Le toolchain sono disponibili solo nella regione degli Stati Uniti Sud.

**Suggerimento**: se desideri avviare lo sviluppo con il codice di origine, assicurati di aver configurato le integrazioni dello strumento Problemi GitHub e GitHub prima di configurare la {{site.data.keyword.deliverypipeline}}.

## Configurazione della delivery pipeline
{: #deliverypipeline}

La {{site.data.keyword.deliverypipeline}} automatizza la distribuzione continua dei tuoi progetti tramite una sequenza di fasi che richiamano i lavori di input ed esecuzione, come le creazioni, le verifiche e le distribuzioni. 

Configura la {{site.data.keyword.deliverypipeline}} per automatizzare la distribuzione, la verifica e la creazione continua delle tue applicazioni: 

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Configurable Integrations, fai clic su **Delivery Pipeline**. A seconda del template che utilizzi, possono essere disponibili diversi campi. Rivedi i valori di campo predefiniti e se necessario, modifica queste impostazioni.
1. Se disponi di una toolchain e stai aggiungendo questa integrazione dello strumento ad essa, nel dashboard DevOps, nella scheda **Toolchain**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Delivery Pipeline**.
1. Specifica un nome per la tua nuova pipeline.
1. Se stai pianificando di utilizzare la tua pipeline per distribuire un'interfaccia utente, seleziona la casella di spunta **Viewable App**. Tutte le applicazioni create dalla tua pipeline vengono visualizzate nell'elenco **VIEW APP** nella pagina Integrazioni dello strumento della toolchain.
1. Fai clic su **Create Integration** per aggiungere la {{site.data.keyword.deliverypipeline}} alla tua toolchain.
1. Fai clic sul tile per la {{site.data.keyword.deliverypipeline}} per visualizzare la pipeline e configurarla. Per informazioni sulla configurazione di una pipeline, consulta [Building and deploying pipelines](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Suggerimento**: se desideri attivare la pipeline quando esegui il push delle modifiche al tuo repository (repo) GitHub, devi configurare GitHub per la tua toolchain prima di definire le fasi per la tua pipeline. Le fasi della pipeline necessitano di URL Git per i tuoi repository GitHub. Ogni fase della pipeline può far riferimento solo a uno dei repository GitHub associato con la tua toolchain. Per istruzioni su come configurare GitHub, consulta la sezione [Problemi GitHub e GitHub](#github).
  
1. Facoltativo: se desideri che Sauce Labs esegua delle verifiche sulla tua applicazione, configura la {{site.data.keyword.deliverypipeline}} per aggiungere un lavoro di verifica Sauce Labs. Per istruzioni sulla configurazione del lavoro di verifica, consulta la sezione [Configurazione di un lavoro di verifica Sauce Labs nella tua pipeline](#config_saucelabs).

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
  
1. Configura il lavoro di distribuzione. Nel campo **Deploy Script**, includi questo comando: export CF_APP_NAME="$CF_APP". Questo comando esporta il nome dell'applicazione come una proprietà di ambiente.
1. Configura il lavoro di verifica. I valori nella seguente immagine sono degli esempi. I campi **Istanza del servizio**, **Destinazione**, **Organizzazione** e **Spazio** vengono popolati con il nome utente, la regione, l'organizzazione e lo spazio Sauce Labs che stai correntemente utilizzando.
![Configura lavoro](images/toolchain_configure_job.png)

  a. Per il tipo di verifica, seleziona **Sauce Labs**.
  
  b. Per il servizio dell'istanza, seleziona il nome utente Sauce Labs che hai utilizzato nella configurazione di Sauce Labs per la tua toolchain. 
  
   **Suggerimento**: per visualizzare il nome utente e la chiave di accesso che hai utilizzato nella configurazione di Sauce Labs per la tua toolchain, fai clic su **Configura**. 
  
  c. Nel campo **Test Execution Command**, immetti i comandi per installare le dipendenze necessarie per le tue verifiche e quindi eseguile. Ad esempio, per un'applicazione Node.js ipotetica, devi immettere:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Se desideri visualizzare i report di verifica nei log del lavoro di verifica, seleziona la casella di spunta **Enable Test Report** e imposta il pattern del file dei risultati della verifica su `test/*.xml`.
  
1. Fai clic su **SALVA**. Ora, se la tua pipeline è in esecuzione, puoi eseguire le tue verifiche Sauce Labs.

Per ulteriori informazioni, consulta [Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.

## Aggiunta di Deployment Risk Analytics
{: #dra}

{{site.data.keyword.DRA_full}} raccoglie e analizza i risultati dalle verifiche di unità, dalle verifiche funzionali e dagli strumenti di copertura del codice per determinare se il tuo codice soddisfa i criteri predefiniti nei gate specificati nel tuo processo di distribuzione. Se il tuo codice non soddisfa o supera i criteri, la distribuzione viene arrestata per prevenire che vengano rilasciati dei rischi. Puoi utilizzare Deployment Risk Analytics come una rete di sicurezza per il tuo ambiente di distribuzione continua o come modo per implementare e migliorare gli standard di qualità. 

 **Suggerimento**: questa integrazione dello strumento è preconfigurata. Non richiede alcun parametro di configurazione e non puoi riconfigurarla.
 
Aggiungi Deployment Risk Analytics per mantenere e migliorare la qualità del tuo codice Bluemix monitorando le tue distribuzioni per identificare i rischi prima che vangano rilasciati:

1. Se disponi di una toolchain e stai aggiungendo questa integrazione dello strumento ad essa, nel dashboard DevOps, nella scheda **Toolchain**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Deployment Risk Analytics**. 
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per Deployment Risk Analytics e quindi completa i primi passi: creazione dei criteri, connessione dei criteri alla pipeline ed esecuzione della pipeline. Per ulteriori informazioni, consulta [Deployment Risk Analytics](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.

## Aggiunta di Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} è un ambiente basato sul web integrato dove puoi creare, modificare, eseguire il debug e completare le attività di controllo dell'origine. Puoi spostare senza interruzioni dalla modifica per l'esecuzione, l'invio e la distribuzione. 

 **Suggerimento**: questa integrazione dello strumento è preconfigurata. Non richiede alcun parametro di configurazione e non puoi riconfigurarla.
 
Aggiungi l'integrazione dello strumento Eclipse Orion {{site.data.keyword.webide}} per completare le attività di controllo dell'origine:

1. Se disponi di una toolchain e stai aggiungendo questa integrazione dello strumento ad essa, nel dashboard DevOps, nella scheda **Toolchain**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Eclipse Orion Web IDE**. 
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per la nuova IDE web Eclipse Orion. Il tuo spazio di lavoro viene prepopolato con i repository GitHub. I repository associati con la tua toolchain corrente sono evidenziati.

Per ulteriori informazioni, consulta [Web IDE](https://www.ibm.com/devops/method/content/code/tool_web_ide/){: new_window}.


## Configurazione dei problemi GitHub e GitHub
{: #github}

GitHub è un servizio host basato sul web per i repository Git. Puoi avere sia copie locali che remote dei tuoi repository, ciò rende più semplice la collaborazione. 

Problemi GitHub è uno strumento di traccia che ti permette di lavorare sui tuoi piani in un solo posto. È integrato con il tuo repository di sviluppo in modo che puoi focalizzarti sulle attività importanti.

Configura Problemi GitHub e GitHub per gestire il tuo codice di origine nel cloud:

1. Se stai configurando questa integrazione dello strumento mentre stai creando la toolchain, segui questi passi:

 a. Nella sezione Configurable, fai clic su **GitHub**. Se non hai autorizzato {{site.data.keyword.Bluemix}} ad accedere a GitHub, fai clic su **Authorize** per andare al sito web GitHub. Se non disponi di una sessione GitHub attiva, ti viene richiesto di accedere. Fai clic su **Authorize Application** per consentire a {{site.data.keyword.Bluemix}} di accedere al tuo account GitHub. Se disponi di una sessione GitHub attiva ma non hai immesso la tua password recentemente, ti potrebbe essere richiesto di immettere la tua password GitHub per la conferma.
 
 b. Rivedi le ubicazioni del repository di destinazione predefinite per i repository GitHub. Questi repository vengono clonati dai repository di esempio. Se necessario, modifica i nomi dei repository di destinazione.
 ![Ubicazioni del repository di destinazione predefinite](images/toolchain_github_config.png)
   
1. Se disponi di una toolchain e stai aggiungendo questa integrazione dello strumento ad essa, nel dashboard DevOps, nella scheda **Toolchain**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **GitHub**.
1. Se disponi di un repository GitHub e desideri utilizzarlo, digita l'URL. Per il tipo di repository, fai clic su **Link**.
1. Se desideri utilizzare un nuovo repository GitHub, immetti un nome per il repository GitHub, l'URL per il repository che stai clonando o dividendo e seleziona il tipo di repository: 

 a. Per creare un repository vuoto, seleziona **New**. 
 
 b. Per creare una copia di un repository GitHub, seleziona **Clone**.
 
 c. Per dividere un repository GitHub in modo che puoi contribuire alle modifiche tramite l'inserimento di richieste, seleziona **Fork**.
 
1. Se desideri utilizzare Problemi GitHub per la traccia del problema, seleziona la casella di spunta **Enable GitHub Issues**.
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per il repository GitHub con cui vuoi lavorare per andare al sito github.com e visualizzare i contenuti del repository.
 
  **Suggerimento**: puoi utilizzare gli strumenti di gestione del codice di origine integrati nella IDE web Eclipse Orion per modificare il repository GitHub e distribuire un'applicazione dal tuo spazio di lavoro.

1. Se hai abilitato Problemi GitHub, fai clic sul tile per Problemi GitHub per visualizzarlo.

Per ulteriori informazioni, consulta [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} e [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.    

##Utilizzo di {{site.data.keyword.ghe_short}} dedicato
{: #ghe}

{{site.data.keyword.ghe_long}} è la versione interamente gestita e ospitata sul cloud di IBM di {{site.data.keyword.ghe_short}}, disponibile per gli ambienti Bluemix dedicati. GitHub fornisce l'esperienza di scrittura di codice sociale che amano gli sviluppatori. [{{site.data.keyword.Bluemix_notm}} dedicato](../dedicated/index.html#dedicated){: new_window} fornisce un ambiente di elaborazione cloud su hardware isolato fisico integrato nella tua rete.

{{site.data.keyword.ghe_short}} dedicato è solo per i clienti {{site.data.keyword.Bluemix_notm}} dedicato.

### Configurazione del tuo account 

{{site.data.keyword.ghe_short}} include SSO (single sign-on) con {{site.data.keyword.Bluemix_notm}} dedicato. Per accedere a {{site.data.keyword.ghe_short}}, incolla l'URL dal tuo amministratore di regione o dalla email di benvenuto nel browser. Il tuo URL segue questo pattern: `github.your-company-dedicated-name.bluemix.net`. Accedi con il tuo ID utente e password {{site.data.keyword.Bluemix_notm}} dedicato e il tuo account {{site.data.keyword.ghe_short}} viene creato automaticamente.

**Nota:** se visualizzi un messaggio di stato per cui il tuo ID utente non esiste, chiedi al tuo amministratore di regione di aggiungere il tuo ID utente al registro utenti {{site.data.keyword.Bluemix_notm}} dedicato. Se tu sei l'amministratore di regione, consulta [Managing {{site.data.keyword.Bluemix_notm}} Dedicated users and permissions](https://new-console.stage1.ng.bluemix.net/docs/admin/index.html#oc_useradmin){: new_window}.

In molti casi, il tuo nome utente GitHub è il tuo nome breve dell'email, a meno che il tuo nome breve non includa caratteri che GitHub non supporta, come ad esempio i punti. Se il tuo nome breve include caratteri che GitHub non supporta, tali caratteri saranno sostituiti da trattini.     

### Aggiunta di un indirizzo email al tuo account.

Devi aggiungere il tuo indirizzo email alle tue impostazioni dell'account {{site.data.keyword.ghe_short}} per ricevere le notifiche. Dopo che hai aggiunto il tuo indirizzo email, puoi usufruire dei vantaggi delle funzioni di scrittura di codice sociale di {{site.data.keyword.ghe_short}}.    
 
Per aggiungere il tuo indirizzo email al tuo account {{site.data.keyword.ghe_short}} dedicato, completa la seguente procedura:    
1. Nell'angolo in alto a destra di una qualsiasi pagina GitHub, fai clic sulla tua icona profilo e quindi fai clic su **Settings**.    
2. Nella barra laterale, fai clic su **Emails**.    
3. Aggiungi il tuo indirizzo email e fai clic su **Add**.     

{: #ghe_auth}
### Creazione di una chiave SSH o di un token di accesso personale per l'autenticazione

Per eseguire operazioni Git remote come `clone` o `push` dal tuo repository Git locale, devi utilizzare una chiave SSH o un token di accesso personale per l'autenticazione con {{site.data.keyword.ghe_short}}. L'autenticazione tramite HTTPS è supportata utilizzando soltanto un token di accesso; non puoi utilizzare l'ID utente e la password per clonare o eseguire il push da un repository locale. Anche le richieste API richiedono un token di accesso personale.

**Nota:** per utilizzare una chiave SSH o di un token di accesso personale per l'autenticazione, devi configurare Git localmente. Per le istruzioni, consulta [Setting up Git](https://help.github.com/enterprise/2.6/user/articles/set-up-git/){: new_window}.    

Per creare un token di accesso personale, completa la seguente procedura:    
   1. Nell'angolo in alto a destra di una qualsiasi pagina GitHub, fai clic sulla tua icona profilo e quindi fai clic su **Settings**.    
   2. Nella barra laterale, fai clic su **Personal access tokens**.   
   3. Fai clic su **Generate new token**.
   4. Aggiungi una descrizione del token e fai clic su **Generate token**.
   5. Copia il token in un'ubicazione sicura e nell'applicazione di gestione delle password.
     **Nota:** per motivi di sicurezza, dopo che hai lasciato la pagina, non puoi visualizzare il token nuovamente.    

Utilizza il tuo token di accesso personale invece della password per l'accesso alla riga di comando su HTTPS. 


Per crea una chiave SSH, completa la seguente procedura:
   1. Apri Git Bash (Windows) o una nuova finestra terminale (Linux e Mac).    
   2. Incolla il seguente testo, sostituendo l'indirizzo email che hai aggiunto al tuo account {{site.data.keyword.ghe_short}}:
   
     ``
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     # Crea una nuova chiave SSH, utilizzando l'email fornita come un'etichetta
     Generazione della coppia di chiavi rsa pubblica/privata.
     ``

   3. Quando ti viene richiesto di specificare un file in cui salvare la chiave, premi Invio per accettare l'ubicazione predefinita.
   4. Quando richiesto, immettere una passphrase di sicurezza. Per ulteriori informazioni, consulta [Working with SSH key passphrases](https://help.github.com/enterprise/2.6/user/articles/working-with-ssh-key-passphrases/){: new_window}.   

Aggiungi la tua chiave SSH all'agent SSH:    
   1. Assicurati che l'agent SSH sia abilitato. Utilizzando Git Bash, immetti questo comando per abilitare l'agent SSH:
      ``
      # start the ssh-agent in the background
      $ eval "$(ssh-agent -s)"
      Agent pid 59566
      ``    
  
   2. Aggiungi la tua chiave SSH all'agent SSH immettendo questo comando:
      ``
      $ ssh-add ~/.ssh/id_rsa
      ``    
   3. Aggiungi la chiave SSH al tuo account GitHub. Per ulteriori informazioni, consulta [Adding a new SSH key to your GitHub account](https://help.github.com/enterprise/2.6/user/articles/adding-a-new-ssh-key-to-your-github-account/){: new_window}.    
   

### Configurazione delle organizzazioni, dei team e dei repository GitHub    

La configurazione delle organizzazioni GitHub è utile perché crei gruppi di utenti distinti che lavorano su progetti o attività simili. L'organizzazione dei team all'interno di un'organizzazione ha il beneficio di controllare l'accesso ai repository. Per ulteriori informazioni, consulta [Organizations and teams](https://help.github.com/enterprise/2.6/admin/guides/user-management/organizations-and-teams/){: new_window}.

**Nota:** le organizzazioni GitHub non sono le stesse delle organizzazioni Bluemix.

Configura il tuo progetto del team completando queste attività:

   1. [Create an organization (org)](https://help.github.com/enterprise/2.6/user/articles/creating-a-new-organization-account/){: new_window}.
   2. [Create a repo for your org](https://help.github.com/enterprise/2.6/user/articles/create-a-repo/){: new_window}.
   3. [Invite users to join your org](https://help.github.com/enterprise/2.6/user/articles/inviting-users-to-join-your-organization/){: new_window}.
   4. [Carefully select at least one team member to have owner permissions in your org](https://help.github.com/enterprise/2.6/user/articles/changing-a-person-s-role-to-owner/){: new_window}.    
   
  **Nota:** prima di invitare utenti nella tua organizzazione, devono accedere a {{site.data.keyword.ghe_short}} almeno una volta o i loro account {{site.data.keyword.ghe_short}} non saranno disponibili per l'invito.
   
### Richiesta di assistenza tecnica
Per ottenere delle risposte ora, invia le domande a [Stack Overflow](http://stackoverflow.com/questions/ask?tags=ibm-bluemix_github-enterprise){: new_window}. 

Per ulteriore supporto, utilizza queste risorse:    
   1. Completa il modulo all'indirizzo https://ibm.biz/bluemixsupport.   
   2. Invia un nuovo ticket tramite il Client Success Portal all'indirizzo https://support.ibmcloud.com/ics/support/mylogin.asp?login=bluemix.    


## Configurazione di PagerDuty
{: #pagerduty}

PagerDuty integra i dati da più sistemi di monitoraggio in un singola vista. Quando si verifica un problema, PagerDuty si assicura che venga inviata una notifica al membro del team più adatto a risolverlo in quel momento. Se il membro del team non risponde al problema, possono essere configurate delle escalation per instradare il problema agli ingegneri secondari o ai gestori delle operazioni.

Configura PagerDuty per inviare notifiche quando si verifica un problema nella fase della pipeline in modo che puoi risolvere i problemi più velocemente e ridurre il tempo di inattività:

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Configurable Integrations, fai clic su **PagerDuty**.
1. Se disponi di una toolchain e stai aggiungendo questa integrazione dello strumento ad essa, nel dashboard DevOps, nella scheda **Toolchain**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **PagerDuty**
1. Digita il nome del sito PagerDuty associato con il tuo account PagerDuty. Se non disponi di un account PagerDuty, [registrane uno](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Digita la chiave di accesso API per il tuo account PagerDuty. Per istruzioni su come trovare la chiave, consulta [API Authentication](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Digita il nome del tuo servizio PagerDuty.
1. Digita l'indirizzo email per il contatto PagerDuty primario.
1. Digita il numero di telefono del contatto PagerDuty primario.
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per PagerDuty per andare alla pagina pagerduty.com. Puoi visualizzare gli eventi associati al servizio PagerDuty che hai specificato quando hai configurato questa integrazione dello strumento per la tua toolchain. 

Per ulteriori informazioni, consulta [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configurazione di Sauce Labs
{: #saucelabs}

Sauce Labs esegue verifiche di unità funzionali. Quando una suite di verifica Sauce Labs è configurata come un lavoro di verifica nella {{site.data.keyword.deliverypipeline}}, la suite di test può eseguire verifiche sulla tua applicazione mobile o web come parte di un processo di distribuzione continua. Queste verifiche possono fornire un controllo prezioso del flusso per i tuoi progetti, che funzionano come gate per prevenire la distribuzione di codice errato.

Configura Sauce Labs per eseguire verifiche funzionali automatizzate su più sistemi operativi e browser in modo che puoi emulare la modalità di utilizzo di un sito o di un'applicazione di un utente.

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Configurable Integrations, fai clic su **Sauce Labs**.
1. Se disponi di una toolchain e stai aggiungendo questa integrazione dello strumento ad essa, nel dashboard DevOps, nella scheda **Toolchain**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain**. Quindi, fai clic su **Integrazioni dello strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Sauce Labs**.
1. Digita il nome utente associato con il tuo account Sauce Labs. Puoi [trovare il tuo nome utente nel messaggio di benvenuto all'inizio della tua pagina account Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Digita la chiave di accesso per il tuo account Sauce Labs. Puoi [trovare la chiave nell'angolo in basso a sinistra della tua pagina account Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per Sauce Labs per andare alla pagina saucelabs.com e visualizzare l'attività di verifica per la toolchain.

 **Suggerimento**: se hai aggiunto un lavoro di verifica Sauce Labs alla {{site.data.keyword.deliverypipeline}}, puoi selezionare l'istanza del servizio.

Per ulteriori informazioni, consulta [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configurazione di Slack
{: #slack}

**Importante**: le notifiche pubblicate nei canali Slack pubblici sono visibili a chiunque nel team. Ricorda che sei responsabile del contenuto che pubblichi.

Slack è un sistema di notifica e messaggistica in tempo reale basato sul cloud. Slack fornisce chat persistente, che è un'alternativa più interattiva alla email per la collaborazione del team. Puoi comunicare con il tuo team su un canale dedicato o su una serie di canali direttamente correlati al tuo lavoro. Puoi inoltre condividere file e immagini tramite i canali o con messaggi diretti tra due o più persone. Le comunicazioni nei messaggi diretti e sui canali vengono conservate in modo che puoi ricercarle. 

Configura Slack per ricevere notifiche sulla tua toolchain dalle integrazioni delle strumento, come ad esempio le attività di distribuzione e verifica:

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Configurable Integrations, fai clic su **Slack**.
1. Se disponi di una toolchain e stai aggiungendo questa integrazione dello strumento ad essa, nel dashboard DevOps, nella scheda **Toolchain**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain**. Quindi, fai clic su **Integrazioni dello strumento**.
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazione toolchain, fai clic su **Slack**.
1. Digita il token di autenticazione API per il tuo account Slack. Devi utilizzare un token di accesso completo generato per l'autenticazione con Slack. Per istruzioni su come trovare il token, consulta [Slack authentication](https://api.slack.com/web#authentication){: new_window}.
1. Digita il nome del canale Slack a cui desideri vengano inviate le notifiche. Se il canale che hai specificato non esiste, viene creato. Se il canale è stato archiviato, viene riattivato.
1. Fai clic su **Create Integration**.
1. Fai clic sul tile per Slack. Puoi visualizzare tutte le attività per la tua toolchain nel canale Slack configurato.

Per ulteriori informazioni, consulta [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
