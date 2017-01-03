---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Gestione di applicazioni Liberty e Node.js
{: #app_management}


La Gestione applicazioni è un insieme di programmi di utilità per lo sviluppo e il debug che è possibile abilitare per
 le tue applicazioni Liberty e Node.js su {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Programmi di utilità di Gestione applicazioni
{: #Utilities}

### Questi programmi di utilità supportano sia Liberty che Node.js
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

Il *proxy* fornisce una minima gestione delle applicazioni tra la tua applicazione e {{site.data.keyword.Bluemix_notm}}.

Quando abilitato, il pacchetto di build avvia un agent proxy ubicato tra il runtime e il contenitore della tua applicazione. Il programma di utilità *proxy* gestisce tutte le richieste ricevute dall'applicazione. A seconda del tipo di richiesta, esegue un'azione di gestione applicazioni oppure inoltra la richiesta alla tua applicazione. *proxy* consente l'abilitazione della maggior parte degli altri programmi di utilità di Gestione applicazioni. Abilitando il *proxy*, il tuo contenitore dell'applicazione continua a funzionare, anche se l'applicazione si arresta in modo anomalo. L'agent proxy consente inoltre aggiornamenti di file incrementali, che abilitano la modalità "Live Edit" per le applicazioni Node.js.

#### devconsole
{: #devconsole}

Il programma di utilità della console di sviluppo (*devconsole*) è accessibile al seguente URL:
```
  http://<yourappname>.mybluemix.net/bluemix-debug/manage
```

Mediante la console di sviluppo, gli utenti possono riavviare, arrestare o sospendere le proprie applicazioni. Gli utenti possono anche abilitare o accedere ai programmi di utilità shell e inspector.

Per Node versione 6.3.0 o superiore, la console di sviluppo fornisce un pulsante di riavvio per la tua applicazione e l'accesso al programma di utilità della shell.  Per ulteriori informazioni, vedi la discussione su *inspector*.

Il programma di utilità devconsole avvia anche *proxy*.

#### hc
{: #hc}

L'agent Health Center (*hc*) abilita il monitoraggio della tua applicazione mediante il client Health Center.

Health Center supporta l'analisi delle prestazioni delle tue applicazioni Liberty e Node.js utilizzando gli strumenti IBM Monitoring and Diagnostic. Per ulteriori informazioni, vedi [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>

#### shell
{: #shell}

Il programma di utilità *shell* abilita una shell basata su Web.  È accessibile dal programma di utilità *devconsole* o mediante il seguente URL:

```
  http://<yourappname>.mybluemix.net/bluemix-debug/shell
```

Dopo aver effettuato l'accesso al programma di utilità *shell* viene visualizzata una finestra di terminale con l'accesso shell nella tua applicazione. Puoi effettuare tutte le attività supportate in una normale shell, ad esempio modificare i file, controllare l'utilizzo della memoria o eseguire i comandi di diagnostica.

Il programma di utilità *shell* avvia anche *proxy*.

### Questi programmi di utilità supportano solo Liberty
{: #liberty_utilities}

#### debug
{: #debug}

Il programma di utilità *debug* mette l'applicazione Liberty in modalità di debug e consente ai client quali IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} di stabilire una sessione di debug remota con l'applicazione.

Per ulteriori informazioni, vedi [Debug remoto](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug).

Il programma di utilità *debug* avvia anche *proxy*.

#### jmx
{: #jmx}

Il programma di utilità *jmx* abilita il connettore JMX REST per consentire a un client JMX remoto di gestire l'applicazione utilizzando le credenziali utente di {{site.data.keyword.Bluemix_notm}}.

Per ulteriori informazioni sulla configurazione di un connettore JMX, vedi [Configuring secure JMX connection to the Liberty profile.](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.

Il programma di utilità *jmx* non avvia proxy.

### Questi programmi di utilità supportano solo Node.js
{: #node_utilities}

#### inspector
{: #inspector}

Per le versioni di Node.js precedenti alla 6.3.0, *inspector* abilita l'interfaccia del programma di debug node inspector a cui è possibile accedere dal programma di utilità *devconsole* o da *https://myApp.mybluemix.net/bluemix-debug/inspector.*

Il processo *inspector* viene eseguito nel contenitore della tua applicazione. Utilizza questo programma di utilità per creare profili di utilizzo CPU, aggiungere punti di interruzione e codice di debug, il tutto mentre la tua applicazione è in esecuzione su {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni sul modulo node inspector, vedi [node-inspector on GitHub](https://github.com/node-inspector/node-inspector){:new_window}.

Il programma di utilità *inspector* avvia anche *proxy*.

Per Node.js versioni 6.3.0 e successive, *inspector* utilizza [V8 Inspector Integration for Node.js](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}. Nei log della tua applicazione troverai un URL che può essere utilizzato per collegare Chrome DevTools alla tua applicazione.  I messaggi di log sono simili ai seguenti:

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node-hc --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

In questo scenario, la *devconsole* **non** mostrerà un link all'*inspector*, in quanto l'URL non esiste.

In questo scenario, il *proxy* non istraderà il traffico all'*inspector*. Dovrai creare un tunnel SSH alla tua applicazione affinché l'URL Chrome DevTools funzioni.  Per creare il tunnel SSH, utilizza il comando 'cf ssh' in un modo simile al seguente:

```
  cf ssh -N -T -L <port>:127.0.0.1:<hostport> <appName>
```

In questo comando, *hostport* deve essere il valore di porta indicato nel messaggio di log "Debugger listening on port xxxx" e *port* è una qualsiasi porta disponibile nel sistema da cui viene immesso il comando "cf ssh".

#### trace
{: #trace}

Il programma di utilità *trace* ti consente di impostare in modo dinamico i livelli di traccia se la tua applicazione utilizza i moduli di registrazione *log4js*, *ibmbluemix* o *bunyan*.

**Nota:** versioni supportate per le dipendenze:
* log4js:(0.6.0 - 0.6.24)
* bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
* ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)

Vai alla pagina Dettagli istanza nella console Web di {{site.data.keyword.Bluemix_notm}} e seleziona **Azioni** per visualizzare l'interfaccia utente.

Il programma di utilità *trace* non è disponibile se l'applicazione è stata avviata utilizzando l'opzione "-b buildpack".

Il programma di utilità *trace* non avvia *proxy*.

##  Come configurare Gestione applicazioni
{: #configure}

Per abilitare i programmi di utilità Gestione applicazioni, imposta la variabile di ambiente *BLUEMIX_APP_MGMT_ENABLE* e prepara di nuovo
l'applicazione. È possibile abilitare più programmi di utilità separandoli con un “+”.

Ad esempio, per abilitare i programmi di utilità *devconsole* e *shell*, immetti il seguente comando:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Prepara di nuovo la tua applicazione dopo aver impostato la variabile di ambiente:

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

## Limitazioni
{: #restrictions}

* Gestione applicazioni supporta solo le applicazioni a istanza singola.
* Le modifiche apportate alla tua applicazione mediante Gestione applicazioni sono transitorie e vengono perse una volta che si esce da questa modalità. Questa modalità serve solo per un uso di sviluppo temporaneo e non è prevista per l'utilizzo in un ambiente di produzione per via delle prestazioni.
* La maggior parte dei programmi di utilità di Gestione applicazioni non funziona se imposti il tuo comando di avvio nel file manifest.yml (comando) o nella CLI CF (-c). Questi metodi sono delle sostituzioni del pacchetto di build e rappresentano l'antimodello per l'avvio delle applicazioni Node.js. Per dei risultati ottimali, imposta il comando di avvio nel file package.json o Procfile.

## Modalità di sviluppo per Eclipse Tools
{: #devmode}

La modalità di sviluppo è una funzione di [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) che offre agli sviluppatori la possibilità di utilizzare le proprie applicazioni mentre sono in esecuzione nel cloud.

Lavorando con le loro applicazioni su {{site.data.keyword.Bluemix_notm}}, gli sviluppatori potrebbero sentire che le
loro normali attività di sviluppo sono limitate rispetto a un ambiente di sviluppo locale. Per risolvere questo problema,
la modalità di sviluppo attraverso Eclipse Tools ti offre un modo per poter lavorare nel cloud e al contempo
operare in uno spazio di lavoro temporaneo e protetto.

La modalità di sviluppo è supportata sia per le applicazioni Liberty che Node.js. Con la modalità di sviluppo
abilitata per la tua applicazione Liberty o Node.js, puoi aggiornare i file di applicazione in modo incrementale
senza dover distribuire l'applicazione. Puoi anche stabilire una sessione di debug con la tua
applicazione. La modalità di sviluppo per le applicazioni Liberty è equivalente all'abilitazione dei programmi di utilità di debug e di Gestione applicazioni
jmx. Per le applicazioni Node.js, è equivalente all'abilitazione dei programmi di utilità *devconsole*, *inspector* e *shell*.
