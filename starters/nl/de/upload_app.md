---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Anwendung hochladen

Nachdem Sie sich bei {{site.data.keyword.Bluemix}} angemeldet haben, können Sie Ihre Anwendung mit dem Befehl `bluemix app push` hochladen.
{:shortdesc}

Bevor Sie damit beginnen, müssen Sie die folgenden Schritte durchführen:
  1. Installieren Sie die {{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle (CLI). 

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/btn_bx_commandline.svg" alt="{{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle herunterladen" /> </a> 

  2. Stellen Sie eine Verbindung zu {{site.data.keyword.Bluemix}} her.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">Domänenname</span></code></pre>

  3. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">Benutzername</var> -o <var class="keyword varname" data-hd-keyref="org_name">Organisationsname</var> -s <var class="keyword varname" data-hd-keyref="space_name">Bereichsname</var></code></pre>

Wenn ein Befehl **bluemix app push** ausgegeben wird, stellt die Befehlszeilenschnittstelle das Arbeitsverzeichnis für die {{site.data.keyword.Bluemix_notm}}-Umgebung bereit, die zum Erstellen und Ausführen der Anwendung ein Buildpack verwendet. 

  1. Geben Sie über Ihr Anwendungsverzeichnis den Befehl **bluemix app push** mit dem Anwendungsnamen ein. Der Anwendungsname muss in der {{site.data.keyword.Bluemix_notm}}-Umgebung eindeutig sein.

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">App-Name</var> -m 512m</code></pre>

  {{site.data.keyword.Bluemix_notm}} umfasst integrierte Buildpacks. In einigen Fällen (selbst für die integrierten Buildpacks) müssen Sie auch die Option -c verwenden, um den Befehl anzugeben, der zum Starten Ihrer Anwendung verwendet wird. So müssen Sie beispielsweise die Option -c verwenden, um eine Push-Operation für Ihre Node.js-Anwendung durchzuführen:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">App-Name</var> -c Startbefehl</code></pre>

  Darüber hinaus muss die Node.js-Anwendung eine gültige Datei package.json enthalten.

  Für alle anderen externen Buildpacks muss eine Push-Operation unter Verwendung der Option -b durchgeführt werden. Beispiel:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">App-Name</var> -b Buildpack-URL</code></pre>

  **Tipp:** Wenn Sie den Befehl **bluemix app push** verwenden, kopiert der Befehl sämtliche Dateien und Verzeichnisse aus Ihrem aktuellen Verzeichnis in Bluemix. Stellen Sie sicher, dass sich in Ihrem Anwendungsverzeichnis nur die erforderlichen Dateien befinden.

  
  2. Wenn Sie Ihre Anwendung ändern, können Sie diese Änderungen hochladen, indem Sie den Befehl `bluemix app push` erneut eingeben. Der Befehl verwendet Ihre vorherigen Optionen und Ihre Antworten auf die Eingabeaufforderungen, um alle aktiven Instanzen Ihrer Anwendung mit den neuen Code-Bits zu aktualisieren. 

Das {{site.data.keyword.Bluemix}}-CLI-Bundle enthält eine CF-Befehlszeilenschnittstelle (CLI) in seiner Installation. Der Befehl `bluemix app push` ruft tatsächlich den Befehl `cf push` auf, um Ihre Anwendung in {{site.data.keyword.Bluemix_notm}} hochzuladen und bereitzustellen. Weitere Informationen zum Befehl 'cf push' finden Sie unter [cf-Befehle](/docs/cli/reference/cfcommands/index.html). Informationen zu Buildpacks finden Sie unter [Community-Buildpacks verwenden](/docs/cfapps/byob.html).


**Tipp:** Sie können eine Anwendung auch über DevOps Services hochladen oder bereitstellen. Weitere Informationen finden Sie auf der Seite zum [Entwickeln von {{site.data.keyword.Bluemix_notm}}-Anwendungen in Node.js mit der Web-IDE](https://hub.jazz.net/tutorials/devopsweb/){: new_window}. 
