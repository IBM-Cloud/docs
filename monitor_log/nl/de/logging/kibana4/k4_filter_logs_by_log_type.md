---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokolle nach Protokolltyp filtern
{:#k4_filter_logs_by_log_type}

Sie können {{site.data.keyword.Bluemix}}-Protokolle nach Protokolltyp anzeigen und filtern.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um nach Einträgen zu suchen, die einen bestimmten Protokolltyp enthalten: 

1. Schauen Sie sich die Kibana-Seite 'Discover' an, um festzustellen, welche Untergruppe Ihrer Daten dort angezeigt wird. Weitere Informationen finden Sie unter [Auf der Kibana-Seite 'Discover' angezeigte Daten ermitteln](logging_kibana_analize_logs_interactively.html#k4_identify_data). 

2. Wählen Sie in der Feldliste *Fields* das Feld **type** aus. 

    In der folgenden Abbildung ist zum Beispiel nur ein Protokolltyp verfügbar: *syslog*. 
    
    ![Filterliste, die das Feld für Protokolltyp zeigt](images/k4_filter_log_type_F1.jpg "Filterliste, die das Feld für Protokolltyp zeigt")
   
3. Zum Hinzufügen eines Filters, der nach einem bestimmten Protokolltyp sucht, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Inklusivmodus](images/k4_include_field_icon.jpg "Schaltfläche mit Lupensymbol im Inklusivmodus") für den Typ von Protokoll aus, den Sie analysieren wollen. 

    Beispiel: Zum Hinzufügen eines Filters, der Protokolleinträge für *syslog* einschließt, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Inklusivmodus](images/k4_include_field_icon.jpg "Schaltfläche mit Lupensymbol im Inklusivmodus") aus, die für den Wert *syslog* im Abschnitt der Feldliste *Fields* verfügbar ist. Die folgende Abbildung zeigt den Filter, der Einträge für den Protokolltyp *syslog* einschließt. 

    ![Filter, der Einträge für den Protokolltyp 'syslog' einschließt](images/k4_filter_log_type_F2.jpg "Filter, der Einträge für den Protokolltyp 'syslog' einschließt")

    Zum Hinzufügen eines Filters, der nach Einträgen sucht, die einen bestimmten Protokolltyp nicht enthalten, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Exklusivmodus](images/k4_exclude_field_icon.jpg "Schaltfläche mit Lupensymbol im Exklusivmodus") für den Wert aus. 

     Beispiel: Zum Hinzufügen eines Filters, der Protokolleinträge für *syslog* ausschließt, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Exklusivmodus](images/k4_exclude_field_icon.jpg "Schaltfläche mit Lupensymbol im Exklusivmodus") aus, die für den Wert *syslog* im Abschnitt der Feldliste *Fields* verfügbar ist. Die folgende Abbildung zeigt den Filter, der Einträge für den Protokolltyp *syslog* ausschließt. 
     
     ![Filter, der Einträge für den Protokolltyp 'syslog' ausschließt](images/k4_filter_log_type_F3.jpg "Filter, der Einträge für den Protokolltyp 'syslog' ausschließt")



