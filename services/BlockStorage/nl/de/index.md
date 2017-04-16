{:new_window: target="_blank"} 

# Einführung in {{site.data.keyword.blockstorageshort}} (BETA)

{{site.data.keyword.blockstoragefull}} bietet Speicherzugriff auf Blockebene für transaktionsintensive Arbeitslasten und Laufzeiten mit permanentem Speicherbedarf.

Sie können IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} zum Erstellen von {{site.data.keyword.blockstorageshort}}-Datenträgern verwenden, die an virtuelle Maschinen angehängt werden können. Die Daten in Block Storage-Datenträgern bleiben über den Lebenszyklus der virtuellen Maschinen hinaus bestehen. IBM {{site.data.keyword.blockstorageshort}} verwendet OpenStack Cinder zum Verwalten des Datenträgerzyklus.

{{site.data.keyword.blockstorageshort}}-Datenträger werden über eine IBM {{site.data.keyword.blockstorageshort}}-Serviceinstanz erstellt. Sie können die Datenträger an eine virtuelle Maschine unter einer bestimmten, von Ihnen bereitgestellten Einheit anhängen oder das System kann automatisch einen verfügbaren Einheitennamen auswählen. Die virtuelle Maschine führt seine E/A-Operationen direkt mit der angegebenen Einheit unabhängig vom {{site.data.keyword.blockstorageshort}}-Service aus.

Sie können auch Momentaufnahmen von Datenträgern auf Blockebene erstellen. Mit dem {{site.data.keyword.blockstorageshort}}-Service können keine Momentaufnahmen erstellt werden, während der Datenträger angehängt ist. Die resultierenden Momentaufnahmen sind so gegen Ausfälle beständig. 

## Vorgehensweise zum Erstellen einer {{site.data.keyword.blockstorageshort}}-Serviceinstanz
Führen Sie die folgenden Schritte durch, um eine Instanz des {{site.data.keyword.blockstorageshort}}-Service in Ihrem Bereich zu erstellen:
 
1.	Rufen Sie die Registerkarte {{site.data.keyword.Bluemix_notm}}-**Katalog** auf und geben Sie **{{site.data.keyword.blockstorageshort}}** in das Suchfeld ein oder wechseln Sie zu **Services** und wählen Sie **Speicher** aus. Klicken Sie auf den **{{site.data.keyword.blockstorageshort}}**-Service. 
2.	Geben Sie einen Bereich und einen Servicenamen ein. Wählen Sie den Plan aus und klicken Sie auf **Erstellen**.
 	
Der {{site.data.keyword.blockstorageshort}}-Service wird nur in einem nicht gebundenen Kontext unterstützt. 

Eine Instanz des {{site.data.keyword.blockstorageshort}}-Service wird in Ihrem Bereich erstellt. Sie können die {{site.data.keyword.blockstorageshort}}-Benutzerschnittstelle jederzeit zum Bearbeiten von Datenträgern öffnen, indem Sie auf das Symbol der Serviceinstanz klicken.

## {{site.data.keyword.blockstorageshort}}-Benutzerschnittstelle (UI)
Die grafische Benutzerschnittstelle von {{site.data.keyword.blockstorageshort}} stellt oben im Fenster eine allgemeine Übersicht zu Ihren Speicherdatenträgern, Momentaufnahmen und zur Gesamtspeicherbelegung für Datenträger und Momentaufnahmen bereit. 

Die Kopfzeile enthält das Datum und die Uhrzeit der letzten Aktualisierung der Benutzerschnittstelle. Bei Bedarf können Sie das Aktualisierungssymbol (ein kreisförmiges Pfeilsymbol) für eine manuelle Aktualisierung verwenden. 

Über die Suchleiste können Sie basierend auf dem von Ihnen eingegebenen Suchbegriff nach Datenträgern suchen. Die Tabellen werden während der Eingabe so gefiltert, dass nur die Datenträger angezeigt werden, die dem eingegebenen Suchbegriff entsprechen.

Unter der Übersicht befinden sich zwei Registerkarten für Datenträger und Momentaufnahmen. Die Registerkarte mit den Datenträgern ist standardmäßig ausgewählt. In den Tabellen auf dieser Registerkarte sind detaillierte Informationen zu den verfügbaren und angehängten Datenträgern aufgeführt. Jede Zeile in einer Tabelle zeigt die wichtigsten Eigenschaften eines Datenträgers an. Wenn Sie eine Zeile erweitern, werden weitere Eigenschaften angezeigt. Angehängte Datenträger zeigen auch die Instanz einer virtuellen Maschine und die Einheit, an die der Datenträger angehängt ist. 

Die Registerkarte mit den Momentaufnahmen zeigt eine Tabelle mit Momentaufnahmen mit ähnlichen Eigenschaften und Verhaltensweisen. 

Verwenden Sie das Symbol 'Erstellen' über den Tabellen, um einen neuen Datenträger zu erstellen oder vorhandene Datenträger zu bearbeiten. Wenn Sie auf der Grundlage eines Snapshots einen Datenträger erstellen, können Sie auch die Dropdown-Liste 'Aktionen' verwenden.


## Aktionen für Datenträger

### Datenträger erstellen

1.	Klicken Sie auf **Erstellen**, um das Dialogfeld **Datenträger erstellen** zu öffnen.
2.	Geben Sie die gewünschte Größe des Datenträgers an. Dezimalzahlen sind nicht zulässig. Die Größe wird durch das Kontingent begrenzt, das Ihrer Organisation zugewiesen ist.
3.	Geben Sie einen Namen an. Der Name ist nur zu Anzeigezwecken gedacht.
4.	Optional können Sie eine detailliertere Beschreibung des Datenträgers angeben. 
5.	Klicken Sie auf **Erstellen**, und die Informationen zu übergeben und das Dialogfeld zu schließen. 

