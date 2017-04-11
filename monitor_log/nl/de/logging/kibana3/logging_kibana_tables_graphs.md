---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Tabellen und Diagramme aus Abfragen in Kibana erstellen
{: #logging_kibana_tables_graphs}


In Kibana können Sie Diagramme und Tabellen für Ihre Abfragen erstellen, um die Protokolldaten zu visualisieren und Ergebnisse zu vergleichen. Sie können über die Registerkarte **Protokolle** für Ihre Cloud Foundry-App auf das Kibana-Dashboard zugreifen. 
{:shortdesc}

Das Kibana-Dashboard besitzt ein Zeilenlayout, bei dem jede Zeile eine oder mehrere Anzeigen enthält. Sie können Anzeigen so konfigurieren, dass sie grafische Darstellungen Ihrer Daten anzeigen. Mithilfe von Abfragen legen Sie fest, welche Daten angezeigt werden sollen. Zum Erstellen eines Diagramms oder einer Tabelle müssen Sie zunächst eine leere Zeile (Row) erstellen. Anschließend erstellen Sie eine Anzeige (Panel). Wenn Sie auf das Kibana-Dashboard über die Registerkarte **Protokolle** Ihrer CF-App zugreifen, zeigt das Dashboard automatisch zwei Anzeigen an: ein Histogramm und eine Tabelle.

Führen Sie die folgenden Tasks aus, um ein Diagramm oder eine Tabelle im Kibana-Dashboard hinzuzufügen:

1. Für den Zugriff auf die Registerkarte **Protokolle** Ihrer Cloud Foundry-App klicken Sie auf den App-Namen in der Tabelle **Cloud Foundry-Anwendungen** im {{site.data.keyword.Bluemix_notm}}-Dashboard **Apps** und anschließend auf die Registerkarte **Protokolle**. Die Protokolle für Ihre App werden angezeigt.

2. Greifen Sie auf die Anzeige im Kibana-Dashboard für Ihre App zu, indem Sie auf **Erweiterte Ansicht** ![Link für erweiterte Ansicht](images/logging_advanced_view.jpg). Das Kibana-Dashboard wird angezeigt.

3. Blättern Sie im Kibana-Dashboard zum Ende der Dashboardanzeige und klicken Sie auf **ADD A ROW** ![Symbol für "Zeile hinzufügen"](images/logging_add_row.jpg), um eine Zeile für die Anzeige zu erstellen, die hinzugefügt werden soll. Das Teilfenster **Dashboard Settings** wird angezeigt. 
	
	![Teilfenster für Dashboardeinstellungen](images/logging_dashboard_settings.jpg)
	
	Geben Sie im Teilfenster 'Add Row' einen Namen für Ihre Zeile in das Feld **Title** ein und klicken Sie dann auf **Create Row**. Eine neue Zeile wird hinzugefügt. Sie können die Reihenfolge der Zeilen anpassen, indem Sie auf das **Aufwärtspfeilsymbol** oder das **Abwärtspfeilsymbol** neben den Zeilentiteln klicken. Wenn Sie die Reihenfolge der Zeilen festgelegt haben, klicken Sie auf **Save**. Eine leere Zeile wurde nun im Kibana-Dashboard erstellt.

4. Fügen Sie eine Anzeige hinzu, indem Sie auf **Add panel to empty row** klicken. Das Teilfenster **Row Settings** wird angezeigt.

    ![Teilfenster für Zeileneinstellungen](images/logging_row_settings.jpg)
	
	Sie können verschiedene Anzeigentypen (Panel Type) wie **table** (Tabelle), **histogram** (Histogramm) oder **terms** (Bedingungen) in der Dropdown-Liste **Select Panel Type** auswählen. Wählen Sie **terms** aus, um ein Balkendiagramm, ein Kreisdiagramm oder eine Tabelle auf der Basis Ihrer Abfragen zu erstellen. Eine Reihe von Konfigurationsoptionen wird im Teilfenster **Row Settings** angezeigt.
	
	![Anzeige im Teilfenster für Zeileneinstellungen hinzufügen](images/logging_add_panel.jpg)
	
	Konfigurieren Sie Ihre Anzeige. Geben Sie einen Titel (**Title**) für Ihre grafische Darstellung ein. Wählen Sie **Span** für Ihre Anzeige in der Dropdown-Liste aus. Der Wert von **Span** legt die Breite Ihrer Anzeige über das Dashboard fest. Löschen Sie im Abschnitt 'Parameters' den Inhalt von **Field** und geben Sie ein gültiges Protokollfeld ein. Beispiel: `instance_id`. 

5. Wählen Sie im Abschnitt 'View Options' die Option **bar**, **pie** oder **table** in der Dropdown-Liste **Style** aus, um ein Balkendiagramm, ein Kreisdiagramm oder eine Tabelle auszuwählen. Wählen Sie im Abschnitt 'Queries' die Option **selected** in der Dropdown-Liste **Queries** aus, um die Protokolldaten aus Ihren Dashboardabfragen zu verwenden. Klicken Sie zum Schluss auf **Save**. Ihre neue Anzeige wird im Dashboard angezeigt.

	![Dashboard mit Anzeige eines Balkendiagramms](images/logging_bar_chart_panel.jpg)
	
6. Wenn Sie diese Anzeige ändern möchten, sodass eine Tabelle angezeigt wird, klicken Sie auf das Symbol **Konfigurieren** ![Symbol für Konfigurieren](images/logging_dashboard_config_panel.jpg). Das Teilfenster **Terms Settings** wird angezeigt. 

	![Teilfenster für Bedingungseinstellungen](images/logging_terms_settings.jpg)
	
	Klicken Sie auf die Registerkarte **Panel** und wählen Sie die Option **table** in der Dropdown-Liste **Style** aus. Klicken Sie auf **Save**, um die Anzeige zu aktualisieren, und kehren Sie zum Dashboard zurück.

7. Fügen Sie Ihrem Dashboard weitere Zeilen und Anzeigen hinzu. Wenn Sie Ihre Anpassungen abgeschlossen haben, speichern Sie die Änderungen an diesem Dashboard, indem Sie auf das Symbol **Speichern** klicken.

    **Hinweis:** Wenn Sie versuchen, ein Dashboard unter einem Namen zu speichern, der Leerzeichen enthält, wird es nicht gespeichert. Geben Sie einen Namen ohne Leerzeichen ein und klicken Sie auf das Symbol **Speichern**.

    ![Name zum Speichern des Dashboards](images/logging_save_dashboard.jpg)


