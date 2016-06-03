---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Gestione di applicazioni Liberty e Node.js
{: #app_management}

*Ultimo aggiornamento: 17 marzo 2016*

La Gestione applicazioni è un insieme di programmi di utilità per lo sviluppo e il debug che è possibile abilitare per
 le tue applicazioni Liberty e Node.js su {{site.data.keyword.Bluemix}}.
{:shortdesc}

##Programmi di utilità di Gestione applicazioni
{: #Utilities}

Questi programmi di utilità supportano sia Liberty che Node.js.

  1. *proxy*: gestione applicazioni minima che funge da proxy tra la tua applicazione e {{site.data.keyword.Bluemix_notm}}.

    Quando abilitato, il pacchetto di build avvia un agent proxy ubicato tra il runtime e il contenitore della tua applicazione. Il programma di utilità *proxy* gestisce tutte le richieste ricevute dall'applicazione. A seconda del tipo di richiesta, esegue un'azione di gestione applicazioni oppure inoltra la richiesta alla tua applicazione. *proxy* consente l'abilitazione della maggior parte degli altri programmi di utilità di Gestione applicazioni. Abilitando il *proxy*, il tuo contenitore dell'applicazione continua a funzionare, anche se l'applicazione si arresta in modo anomalo. L'agent proxy consente inoltre aggiornamenti di file incrementali, che abilitano la modalità "Live Edit" per le applicazioni Node.js.
	
  2. *devconsole*: abilita il programma di utilità della console di sviluppo che è accessibile al seguente URL:
    ```
    http://<ilnomedellatuaapplicazione>.mybluemix.net/bluemix-debug/manage
    ```
	
    Mediante la console di sviluppo, gli utenti possono riavviare, arrestare o sospendere le proprie applicazioni. Gli utenti possono anche abilitare o accedere ai programmi di utilità shell e inspector.

    Il programma di utilità devconsole avvia anche *proxy*.
	
  3. *hc*: agent Health Center che abilita il monitoraggio della tua applicazione mediante il client Health Center.

    Health Center supporta l'analisi delle prestazioni delle tue applicazioni Liberty e Node.js utilizzando gli strumenti IBM Monitoring and Diagnostic. Per ulteriori informazioni, vedi [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>
	
  4. *shell*: abilita una shell basata su Web a cui è possibile accedere dal programma di utilità devconsole o mediante il seguente URL:
    ```
    http://<ilnomedellatuaapplicazione>.mybluemix.net/bluemix-debug/shell
    ```
	
    Dopo aver effettuato l'accesso al programma di utilità shell, viene visualizzata una finestra di terminale con l'accesso shell nella tua applicazione. Puoi effettuare tutte le attività supportate in una normale shell, ad esempio modificare i file, controllare l'utilizzo della memoria o eseguire i comandi di diagnostica.
	
    Il programma di utilità *shell* avvia anche *proxy*.

Questi programmi di utilità supportano solo Liberty.

  1. *debug*: attiva la modalità di debug per l'applicazione Liberty e consente ai client quali IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} di stabilire una sessione di debug remota con l'applicazione.
  
   Per ulteriori informazioni, vedi [Debug remoto](../manageapps/eclipsetools/eclipsetools.html#remotedebug).
   
   Il programma di utilità *debug* avvia anche *proxy*.
   
  2. *jmx*: abilita il connettore JMX REST per consentire a un client JMX remoto di gestire l'applicazione utilizzando le credenziali utente di {{site.data.keyword.Bluemix_notm}}.
  
  Per ulteriori informazioni sulla configurazione di un connettore JMX, vedi [Configuring secure JMX connection to the Liberty profile.](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.
  
  Il programma di utilità *jmx* non avvia proxy.

Questi programmi di utilità supportano solo Node.js.

  1. *inspector*: abilita l'interfaccia del programma di debug node inspector a cui è possibile accedere dal programma di utilità *devconsole* o da *https://myApp.mybluemix.net/bluemix-debug/inspector.*
  
  Il processo inspector viene eseguito nel contenitore della tua applicazione. Utilizza questo programma di utilità per creare profili di utilizzo CPU, aggiungere punti di interruzione e codice di debug, il tutto mentre la tua applicazione è in esecuzione su {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni sul modulo node inspector, vedi [node-inspector on GitHub](https://github.com/node-inspector/node-inspector){:new_window}.
  
  Il programma di utilità *inspector* avvia anche *proxy*.
  
  2. *strongpm*: abilita l'utilizzo di [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} per analizzare la tua applicazione Node.js con programmi di utilità quali [StrongLoop Metrics, Profiling e Tracing](https://strongloop.com/node-js/devops-tools/){:new_window}.
    
  Il programma di utilità *strongpm* avvia anche *proxy*.
  
  Completa la seguente procedura per configurare la tua applicazione Node.js con [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window}.

    1. Configura la variabile di ambiente *strongpm* BlUEMIX_APP_MGMT_ENABLE e prepara di nuovo l'applicazione.
    
	```
    cf set-env <nomeapplicazione> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <nomeapplicazione>
```
	
    2. Dalla riga di comando Cloud Foundry, aggiungi una rotta alla tua applicazione, dove la rotta ha "-pm" aggiunto al nome applicazione, ad esempio <nomeapplicazione>-pm.mybluemix.net.
    
	```
    cf map-route <nomeapplicazione> ng.bluemix.net -n <nomeapplicazione>-pm
```
	
    3. Installa il [modulo StrongLoop npm](https://www.npmjs.com/package/strongloop){:new_window} sulla tua workstation locale.
    
	```
    npm install -g strongloop
```
	
    4. Crea un account sul [sito Web di StrongLoop](https://strongloop.com/register/){:new_window}.
    5. Avvia Arc sulla tua workstation locale e accedi con l'account creato.
    
	```
    slc arc
```
	
    6. Passa alla vista Process Manager all'interno di Arc. Immetti la rotta appena creata con la porta 80 in Process Manager. Premi il pulsante Attiva. Per ulteriori dettagli, consulta la [documentazione completa sull'utilizzo di Arc](https://docs.strongloop.com/display){:new_window}.
	
  3. *trace*: imposta in modo dinamico i livelli di traccia se la tua applicazione utilizza i moduli di registrazione *log4js*, *ibmbluemix* o *bunyan*.
  
  **Nota:** versioni supportate per le dipendenze:

    * log4js:(0.6.0 - 0.6.24)
    * bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
    * ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)
  
  Vai alla pagina Dettagli istanza nella console Web di {{site.data.keyword.Bluemix_notm}} e seleziona **Azioni** per visualizzare l'interfaccia utente.

  Il programma di utilità *trace* non avvia *proxy*.

##Come configurare Gestione applicazioni
{: #configure}

Per abilitare i programmi di utilità Gestione applicazioni, imposta la variabile di ambiente *BLUEMIX_APP_MGMT_ENABLE* e prepara di nuovo
l'applicazione. È possibile abilitare più programmi di utilità separandoli con un “+”.

Ad esempio, per abilitare i programmi di utilità devconsole e *shell*, immetti il seguente comando:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Non dimenticarti di preparare di nuovo la tua applicazione dopo che hai impostato la variabile di ambiente:

```
cf restage myApp
```

Se non vuoi che i programmi di utilità Gestione applicazioni siano installati con la tua applicazione, imposta
la variabile di ambiente *BLUEMIX_APP_MGMT_INSTALL* su 'false' e prepara di nuovo la tua applicazione.

Ad
esempio:

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

##Limitazioni
{: #restrictions}

* Gestione applicazioni supporta solo le applicazioni a istanza singola.
* Le modifiche apportate alla tua applicazione mediante Gestione applicazioni sono transitorie e vengono perse una volta che si esce da questa modalità. Questa modalità serve solo per un uso di sviluppo temporaneo e non è prevista per l'utilizzo in un ambiente di produzione per via delle prestazioni.
* La maggior parte dei programmi di utilità di Gestione applicazioni non funziona se imposti il tuo comando di avvio nel file manifest.yml (comando) o nella CLI CF (-c). Questi metodi sono delle sostituzioni del pacchetto di build e rappresentano l'antimodello per l'avvio delle applicazioni Node.js. Per dei risultati ottimali, imposta il comando di avvio nel file package.json o Procfile.

##Modalità di sviluppo per Eclipse Tools
{: #devmode}

La modalità di sviluppo è una funzione di [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools) che offre agli sviluppatori la possibilità di utilizzare le proprie applicazioni mentre sono in esecuzione nel cloud.

Lavorando con le loro applicazioni su {{site.data.keyword.Bluemix_notm}}, gli sviluppatori potrebbero sentire che le
loro normali attività di sviluppo sono limitate rispetto a un ambiente di sviluppo locale. Per risolvere questo problema,
la modalità di sviluppo attraverso Eclipse Tools ti offre un modo per poter lavorare nel cloud e al contempo
operare in uno spazio di lavoro temporaneo e protetto.

La modalità di sviluppo è supportata sia per le applicazioni Liberty che Node.js. Con la modalità di sviluppo
abilitata per la tua applicazione Liberty o Node.js, puoi aggiornare i file di applicazione in modo incrementale
senza dover distribuire l'applicazione. Puoi anche stabilire una sessione di debug con la tua
applicazione. La modalità di sviluppo per le applicazioni Liberty è equivalente all'abilitazione dei programmi di utilità di debug e di Gestione applicazioni
jmx. Per le applicazioni Node.js, è equivalente all'abilitazione dei programmi di utilità *devconsole*, *inspector* e *shell*.
