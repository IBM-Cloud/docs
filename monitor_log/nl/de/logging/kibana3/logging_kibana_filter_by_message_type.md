---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-16"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Protokolle für Cloud Foundry-Apps nach Nachrichtentyp in Kibana filtern
<!-- for example, Uploading your data -->
{: #logging_kibana_message_type_filter}
<!-- Provide an appropriate ID above -->

Sie können Protokolle für {{site.data.keyword.Bluemix_notm}}-Anwendungen nach Nachrichtentyp im Kibana-Dashboard anzeigen und filtern. Sie können über die Registerkarte **Protokolle** für Ihre Cloud Foundry-App auf das Kibana-Dashboard zugreifen. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Führen Sie die folgenden Tasks aus, um Ihre Cloud Foundry-App-Protokolle nach Nachrichtentyp im Kibana-Dashboard anzuzeigen und zu filtern:

1. Greifen Sie auf die Registerkarte **Protokolle** Ihrer Cloud Foundry-App zu. 

    1. Klicken Sie auf den App-Namen im {{site.data.keyword.Bluemix_notm}}-Dashboard **Apps**.
    2. Klicken Sie auf die Registerkarte **Protokolle**. 
    
    Die Protokolle für Ihre App werden angezeigt.

2. Greifen Sie auf das Kibana-Dashboard für Ihre App zu. Klicken Sie auf **Erweiterte Ansicht** ![Link für erweiterte Ansicht](images/logging_advanced_view.jpg). Das Kibana-Dashboard wird angezeigt.

3. Klicken Sie im Fenster **ALL EVENTS** auf das Rechtspfeilsymbol, um alle Felder anzuzeigen. 

    ![Fenster 'All Events' mit dem Rechtspfeilsymbol](images/logging_all_events_no_fields.jpg)

4. Wählen Sie im Teilfenster **Fields** die Option **message_type** aus, um die Komponente anzuzeigen, die den jeweiligen Protokolleintrag im Fenster **ALL EVENTS** generiert hat.

    ![Fenster 'All Events' mit ausgewähltem Feld 'message_type'](images/logging_message_type.png)

5. Klicken Sie im Fenster **ALL EVENTS** auf eine Protokollereigniszeile, um die Details für dieses Ereignis anzuzeigen. Wählen Sie ein Ereignis aus, das den Wert für **message_type** anzeigt, nach dem Sie filtern wollen.

    ![Fenster 'All Events' mit Details für ein ausgewähltes Protokollereignis](images/logging_message_type_add_filter.png)

6. Fügen Sie einen Filter hinzu, um Informationen zu einem Nachrichtentyp ein- oder auszuschließen. 

    * Zum Hinzufügen eines Filters, der Informationen zu einem Nachrichtentyp einschließt, klicken Sie auf das **Lupensymbol** ![Lupensymbol](images/logging_magnifying_glass.jpg) in der Zeile 'message_type' der Tabelle. 
    
           ![Filterbedingung für das Feld 'message_type'](images/logging_message_type_filter.png)
    
    * Zum Hinzufügen eines Filters, der Informationen zu einem bestimmten Nachrichtentyp ausschließt, klicken Sie auf das **Ausschlusssymbol** ![Ausschlusssymbol](images/logging_exclusion_icon.png) in der Zeile 'message_type' der Tabelle. 
    
    Im Kibana-Dashboard wird eine neue Filterbedingung hinzugefügt.

7. Sie können den vorherigen Schritt optional wiederholen, um einen Filter für andere Nachrichtentypen hinzuzufügen. Eine vollständige Liste der Nachrichtentypen finden Sie unter [Protokollformat](../logging_view_kibana3.html#kibana_log_format_cf).

9. Speichern Sie das Dashboard.    
        
    Wenn Sie die Erstellung Ihrer Filter abgeschlossen haben, klicken Sie auf das Symbol **Speichern** ![Symbol für Speichern](images/logging_save.jpg) und geben einen Namen für Ihr Dashboard ein. 
      
    **Hinweis:** Wenn Sie versuchen, ein Dashboard unter einem Namen zu speichern, der Leerzeichen enthält, wird es nicht gespeichert. Geben Sie einen Namen ohne Leerzeichen ein und klicken Sie auf das Symbol **Speichern**.
    
    ![Name zum Speichern des Dashboards](images/logging_save_dashboard.jpg)

Sie haben jetzt ein Dashboard erstellt, das Ihre Protokolleinträge nach Nachrichtentyp filtert. Sie können Ihr gespeichertes Dashboard jederzeit laden, indem Sie auf das Symbol **Ordner** ![Ordnersymbol](images/logging_folder.jpg) klicken und Ihr Dashboard über den Namen auswählen.
