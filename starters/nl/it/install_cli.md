{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
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

# Distribuisci la tua applicazione con l'interfaccia riga di comando Cloud Foundry
*Ultimo aggiornamento: 11 novembre 2015*

Puoi usare l'interfaccia riga di comando Cloud Foundry per distribuire e modificare
applicazioni e istanze del servizio.
{:shortdesc}

Prima di iniziare, installa l'interfaccia riga di comando cf.

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_cf_commandline.svg" alt="Scarica l'interfaccia riga di comando Cloud Foundry" /> </a>
</p>

**Limitazione:** l'interfaccia riga di comando Cloud Foundry non
è supportata da Cygwin. Utilizza l'interfaccia riga di comando Cloud Foundry
in una finestra riga di comando diversa da quella di Cygwin.

Dopo che l'interfaccia riga di comando cf è stata installata, puoi iniziare a lavorare:

  1. Scarica il codice starter.
  
    <p>
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_starter-code.svg" alt="Scarica codice di starter" /> </a>
    </p>
  
  {:download}
  2. Estrai il pacchetto in una nuova directory per configurare il tuo ambiente di sviluppo.
  3. Passa alla tua nuova directory.
  
  <pre class="pre">cd <var class="keyword varname">your_new_directory</var></pre>
  
  4. Stabilisci una connessione a {{site.data.keyword.Bluemix}}.
  
  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  5. Accedi a {{site.data.keyword.Bluemix_notm}}.
 
  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">nomeutente</var> -o <var class="keyword varname" data-hd-keyref="org_name">nome_org</var> -s <var class="keyword varname" data-hd-keyref="space_name">nome_spazio</var></pre>
  
  6. Distribuisci la tua applicazione a {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni sul comando cf push, vedi [Caricamento della tua applicazione](upload_app.html#upload_app__push).
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var></pre>
  
  7. Accedi alla tua applicazione immettendo il seguente URL
nel browser:
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
