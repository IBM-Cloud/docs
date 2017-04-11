---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Protokolle für Cloud Foundry-Apps mit Abfragen in Kibana filtern
{: #logging_kibana_query}

Mit Kibana können Sie Abfragen erstellen, um Ihre Protokolle auf Schlüsselbegriffe zu durchsuchen und nach diesen Begriffen zu filtern. Sie können die Abfragen visuell im Kibana-Dashboard vergleichen. Sie können über die Registerkarte **Protokolle** für Ihre Cloud Foundry-App auf das Kibana-Dashboard zugreifen. 
{:shortdesc}

Führen Sie die folgenden Tasks aus, um eine Abfrage für Ihre Cloud Foundry-App-Protokolle im Kibana-Dashboard zu erstellen:

1. Greifen Sie auf die Registerkarte **Protokolle** Ihrer Cloud Foundry-App zu. 

    1. Klicken Sie auf den App-Namen im {{site.data.keyword.Bluemix_notm}}-Dashboard **Apps**.
    2. Klicken Sie auf die Registerkarte **Protokolle**. 
    
    Die Protokolle für Ihre App werden angezeigt.

2. Greifen Sie auf das Kibana-Dashboard für Ihre App zu. Klicken Sie auf **Erweiterte Ansicht** ![Link für erweiterte Ansicht](images/logging_advanced_view.jpg). Das Kibana-Dashboard wird angezeigt.

3. Klicken Sie im Kibana-Dashboard auf das Symbol **QUERY** ![Abfragesymbol](images/logging_query.jpg), um das Feld anzuzeigen. Wenn Sie auf Kibana zugreifen, um Ihre App-Protokolle auf der Registerkarte **Protokolle** für Ihre App anzuzeigen, wird eine Abfrage erstellt, durch die alle Protokolle für die Anwendungs-ID (application_id) Ihrer App angezeigt werden.
	
    Zum Bearbeiten Ihrer Abfrage klicken Sie auf das Feld **QUERY** und geben einen Suchbegriff ein.

    * Für die Suche nach einem Schlüsselwort oder einem Teil eines Schlüsselworts geben Sie ein Wort gefolgt von einem Platzhalterzeichen \* ein. Beispiel: `Java*`. 
	* Für die Suche nach einem bestimmten Ausdruck geben Sie diesen Ausdruck in doppelten Anführungszeichen ein. Beispiel: `"Java/1.8.0"`.
	* Für komplexere Suchen können Sie die logischen Bedingungsverknüpfungen AND und OR verwenden. Beispiel: `"Java/1.8.0" OR "Java/1.7.0"`.
	* Für die Suche nach einem Wert in einem bestimmten Feld geben Sie Ihre Suche in der folgenden Form an: *Protokollfeldname:Suchbegriff*. Beispiel: `instance_id:1`.
	* Für die Suche nach einem Wertebereich für ein bestimmtes Protokollfeld geben Sie Ihre Suche in der folgenden Form ein: *Protokollfeldname:[Bereichsanfang TO Bereichsende]*. Beispiel: `instance_id:[1 TO 2]`.

4. Wenn Sie die Ergebnisse von zwei separaten Abfragen vergleichen wollen, können Sie Ihrem Dashboard eine weitere Abfragebedingung hinzufügen. Zum Hinzufügen einer weiteren Abfrage klicken Sie auf das Symbol **+** am Ende des Felds **QUERY**.

    ![Abfragefeld](images/logging_query_field.jpg)
	
    Ein neues Feld **QUERY** mit dem Platzhalterzeichen \* wird angezeigt. Diese Abfrage weist Kibana an, alle Einträge einzuschließen.
	
    ![Zusätzliches Abfragefeld](images/logging_additional_query_field.jpg)
	
    Ihr Dashboard wird mit den Ergebnissen Ihrer neuen Abfrage aktualisiert. Das Teilfenster **EVENTS BY TIME** zeigt eine grafische Darstellung für beide Abfragen mit Angabe der Anzahl der Bedingungen (Terms) für jede Abfrage in Klammern an. 
	
    ![Dashboard mit einem Diagramm für beide Abfragen](images/logging_dashboard_queries.jpg)
	
5. Klicken Sie auf das neue Feld **QUERY**, um den Inhalt zu bearbeiten und eine Abfragebedingung hinzuzufügen. Beispiel: `instance_id:1`. Vergleichen Sie die Ergebnisse Ihrer Abfragen im Teilfenster **EVENTS BY TIME**.

    ![Dashboard mit einem Diagramm für beide Abfragen](images/logging_dashboard_queries2.jpg)

6. Zum Löschen einer Abfrage setzen Sie den Mauszeiger auf das Feld **QUERY**, das Sie löschen wollen, um das Symbol **Löschen** einzublenden. Klicken Sie auf das Symbol **Löschen**.

    ![Abfragefeld mit Löschsymbol](images/logging_delete_query.jpg)

7. Zum Speichern dieses Dashboards unter einem wiedererkennbaren Namen klicken Sie auf das Symbol **Speichern** ![Symbol für Speichern](images/logging_save.jpg) und geben einen Namen für Ihr Dashboard an. 

    **Hinweis:** Wenn Sie versuchen, ein Dashboard unter einem Namen zu speichern, der Leerzeichen enthält, wird es nicht gespeichert. Geben Sie einen Namen ohne Leerzeichen ein und klicken Sie auf das Symbol **Speichern**.

    ![Name zum Speichern des Dashboards](images/logging_save_dashboard.jpg)


