---

copyright:
  years: 2015, 2017

lastupdated: "2017-01-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Überwachung und Protokollierung mit Cloud Foundry
{: #monitoringandlogging}


Indem Sie Ihre Apps überwachen und Protokolle überprüfen, können Sie die Anwendungsausführung und den Datenfluss verfolgen, um Ihre Bereitstellung besser zu verstehen. Darüber hinaus können Sie die Zeit und den Aufwand für das Auffinden und Beheben von Problemen reduzieren.
{:shortdesc}

Bei {{site.data.keyword.Bluemix}}-Anwendungen kann es sich um weit verteilte Anwendungen mit mehreren Instanzen handeln und die Ausführung Ihrer Anwendung mitsamt der zugehörigen Daten kann von vielen verschiedenen Services übernommen werden. In einer solchen komplexen Umgebung ist das Überwachen Ihrer Apps und das Überprüfen von Protokollen von zentraler Bedeutung für das Verwalten Ihrer Apps.

## Cloud Foundry-Apps für Überwachung und Protokollierung
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}} hat einen integrierten Protokolliermechanismus, um Protokolldateien für Ihre Apps zu erstellen, während sie ausgeführt werden. In den Protokollen können Sie die Fehler, Warnungen und Informationsnachrichten sehen, die für Ihre App erzeugt werden. Sie können Ihre App auch so konfigurieren, dass Protokollnachrichten in die Protokolldatei geschrieben werden. Weitere Informationen zu Protokollformaten und zur Anzeige von Protokollen finden Sie unter [Protokollierung für Apps, die in Cloud Foundry ausgeführt werden](#logging_for_bluemix_apps).

Durch die Überwachung Ihrer App können Sie Ihre App-Bereitstellung anzeigen und steuern. Mithilfe der Überwachung können Sie die folgenden Tasks ausführen:

* Sammeln und überwachen Sie die Leistungsinformationen für App-Instanzen und prüfen Sie, ob diese funktional sind.
* Gewinnen Sie Einblick in Anwendungsoperationen - erkennen Sie beispielsweise potenzielle Engpässe oder stellen Sie fest, wann Upgrades erforderlich sind.
* Prognostizieren Sie die Ressourcennutzung und die anfallenden Gebühren.

Für einen stabilen Betrieb Ihrer Bereitstellungen auf der {{site.data.keyword.Bluemix_notm}}-Plattform möchten Sie Probleme schnell erkennen und Ursachen effizient bestimmen. Dieses Ziel erreichen Sie, wenn Sie bei der Konzeption Ihrer Apps die Fehlerbehebung im Hinterkopf behalten und Services oder Tools für die Überwachung und Protokollierung verwenden, wenn Ihre App in {{site.data.keyword.Bluemix_notm}} bereitgestellt wird.

### Überwachung von Apps, die in Cloud Foundry ausgeführt werden
{: #monitoring_bluemix_apps}

Wenn Sie die Cloud Foundry-Infrastruktur verwenden, um Ihre Apps in {{site.data.keyword.Bluemix_notm}} auszuführen, sollten Sie über die Leistungsinformationen, wie z. B. Allgemeinzustand, Ressourcennutzung und Datenverkehr, auf dem Laufenden bleiben. Anhand dieser Leistungsinformationen können Sie Entscheidungen treffen oder Maßnahmen ergreifen.

Wenden Sie eine der folgenden Methoden an, um {{site.data.keyword.Bluemix_notm}}-Apps zu überwachen:

* {{site.data.keyword.Bluemix_notm}}-Services. Monitoring and Analytics bietet einen Service, den Sie zur Überwachung Ihrer Anwendungsleistung verwenden können. Dieser Service bietet nun auch Analysefunktionen wie die Protokollanalyse. Weitere Informationen finden Sie unter [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate).
* Optionen von Drittanbietern. Beispiel: [New Relic
![Symbol für externen Link](../icons/launch-glyph.svg)](http://newrelic.com/){:new_window}.

### Protokollierung für Apps, die in Cloud Foundry ausgeführt werden
{: #logging_for_bluemix_apps}

Protokolldateien werden automatisch erstellt, wenn Sie die Cloud Foundry-Infrastruktur verwenden, um Ihre Apps in {{site.data.keyword.Bluemix_notm}} auszuführen. Wenn in einer der Phasen von der Entwicklung bis zur Laufzeit Fehler auftreten, können Sie die Protokolle auf Hinweise prüfen, die Ihnen bei der Lösung des Problems möglicherweise helfen.


<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



### Protokollformat und -aufbewahrungsdauer
{: #log_format}

In den {{site.data.keyword.Bluemix_notm}} Public Cloud Foundry-Apps werden die Protokolldaten standardmäßig 7 Tage lang gespeichert.

Protokolle für {{site.data.keyword.Bluemix_notm}}-Anwendungen werden in einem festen Format angezeigt, ähnlich dem folgenden Muster:

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
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

### Protokolle anzeigen
{: #viewing_logs}

Sie können die Protokolle für Ihre Cloud Foundry-Apps an vier Positionen anzeigen:

  * {{site.data.keyword.Bluemix_notm}}-Dashboard
  * Dashboard
  * Befehlszeilenschnittstelle
  * Externe Protokollhosts

#### Protokolle im {{site.data.keyword.Bluemix_notm}}-Dashboard anzeigen
{: #viewing_logs_UI}

Führen Sie die folgenden Schritte aus, um die Bereitstellungs- oder Laufzeitprotokolle anzuzeigen:
1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und klicken Sie dann auf die Kachel für Ihre App. Daraufhin wird die Detailseite der App angezeigt.
2. Klicken Sie in der Navigationsleiste auf **Protokolle**.

In der Konsole für **Protokolle** können Sie die kürzlich generierten Protokolle für Ihre App oder Protokollendabschnitte in Echtzeit anzeigen. Darüber hinaus können Sie Protokolle nach Protokolltyp und Kanal filtern.

**Hinweis:** Protokolle werden nicht über App-Abstürze und App-Bereitstellungen hinweg gespeichert.


#### Protokolle im Kibana-Dashboard anzeigen
{: #viewing_logs_Kibana}

Erstellen Sie ein angepasstes Dashboard, in dem die Protokolle für in einem Bereich ausgeführte Apps auf einfache oder kreative Weise angezeigt werden sollen.

1. Öffnen Sie [https://logmet.<span class="keyword" data-hd-keyref="DomainName">Domänenname</span>](https://logmet.{DomainName}), um sich bei der Kibana-Benutzerschnittstelle anzumelden.
2. Wählen Sie die Registerkarte **Kibana 3** aus.
3. Wenn keine Protokolle angezeigt werden, passen Sie das Zeitauswahlfeld im Header an.
4. Speichern Sie das Dashboard als neues Dashboard.
  1. Klicken Sie in der Symbolleiste auf das Symbol **Speichern**.
  2. Geben Sie einen Namen für das Dashboard ein.
  3. Klicken Sie neben dem Namensfeld auf das Symbol **Speichern**.

Weitere Informationen zum Anpassen eines Kibana-Dashboards finden Sie in [diesem Blogbeitrag ![Symbol für externen Link](../icons/launch-glyph.svg)](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} oder in der Dokumentation zu [Kibana ![Symbol für externen Link](../icons/launch-glyph.svg)](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.


#### Protokolle über die Befehlszeilenschnittstelle anzeigen
{: #viewing_logs_cli}

Wählen Sie eine der folgenden Optionen zum Anzeigen von Protokollen über die Befehlszeilenschnittstelle aus:

<ul>
<li>Tailing-Protokolle beim Bereitstellen von Apps.
<p>Verwenden Sie den Befehl **cf logs**, um Protokolle aus Ihrer App und aus den Systemkomponenten anzuzeigen, die mit Ihrer App interagieren, wenn Sie Apps in {{site.data.keyword.Bluemix_notm}} bereitstellen. Sie können die folgenden Befehle in die Befehlszeilenschnittstelle 'cf' eingeben. Weitere Informationen zum Befehl 'cf logs' finden Sie in der Beschreibung der <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target=" _blank">Protokolltypen und ihrer Nachrichten in Cloud Foundry <img src="../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>. </p>
<dl>
<dt><strong>cf logs <var class="keyword varname">App-Name</var> --recent</strong></dt>
<dd>Zeigt kürzlich erstellte Protokolle an.</dd>

<dt><strong>cf logs <var class="keyword varname">App-Name</var></strong></dt>
<dd>Zeigt Protokolle an, die in dem Moment generiert werden, in dem Sie diesen Befehl eingeben.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Tipp:</span> Wenn Sie den Befehl <span class="keyword cmdname">cf push</span> oder <span class="keyword cmdname">cf start</span> in einem Befehlszeilenfenster ausführen, können Sie <samp class="ph codeph">cf logs App-Name --recent</samp> in einem anderen Befehlszeilenfenster eingeben, um die Protokolle in Echtzeit anzuzeigen. </div>
</li>

<li>Protokolle anzeigen, nachdem die Apps bereitgestellt wurden.

<p>Wenn die Anwendungsprotokollierung aktiviert ist, können Sie die folgenden Anwendungsprotokolle anzeigen, falls Probleme mit Ihrer App während der Laufzeit auftreten. Mithilfe von Anwendungsprotokollen lässt sich die Ursache eines Fehlers einfacher bestimmen.</p>

<dl>
<dt><strong>buildpack.log</strong></dt>
<dd>
<p>Diese Protokolldatei zeichnet differenzierte Informationsereignisse für das Debugging auf. Sie können dieses Protokoll verwenden, um Probleme bei der Ausführung des Buildpacks zu beheben.</p>
<p>Wenn Daten in der Datei <span class="ph filepath">buildpack.log</span> generiert werden sollen, müssen Sie die Traceerstellung für Buildpacks aktivieren, indem Sie den folgenden Befehl ausführen:
   <pre class="pre">cf set-env <var class="keyword varname">App-Name</var> JBP_LOG_LEVEL DEBUG</pre>
</p>
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


**Hinweis:** Informationen zur Aktivierung der Anwendungsprotokollierung finden Sie unter [Laufzeitfehler beheben](/docs/debug/index.html#debugging-runtime-errors).

#### Protokolle in externen Hosts anzeigen
{: #viewing_logs_external}


Wenn Protokolle generiert werden, können Sie nach einer kurzen Verzögerung Nachrichten in Ihrem externen Protokollhost anzeigen, die den Nachrichten ähnlich sind, die Sie über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle oder über die Befehlszeilenschnittstelle 'cf' anzeigen.  Wenn Sie über mehrere Instanzen Ihrer App verfügen, werden die Protokolle zusammengefasst und Sie können alle Protokolle für Ihre App anzeigen. Darüber hinaus werden die Protokolle über App-Abstürze und App-Bereitstellungen hinweg gespeichert.

**Hinweis:** Protokolle, die Sie über die Befehlszeilenschnittstelle anzeigen, haben nicht das Syslog-Format und stimmen daher möglicherweise nicht genau mit den Nachrichten überein, die in Ihren externen Protokollhost angezeigt werden.




### Protokolle filtern
{: #filtering_logs}

Zum Anzeigen von für Sie relevanten Protokollen oder zum Ausschließen des Inhalts, den Sie nicht anzeigen möchten, können Sie den Befehl **cf logs** mit Filteroptionen wie **cut** und **grep** in der Befehlszeilenschnittstelle 'cf' verwenden.

* Wenn Sie nur einen Teil statt des gesamten ausführlichen Protokolls anzeigen möchten, verwenden Sie die Option **cut**. Geben Sie beispielsweise den folgenden Befehl ein, um die Komponenten- und Nachrichteninformationen anzuzeigen:
```
cf logs App-Name --recent | cut -c 29-40,46-
```

Für weitere Informationen zur Option **cut** geben Sie 'cut --help' ein.
* Zum Anzeigen von Protokolleinträgen, die bestimmte Schlüsselwörter enthalten, verwenden Sie die Option **grep**. Protokolleinträge, die das Schlüsselwort `[APP` enthalten, können Sie beispielsweise mithilfe des folgenden Befehls anzeigen:

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

	 Verwenden Sie den Befehl `cf create-user-provided-service ` (oder die Kurzversion des Befehls `cups`), um eine vom Benutzer bereitgestellte Serviceinstanz zu erstellen:
	 ```
	 cf create-user-provided-service <Servicename> -l <Protokollierungsendpunkt>
	 ```
	 &lt;Servicename&gt;

	 Der Name der vom Benutzer bereitgestellten Serviceinstanz.

	 &lt;Protokollierungsendpunkt&gt;

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
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;Appname&gt;

	 Der Name Ihrer App.

	 &lt;Servicename&gt;

	 Der Name der vom Benutzer bereitgestellten Serviceinstanz.

  4. Führen Sie für die App ein erneutes Staging durch. Geben Sie `cf restage appname` ein, damit die Änderungen wirksam werden.


### Beispiel: Streaming von Cloud Foundry-Anwendungsprotokollen in Splunk
{: #splunk}

In diesem Beispiel erstellt die Entwicklerin Jane einen virtuellen Server unter Verwendung von IBM Virtual Servers Beta und des Ubuntu-Image.  Die Cloud Foundry-Anwendungsprotokolle sollen per Streaming von {{site.data.keyword.Bluemix_notm}} in Splunk übertragen werden.

  1. Zunächst muss Splunk von Jane installiert werden.

     a. Jane lädt Splunk Light von der [Download-Site für Splunk Light ![Symbol für externen Link](../icons/launch-glyph.svg)](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} herunter und installiert das Programm mithilfe des folgenden Befehls. Die Software wird in */opt/splunk* installiert.

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane installiert und korrigiert das RFC5424-Add-on der syslog-Technologie für die Integration mit {{site.data.keyword.Bluemix_notm}}. Weitere Informationen zur Installation des Add-ons finden Sie in der
[Cloud Foundry-Richtlinie ![Symbol für externen Link](../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jane installiert das Add-on mithilfe der folgenden Befehle:

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        Anschließend korrigiert Jane das Add-on, indem sie */opt/splunk/etc/apps/rfc5424/default/transforms.conf* durch eine neue Datei *transforms.conf* ersetzt, die den folgenden Text enthält:

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

     Nach der Installation von Splunk muss Jane einige Ports auf der Ubuntu-Maschine öffnen, damit der eingehende syslog-Drain (Port 5140) und die Splunk-Webbenutzerschnittstelle (Port 8000) akzeptiert werden, da für den virtuellen {{site.data.keyword.Bluemix_notm}}-Server standardmäßig eine Firewall eingerichtet ist.

	    **Hinweis:** Die hier vorgenommene iptable-Konfiguration dient nur zu Testzwecken und ist temporär. Einzelheiten zum Konfigurieren der Firewalleinstellung auf dem virtuellen Bluemix-Server in einer Produktionsumgebung finden Sie in der Dokumentation zu [Network Security Groups
![Symbol für externen Link](../icons/launch-glyph.svg)](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window}.

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   Anschließend startet Jane die Ausführung von Splunk mithilfe des folgenden Befehls:

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane konfiguriert die Splunk-Einstellungen, um den syslog-Drain von {{site.data.keyword.Bluemix_notm}} zu akzeptieren. Für den syslog-Drain muss eine Dateneingabe erstellt werden.

     a. Jane klickt auf der Splunk-Webschnittstelle auf **Data > Data inputs**. Eine Liste der von Splunk unterstützten Eingabetypen wird angezeigt.

     b. Jane wählt **TCP** aus, da der syslog-Drain das TCP-Protokoll verwendet.

     c. Im Teilfenster **TCP** gibt sie **5140** in das Feld **Port** ein, lässt die verbleibenden Felder leer und klickt dann auf **Next**.

     d. In der Liste **Source Type** wählt Jane **Uncategorized > rfc5424_syslog** aus.

     e. Als Methodentyp wählt sie **IP** aus.

     f. Im Feld **Index** klickt Jane auf **Create a new index**. Sie ordnet dem Index den Namen 'bluemix' zu und klickt dann auf **Save**.

     g. Zuletzt bestätigt Jane im Fenster **Review**, dass die Einstellung korrekt ist. Dann klickt sie auf **Submit**, um die Dateneingabe zu aktivieren.

  3. In {{site.data.keyword.Bluemix_notm}} erstellt Jane einen syslog-Drain-Service und bindet den Service an eine App.

     a. Jane erstellt den syslog-Drain-Service in der Befehlszeilenschnittstelle 'cf' unter Verwendung des folgenden Befehls:

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Hinweis:** *dummyhost* ist nicht der richtige Name. Er wird verwendet, um den tatsächlichen Hostnamen zu verdecken.

     b. Jane bindet den syslog-Drain-Service an eine App in ihrem Bereich und führt dann ein erneutes Staging für die App aus.

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane testet die App und gibt dann die folgende Abfragezeichenfolge in die Splunk-Webschnittstelle ein:

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

In der Splunk-Webschnittstelle wird ein Protokolldatenstrom angezeigt. Obwohl nur Splunk Light installiert wurde, kann eine Protokollmenge von 500 MB pro Tag gespeichert werden.

## Protokollierung für Cloud Foundry-Apps in
{{site.data.keyword.Bluemix_dedicated_notm}} und {{site.data.keyword.Bluemix_local_notm}}
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
{: caption="Table 1. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

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
4. Klicken Sie auf die Schaltfläche **Erweiterte Ansicht**. Die **erweiterte Ansicht** zeigt mehr Details der Protokolle und verwendet hierzu Kibana, ein Visualisierungstool, das mithilfe von Protokollen und Daten mit Zeitmarken angepasste Visualisierungen erstellt. Weitere Informationen zur Verwendung der erweiterten Ansicht enthält die Dokumentation zu [Kibana ![Symbol für externen Link](../icons/launch-glyph.svg)](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window}.

Als nächstes können Sie ein Kibana-Dashboard anpassen. Weitere Informationen finden Sie unter [Anzeige von Protokollen in einem Kibana-Dashboard anpassen](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom).
