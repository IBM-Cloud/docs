---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# CF-App-Protokolle nach Quelle filtern
{:#k4_filter_logs_by_source}

Sie können Cloud Foundry-Anwendungsprotokolle über das Kibana-Dashboard nach Quellentyp anzeigen und filtern.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um nach Einträgen zu suchen, die eine bestimmte Protokollquelle enthalten:

1. Schauen Sie sich die Kibana-Seite 'Discover' an, um festzustellen, welche Untergruppe Ihrer Daten dort angezeigt wird. Weitere Informationen finden Sie unter [Auf der Kibana-Seite 'Discover' angezeigte Daten ermitteln](logging_kibana_analize_logs_interactively.html#k4_identify_data). 

2. Wählen Sie in der Feldliste *Fields* das Feld **source_id** aus. 

    ![Filterliste mit dem Feld 'source_id'](images/k4_filter_sourceid_F1.jpg "Filterliste mit dem Feld 'source_id'")     

3. Zum Hinzufügen eines Filters, der nach Einträgen mit einem bestimmten Wert für 'source_id' sucht, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Inklusivmodus](images/k4_include_field_icon.jpg "Schaltfläche mit Lupensymbol im Inklusivmodus") für diesen Wert aus. 

    Eine Liste von Protokollquellen, die für CF-Apps verfügbar sind, finden Sie unter [Protokollquellen für CF-Apps](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources). 

    Beispiel: Zum Hinzufügen eines Filters, der Protokolleinträge zu Start-, Stopp- oder Ausfallereignissen einer CF-Anwendung einschließt, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Inklusivmodus](images/k4_include_field_icon.jpg "Schaltfläche mit Lupensymbol im Inklusivmodus") aus, die für den Wert *CELL* im Abschnitt der Feldliste *Fields* verfügbar ist. Die folgende Abbildung zeigt den aktivierten Filter für den Wert *CELL* im Feld 'source_id '. 
    
    ![Filter, der den Feldwert einschließt](images/k4_filter_sourceid_F2.jpg "Filter, der den Feldwert einschließt")

    Zum Hinzufügen eines Filters, der nach Einträgen sucht, die einen bestimmten Wert für 'source_id' nicht enthalten, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Exklusivmodus](images/k4_exclude_field_icon.jpg "Schaltfläche mit Lupensymbol im Exklusivmodus") für den Wert aus. 
    
    Beispiel: Zum Hinzufügen eines Filters, der Protokolleinträge zu Start-, Stopp- oder Ausfallereignissen einer CF-Anwendung ausschließt, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Exklusivmodus](images/k4_exclude_field_icon.jpg "Schaltfläche mit Lupensymbol im Exklusivmodus") aus, die für den Wert *CELL* im Abschnitt der Feldliste *Fields* verfügbar ist. Die folgende Abbildung zeigt den Filter, der mit dem Wert *CELL* für 'source_id' ausschließt. 

    ![Filter, der den Feldwert ausschließt](images/k4_filter_sourceid_F3.jpg "Filter, der den Feldwert ausschließt")




