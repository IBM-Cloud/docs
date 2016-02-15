{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Überwachung und Protokollierung
{: #monitoringandlogging}

*Letzte Aktualisierung: 8. Dezember 2015*

Indem Sie Ihre Apps überwachen und Protokolle überprüfen, können Sie die Anwendungsausführung und den Datenfluss verfolgen, um Ihre Bereitstellung besser zu verstehen. Darüber hinaus können Sie die Zeit und den Aufwand für das Auffinden und Beheben von Problemen reduzieren.
{:shortdesc}

Bei {{site.data.keyword.Bluemix}}-Anwendungen kann es sich um weit verteilte Anwendungen mit mehreren Instanzen handeln und die Ausführung Ihrer Anwendung mitsamt der zugehörigen Daten kann von vielen verschiedenen Services übernommen werden. In einer solchen komplexen Umgebung ist das Überwachen Ihrer Apps und das Überprüfen von Protokollen von zentraler Bedeutung für das Verwalten Ihrer Apps.

{{site.data.keyword.Bluemix_notm}} hat einen integrierten Protokolliermechanismus, um Protokolldateien für Ihre Apps zu erstellen, während sie ausgeführt werden. In den Protokollen können Sie die Fehler, Warnungen und Informationsnachrichten sehen, die für Ihre Apps erzeugt werden. Sie können Ihre App auch so konfigurieren, dass Protokollnachrichten in die Protokolldatei geschrieben werden. Weitere Informationen zu Protokollformaten und zur Anzeige von Protokollen finden Sie unter [Protokollierung für {{site.data.keyword.Bluemix_notm}}-Apps](#logging_for_bluemix_apps).

Durch die Überwachung Ihrer App können Sie Ihre App-Bereitstellung anzeigen und steuern. Mithilfe der Überwachung können Sie die folgenden Tasks ausführen:

* Sammeln und überwachen Sie die Leistungsinformationen für App-Instanzen und prüfen Sie, ob diese funktional sind.
* Gewinnen Sie Einblick in Anwendungsoperationen - erkennen Sie beispielsweise potenzielle Engpässe oder stellen Sie fest, wann Upgrades erforderlich sind.
* Prognostizieren Sie die Ressourcennutzung und die anfallenden Gebühren.

Für einen stabilen Betrieb Ihrer Bereitstellungen auf der {{site.data.keyword.Bluemix_notm}}-Plattform möchten Sie Probleme schnell erkennen und Ursachen effizient bestimmen. Dieses Ziel erreichen Sie, wenn Sie bei der Konzeption Ihrer Apps die Fehlerbehebung im Hinterkopf behalten und Services oder Tools für die Überwachung und Protokollierung verwenden, wenn Ihre App in {{site.data.keyword.Bluemix_notm}} bereitgestellt wird.

##Überwachung von Apps, die in Cloud Foundry ausgeführt werden
{: #monitoring_bluemix_apps}

Wenn Sie die Cloud Foundry-Infrastruktur verwenden, um Ihre Apps in {{site.data.keyword.Bluemix_notm}} auszuführen, möchten Sie über aktuelle Leistungsdaten wie den allgemeinen Status, die Ressourcennutzung und Datenverkehrsmetriken auf dem Laufenden bleiben. Anhand dieser Leistungsdaten können Sie Entscheidungen treffen oder entsprechende Maßnahmen ergreifen.

Setzen Sie zur Überwachung von {{site.data.keyword.Bluemix_notm}}-Apps eine der folgenden Methoden ein:

* {{site.data.keyword.Bluemix_notm}}-Services. 'Monitoring and Analytics' ist ein Service, mit dem Sie Ihre Anwendungsleistung überwachen können. Zusätzlich stellt dieser Service Analysefunktionen wie eine Protokollanalyse bereit. Weitere Informationen finden Sie unter [Monitoring and Analytics](../services/monana/index.html).
* Optionen von Drittanbietern. Beispiel: [New Relic](http://newrelic.com/){:new_window}.

##Protokollierung für Apps, die in Cloud Foundry ausgeführt werden
{: #logging_for_bluemix_apps}

Protokolldateien werden automatisch erstellt, wenn Sie die Cloud Foundry-Infrastruktur verwenden, um Ihre Apps in {{site.data.keyword.Bluemix_notm}} auszuführen. Sie können die Protokolle entweder im {{site.data.keyword.Bluemix_notm}}-Dashboard oder über die Befehlszeilenschnittstelle 'cf' anzeigen. Sie können die Protokolle auch filtern, um nur die für Sie relevanten Teile anzuzeigen.

###Protokollformat
{: #log_format}

Protokolle für {{site.data.keyword.Bluemix_notm}}-Anwendungen werden in einem festen Format angezeigt, ähnlich dem folgenden Muster:

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <Nachricht>
```
{:screen}

Jeder Protokolleintrag enthält vier Felder. In der folgenden Liste finden Sie eine kurze Beschreibung der einzelnen Felder:

<dl>
<dt><strong>Zeitmarke</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>Spalten: 1 - 27</p>
<p>Die Zeit der Protokollanweisung. Die Zeitmarke ist bis auf die Millisekunde definiert.</p>
</dd>

<dt><strong>Komponente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Spalten: 29 - 40</p>
<p>Die Komponente, die Protokolle produziert. In der folgenden Liste finden Sie die Definition aller Komponenten:</p>

<dl>
<dt><strong>APP</strong></dt>
<dd>Anwendung. Der Komponente APP folgt ein Schrägstrich und eine Ziffer, die die Anwendungsinstanz angibt. Dabei ist 0 die erste Instanz, 1 die zweite Instanz usw.</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry-API.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent.</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator.</dd>

<dt><strong>RTR</strong></dt>
<dd>Router.</dd>

<dt><strong>STG</strong></dt>
<dd>Staging.</dd>
</dl>
</dd>

<dt><strong>Datenstrom</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Spalte: 42 - 44</p>
<p>Der Datenstrom, in den die Protokollnachricht geschrieben wird. <samp class="ph codeph">OUT</samp> bezieht sich auf den Datenstrom <samp class="ph codeph">stdout</samp> und <samp class="ph codeph">ERR</samp> bezieht sich auf den Datenstrom <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>Nachricht</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Nachricht</var>&gt;</code></pre>
<p>Spalte: 46 - Zeilenende</p>
<p>Die Nachricht, die von der Komponente ausgegeben wird. Die Nachricht variiert abhängig vom Kontext.</p>
</dd>

</dl>

###Protokolle anzeigen
{: #viewing_logs}

Protokolle können Sie entweder im {{site.data.keyword.Bluemix_notm}}-Dashboard oder über die Befehlszeilenschnittstelle anzeigen.

####Protokolle im {{site.data.keyword.Bluemix_notm}}-Dashboard anzeigen

Führen Sie die folgenden Schritte aus, um die Protokolle zur **Bereitstellung** oder zur **Laufzeit** anzuzeigen:
1. Klicken Sie auf die Kachel für Ihre App. Die Seite mit den Anwendungsdetails wird angezeigt.
2. Klicken Sie in der linken Navigationsleiste auf **Protokolle**.

####Protokolle über die Befehlszeilenschnittstelle anzeigen

Wählen Sie eine der folgenden Optionen zum Anzeigen von Protokollen über die Befehlszeilenschnittstelle aus:

<ul>
<li>Tailing-Protokolle beim Bereitstellen von Apps.
<p>Verwenden Sie den Befehl **cf logs**, um Protokolle aus Ihrer App und aus den Systemkomponenten anzuzeigen, die mit Ihrer App interagieren, wenn Sie Apps in {{site.data.keyword.Bluemix_notm}} bereitstellen. Sie können die folgenden Befehle in die Befehlszeilenschnittstelle 'cf' eingeben. Weitere Informationen zum Befehl 'cf logs' finden Sie unter [Log Types and Their Messages in Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}. </p>
<dl>
<dt><strong>cf logs <var class="keyword varname">App-Name</var> --recent</strong></dt>
<dd>Zeigt kürzlich erstellte Protokolle an.</dd>

<dt><strong>cf logs <var class="keyword varname">App-Name</var></strong></dt>
<dd>Zeigt Protokolle an, die in dem Moment generiert werden, in dem Sie diesen Befehl eingeben.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Tipp:</span> Wenn Sie den Befehl <span class="keyword cmdname">cf push</span> oder <span class="keyword cmdname">cf
start</span> in einem Befehlszeilenfenster ausführen, können Sie <samp class="ph codeph">cf logs App-Name --recent</samp> in einem anderen Befehlszeilenfenster eingeben, um die Protokolle in Echtzeit anzuzeigen.
</div>
</li>

<li>Protokolle anzeigen, nachdem die Apps bereitgestellt wurden.

<p>Wenn die Anwendungsprotokollierung aktiviert ist, können Sie die folgenden Anwendungsprotokolle anzeigen, falls Probleme mit Ihrer App während der Laufzeit auftreten. Mithilfe von Anwendungsprotokollen lässt sich die Ursache eines Fehlers einfacher bestimmen.</p>

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>Diese Protokolldatei zeichnet differenzierte Informationsereignisse für das Debugging auf. Sie können dieses Protokoll verwenden, um Probleme bei der Ausführung des Buildpacks zu beheben.</p>
<p>Wenn Daten in der Datei <span class="ph filepath">buildpack.log</span> generiert werden sollen, müssen Sie die Traceerstellung für Buildpacks aktivieren, indem Sie den folgenden Befehl ausführen:
   <pre class="pre">cf set-env <var class="keyword varname">App-Name</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
<p>Geben Sie den folgenden Befehl ein, um dieses Protokoll anzuzeigen:
<pre class="pre">cf files <var class="keyword varname">App-Name</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>Diese Protokolldatei zeichnet Nachrichten nach den wichtigsten Schritten der Staging-Task auf. Mithilfe dieses Protokolls können Sie Probleme beim Staging beheben. </p>
<p>Geben Sie den folgenden Befehl ein, um dieses Protokoll anzuzeigen:
<pre class="pre">cf files <var class="keyword varname">App-Name</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Hinweis:** Informationen zur Aktivierung der Anwendungsprotokollierung finden Sie unter [Laufzeitfehler beheben](../troubleshoot/debugging.html#debug_runtime).

###Protokolle filtern
{: #filtering_logs}

Zum Anzeigen von für Sie relevanten Protokollen oder zum Ausschließen des Inhalts, den Sie nicht anzeigen möchten, können Sie den Befehl **cf logs** mit Filteroptionen wie **cut** und **grep** in der Befehlszeilenschnittstelle 'cf' verwenden.

* Wenn Sie nur einen Teil statt des gesamten ausführlichen Protokolls anzeigen möchten, verwenden Sie die Option **cut**. Geben Sie beispielsweise den folgenden Befehl ein, um die Komponenten- und Nachrichteninformationen anzuzeigen:
```
cf logs App-Name --recent | cut -c 29-40,46-
```

Für weitere Informationen zur Option **grep** geben Sie 'cut --help' ein.
* Zum Anzeigen von Protokolleinträgen, die bestimmte Schlüsselwörter enthalten, verwenden Sie die Option **grep**. Protokolleinträge, die das Schlüsselwort '[APP' enthalten, können Sie beispielsweise mithilfe des folgenden Befehls anzeigen:
```
cf logs App-Name --recent | grep '\[App'
```
Für weitere Informationen zur Option **grep** geben Sie `grep --help` ein.

###Protokollierung durch Drittanbieter konfigurieren
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} bewahrt eine
begrenzte Menge an Protokolldaten im Speicher. Bei der Protokollierung von Daten
werden die alten Informationen durch die neueren Daten ersetzt.
Zur Aufbewahrung sämtlicher Protokolldaten können Sie Ihre Protokolle
in einem Protokoll-Management-Service eines anderen Anbieters speichern. 

Führen Sie die folgenden Schritte aus, um Protokolle von Ihrer Anwendung
und dem System an den Protokoll-Management-Service eines anderen Anbieters zu übermitteln: 

1. Registrieren Sie sich bei einem Protokoll-Management-Service eines anderen Anbieters.
    
    Sie können jeden beliebigen Protokoll-Management-Service eines anderen Anbieters
nutzen, der das [syslog-Protokoll](http://tools.ietf.org/html/rfc5424){:new_window}
unterstützt, z. B. Papertail, Splunk Storm, SumoLogic und Logentries.
Registrieren Sie sich bei einem Protokoll-Management-Service eines anderen Anbieters und konfigurieren
Sie den Service anschließend, um ein Ziel für Ihre Protokolle
in {{site.data.keyword.Bluemix_notm}} anzugeben.
Nach Abschluss der Konfiguration stellt der Service standardmäßig
eine syslog-URL als Ziel für Ihre Protokolle in {{site.data.keyword.Bluemix_notm}} bereit. Informationen
zur Konfiguration von Protokoll-Management-Services anderer Anbieter finden Sie unter
[Configuring Selected Third-Party Log Management Services](http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html){:new_window}. 

2. Erstellen Sie eine vom Benutzer bereitgestellte Serviceinstanz.
	
	Um Protokolle in {{site.data.keyword.Bluemix_notm}} an
den Protokoll-Management-Service des anderen Anbieters zu übermitteln,
müssen Sie zunächst eine vom Benutzer bereitgestellte Serviceinstanz erstellen. Verwenden Sie für die Erstellung
einer vom Benutzer bereitgestellten Serviceinstanz den folgenden Befehl; dabei ist 'Servicename' der
Name der vom Benutzer bereitgestellten Serviceinstanz und 'syslog-URL' ist die
URL, die Sie vom Protokollierungsservice des anderen Anbieters erhalten. 
	
	```
	cf create-user-provided-service <Servicename> -l <syslog-URL>
	```
	
3. Binden Sie die Serviceinstanz an Ihre Anwendung.

	Verwenden Sie zum Binden der Serviceinstanz an Ihre Anwendung den folgenden Befehl;
dabei ist 'App-Name' der Name Ihrer Anwendung und
'Servicename' ist der Name für die vom Benutzer bereitgestellte Serviceinstanz. 
	
	```
	cf bind-service App-Name <Servicename>
	```
	
	Anschließend
werden Sie dazu aufgefordert, für die Anwendung ein erneutes Staging durchzuführen; geben Sie hierfür 'cf
restage App-Name' ein, damit die Änderungen wirksam werden. Wenn Protokolle generiert werden,
können Sie nach einer kurzen Verzögerung ähnliche Nachrichten im Protokoll-Management-Service des anderen Anbieters sehen.


**Hinweis:** Protokolle, die Sie in der Befehlszeilenschnittstelle sehen,
weisen nicht das syslog-Format auf und stimmen möglicherweise nicht genau
mit den Nachrichten überein, die in den Protokoll-Management-Services anderer Anbieter angezeigt
werden. 
