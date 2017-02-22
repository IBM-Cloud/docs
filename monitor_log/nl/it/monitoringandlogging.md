---

copyright:
  years: 2015, 2017

lastupdated: "2017-01-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Monitoraggio e registrazione con Cloud Foundry
{: #monitoringandlogging}


Mediante il monitoraggio delle tue applicazioni e la revisione dei log, puoi seguire l'esecuzione dell'applicazione e il flusso di dati per comprendere al meglio la tua distribuzione. Inoltre, puoi ridurre il tempo e lo sforzo necessari per individuare e correggere eventuali problemi.
{:shortdesc}

Le applicazioni {{site.data.keyword.Bluemix}} possono essere applicazioni a più istanze ampiamente distribuite e l'esecuzione della tua applicazione e dei suoi dati può essere condivisa tra diversi servizi. In questo ambiente complesso, il processo di monitoraggio delle applicazioni e di revisione dei log è importante per gestire le tue applicazioni.

## Monitoraggio e registrazione di applicazioni Cloud Foundry
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}} è dotato di un meccanismo di registrazione integrato per produrre file di log per le applicazioni in esecuzione. Nei log, puoi visualizzare gli errori, le avvertenze e i messaggi informativi che vengono generati per la tua applicazione. Inoltre, puoi configurare la tua applicazione in modo da scrivere i messaggi di log nel file di log. Per ulteriori informazioni sui formati e sulla visualizzazione dei log, vedi [Registrazione per le applicazioni eseguite su Cloud Foundry](#logging_for_bluemix_apps).

Il monitoraggio ti consente di visualizzare e controllare la distribuzione della tua applicazione. Con il monitoraggio, puoi realizzare le seguenti attività:

* Raccogliere e monitorare informazioni sulle prestazioni relative a istanze di applicazione e verificare che siano funzionali.
* Acquisire informazioni approfondite sulle operazioni dell'applicazione, ad esempio, individuare i potenziali colli di bottiglia o se sono necessari degli aggiornamenti.
* Stimare i costi e l'utilizzo delle risorse.

Per le operazioni stabili delle tue distribuzioni sulla piattaforma {{site.data.keyword.Bluemix_notm}}, desideri rilevare tempestivamente i problemi e determinarne le cause in modo efficiente. Per raggiungere questo obiettivo, tieni a mente la risoluzione dei problemi quando progetti le tue applicazioni e utilizza i servizi o gli strumenti per il monitoraggio e la registrazione quando la tua applicazione viene distribuita a {{site.data.keyword.Bluemix_notm}}.

### Monitoraggio di applicazioni in esecuzione su Cloud Foundry
{: #monitoring_bluemix_apps}

Se utilizzi l'infrastruttura Cloud Foundry per eseguire le tue applicazioni su {{site.data.keyword.Bluemix_notm}}, puoi tenere sotto controllo le informazioni sulle prestazioni, ad esempio lo stato di integrità, l'utilizzo delle risorse e le metriche di traffico. Mediante queste informazioni, puoi prendere decisioni o agire di conseguenza.

Per monitorare le applicazioni {{site.data.keyword.Bluemix_notm}}, utilizza uno dei seguenti metodi:

* Servizi {{site.data.keyword.Bluemix_notm}}. Monitoring and Analytics offre un servizio che ti permette di monitorare le prestazioni della tua applicazione. Inoltre, questo servizio fornisce anche delle funzioni analitiche come l'analisi dei log. Per ulteriori informazioni, vedi [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate).
* Opzioni di terze parti. Ad esempio, [New Relic
![icona link esterno](../icons/launch-glyph.svg)](http://newrelic.com/){:new_window}.

### Registrazione per le applicazioni in esecuzione su Cloud Foundry
{: #logging_for_bluemix_apps}

I file di log vengono creati automaticamente quando utilizzi l'infrastruttura Cloud Foundry per eseguire le tue applicazioni su {{site.data.keyword.Bluemix_notm}}. Quando riscontri errori in qualsiasi fase, dalla distribuzione al runtime, puoi controllare i log alla ricerca di indizi che possano aiutarti a risolvere il problema.


<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



### Formato e conservazione dei log
{: #log_format}

Nelle applicazioni {{site.data.keyword.Bluemix_notm}} Cloud Foundry pubbliche, i dati dei log vengono memorizzati per 7 giorni per impostazione predefinita.

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

### Visualizzazione dei log
{: #viewing_logs}

Puoi visualizzare i log delle tue applicazioni Cloud Foundry in quattro punti:

  * Dashboard {{site.data.keyword.Bluemix_notm}}
  * Il
  dashboard
  * Interfaccia riga di comando
  * Host di log esterni

#### Visualizzazione dei log dal dashboard {{site.data.keyword.Bluemix_notm}}
{: #viewing_logs_UI}

Per visualizzare i log di distribuzione o di runtime, completa la seguente procedura:
1. Accedi a {{site.data.keyword.Bluemix_notm}}, quindi fai clic sul tile della tua applicazione. Viene visualizzata la pagina dei dettagli dell'applicazione. .
2. Nella barra di navigazione, fai clic su **Log**.

Nella console **Log**, puoi visualizzare in tempo reale i log recenti riguardanti la tua applicazione o le parti finali dei log. Inoltre, puoi filtrare i log in base al canale e al tipo di log.

**Nota:** i log non vengono conservati dopo gli arresti anomali dell'applicazione e tra varie distribuzioni.


#### Visualizzazione dei log dal dashboard Kibana
{: #viewing_logs_Kibana}

Crea un dashboard personalizzato per visualizzare, in modo creativo e semplice, i log per le applicazioni in esecuzione in uno spazio.

1. Apri [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) per accedere all'interfaccia utente Kibana.
2. Seleziona la scheda **Kibana 3**.
3. Se non visualizzi alcun log, modifica il selezionatore di tempo nell'intestazione.
4. Salva il dashboard come un nuovo dashboard.
  1. Nella barra degli strumenti, fai clic sull'icona **Salva**.
  2. Immetti un nome per il dashboard.
  3. Accanto al nome campo, fai clic sull'icona **Salva**.

Per ulteriori informazioni sulla personalizzazione di un dashboard Kibana, consulta [questo post del blog ![icona link esterno](../icons/launch-glyph.svg)](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} o la documentazione [Kibana ![icona link esterno](../icons/launch-glyph.svg)](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.


#### Visualizzazione dei log dall'interfaccia riga di comando
{: #viewing_logs_cli}

Scegli una delle seguenti opzioni per visualizzare i log dall'interfaccia riga di comando:

<ul>
<li>Accodamento dei log quando distribuisci le applicazioni.
<p>Utilizza il comando **cf logs** per visualizzare i log dalla tua applicazione e dai componenti di sistema che interagiscono con la tua applicazione quando distribuisci le applicazioni a {{site.data.keyword.Bluemix_notm}}. Nell'interfaccia riga di comando cf puoi immettere i seguenti comandi. Per ulteriori informazioni sui log cf, vedi <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target=" _blank">Log Types and Their Messages in Cloud Foundry <img src="../icons/launch-glyph.svg" alt="icona link esterno"></a> </p>
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

<dl>
<dt><strong>buildpack.log</strong></dt>
<dd>
<p>Questo file di log registra eventi informativi accurati per il
debug. Puoi utilizzare il log per risolvere problemi relativi all'esecuzione dei pacchetti di
build.</p>
<p>Per generare dei dati nel file <span class="ph filepath">buildpack.log</span>, devi abilitare la traccia del pacchetto di build utilizzando il seguente comando:
   <pre class="pre">cf set-env <var class="keyword varname">nomeapplicazione</var> JBP_LOG_LEVEL DEBUG</pre>
</p>
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


**Nota:** per informazioni su come abilitare la registrazione dell'applicazione, vedi [Debug degli errori di runtime](/docs/debug/index.html#debugging-runtime-errors).

#### Visualizzazione dei log dagli host esterni
{: #viewing_logs_external}


Alla generazione dei log, trascorso qualche istante puoi visualizzare i messaggi del tuo host log esterno simili ai messaggi che visualizzi dall'interfaccia utente {{site.data.keyword.Bluemix_notm}} o dall'interfaccia riga di comando cf.  In caso di più istanze della tua applicazione, i log vengono aggregati e puoi visualizzare tutti i log riguardanti la tua applicazione. Inoltre, i log vengono conservati anche dopo gli arresti anomali dell'applicazione e tra varie distribuzioni.

**Nota:** i log che vedi nell'interfaccia riga di comando non sono in formato syslog e potrebbero non corrispondere esattamente ai messaggi visualizzati nel tuo host log esterno.




### Filtraggio dei log
{: #filtering_logs}

Per visualizzare i log che ti interessano o per escludere i contenuti che non vuoi visualizzare, puoi utilizzare il comando **cf logs** con le opzioni di filtro come **cut** e **grep** nell'interfaccia riga di comando cf.

* Per visualizzare solo una parte dei log, anziché i log dettagliati, utilizza l'opzione **cut**. Ad esempio, per visualizzare le informazioni su componente e messaggio, utilizza il seguente comando:
```
cf logs appname --recent | cut -c 29-40,46-
```

Per ulteriori informazioni sull'opzione **cut**, immetti cut --help.
* Per visualizzare le voci di log che contengono determinate parole chiave, utilizza l'opzione **grep**. Ad esempio, per visualizzare le voci di log che contengono la parola chiave `[APP`, puoi utilizzare il seguente comando:

```
cf logs appname --recent | grep '\[App'
```
Per ulteriori informazioni sull'opzione **grep**, immetti `grep --help`.



### Configurazione di host log esterno
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} conserva in memoria una quantità limitata di informazioni di log. Quando si registrano le informazioni, i dati precedenti vengono sostituiti con le informazioni più recenti. Per conservare tutte le informazioni di log, puoi salvare i tuoi log in un log host esterno, quale un servizio di gestione log di terze parti o un altro host.

Per trasmettere i log dalla tua applicazione e dal sistema a un host log esterno, completa la seguente procedura:

  1. Determina l'endpoint di registrazione.

	 Puoi inviare i log a un aggregatore di log di terze parti, quale ad esempio Papertrail, Splunk o Sumologic. Puoi anche inviare i log a un host syslog, un host syslog crittografato con TLS (Transport Layer Security) o un endpoint HTTPS POST. I metodi per ottenere gli endpoint di registrazione variano per i diversi host log.

  2. Crea un'istanza del servizio fornito dall'utente.

	 Utilizza il comando `cf create-user-provided-service` (o `cups`, una versione breve del comando) per creare un'istanza del servizio fornita dall'utente:
	 ```
	 cf create-user-provided-service <nome_servizio> -l <endpoint_registrazione>
	 ```
	 &lt;service_name&gt;

	 Il nome dell'istanza di servizio fornita dall'utente.

	 &lt;endpoint_registrazione&gt;

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
	 cf bind-service <appname> <nome_servizio>
	 ```
	 &lt;appname&gt;

	 Il nome della tua applicazione.

	 &lt;nome_servizio&gt;

	 Il nome dell'istanza di servizio fornita dall'utente.

  4. Riprepara l'applicazione.
     Immetti `cf restage appname` per rendere effettive le modifiche.


### Esempio: trasmissione di log di applicazioni Cloud Foundry a Splunk
{: #splunk}

In questo esempio, uno sviluppatore di nome Jane crea un server virtuale utilizzando dei server virtuali IBM beta e l'immagine Ubuntu.  Jane tenta di trasmettere i log dell'applicazione Cloud Foundry da {{site.data.keyword.Bluemix_notm}} a Splunk.

  1. Per iniziare, Jane configura Splunk.

     a. Jane scarica Splunk Light dal [sito di download di Splunk Light
![icona link esterno](../icons/launch-glyph.svg)](https://www.splunk.com/en_us/download/splunk-light.html){:new_window}, quindi lo installa utilizzando il seguente comando. Il software viene installato su */opt/splunk*.

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane installa e applica le patch al componente aggiuntivo con tecnologia syslog RFC5424 da integrare con {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni sulle istruzioni di installazione del componente aggiuntivo, consulta la [Guida Cloud Foundry
![icona link esterno](../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jane installa il componente aggiuntivo utilizzando i seguenti comandi:

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        Quindi, Jane applica la patch al componente aggiuntivo sostituendo */opt/splunk/etc/apps/rfc5424/default/transforms.conf* con un nuovo file *transforms.conf* che comprende il testo seguente:

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. Una volta impostato Splunk, Jane deve aprire alcune porte sulla macchina Ubuntu per accettare lo scarico syslog in entrata (porta 5140) e Splunk Web UI (porta 8000), poiché il firewall del server virtuale {{site.data.keyword.Bluemix_notm}} è configurato con valori predefiniti.

	    **Nota:** la conferma iptable viene effettuata in questo punto per gli scopi di valutazione di Jane ed è temporanea. Per configurare l'impostazione del
firewall nel server virtuale Bluemix produttivo, vedi la documentazione [Network Security Groups
![icona link esterno](../icons/launch-glyph.svg)](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} contenente informazioni dettagliate.


	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   Quindi, Jane esegue Splunk utilizzando il seguente comando:

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane configura le impostazioni di Splunk in modo da accettare lo scarico syslog da {{site.data.keyword.Bluemix_notm}}. Deve creare un input di dati per lo scarico syslog.

     a. Dall'interfaccia Web Splunk, Jane fa clic su **Dati > Input di dati**. Viene visualizzato un elenco di tipi di input supportati da Splunk.

     b. Seleziona **TCP**, perché lo scarico syslog utilizza il protocollo TCP.

     c. Nel riquadro **TCP**, immette **5140** all'interno del campo **Porta**, lascia gli altri campi vuoti e fa clic su **Avanti**.

     d. Dall'elenco **Tipo di origine**, seleziona **Non categorizzato > rfc5424_syslog**.

     e. Per il tipo di **Metodo**, seleziona **IP**.

     f. Nel campo **Indice**, Jane fa clic su **Crea un nuovo indice**. Dopo aver rinominato il nuovo indice "bluemix", fa clic su **Salva**.

     g. Infine, nella finestra **Riesamina**, Jane conferma che l'impostazione è corretta e fa clic su **Invia** per abilitare l'input di dati.

  3. In {{site.data.keyword.Bluemix_notm}}, Jane crea un servizio di scarico syslog e lo collega a un'applicazione.

     a. Jane crea un servizio di scarico syslog utilizzando il seguente comando dalla cli cf:

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Nota:** *dummyhost* non è il nome reale. Viene utilizzato per nascondere il nome host effettivo.

     b. Jane associa il servizio di scarico syslog a un'applicazione nel proprio spazio, quindi riprepara l'applicazione.

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane testa l'applicazione, quindi digita la seguente stringa di query nell'interfaccia Web di Splunk:

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane visualizza un flusso di log nella propria interfaccia Web Splunk. Sebbene la versione di Splunk installata da Jane sia la Splunk Light, può comunque conservare 500 MB di registri al giorno.

## Registrazione per le applicazioni Cloud Foundry in {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}
{: #hybrid_apps_logs_ov}


In {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, le applicazioni Cloud Foundry sono fornite con la registrazione integrata. Puoi rivedere i dati raccolti dalle tue applicazioni nella console {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Le applicazioni Cloud Foundry utilizzano il  Loggregator per monitorare e inoltrare i log dall'esterno dell'applicazione. Non devi installare gli agent nell'applicazione.

### Requisiti hardware


| **Requisito** |    **1 nodo**     | **3 nodi per l'alta disponibilità** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| Memoria | 80 GB | 240 GB |
| Memoria locale | 2.98 TB | 8.94 TB |
{: caption="Table 1. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

### Configurazione

In {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, i log sono attivi per tutte le applicazioni per impostazione predefinita. Per visualizzare le informazioni sulla lettura dei log standard, consulta [Registrazione per le applicazioni in esecuzione su Cloud Foundry](#logging_for_bluemix_apps). In aggiunta, può essere abilitata la registrazione avanzata negli ambienti {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}.

* Per confermare che la registrazione avanzata è abilitata nei tuoi ambienti {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, segui le istruzioni in [Visualizzazione dei log](#hybrid_apps_logs_dash). Se non visualizzi il pulsante **Vista avanzata**, questa funzione non è abilitata.

* Per aggiungere la registrazione avanzata al tuo ambiente, segui le istruzioni nella documentazione [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) o [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local).

### Conservazione log

Nelle applicazioni Cloud Foundry {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}, i dati dei log vengono memorizzati per 30 giorni per impostazione predefinita.

## Visualizzazione dei log per le applicazioni Cloud Foundry in {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}
{: #hybrid_apps_logs_dash}

Puoi rivedere i log per le applicazioni che stai eseguendo in {{site.data.keyword.Bluemix_dedicated_notm}} e {{site.data.keyword.Bluemix_local_notm}}.
{:shortdesc}

Per visualizzare i tuoi log delle applicazioni, segui queste istruzioni.
1. Seleziona un'applicazione in esecuzione.
2. Fai clic su **Log**. Nella vista **Log**, puoi visualizzare i log dalla tua applicazione in esecuzione.
4. Fai clic sul pulsante **Vista avanzata**. **Vista avanzata** mostra una vista più dettagliata dei log utilizzando Kibana, uno strumento di visualizzazione che utilizza i log e i dati con data/ora per creare le visualizzazioni personalizzate. Per ulteriori informazioni sull'utilizzo della vista avanzata, consulta la documentazione di [Kibana ![icona link esterno](../icons/launch-glyph.svg)](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.

Successivamente, puoi personalizzare un dashboard Kibana. Per ulteriori informazioni, consulta [Personalizzazione della visualizzazione del log nel dashboard Kibana](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom).
