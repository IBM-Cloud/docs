{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Monitoraggio e registrazione
{: #monitoringandlogging}

*Ultimo aggiornamento: 8 dicembre 2015*

Mediante il monitoraggio delle tue applicazioni e la revisione dei log, puoi seguire l'esecuzione dell'applicazione e il flusso di dati per comprendere al meglio la tua distribuzione. Inoltre, puoi ridurre il tempo e lo sforzo necessari per individuare e correggere eventuali problemi.
{:shortdesc}

Le applicazioni {{site.data.keyword.Bluemix}} possono essere applicazioni a più istanze ampiamente distribuite e l'esecuzione della tua applicazione e dei suoi dati può essere condivisa tra diversi servizi. In questo ambiente complesso, il processo di monitoraggio delle applicazioni e di revisione dei log è importante per gestire le tue applicazioni.

{{site.data.keyword.Bluemix_notm}} è dotato di un meccanismo di registrazione integrato per produrre file di log per le applicazioni in esecuzione. Nei log, puoi visualizzare gli errori, le avvertenze e i messaggi informativi che vengono generati per la tua applicazione. Inoltre, puoi configurare la tua applicazione in modo da scrivere i messaggi di log nel file di log. Per ulteriori informazioni sui formati e sulla visualizzazione dei log, vedi [Registrazione per le applicazioni {{site.data.keyword.Bluemix_notm}}](#logging_for_bluemix_apps).

Il monitoraggio ti consente di visualizzare e controllare la distribuzione della tua applicazione. Con il monitoraggio, puoi realizzare le seguenti attività:

* Raccogliere e monitorare informazioni sulle prestazioni relative a istanze di applicazione e verificare che siano funzionali.
* Acquisire informazioni approfondite sulle operazioni dell'applicazione, ad esempio, individuare i potenziali colli di bottiglia o se sono necessari degli aggiornamenti.
* Stimare i costi e l'utilizzo delle risorse.

Per le operazioni stabili delle tue distribuzioni sulla piattaforma {{site.data.keyword.Bluemix_notm}}, desideri rilevare tempestivamente i problemi e determinarne le cause in modo efficiente. Per raggiungere questo obiettivo, tieni a mente la risoluzione dei problemi quando progetti le tue applicazioni e utilizza i servizi o gli strumenti per il monitoraggio e la registrazione quando la tua applicazione viene distribuita a {{site.data.keyword.Bluemix_notm}}.

##Monitoraggio di applicazioni in esecuzione su Cloud Foundry
{: #monitoring_bluemix_apps}

Se utilizzi l'infrastruttura Cloud Foundry per eseguire le tue applicazioni su {{site.data.keyword.Bluemix_notm}}, puoi tenere sotto controllo le informazioni sulle prestazioni, ad esempio lo stato di integrità, l'utilizzo delle risorse e le metriche di traffico. Mediante queste informazioni, puoi prendere decisioni o agire di conseguenza.

Per monitorare le applicazioni {{site.data.keyword.Bluemix_notm}}, utilizza uno dei seguenti metodi:

* Servizi {{site.data.keyword.Bluemix_notm}}. Monitoring and Analytics offre un servizio che ti permette di monitorare le prestazioni della tua applicazione. Inoltre, questo servizio fornisce anche delle funzioni analitiche come l'analisi dei log. Per ulteriori informazioni, vedi [Monitoring and Analytics](../services/monana/index.html).
* Opzioni di terze parti. Ad esempio, [New Relic](http://newrelic.com/){:new_window}.

##Registrazione per le applicazioni in esecuzione su Cloud Foundry
{: #logging_for_bluemix_apps}

I file di log vengono creati automaticamente quando utilizzi l'infrastruttura Cloud Foundry per eseguire le tue applicazioni su {{site.data.keyword.Bluemix_notm}}. Puoi visualizzare i log sia dal Dashboard {{site.data.keyword.Bluemix_notm}} che dall'interfaccia riga di comando cf. Puoi anche filtrare i log in modo da visualizzare solo le parti che ti interessano.

###Formato dei log
{: #log_format}

I log per le applicazioni {{site.data.keyword.Bluemix_notm}} vengono visualizzati in un formato fisso, simile al seguente modello:

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

Ogni voce di log contiene quattro campi. Fai riferimento al seguente elenco per una breve descrizione di ciascun campo:

<dl>
<dt><strong>Timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>Colonne: 1 - 27</p>
<p>L'ora dell'istruzione di log. La data e ora è definita fino al millisecondo.</p>
</dd>

<dt><strong>Componente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Colonne: 29 - 40</p>
<p>Il componente che produce i log. Il seguente elenco fornisce la definizione per tutti i componenti:</p>

<dl>
<dt><strong>APP</strong></dt>
<dd>Applicazione. Il componente APP è seguito da una barra e da un numero che indica l'istanza dell'applicazione. Se 0 è la prima istanza, 1 sarà la seconda e così via.</dd>

<dt><strong>API</strong></dt>
<dd>API Cloud Foundry.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent.</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator.</dd>

<dt><strong>RTR</strong></dt>
<dd>Router.</dd>

<dt><strong>STG</strong></dt>
<dd>Preparazione.</dd>
</dl>
</dd>

<dt><strong>Flusso</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Colonne: 42 - 44</p>
<p>Il flusso in cui viene scritto il messaggio di log. <samp class="ph codeph">OUT</samp> si riferisce al flusso <samp class="ph codeph">stdout</samp> e <samp class="ph codeph">ERR</samp> si riferisce al flusso <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>Messaggio</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Messaggio</var>&gt;</code></pre>
<p>Colonne: 46 - fine riga</p>
<p>Il messaggio che viene emesso dal componente. Il messaggio varia a seconda dal contesto.</p>
</dd>

</dl>

###Visualizzazione dei log
{: #viewing_logs}

Per visualizzare i log puoi utilizzare il Dashboard {{site.data.keyword.Bluemix_notm}} o l'interfaccia riga di comando.

####VISUALIZZAZIONE DEI LOG DAL DASHBOARD {{site.data.keyword.Bluemix_notm}}

Per visualizzare i log **Distribuzione** o **Runtime**, completa la seguente procedura:
1. Fai clic sul tile della tua applicazione. Viene visualizzata la pagina dei dettagli dell'applicazione.
2. Nella barra di navigazione sinistra, fai clic su **Log**.

####VISUALIZZAZIONE DEI LOG DALL'INTERFACCIA RIGA DI COMANDO

Scegli una delle seguenti opzioni per visualizzare i log dall'interfaccia riga di comando:

<ul>
<li>Accodamento dei log quando distribuisci le applicazioni.
<p>Utilizza il comando **cf logs** per visualizzare i log dalla tua applicazione e dai componenti di sistema che interagiscono con la tua applicazione quando distribuisci le applicazioni a {{site.data.keyword.Bluemix_notm}}. Nell'interfaccia riga di comando cf puoi immettere i seguenti comandi. Per ulteriori informazioni sui log cf, vedi [Log Types and Their Messages in Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.</p>
<dl>
<dt><strong>cf logs <var class="keyword varname">appname</var> --recent</strong></dt>
<dd>Visualizzare i log recenti.</dd>

<dt><strong>cf logs <var class="keyword varname">appname</var></strong></dt>
<dd>Visualizza i log che vengono generati dal momento in cui esegui questo
comando.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Suggerimento:</span> quando esegui il comando <span class="keyword cmdname">cf push</span> o <span class="keyword cmdname">cf
start</span> in una finestra della riga di comando, puoi immettere <samp class="ph codeph">cf
logs appname --recent</samp> in un'altra finestra di riga di comando per visualizzare
i log in tempo reale. </div>
</li>

<li>Visualizzazione dei log dopo la distribuzione delle applicazioni.

<p>Se la registrazione dell'applicazione è abilitata, in caso di problemi con l'applicazione durante il runtime, puoi visualizzare i seguenti log. I log dell'applicazione ti consentono di determinare la causa dell'errore.</p>

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>Questo file di log registra eventi informativi accurati per il
debug. Puoi utilizzare il log per risolvere problemi relativi all'esecuzione dei pacchetti di
build.</p>
<p>Per generare dei dati nel file <span class="ph filepath">buildpack.log</span>, devi abilitare la traccia del pacchetto di build utilizzando il seguente comando:
   <pre class="pre">cf set-env <var class="keyword varname">nomeapplicazione</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
<p>Per visualizzare questo log, immetti il seguente comando:
<pre class="pre">cf files <var class="keyword varname">nomeapp</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>Questo file di log registra i messaggi dopo i passi principali dell'attività di
preparazione. Puoi utilizzare questo log per risolvere i problemi relativi alla
preparazione.</p>
<p>Per visualizzare questo log, immetti il seguente comando:
<pre class="pre">cf files <var class="keyword varname">nomeapp</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Nota:** per informazioni su come abilitare la registrazione dell'applicazione, vedi [Debug degli errori di runtime](../troubleshoot/debugging.html#debug_runtime).

###Filtraggio dei log
{: #filtering_logs}

Per visualizzare i log che ti interessano o per escludere i contenuti che non vuoi visualizzare, puoi utilizzare il comando **cf logs** con le opzioni di filtro come **cut** e **grep** nell'interfaccia riga di comando cf.

* Per visualizzare solo una parte dei log, anziché i log dettagliati, utilizza l'opzione **cut**. Ad esempio, per visualizzare le informazioni su componente e messaggio, utilizza il seguente comando:
```
cf logs appname --recent | cut -c 29-40,46- 
```

Per ulteriori informazioni sull'opzione **grep**, immetti cut --help.
* Per visualizzare le voci di log che contengono determinate parole chiave, utilizza l'opzione **grep**. Ad esempio, per visualizzare le voci di log che contengono la parola chiave [APP, puoi utilizzare il seguente comando:
```
cf logs appname --recent | grep '\[App'
```
Per ulteriori informazioni sull'opzione **grep**, immetti `grep --help`.

###Configurazione della registrazione di terze parti
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} conserva in memoria una quantità limitata di informazioni di log. Quando si registrano le informazioni, i dati precedenti vengono sostituiti con le informazioni più recenti. Per conservare tutte le informazioni di log, puoi salvare i tuoi log in un servizio di gestione log di terze parti.

Per trasmettere i log dalla tua applicazione e dal sistema a un servizio di gestione log di terze parti, completa la seguente procedura:

1. Registra un servizio di gestione log di terze parti.
    
    Puoi utilizzare un qualsiasi servizio di gestione log di terze parti che supporti il [protocollo syslog](http://tools.ietf.org/html/rfc5424){:new_window}, come Papertail, Splunk Storm, SumoLogic e Logentries. Registra un servizio di gestione log di terze parti, quindi configura il servizio per fornire una destinazione per i log in {{site.data.keyword.Bluemix_notm}}. Dopo che hai completato la configurazione, il servizio di solito ti fornisce un URL syslog come destinazione per i tuoi log in {{site.data.keyword.Bluemix_notm}}. Per
informazioni su come configurare i servizi di gestione log di terze parti,
vedi [Configuring Selected Third-Party Log Management Services](http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html){:new_window}.

2. Crea un'istanza del servizio fornito dall'utente.
	
	Per trasmettere i log presenti in {{site.data.keyword.Bluemix_notm}} al servizio di gestione log di terze parti, devi prima creare un'istanza del servizio fornito dall'utente. Utilizza il seguente comando per creare un'istanza del servizio fornito dall'utente, dove nome_servizio è il nome per l'istanza del servizio fornito dall'utente e URL_syslog è l'URL che ottieni dal servizio di registrazione di terze parti.
	
	```
	cf create-user-provided-service <nome_servizio> -l <URL_>
	```
	
3. Esegui il bind dell'istanza del servizio alla tua applicazione.

	Utilizza il seguente comando per eseguire il bind dell'istanza del servizio alla tua applicazione, dove nomeapp è il nome della tua applicazione e nome_servizio è il nome per l'istanza del servizio fornito dall'utente.
	
	```
	cf bind-service nomeapp <nome_servizio>
	```
	
	Successivamente, ti verrà richiesto di preparare nuovamente l'applicazione immettendo cf restage nomeapp per rendere effettive le modifiche. Quando i log vengono generati, puoi visualizzare dei messaggi simili nel servizio di gestione log di terze parti dopo un breve intervallo.

**Nota:** i log che vedi nell'interfaccia riga di comando non sono in formato syslog e potrebbero non corrispondere esattamente ai messaggi visualizzati nei servizi di gestione log di terze parti.
