---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Protokolle für Cloud Foundry-Apps nach Instanz-ID in Kibana filtern
{: #logging_kibana_instance_id}

Sie können {{site.data.keyword.Bluemix_notm}}-Instanzprotokolle nach Instanz-ID (instance_id) Ihrer App im Kibana-Dashboard anzeigen und filtern. Sie können über die Registerkarte **Protokolle** für Ihre Cloud Foundry-App auf das Kibana-Dashboard zugreifen. 
{:shortdesc}

Führen Sie die folgenden Tasks aus, um Ihre Cloud Foundry-App-Protokolle nach Instanz-ID im Kibana-Dashboard anzuzeigen und zu filtern:

1. Greifen Sie auf die Registerkarte **Protokolle** Ihrer Cloud Foundry-App zu. 

    1. Klicken Sie auf den App-Namen im {{site.data.keyword.Bluemix_notm}}-Dashboard **Apps**.
    2. Klicken Sie auf die Registerkarte **Protokolle**. 
    
    Die Protokolle für Ihre App werden angezeigt.

2. Greifen Sie auf das Kibana-Dashboard für Ihre App zu. Klicken Sie auf **Erweiterte Ansicht** ![Link für erweiterte Ansicht](images/logging_advanced_view.jpg "Link für Erweiterte Ansicht"). Das Kibana-Dashboard wird angezeigt.

3. Klicken Sie auf dem Kibana-Dashboard auf das Symbol **Zu gespeichertem Standard** ![Symbol 'Zu gespeichertem Standard'](images/logging_default_dash.jpg "Symbol 'Zu gespeichertem Standard'"), um alle Protokolle für einen Bereich anzuzeigen. Klicken Sie im Fenster **ALL EVENTS** auf das Rechtspfeilsymbol, um alle Felder anzuzeigen. 

    ![Fenster 'All Events' mit dem Rechtspfeilsymbol](images/logging_all_events_no_fields.jpg "Fenster 'All Events' mit dem Rechtspfeilsymbol")

4. Wählen Sie im Teilfenster **Fields** die Optionen **application_id** und **instance_id** aus, um die Felder 'application_id' und 'instance_id' im Fenster **ALL EVENTS** anzuzeigen.

    ![Fenster 'All Events' mit den ausgewählten Feldern 'application_id' und 'instance_id'](images/logging_all_events_app_instance_select.jpg "Fenster 'All Events' mit den ausgewählten Feldern 'application_id' und 'instance_id'")

5. Klicken Sie im Fenster **ALL EVENTS** auf eine Protokollereigniszeile, um die Details für dieses Ereignis anzuzeigen. Wählen Sie ein Ereignis aus, das den Wert für 'instance_id' anzeigt, nach dem Sie filtern wollen.

    ![Fenster 'All Events' mit Details für ein ausgewähltes Protokollereignis](images/logging_selected_log_event.jpg "Fenster 'All Events' mit Details für ein ausgewähltes Protokollereignis")

6. Fügen Sie einen Filter hinzu, um Informationen zu einer App-ID ein- oder auszuschließen. 

    * Zum Hinzufügen eines Filters, der Informationen zu einer bestimmten Anwendungs-ID einschließt, klicken Sie auf das **Lupensymbol** ![Lupensymbol](images/logging_magnifying_glass.jpg) in der Zeile 'application_id' der Tabelle. 
    
           ![Filterbedingung für das Feld 'application_id'](images/logging_application_id_filter.jpg "Filterbedingung für das Feld 'application_id'")
    
    * Zum Hinzufügen eines Filters, der Informationen zu einer bestimmten Anwendungs-ID ausschließt, klicken Sie auf das **Ausschlusssymbol** ![Ausschlusssymbol](images/logging_exclusion_icon.png) in der Zeile 'application_id' der Tabelle. 
    
           ![Filterbedingung für den Ausschluss einer Anwendungs-ID](images/logging_application_id_exclude_filter.jpg "Filterbedingung für den Ausschluss einer Anwendungs-ID")
    
    Im Kibana-Dashboard wird eine neue Filterbedingung hinzugefügt.
 

7. Fügen Sie einen Filter hinzu, um Informationen zu einer App-Instanz-ID ein- oder auszuschließen. 

    * Zum Hinzufügen eines Filters, der Informationen zu einer bestimmten Instanz-ID einschließt, klicken Sie auf das **Lupensymbol** ![Lupensymbol](images/logging_magnifying_glass.jpg "Lupensymbol") in der Zeile 'instance_id' der Tabelle.  

    ![Filterbedingung für das Feld 'instance_id'](images/logging_instance_id_filter.jpg "Filterbedingung für das Feld 'instance_id'")

     * Zum Hinzufügen eines Filters, der Informationen zu einer bestimmten Instanz-ID ausschließt, klicken Sie auf das **Ausschlusssymbol** ![Ausschlusssymbol](images/logging_exclusion_icon.png "Ausschlusssymbol") in der Zeile 'instance_id' der Tabelle.  
    
           ![Filterbedingung für den Ausschluss einer Instanz-ID](images/logging_application_instance_id_exclude_filter.jpg "Filterbedingung für den Ausschluss einer Instanz-ID")
    
    Im Kibana-Dashboard wird eine neue Filterbedingung hinzugefügt.

9. Speichern Sie das Dashboard. Wenn Sie die Erstellung Ihres Filters abgeschlossen haben, klicken Sie auf das Symbol **Speichern** ![Symbol für Speichern](images/logging_save.jpg "Symbol für Speichern") und geben einen Namen für Ihr Dashboard ein.  

    **Hinweis:** Wenn Sie versuchen, ein Dashboard unter einem Namen zu speichern, der Leerzeichen enthält, wird es nicht gespeichert. Geben Sie einen Namen ohne Leerzeichen ein und klicken Sie auf das Symbol **Speichern**.

    ![Name zum Speichern des Dashboards](images/logging_save_dashboard.jpg "Name zum Speichern des Dashboards"). 

Sie haben jetzt ein Dashboard erstellt, das Ihre Protokolleinträge nach Instanz-ID filtert. Sie können Ihr gespeichertes Dashboard jederzeit laden, indem Sie auf das Symbol **Ordner** ![Ordnersymbol](images/logging_folder.jpg "Ordnersymbol") klicken und Ihr Dashboard über den Namen auswählen.  
