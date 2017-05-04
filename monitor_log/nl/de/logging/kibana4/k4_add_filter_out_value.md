---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filter für einen Wert hinzufügen, der nicht in der Liste *Fields* enthalten ist
{:#k4_add_filter_out_value}

Wenn Sie einen Filter für einen Wert hinzufügen wollen, der nicht in der Feldliste *Fields* angezeigt wird, suchen Sie durch eine Abfrage nach Datensätzen, die den Wert enthalten. Anschließend fügen Sie den Filter über den Tabelleneintrag hinzu, der auf der Seite 'Discover' verfügbar ist.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um einen Filter für einen Wert hinzuzufügen, der nicht in der Liste im Abschnitt *Fields* verfügbar ist: 

1. Schauen Sie sich die Kibana-Seite 'Discover' an, um festzustellen, welche Untergruppe Ihrer Daten dort angezeigt wird. Weitere Informationen finden Sie unter [Auf der Kibana-Seite 'Discover' angezeigte Daten ermitteln](logging_kibana_analize_logs_interactively.html#k4_identify_data). 

    Die folgende Abbildung zeigt zum Beispiel die Werte von Instanzen für eine CF-App in der Feldliste *Fields*.  
    
    ![Werte in der Feldliste 'Fields'](images/k4_add_filter_f1.jpg "Werte in der Feldliste 'Fields'")
    
    Sie interessieren sich für die Instanz mit der Nummer *3*, die jedoch in der angezeigten Liste nicht verfügbar ist. 

2. Ändern Sie auf der Seite 'Discover' die Abfrage, um nach einem bestimmten Feldwert zu suchen. 

    Beispiel: Für die Suche nach Instanz *3* sieht die Abfrage, die Sie eingeben, wie folgt aus:
   `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:"3"`
    
    ![Abfrage ändern](images/k4_add_filter_f2.jpg "Abfrage ändern")
    
    In der Tabelle werden alle Datensätze angezeigt, die Ihrer Abfrage entsprechen.  
    
 3. Erweitern Sie einen Datensatz und wählen Sie die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Inklusivmodus](images/k4_include_field_icon.jpg "Schaltfläche mit Lupensymbol im Inklusivmodus") aus, um einen Filter hinzuzufügen. 
 
     Beispiel: Zum Hinzufügen eines Filters für die Instanz-ID mit dem Wert *3* klicken Sie auf die Schaltfläche mit dem Lupensymbol ![Schaltfläche mit Lupensymbol im Inklusivmodus](images/k4_include_field_icon.jpg "Schaltfläche mit Lupensymbol im Inklusivmodus") neben dem Feld *instance_id*. 
     
     ![Tabelle anzeigen](images/k4_add_filter_f3.jpg "Tabelle anzeigen")
     
4. Prüfen Sie, ob der Filter hinzugefügt wurde. 

    Die folgende Abbildung zeigt zum Beispiel den aktivierten Filter, nachdem Sie ihn über die Tabelle hinzugefügt haben. 
    
    ![Filter anzeigen](images/k4_add_filter_f4.jpg "Filter anzeigen")
    
    
