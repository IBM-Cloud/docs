---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Monitoraggio e registrazione
{: #monitoringandlogging}

*Ultimo aggiornamento: 11 maggio 2016*

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

I file di log vengono creati automaticamente quando utilizzi l'infrastruttura Cloud Foundry per eseguire le tue applicazioni su {{site.data.keyword.Bluemix_notm}}. Quando riscontri errori in qualsiasi fase, dalla distribuzione al runtime, puoi controllare i log alla ricerca di indizi che possano aiutarti a risolvere il problema.

<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



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
<dt><strong>Data/ora</strong></dt>
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

Puoi visualizzare i log delle tue applicazioni Cloud Foundry in tre punti:

  * Dashboard [ {{site.data.keyword.Bluemix_notm}}](#viewing_logs_UI){:new_window}
  * [Interfaccia riga di comando](#viewing_logs_cli){:new_window}
  * [Host log esterni](#thirdparty_logging){:new_window}

#### Visualizzazione dei log dal dashboard {{site.data.keyword.Bluemix_notm}}
{: #viewing_logs_UI}

Per visualizzare i log di distribuzione o di runtime, completa la seguente procedura:
1. Accedi a {{site.data.keyword.Bluemix_notm}}, quindi fai clic sul tile della tua applicazione sul Dashboard. Viene visualizzata la pagina dei dettagli dell'applicazione.
2. Nella barra di navigazione sinistra, fai clic su **Log**.

Nella console **Log**, puoi visualizzare in tempo reale i log recenti riguardanti la tua applicazione o le parti finali dei log. Inoltre, puoi filtrare i log in base al canale e al tipo di log.

**Nota:** i log non vengono conservati dopo gli arresti anomali dell'applicazione e tra varie distribuzioni.



#### Visualizzazione dei log dall'interfaccia riga di comando
{: #viewing_logs_cli}

Scegli una delle seguenti opzioni per visualizzare i log dall'interfaccia riga di comando:

<ul>
<li>Accodamento dei log quando distribuisci le applicazioni.
<p>Utilizza il comando **cf logs** per visualizzare i log dalla tua applicazione e dai componenti di sistema che interagiscono con la tua applicazione quando distribuisci le applicazioni a {{site.data.keyword.Bluemix_notm}}. Nell'interfaccia riga di comando cf puoi immettere i seguenti comandi. Per ulteriori informazioni sui log cf, vedi <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target="_blank">Log Types and Their Messages in Cloud Foundry</a>. </p>
<dl>
<dt><strong>cf logs <var class="keyword varname">nomeapplicazione</var> --recent</strong></dt>
<dd>Visualizzare i log recenti.</dd>

<dt><strong>cf logs <var class="keyword varname">nomeapplicazione</var></strong></dt>
<dd>Visualizza i log che vengono generati dal momento in cui esegui questo
comando.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Suggerimento:</span> quando esegui il comando <span class="keyword cmdname">cf push</span> o <span class="keyword cmdname">cf
start</span> in una finestra della riga di comando, puoi immettere <samp class="ph codeph">cf
logs nomeapplicazione --recent</samp> in un'altra finestra di riga di comando per visualizzare
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


**Nota:** per informazioni su come abilitare la registrazione dell'applicazione, vedi [Debug degli errori di runtime](../debug/index.html#debugging-runtime-errors).




###Filtraggio dei log
{: #filtering_logs}

Per visualizzare i log che ti interessano o per escludere i contenuti che non vuoi visualizzare, puoi utilizzare il comando **cf logs** con le opzioni di filtro come **cut** e **grep** nell'interfaccia riga di comando cf.

* Per visualizzare solo una parte dei log, anziché i log dettagliati, utilizza l'opzione **cut**. Ad esempio, per visualizzare le informazioni su componente e messaggio, utilizza il seguente comando:
```
cf logs nomeapplicazione --recent | cut -c 29-40,46- 
```

Per ulteriori informazioni sull'opzione **grep**, immetti cut --help.
* Per visualizzare le voci di log che contengono determinate parole chiave, utilizza l'opzione **grep**. Ad esempio, per visualizzare le voci di log che contengono la parola chiave [APP, puoi utilizzare il seguente comando:
```
cf logs nomeapplicazione --recent | grep '\[App'
```
Per ulteriori informazioni sull'opzione **grep**, immetti `grep --help`.



### Configurazione di host log esterno
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} conserva in memoria una quantità limitata di informazioni di log. Quando si registrano le informazioni, i dati precedenti vengono sostituiti con le informazioni più recenti. Per conservare tutte le informazioni di log, puoi salvare i tuoi log in un log host esterno, quale un servizio di gestione log di terze parti o un altro host.

Per trasmettere i log dalla tua applicazione e dal sistema a un host log esterno, completa la seguente procedura:

  1. Determina l'endpoint di registrazione. 
     
	 Puoi inviare i log a un aggregatore di log di terze parti, quale ad esempio Papertrail, Splunk o Sumologic. Puoi anche inviare i log a un host syslog, un host syslog crittografato con TLS (Transport Layer Security) o un endpoint HTTPS POST. I metodi per ottenere gli endpoint di registrazione variano per i diversi host log.

  2. Crea un'istanza del servizio fornito dall'utente.
     
	 Utilizza il comando ``"cf create-user-provided-service"`` (o ```cups``, una versione breve del comando) per creare un'istanza del servizio fornita dall'utente:
```
	 cf create-user-provided-service <nome_servizio> -l <endpoint_registrazione>
```
	 **nome_servizio**
	 
	 Il nome dell'istanza di servizio fornita dall'utente.
	 
	 **endpoint_registrazione**
	 
	 L'endpoint di registrazione a cui invia i log {{site.data.keyword.Bluemix_notm}}. Fai riferimento alla seguente tabella per sostituire *endpoint_registrazine* con il tuo valore:
	 
	 <table>
     <thead>
     <tr>
     <th>Endpoint_registrazione</th>
     <th>Comando</th>
	 <th>Note</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog host</td>
     <td>`cf cups my-logs -l syslog://HOST:PORTA`</td>
	 <td>Ad esempio, per consentire la registrazione in Papertrail, immetti `cf cups my-logs -l syslog://<papertrail-url>`. Sostituisci `<papertrail-url>` con l'URL del tuo endpoint di registrazione proveniente da Papertrail.</td>
     </tr>
	 <tr>
     <td>syslog-tls host</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORTA`</td>
	 <td>Il certificato deve essere garantito da un'autorità di certificazione. Non utilizzare certificati autofirmati.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORTA`</td>
	 <td>Questo endpoint deve trovarsi sull'Internet pubblico e deve essere accessibile da {{site.data.keyword.Bluemix_notm}}</td>
     </tr>
     </tbody>
     </table>	
  3. Esegui il bind dell'istanza del servizio alla tua applicazione.

	 Utilizza il seguente comando per eseguire il bind dell'istanza del servizio alla tua applicazione: 
	
	 ```
	 cf bind-service nomeapp <nome_servizio>
```
	 **nomeapplicazione**
	 
	 Il nome della tua applicazione.
	 
	 **nome_servizio**
	 
	 Il nome dell'istanza di servizio fornita dall'utente.
	 
  4. Riprepara l'applicazione. 
     Digita ```cf restage nomeapplicazione``` per rendere effettive le modifiche. 

#### Visualizzazione dei log dagli host esterni
{: #viewing_logs_external}

	 
Alla generazione dei log, trascorso qualche istante puoi visualizzare i messaggi del tuo host log esterno simili ai messaggi che visualizzi dall'interfaccia utente {{site.data.keyword.Bluemix_notm}} o dall'interfaccia riga di comando cf.  In caso di più istanze della tua applicazione, i log vengono aggregati e puoi visualizzare tutti i log riguardanti la tua applicazione. Inoltre, i log vengono conservati anche dopo gli arresti anomali dell'applicazione e tra varie distribuzioni.

**Nota:** i log che vedi nell'interfaccia riga di comando non sono in formato syslog e potrebbero non corrispondere esattamente ai messaggi visualizzati nel tuo host log esterno. 


