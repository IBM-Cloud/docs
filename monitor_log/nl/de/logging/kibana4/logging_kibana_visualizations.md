---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokolle in Kibana mit Visualisierungen analysieren 
{:#logging_kibana_visualizations}

Auf der Seite *Visualize* in Kibana können Sie Visualisierungen wie Diagramme und Tabellen erstellen, mit deren Hilfe Sie Ihre Protokolldaten analysieren und Ergebnisse vergleichen können.
{:shortdesc}

Sie können eine Visualisierung allein zur Analyse Ihrer Protokolle verwenden.  

* Sie können Visualisierungen über eine Suche, die Sie auf der Seite *Discover* definieren und speichern, oder über eine neue Abfrage, die Sie auf der Seite *Visualize* definieren, erstellen. Die Suche definiert die Untergruppe von Daten, die eine Visualisierung darstellt. 

* Durch den Typ von Visualisierung, den Sie auswählen, wird bestimmt, wie die Daten zur Analyse angezeigt werden. 

In der folgenden Tabelle sind die verschiedenen Visualisierungstypen aufgeführt: 

| Visualisierungstyp | Beschreibung |
|-----------------------|-------------|
| Flächendiagramm (Area Chart) | Zeigt quantitative Daten grafisch an. Dient zum Vergleich von zwei oder mehr Gruppen aggregierter Daten. |
| Datentabelle (Data Table) | Zeigt Rohdaten in tabellarischer Form für eine zusammengesetzte Aggregation an. |
| Kurvendiagramm (Line Chart) | Zeigt zeitbasierte Daten an. Dient zum Vergleich von zwei oder mehr Gruppen zeitbasierter aggregierter Daten. |
| Markdown-Widget | Dient zum Anzeigen von Textinformationen. |
| Metrik (Metric) | Dient zum Anzeigen einer Trefferanzahl oder des exakten Durchschnittswerts eines numerischen Felds. |
| Kreisdiagramm (Pie Chart) | Dient zum Anzeigen verschiedener Werte eines Felds. | 
| Vertikales Balkendiagramm (Vertical Bar Chart) | Zeigt zeitbasierte und nicht zeitbasierte Daten an. Dient zum Gruppieren von Daten. |

Auf der Seite 'Visualize' können Sie beliebige der folgenden Tasks ausführen:

| Task | Weitere Informationen |
|------|------------------|
| [Neue Visualisierung erstellen](logging_kibana_visualizations.html#logging_k4_visualizations_create) | Sie können Visualisierungen über eine Suche, die Sie auf der Seite *Discover* definieren und speichern, oder über eine neue Abfrage, die Sie auf der Seite *Visualize* definieren, erstellen. |
| [Visualisierung speichern](logging_kibana_visualizations.html#logging_kibana_visualizations_save) | Sie können Visualisierungen zur späteren Wiederverwendung speichern. |
| [Visualisierung laden](logging_kibana_visualizations.html#logging_kibana_visualizations_reload) | Sie können eine Visualisierung hochladen, um die Daten zu aktualisieren, zu ändern oder zu analysieren. |
| [Visualisierung löschen](logging_kibana_visualizations.html#logging_kibana_visualizations_delete) | Sie können Visualisierungen löschen, die nicht benötigt werden. |
| [Visualisierung exportieren](logging_kibana_visualizations.html#logging_kibana_visualizations_export) | Sie können eine Visualisierung als JSON-Datei exportieren.  |
| [Visualisierung importieren](logging_kibana_visualizations.html#logging_kibana_visualizations_import) | Sie können eine Visualisierung als JSON-Datei importieren.  |
| [Visualisierung gemeinsam nutzen](logging_kibana_visualizations.html#logging_kibana_visualizations_share) | Sie können eine Visualisierung in Ihrem HTML-Quelltext oder über das Kibana-Dashboard zur gemeinsamen Nutzung verfügbar machen.  |


## Visualisierungen über Abfragen in Kibana erstellen
{:#logging_k4_visualizations_create}

Führen Sie die folgenden Schritte aus, um eine Visualisierung auf der Seite 'Visualize' zu erstellen: 

1. Starten Sie Kibana und wählen Sie die Seite **Visualize** aus. 

2. Erstellen Sie eine neue Visualisierung. Klicken Sie in der Symbolleiste auf die Schaltfläche für **Neue Visualisierung** ![Neue Visualisierung](images/k4_visualization_new_icon.jpg "Neue Visualisierung"). 

3. Wählen Sie eine Visualisierung aus. 
    
4. Wählen Sie eine Suchquelle aus. Wählen Sie eine der folgenden Optionen aus:

    * Klicken Sie auf **From a new search** (Aus neuer Suche). 
    * Klicken Sie auf **From a saved search** (Aus gespeicherter Suche).  
  
5. Konfigurieren Sie die Abfrage. 

    * Wenn Sie die Option **From a saved search** auswählen, wählen Sie eine Suchabfrage aus. Die Abfrage dient zum Abrufen der Daten, die für die Visualisierung verwendet werden. 

        Nach der Auswahl einer Suche werden das Erstellungsprogramm für Visualisierungen (Visualization Builder) geöffnet und die Daten für die ausgewählte Abfrage geladen. Die folgende Nachricht wird angezeigt: *This visualization is linked to a saved search: Name_Ihrer_Suche* (Diese Visualisierung ist mit einer gespeicherten Suche verknüpft: Name_Ihrer_Suche). 
	
	**Hinweis:** Alle Änderungen, die Sie an der gespeicherten Suche vornehmen, werden automatisch in der Visualisierung wiedergegeben. Wenn Sie die automatischen Aktualisierungen nach Änderungen, die Sie an der Abfrage vornehmen, die mit dieser Visualisierung verknüpft ist, inaktivieren wollen, klicken Sie doppelt auf die Nachricht *This visualization is linked to a saved search: Name_Ihrer_Suche*.  

    * Wenn Sie die Option **From a new search** auswählen, definieren Sie eine neue Abfrage. Die Abfrage dient zum Definieren der Untergruppe von Daten, die von der Visualisierung abgerufen und verwendet werden.

        Weitere Informationen finden Sie unter [Protokolle durch Definieren angepasster Abfragen filtern](k4_filter_queries.html#k4_filter_queries). 

6. Wählen Sie im Erstellungsprogramm für Visualisierungen eine Metrikaggregation für die Y-Achse aus. 

7. Wählen Sie im Erstellungsprogramm für Visualisierungen einen Buckettyp aus. Wählen Sie anschließend eine Bucketaggregation aus.
  
8. Fügen Sie Subbuckets hinzu, um die Daten weiter aufzugliedern.

Weitere Informationen zu Kibana finden Sie in der Veröffentlichung [Kibana User Guide ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
 
## Visualisierung speichern
{:#logging_kibana_visualizations_save}

Führen Sie die folgenden Schritte aus, um eine Visualisierung auf der Seite 'Visualize' zu speichern:

1. Klicken Sie in der Symbolleiste der Seite 'Visualize' auf die Schaltfläche **Save Visualization** ![Visualisierung speichern](images/k4_visualization_save_icon.jpg "Visualisierung speichern"). 

2. Geben Sie einen Namen für die Visualisierung ein. 

3. Klicken Sie auf 'Save' (Speichern).  

## Visualisierung laden
{:#logging_kibana_visualizations_reload}

Führen Sie die folgenden Schritte aus, um eine gespeicherte Visualisierung zu laden: 

1. Klicken Sie in der Symbolleiste der Seite 'Visualize' auf die Schaltfläche **Load Saved Visualization** ![Gespeicherte Visualisierung laden](images/k4_visualization_open_icon.jpg "Gespeicherte Visualisierung laden"). 

2. Wählen Sie die Visualisierung aus, die Sie laden wollen.  



## Visualisierung löschen
{:#logging_kibana_visualizations_delete}

Führen Sie die folgenden Schritte auf der Seite 'Settings' aus, um eine Visualisierung zu löschen: 

1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus. 

2. Wählen Sie auf der Registerkarte **Visualizations** die Visualisierungen aus, die Sie löschen wollen. 

3. Klicken Sie auf **Delete** (Löschen). 


## Visualisierung exportieren
{:#logging_kibana_visualizations_export}

Führen Sie die folgenden Schritte auf der Seite 'Settings' aus, um eine Visualisierung als JSON-Datei zu exportieren: 

1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus. 

2. Wählen Sie auf der Registerkarte **Visualizations** die Visualisierung aus, die Sie exportieren wollen. 

3. Klicken Sie auf **Export**. 

4. Speichern Sie Datei. 

## Visualisierung importieren
{:#logging_kibana_visualizations_import}

Führen Sie die folgenden Schritte auf der Seite 'Settings' aus, um eine Visualisierung als JSON-Datei zu importieren: 

1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus. 

2. Wählen Sie auf der Registerkarte **Visualizations** die Option **Import** aus. 

3. Wählen Sie eine Datei aus und klicken Sie auf **Open**. 

Die Visualisierung wird der Liste der Visualisierungen hinzugefügt. 


## Visualisierung gemeinsam nutzen
{:#logging_kibana_visualizations_share}

Führen Sie die folgenden Schritte aus, um eine Visualisierung auf der Seite 'Visualize' zur gemeinsamen Nutzung verfügbar zu machen:

1. Klicken Sie in der Symbolleiste der Seite 'Visualize' auf die Schaltfläche **Share Visualization** ![Visualisierung gemeinsam nutzen](images/k4_visualization_share_icon.jpg "Visualisierung gemeinsam nutzen"). 

2. Wählen Sie eine der folgenden Aktionen aus: 

    * **Embed this visualization:** Wählen Sie diese Option aus, um die Visualisierung in Ihrem HTML-Quelltext zur gemeinsamen Nutzung verfügbar zu machen.  
    
        Klicken Sie auf die Kopierschaltfläche ![In Zwischenablage kopieren](images/k4_copy_to_clipboard.jpg "In Zwischenablage kopieren"), um den HTML-Code zu kopieren, mit dem Sie die Visualisierung in Ihren HTML-Quelltext einbetten können. 
	
	**Hinweis:** Zum Anzeigen der Visualisierung müssen Benutzer Zugriff auf Kibana haben. 
	
    * **Share a link:** Wählen Sie diese Option aus, um die Visualisierung zur gemeinsamen Nutzung mit anderen Benutzern in Kibana verfügbar zu machen.