Das Erstellen eines Datenträgers kann einen Moment dauern. 

### Datenträger löschen

1.	Wählen Sie den Datenträger aus, der gelöscht werden soll.
2.	Klicken Sie auf **Löschen**.
3.	Bestätigen Sie den Löschvorgang für diesen Datenträger.

Sie können keinen Datenträger löschen, der an eine virtuelle Maschine angehängt ist. Sie müssen den Datenträger zuerst abhängen.

### Datenträger erweitern
Mit der Aktion **Erweitern** können Sie die Größe des Datenträgers erhöhen. Die Größe eines Datenträgers kann jedoch nicht reduziert werden.

1.	Wählen Sie den Datenträger aus, der erweitert werden soll.
2.	Klicken Sie auf **Erweitern**.
3.	Wählen Sie die neue Größe des Datenträgers aus. Geben Sie die neue Gesamtgröße des Datenträgers an.
4.	Klicken Sie auf **Erweitern**, und die Informationen zu übergeben und das Dialogfeld zu schließen. 

Um erweitert werden zu können, muss ein Datenträger den Status **Verfügbar** aufweisen. 

### Datenträger für eine virtuelle Maschine anhängen und abhängen
Datenträger werden für virtuelle Maschinen als Einheiten mit einem bestimmten Einheitennamen angehängt und abgehängt. Damit eine virtuelle Maschine Daten auf einem Datenträger als persistent definieren kann, müssen Sie den Datenträger an die virtuelle Maschine anhängen.

Führen Sie zum Anhängen eines Datenträgers die folgenden Schritte aus: 

1.	Wählen Sie einen Datenträger aus der Liste der verfügbaren Datenträger aus.
2.	Klicken Sie auf **Anhängen**.
3.	Wählen Sie im Dialogfeld 'Anhängen' eine Instanz einer virtuellen Maschine aus der Dropdown-Liste aus. 
4.	Geben Sie optional die Einheit an, an die dieser Datenträger angehängt werden soll. Wenn Sie die Einheit nicht angegeben, wählt das System automatisch die erste verfügbare Einheit auf der virtuellen Maschine aus.
5.	Klicken Sie auf **Anhängen**, und die Informationen zu übergeben und das Dialogfeld zu schließen.

Der Datenträger wird in der Tabelle der angehängten Datenträger mit den Informationen zu der Instanz der virtuellen Maschine aufgeführt. 
Die virtuelle Maschine kann nun die Einheit verwenden, um Daten als persistent zu definieren. 

Führen Sie zum Abhängen eines Datenträgers die folgenden Schritte aus: 

1.	Wählen Sie einen Datenträger aus der Liste der angehängten Datenträger aus. 
2.	Klicken Sie auf **Abhängen**.
3.	Bestätigen Sie das Abhängen im Dialogfeld. 

Nachdem der Datenträger abgehängt wurde, steht er nicht länger für E/A-Operationen in der Instanz der virtuellen Maschine zur Verfügung. In der Benutzerschnittstelle des {{site.data.keyword.blockstorageshort}}-Service kann der Datenträger nun an andere virtuelle Maschinen angehängt werden.

## Aktionen für Momentaufnahmen

### Momentaufnahme erstellen

1.	Wählen Sie die Registerkarte **Datenträger** aus, um eine Liste der Datenträger abzurufen.
2.	Wählen Sie in der Spalte mit den nicht angehängten Datenträgern den Datenträger aus, von dem Sie eine Momentaufnahme erstellen möchten. Stellen Sie sicher, dass der von Ihnen ausgewählte Datenträger nicht angehängt ist. Der ausgewählte Datenträger wird hervorgehoben. 
3.	Klicken Sie auf **Aktionen** und wählen Sie die Option zum Erstellen einer Momentaufnahme aus der Dropdown-Liste aus.
4.	Geben Sie der Momentaufnahme einen Namen und klicken Sie auf **Erstellen**.

**Hinweis:** Wenn Momentaufnahmen für einen Datenträger vorhanden sind, kann dieser Datenträger nicht gelöscht werden. 

### Datenträger von einer Momentaufnahme erstellen

1.	Wählen Sie die Registerkarte mit den Momentaufnahmen aus, um eine Liste der Momentaufnahmen abzurufen.
2.	Wählen Sie die Momentaufnahme aus, von der Sie einen Datenträger erstellen möchten. Die ausgewählte Momentaufnahme wird hervorgehoben.
3.	Klicken Sie auf **Aktionen** und wählen Sie die Option zum Erstellen eines Datenträgers aus der Dropdown-Liste aus.
4.	Geben Sie dem neuen Datenträger einen Namen und optional eine neue Größe und klicken Sie auf **Erstellen**. 

**Hinweis:** Die neue Größe des Datenträgers muss gleich der oder größer als die Momentaufnahmengröße sein. 

### Momentaufnahme löschen

1.	Wählen Sie die Registerkarte mit den Momentaufnahmen aus, um eine Liste der Momentaufnahmen abzurufen.
2.	Wählen Sie die Momentaufnahme aus, die gelöscht werden soll. Die ausgewählte Momentaufnahme wird hervorgehoben.
3.	Klicken Sie auf **Aktionen** und wählen Sie **Löschen** aus. 



># Zugehörige Links {:class="linklist"}
>## API-Referenz {:id="api"}
>* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}
>
>{:elementKind="article" id="rellinks"}
