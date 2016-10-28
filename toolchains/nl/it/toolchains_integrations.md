---

copyright:
  anni: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurazione di integrazioni dello strumento
{: #integrations}

Ultimo aggiornamento: 13 settembre 2016
{: .last-updated}

Puoi configurare le integrazioni dello strumento che supportano attività di sviluppo, distribuzione e operative quando crei una toolchain oppure puoi aggiungere e configurare le integrazioni per personalizzare una toolchain esistente.  
{:shortdesc}

**Importante**: questa funzionalità è sperimentale. Le toolchain potrebbero non essere stabili e potrebbero essere modificate secondo modalità non compatibili con le versioni precedenti. Non se ne consiglia l'utilizzo negli ambienti di produzione. In {{site.data.keyword.Bluemix_notm}} pubblico, le toolchain sono disponibili solo nella regione Stati Uniti Sud.

Le integrazioni dello strumento disponibili che puoi aggiungere e configurare per la tua toolchain variano a seconda che tu stia utilizzando la toolchain in {{site.data.keyword.Bluemix_notm}} pubblico o {{site.data.keyword.Bluemix_notm}} dedicato.

*Tabella 1. Integrazioni dello strumento disponibili per le toolchain in {{site.data.keyword.Bluemix_notm}} pubblico e dedicato*

|Integrazione dello strumento |Disponibile in {{site.data.keyword.Bluemix_notm}} pubblico	|Disponibile in {{site.data.keyword.Bluemix_notm}} dedicato|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|Sì	   	|Sì  		|
|{{site.data.keyword.DRA_short}} 		|Sì		|No			|
|Eclipse Orion {{site.data.keyword.webide}}		|Sì		|Sì			|
|GitHub		|Sì		|No		|
|Dedicated GitHub Enterprise			|No		|Sì		|
|PagerDuty			|Sì		|No		|
|Sauce Labs		|Sì		|No		|
|Slack			|Sì		|No		|

**Suggerimento**: se vuoi iniziare a sviluppare con il tuo codice sorgente in {{site.data.keyword.Bluemix_notm}} pubblico, configura l'integrazione dello strumento GitHub prima di configurare la {{site.data.keyword.deliverypipeline}}. Se vuoi iniziare a sviluppare con il tuo codice in {{site.data.keyword.Bluemix_notm}} dedicato, configura l'integrazione dello strumento {{site.data.keyword.ghe_short}} prima di configurare la {{site.data.keyword.deliverypipeline}}. 


## Configurazione della pipeline di fornitura
{: #deliverypipeline}

La {{site.data.keyword.deliverypipeline}} automatizza la distribuzione continua dei tuoi progetti attraverso le sequenze di fasi che richiamano i lavori di immissione e di esecuzione, come creazioni, test e distribuzioni.  

Configura la {{site.data.keyword.deliverypipeline}} per automatizzare i processi continui di creazione, test e distribuzione delle tue applicazioni: 

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Integrazioni configurabili, fai clic su **Delivery Pipeline**. A seconda del template utilizzato, potrebbero essere disponibili campi diversi. Controlla i valori di campo predefiniti e, se necessario, modifica tali impostazioni. 
1. Se disponi di una toolchain in {{site.data.keyword.Bluemix_notm}} pubblico e stai aggiungendo questa integrazione dello strumento, nel dashboard DevOps, sulla scheda **Toolchain**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica della tua applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**. Se stai utilizzando una toolchain in {{site.data.keyword.Bluemix_notm}} dedicato, nel Dashboard, sulla scheda **DEVOPS**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nell'angolo superiore destro della pagina Panoramica dell'applicazione, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazioni strumento, fai clic su **Delivery Pipeline**.
1. Specifica un nome per la tua nuova pipeline.
1. Se hai intenzione di utilizzare la tua pipeline per distribuire un'interfaccia utente, seleziona la casella di spunta **Applicazione visualizzabile**. Tutte le applicazioni create dalla tua pipeline vengono mostrate nell'elenco **VISUALIZZA APPLICAZIONE** nella pagina Integrazioni strumento della toolchain.
1. Fai clic su **Crea integrazione** per aggiungere la {{site.data.keyword.deliverypipeline}} alla tua toolchain.
1. Fai clic sul tile di {{site.data.keyword.deliverypipeline}} per visualizzare la pipeline e configurarla. Per apprendere le procedure fondamentali per la configurazione di una pipeline, vedi [Building and deploying pipelines](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Suggerimento**: se vuoi attivare la pipeline quando esegui il push delle modifiche al tuo repository GitHub o {{site.data.keyword.ghe_short}}, devi configurare GitHub o {{site.data.keyword.ghe_short}} per la tua toolchain prima di definire le fasi per la pipeline. Le fasi della pipeline richiedono gli URL Git dei tuoi repository. Ogni fase della pipeline può fare riferimento a solo uno dei repository GitHub o {{site.data.keyword.ghe_short}} che viene associato alla tua toolchain. Per istruzioni sulla configurazione di GitHub, vedi la sezione [GitHub](#github). Per le istruzioni sulla configurazione di Dedicated GitHub Enterprise, vedi [Introduzione a {{site.data.keyword.ghe_long}}](../services/ghededicated/index.html){: new_window}.
  
1. Facoltativo: se stai utilizzando una toolchain in {{site.data.keyword.Bluemix_notm}} pubblico e vuoi che Sauce Labs esegua i test sulla tua applicazione, configura {{site.data.keyword.deliverypipeline}} per aggiungere un lavoro di test Sauce Labs. Per istruzioni su come configurare il lavoro di test, vedi la sezione [Configurazione di un lavoro di test Sauce Labs nella tua pipeline](#config_saucelabs).

### Configurazione di un lavoro di test Sauce Labs nella tua pipeline
{: #config_saucelabs}

Prima di configurare un lavoro di test Sauce Labs nella tua pipeline, hai bisogno di una pipeline di lavoro che includa le fasi per creare e distribuire la tua applicazione e devi configurare Sauce Labs per la tua toolchain. Per istruzioni sulla configurazione di Sauce Labs, vedi la sezione [Sauce Labs](#saucelabs).

Configura la {{site.data.keyword.deliverypipeline}} per aggiungere un lavoro di test Sauce Labs:

1. Se non disponi di una fase per la distribuzione di una versione di test della tua applicazione, creane una.
1. Nella fase, aggiungi un lavoro di test dopo il lavoro di distribuzione. Inserendo questi lavori nella stessa fase, essi possono accedere alla stessa serie di proprietà di ambiente.
  ![Lavoro di test](images/toolchain_test_job.png) 

1. Configura la fase: 

  a. Nella scheda **PROPRIETÀ AMBIENTE**, crea tre proprietà: CF_APP_NAME, SAUCE_USERNAME e SAUCE_ACCESS_KEY.
  
  b. Immetti il tuo nome utente Sauce Labs e la chiave di accesso. In questo modo, esternalizzi questi valori in modo da poterli utilizzare nei tuoi test. 
  
1. Configura il lavoro di distribuzione. Nel campo **Script di distribuzione**, includi il seguente comando: `export CF_APP_NAME="$CF_APP"`. Questo comando esporta il nome applicazione come una proprietà di ambiente.
1. Configura il lavoro di test. I valori riportati nella seguente immagine sono degli esempi. I campi **Istanza del servizio**, **Destinazione**, **Organizzazione** e **Spazio** vengono compilati con il nome utente Sauce Labs, la regione, l'organizzazione e lo spazio che stai utilizzando.
![Configura lavoro](images/toolchain_configure_job.png)

  a. Per il tipo di tester, seleziona **Sauce Labs**.
  
  b. Per l'istanza del servizio, seleziona il nome utente Sauce Labs che hai utilizzato per la configurazione di Sauce Labs per la tua toolchain. 
  
   **Suggerimento**: per visualizzare il nome utente e la chiave di accesso utilizzati durante la configurazione di Sauce Labs per la tua toolchain, fai clic su **Configura**. 
  
  c. Nel campo **Comando di esecuzione test**, immetti i comandi che installano le dipendenze richieste dai tuoi test ed esegui quindi i test. Ad esempio, per un'applicazione Node.js, puoi immettere i seguenti comandi:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Se vuoi visualizzare i report del test nei log del lavoro di test, seleziona la casella di spunta **Abilita report di test** e imposta il modello di file dei risultati del test su `test/*.xml`.
  
1. Fai clic su **SALVA**. Ogni volta che la tua pipeline viene eseguita, vengono eseguiti i test Sauce Labs.

Per ulteriori informazioni, vedi [Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.


## Aggiunta di {{site.data.keyword.DRA_short}}
{: #dra}

{{site.data.keyword.DRA_full}} raccoglie e analizza i risultati di unit test, test funzionali e strumenti di code coverage per determinare se il tuo codice soddisfa i criteri predefiniti nelle porte specificate nel tuo processo di distribuzione. Se il codice non soddisfa o supera i criteri indicati, la distribuzione viene interrotta per evitare l'insorgere di rischi. Puoi utilizzare {{site.data.keyword.DRA_short}} come rete di sicurezza per il tuo ambiente di fornitura continua o come metodo per implementare e migliorare gli standard di qualità.  

 **Nota**: questa integrazione dello strumento è preconfigurata. Non richiede alcun parametro di configurazione e non puoi riconfigurarla. 
 
Aggiungi {{site.data.keyword.DRA_short}} per mantenere e migliorare la qualità del tuo codice in {{site.data.keyword.Bluemix_notm}} mediante il monitoraggio delle tue distribuzioni per identificare i rischi prima che insorgano.

1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, sulla scheda **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazioni strumento, fai clic su **Analisi dei rischi di distribuzione**. 
1. Fai clic su **Crea integrazione**.
1. Fai clic sul tile di {{site.data.keyword.DRA_short}} e completa i passi preliminari: creazione dei criteri, collegamento dei criteri alla pipeline ed esecuzione della pipeline. Per ulteriori informazioni, vedi [{{site.data.keyword.DRA_short}}](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.


## Aggiunta di Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} è un ambiente basato sul Web integrato in cui puoi creare, modificare, eseguire, sottoporre a debug e completare le attività di controllo del codice sorgente. Puoi passare tranquillamente dalla modifica all'esecuzione, dall'invio alla distribuzione. 

 **Nota**: questa integrazione dello strumento è preconfigurata. Non richiede alcun parametro di configurazione e non puoi riconfigurarla. 
 
Per completare le attività di controllo del codice sorgente, aggiungi l'integrazione dello strumento Eclipse Orion {{site.data.keyword.webide}}.

1. Se disponi di una toolchain in {{site.data.keyword.Bluemix_notm}} pubblico e stai aggiungendo questa integrazione dello strumento, nel dashboard DevOps, sulla scheda **Toolchain**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**. Se stai utilizzando una toolchain in {{site.data.keyword.Bluemix_notm}} dedicato, nel Dashboard, sulla scheda **DEVOPS**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nell'angolo superiore destro della pagina Panoramica dell'applicazione, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**.
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazioni strumento, fai clic su **Eclipse Orion Web IDE**. 
1. Fai clic su **Crea integrazione**.
1. Fai clic sul tile del nuovo Eclipse Orion {{site.data.keyword.webide}}. Il tuo spazio di lavoro viene precompilato con i repository GitHub o {{site.data.keyword.ghe_short}}. I repository associati alla tua toolchain corrente vengono evidenziati.

Per ulteriori informazioni, vedi [Modifica del codice con Eclipse Orion {{site.data.keyword.webide}}](../toolchains/web_ide.html){: new_window}.


## Configurazione di GitHub
{: #github}

GitHub è un servizio di hosting basato su Web per i repository Git. Puoi disporre di copie locali e remote dei tuoi repository, il che rende più semplice la collaborazione. 

GitHub Issues è uno strumento di traccia che mantiene tutto il tuo lavoro e i tuoi progetti in un unico posto. Viene integrato nel tuo repository di sviluppo in modo che tu possa concentrarti sulle attività importanti.

Configura GitHub per gestire il tuo codice sorgente nel cloud:

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, completa la seguente procedura:

 a. Nella sezione Integrazioni configurabili, fai clic su **GitHub**. Se non hai autorizzato {{site.data.keyword.Bluemix_notm}} ad accedere a GitHub, fai clic su **Autorizza** per accedere al sito Web GitHub. Se non hai una sessione GitHub attiva, ti viene richiesto di effettuare l'accesso. Fai clic su **Autorizza applicazione** per consentire a {{site.data.keyword.Bluemix_notm}} di accedere al tuo account GitHub. Se hai una sessione GitHub attiva ma non hai immesso la tua password di recente, è possibile che ti venga richiesto di confermare la tua password GitHub.
 
 b. Controlla i percorsi dei repository di destinazione predefiniti per i repository GitHub. Questi repository vengono clonati da quelli di esempio. Se necessario, modifica i nomi dei repository di destinazione.
 ![Percorsi dei repository di destinazione predefiniti](images/toolchain_github_config.png)
   
1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, sulla scheda **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazioni strumento, fai clic su **GitHub**.
1. Se disponi di un repository GitHub che vuoi utilizzare, immetti l'URL. Per il tipo di repository, fai clic su **Link**.
1. Se vuoi utilizzare un nuovo repository GitHub, immetti un nome per il repository GitHub, immetti l'URL del repository da clonare o biforcare e seleziona il tipo di repository: 

 a. Per creare un repository vuoto, fai clic su **Nuovo**. 
 
 b. Per creare una copia di un repository GitHub, fai clic su **Clona**.
 
 c. Per biforcare un repository GitHub in modo che sia possibile fornire le modifiche attraverso le richieste di importazione , fai clic su **Fork**.
 
1. Se vuoi utilizzare GitHub Issues per tracciare i problemi, seleziona la casella di spunta **Abilita GitHub Issues**.
1. Fai clic su **Crea integrazione**.
1. Fai clic sul tile del repository GitHub con cui vuoi lavorare. Si apre il sito Web di GitHub in cui puoi visualizzare i contenuti del repository.
 
  **Suggerimento**: puoi utilizzare gli strumenti per la gestione del codice sorgente integrati in Eclipse Orion {{site.data.keyword.webide}} per modificare il repository GitHub e distribuire un'applicazione dal tuo spazio di lavoro.

1. Se hai abilitato GitHub Issues, fai clic sul suo tile per aprirlo.

Per ulteriori informazioni, vedi [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} e [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configurazione di Dedicated GitHub Enterprise
{: #configghe}

{{site.data.keyword.ghe_long}}  è un servizio di hosting Web installato in loco per i repository Git. Dedicated GitHub Enterprise è disponibile solo per i clienti di {{site.data.keyword.Bluemix_notm}} dedicato. GitHub Issues è uno strumento di traccia che mantiene il tuo lavoro e i tuoi progetti in un unico posto. Viene integrato nel tuo repository di sviluppo in modo che tu possa concentrarti sulle attività importanti. Per ulteriori informazioni su Dedicated GitHub Enterprise e GitHub Issues, vedi [Using Dedicated GitHub Enterprise](../services/ghededicated/index.html){: new_window} e [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Puoi configurare {{site.data.keyword.ghe_short}} come integrazione dello strumento nella tua toolchain in modo da poter gestire il codice sorgente nell'istanza [{{site.data.keyword.Bluemix_notm}} dedicato](../dedicated/index.html#dedicated){: new_window} all'interno della tua azienda.

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, completa la seguente procedura:

 a. Prima di effettuare il primo accesso a Dedicated GitHub Enterprise, chiedi all'amministratore della tua regione aziendale di aggiungere il tuo ID utente all'istanza di {{site.data.keyword.Bluemix_notm}} dedicato dal registro utente della tua azienda utilizzando LDAP. Per informazioni sull'impostazione del tuo account {{site.data.keyword.ghe_short}}, vedi [Using Dedicated GitHub Enterprise](../services/ghededicated/index.html){: new_window}.
 
 b. Nella sezione Integrazioni configurabili, fai clic su **{{site.data.keyword.ghe_short}}**.    
 
 c. Controlla il nome predefinito per il nuovo repository {{site.data.keyword.ghe_short}}. Se necessario, modifica il nome del nuovo repository. La seguente immagine mostra un esempio di repository che viene clonato da un repository campione. Puoi utilizzare un repository nuovo o esistente. Per utilizzare un nuovo repository, puoi scegliere di crearne uno vuoto, clonare o biforcare un repository.
 ![Percorsi dei repository predefiniti](images/toolchain_ghe_config.png)
   
1. Se disponi di una toolchain in {{site.data.keyword.Bluemix_notm}} pubblico e stai aggiungendo questa integrazione dello strumento, nel dashboard DevOps, sulla scheda **Toolchain**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica della tua applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**. Se stai utilizzando una toolchain in {{site.data.keyword.Bluemix_notm}} dedicato, nel Dashboard, sulla scheda **DEVOPS**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nell'angolo superiore destro della pagina Panoramica dell'applicazione, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**.
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazioni strumento, fai clic su **{{site.data.keyword.ghe_short}}**.
1. Se disponi di un repository {{site.data.keyword.ghe_short}} che vuoi utilizzare, immetti l'URL del repository. Per il tipo di repository, fai clic su **Esistente**.
1. Se vuoi utilizzare un nuovo repository {{site.data.keyword.ghe_short}}, immetti un nome per il repository, immetti l'URL del repository da clonare o biforcare e seleziona il tipo di repository: 

 a. Per creare un repository vuoto, fai clic su **Nuovo**. 
 
 b. Per creare una copia di un repository, fai clic su **Clona**.
 
 c. Per biforcare un repository in modo che sia possibile fornire le modifiche attraverso le richieste di importazione , fai clic su **Fork**.
 
1. Per utilizzare GitHub Issues per la traccia dei problemi, seleziona la casella di spunta **Abilita GitHub Issues**.
1. Fai clic su **Crea integrazione**.
1. Fai clic sul tile del repository {{site.data.keyword.ghe_short}} con cui vuoi lavorare. Si aprirà l'istanza di [{{site.data.keyword.Bluemix_notm}} dedicato ](../dedicated/index.html#dedicated){: new_window} della tua azienda, in cui puoi visualizzare i contenuti del repository.
 
  **Suggerimento**: puoi utilizzare gli strumenti per la gestione del codice sorgente integrati in Eclipse Orion {{site.data.keyword.webide}} per modificare il repository {{site.data.keyword.ghe_short}} e distribuire un'applicazione dal tuo spazio di lavoro.

1. Se hai abilitato GitHub Issues, fai clic sul suo tile.

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## Configurazione di PagerDuty
{: #pagerduty}

PagerDuty integra i dati provenienti da più sistemi di monitoraggio in una singola vista. Quando si verifica un problema, PagerDuty garantisce che il membro del team più adatto a risolverlo riceva subito una notifica. Se il membro del team non risponde al problema, è possibile configurare delle escalation per indirizzare la notifica ad assistenti tecnici o responsabili operativi secondari.

Configura PagerDuty per inviare notifiche quando si verificano degli errori nelle fasi della pipeline per consentirti di risolvere i problemi più rapidamente e ridurre i tempi di inattività:

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Integrazioni configurabili, fai clic su **PagerDuty**.
1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, sulla scheda **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazioni strumento, fai clic su **PagerDuty**
1. Immetti il nome del sito PagerDuty associato al tuo account PagerDuty. Se non disponi di un account PagerDuty, [registrane uno](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Immetti la chiave di accesso API per il tuo account PagerDuty. Per istruzioni su come individuare la chiave, vedi [Autenticazione API](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Immetti il nome del tuo servizio PagerDuty.
1. Immetti l'indirizzo e-mail del contatto PagerDuty principale.
1. Immetti il numero di telefono del contatto PagerDuty principale.
1. Fai clic su **Crea integrazione**.
1. Fai clic sul tile di PagerDuty per andare alla pagina pagerduty.com. Puoi visualizzare gli eventi associati al servizio PagerDuty che hai specificato durante la configurazione di questa integrazione dello strumento per la tua toolchain. 

Per ulteriori informazioni, vedi [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configurazione di Sauce Labs
{: #saucelabs}

Sauce Labs esegue gli unit test funzionali. Quando una suite di test Sauce Labs viene configurata come lavoro di test in {{site.data.keyword.deliverypipeline}}, la suite può eseguire i test nella tua applicazione Web o mobile come parte del processo di fornitura continua. Questi test possono fornire un utile controllo dei flussi per i tuoi progetti, in quanto fungono da porte per impedire la distribuzione di codice errato.

Configura Sauce Labs per eseguire test funzionali automatizzati su più sistemi operativi e browser affinché tu possa emulare il modo in cui un utente può utilizzare un sito Web o un'applicazione:

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Integrazioni configurabili, fai clic su **Sauce Labs**.
1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, sulla scheda **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**. 
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazioni strumento, fai clic su **Sauce Labs**.
1. Immetti il nome utente associato al tuo account Sauce Labs. Puoi [trovare il tuo nome utente nel messaggio di benvenuto nella parte superiore della pagina di account Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Immetti la chiave di accesso per il tuo account Sauce Labs. Puoi [trovare la chiave nell'angolo inferiore a sinistra della pagina di account Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Fai clic su **Crea integrazione**.
1. Fai clic sul tile di Sauce Labs per accedere alla pagina saucelabs.com e visualizzare l'attività di test per la toolchain.

 **Suggerimento**: se hai aggiunto un lavoro di test Sauce Labs a {{site.data.keyword.deliverypipeline}}, puoi selezionare l'istanza del servizio.

Per ulteriori informazioni, vedi [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configurazione di Slack
{: #slack}

**Importante**: le notifiche che vengono pubblicate nei canali Slack pubblici sono visibili a tutti i membri del team. Ricorda che sei responsabile dei contenuti che pubblichi.

Slack è un sistema di messaggistica e notifica in tempo reale basato su cloud. Il sistema Slack fornisce una chat permanente, consentendo ai team di collaborare in modo più interattivo rispetto all'utilizzo delle sole e-mail. Puoi comunicare con il tuo team su un canale dedicato o su un insieme di canali direttamente correlato al tuo lavoro. Puoi anche condividere file e immagini attraverso i canali o in messaggi diretti tra due o più persone. Le comunicazioni nei messaggi diretti e sui canali vengono conservate affinché tu possa ricercarle. 

Configura Slack per ricevere le notifiche relative alla tua toolchain dalle integrazioni dello strumento, ad esempio le attività di test e di distribuzione.

1. Se stai configurando questa integrazione dello strumento mentre crei la toolchain, nella sezione Integrazioni configurabili, fai clic su **Slack**.
1. Se disponi di una toolchain a cui stai aggiungendo questa integrazione dello strumento, sulla scheda **Toolchain** del dashboard DevOps, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**.
1. Fai clic sul pulsante di aggiunta (+).
1. Nella sezione Integrazioni strumento, fai clic su **Slack**.
1. Immetti il token di autenticazione dell'API per il tuo account Slack. Per l'autenticazione con Slack, devi utilizzare un token di accesso completo generato. Per istruzioni su come trovare il token, vedi [Slack authentication](https://api.slack.com/web#authentication){: new_window}.
1. Immetti il nome del canale Slack su cui desideri inviare le notifiche. Se il canale specificato non esiste, verrà creato automaticamente. Se il canale è stato archiviato, verrà riattivato. 
1. Fai clic su **Crea integrazione**.
1. Fai clic sul tile di Slack. Puoi visualizzare tutte le attività della tua toolchain nel canale Slack configurato.

Per ulteriori informazioni, fai clic su [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
