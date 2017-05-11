---



copyright:

  years: 2015，2017

lastupdated: "2017-04-19"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# Scarica, modifica e ridistribuisci la tua applicazione Cloud Foundry con l'interfaccia della riga di comando

Utilizza l'interfaccia riga di comando {{site.data.keyword.Bluemix_notm}} per scaricare, modificare e ridistribuire le tue istanze del servizio e applicazioni Cloud Foundry.
{:shortdesc}

Prima di iniziare, scarica e installa l'interfaccia di riga di comando {{site.data.keyword.Bluemix_notm}}. 

<p>
<a class="xref" href="https://clis.ng.bluemix.net" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_bx_commandline.svg" alt="Scarica l'interfaccia riga di comando Bluemix" /> </a>
</p>

**Limitazione:** lo strumento della riga di comando non è supportato da Cygwin. Utilizzalo in una finestra della riga di comando diversa da quella di Cygwin.
{:prereq}

Dopo aver installato l'interfaccia riga di comando, puoi iniziare:

  1. {: download} Scarica il codice per la tua applicazione in una nuova directory per configurare il tuo ambiente di sviluppo.
  
    <a class="xref" href="http://bluemix.net" target="_blank" title="(si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_starter-code.svg" alt="Scarica il codice dell'applicazione" /> </a>

  2. Passa alla directory in cui si trova il codice.

  <pre class="pre"><code class="hljs">cd <var class="keyword varname">la_tua_nuova_directory</var></code></pre>

  3.  Apporta le modifiche al codice della tua applicazione, adattandolo. Ad esempio, se stai utilizzando un'applicazione di esempio {{site.data.keyword.Bluemix}} che contiene il file `src/main/webapp/index.html`, puoi modificarlo con "Thanks for creating ..." per fare qualcosa di nuovo. Assicurati che l'applicazione sia in esecuzione localmente prima di distribuirla a {{site.data.keyword.Bluemix_notm}}.

    Prendi nota del file `manifest.yml`. Quando ridistribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}}, questo file viene utilizzato per determinare l'URL, l'allocazione di memoria, il numero di istanze e altri parametri fondamentali della tua applicazione. Per [ulteriori informazioni sul file manifest](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window}, consulta la documentazione Cloud Foundry.

    Presta inoltre attenzione al file `README.md`, che contiene dettagli come le istruzioni di creazione se applicabili.

    Nota: se la tua applicazione è un'applicazione Liberty, devi crearla prima di ridistribuirla.

  4. Collegati ed accedi a {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></code></pre>

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var></code></pre>

  Se stai utilizzando un ID federato, usa l'opzione `-sso`.

  <pre class="pre"><code class="hljs">bluemix login  -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var> -sso</code></pre>

  5. Da <var class="keyword varname">la_tua_nuova_directory</var>, ridistribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando il comando `bluemix app push`. Per ulteriori informazioni sul comando `bx app push`, vedi [Caricamento della tua applicazione](/docs/starters/upload_app.html).

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">nome_app</var></code></pre>

  6. Accedi alla tua applicazione andando all'indirizzo https://<var class="keyword varname" data-hd-keyref="app_url">url_app</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span>.
