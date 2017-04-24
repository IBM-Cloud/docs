---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokolle durch Definieren von angepassten Suchabfragen filtern
{:#k4_filter_queries}

In der Suchleiste der Seite 'Discover' können Sie Suchabfragen in der Abfragesprache 'Lucene' definieren und speichern. Auf jede Suche können Sie Filter anwenden, um die Einträge einzugrenzen, die für die Analyse verfügbar sind.
{:shortdesc}

Führen Sie die folgenden Tasks aus, um Ihre Protokolle durch eine angepasste Suche zu filtern: 

1. Greifen Sie auf die Registerkarte **Protokolle** Ihrer Cloud Foundry-App (CF-App) oder Ihres Containers zu.  

    1. Klicken Sie auf den App-Namen oder Container im {{site.data.keyword.Bluemix}}-Dashboard. 
    2. Klicken Sie für CF-Anwendungen auf die Registerkarte **Protokolle**. Klicken Sie für Container auf **Überwachung und Protokolle** und wählen Sie anschließend die Registerkarte **Protokollierung** aus. 
    
    Die Protokolle werden angezeigt. 

2. Greifen Sie auf Kibana zu. Klicken Sie auf **Erweiterte Ansicht** ![Link für erweiterte Ansicht](images/logging_advanced_view.jpg). Das Kibana-Dashboard wird angezeigt.

    Wenn Sie auf Kibana zugreifen, wird die Standardsuche angewendet. Die Protokolle für die Liste der Instanzen der Ressource wird angezeigt, für die Sie Kibana gestartet haben. Sie können die Protokolle nach beliebigen oder allen {{site.data.keyword.Bluemix_notm}}-Ressourcen in dem jeweiligen Bereich filtern. 

Für Lucene wird nicht "Schlüsselwort" ("keyword"), sondern vielmehr "Begriff" ("term") verwendet. 

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



