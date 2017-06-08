---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Angepasste Suchabfragen definieren
{:#k4_define_search}

In der Suchleiste der Seite 'Discover' können Sie Suchabfragen in der Abfragesprache 'Lucene' definieren und speichern. Auf jede Suche können Sie Filter anwenden, um die Einträge einzugrenzen, die für die Analyse verfügbar sind.
{:shortdesc}

Führen Sie die folgenden Tasks aus, um eine angepasste Suche zu definieren:

1. Greifen Sie auf die Registerkarte **Protokolle** Ihrer Cloud Foundry-App (CF-App) oder Ihres Containers zu. 

    1. Klicken Sie auf den App-Namen oder Container im {{site.data.keyword.Bluemix}}-Dashboard.
    2. Klicken Sie für CF-Anwendungen auf die Registerkarte **Protokolle**. Klicken Sie für Container auf **Überwachung und Protokolle** und wählen Sie anschließend die Registerkarte **Protokollierung** aus.
    
    Die Protokolle werden angezeigt.

2. Greifen Sie auf Kibana zu. Klicken Sie auf **Erweiterte Ansicht** ![Link für erweiterte Ansicht](images/logging_advanced_view.jpg "Link für Erweiterte Ansicht"). Das Kibana-Dashboard wird angezeigt.

    Wenn Sie auf Kibana zugreifen, wird die Standardsuche angewendet. Die Protokolle für die Liste der Instanzen der Ressource wird angezeigt, für die Sie Kibana gestartet haben. Sie können die Protokolle nach beliebigen oder allen {{site.data.keyword.Bluemix_notm}}-Ressourcen in dem jeweiligen Bereich filtern.

3. Schauen Sie sich die Seite 'Discover' an, um festzustellen, welche Untergruppe Ihrer Daten dort angezeigt wird. Weitere Informationen finden Sie unter [Auf der Kibana-Seite 'Discover' angezeigte Daten ermitteln](logging_kibana_analize_logs_interactively.html#k4_identify_data). Ändern Sie anschließend die Standardabfrage, um Einträge zu filtern.

    **Hinweis:** Verwenden Sie die Abfragesprache Lucene zum Definieren Ihrer angepassten Abfrage. Weitere Informationen finden Sie unter [Apache Lucene - Query Parser Syntax  ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}.
    
    Wenn Kibana aus {{site.data.keyword.Bluemix_notm}} heraus gestartet wird, können Sie zum Ändern der Abfrage und zum Definieren mehrerer Suchkriterien die logischen Operatoren **AND** und **OR** verwenden. Diese Operatoren müssen in Großbuchstaben angegeben werden.    
    
    * Für die Suche nach einem Schlüsselwort oder einem Teil eines Schlüsselworts geben Sie ein Wort gefolgt von einem Platzhalterzeichen \* ein. Beispiel: `Java*`. 
    * Für die Suche nach einem bestimmten Ausdruck geben Sie diesen Ausdruck in doppelten Anführungszeichen ein. Beispiel: `"Java/1.8.0"`.
    * Für komplexere Suchen können Sie die logischen Bedingungsverknüpfungen AND und OR verwenden. Beispiel: `"Java/1.8.0" OR "Java/1.7.0"`.
    * Für die Suche nach einem Wert in einem bestimmten Feld geben Sie Ihre Suche in der folgenden Form an: *Protokollfeldname:Suchbegriff*. Beispiel: `instance_id:"1"`.
    * Für die Suche nach einem Wertebereich für ein bestimmtes Protokollfeld geben Sie Ihre Suche in der folgenden Form ein: *Protokollfeldname:[Bereichsanfang TO Bereichsende]*. Beispiel: `instance_id:["1" TO "2"]`.

     Beispiel: Für eine CF-App können Sie eine Abfrage wie `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]` erstellen, die nur Einträge für Instanzen *0* und *1* auflistet. 

4. Speichern Sie die Abfrage, sodass Sie sie später wiederverwenden können. Weitere Informationen finden Sie unter [Suche speichern](logging_kibana_filtering_logs.html#k4_save_search). 

**Hinweis:** Wenn Sie eine Abfrage löschen müssen, finden Sie weitere Informationen unter [Suche löschen](logging_kibana_filtering_logs.html#k4_delete_search).



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


## Suche erneut laden
{: #k4_reload_search}

Führen Sie die folgenden Schritte aus, um eine gespeicherte Suche zu laden:

1. Klicken Sie in der Symbolleiste der Seite 'Discover' auf die Schaltfläche **Load Search** ![Suche laden](images/k4_load_icon.jpg "Suche laden").

2. Wählen Sie die Suche aus, die Sie laden wollen. 

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
