---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---



{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}


# Debug
{: #debugging}

Se si verificano problemi con {{site.data.keyword.Bluemix}}, puoi visualizzare i file di log per analizzare i problemi ed eseguire il debug degli errori.
{:shortdesc}

I log forniscono informazioni quali la corretta esecuzione di un lavoro o la sua mancata riuscita. Forniscono anche informazioni pertinenti che possono essere utilizzate per eseguire il debug e determinare la causa di un problema.

I log sono in un formato fisso. Per i log dettagliati, puoi filtrarli o utilizzare degli host di registrazione esterni per memorizzare ed elaborare i log. Per ulteriori informazioni su formati dei log, visualizzazione e filtraggio dei log e configurazione della registrazione esterna, vedi [Registrazione per le applicazioni in esecuzione su Cloud Foundry](/docs/monitor_log/monitoringandlogging.html#logging_for_bluemix_apps).


## Debug degli errori di preparazione
{: #debugging-staging-errors}
Potrebbero verificarsi dei problemi durante la preparazione delle tue applicazioni su {{site.data.keyword.Bluemix_notm}}. Se la preparazione della tua applicazione non viene eseguita correttamente, puoi visualizzare ed effettuare ricerche nei log di preparazione (STG) al fine di scoprire cosa è accaduto durante la distribuzione dell'applicazione e risolvere il problema. Per ulteriori informazioni sui metodi di visualizzazione dei log per le applicazioni Bluemix, vedi [visualizzazione dei log](/docs/monitor_log/monitoringandlogging.html#viewing_logs).  

Per comprendere il motivo per cui la tua applicazione potrebbe provocare errori in {{site.data.keyword.Bluemix_notm}}, devi sapere come vengono distribuite ed eseguite le applicazioni in {{site.data.keyword.Bluemix_notm}}. Per informazioni dettagliate, vedi [Distribuzione
delle applicazioni](/docs/manageapps/depapps.html#appdeploy).


La seguente procedura mostra come puoi utilizzare il comando `cf logs` per eseguire il debug degli errori di preparazione. Prima di iniziare
la procedura, assicurati di aver installato l'interfaccia riga di comando cf. Per ulteriori informazioni sull'installazione dell'interfaccia
riga di comando cf, vedi [Installing the cf
command line           interface](/docs/starters/install_cli.html).

  1. Connettiti a {{site.data.keyword.Bluemix_notm}} immettendo il seguente codice nell'interfaccia riga di comando cf:
     ```
	 cf api https://api.ng.bluemix.net
	 ```

  2. Accedi a {{site.data.keyword.Bluemix_notm}} immettendo `cf login`.

  3. Recupera i log recenti immettendo `cf logs appname --recent`. Se vuoi filtrare un log dettagliato, utilizza l'opzione `grep`. Ad esempio, puoi immettere il seguente codice per visualizzare solo i log [STG]:
    ```
	cf logs appname --recent | grep '\[STG\]'
	```
  4. Visualizza il primo errore mostrato nel log.

Se utilizzi distribuisci le applicazioni attraverso gli strumenti IBM Eclipse per il plug-in {{site.data.keyword.Bluemix_notm}}, nella scheda **Console** dello strumento Eclipse puoi visualizzare dei log simili all'output di cf logs. Puoi anche aprire una finestra di Eclipse separata per tracciare `i log` quando distribuisci l'applicazione.

Oltre al comando `cf logs`, in {{site.data.keyword.Bluemix_notm}} puoi utilizzare anche il servizio Monitoring and Analytics per raccogliere i dettagli del log. Inoltre, il servizio Monitoring and Analytics monitora le prestazioni, l'integrità e la disponibilità delle tue applicazioni. Fornisce anche analisi di log per le applicazioni di runtime Node.js e Liberty.  

### Debug degli errori di preparazione per un'applicazione Node.js

Il seguente esempio mostra un log che viene visualizzato dopo che immetti `cf logs nomeapplicazione --recent`. Nell'esempio
si suppone che si siano verificati errori di preparazione per un'applicazione Node.js:
```
2014-08-11T14:19:36.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({name"=>"SampleExpressApp"}
2014-08-11T14:20:44.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STOPPED"})
2014-08-11T14:20:44.19+0100 [App/0]   ERR
2014-08-11T14:20:44.43+0100 [DEA]     OUT Stopping app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:44.44+0100 [DEA]     OUT Stopped app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:48.97+0100 [DEA]     OUT Got staging request for app with id 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:50.94+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STARTED"})
2014-08-11T14:20:51.66+0100 [STG]     OUT -----> Download app package (4.1M)
2014-08-11T14:20:51.90+0100 [STG]     OUT -----> Download app buildpack cache (1.1M)
2014-08-11T14:20:52.78+0100 [STG]     OUT -----> Buildpack Version: v1.1-20140717-1447
2014-08-11T14:20:52.78+0100 [STG]     ERR parse error: Expected another key-value pair at line 18, column 3
2014-08-11T14:20:52.79+0100 [STG]     OUT 0 info it worked if it ends with ok
```
{: screen}


Il primo errore nel log mostra il motivo per cui la preparazione non riesce. Nell'esempio, il primo errore è un output del componente DEA
durante la fase di preparazione.
```
2014-08-11T14:20:52.78+0100 [STG]   ERR parse error: expected another key-value pair at line 18, column 3
```
{: screen}


Per un'applicazione Node.js, il DEA utilizza le informazioni contenute nel file `package.json` per scaricare i moduli. Da questo errore, puoi vedere
che l'errore si verifica per il modulo. Pertanto, potresti dover riesaminare la riga 18 del file `package.json`.

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*",
18   }
```
{: screen}


Puoi notare che viene inserita una virgola alla fine della riga 17 e quindi è prevista una coppia chiave-valore alla riga 18. Per correggere il problema, rimuovi la virgola:

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*"
18   }
```
{: screen}


## Debug degli errori di runtime
{: #debugging-runtime-errors}
Se durante il runtime riscontri dei problemi con la tua applicazione, i log dell'applicazione possono aiutarti a individuare la causa dell'errore e a risolvere il problema.

In particolare, è possibile abilitare la registrazione in stdout e stderr. Per ulteriori informazioni su come configurare i file di log per le applicazioni
che vengono distribuite tramite i pacchetti di build integrati {{site.data.keyword.Bluemix_notm}}, consulta il seguente elenco:

  * Per le applicazioni Liberty for Java™, consulta [Liberty Profile: Logging and Trace ![icona link esterno](../icons/launch-glyph.svg)](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}.
  * Per le applicazioni Node.js, vedi [How to log in node.js ![icona link esterno](../icons/launch-glyph.svg)](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}.
  * Per le applicazioni PHP, vedi [error_log ![icona link esterno](../icons/launch-glyph.svg)](http://php.net/manual/en/function.error-log.php){: new_window}.
  * Per le applicazioni Python, vedi [Logging HOWTO ![icona link esterno](../icons/launch-glyph.svg)](https://docs.python.org/2/howto/logging.html){: new_window}.
  * Per le applicazioni Ruby on Rails, vedi [The Logger ![icona link esterno](../icons/launch-glyph.svg)](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}.
  * Per le applicazioni Ruby Sinatra, vedi [Logging ![icona link esterno](../icons/launch-glyph.svg)](http://www.sinatrarb.com/intro.html#Logging){: new_window}.

Quando immetti `cf logs nomeapplicazione --recent` nell'interfaccia riga di comando cf, vengono visualizzati solo i log più recenti. Per visualizzare i log con gli errori che si sono verificati in precedenza, devi recuperare tutti i log e ricercare gli errori. Per recuperare tutti i log per la tua applicazione, utilizza uno dei seguenti metodi:
<dl>
<dt><strong>Servizio {{site.data.keyword.Bluemix_notm}} Monitoring and Analytics</strong></dt>
<dd>La capacità di ricerca e analisi dei file di log del servizio Monitoring and Analytics possono aiutarti a identificare rapidamente gli errori. Per ulteriori informazioni, vedi <a href="../services/monana/index.html#gettingstartedtemplate" target="_blank">Monitoring and Analytics</a>.</dd>
<dt><strong>Strumenti di terze parti </strong></dt>
<dd>Puoi raccogliere ed esportare i log dalla tua applicazione a un host di log esterno. Per ulteriori informazioni, vedi <a href="../monitor_log/monitoringandlogging.html#thirdparty_logging" target="_blank">Configurazione della registrazione esterna</a>.</dd>
<dt><strong>Script per la raccolta e l'esportazione dei log  </strong></dt>
<dd>Per utilizzare uno script per la raccolta e l'esportazione automatica dei log in un file esterno, devi connetterti alla console {{site.data.keyword.Bluemix_notm}} dal tuo computer in cui deve essere disponibile spazio sufficiente per scaricare i log. Per ulteriori informazioni, vedi <a href="../support/index.html#collecting-diagnostic-information" target="_blank">Raccolta delle informazioni di diagnostica</a>. </dd>
</dl>

I file `stdout.log` e `stderr.log` erano precedentemente accessibili, per impostazione predefinita, tramite la vista dell'applicazione nella console {{site.data.keyword.Bluemix_notm}} sotto **File** > **log**. Tuttavia, tale registrazione dell'applicazione non è più disponibile
con la versione corrente di Cloud Foundry in cui è ospitato {{site.data.keyword.Bluemix_notm}}. Per fare in modo che la registrazione dell'applicazione stdout e stderr continui a essere accessibile tramite la console {{site.data.keyword.Bluemix_notm}} sotto **File** > **log**, puoi reindirizzare la registrazione ad altri file nel file system {{site.data.keyword.Bluemix_notm}}, a seconda del runtime che stai utilizzando.

  * Per le applicazioni Liberty for Java, l'output indirizzato a stdout e stderr è già contenuto nel file `messages.log` nella directory logs. Ricerca le voci con prefisso SystemOut e SystemErr.
  * Per le applicazioni Node.js, puoi sovrascrivere la funzione console.log per scrivere esplicitamente in un file nella directory logs.
  * Per le applicazioni PHP, puoi utilizzare la funzione error_log per scrivere in un file nella directory logs.
  * Per le applicazioni Python, puoi fare in modo che il logger scriva in un file nella directory logs: `logging.basicConfig(filename='/docs/logs/example.log',level=logging.DEBUG)`
  * Per le applicazioni Ruby, puoi fare in modo che il logger scriva in un file nella directory logs.


### Debug delle modifiche al codice
{: #debug_code_changes}

Se stai apportando modifiche al codice in un'applicazione già distribuita e funzionante, ma le modifiche non vengono rispecchiate in {{site.data.keyword.Bluemix_notm}}, puoi eseguire il debug utilizzando i log. A prescindere che la tua applicazione sia o no in esecuzione, puoi controllare i log generati durante la distribuzione dell'applicazione o il runtime per scoprire il motivo per cui il nuovo codice non funziona.

A seconda del modo in cui il nuovo codice viene distribuito, scegli uno dei seguenti metodi per eseguire il debug delle modifiche al codice:

  * In caso di nuovo codice distribuito dalla riga di comando cf, controlla l'output del comando *cf push*. Inoltre, puoi utilizzare il comando *cf logs* per trovare ulteriori indizi utili per la risoluzione del problema. Per ulteriori informazioni su come utilizzare il comando *cf logs*, vedi [visualizzazione dei log dall'interfaccia riga di comando](/docs/monitor_log/monitoringandlogging.html#viewing_logs_cli).

  * In caso di nuovo codice distribuito da una GUI, quale ad esempio la console {{site.data.keyword.Bluemix_notm}}, DevOps Delivery Pipeline o l'IC di Travis, puoi controllare i log dall'interfaccia. Ad esempio, se distribuisci il nuovo codice dalla console {{site.data.keyword.Bluemix_notm}}, puoi passare al dashboard, trovare la tua applicazione e visualizzare i log per trovare degli indizi.   Per ulteriori informazioni su come visualizzare i log dalla console {{site.data.keyword.Bluemix_notm}}, vedi [Visualizzazione dei log dal dashboard Bluemix](/docs/monitor_log/monitoringandlogging.html#viewing_logs_UI).  


# rellinks
{: #rellinks}

## general
{: #general}

  * [DEA (Droplet Execution Agent) ![icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/concepts/architecture/execution-agent.html){: new_window}
  * [Introduzione al servizio IBM Monitoring and Analytics per Bluemix](/docs/services/monana/index.html#gettingstartedtemplate)
  * [Come funziona Bluemix](/docs/overview/whatisbluemix.html#howwork)
  * [Installazione dello strumento di comando cf](/docs/starters/install_cli.html)
  * [Visualizzazione dei log](/docs/monitor_log/monitoringandlogging.html#viewing_logs)

  
  
 














