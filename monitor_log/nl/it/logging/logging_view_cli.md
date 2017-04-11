---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisi dei log dell'applicazione CF dalla CLI
{: #analyzing_logs_cli}

In {{site.data.keyword.Bluemix}}, puoi visualizzare, filtrare e analizzare i log attraverso l'interfaccia riga di comando utilizzando il comando **cf logs**. Utilizza la riga comandi per gestire i log a livello di programmazione. 
{:shortdesc}

Utilizza il comando **cf logs** per visualizzare i log da un'applicazione Cloud Foundry e dai componenti di sistema che interagiscono con essa quando la distribuisci in {{site.data.keyword.Bluemix_notm}}. Il comando **cf logs** visualizza i flussi di log STDOUT e STDERR di un'applicazione Cloud Foundry.

Per visualizzare i log che ti interessano o per escludere i contenuti che non vuoi visualizzare, puoi utilizzare il comando **cf logs** con le opzioni di filtro come **cut** e **grep** nell'interfaccia riga di comando cf:

* Per visualizzare i log di un'applicazione Cloud Foundry, vedi [Visualizzazione dei log per un'applicazione Cloud Foundry](logging_view_cli.html#full_log_cli).
* Per visualizzare i record di log più recenti di un'applicazione Cloud Foundry, vedi [Visualizzazione delle ultime voci di log per un'applicazione Cloud Foundry](logging_view_cli.html#tailing_log_cli).
* Per visualizzare i record di log di un'applicazione Cloud Foundry in uno specifico intervallo di tempo, vedi [Visualizzazione di una sezione dei log](logging_view_cli.html#partial_log_cli).
* Per visualizzare le voci di log di un'applicazione Cloud Foundry che contengono specifiche parole chiave, vedi [Visualizzazione di voci di log contenenti determinate parole chiave](logging_view_cli.html#partial_by_keyword_log_cli).


## Visualizzazione dei log per un'applicazione Cloud Foundry
{: #full_log_cli}

Per visualizzare tutti i log disponibili per un'applicazione Cloud Foundry, completa la seguente procedura:

1. Apri un terminale e accedi a {{site.data.keyword.Bluemix}}.

2. Nella riga di comando, immetti il seguente comando per visualizzare tutti i log:

   <pre class="pre screen"><code>cf logs <var class="keyword varname">nomeapplicazione</var></code></pre>
   
   
## Visualizzazione delle ultime voci di log per un'applicazione Cloud Foundry
{: #tailing_log_cli}

Per visualizzare i log più recenti disponibili per un'applicazione Cloud Foundry, completa la seguente procedura:

1. Apri un terminale e accedi a {{site.data.keyword.Bluemix}}.

2. Nella riga di comando, immetti il seguente comando per visualizzare tutti i log:

     <pre class="pre screen"><code>cf logs <var class="keyword varname">nomeapplicazione</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">Suggerimento:</span> quando esegui il comando <span class="keyword cmdname">cf push</span> o <span class="keyword cmdname">cf
start</span> in una finestra della riga di comando, puoi immettere <samp class="ph codeph">cf
logs nomeapplicazione --recent</samp> in un'altra finestra di riga di comando per visualizzare
i log in tempo reale. </div>


## Visualizzazione di una sezione di un log Cloud Foundry
{: #partial_log_cli}

Per visualizzare una parte dei log disponibili per un'applicazione Cloud Foundry all'interno di un intervallo di tempo, completa la seguente procedura:

1. Apri un terminale e accedi a {{site.data.keyword.Bluemix}}.

2. Nella riga di comando, immetti il seguente comando per visualizzare tutti i log:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent  | cut -c 29-40,46-</code></pre>
    
    Per ulteriori informazioni sull'opzione **cut**, immetti **cut --help**.


## Visualizzazione di voci di log contenenti determinate parole chiave
{: #partial_by_keyword_log_cli}

Per visualizzare le voci di log che contengono determinate parole chiave per un'applicazione Cloud Foundry, completa la seguente procedura:

1. Apri un terminale e accedi a {{site.data.keyword.Bluemix}}.

2. Nella riga di comando, immetti il seguente comando per visualizzare tutti i log:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent | grep '<var class="keyword varname">keyword</var>'</code></pre>
    

Ad esempio, per visualizzare le voci di log che contengono la parola chiave **APP**, puoi utilizzare il seguente comando:

<pre class="pre screen"><code>cf logs appname --recent | grep '\[App'
</code></pre>

Per ulteriori informazioni sull'opzione **grep**, immetti **grep --help**.


## Log dell'applicazione Cloud Foundry
{: #cf_app_logs_cli}

I seguenti log sono disponibili per un'applicazione Cloud Foundry dopo averla distribuita in {{site.data.keyword.Bluemix}}:

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>Questo file di log registra eventi informativi accurati per il
debug. Puoi utilizzare il log per risolvere problemi relativi all'esecuzione dei pacchetti di
build.</p>

<p>Per generare dei dati nel file <span class="ph filepath">buildpack.log</span>, devi abilitare la traccia del pacchetto di build utilizzando il seguente comando:</p>

   <pre class="pre">cf set-env <var class="keyword varname">nomeapplicazione</var> JBP_LOG_LEVEL DEBUG</pre>
   
<p>Per visualizzare questo log, immetti il seguente comando:</p>

    <pre class="pre">cf files <var class="keyword varname">nomeapp</var> app/.buildpack-diagnostics/buildpack.log</pre>

</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>Questo file di log registra i messaggi dopo i passi principali dell'attività di
preparazione. Puoi utilizzare questo log per risolvere i problemi relativi alla
preparazione.</p>

<p>Per visualizzare questo log, immetti il seguente comando:</p>

    <pre class="pre">cf files <var class="keyword varname">nomeapp</var> logs/staging_task.log</pre>
</dd>
</dl>

**Nota:** per informazioni su come abilitare la registrazione dell'applicazione, vedi [Debug degli errori di runtime](/docs/debug/index.html#debugging-runtime-errors).

