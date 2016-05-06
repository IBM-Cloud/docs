---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizzo di Dynatrace
{: #using_dynatrace}

*Ultimo aggiornamento: 08 aprile 2016*

Dynatrace è un servizio di terze parti che fornisce monitoraggio per la tua applicazione.

Per ulteriori informazioni su cosa Dynatrace fornisce, consulta [Monitoraggio applicazione Dynatrace](http://www.dynatrace.com/en/products/application-monitoring.html).

Quando abiliti il servizio Dynatrace per essere utilizzato con la tua applicazione Liberty, devi seguire questi passi di elaborazione:

1. Acquisisci e ospita il file jar dell'agent Dynatrace in modo che il pacchetto di build di Liberty possa scaricarlo.
2. Configura un'istanza del server Dynatrace in modo che l'agent Dynatrace in esecuzione con la tua applicazione Liberty possa comunicare con essa.
3. Configura la tua applicazione Liberty in modo che possa scaricare l'agent Dynatrace e collegarsi al server Dynatrace.

## Ospitare l'agent Dynatrace
{: #hosting_dynatrace_agent}
L'agent Dynatrace deve essere ospitato su un server Web e il pacchetto di build Liberty deve essere in grado di scaricare il jar dell'agent da tale server. Il server deve essere configurato con un file index.yml che specifica i dettagli sul jar dell'agent. Completa i seguenti passi per impostare l'agent Dynatrace:
  1. Scarica il jar dell'agent Dynatrace. Consulta [Dynatrace Server Platform Installers](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) presso il sito Web della community Dynatrace per istruzioni su come scaricare il file jar dell'agent Dynatrace. Il file jar dell'agent appropriato per l'esecuzione su Bluemix è **dynatrace-agent-unix.jar** versione **6.3.0+**.
  2. Ospita il file jar dell'agent in un'ubicazione da cui il pacchetto di build Liberty può scaricarlo. Puoi ospitarlo in Bluemix stesso utilizzando una qualunque delle funzioni del server disponibili, oppure puoi ospitarlo in alcune ubicazioni disponibili pubblicamente
     * Assicurati di fornire un file index.yml all'ubicazione che lo ospita. Il file index.yml deve contenere una voce composta da l'ID versione del jar dell'agente seguito da due punti e l'URL completo dell'ubicazione di tale jar dell'agent. Ad esempio:
```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```
{: #codeblock}
     * Alla fine dell'URL, il nome del file jar deve essere **dynatrace-agent-version-unix.jar**. La versione deve essere **6.3.0** o **6.3.0_nnnn** dove nnnn è l'identificativo della versione micro. Tieni presente che potrebbe essere differente dal nome del file jar che Dynatrace utilizza e quindi potrebbe essere necessario ridenominare il jar.       
     * Il file **dynatrace-agent-6.3.0-unix.jar** deve essere disponibile nell'ubicazione specificata nel file index.yml. L'ubicazione per il file jar e il file index.yml può essere la stessa directory.

## Configurazione del raccoglitore Dynatrace

Successivamente, avrai bisogno di configurare un raccoglitore Dynatrace che sia accessibile dall'agent Dynatrace. Devi inoltre creare un servizio fornito dall'utente per trasmettere le informazioni per l'agent Dynatrace per stabilire una connessione con il raccoglitore Dynatrace. Consulta [Dynatrace Architecture](https://community.dynatrace.com/community/display/DOCDT63/Architecture) per comprendere meglio le relazioni tra i componenti Dynatrace.

  1. Configura un raccoglitore Dynatrace.
    * Consulta [Dynatrace community website](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace) per istruzioni su come scaricare e configurare il raccoglitore Dynatrace.
    * Verifica che il raccoglitore sia configurato in un'ubicazione che sia accessibile dall'agent Dynatrace in esecuzione con la tua applicazione in Bluemix.
  2. Crea un servizio fornito dall'utente che punta al raccoglitore Dynatrace in esecuzione. <b>NOTA</b> il nome del servizio fornito per l'utente deve contenere <b>dynatrace</b>.  Ad esempio, utilizzare il seguente comando:
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
```
{: #codeblock}
In questo esempio, my-dynatrace-collector è il nome fornito al servizio, DynatraceCollectorIPaddress è l'indirizzo IP del raccoglitore Dynatrace che hai configurato e profile è il nome del profilo Dynatrace facoltativo associato a questa applicazione monitorata. Il valore predefinito è Monitoring. Puoi specificare i parametri facoltativi come nel seguente esempio.
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                          "options" : {
                                                       "dynatrace-parameter-1": "value",
                                                       "dynatrace-parameter-2": "value"
                                         }}'
```
{: #codeblock}
Consulta [Agent Setting section of Agent Configuration](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration) nel sito Web della community Dynatrace per ulteriori informazioni sulle opzioni disponibili. Ad esempio, utilizzando l'opzione exclude, puoi escludere le classi dal monitoraggio di Dynatrace. Consulta [DynaTrace Agent Framework](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md) per ulteriori dettagli sul servizio fornito dall'utente.
  3. Dopo aver eseguito il push della tua applicazione a Bluemix, esegui il bind del servizio fornito dall'utente che hai creato per l'applicazione. Ad esempio, utilizza il comando
```
    $ cf bs myApp my-dynatrace-service
```
**Nota**: devi ripreparare la tua applicazione dopo il bind del servizio.

## Configurazione dell'applicazione Liberty
{: #configuring_liberty_app}

L'applicazione Liberty che desideri monitorare deve essere configurata per individuare il server che ospita il jar dell'agent che hai precedentemente configurato. Puoi configurare l'applicazione con la variabile di ambiente **JBP_CONFIG_DYNATRACEAGENT**. La variabile di ambiente **JBP_CONFIG_DYNATRACEAGENT** indica che il pacchetto di build da cui scaricare l'agent Dynatrace. Per impostare la variabile di ambiente, completa la seguente procedura:
<ol>
   <li> Imposta la variabile **JBP_CONFIG_DYNATRACEAGENT** in modo che abbia il valore
   *"repository_root: URL_of_server_hosting_index.yml"*. Ad esempio, dopo aver eseguito il push della tua applicazione immetti il seguente comando:
```
    $ cf se myApp JBP_CONFIG_DYNATRACEAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
```
{: #codeblock}
  In questo esempio, *my-dynatrace-agent-host.mybluemix.net* è l'URL del file index.yml ospitato dal server che hai precedentemente configurato.
  </li>
  <li> Dopo aver impostato la variabile di ambiente, riprepara la tua applicazione. staging_task.log per la tua applicazione Liberty emette un messaggio che indica che hai scaricato con successo l'agent Dynatrace dal tuo server che ospita l'agent. Ad esempio:
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: #codeblock}
</li>
<li>Per visualizzare staging_task.log, immetti il seguente comando:
```
    $ cf files myAppName logs/staging_task.log
```
{: #codeblock}
</li>
</ol>

# rellinks
## general
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
