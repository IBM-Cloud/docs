---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Registrazione e traccia
{: #logging_tracing}

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
* Utilizza Dump per creare i dump di heap e di thread su istanze dell'applicazione in esecuzione. 

Per eseguire tale azione, seleziona un'applicazione Liberty
nell'interfaccia utente. Nella categoria Runtime nella navigazione, puoi aprire i dettagli dell'istanza. Seleziona una o più istanze. Nel menu Azioni, puoi scegliere TRACCIA o DUMP.

## Scarica file dump
{: #download_dumps}

<strong>Prerequisiti: </strong>
* [Installa la CLI CF](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
* [Installa il plug-in Diego-Enabler](https://github.com/cloudfoundry-incubator/Diego-Enabler) se la tua applicaizone viene eseguita in Diego

<strong>Se la tua applicazione viene eseguita in DEA, utilizza le seguenti istruzioni:</strong>
  
1. get app_guid
```
$ cf app <app_name> --guid
```

2. download dump file
```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```

<strong>Se la tua applicazione viene eseguita in Diego, utilizza le seguenti istruzioni:</strong>
  
1. get app_guid
```
$ cf app <app_name> --guid
```

2. get app_ssh_endpoint(host and port) and app_ssh_host_key_fingerprint
```
$ cf curl /v2/info
```

3. get ssh-code for scp command
```
$ cf ssh-code
```

4. scp remote dump file to local, use ssh-code when prompted for a password
```
$ scp -P <app_ssh_endpoint_port> -o User=cf:<app_guid>/<instance_id> <app_ssh_endpoint_host>:/home/vcap/dumps/<dump_file_name> <local_dump_file_name>
```

Consulta [](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) per ulteriori dettagli


# rellinks
{: #rellinks}
## general
{: #general}
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

