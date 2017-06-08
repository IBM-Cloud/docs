---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Registrazione delle applicazioni di runtime attraverso le applicazioni CF
{: #logging_writing_to_log_from_cf_app}

In {{site.data.keyword.Bluemix}}, per conservare i dati di log per un'applicazione Cloud Foundry e il relativo runtime, devi scrivere i tuoi log in STDOUT e STDERR. 
{:shortdesc}

In {{site.data.keyword.Bluemix_notm}}, i record dei log STDOUT e STDERR vengono raccolti automaticamente:

* STDOUT (output standard) fornisce informazioni generali.  
* STDERR (errore standard) fornisce informazioni che includono messaggi di errore e altre avvertenze di diagnostica. 

Loggregator raccoglie automaticamente i dati di output standard ed errore standard. Loggregator è il componente che inoltra i log dall'interno di Cloud Foundry. 

Ad esempio, 

Per un'**applicazione Cloud Foundry Liberty**, il console.log predefinito per il server Liberty viene prelevato automaticamente dal Loggregator. 

* Il console.log contiene i STDOUT e STDERR reindirizzati dal processo JVM. L'output della console contiene gli eventi e gli errori principali se utilizzi la configurazione consoleLogLevel predefinita. Se utilizzi la configurazione copySystemStreams predefinita, questo output contiene anche i messaggi che vengono scritti nei flussi system.out e system.err. L'output della console contiene sempre i messaggi scritti direttamente dal processo JVM, come l'output -verbose:gc. Puoi regolare il livello di registrazione di Liberty tramite il file server.xml.
* Il consoleLogLevel imposta il livello di filtro del gestore console.log. Quando imposti il consoleLogLevel su INFO, configuri tutti i messaggi INFO, AUDIT, WARNING e ERROR in modo che vengano scritti nel file console.log. **Nota:** le voci di log FINE, FINER, FINEST vengono scritte solo nel file trace.log.

Per ulteriori informazioni sulle applicazioni Liberty for Java™, vedi [Liberty Profile: Logging and Trace ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}.

Per un'**applicazione Cloud Foundry Node.js**, puoi utilizzare il modulo di registrazione integrato della console per configurare la registrazione per il runtime in {{site.data.keyword.Bluemix}}. Puoi inserire i messaggi in stdout e in stderr:

* console.log('message') invierà il messaggio al flusso STDOUT
* console.error('error_message') invierà l'errore al flusso STDERR

Per ulteriori informazioni sulle applicazioni Node.js, vedi [How to log in node.js ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}.


Per ulteriori informazioni sulle **applicazioni Ruby on Rails**, vedi [The Logger ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}.

La seguente tabella elenca l'associazione tra alcuni log dei runtime dell'applicazione e i log raccolti automaticamente da Loggregator:

| **Runtime** |    **STDOUT**     | **STDERR** |
|-----------------|-------------------|-------------------|
| Liberty | system.out | system.err |
| Node.js | console.log, console.info | console.error, console.warn |
| Ruby | stdout| stderr |
{: caption="Tabella 1. Associazione tra alcuni log dei runtime dell'applicazione e i log raccolti automaticamente da Loggregator" caption-side="top"}

