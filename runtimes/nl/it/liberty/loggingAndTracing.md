---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Registrazione e traccia
{: #logging_tracing}

*Ultimo aggiornamento: 23 marzo 2016*

## File di log
{: #log_files}

I log Liberty standard, come messages.log  o la directory ffdc, sono disponibili in IBM Bluemix nella directory dei log di ciascuna istanza dell'applicazione. A questi log è possibile accedere dalla console IBM Bluemix oppure utilizzando i comandi cf logs e cf files.
Ad esempio, per visualizzare il file messages.log, esegui il comando:
```
    $ cf files <nomedellatuaapplicazione> logs/messages.log
```
{: codeblock}

Il livello di log
e le altre opzioni di traccia possono essere impostati mediante il file di configurazione di Liberty. Per ulteriori informazioni, consulta [Liberty profile: Trace and logging](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). La traccia può anche essere regolata su un'istanza dell'applicazione in esecuzione utilizzando la console IBM Bluemix.

## Utilizzo delle funzionalità di traccia e di dump
{: #using_trace_and_dump}

Nell'interfaccia utente IBM Bluemix, sono disponibili delle funzionalità di traccia e di dump.
* Utilizza Traccia per visualizzare e aggiornare la registrazione Liberty traceSpecification sulle istanze dell'applicazione in esecuzione.
* Utilizza Dump per creare e manipolare dump di heap e di thread su istanze dell'applicazione in esecuzione.

Per eseguire tale azione, seleziona un'applicazione Liberty
nell'interfaccia utente. Sotto Runtime nella navigazione sulla sinistra, puoi aprire i dettagli dell'istanza. Seleziona una o più istanze. Nel menu Azioni, puoi scegliere TRACCIA o DUMP.

# rellinks
## general
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
