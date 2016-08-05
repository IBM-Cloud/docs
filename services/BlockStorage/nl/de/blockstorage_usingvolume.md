{:new_window: target="_blank"} 

# {{site.data.keyword.blockstorageshort}}-Datenträger verwenden {: #using-block-storage-volume} 

*Letzte Aktualisierung: 20. Juni 2016*
{: .last-updated}

## Datenträger erstellen {: #creating-volume} 

1.	Klicken Sie auf **Erstellen**, um das Dialogfeld **Datenträger erstellen** zu öffnen.
2.	Geben Sie die gewünschte Größe des Datenträgers an. Dezimalzahlen sind nicht zulässig. Die Größe wird durch das Kontingent begrenzt, das Ihrer Organisation zugewiesen ist.
3.	Geben Sie einen Namen an. Der Name ist nur zu Anzeigezwecken gedacht.
4.	Optional können Sie eine detailliertere Beschreibung des Datenträgers angeben. 
5.	Klicken Sie auf **Erstellen**, und die Informationen zu übergeben und das Dialogfeld zu schließen. 

Das Erstellen eines Datenträgers kann einen Moment dauern. 

## Datenträger löschen {: #deleting-volume}

1.	Wählen Sie den Datenträger aus, der gelöscht werden soll.
2.	Klicken Sie auf **Löschen**.
3.	Bestätigen Sie den Löschvorgang für diesen Datenträger.

Sie können keinen Datenträger löschen, der an einen virtuellen Server angehängt ist. Sie müssen den Datenträger zuerst abhängen.

## Datenträger erweitern {: #extending-volume}
Mit der Aktion **Erweitern** können Sie den Wert für die Originalgröße des Datenträgers bis zu zehnmal erhöhen. Die Größe eines Datenträgers kann jedoch nicht reduziert werden.

1.	Wählen Sie den Datenträger aus, der erweitert werden soll.
2.	Klicken Sie auf **Erweitern**.
3.	Wählen Sie die neue Größe des Datenträgers aus. Geben Sie die neue Gesamtgröße des Datenträgers an.
4.	Klicken Sie auf **Erweitern**, und die Informationen zu übergeben und das Dialogfeld zu schließen. 

Um erweitert werden zu können, muss ein Datenträger den Status **Verfügbar** aufweisen. 

## Datenträger an virtuellen Server anhängen und wieder abhängen {: #attaching-detaching-volume}
Datenträger werden für virtuelle Server als Geräte mit einem bestimmten Gerätenamen angehängt und abgehängt. Damit ein virtueller Server Daten auf einem Datenträger als persistent definieren kann, müssen Sie den Datenträger an den virtuellen Server anhängen.

Führen Sie zum Anhängen eines Datenträgers die folgenden Schritte aus: 

1.	Wählen Sie einen Datenträger aus der Liste der verfügbaren Datenträger aus.
2.	Klicken Sie auf **Anhängen**.
3.	Wählen Sie im Dialogfeld 'Anhängen' eine Instanz eines virtuellen Servers aus der Dropdown-Liste aus. 
4.	Geben Sie optional das Gerät an, an das dieser Datenträger angehängt werden soll. Wenn Sie das Gerät nicht angegeben, wählt das System automatisch das erste verfügbare Gerät auf dem virtuellen Server aus.
5.	Klicken Sie auf **Anhängen**, und die Informationen zu übergeben und das Dialogfeld zu schließen.

Der Datenträger wird in der Tabelle der angehängten Datenträger mit den Informationen zu der Instanz des virtuellen Servers aufgeführt.
Der virtuelle Server kann nun das Gerät verwenden, um Daten als persistent zu definieren. 

Führen Sie zum Abhängen eines Datenträgers die folgenden Schritte aus: 

1.	Wählen Sie einen Datenträger aus der Liste der angehängten Datenträger aus. 
2.	Klicken Sie auf **Abhängen**.
3.	Bestätigen Sie das Abhängen im Dialogfeld. 

Nachdem der Datenträger abgehängt wurde, steht er nicht länger für E/A-Operationen in der Instanz des virtuellen Servers zur Verfügung. In der Benutzerschnittstelle des {{site.data.keyword.blockstorageshort}}-Service kann der Datenträger nun an andere virtuelle Server angehängt werden.
