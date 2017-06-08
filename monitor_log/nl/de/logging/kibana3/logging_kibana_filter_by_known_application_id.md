---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Protokolle für Cloud Foundry-Apps nach bekannter Anwendungs-ID in Kibana filtern
{: #logging_kibana_known_application_id}

Wenn Sie die Anwendungs-ID Ihrer Cloud Foundry-App kennen, können Sie die Protokolle nach der Anwendungs-ID (application_id) Ihrer App im Kibana-Dashboard schnell anzeigen und filtern. Sie können über die Registerkarte **Protokolle** für Ihre Cloud Foundry-App auf das Kibana-Dashboard zugreifen. 
{:shortdesc}


Führen Sie die folgenden Tasks aus, um Ihre Cloud Foundry-App-Protokolle nach bekannter Anwendungs-ID im Kibana-Dashboard anzuzeigen und zu filtern:

1. Greifen Sie auf die Registerkarte **Protokolle** Ihrer Cloud Foundry-App zu. 

    1. Klicken Sie auf den App-Namen im {{site.data.keyword.Bluemix_notm}}-Dashboard **Apps**.
    2. Klicken Sie auf die Registerkarte **Protokolle**. 
    
    Die Protokolle für Ihre App werden angezeigt.

2. Greifen Sie auf das Kibana-Dashboard für Ihre App zu. Klicken Sie auf **Erweiterte Ansicht** ![Link für erweiterte Ansicht](images/logging_advanced_view.jpg "Link für Erweiterte Ansicht"). Das Kibana-Dashboard wird angezeigt.

3. Klicken Sie im Kibana-Dashboard auf das Symbol **Ordner** ![Ordnersymbol](images/logging_folder.jpg "Ordnersymbol"), um ein Menü anzuzeigen, in dem alle zuletzt verwendeten Dashboards aufgelistet sind. 

    **Hinweis:** Neben den Dashboards, die Sie unter einem Namen gespeichert haben, werden in dem Menü unbenannte Dashboards im folgenden Format aufgelistet: *ALCH_TENANT_ID_Anwendungs-ID*. 

    ![Liste der Dashboards](images/logging_list_of_dashboards.jpg "Liste der Dashboards")

4. Wählen Sie das Dashboard mit einem Namen aus, der Ihre bekannte Anwendungs-ID (application_id) enthält. 

    Das Dashboard wird geladen und zeigt Informationen an, die nach Ihrer Anwendungs-ID gefiltert sind.

5. Optional können Sie Ihrem Filterabschnitt weitere Felder hinzufügen, wie zum Beispiel **instance_id**, um die Filterung von Datensätzen nach Instanz-ID zu aktivieren bzw. zu inaktivieren. 
  
    1. Klicken Sie im Fenster **ALL EVENTS** auf eine Protokollereigniszeile, um die Details für dieses Ereignis anzuzeigen. 
	
        ![Fenster 'All Events' mit Details für ein ausgewähltes Protokollereignis](images/logging_selected_log_event.jpg "Fenster 'All Events' mit Details für ein ausgewähltes Protokollereignis")
	
    2. Wählen Sie ein Ereignis aus, das den Feldwert anzeigt, nach dem Sie filtern wollen.
	
    3. Fügen Sie einen Filter hinzu.
    
        Zum Hinzufügen eines Filters, der Informationen zu einem bestimmten Feldwert einschließt, klicken Sie auf das **Lupensymbol** ![Lupensymbol](images/logging_magnifying_glass.jpg "Lupensymbol") in der Zeile der Tabelle, die das Feld enthält, nach dem gefiltert werden soll. 
	
        Zum Hinzufügen eines Filters, der Informationen zu einem bestimmten Feldwert ausschließt, klicken Sie auf das **Ausschlusssymbol** ![Ausschlusssymbol](images/logging_exclusion_icon.png "Ausschlusssymbol") in der Zeile der Tabelle, die das Feld enthält, nach dem gefiltert werden soll.  

        Im Kibana-Dashboard wird eine neue Filterbedingung hinzugefügt.
	
	    ![Filterbedingung für das Feld 'instance_id'](images/logging_instance_id_filter.jpg "Filterbedingung für das Feld 'instance_id'")
	
6. Speichern Sie dieses Dashboard mit einem wiedererkennbaren Namen. 

    Klicken Sie auf das Symbol **Speichern** ![Symbol für Speichern](images/logging_save.jpg "Symbol für Speichern") und geben Sie einen Namen für Ihr Dashboard ein. 

    **Hinweis:** Wenn Sie versuchen, ein Dashboard unter einem Namen zu speichern, der Leerzeichen enthält, wird es nicht gespeichert. Geben Sie einen Namen ohne Leerzeichen ein und klicken Sie auf das Symbol **Speichern**.

    ![Name zum Speichern des Dashboards](images/logging_save_dashboard.jpg "Name zum Speichern des Dashboards").


Sie haben jetzt ein Dashboard erstellt, das Ihre Protokolleinträge nach Anwendungs-ID und Instanz-ID filtert. Sie können Ihr gespeichertes Dashboard jederzeit laden, indem Sie auf das Symbol **Ordner** ![Ordnersymbol](images/logging_folder.jpg "Ordnersymbol") klicken und Ihr Dashboard über den Namen auswählen.
