---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokolle in Kibana analysieren
{: #analyzing_logs_Kibana3}

In {{site.data.keyword.Bluemix}} können Sie Kibana, eine quelloffene Analyse- und Visualisierungsplattform, dazu verwenden, Ihre Daten in einer Reihe von Darstellungsarten, wie zum Beispiel Diagrammen und Tabellen, zu überwachen, zu durchsuchen, zu analysieren und zu visualisieren. Verwenden Sie Kibana für erweiterte Analysetasks.
{:shortdesc}

Sie können Kibana auf eine beliebige der folgenden Arten starten:

* Über das Cloud Foundary-Dashboard 'App'

    Sie können Ihre CF-App-Protokolle in Kibana im Kontext der jeweiligen App starten.
    
    Die Abfrage, die zum Filtern der im Dashboard angezeigten Daten verwendet wird, ruft Protokolleinträge für die Cloud Foundry-Anwendung ab. Die Protokollinformationen, die standardmäßig im Kibana-Dashboard angezeigt werden, beziehen sich sämtlich auf eine einzelne Cloud Foundry-Anwendung und alle zugehörigen Instanzen. Weitere Informationen finden Sie unter [Kibana-Dashboard über das {{site.data.keyword.Bluemix}}-Dashboard aufrufen](logging_view_kibana3.html#launch_Kibana_from_bluemix).

* Über einen direkten Browser-Link

    Sie können ein angepasstes Kibana-Dashboard starten, das Daten aus Services in einem bereitgestellten {{site.data.keyword.Bluemix}}-Bereich zusammenfasst.
    
    Die Abfrage, durch die die Daten gefiltert werden, die im Dashboard angezeigt werden, ruft Protokolleinträge für einen Bereich in der {{site.data.keyword.Bluemix}}-Organisation ab. Die Protokollinformationen, die im Kibana-Dashboard angezeigt werden, umfassen Einträge für alle Ressourcen, die innerhalb des Bereichs der {{site.data.keyword.Bluemix}}-Organisation bereitgestellt wurden, an der Sie angemeldet sind. Weitere Informationen finden Sie unter [Kibana-Dashboard im Web-Browser aufrufen](logging_view_kibana3.html#launch_Kibana_from_browser).
    
    Sie können die Anfangsabfrage auch ändern oder entfernen und Sie können weitere Abfragen hinzufügen. Weitere Informationen finden Sie unter [Protokolle für Cloud Foundry-Apps mit Abfragen in Kibana filtern](kibana3/logging_kibana_query.html#logging_kibana_query).


Kibana ist eine browserbasierte Schnittstelle, in der Sie Dashboards anpassen können, mit denen Sie anschließend Protokolldaten analysieren und erweiterte Management-Tasks durchführen können. 

In {{site.data.keyword.Bluemix}} können Sie Daten mithilfe des Kibana-Standarddashboards analysieren, das für jede Cloud Foundry-App und für jeden Bereich Ihrer Organisation verfügbar ist. Diese Dashboards zeigen standardmäßig alle Daten, die für die letzten 24 Stunden verfügbar sind, in einer Anzeige an, die eine Zeile mit einem Histogramm und eine Zeile mit einer Ereignistabelle enthält. 

Wenn Sie die Informationen, die durch ein Standarddashboard angezeigt werden, eingrenzen möchten, können Sie dem Standarddashboard Abfragen und Filter hinzufügen. Anschließend können Sie das Dashboard zur künftigen Wiederverwendung speichern. 

Die Daten, die in einem Kibana-Dashboard angezeigt werden, werden durch die Abfrage gesteuert. Zum Ändern der in einem Dashboard angezeigten Informationen können Sie die Abfrage ändern, weitere Abfragen hinzufügen und das Dashboard anschließend speichern. Sie können mehrere Dashboards gleichzeitig anpassen, speichern und zur gemeinsamen Nutzung freigeben. Auf diese Weise kann Kibana zum Beispiel Informationen zu einer einzelnen App in Ihrem Bereich anzeigen.

Sie können darüber hinaus Filter für Protokollfelder wie zum Beispiel für Nachrichtentyp (message_type) und Instanz-ID (instance_ID) konfigurieren. Weitere Informationen finden Sie unter [Kibana-Protokollformat](logging_view_kibana3.html#kibana_log_format_cf). Sie können diese Filter dynamisch aktivieren oder inaktivieren. Das Dashboard zeigt die Protokolleinträge, die der Abfrage und den aktivierten Filterbedingungen entsprechen. Weitere Informationen finden Sie unter [Daten in einem Kibana-Dashboard filtern](logging_view_kibana3.html#filter_data_kibana_dashboard).

Sie können Anzeigen (Panels) zur Visualisierung der Daten konfigurieren. Kibana enthält verschiedene Anzeigen, wie zum Beispiel Anzeigen für Tabellen, Trends und Histogramme, die Sie zur Analyse der Informationen verwenden können. Sie können Anzeigen im Dashboard hinzufügen, entfernen und neu anordnen. Der Zweck jeder Anzeige variiert. Einige Anzeigen werden in Zeilen aufbereitet, in denen die Ergebnisse einer oder mehrerer Abfragen dargestellt werden. Andere Anzeigen enthalten Dokumente oder angepasste Informationen. Weitere Informationen finden Sie unter [Kibana-Dashboard anpassen](logging_view_kibana3.html#customize_kibana_dashboard).

Nach der Anpassung eines Dashboards können Sie beliebige der folgenden Aktionen auswählen:

* Sie können das Dashboard zur künftigen Wiederverwendung speichern. Weitere Informationen finden Sie unter [Kibana-Dashboard speichern](logging_view_kibana3.html#save_Kibana_dashboard).

* Sie können einen direkten Link zu einem Kibana-Dashboard exportieren und zur gemeinsamen Nutzung mit einem anderen Benutzer freigeben. Weitere Informationen finden Sie unter [Kibana-Dashboards exportieren und gemeinsam nutzen](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash).

* Sie können das Dashboard in eine Webseite integrieren. Ein Benutzer, der ein integriertes Dashboard anzeigen möchte, muss über eine Zugriffsberechtigung für Kibana verfügen.

Weitere Informationen finden Sie in der [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html)-Dokumentation.

**Hinweis:** Kibana 4 und Kibana 3 werden unterstützt. Kibana 3 ist veraltet.


##  Kibana-Dashboard über das Bluemix-Dashboard aufrufen
{: #launch_Kibana_from_bluemix}

Die Abfrage, die zum Filtern der im Dashboard angezeigten Daten verwendet wird, ruft Protokolleinträge für die Cloud Foundry-Anwendung ab. Die Protokollinformationen, die standardmäßig im Kibana-Dashboard angezeigt werden, beziehen sich sämtlich auf eine einzelne Cloud Foundry-Anwendung und alle zugehörigen Instanzen.

Führen Sie die folgenden Schritte aus, um die Protokolle einer Cloud Foundry-Anwendung in Kibana anzuzeigen:

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und klicken Sie auf den App-Namen im {{site.data.keyword.Bluemix_notm}}-Dashboard **Apps**. Die Seite mit den Anwendungsdetails wird geöffnet.
    
2. Klicken Sie in der Navigationsleiste auf **Protokolle**. Die Registerkarte für Protokolle wird geöffnet. 
    
3. Klicken Sie auf **Erweiterte Ansicht**. Das Dashboard **Kibana 3** wird geöffnet.

Wenn keine Protokolle angezeigt werden, passen Sie das Zeitauswahlfeld im Header an.

Weitere Informationen zur Anpassung eines Kibana-Dashboards finden Sie in [diesem Blogbeitrag](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/) oder in der Dokumentation zu [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

##  Kibana-Dashboard im Web-Browser aufrufen
{: #launch_Kibana_from_browser}

Die Abfrage, durch die die Daten gefiltert werden, die im Dashboard angezeigt werden, ruft Protokolleinträge für einen Bereich in der {{site.data.keyword.Bluemix}}-Organisation ab. Die Protokollinformationen, die im Kibana-Dashboard angezeigt werden, umfassen Einträge für alle Ressourcen, die innerhalb des Bereichs der {{site.data.keyword.Bluemix}}-Organisation bereitgestellt wurden, an der Sie angemeldet sind.

Führen Sie die folgenden Schritte aus, um ein Kibana-Dashboard über einen Browser zu öffnen:

1. Öffnen Sie [https://logmet.<span class="keyword" data-hd-keyref="DomainName">Domänenname</span>](https://logmet.{DomainName}), um sich bei der Kibana-Benutzerschnittstelle anzumelden.

2. Wählen Sie die Registerkarte **Kibana 3** aus, um mit Kibana 3 zu arbeiten. Wählen Sie die Registerkarte **Kibana 4** aus, um mit Kibana 4 zu arbeiten. Das Kibana-Standarddashboard wird geöffnet. 

Wenn keine Protokolle angezeigt werden, passen Sie das Zeitauswahlfeld im Header an.

Weitere Informationen zur Anpassung eines Kibana-Dashboards finden Sie in [diesem Blogbeitrag](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/) oder in der Dokumentation zu [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).



## Daten in einem Kibana-Dashboard filtern
{: #filter_data_kibana_dashboard}

In {{site.data.keyword.Bluemix}} können Sie Daten mithilfe des Kibana-Standarddashboards analysieren, das für jede Ressource bzw. jeden {{site.data.keyword.Bluemix}}-Bereich bereitgestellt wird. Diese Dashboards zeigen standardmäßig alle Daten an, die für die letzten 24 Stunden verfügbar sind. Sie können die durch ein Dashboard angezeigten Informationen jedoch eingrenzen. Sie können einem Standarddashboard Abfragen und Filter hinzufügen und es anschließend zur künftigen Wiederverwendung speichern.

In einem Dashboard können Sie mehrere Abfragen und Filter hinzufügen. Eine Abfrage definiert eine Teilmenge von Protokolleinträgen.  Ein Filter verfeinert die Datenauswahl durch Ein- oder Ausschluss von Informationen. 

In der folgenden Liste werden kurz einige Beispiele zur Filterung von Daten für Cloud Foundry-Apps dargestellt:
* Wenn Sie nach Informationen in Ihren Protokollen suchen, die Schlüsselbegriffe enthalten, können Sie Abfragen erstellen, um nach diesen Begriffen zu filtern. Sie können die Abfragen visuell im Kibana-Dashboard vergleichen. Weitere Informationen finden Sie unter [Protokolle für Cloud Foundry-Apps mit Abfragen in Kibana filtern](kibana3/logging_kibana_query.html#logging_kibana_query).

* Wenn Sie nach Informationen innerhalb eines bestimmten Zeitraums suchen, können Sie Daten nach einem Zeitbereich filtern. Weitere Informationen finden Sie unter [Protokolle für Cloud Foundry-Apps nach Zeit in Kibana filtern](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter).

* Wenn Sie nach Informationen für eine bestimmte Instanz-ID suchen, können Sie Daten nach Instanz-ID filtern. Weitere Informationen finden Sie unter [Protokolle für Cloud Foundry-Apps nach Instanz-ID in Kibana filtern](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id) und [Protokolle für Cloud Foundry-Apps nach bekannter Anwendungs-ID in Kibana filtern](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id).

* Wenn Sie nach Informationen für eine bestimmte Komponente suchen, können Sie Daten nach Komponente (Protokolltyp) filtern. Weitere Informationen finden Sie unter [Protokolle für Cloud Foundry-Apps nach Protokolltyp in Kibana filtern](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter).

* Wenn Sie nach Informationen, zum Beispiel nach Fehlernachrichten suchen, können Sie Daten nach Nachrichtentyp filtern. Weitere Informationen finden Sie unter [Protokolle für Cloud Foundry-Apps nach Nachrichtentyp in Kibana filtern](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter).

## Kibana-Dashboard anpassen
{: #customize_kibana_dashboard}

Es gibt verschiedene Typen von Dashboards, die Sie zum Visualisieren und Analysieren der Daten anpassen können, wie zum Beispiel die folgenden:
* Single-cf-app-Dashboard: Dies ist ein Dashboard, das Informationen zu einer einzelnen Cloud Foundry-Anwendung anzeigt.  
* Multi-cf-app-Dashboard: Dies ist ein Dashboard, das Informationen zu allen Cloud Foundry-Anwendungen anzeigt, die im selben {{site.data.keyword.Bluemix}}-Bereich bereitgestellt werden. 

Wenn Sie ein Dashboard anpassen, können Sie Abfragen und Filter konfigurieren, um eine Teilmenge der Protokolldaten zur Anzeige durch das Dashboard auszuwählen.

Sie können Anzeigen (Panels) zur Visualisierung der Daten konfigurieren. Kibana enthält verschiedene Anzeigen, wie zum Beispiel Anzeigen für Tabellen, Trends und Histogramme, die Sie zur Analyse der Informationen verwenden können. Sie können Anzeigen im Dashboard hinzufügen, entfernen und neu anordnen. Der Zweck jeder Anzeige variiert. Einige Anzeigen werden in Zeilen aufbereitet, in denen die Ergebnisse einer oder mehrerer Abfragen dargestellt werden. Andere Anzeigen enthalten Dokumente oder angepasste Informationen. Sie können zum Beispiel ein Balkendiagramm, ein Kreisdiagramm oder eine Tabelle zum Visualisieren und Analysieren der Daten konfigurieren.  


## Kibana-Dashboard speichern
{: #save_Kibana_dashboard}

Führen Sie die folgenden Schritte aus, um ein Kibana-Dashboard nach einer Anpassung zu speichern:

1. Klicken Sie in der Symbolleiste auf das Symbol **Speichern**.

2. Geben Sie einen Namen für das Dashboard ein.

    **Hinweis:** Wenn Sie versuchen, ein Dashboard unter einem Namen zu speichern, der Leerzeichen enthält, wird es nicht gespeichert.

3. Klicken Sie neben dem Namensfeld auf das Symbol **Speichern**.



## Protokolle über ein Kibana-Dashboard analysieren
{: #analyze_kibana_logs}

Nach der Anpassung eines Kibana-Dashboards können Sie die Daten in den Dashboardanzeigen visualisieren und analysieren. 

Für die Suche nach Informationen können Sie Abfragen fixieren (Pin) oder freigeben (Unpin). 

* Sie können eine Abfrage im Dashboard fixieren und die Suche wird automatisch aktiviert.
* Zum Entfernen des Inhalts aus dem Dashboard können Sie eine Abfrage inaktivieren.

Zum Filtern von Informationen können Sie Filter aktivieren oder inaktivieren. 

* Sie können das Kontrollkästchen unter **Toggle** ![Umschaltfeld zum Einschließen eines Filters](images/logging_toggle_include_filter.jpg) in einem Filter auswählen, um den Filter zu aktivieren.   
* Sie können das Kontrollkästchen unter **Toggle** ![Umschaltfeld zum Einschließen eines Filters](images/logging_toggle_exclude_filter.jpg) in einem Filter abwählen, um den Filter zu inaktivieren. 

Die Grafiken und Diagramme in Ihrem Dashboard zeigen die Daten an. Sie können die Grafiken und Diagramme in Ihrem Dashboard zum Überwachen der Daten verwenden. 

Bei einem Single-cf-app-Dashboard enthält das Dashboard zum Beispiel Informationen zu genau einer Cloud Foundry-Anwendung. Die Daten, die Sie visualisieren und analysieren können, sind auf diese App beschränkt. Sie können das Dashboard zum Analysieren aller Instanzen der App verwenden. Sie können Instanzen vergleichen. Sie können die Informationen nach Instanz-ID filtern. 

Sie können für jede Instanz-ID eine Abfrage definieren und im Dashboard fixieren. 

![Dashboard mit fixierten Abfragen](images/logging_kibana_dash_activate_query.jpg)

Anschließend können Sie einzelne Abfragen abhängig von den gewünschten Instanzinformationen, die im Dashboard angezeigt werden sollen, aktivieren oder inaktivieren. 

Die folgende Abbildung zeigt eine aktivierte Abfrage und eine inaktivierte Abfrage:

![Dashboard mit fixierten Abfragen](images/logging_kibana_dash_deactivate_query.jpg)

Wenn Sie zwei Instanzen in einem Histogramm vergleichen wollen, können Sie zwei Abfragen im selben Dashboard, eine für jede Instanz-ID, definieren. Sie können ihnen einen Aliasnamen und eine eindeutige Farbe zur einfachen Unterscheidung zuordnen. Kibana verarbeitet mehrere Abfragen mit Verknüpfung durch ein logisches OR. 

Die folgende Abbildung zeigt die Anzeige zum Konfigurieren eines Aliasnamens und einer Farbe für eine Abfrage, zum Fixieren ('Pin') der Abfrage an das Dashboard und zum Inaktivieren der Abfrage:

![Dashboardassistent zum Konfigurieren einer Abfrage](images/logging_kibana_query_def.jpg)



## Kibana-Protokollformat für Cloud Foundry-Anwendungen
{: #kibana_log_format_cf}

Sie können ein Kibana-Dashboard so konfigurieren, dass es die folgenden Felder für jeden Protokolleintrag anzeigt:

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>jjjj-MM-ttTHH:mm:ss:SS-0500</code></pre>
<p>Der Zeitpunkt des protokollierten Ereignisses. Die Zeitmarke ist bis auf die Millisekunde definiert.</p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>Die ID der {{site.data.keyword.Bluemix_notm}}-Ressource.</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>Die eindeutige ID für Ihr Protokolldokument.</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>Der Index für Ihren Protokolleintrag.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>Der Typ von Protokoll. Beispiel: <samp>syslog</samp>.</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>Der Name Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendung.</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>Die eindeutige ID Ihrer {{site.data.keyword.Bluemix_notm}}-Anwendung.</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>Der Name Ihrer Anwendung, die die Protokolldaten generiert hat.</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>Die Instanz-ID Ihrer Anwendungsinstanz, die die Protokolldaten generiert hat.</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>Die Priorität des protokollierten Ereignisses.</p>
</dd>

<dt><strong>message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Nachricht</var>&gt;</code></pre>
<p>Die Nachricht, die von der Komponente ausgegeben wird. Die Nachricht variiert abhängig vom Kontext.</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Der Datenstrom, in den die Protokollnachricht geschrieben wird. <samp class="ph codeph">OUT</samp> bezieht sich auf den Datenstrom <samp class="ph codeph">stdout</samp> und <samp class="ph codeph">ERR</samp> bezieht sich auf den Datenstrom <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>Die eindeutige ID Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation.</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>Der Name der {{site.data.keyword.Bluemix_notm}}-Organisation, in der das Staging für Ihre App erfolgt.</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Die Komponente, die Protokolle produziert. In der folgenden Liste werden die Protokolle aus jeder Komponente beschrieben:</p>

<dl>
<dt><strong>API</strong></dt>
<dd>Protokollierte Antworten auf API-Aufrufe, die eine Änderung an Ihrem App-Status anfordern.</dd>

<dt><strong>APP</strong></dt>
<dd>Protokollierte Antworten aus Ihrer App.</dd>

<dt><strong>CELL</strong></dt>
<dd>Protokollierte Antworten aus der Diego-Zelle, die den Zeitpunkt eines Starts, Stopps oder Absturzes einer App angeben.</dd>

<dt><strong>LGR</strong></dt>
<dd>Protokollierte Antworten aus Loggregator, die auf Probleme mit dem Protokollierungsprozess hinweisen.</dd>

<dt><strong>RTR</strong></dt>
<dd>Protokollierte Antworten aus dem Router, wenn er HTTP-Anforderungen an Ihre App leitet.</dd>

<dt><strong>SSH</strong></dt>
<dd>Protokollierte Antworten aus der Diego-Zelle, wenn ein Benutzer auf einen App-Container mit dem Befehl **cf ssh** zugreift.</dd>

<dt><strong>STG</strong></dt>
<dd>Protokollierte Antworten aus der Diego-Zelle oder dem Droplet Execution Agent (DEA), wenn ein Staging oder erneutes Staging für Ihre App erfolgt.</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>Der Name des {{site.data.keyword.Bluemix_notm}}-Bereichs, in das Staging für Ihre App erfolgt.</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>Der Zeitpunkt des protokollierten Ereignisses. Die Zeitmarke ist bis auf die Millisekunde definiert.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>Der Typ von Protokoll. Beispiel: <samp>syslog</samp>.</p>
</dd>
</dl>




