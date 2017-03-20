---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# CF-App-Protokolle über das Bluemix-Dashboard analysieren
{: #analyzing_logs_bmx_ui}

In {{site.data.keyword.Bluemix}} können Sie Protokolle über die Registerkarte **Protokolle** anzeigen, filtern und analysieren, die für jede Cloud Foundry-Anwendung verfügbar ist. Im {{site.data.keyword.Bluemix}}-Dashboard können Sie die letzte Aktivität der Anwendung analysieren.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Public bietet einen integrierten Protokollierungsserivce an. Wenn Sie Ihre Anwendungen in Cloud Foundry ausführen, erfasst der Protokollierungsservice (Logging) aus Systemkomponenten, die mit Ihrer Anwendung interagieren, Protokolldaten zu Ihrer Anwendung und sogar Protokolldaten aus Ihrer Anwendung, wenn Sie die Standardausgabe (STDOUT) und die Standard-Fehlerausgabe (STDERR) verwenden. 

Protokolle für {{site.data.keyword.Bluemix_notm}}-Anwendungen werden in einem festen Format angezeigt, ähnlich dem folgenden Muster:

<code><var class="keyword varname">Komponente</var>/<var class="keyword varname">Instanz-ID</var>     <var class="keyword varname">Nachricht</var>     <var class="keyword varname">Zeitmarke</var></code>
   
Weitere Informationen zum Protokollformat finden Sie unter [Protokollformat für Cloud Foundry-App-Protokolle](logging_view_dashboard.html#log_format_cf).

**Hinweis:** In {{site.data.keyword.Bluemix_notm}} Public werden Protokolldaten standardmäßig sieben 7 Tage lang gespeichert. Sie können bis zu 1 GB an Daten pro Tag durchsuchen.



##  Bluemix-Protokollregisterkarte öffnen
{: #launch_logs_tab_bmx_ui}

Führen Sie die folgenden Schritte aus, um Bereitstellungs- oder Laufzeitprotokolle einer Cloud Foundry-Anwendung anzuzeigen:

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und klicken Sie auf den App-Namen im {{site.data.keyword.Bluemix_notm}}-Dashboard **Apps**.  

    Die Detailseite für die App wird angezeigt.
    
2. Klicken Sie in der Navigationsleiste auf **Protokolle**.

    Die Registerkarte für Protokolle wird geöffnet. 
    
    Auf der Registerkarte **Protokolle** können Sie die zuletzt generierten Protokolle für Ihre App oder Protokollendabschnitte in Echtzeit anzeigen. Darüber hinaus können Sie Protokolle nach Komponente (Protokolltyp), App-Instanz-ID und nach Fehler filtern.



## Protokollformat für Cloud Foundry-App-Protokolle
{: #log_format_cf}

Jeder Protokolleintrag enthält die folgenden Felder:

<dl>
<dt><strong>Zeitmarke</strong></dt>
<dd>
<p>Die Zeit der Protokollanweisung. Die Zeitmarke ist bis auf die Millisekunde definiert.</p>
</dd>

<dt><strong>Komponente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Die Komponente, die das Protokoll generiert. </p>
<p>Auf jeden Komponententyp folgt ein Schrägstrich und eine Ziffer, die die Anwendungsinstanz angibt. 0 ist die Ziffer, die der ersten Instanz zugeordnet ist, 1 die der zweiten usw. Beachten Sie, dass Sie filtern können, um nur eine App-Instanz im Dashboard anzuzeigen. </p>
<p>In der folgenden Liste werden die verschiedenen Typen von Komponenten kurz beschrieben: </p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: Die LGR-Komponente stellt Informationen über den Cloud Foundry Loggregator bereit, der Protokolle aus Cloud Foundry heraus weiterleitet. </dd>

<dt><strong>RTR</strong></dt>
<dd>Router: Die RTR-Komponente stellt Informationen zu HTTP-Anforderungen an eine Anwendung bereit. </dd>

<dt><strong>STG</strong></dt>
<dd>Staging: Die STG-Komponente stellt Informationen zum Staging und erneuten Staging einer Anwendung bereit. </dd>

<dt><strong>APP</strong></dt>
<dd>Anwendung: Die APP-Komponente stellt Protokolle aus der Anwendung bereit. Hier wird die Standard-Fehlerausgabe (STDERR) und die Standardausgabe (STDOUT) in Ihrem Code angezeigt.
</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry-API: Die API-Komponente stellt Informationen zu den internen Aktionen bereit, die aus der Anforderung eines Benutzers zum Ändern des Status einer Anwendung resultieren.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent: Die DEA-Komponente stellt Informationen zum Start, Stopp oder Absturz einer Anwendung bereit.
<p>Diese Komponente ist nur verfügbar, wenn Ihre Anwendung in der Cloud Foundry-Architektur bereitgestellt wurde, die auf DEA basiert. </p></dd>

<dt><strong>CELL</strong></dt>
<dd>Diego-Zelle: Die CELL-Komponente stellt Informationen zum Start, Stopp oder Absturz einer Anwendung bereit.
<p>Diese Komponente ist nur verfügbar, wenn Ihre Anwendung in der Cloud Foundry-Architektur bereitgestellt wurde, die auf Diego basiert. </p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH: Die SSH-Komponente stellt jedes Mal Informationen bereit, wenn ein Benutzer auf eine Anwendung mit dem Befehl **cf ssh** zugreift.
<p>Diese Komponente ist nur verfügbar, wenn Ihre Anwendung in der Cloud Foundry-Architektur bereitgestellt wurde, die auf Diego basiert. </p></dd>

</dl>
</dd>

<dt><strong>Nachricht</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Nachricht</var>&gt;</code></pre>
<p>Die Nachricht, die von der Komponente ausgegeben wird. Die Nachricht variiert abhängig vom Kontext.</p>
</dd>
</dl>

Die folgende Abbildung zeigt die verschiedenen Komponenten (Protokolltypen) in einer Cloud Foundry-Architektur, die auf dem Droplet Execution Agent (DEA) basiert:
![Protokolltypen in einer Cloud Foundry-Architektur auf DEA-Basis.](images/logging_F1.png "Komponenten (Protokolltypen") in einer Cloud Foundry-Architektur, die auf dem Droplet Execution Agent (DEA) basiert.")



