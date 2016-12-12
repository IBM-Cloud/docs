---



copyright:

  years: 2015，20166

lastupdated: "2016-10-05"



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

# App mit der Befehlszeilenschnittstelle bereitstellen
Letzte Aktualisierung: 5. Oktober 2016
{: .last-updated}

Mithilfe der Befehlszeilenschnittstelle können Sie Anwendungen und Serviceinstanzen bereitstellen und ändern.
{:shortdesc}

Installieren Sie vor Beginn die {{site.data.keyword.Bluemix}}- und Cloud Foundry-Befehlszeilenschnittstellen.

<p>
<a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/btn_bx_commandline.svg" alt="{{site.data.keyword.Bluemix}}-Befehlszeilenschnittstelle herunterladen" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/btn_cf_commandline.svg" alt="Cloud Foundry-Befehlszeilenschnittstelle herunterladen" /> </a>
</p>

**Einschränkung:** Die Befehlszeilentools werden von Cygwin nicht unterstützt. Verwenden Sie die Tools in einem anderen Befehlszeilenfenster als dem Cygwin-Befehlszeilenfenster.
{:prereq}

Nach der Installation der Befehlszeilenschnittstellen können Sie beginnen:

  1. {: download} Laden Sie den Startercode herunter und extrahieren Sie das Paket in ein neues Verzeichnis, um Ihre Entwicklungsumgebung einzurichten.

    <a class="xref" href="http://bluemix.net" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)"><img class="image" src="images/btn_starter-code.svg" alt="Starter-Code herunterladen" /> </a>

  2. Wechseln Sie in das Verzeichnis, in dem sich Ihr Code befindet.

  <pre class="pre">cd <var class="keyword varname">neues_verzeichnis</var></pre>

  3.  Nehmen Sie die gewünschten Änderungen an Ihrem App-Code vor. Es wird empfohlen, zunächst sicherzustellen, dass sich die App lokal ausführen lässt, bevor sie wieder in {{site.data.keyword.Bluemix}} bereitgestellt wird.<br><br>Eine Datei, die zu beachten ist, ist die Datei `manifest.yml`. Wenn Ihre App wieder in {{site.data.keyword.Bluemix}} bereitgestellt wird, dient diese Datei zum Ermitteln der URL, der Speicherzuordnung, der Anzahl von Instanzen und anderer wichtiger Parameter für Ihre Anwendung. Weitere [Informationen zur Manifestdatei](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window} finden Sie in der Cloud Foundry-Dokumentation.

  4. Stellen Sie eine Verbindung zu {{site.data.keyword.Bluemix}} her.

  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">domänenname</span></pre>

  5. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">benutzername</var> -o <var class="keyword varname" data-hd-keyref="org_name">organisationsname</var> -s <var class="keyword varname" data-hd-keyref="space_name">bereichsname</var></pre>

  Wenn Sie eine eingebundene ID verwenden, nehmen Sie die Option -sso.

  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">username</var> -o "<var class="keyword varname" data-hd-keyref="org_name">org_name</var>" -s "<var class="keyword varname" data-hd-keyref="space_name">space_name</var>" -sso</pre>

  6. Stellen Sie Ihre Anwendung für {{site.data.keyword.Bluemix_notm}} bereit. Weitere Informationen zum Befehl 'cf push' finden Sie unter [Anwendung hochladen](/docs/starters/upload_app.html).

  <pre class="pre">cf push "<var class="keyword varname" data-hd-keyref="app_name">app-name</var>"</pre>

  7. Greifen Sie auf die App zu, indem Sie die folgende URL in Ihren Browser eingeben:

  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">App-Domänenname</span></code></pre>
