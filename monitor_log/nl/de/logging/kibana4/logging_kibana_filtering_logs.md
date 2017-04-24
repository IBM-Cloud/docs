---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokolle in Kibana filtern
{:#kibana_filtering_logs}

Auf der Seite 'Discover' können Sie Suchabfragen erstellen und Filter anwenden, um die Informationen zu beschränken, die zur Analyse angezeigt werden.
{:shortdesc}

* Sie können eine oder mehrere Suchabfragen über die Suchleiste der Seite 'Discover' definieren. Eine Suchabfrage definiert eine Teilmenge von Protokolleinträgen. Zum Definieren einer Suchabfrage verwenden Sie die Abfragesprache Lucene.  

* Sie können Filter über die Feldliste (*Fields*) oder über die Tabelleneinträge hinzufügen. Ein Filter verfeinert die Datenauswahl durch Ein- oder Ausschluss von Informationen. Sie können einen Filter aktivieren oder inaktivieren, die Filteraktion umkehren, den Filter ein- oder ausschalten oder den Filter ganz entfernen.  

Wenn Sie eine neue Suche definiert haben, speichern Sie sie, sodass Sie sie für zukünftige Analysen auf der Seite 'Discover' oder zum Erstellen von Visualisierungen wiederverwenden können, die Sie in angepassten Dashboards nutzen können. Weitere Informationen finden Sie unter [Suche speichern](logging_kibana_filtering_logs.html#k4_save_search).

Wenn Sie eine neue Suche ausführen, werden das Histogramm, die Tabelle und die Feldliste automatisch aktualisiert, um die Suchergebnisse anzuzeigen. Informationen dazu, wie Sie ermitteln, welche Daten angezeigt werden, finden Sie unter [Auf der Seite 'Discover' angezeigte Daten ermitteln](k4_identify_data.html#k4_identify_data).

In der folgenden Liste werden Szenarios für die Möglichkeiten zum Filtern von Daten in den Protokollen zusammengefasst: 

* Sie können angepasste Suchen zum Filtern Ihrer Protokolle erstellen. Weitere Informationen finden Sie unter [Protokolle durch Definieren angepasster Abfragen filtern](k4_filter_queries.html#k4_filter_queries). 

* Sie können Ihre Protokolle nach Einträgen durchsuchen, die einen bestimmten Text im Wert eines Felds enthalten. Weitere Informationen finden Sie unter [Protokolle nach bestimmtem Text in einem Feldwert filtern](k4_filter_logs_spec_text.html#k4_filter_logs_spec_text).
 
* Sie können Ihr Protokoll nach einem bestimmten Feldwert durchsuchen oder Einträge aus dem Protokoll mit einem bestimmten Feldwert ausschließen. Weitere Informationen finden Sie unter [Protokolle nach einem bestimmten Feldwert filtern](k4_filter_logs_spec_field.html#k4_filter_logs_spec_field).

    * Sie können Ihre Protokolle nach Protokolltyp filtern. Weitere Informationen finden Sie unter [Protokolle nach Protokolltyp filtern](k4_filter_logs_by_log_type.html#k4_filter_logs_by_log_type). 
    * Sie können Ihre CF-App-Protokolle nach Quelle filtern. Weitere Informationen finden Sie unter [CF-App-Protokolle nach Quelle filtern](k4_filter_logs_by_source.html#k4_filter_logs_by_source). 
    * Sie können Ihre Protokolle nach Instanz-ID filtern. Weitere Informationen finden Sie unter [Protokolle nach Instanz-ID filtern](k4_filter_logs_by_instance_id.html#k4_filter_logs_by_instance_id).    
    * Sie können Ihre Protokolle nach Nachrichtentyp filtern. Weitere Informationen finden Sie unter [CF-App-Protokolle nach Nachrichtentyp filtern](k4_filter_cf_logs_by_msg_type.html#k4_filter_cf_logs_by_msg_type).   
 
* Sie können Ihre Protokolle filtern, um Einträge innerhalb eines Zeitraums anzuzeigen. Weitere Informationen finden Sie unter [Zeitfilter festlegen](logging_kibana_set_time_filter.html#set_time_filter).
     

## Neue Suche starten
{: #k4_new_search}

Zum Starten einer neuen Suche klicken Sie auf die Schaltfläche **New Search** ![Neue Suche](images/k4_new_search_icon.jpg "New search") in der Symbolleiste der Seite 'Discover'. 

## Suche speichern 
{: #k4_save_search}

Wenn Sie eine Suche speichern, werden die Zeichenfolge der Suchabfrage und das zurzeit ausgewählte Indexmuster gespeichert. 

Führen Sie die folgenden Schritte aus, um die aktuelle Suche auf der Seite 'Discover' zu speichern: 

1. Klicken Sie in der Symbolleiste der Seite 'Discover' auf die Schaltfläche **Save Search** ![Suche speichern](images/k4_save_search_icon.jpg "Suche speichern"). 

2. Geben Sie einen Namen für die Suche ein. 

3. Klicken Sie auf 'Save' (Speichern).  

## Suche löschen
{: #k4_delete_search}

Führen Sie die folgenden Schritte auf der Seite 'Settings' aus, um eine Suche zu löschen: 

1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus. 

2. Wählen Sie auf der Registerkarte **Searches** die Suche aus, die Sie löschen wollen. 

3. Klicken Sie auf **Delete** (Löschen). 


## Suche exportieren
{: #k4_export_search}

Führen Sie die folgenden Schritte auf der Seite 'Settings' aus, um eine Suche zu exportieren: 

1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus. 

2. Wählen Sie auf der Registerkarte **Searches** die Suche aus, die Sie exportieren wollen. 

3. Klicken Sie auf **Export**. 

4. Speichern Sie Datei. 

## Suche importieren
{: #k4_import_search}

Führen Sie die folgenden Schritte auf der Seite 'Settings' aus, um eine Suche zu importieren: 

1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus. 

2. Wählen Sie auf der Registerkarte **Searches** die Option **Import** aus. 

3. Wählen Sie eine Datei aus und klicken Sie auf **Open**. 

Die Suche wird der Liste der Suchen hinzugefügt. 


## Suche erneut laden
{: #k4_reload_search}

Führen Sie die folgenden Schritte aus, um eine gespeicherte Suche zu laden: 

1. Klicken Sie in der Symbolleiste der Seite 'Discover' auf die Schaltfläche **Load Search** ![Suche laden](images/k4_load_icon.jpg "Suche laden"). 

2. Wählen Sie die Suche aus, die Sie laden wollen.  


## Inhalt einer Suche aktualisieren
{: #k4_refresh_search}

Zum manuellen Aktualisieren des Inhalts einer Suche können Sie auf das Lupensymbol klicken, das in der Suchleiste verfügbar ist.  

Sie können ein Aktualisierungsintervall konfigurieren, wenn die Daten, die auf der Seite 'Discover' angezeigt werden, automatisch aktualisiert werden sollen. Der aktuelle Wert des Aktualisierungsintervalls wird in der Menüleiste der Seite 'Discover' angezeigt. Standardmäßig ist die automatische Aktualisierung (Auto-refresh) inaktiviert (**OFF**). 

Führen Sie die folgenden Schritte aus, um ein Aktualisierungsintervall festzulegen: 

1. Klicken Sie auf der Seite 'Discover' auf den Zeitfilter (**Time Filter**), der in der Menüleiste verfügbar ist. 

2. Klicken Sie auf **Auto Refresh** ![Automatische Aktualisierung](images/k4_auto_refresh_icon.jpg "Automatische Aktualisierung"). 

3. Wählen Sie ein Aktualisierungsintervall in der Liste aus.  

    ![Optionen für Aktualisierungsintervall](images/k4_change_autorefresh.jpg "Optionen für Aktualisierungsintervall")


**Hinweis:** Wenn ein automatisches Aktualisierungsintervall aktiviert ist, können Sie dieses anhalten, indem Sie auf die Pauseschaltfläche ![Pause](images/k4_auto_refresh_pause_icon.jpg "Pause") klicken. 




