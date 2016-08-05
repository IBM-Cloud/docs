{:new_window: target="_blank"} 

# Einführung in {{site.data.keyword.blockstorageshort}} (Beta)

*Letzte Aktualisierung: 15. Juli 2016*
{: .last-updated}

{{site.data.keyword.blockstoragefull}} bietet Speicherzugriff auf Blockebene für transaktionsintensive Arbeitslasten und Laufzeiten mit permanentem Speicherbedarf.

Sie können IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} zum Erstellen von {{site.data.keyword.blockstorageshort}}-Datenträgern verwenden, die an virtuelle Server angehängt werden können. Die Daten in Block Storage-Datenträgern bleiben über den Lebenszyklus der virtuellen Server hinaus bestehen. IBM {{site.data.keyword.blockstorageshort}} verwendet OpenStack Cinder zum Verwalten des Datenträgerzyklus.

{{site.data.keyword.blockstorageshort}}-Datenträger werden über eine IBM {{site.data.keyword.blockstorageshort}}-Serviceinstanz erstellt. Sie können die Datenträger an einen virtuellen Server unter einem bestimmten, von Ihnen bereitgestellten Gerät anhängen oder das System kann automatisch einen verfügbaren Gerätenamen auswählen. Der virtuelle Server führt seine E/A-Operationen direkt mit dem angegebenen Gerät unabhängig vom {{site.data.keyword.blockstorageshort}}-Service aus.

Sie können auch Momentaufnahmen von Datenträgern auf Blockebene erstellen. Mit dem {{site.data.keyword.blockstorageshort}}-Service können keine Momentaufnahmen erstellt werden, während der Datenträger angehängt ist. Die resultierenden Momentaufnahmen sind so gegen Ausfälle beständig. 


## Vorgehensweise zum Erstellen einer {{site.data.keyword.blockstorageshort}}-Serviceinstanz
Führen Sie die folgenden Schritte durch, um eine Instanz des {{site.data.keyword.blockstorageshort}}-Service in Ihrem Bereich zu erstellen:
 
1.	Rufen Sie die Registerkarte {{site.data.keyword.Bluemix_notm}}-**Katalog** auf und geben Sie **{{site.data.keyword.blockstorageshort}}** in das Suchfeld ein oder wechseln Sie zu **Services** und wählen Sie **Speicher** aus. Klicken Sie auf den **{{site.data.keyword.blockstorageshort}}**-Service. 
2.	Geben Sie einen Bereich und einen Servicenamen ein. Wählen Sie den Plan aus und klicken Sie auf **Erstellen**.
 	
Der {{site.data.keyword.blockstorageshort}}-Service wird nur in einem nicht gebundenen Kontext unterstützt. 

Eine Instanz des {{site.data.keyword.blockstorageshort}}-Service wird in Ihrem Bereich erstellt. Sie können die {{site.data.keyword.blockstorageshort}}-Benutzerschnittstelle jederzeit zum Bearbeiten von Datenträgern öffnen, indem Sie auf das Symbol der Serviceinstanz klicken.



## Die {{site.data.keyword.blockstorageshort}}-Benutzerschnittstelle verwenden{: #using-block-storage-ui}
Die grafische Benutzerschnittstelle von {{site.data.keyword.blockstorageshort}} stellt oben im Fenster eine allgemeine Übersicht zu Ihren Speicherdatenträgern, Momentaufnahmen und zur Gesamtspeicherbelegung für Datenträger und Momentaufnahmen bereit. 

Die Kopfzeile enthält das Datum und die Uhrzeit der letzten Aktualisierung der Benutzerschnittstelle. Bei Bedarf können Sie das Aktualisierungssymbol (ein kreisförmiges Pfeilsymbol) für eine manuelle Aktualisierung verwenden. 

Über die Suchleiste können Sie basierend auf dem von Ihnen eingegebenen Suchbegriff nach Datenträgern suchen. Die Tabellen werden während der Eingabe so gefiltert, dass nur die Datenträger angezeigt werden, die dem eingegebenen Suchbegriff entsprechen.

Unter der Übersicht befinden sich zwei Registerkarten für Datenträger und Momentaufnahmen. Die Registerkarte mit den Datenträgern ist standardmäßig ausgewählt. In den Tabellen auf dieser Registerkarte sind detaillierte Informationen zu den verfügbaren und angehängten Datenträgern aufgeführt. Jede Zeile in einer Tabelle zeigt die wichtigsten Eigenschaften eines Datenträgers an. Wenn Sie eine Zeile erweitern, werden weitere Eigenschaften angezeigt. Angehängte Datenträger zeigen auch die Instanz eines virtuellen Servers und das Gerät, an das der Datenträger angehängt ist. 

Die Registerkarte mit den Momentaufnahmen zeigt eine Tabelle mit Momentaufnahmen mit ähnlichen Eigenschaften und Verhaltensweisen. 

Verwenden Sie das Symbol 'Erstellen' über den Tabellen, um einen neuen Datenträger zu erstellen oder vorhandene Datenträger zu bearbeiten. Wenn Sie auf der Grundlage eines Snapshots einen Datenträger erstellen, können Sie auch die Dropdown-Liste 'Aktionen' verwenden.




## Datenträger an virtuellen Server anhängen{: #attaching-detaching-volume}
Datenträger werden für virtuelle Server als Geräte mit einem bestimmten Gerätenamen angehängt und abgehängt. Damit ein virtueller Server Daten auf einem Datenträger als persistent definieren kann, müssen Sie den Datenträger an den virtuellen Server anhängen.

Führen Sie zum Anhängen eines Datenträgers die folgenden Schritte aus: 

1.	Wählen Sie einen Datenträger aus der Liste der verfügbaren Datenträger aus.
2.	Klicken Sie auf **Anhängen**.
3.	Wählen Sie im Dialogfeld 'Anhängen' eine Instanz eines virtuellen Servers aus der Dropdown-Liste aus. 
4.	Geben Sie optional das Gerät an, an das dieser Datenträger angehängt werden soll. Wenn Sie das Gerät nicht angegeben, wählt das System automatisch das erste verfügbare Gerät auf dem virtuellen Server aus.
5.	Klicken Sie auf **Anhängen**, und die Informationen zu übergeben und das Dialogfeld zu schließen.

Der Datenträger wird in der Tabelle der angehängten Datenträger mit den Informationen zu der Instanz des virtuellen Servers aufgeführt.
Der virtuelle Server kann nun das Gerät verwenden, um Daten als persistent zu definieren. 


# Zugehörige Links
{: #rellinks}

## API-Referenz
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

