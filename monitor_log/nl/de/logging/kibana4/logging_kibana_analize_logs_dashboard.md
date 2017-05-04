---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokolle in Kibana über ein Dashboard analysieren
{:#kibana_analize_logs_dashboard}

Auf der Seite *Dashboard* in Kibana können Sie Sammlungen von Visualisierungen anzeigen, die in Dashboards gruppiert sind. Verwenden Sie die Dashboards, um Ihre Protokolldaten zu analysieren und Ergebnisse zu vergleichen.
{:shortdesc}

In {{site.data.keyword.Bluemix}} gibt es verschiedene Typen von Dashboards, die Sie definieren und anpassen können, um Daten zu visualisieren und zu analysieren. In der folgenden Tabelle werden zum Beispiel einige der gängigen Dashboardtypen aufgeführt: 

| Typ von Dashboard | Beschreibung |
|-------------------|-------------|
| Single-cf-app-Dashboard | Dies ist ein Dashboard, das Informationen für eine einzelne Cloud Foundry-Anwendung anzeigt. |
| Single Container-Dashboard  | Dies ist ein Dashboard, das Informationen für einen einzelnen Container anzeigt.  |
| Container Group-Dashboard  | Dies ist ein Dashboard, das Informationen für eine bestimmte Containergruppe anzeigt.  |
| Multi-cf-app-Dashboard | Dies ist ein Dashboard, das Informationen für alle Cloud Foundry-Anwendungen anzeigt, die im selben {{site.data.keyword.Bluemix_notm}}-Bereich bereitgestellt werden.  | 
| Multi-Container-Dashboard | Dies ist ein Dashboard, das Informationen für alle Container anzeigt, die im selben {{site.data.keyword.Bluemix_notm}}-Bereich bereitgestellt werden.  |
| Space-Dashboard | Dies ist ein Dashboard, das Protokolldaten anzeigt, die in einem {{site.data.keyword.Bluemix_notm}}-Bereich verfügbar sind.  | 

Zur Visualisierung der Daten in einem Dashboard konfigurieren Sie Anzeigen (Panels). Kibana enthält verschiedene Visualisierungen, wie zum Beispiel Tabellen, Trends und Histogramme, die Sie zur Analyse der Informationen verwenden können. Eine Visualisierung wird einem Dashboard als Anzeige hinzugefügt. Sie können Anzeigen im Dashboard hinzufügen, entfernen und neu anordnen. Der Zweck jeder Anzeige variiert. Einige Anzeigen werden in Zeilen aufbereitet, in denen die Ergebnisse einer oder mehrerer Abfragen dargestellt werden. Andere Anzeigen enthalten Dokumente oder angepasste Informationen. Jede Anzeige basiert auf einer Suche. Die Suche definiert die Untergruppe von Daten, die in der Anzeige dargestellt werden. Sie können zum Beispiel ein Balkendiagramm, ein Kreisdiagramm oder eine Tabelle zum Visualisieren und Analysieren der Daten konfigurieren.  

In der folgenden Tabelle sind verschiedene Tasks aufgeführt, die Sie auf der Seite 'Dashboard' ausführen können: 

| Task | Weitere Informationen |
|------|------------------|
| [Neues Dashboard erstellen](logging_kibana_analize_logs_dashboard.html#K4_dashboard_new) | Sie können mehrere Dashboards erstellen. Jedes Dashboard kann so gestaltet werden, dass es andere Suchen und Visualisierungen sowie eine andere Untergruppe von Protokolldaten umfasst.  |
| [Dashboard speichern](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save) | Sie können ein Dashboard zur späteren Wiederverwendung speichern. |
| [Dashboard laden](logging_kibana_analize_logs_dashboard.html#k4_dashboard_reload) | Sie können ein Dashboard hochladen, um die entsprechenden Daten zu aktualisieren, zu ändern oder zu analysieren. |
| [Dashboard löschen](logging_kibana_analize_logs_dashboard.html#k4_dashboard_delete) | Sie können Dashboard löschen, die nicht benötigt werden. |
| [Dashboard exportieren](logging_kibana_analize_logs_dashboard.html#k4_dashboard_export) | Sie können ein Dashboard als JSON-Datei exportieren. |
| [Dashboard importieren](logging_kibana_analize_logs_dashboard.html#k4_dashboard_import) | Sie können ein Dashboard als JSON-Datei importieren. |
| [Dashboard gemeinsam nutzen](logging_kibana_analize_logs_dashboard.html#k4_dashboard_share) | Sie können ein Dashboard in Ihrem HTML-Quelltext oder über das Kibana-Dashboard zur gemeinsamen Nutzung verfügbar machen. |
| [Visualisierung hinzufügen](logging_kibana_analize_logs_dashboard.html#k4_dashboard_add_visualization) | Sie können einem Dashboard eine vorhandene Visualisierung oder Suche hinzufügen.|

Weitere Informationen zu Kibana finden Sie in der Veröffentlichung [Kibana User Guide ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.



## Neues Kibana-Dashboard erstellen
{: #K4_dashboard_new}

Führen Sie die folgenden Schritte aus, um ein neues Dashboard zu erstellen: 

1. Klicken Sie in der Symbolleiste der Seite 'Dashboard' auf die Schaltfläche **New dashboard** ![Neues Dashboard](images/k4_dash_new_icon.jpg "Neues Dashboard").

2. Fügen Sie eine oder mehrere Suchen und Visualisierungen hinzu. Weitere Informationen finden Sie unter [Neue Suche oder Visualisierung hinzufügen](logging_kibana_analize_logs_dashboard.html#K4_dashboard_add_visualization). 

    Wenn Sie eine Suche oder eine Visualisierung hinzufügen, wird im Dashboard eine Anzeige hinzugefügt. 

3. Ziehen Sie eine Anzeige und übergeben Sie sie an der Position im Dashboard, an der Sie sie positionieren wollen. 
 
4. Speichern Sie das Dashboard zur künftigen Wiederverwendung. Weitere Informationen finden Sie unter [Kibana-Dashboard speichern](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save).


## Neue Suche oder Visualisierung hinzufügen
{: #k4_dashboard_add_visualization}

Führen Sie die folgenden Schritte aus, um eine vorhandene Visualisierung oder Suche hinzuzufügen: 

1. Klicken Sie in der Symbolleiste der Seite 'Dashboard' auf die Schaltfläche **Add visualization** ![Visualisierung hinzufügen](images/k4_dash_add_visualization_icon.jpg "Visualisierung hinzufügen"). 

    **Hinweis:** Sie können Visualisierungen und Suchen hinzufügen.  

2. Wählen Sie zum Hinzufügen einer Visualisierung die Registerkarte **Visualizations** oder zum Hinzufügen einer Suche die Registerkarte **Searches** aus. 

3. Klicken Sie auf die Suche bzw. die Visualisierung, die Sie hinzufügen wollen. 

    Eine Anzeige für diese Suche oder Visualisierung wird im Dashboard hinzugefügt. 



## Kibana-Dashboard speichern
{: #k4_dashboard_save}

Führen Sie die folgenden Schritte aus, um ein Kibana-Dashboard nach einer Anpassung zu speichern:

1. Klicken Sie in der Symbolleiste auf die Schaltfläche **Save** ![Dashboard speichern](images/k4_dash_save_icon.jpg "Dashboard speichern"). 

2. Geben Sie einen Namen für das Dashboard ein.

    **Hinweis:** Wenn Sie versuchen, ein Dashboard unter einem Namen zu speichern, der Leerzeichen enthält, wird es nicht gespeichert.

3. Klicken Sie neben dem Namensfeld auf das Symbol **Save** (Speichern). 


## Kibana-Dashboard löschen
{: #k4_dashboard_delete}

Führen Sie die folgenden Schritte auf der Seite 'Settings' aus, um eine Visualisierung zu löschen: 

1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus. 

2. Wählen Sie auf der Registerkarte **Visualizations** die Visualisierungen aus, die Sie löschen wollen. 

3. Klicken Sie auf **Delete** (Löschen). 


## Kibana-Dashboard laden
{: #k4_dashboard_reload}

Führen Sie die folgenden Schritte aus, um ein gespeichertes Dashboard zu laden: 

1. Klicken Sie in der Symbolleiste der Seite 'Dashboard' auf die Schaltfläche **Load Saved Dashboard** ![Gespeichertes Dashboard laden](images/k4_dash_load_icon.jpg "Gespeichertes Dashboard laden"). 

2. Wählen Sie das Dashboard, das Sie laden wollen.  


## Kibana-Dashboard exportieren
{: #k4_dashboard_export}

Führen Sie die folgenden Schritte auf der Seite 'Settings' aus, um ein Dashboard als JSON-Datei zu exportieren: 

1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus. 

2. Wählen Sie auf der Registerkarte **Dashboard** das Dashboard aus, das Sie exportieren wollen. 

3. Klicken Sie auf **Export**. 

4. Speichern Sie Datei. 


## Kibana-Dashboard importieren
{: #k4_dashboard_import}

Führen Sie die folgenden Schritte auf der Seite 'Settings' aus, um ein Dashboard als JSON-Datei zu importieren: 

1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus. 

2. Wählen Sie auf der Registerkarte **Dashboard** die Option **Import** aus. 

3. Wählen Sie eine Datei aus und klicken Sie auf **Open**. 

Das Dashboard wird der Liste der Dashboards hinzugefügt. 


## Kibana-Dashboard gemeinsam nutzen
{: #k4_dashboard_share}

Führen Sie die folgenden Schritte aus, um ein Dashboard zur gemeinsamen Nutzung verfügbar zu machen: 

1. Klicken Sie in der Symbolleiste der Seite 'Dashboard' auf die Schaltfläche **Share dashboard** ![Dashboard gemeinsam nutzen](images/k4_dash_share_icon.jpg "Dashboard gemeinsam nutzen"). 

2. Wählen Sie eine der folgenden Aktionen aus: 

    * **Embed this dashboard:** Wählen Sie diese Option aus, um das Dashboard in Ihrem HTML-Quelltext zur gemeinsamen Nutzung verfügbar zu machen.  
    
        Klicken Sie auf die Kopierschaltfläche ![In Zwischenablage kopieren](images/k4_copy_to_clipboard.jpg "In Zwischenablage kopieren"), um den HTML-Code zu kopieren, mit dem Sie das Dashboard in Ihren HTML-Quelltext einbetten können. 
        
        **Hinweis:** Zum Anzeigen des Dashboards müssen Benutzer Zugriff auf Kibana haben. 
	
    * **Share a link:**: Wählen Sie diese Option aus, um das Dashboard in Kibana mit anderen Benutzern gemeinsam zu nutzen. 



