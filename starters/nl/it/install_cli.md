---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"


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

Utilizza l'interfaccia riga di comando Cloud Foundry per scaricare, modificare e ridistribuire le tue istanze del servizio e applicazioni Cloud Foundry.
{:shortdesc}

Prima di iniziare, scarica e installa l'interfaccia di riga di comando Cloud Foundry. 

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_cf_commandline.svg" alt="Scarica l'interfaccia riga di comando Cloud Foundry" /> </a>
</p>

**Limitazione:** lo strumento della riga di comando non è supportato da Cygwin. Utilizzalo in una finestra della riga di comando diversa da quella di Cygwin.
{:prereq}

Dopo aver installato l'interfaccia riga di comando, puoi iniziare:

  1. {: download} Scarica il codice per la tua applicazione in una nuova directory per configurare il tuo ambiente di sviluppo.
  
    <a class="xref" href="http://bluemix.net" target="_blank" title="(si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_starter-code.svg" alt="Scarica il codice dell'applicazione" /> </a>

  2. Passa alla directory in cui si trova il codice.

  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>

  3.  Apporta le modifiche al codice della tua applicazione, adattandolo. Ad esempio, se stai utilizzando un'applicazione di esempio {{site.data.keyword.Bluemix}} che contiene il file `src/main/webapp/index.html`, puoi modificarlo con "Thanks for creating ..." per fare qualcosa di nuovo. Assicurati che l'applicazione sia in esecuzione localmente prima di distribuirla a {{site.data.keyword.Bluemix_notm}}.

    Prendi nota del file `manifest.yml`. Quando ridistribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}}, questo file viene utilizzato per determinare l'URL, l'allocazione di memoria, il numero di istanze e altri parametri fondamentali della tua applicazione. Puoi [leggere ulteriori informazioni sul file manifest ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window} nella documentazione Cloud Foundry.

    Presta inoltre attenzione al file `README.md`, che contiene dettagli come le istruzioni di creazione se applicabili.

    Nota: se la tua applicazione è un'applicazione Liberty, devi crearla prima di ridistribuirla.

  4. Collegati ed accedi a {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>

  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">nomeutente</var> -o <var class="keyword varname" data-hd-keyref="org_name">nome_org</var> -s <var class="keyword varname" data-hd-keyref="space_name">nome_spazio</var></pre>

  Se stai utilizzando un ID federato, usa l'opzione `-sso`.

  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o <var class="keyword varname" data-hd-keyref="org_name">org_name</var> -s <var class="keyword varname" data-hd-keyref="space_name">space_name</var> -sso</pre>

  5. Da <var class="keyword varname">your_new_directory</var>, ridistribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}} utilizzando il comando `cf push`. Per ulteriori informazioni sul comando `cf push`, consulta [Caricamento della tua applicazione](/docs/starters/upload_app.html).

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">nome_applicazione</var></pre>

  6. Accedi alla tua applicazione andando all'indirizzo https://<var class="keyword varname" data-hd-keyref="app_name">nome_applicazione</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span>.
