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

# App mit der Cloud Foundry-Befehlszeilenschnittstelle bereitstellen
*Letzte Aktualisierung: 11. November 2015*

Mithilfe der Cloud Foundry-Befehlszeilenschnittstelle können Sie Anwendungen und Serviceinstanzen bereitstellen und ändern. 
{:shortdesc}

Installieren Sie vor Beginn die Befehlszeilenschnittstelle 'cf'.

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/btn_cf_commandline.svg" alt="Cloud Foundry-Befehlszeilenschnittstelle herunterladen" /> </a>
</p>

**Einschränkung:** Die
Cloud Foundry-Befehlszeilenschnittstelle wird nicht von Cygwin unterstützt. Verwenden Sie
die Cloud Foundry-Befehlszeilenschnittstelle in einem
Befehlszeilenfenster, das sich von dem Befehlszeilenfenster von Cygwin unterscheidet. 

Nach der Installation der Befehlszeilenschnittstelle 'cf' können Sie die folgenden ersten Schritte durchführen:

  1. Laden Sie den Startercode herunter. 
  
    <p>
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/btn_starter-code.svg" alt="Startercode herunterladen" /> </a>
  </p>
  
  {:download}
  2. Extrahieren Sie das Paket in ein neues Verzeichnis, um Ihre Entwicklungsumgebung einzurichten. 
  3. Wechseln Sie in Ihr neues Verzeichnis.
  
  <pre class="pre">cd <var class="keyword varname">neues_verzeichnis</var></pre>
  
  4. Stellen Sie eine Verbindung zu {{site.data.keyword.Bluemix}} her.
  
  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  5. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an. 
 
  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">Benutzername</var> -o <var class="keyword varname" data-hd-keyref="org_name">Organisationsname</var> -s <var class="keyword varname" data-hd-keyref="space_name">Bereichsname</var></pre>
  
  6. Stellen Sie Ihre Anwendung für {{site.data.keyword.Bluemix_notm}} bereit. Weitere Informationen zum Befehl 'cf push' finden Sie unter [Anwendung hochladen](upload_app.html#upload_app__push). 
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">App-Name</var></pre>
  
  7. Greifen Sie auf die App zu, indem Sie die folgende URL in Ihren Browser eingeben: 
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">Host</var>.<span class="keyword" data-hd-keyref="APPDomain">AppDomainName</span></code></pre>
