---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Überwachung und Protokollierung
{: #monitoringandlogging}

*Letzte Aktualisierung: 11. Mai 2016*

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

Protokolldateien werden automatisch erstellt, wenn Sie die Cloud Foundry-Infrastruktur verwenden, um Ihre Apps in {{site.data.keyword.Bluemix_notm}} auszuführen. Wenn in einer der Phasen von der Entwicklung bis zur Laufzeit Fehler auftreten, können Sie die Protokolle auf Hinweise prüfen, die Ihnen bei der Lösung des Problems möglicherweise helfen.

<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



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

Sie können die Protokolle für Ihre Cloud Foundry-Apps an drei Positionen anzeigen:

  * [{{site.data.keyword.Bluemix_notm}}-Dashboard](#viewing_logs_UI){:new_window}
  * [Befehlszeilenschnittstelle](#viewing_logs_cli){:new_window}
  * [Externe Protokollhosts](#thirdparty_logging){:new_window}

#### Protokolle im {{site.data.keyword.Bluemix_notm}}-Dashboard anzeigen
{: #viewing_logs_UI}

Führen Sie die folgenden Schritte aus, um die Bereitstellungs- oder Laufzeitprotokolle anzuzeigen:
1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und klicken Sie dann auf die Kachel für Ihre App auf dem Dashboard. Die Seite mit den Anwendungsdetails wird angezeigt.
2. Klicken Sie in der linken Navigationsleiste auf **Protokolle**.

In der Konsole für **Protokolle** können Sie die kürzlich generierten Protokolle für Ihre App oder Protokollendabschnitte in Echtzeit anzeigen. Darüber hinaus können Sie Protokolle nach Protokolltyp und Kanal filtern.

**Hinweis:** Protokolle werden nicht über App-Abstürze und App-Bereitstellungen hinweg gespeichert.



#### Protokolle über die Befehlszeilenschnittstelle anzeigen
{: #viewing_logs_cli}

Wählen Sie eine der folgenden Optionen zum Anzeigen von Protokollen über die Befehlszeilenschnittstelle aus:

<ul>
<li>Tailing-Protokolle beim Bereitstellen von Apps.
<p>Verwenden Sie den Befehl **cf logs**, um Protokolle aus Ihrer App und aus den Systemkomponenten anzuzeigen, die mit Ihrer App interagieren, wenn Sie Apps in {{site.data.keyword.Bluemix_notm}} bereitstellen. Sie können die folgenden Befehle in die Befehlszeilenschnittstelle 'cf' eingeben. Weitere Informationen zum Befehl 'cf logs' finden Sie in der Beschreibung der <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target="_blank">Protokolltypen und ihrer Nachrichten in Cloud Foundry</a>. </p>
<dl>
<dt><strong>cf logs <var class="keyword varname">App-Name</var> --recent</strong></dt>
<dd>Zeigt kürzlich erstellte Protokolle an.</dd>

<dt><strong>cf logs <var class="keyword varname">App-Name</var></strong></dt>
<dd>Zeigt Protokolle an, die in dem Moment generiert werden, in dem Sie diesen Befehl eingeben.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Tipp:</span> Wenn Sie den Befehl <span class="keyword cmdname">cf push</span> oder <span class="keyword cmdname">cf
start</span> in einem Befehlszeilenfenster ausführen, können Sie <samp class="ph codeph">cf logs App-Name --recent</samp> in einem anderen Befehlszeilenfenster eingeben, um die Protokolle in Echtzeit anzuzeigen. </div>
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
<dd><p>Diese Protokolldatei zeichnet Nachrichten nach den wichtigsten Schritten der Staging-Task auf. Mithilfe dieses Protokolls können Sie Probleme beim Staging beheben.</p>
<p>Geben Sie den folgenden Befehl ein, um dieses Protokoll anzuzeigen:
<pre class="pre">cf files <var class="keyword varname">App-Name</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Hinweis:** Informationen zur Aktivierung der Anwendungsprotokollierung finden Sie unter [Laufzeitfehler beheben](../debug/index.html#debugging-runtime-errors).




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



### Externe Protokollhosts konfigurieren
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} bewahrt eine begrenzte Menge an Protokolldaten im Speicher. Bei der Protokollierung von Daten werden die alten Informationen durch die neueren Daten ersetzt. Zur Aufbewahrung aller Protokolldaten können Sie Ihre Protokolle auf einem externen Protokollhost, wie zum Beispiel einem Protokoll-Management-Service eines anderen Anbieters, oder auf einem anderen Host speichern.

Führen Sie die folgenden Schritte aus, um Protokolle aus Ihrer App und dem System an einen externen Protokollhost zu übermitteln:

  1. Bestimmen Sie den Protokollierungsendpunkt. 
     
	 Sie können Protokolle an einen Protokollaggregator eines Drittanbieters wie Papertrail, Splunk oder Sumologic senden. Sie können Protokolle auch an einen Syslog-Host, einen Syslog-Host mit TLS-Verschlüsselung (Transport Layer Security) oder an einen HTTP-POST-Endpunkt senden. Die Methoden zum Anfordern von Protokollierungsendpunkten sind für verschiedene Protokollhosts unterschiedlich.

  2. Erstellen Sie eine vom Benutzer bereitgestellte Serviceinstanz.
     
	 Verwenden Sie den Befehl ```cf create-user-provided-service``` (oder die Kurzversion des Befehls ```cups``), um eine vom Benutzer bereitgestellte Serviceinstanz zu erstellen: 
	 ```
	 cf create-user-provided-service <Servicename> -l <Protokollierungsendpunkt>
	 ```
	 **Servicename**
	 
	 Der Name der vom Benutzer bereitgestellten Serviceinstanz.
	 
	 **Protokollierungsendpunkt**
	 
	 Der Protokollierungsendpunkt, an den {{site.data.keyword.Bluemix_notm}} Protokolle sendet. In der folgenden Tabelle finden Sie Informationen zu den Werten, durch die die Variable *Protokollierungsendpunkt* in Ihrem Fall ersetzt werden kann:
	 
	 <table>
     <thead>
     <tr>
     <th>Protokollierungsendpunkt</th>
     <th>Befehl</th>
	 <th>Anmerkungen</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>Syslog-Host</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>Beispiel: Zum Aktivieren der Protokollierung an Papertrail geben Sie den Befehl `cf cups my-logs -l syslog://<papertrail-url>` ein. Ersetzen Sie `<papertrail-url>` durch die URL für Ihren Protokollierungsendpunkt von Papertrail.</td>
     </tr>
	 <tr>
     <td>Syslog-TLS-Host</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>Dem Zertifikat muss von einer Zertifizierungsstelle vertraut werden. Verwenden Sie keine selbst signierten Zertifikate.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>Dieser Endpunkt muss sich im öffentlichen Internet befinden und für {{site.data.keyword.Bluemix_notm}} zugänglich sein.</td>
     </tr>
     </tbody>
     </table>	
  3. Binden Sie die Serviceinstanz an Ihre App.

	 Verwenden Sie den folgenden Befehl, um die Serviceinstanz an Ihre App zu binden: 
	
	 ```
	 cf bind-service App-Name <Servicename>
	 ```
	 **App-Name**
	 
	 Der Name Ihrer App.
	 
	 **Servicename**
	 
	 Der Name der vom Benutzer bereitgestellten Serviceinstanz.
	 
  4. Führen Sie ein erneutes Staging für die App durch. 
     Geben Sie den Befehl ```cf restage appname``` ein, damit die Änderungen wirksam werden. 

#### Protokolle in externen Hosts anzeigen
{: #viewing_logs_external}

	 
Wenn Protokolle generiert werden, können Sie nach einer kurzen Verzögerung Nachrichten in Ihrem externen Protokollhost anzeigen, die den Nachrichten ähnlich sind, die Sie über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder über die Befehlszeilenschnittstelle 'cf' anzeigen.  Wenn Sie mehrere Instanzen Ihrer App haben, werden die Protokolle zusammengefasst und Sie können alle Protokolle für Ihre App anzeigen. Darüber hinaus werden die Protokolle über App-Abstürze und App-Bereitstellungen hinweg gespeichert.

**Hinweis:** Protokolle, die Sie über die Befehlszeilenschnittstelle anzeigen, haben nicht das Syslog-Format und stimmen daher möglicherweise nicht genau mit den Nachrichten überein, die in Ihren externen Protokollhost angezeigt werden. 


