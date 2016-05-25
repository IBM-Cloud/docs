---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Anwendung hochladen
*Letzte Aktualisierung: 17. Februar 2016*

Nachdem Sie sich bei {{site.data.keyword.Bluemix}} angemeldet haben, können Sie Ihre Anwendung mit dem Befehl 'cf push' hochladen.
{:shortdesc}

Bevor Sie damit beginnen, müssen Sie die folgenden Schritte durchführen:
  1. Installieren Sie die {{site.data.keyword.Bluemix}}- und Cloud Foundry-Befehlszeilenschnittstellen.

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/btn_bx_commandline.svg" alt="{{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle herunterladen" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/btn_cf_commandline.svg" alt="Cloud Foundry-Befehlszeilenschnittstelle herunterladen" /> </a> 

  2. Stellen Sie eine Verbindung zu {{site.data.keyword.Bluemix}} her.

  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">domänenname</span></pre>
  
  3. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">benutzername</var> -o <var class="keyword varname" data-hd-keyref="org_name">organisationsname</var> -s <var class="keyword varname" data-hd-keyref="space_name">bereichsname</var></pre>

Wenn ein Befehl **cf push** ausgegeben wird, stellt die Befehlszeilenschnittstelle
**cf** das Arbeitsverzeichnis für die
{{site.data.keyword.Bluemix_notm}}-Umgebung bereit, die zum Erstellen und Ausführen der Anwendung ein Buildpack
verwendet.

  1. Geben Sie über Ihr Anwendungsverzeichnis den Befehl **cf push** mit dem Anwendungsnamen ein. Der Anwendungsname muss in der {{site.data.keyword.Bluemix_notm}}-Umgebung eindeutig sein.
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app-name</var> -m 512m</pre>
  
  {{site.data.keyword.Bluemix_notm}} umfasst integrierte
Buildpacks. In einigen Fällen (selbst für die integrierten Buildpacks) müssen Sie auch die Option -c
verwenden, um den Befehl anzugeben, der zum Starten Ihrer Anwendung verwendet wird. So müssen Sie
beispielsweise die Option -c verwenden, um eine Push-Operation für Ihre Node.js-Anwendung durchzuführen:
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app-name</var> -c startbefehl</pre>
  
  Darüber hinaus muss die Node.js-Anwendung eine gültige Datei package.json enthalten.

  Für alle anderen externen Buildpacks muss eine Push-Operation unter Verwendung der Option -b durchgeführt werden. Beispiel:

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app-name</var> -b buildpack_URL</pre>
  
  **Tipp:** Wenn Sie den Befehl **cf push** verwenden, kopiert die Befehlszeilenschnittstelle **cf** sämtliche Dateien und Verzeichnisse aus Ihrem aktuellen Verzeichnis in Bluemix. Stellen Sie sicher, dass sich in Ihrem Anwendungsverzeichnis nur die erforderlichen Dateien befinden.

  Mit dem Befehl 'cf push' wird Ihre Anwendung hochgeladen und für {{site.data.keyword.Bluemix_notm}} bereitgestellt. Weitere Informationen zum Befehl 'cf push' finden Sie unter [cf-Befehle](../cli/reference/cfcommands/index.html). Informationen zu Buildpacks finden Sie unter [Community-Buildpacks verwenden](../cfapps/byob.html).

  2. Wenn Sie Ihre Anwendung ändern, können Sie diese Änderungen hochladen, indem Sie den Befehl 'cf push' erneut eingeben. Die Befehlszeilenschnittstelle 'cf' verwendet Ihre vorherigen Optionen und Ihre Antworten auf die Eingabeaufforderungen, um alle aktiven Instanzen Ihrer Anwendung mit den neuen Code-Bits zu aktualisieren.

**Tipp:** Sie können eine Anwendung auch über DevOps Services hochladen oder bereitstellen. Siehe [{{site.data.keyword.Bluemix_notm}}-Anwendungen in Node.js mit der Web-IDE entwickeln](https://hub.jazz.net/tutorials/devopsweb/){: new_window}.
