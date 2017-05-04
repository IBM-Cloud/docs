---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokolle nach Instanz-ID filtern
{:#k4_filter_logs_by_instance_id}

Sie können {{site.data.keyword.Bluemix}}-Protokolle nach Instanz-ID anzeigen und filtern.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um Ihre Protokolle nach Instanz-ID im Kibana-Dashboard anzuzeigen und zu filtern: 

1. Schauen Sie sich die Kibana-Seite 'Discover' an, um festzustellen, welche Untergruppe Ihrer Daten dort angezeigt wird. Weitere Informationen finden Sie unter [Auf der Kibana-Seite 'Discover' angezeigte Daten ermitteln](logging_kibana_analize_logs_interactively.html#k4_identify_data). 

2. Wählen Sie in der Feldliste *Fields* eines der folgenden Felder aus, um nach einer bestimmten Instanz-ID zu suchen: 

    * **instance_ID**: In diesem Feld werden die verschiedenen Instanz-IDs aufgelistet, die in dem Protokoll für eine Cloud Foundry-Anwendung verfügbar sind.  
    * **instance**: In diesem Feld werden die verschiedenen GUIDs aller Instanzen für eine Containergruppe aufgelistet.  

    Die folgende Abbildung zeigt zum Beispiel verschiedene Werte von Instanzen für eine CF-App: 
    
    ![Filterliste mit dem Feld 'instance_id'](images/k4_filter_instanceid_f1.jpg "Filterliste mit dem Feld 'instance_id'")
   
3. Zum Hinzufügen eines Filters, der nach einem bestimmten Protokolltyp sucht, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Inklusivmodus](images/k4_include_field_icon.jpg "Schaltfläche mit Lupensymbol im Inklusivmodus") für den Typ von Protokoll aus, den Sie analysieren wollen. 

   Beispiel: Zum Hinzufügen eines Filters, der Einträge für die CF-App-Instanz *2* einschließt, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Inklusivmodus](images/k4_include_field_icon.jpg "Schaltfläche mit Lupensymbol im Inklusivmodus") aus, die für den Wert *2* im Feldlistenabschnitt verfügbar ist. Die folgende Abbildung zeigt den Filter, der Einträge für die Instanz *2* einschließt. 
    
    ![Filter, der Einträge 'instance_id' für die Instanz 2 einschließt](images/k4_filter_instanceid_f2.jpg "Filter, der Einträge 'instance_id' für die Instanz 2 einschließt")

    Zum Hinzufügen eines Filters, der nach Einträgen sucht, die eine bestimmte Instanz-ID nicht enthalten, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Exklusivmodus](images/k4_exclude_field_icon.jpg "Schaltfläche mit Lupensymbol im Exklusivmodus") für den Wert aus. 

     Beispiel: Zum Hinzufügen eines Filters, der Einträge für die CF-App-Instanz *2* ausschließt, wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Exklusivmodus](images/k4_exclude_field_icon.jpg "Schaltfläche mit Lupensymbol im Exklusivmodus") aus, die für den Wert *2* im Feldlistenabschnitt verfügbar ist. Die folgende Abbildung zeigt den Filter, der Einträge für die Instanz *2* ausschließt. 
     
      ![Filter, der Einträge 'instance_id' für die Instanz 2 ausschließt](images/k4_filter_instanceid_f3.jpg "Filter, der Einträge 'instance_id' für die Instanz 2 ausschließt")

