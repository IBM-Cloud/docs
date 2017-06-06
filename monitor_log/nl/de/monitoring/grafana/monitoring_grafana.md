---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Grafana-Dashboard erstellen
{:#monitoring_grafana}

Sie können ein angepasstes Grafana-Dashboard erstellen, um Metriken für alle Container anzuzeigen, die in einem Bereich Ihrer {{site.data.keyword.Bluemix}}-Organisation ausgeführt werden.
{:shortdesc}

Führen Sie zum Erstellen eines Grafana-Dashboards die folgenden Schritte aus:

1. Starten Sie Grafana in einem Web-Browser. Weitere Informationen finden Sie unter [Zum Grafana-Dashboard über einen Web-Browser navigieren](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser).

2. Speichern Sie das Standarddashboard.

    1. Klicken Sie in der Symbolleiste auf das Symbol zum Speichern (Save).
    2. Geben Sie einen Namen für das Dashboard ein.
    3. Klicken Sie neben dem Namensfeld auf das Symbol zum Speichern (Save).
   
3. Inaktivieren Sie die automatische Seitenaktualisierung, während Sie an Ihrem Dashboard arbeiten. 

    1. Klicken Sie auf das Zeitauswahlfeld im Kopfbereich.
    2. Wählen Sie die Option **Auto-refresh** (Automatisches Aktualisieren) aus.
    3. Klicken Sie auf **Off** (Aus).
 
 5. Löschen Sie die Beispielzeilen.
 
     1. Setzen neben der Überschrift *Welcome to Grafana* Ihren Cursor auf die Aufwahlleiste für das Menü 'Row' und klicken Sie auf das Symbol des Menüs 'Row', das eingeblendet wird.
     2. Klicken Sie auf **Delete row** (Zeile löschen) und anschließend auf **Yes**.
     
     Wiederholen Sie diese Schritte, um die Dokumentationslinks und die Zeile des ersten Diagramms ('First Graph') zu entfernen. 
     
     Passen Sie das Zeitauswahlfeld im Seitenkopf an, um sicherzustellen, dass die Daten angezeigt werden. Der Standardwert gibt eine Zeit zwischen einem Zeitpunkt 6 Stunden zuvor und einem Zeitpunkt einige Sekunden zuvor an. Wählen Sie **Last 30d** aus.
     
6. Fügen Sie eine Visualisierung hinzu.

    * Informationen zum Hinzufügen einer Visualisierung für CPU-Inaktivität finden Sie unter [Visualisierung für CPU-Inaktivität hinzufügen](monitoring_grafana.html#grafana_add_cpu).
    * Informationen zum Hinzufügen einer Visualisierung für belegten Hauptspeicher finden Sie unter [Visualisierung für belegten Hauptspeicher hinzufügen](monitoring_grafana.html#grafana_add_mem).
        
7. Speichern Sie das angepasste Dashboard.

    1. Klicken Sie in der Symbolleiste auf das Symbol zum Speichern (Save).
    2. Geben Sie einen Namen für das Dashboard ein.
    3. Klicken Sie neben dem Namensfeld auf das Symbol zum Speichern (Save).
    

## Visualisierung für CPU-Inaktivität hinzufügen
{:#grafana_add_cpu}

Führen Sie die folgenden Schritte aus, um ein Diagramm zur CPU-Inaktivität hinzuzufügen, das Daten aus allen Containern in Ihrem Bereich enthält:

1. Klicken Sie auf die Schaltfläche **Add a row** (Zeile hinzufügen). Eine Auswahlleiste für das Menü 'Row' wird neben der Zeile angezeigt.
    
2. Setzen Sie Ihren Cursor auf die Auswahlleiste des Row-Menüs und klicken Sie auf das Symbol des Row-Menüs, das eingeblendet wird.

3. Klicken Sie auf **Add Panel** (Anzeige hinzufügen). Klicken Sie auf **Graph**.

4. Klicken Sie auf den Diagrammtitel, um das Anzeigemenü zu öffnen, und klicken Sie auf **Edit** (Bearbeiten). 

    Das übrige Dashboard wird verdeckt, nur der Editor für dieses Diagramm und eine Vorschau des Diagramms werden angezeigt.
    
5. Erstellen Sie auf der Registerkarte 'Metrics' eine Abfrage, um die Daten für das Diagramm zu erfassen. 

    Wenn Sie zum Beispiel mit Containern arbeiten, beinhaltet das Abfrageformat die Bereichs-ID, eine Containergruppen-ID und eine einzelne Containerinstanz-ID im folgenden Format: `Bereichs-ID.Gruppen-ID.Instanz-ID.metric`
        
    1. Klicken Sie in der Zeile A auf **Select metric**. Wählen Sie dann Ihre Bereichs-ID (space_ID) aus.
    2. Klicken Sie auf **Select metric** und wählen Sie den Stern (\*) aus.
    
    Wenn Sie den Stern (\*) auswählen, umfassen die Daten Metriken aus jeder Containergruppe im Bereich. Optional können Sie dieses Format durch einen regulären Ausdruck modifizieren, um nur Metriken aus bestimmten Containern einzuschließen. Beispiel: Wenn Sie nur die Metriken aus einzelnen Containern anzeigen und Containergruppen ausschließen wollen, klicken Sie auf **Select metric** und wählen **0000** aus.
        
    3. Klicken Sie erneut auf **Select metric** und wählen Sie wieder den Stern (\*) aus. Dieses Format schließt Metriken aus jedem einzelnen Container im Bereich ein.
        
    4. Klicken Sie auf **Select metric** und **cpu-0**.
        
    5. Klicken Sie auf **Select metric** und **cpu-idle**. Die Diagrammvorschau wird mit der Anzeige der Metriken aktualisiert, die dieser Abfrage entsprechen.
    
6. Optional: Passen Sie die Anzeige des Diagramms an.
    
    * Zur Benennung des Diagramms klicken Sie auf die Registerkarte 'General' und geben im Feld 'Title' einen Namen für das Diagramm ein. Beispiel: CPU Idle.
    * Zur Benennung der vertikalen Achse klicken Sie auf die Registerkarte 'Axes' (für Achsen und das Raster) und geben im Achsenabschnitt 'Left Y' im Feld 'Label' die Bezeichnung 'CPU' ein.
    * Zur Änderung der Hintergrundfarbe des Diagramms klicken Sie im Abschnitt 'Grid Thresholds' für Level 2 auf das Symbol der Auswahlfunktion für die Hintergrundfarbe und ändern die Hintergrundfarbe in Weiß oder Hellgrau.
    
    Klicken Sie im Seitenkopf auf **Back to dashboard**.
    
7. Zum Speichern der Änderungen, die Sie an diesem Dashboard vorgenommen haben, klicken Sie im Seitenkopf auf das Symbol zum Speichern (Save) und dann auf das Symbol zum Speichern im Menü.


## Visualisierung für belegten Hauptspeicher hinzufügen
{:#grafana_add_mem}

Führen Sie die folgenden Schritte aus, um eine Visualisierung zum belegten Speicher hinzuzufügen:

1. Klicken Sie auf die Schaltfläche 'Add row'. Eine Auswahlleiste für das Row-Menü wird neben der Zeile angezeigt.
   
2. Setzen Sie Ihren Cursor auf die Auswahlleiste des Row-Menüs und klicken Sie auf das Symbol des Row-Menüs, das eingeblendet wird.

    1. Klicken Sie auf 'Add Panel > Graph'.
    2. Klicken Sie auf 'Edit'. Das übrige Dashboard wird verdeckt, nur der Editor für dieses Diagramm und eine Vorschau des Diagramms werden angezeigt.
    
3. Erstellen Sie auf der Registerkarte 'Metrics' eine Abfrage, um die Daten für das Diagramm zu erfassen. 

    Wenn Sie zum Beispiel mit Containern arbeiten, beinhaltet das Abfrageformat die Bereichs-ID, eine Containergruppen-ID und eine einzelne Containerinstanz-ID im folgenden Format: 'Bereichs-ID.Gruppen-ID.Instanz-ID.metric'.
        
    1. Klicken Sie in der Zeile A auf **Select metric**. Wählen Sie dann Ihre Bereichs-ID (space_ID) aus.
    2. Klicken Sie auf **Select metric** und wählen Sie den Stern (\*) aus.
    
    Wenn Sie den Stern (\*) auswählen, umfassen die Daten Metriken aus jeder Containergruppe im Bereich. Optional können Sie dieses Format durch einen regulären Ausdruck modifizieren, um nur Metriken aus bestimmten Containern einzuschließen. Beispiel: Wenn Sie nur die Metriken aus einzelnen Containern anzeigen und Containergruppen ausschließen wollen, klicken Sie auf **Select metric** und wählen **0000** aus.
    
    3. Klicken Sie erneut auf **Select metric** und wählen Sie wieder den Stern (\*) aus. Dieses Format schließt Metriken aus jedem einzelnen Container im Bereich ein.
        
    4. Klicken Sie auf **Select metric** und **memory**.
        
    5. Klicken Sie auf **Select metric** und **memory-used**. Die Diagrammvorschau wird mit der Anzeige der Metriken aktualisiert, die dieser Abfrage entsprechen.
    
6. Optional: Passen Sie die Anzeige des Diagramms an.
    
    * Zur Benennung des Diagramms klicken Sie auf die Registerkarte 'General' und geben im Feld 'Title' einen Namen für das Diagramm ein. Beispiel: Memory Used.
    *  Zur Änderung des Formats für die Werte der vertikalen Achse klicken Sie auf die Registerkarte 'Axes' (für Achsen und das Raster) und wählen 'bytes' für das Format im Achsenabschnitt 'Left Y' aus.
    * Geben Sie in das Feld 'Label' die Bezeichnung 'Memory' für die vertikale Achse ein.
    * Zur Änderung der Hintergrundfarbe des Diagramms klicken Sie im Abschnitt 'Grid Thresholds' für Level 2 auf das Symbol der Auswahlfunktion für die Hintergrundfarbe und ändern die Hintergrundfarbe in Weiß oder Hellgrau.
    
    Klicken Sie im Seitenkopf auf **Back to dashboard**.

7. Zum Speichern der Änderungen, die Sie an diesem Dashboard vorgenommen haben, klicken Sie im Seitenkopf auf das Symbol zum Speichern (Save) und dann auf das Symbol zum Speichern im Menü.

