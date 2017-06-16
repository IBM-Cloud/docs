---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Caricamento della tua applicazione

Dopo che hai eseguito l'accesso a {{site.data.keyword.Bluemix}}, puoi caricare la tua applicazione con il comando `bluemix app push`.
{:shortdesc}

Prima di iniziare:
  1. Installa l'interfaccia riga di comando {{site.data.keyword.Bluemix}}.

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_bx_commandline.svg" alt="Scarica l'interfaccia riga di comando {{site.data.keyword.Bluemix}}" /> </a>

  2. Stabilisci una connessione a {{site.data.keyword.Bluemix}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  3. Accedi a {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

Quando viene immesso un comando **bluemix app push**, l'interfaccia riga di comando fornisce la directory di lavoro all'ambiente {{site.data.keyword.Bluemix_notm}} che usa un pacchetto di build per creare ed eseguire l'applicazione.

  1. Dalla directory della tua applicazione, immetti il comando **bluemix app push** con il nome dell'applicazione. Il nome dell'applicazione deve essere univoco nell'ambiente {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</code></pre>

  {{site.data.keyword.Bluemix_notm}} include
i pacchetti di build integrati. In alcuni casi, anche per i pacchetti di build integrati, devi fornire inoltre un'opzione -c per specificare il comando utilizzato per avviare la tua applicazione. Ad esempio, devi usare l'opzione -c per distribuire la tua applicazione Node.js:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</code></pre>

  Inoltre, l'applicazione Node.js deve contenere un file package.json valido.

  La distribuzione di tutti gli altri pacchetti di build esterni deve essere eseguita utilizzando l'opzione -b. Ad
esempio:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</code></pre>

  **Suggerimento:** quando usi il comando **bluemix app push**, il comando copia tutti i file e tutte le directory dalla tua directory corrente a Bluemix. Assicurati di avere solo i file richiesti nella directory della tua applicazione.


  2. Se modifichi la tua applicazione, puoi caricare tali modifiche immettendo nuovamente il comando `bluemix app push`. Il comando utilizza le tue opzioni precedenti e le tue risposte ai prompt per aggiornare con i nuovi bit di codice le eventuali istanze dell'applicazione in esecuzione.

La CLI {{site.data.keyword.Bluemix}} ha incluso una cli cf nella sua installazione. Il comando `bluemix app push` richiama effettivamente `cf push` per caricare e distribuire la tua applicazione in {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni su cf push, vedi [Comandi cf](/docs/cli/reference/cfcommands/index.html). Per informazioni sui pacchetti di build, vedi [Utilizzo dei pacchetti di build della community](/docs/cfapps/byob.html).
