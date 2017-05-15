---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Überwachung und Protokollierung mit Cloud Foundry
{: #monitoringandlogging}


Durch Überwachen Ihrer Apps und Prüfen von Protokollen können Sie die Anwendungsausführung und den Datenfluss verfolgen, um einen besseren Einblick in Ihre Bereitstellung zu erhalten. Darüber hinaus können Sie auf diese Weise den Zeit- und Arbeitsaufwand zur Ermittlung und Behebung von Problemen verringern.
{:shortdesc}

{{site.data.keyword.Bluemix}}-Anwendungen können weit verteilt sein und mehrere Instanzen umfassen. Ihre ausgeführte Anwendung sowie die Daten der Anwendung können über viele Services hinweg gemeinsam genutzt werden. In einer solchen komplexen Umgebung kommt der Überwachung der Apps und der Prüfung von Protokollen eine besondere Bedeutung für die Verwaltung Ihrer Apps zu. 

## Überwachung und Protokollierung für Cloud Foundry-Apps
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}} hat einen integrierten Protokolliermechanismus, um Protokolldateien für Ihre Apps zu erstellen, während sie ausgeführt werden. In den Protokollen können Sie die Fehler, Warnungen und Informationsnachrichten prüfen, die für Ihre App generiert werden. Sie können Ihre App auch so konfigurieren, dass Protokollnachrichten in die Protokolldatei geschrieben werden. Weitere Informationen zu Protokollformaten und zur Anzeige von Protokollen finden Sie unter [Protokollierung für Apps, die in Cloud Foundry ausgeführt werden](#logging_for_bluemix_apps).

Durch die Überwachung Ihrer App können Sie Ihre App-Bereitstellung anzeigen und steuern. Mithilfe der Überwachung können Sie die folgenden Tasks ausführen:

* Sie können Leistungsinformationen für App-Instanzen sammeln und überwachen und prüfen, ob diese funktional sind.
* Sie können Anwendungsoperationen untersuchen, um zum Beispiel potenzielle Engpässe zu erkennen oder festzustellen, wann Upgrades erforderlich sind.
* Sie können die Ressourcennutzung und die anfallenden Gebühren schätzen. 

Für einen stabilen Betrieb Ihrer Bereitstellungen auf der {{site.data.keyword.Bluemix_notm}}-Plattform möchten Sie Probleme schnell erkennen und Ursachen effizient bestimmen. Dieses Ziel erreichen Sie, wenn Sie bei der Konzeption Ihrer Apps die Fehlerbehebung im Hinterkopf behalten und Services oder Tools für die Überwachung und Protokollierung verwenden, wenn Ihre App in {{site.data.keyword.Bluemix_notm}} bereitgestellt wird.

### Überwachung von Apps, die in Cloud Foundry ausgeführt werden
{: #monitoring_bluemix_apps}

Wenn Sie die Cloud Foundry-Infrastruktur verwenden, um Ihre Apps in {{site.data.keyword.Bluemix_notm}} auszuführen, sollten Sie über die Leistungsinformationen, wie z. B. Allgemeinzustand, Ressourcennutzung und Datenverkehr, auf dem Laufenden bleiben. Anhand dieser Leistungsinformationen können Sie Entscheidungen treffen oder Maßnahmen ergreifen.

Verwenden Sie eine der folgenden Methoden, um {{site.data.keyword.Bluemix_notm}}-Apps zu überwachen:

* {{site.data.keyword.Bluemix_notm}}-Services. Monitoring and Analytics bietet einen Service, den Sie zur Überwachung Ihrer Anwendungsleistung verwenden können. Darüber hinaus stellt dieser Service Analysefunktionen zum Beispiel zur Protokollanalyse bereit. Weitere Informationen finden Sie unter [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate).
* Optionen von Drittanbietern. Beispiel: [New Relic ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://newrelic.com/){:new_window}.

### Protokollierung für Apps, die in Cloud Foundry ausgeführt werden
{: #logging_for_bluemix_apps}

Protokolldateien werden automatisch erstellt, wenn Sie die Cloud Foundry-Infrastruktur zur Ausführung Ihrer Apps in {{site.data.keyword.Bluemix_notm}} verwenden. Wenn zu irgendeinem Zeitpunkt, angefangen mit der Bereitstellung bis hin zur Laufzeit, Fehler auftreten, können Sie die Protokolle auf Hinweise prüfen, die bei der Fehlerbehebung hilfreich sein können. 


<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



### Protokollformat und Protokollspeicherung
{: #log_format}

In {{site.data.keyword.Bluemix_notm}} Public werden Protokolldaten für Cloud Foundry-Apps standardmäßig sieben Tage lang gespeichert. Sie können bis zu 1 GB an Daten pro Tag durchsuchen. 

Protokolle für {{site.data.keyword.Bluemix_notm}}-Anwendungen werden in einem festen Format nach dem folgenden Muster angezeigt: 

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
jjjj-MM-ttTHH:mm:ss:SS-0500 [App/0]      OUT <Nachricht>
```
{:screen}

Jeder Protokolleintrag enthält vier Felder. In der folgenden Liste werden die einzelnen Felder kurz beschrieben: 

<dl>
<dt><strong>Zeitmarke</strong></dt>
<dd>
<pre class="pre screen"><code>jjjj-MM-ttTHH:mm:ss:SS-0500</code></pre>
<p>Spalten: 1 - 27</p>
<p>Die Zeit des Protokolleintrags. Die Zeitmarke ist bis auf die Millisekunde definiert.</p>
</dd>

<dt><strong>Komponente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Spalten: 29 - 40</p>
<p>Die Komponente, die Protokolle generiert. </p>
<p>Auf jeden Komponententyp folgt ein Schrägstrich und eine Ziffer, die die Anwendungsinstanz angibt. 0 ist die Ziffer, die der ersten Instanz zugeordnet ist, 1 die der zweiten usw.</p>
<p>In der folgenden Liste werden die verschiedenen Typen von Komponenten kurz beschrieben: </p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: Die Komponente LGR stellt Informationen zum Protokollierungsservice (Logging) bereit. </dd>

<dt><strong>RTR</strong></dt>
<dd>Router: Die Komponente RTR stellt Informationen zu HTTP-Anforderungen an eine Anwendung bereit. </dd>

<dt><strong>STG</strong></dt>
<dd>Staging: Die Komponente STG stellt Informationen zum Staging und erneuten Staging einer Anwendung bereit. </dd>

<dt><strong>APP</strong></dt>
<dd>Anwendung: Die Komponente APP stellt Informationenen zu einer Anwendung bereit. </dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry-API: Die Komponente API stellt Informationen zu den internen Aktionen bereit, die aus der Anforderung eines Benutzers zum Ändern des Status einer Anwendung resultieren. </dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent: Die Komponente DEA stellt Informationen zum Start, Stopp oder Absturz einer Anwendung bereit.
<p>Diese Komponente ist nur verfügbar, wenn Ihre Anwendung in der Cloud Foundry-Architektur bereitgestellt wurde, die auf DEA basiert.</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Diego-Zelle: Die Komponente CELL stellt Informationen zum Start, Stopp oder Absturz einer Anwendung bereit.
<p>Diese Komponente ist nur verfügbar, wenn Ihre Anwendung in der Cloud Foundry-Architektur bereitgestellt wurde, die auf Diego basiert.</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH: Die Komponente SSH stellt jedes Mal Informationen bereit, wenn ein Benutzer auf eine Anwendung mit dem Befehl **cf ssh** zugreift.
<p>Diese Komponente ist nur verfügbar, wenn Ihre Anwendung in der Cloud Foundry-Architektur bereitgestellt wurde, die auf Diego basiert.</p></dd>

</dl>
</dd>

<dt><strong>Datenstrom</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Spalten: 42 - 44</p>
<p>Der Datenstrom, in den die Protokollnachricht geschrieben wird. <samp class="ph codeph">OUT</samp> bezeichnet den Datenstrom <samp class="ph codeph">stdout</samp> und <samp class="ph codeph">ERR</samp> den Datenstrom <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>Nachricht</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Nachricht</var>&gt;</code></pre>
<p>Spalten: 46 - bis Zeilenende</p>
<p>Die Nachricht, die von der Komponente ausgegeben wird. Die Nachricht variiert abhängig vom Kontext.</p>
</dd>
</dl>

Die folgende Abbildung zeigt die verschiedenen Komponenten (Protokolltypen) in einer Cloud Foundry-Architektur, die auf dem Droplet Execution Agent (DEA) basiert:
![Protokolltypen in einer DEA-Architektur.](images/logging_F1.png "Komponenten (Protokolltypen) in einer Cloud Foundry-Architektur, die auf dem Droplet Execution Agent (DEA) basiert.")


## Protokolle anzeigen
{: #viewing_logs}

Sie können die Protokolle für Ihre Cloud Foundry-Apps an vier Positionen anzeigen: 

  * {{site.data.keyword.Bluemix_notm}}-Dashboard
  * Kibana-Dashboard
  * Befehlszeilenschnittstelle (CLI)
  * Externe Protokollhosts

### Protokolle über das {{site.data.keyword.Bluemix_notm}}-Dashboard anzeigen
{: #viewing_logs_UI}

Führen Sie die folgenden Schritte aus, um die Bereitstellungs- oder Laufzeitprotokolle anzuzeigen: 
1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und klicken Sie auf die Kachel für Ihre App. Die App-Detailseite wird angezeigt. 
2. Klicken Sie in der Navigationsleiste auf **Protokolle**. 

In der Konsole **Protokolle** können Sie die letzten Protokolle für Ihre App oder Protokollendabschnitte in Echtzeit anzeigen. Darüber hinaus können Sie Protkolle nach Protokolltyp und Kanal filtern. 

**Hinweis:** Protokolle werden zwischen Abstürzen und Bereitstellungen von Apps nicht gespeichert. 


### Protokolle über das Kibana-Dashboard anzeigen
{: #viewing_logs_Kibana}

Erstellen Sie ein angepasstes Dashboard, um die Protokolle für die Apps, die in einem Bereich ausgeführt werden, auf einfache und kreative Weise anzuzeigen. 

1. Öffnen Sie [https://logmet.<span class="keyword" data-hd-keyref="DomainName">Domänenname</span>](https://logmet.{DomainName}), um sich bei der Kibana-Benutzerschnittstelle anzumelden.
2. Wählen Sie die Registerkarte **Kibana 3** aus. 
3. Wenn keine Protokolle angezeigt werden, passen Sie das Zeitauswahlfeld im Header an.
4. Speichern Sie das Dashboard als neues Dashboard. 
  1. Klicken Sie in der Symbolleiste auf das Symbol **Save** (Speichern).
  2. Geben Sie einen Namen für das Dashboard ein.
  3. Klicken Sie neben dem Namensfeld auf das Symbol **Save** (Speichern).

Weitere Informationen zur Anpassung eines Kibana-Dashboards finden Sie in [diesem Blogbeitrag](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/) oder in der Dokumentation zu [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).


### Protokolle über die Befehlszeilenschnittstelle anzeigen
{: #viewing_logs_cli}

Wählen Sie unter folgenden Optionen zum Anzeigen von Protokollen über die Befehlszeilenschnittstelle aus: 

<ul>
<li>Tailing-Protokolle beim Bereitstellen von Apps anzeigen.
<p>Verwenden Sie den Befehl **cf logs**, um Protokolle aus Ihrer App und aus den Systemkomponenten anzuzeigen, die mit Ihrer App interagieren, wenn Sie Apps in {{site.data.keyword.Bluemix_notm}} bereitstellen. Sie können die folgenden Befehle in der CF-Befehlszeilenschnittstelle eingeben. Weitere Informationen zum Befehl 'cf logs' finden Sie unter <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target=" _blank">Protokolltypen und zugehörige Nachrichten in Cloud Foundry <img src="../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. </p>
<dl>
<dt><strong>cf logs <var class="keyword varname">App-Name</var> --recent</strong></dt>
<dd>Zeigt Protokolle aus der jüngsten Vergangenheit an. </dd>

<dt><strong>cf logs <var class="keyword varname">App-Name</var></strong></dt>
<dd>Zeigt Protokolle an, die ab dem Moment generiert werden, in dem Sie diesen Befehl ausführen. </dd>
</dl>
<div class="note tip"><span class="tiptitle">Tipp:</span> Wenn Sie den Befehl <span class="keyword cmdname">cf push</span> oder <span class="keyword cmdname">cf start</span> in einem Befehlszeilenfenster ausführen, können Sie <samp class="ph codeph">cf logs App-Name --recent</samp> in einem anderen Befehlszeilenfenster eingeben, um die Protokolle in Echtzeit anzuzeigen. </div>
</li>

<li>Protokolle nach der Bereitstellung der Apps anzeigen.

<p>Wenn die Anwendungsprotokollierung aktiviert ist, können Sie die folgenden Anwendungsprotokolle anzeigen, falls während der Ausführung Probleme mit Ihrer App auftreten. Anwendungsprotokolle können Ihnen bei der Ermittlung der Fehlerursache helfen. </p>

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>Diese Protokolldatei zeichnet differenzierte Informationsereignisse für das Debugging auf. Sie können dieses Protokoll verwenden, um Probleme bei der Ausführung des Buildpacks zu beheben.</p>
<p>Wenn Daten in der Datei <span class="ph filepath">buildpack.log</span> generiert werden sollen, müssen Sie die Traceerstellung für Buildpacks mit dem folgenden Befehl aktivieren:
   <pre class="pre">cf set-env <var class="keyword varname">App-Name</var> JBP_LOG_LEVEL DEBUG</pre></p>
<p>Zum Anzeigen diesen Protokolls geben Sie den folgenden Befehl ein:
<pre class="pre">cf files <var class="keyword varname">App-Name</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>
<dt><strong>staging_task.log</strong></dt>
<dd><p>Diese Protokolldatei zeichnet Nachrichten nach den wichtigsten Schritten der Staging-Task auf. Mithilfe dieses Protokolls können Sie Probleme beim Staging beheben.</p>
<p>Zum Anzeigen diesen Protokolls geben Sie den folgenden Befehl ein:
<pre class="pre">cf files <var class="keyword varname">App-Name</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Hinweis:** Informationen zur Aktivierung der Anwendungsprotokollierung finden Sie unter [Laufzeitfehler beheben](/docs/debug/index.html#debugging-runtime-errors).

### Protokolle über externe Hosts anzeigen
{: #viewing_logs_external}


Wenn Protokolle generiert werden, können Sie nach kurzer Verzögerung Nachrichten auf Ihrem externen Host anzeigen, die den Nachrichten ähnlich sind, die Ihnen in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder über die CF-Befehlszeilenschnittstelle angezeigt werden. Wenn Sie mehrere Instanzen Ihrer App haben, werden die Protokolle zusammengefasst, sodass Sie alle Protokolle für Ihre App prüfen können. Darüber hinaus werden die Protokolle zwischen Abstürzen und Bereitstellungen von Apps persistent gespeichert. 

**Hinweis:** Protokolle, die Sie über die Befehlszeile anzeigen, haben nicht das Syslog-Format und entsprechen möglicherweise nicht exakt den Nachrichten, die auf Ihrem externen Protokollhost angezeigt werden. 




## Protokolle über die Befehlszeilenschnittstelle filtern
{: #filtering_logs}

Zum Anzeigen von für Sie relevanten Protokollen oder zum Ausschließen des Inhalts, den Sie nicht anzeigen möchten, können Sie den Befehl **cf logs** mit Filteroptionen wie **cut** und **grep** in der CF-Befehlszeilenschnittstelle verwenden. 

* Zum Anzeigen nur eines Teils anstelle der vollständigen und ausführlichen Protokolle verwenden Sie die Option **cut**. Verwenden Sie zum Beispiel den folgenden Befehl, um die Komponenten- und Nachrichteninformationen anzuzeigen: 
```
cf logs App-Name --recent | cut -c 29-40,46-
```

Weitere Informationen zur Option **grep** können Sie durch Eingabe von 'cut --help' abrufen. 
* Zum Anzeigen von Protokolleinträgen, die bestimmte Schlüsselwörter enthalten, verwenden Sie die Option **grep**. Protokolleinträge, die das Schlüsselwort `[APP` enthalten, können Sie beispielsweise mithilfe des folgenden Befehls anzeigen: 

```
cf logs appname --recent | grep '\[App'
```
Weitere Informationen zur Option **grep** können Sie mit `grep --help` abrufen.



## Externe Protokollhosts konfigurieren
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} bewahrt eine begrenzte Menge an Protokolldaten im Speicher. Bei der Protokollierung von Daten werden die alten Informationen durch die neueren Daten ersetzt. Zur Aufbewahrung aller Protokolldaten können Sie Ihre Protokolle auf einem externen Protokollhost, wie zum Beispiel in einem Protokoll-Management-Service eines anderen Anbieters, oder auf einem anderen Host speichern. 

Führen Sie die folgenden Schritte aus, um Protokolle aus Ihrer App und dem System an einen externen Protokollhost zu übertragen: 

  1. Bestimmen Sie den Protokollierungsendpunkt.

	 Sie können Protokolle an einen Protokollaggregator eines Drittanbieters wie Papertrail, Splunk oder Sumologic senden. Sie können Protokolle auch an einen Syslog-Host, einen Syslog-Host mit TLS-Verschlüsselung (Transport Layer Security) oder an einen HTTP-POST-Endpunkt senden. Die Methoden zum Anfordern von Protokollierungsendpunkten sind für verschiedene Protokollhosts unterschiedlich.

  2. Erstellen Sie eine vom Benutzer bereitgestellte Serviceinstanz.

	 Verwenden Sie den Befehl `cf create-user-provided-service ` (oder die Kurzversion des Befehls `cups`), um eine vom Benutzer bereitgestellte Serviceinstanz zu erstellen:
	 ```
	 cf create-user-provided-service <Servicename> -l <Protokollierungsendpunkt>
	 ```
	 &lt;Servicename&gt;

	 Der Name der vom Benutzer bereitgestellten Serviceinstanz.

	 &lt;Protokollierungsendpunkt&gt;

	 Der Protokollierungsendpunkt, an den {{site.data.keyword.Bluemix_notm}} Protokolle sendet. In der folgenden Tabelle finden Sie Informationen zu den Werten, durch die die Variable *Protokollierungsendpunkt* in Ihrem Fall ersetzt werden kann:

	 <table>
	 <caption>Tabelle 1. Werte für Protokollierungsendpunkte</caption>
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
	 cf bind-service <App-Name> <Servicename>
	 ```
	 &lt;App-Name&gt;

	 Der Name Ihrer App.

	 &lt;Servicename&gt;

	 Der Name der vom Benutzer bereitgestellten Serviceinstanz.

  4. Führen Sie für die App ein erneutes Staging durch. Geben Sie `cf restage appname` ein, damit die Änderungen wirksam werden.


### Beispiel: Cloud Foundry-Anwendung durch Streaming an Splunk übertragen
{: #splunk}

In diesem Beispiel erstellt eine Entwicklerin namens Jane einen virtuellen Server unter Verwendung von IBM Virtual Servers Beta und dem Ubuntu-Image. Jane versucht, die Cloud Foundry-App-Protokolle aus {{site.data.keyword.Bluemix_notm}} an Splunk durch Streaming zu übertragen.


  1. Zu Anfang richtet Jane Splunk ein. 

     a. Jane lädt Splunk Light von der Website [Download von Splunk Light ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} herunter und installiert das Produkt mithilfe des folgenden Befehls. Die Software wird in */opt/splunk* installiert. 

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane installiert und aktualisiert das Add-on RFC5424 für Syslog-Technologie, um Splunk in {{site.data.keyword.Bluemix_notm}} zu integrieren. Weitere Informationen zu den Anweisungen für die Installation des Add-ons finden Sie in der [Cloud Foundry-Anleitung ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jane installiert das Add-on mithilfe der folgenden Befehle: 

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        Anschließend aktualisiert Jane das Add-on, indem Sie die Datei */opt/splunk/etc/apps/rfc5424/default/transforms.conf* durch eine neue Datei *transforms.conf* ersetzt, die den folgenden Text enthält: 

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. Nach der Einrichtung von Splunk muss Jane einige Ports auf der Ubuntu-Maschine öffnen, um den eingehenden Syslog-Drain (Port 5140) und die Splunk-Webbenutzerschnittstelle (Web UI: Port 8000) zu akzeptieren, weil die Firewall für den virtuellen {{site.data.keyword.Bluemix_notm}}-Server standardmäßig konfiguriert ist. 

	    **Hinweis:** Die Konfiguration der IP-Tabelle ('iptable') erfolgt hier zu Auswertungszwecken für Jane und ist temporär. Details zur Konfiguration der Firewalleinstellung in der Produktionsumgebung des virtuellen Bluemix-Servers finden Sie in der Dokumentation [Network Security Groups ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window}. 

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   Dann führt Jane Splunk mit dem folgenden Befehl aus: 

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane konfiguriert die Splunk-Einstellungen so, dass der Syslog-Drain aus {{site.data.keyword.Bluemix_notm}} akzeptiert wird. Sie muss eine Dateneingabe für den Syslog-Drain erstellen. 

     a. Jane klickt in der Splunk-Webschnittstelle auf **Data > Data inputs**. Eine Liste der von Splunk unterstützten Eingabetypen wird angezeigt. 

     b. Sie wählt **TCP** aus, weil der Syslog-Drain das TCP-Protokoll verwendet. 

     c. Im Fenster **TCP** gibt sie in das Feld **Port** den Wert **5140** ein und lässt die übrigen Felder leer. Anschließend klickt sie auf **Next**. 

     d. In der Liste **Source Type** wählt Sie den Quellentyp **Uncategorized > rfc5424_syslog** aus. 

     e. Für den Typ im Feld **Method** wählt sie **IP** aus. 

     f. Im Feld **Index** klickt sie auf **Create a new index**. Sie gibt dem neuen Index den Namen "bluemix" und klickt auf **Save**. 

     g. Schließlich bestätigt Jane im Fenster **Review**, dass die Einstellung korrekt ist, und klickt auf **Submit**, um diese Dateneingabe zu aktivieren. 

  3. In {{site.data.keyword.Bluemix_notm}} erstellt Jane einen Syslog-Drain-Service und bindet den Service an eine App. 

     a. Jane erstellt den Syslog-Drain-Service mithilfe des folgenden Befehls über die CF-CLI: 

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Hinweis:** *dummyhost* ist nicht der reale Name. Dies dient zur Verschleierung des tatsächlichen Hostnamens. 

     b. Jane bindet den Syslog-Drain-Service an eine App in ihrem Bereich und führt ein erneutes Staging der App durch. 

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane probiert ihre App aus und gibt anschließend die folgende Abfragezeichenfolge in der Splunk-Webschnittstelle ein: 

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane wird ein Datenstrom von Protokollen in ihrer Splunk-Webschnittstelle angezeigt. Obwohl Jane Splunk Light installiert hat, kann sie 500 MB an Protokollen pro Tag aufbewahren. 

## Protokollierung für Cloud Foundry-Apps in {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}}
{: #hybrid_apps_logs_ov}


In {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} werden Cloud Foundry-Apps mit integrierter Protokollierung bereitgestellt. Die Daten, die aus Ihren Apps erfasst werden, können Sie in der {{site.data.keyword.Bluemix_notm}}-Konsole prüfen.
{:shortdesc}

Cloud Foundry-Apps verwenden Cloud Foundry Loggregator, um Protokolle außerhalb der App zu überwachen und weiterzuleiten. Innerhalb der App müssen keine Agenten installiert werden.

### Hardwarevoraussetzungen


| **Voraussetzung** |    **1 Knoten**     | **3 Knoten für Hochverfügbarkeit** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| Hauptspeicher | 80 GB | 240 GB |
| Lokaler Speicher | 2,98 TB | 8,94 TB |
{: caption="Tabelle 2. Hardwarevoraussetzungen für die Protokollierung für {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

### Konfiguration

In {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} sind Protokolle standardmäßig für alle Apps aktiv. Informationen zum Lesen der Standardprotokolle finden Sie unter [Protokollierung für Apps, die in Cloud Foundry ausgeführt werden](#logging_for_bluemix_apps). In Umgebungen mit {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} kann darüber hinaus eine erweiterte Protokollierung aktiviert werden.

* Zum Aktivieren der erweiterten Protokollierung in Ihrer {{site.data.keyword.Bluemix_dedicated_notm}}- und {{site.data.keyword.Bluemix_local_notm}}-Umgebung führen Sie die Schritte im Abschnitt [Protokolle anzeigen](#hybrid_apps_logs_dash) aus. Falls die Schaltfläche **Erweiterte Ansicht** nicht angezeigt wird, ist diese Funktion nicht aktiviert.

* Die Schritte, mit denen Sie die erweiterte Protokollierung zu Ihrer Umgebung hinzufügen, sind in der Dokumentation für [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) bzw. [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local) beschrieben.

### Protokollspeicherung

In {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} werden Protokolldaten für Cloud Foundry-Apps standardmäßig 30 Tage gespeichert.

## Protokolle für Cloud Foundry-Apps in {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} anzeigen
{: #hybrid_apps_logs_dash}

Für die Apps, die Sie unter {{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}} ausführen, können Sie Protokolle prüfen.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um die Protokolle für Ihre Apps anzuzeigen.
1. Wählen Sie eine aktive App aus.
2. Klicken Sie auf **Protokolle**. In der Ansicht **Protokolle** können Sie die Protokolle für Ihre aktive App einsehen.
4. Klicken Sie auf die Schaltfläche **Erweiterte Ansicht**. Die **erweiterte Ansicht** zeigt mehr Details der Protokolle und verwendet hierzu Kibana, ein Visualisierungstool, das mithilfe von Protokollen und Daten mit Zeitmarken angepasste Visualisierungen erstellt. Weitere Informationen zur Verwendung der erweiterten Ansicht enthält die Dokumentation zu [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Als Nächstes können Sie ein Kibana-Dashboard anpassen. Weitere Informationen finden Sie unter [Anzeige von Protokollen in einem Kibana-Dashboard anpassen](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom).
