---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Dashboards und Berichte anzeigen
{: #DRA_toolchain_reports}

{{site.data.keyword.DRA_short}} stellt Ihnen eine Menge an umsetzbaren Informationen zu Ihren Projekten bereit.
{:shortdesc}

## {{site.data.keyword.DRA_short}}-Dashboards    
{: #DI_toolchain_dashboards}

{{site.data.keyword.DRA_short}} stellt Dashboards bereit, in denen Informationen zur Leistung in Ihrer gesamten Bluemix-Organisation angezeigt werden. Um diese Informationen sehen zu können, müssen Sie nach dem Öffnen von {{site.data.keyword.DRA_short}} auf die Option zur Buildüberprüfung oder zur Bereitstellungsüberprüfung klicken.

Die Dashboards werden automatisch mit den aktuellen Informationen aus den {{site.data.keyword.DRA_short}}-Testjobs der Pipelines gefüllt. Für weitere Informationen hierzu müssen Sie auf die Elemente in den Dashboards klicken.

### Key Performance Indicators in Builds    
{: #DI_key_performance_indicators}

Auf der Seite für die Buildüberprüfung sind drei Diagramme mit Informationen zum Zustand des ausgewählten Entwicklungszweigs enthalten:

<table>
<thead>
<tr>
<th>Diagramm</th>
<th>Beschreibung</th>
</tr>
</thead>

<tbody>
<tr>
<td>Aktuelle Builds</td>
<td>Die Anzahl der aktuellen abgeschlossenen Builds im Vergleich zur Gesamtzahl der aktuellen Builds.</td>
</tr>
<tr>
<td>Tests</td>
<td>Die Anzahl der bestandenen Tests im Vergleich zur Gesamtzahl der Tests.</td>
</tr>
<tr>
<td>Codeabdeckung</td>
<td>Der prozentuale Anteil Ihrer Codeanweisungen und -funktionen, die von Ihren Tests aufgerufen werden.</td>
</tr>
</tbody></table>

## Entscheidungsberichte anzeigen    
{: #DI_decision_reports}

Nach der Pipeline-Ausführung beginnt {{site.data.keyword.DRA_short}} für die Erstellung einer Baseline mit der Erfassung und Analyse der Testergebnisse aus der Pipeline. Es werden Daten aus allen nachfolgenden Ausführungen erfasst und mit den vorherigen Ergebnissen verglichen. In Entscheidungsgates werden diese Daten verwendet, um zu bestimmen, wann eine Bereitstellung gestoppt werden soll. 

Führen Sie die folgenden Schritte aus, um den Entscheidungsbericht für ein Gate aus der Pipeline anzuzeigen:

   1. Klicken Sie bei der Stufe mit dem zu überprüfenden Gate auf die Option zum Anzeigen von Protokollen und Verlauf.

   2. Klicken Sie im Jobfenster der Stufe auf den Namen des Gates.

   3. Suchen Sie in der Protokollansicht nach der Nachricht 'Check {{site.data.keyword.DRA_short}} report here' und klicken Sie auf den angegebenen Link, um den Bericht zu öffnen.
