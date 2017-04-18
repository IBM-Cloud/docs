{:new_window: target="_blank"} 

# {{site.data.keyword.blockstorageshort}}-Datenträger verwenden 
{: #using-block-storage-volume} 
Letzte Aktualisierung: 07. September 2016
{: .last-updated}

Führen Sie für die Verwendung von Datenträgern die folgenden Schritte aus:

## Datenträger löschen {: #deleting-volume}

1.  Wählen Sie in der Bluemix-Benutzerschnittstelle die Optionen **Konsole > Speicher** aus.
2.  Wählen Sie die Block Storage-Instanz aus, die Sie bereits bereitgestellt haben.
3.	Wählen Sie den Datenträger aus, der gelöscht werden soll.
4.	Klicken Sie im Dropdown-Menü 'Aktionen' auf **Löschen**.
5.	Bestätigen Sie den Löschvorgang für diesen Datenträger.

Sie können keinen Datenträger löschen, der an einen virtuellen Server angehängt ist. Sie müssen den Datenträger zuerst abhängen. Durch das Löschen des Datenträgers kann in Zukunft nicht mehr darauf zugegriffen werden und die darin enthaltenen Daten sind nicht mehr vorhanden. Außerdem können Sie keine Datenträger mit zugeordneten Momentaufnahmen löschen.

## Datenträger erweitern {: #extending-volume}
Mit der Aktion **Erweitern** können Sie den Wert für die Originalgröße des Datenträgers bis zu zehnmal erhöhen. Die Größe eines Datenträgers kann jedoch nicht reduziert werden.

1.  Wählen Sie in der Bluemix-Benutzerschnittstelle die Optionen **Konsole > Speicher** aus.
2.  Wählen Sie die Block Storage-Instanz aus, die Sie bereits bereitgestellt haben.
3.	Wählen Sie den Datenträger aus, der erweitert werden soll.
4.	Klicken Sie im Dropdown-Menü 'Aktionen' auf **Erweitern**.
5.	Wählen Sie die neue Größe des Datenträgers aus. Geben Sie die neue Gesamtgröße des Datenträgers an.
6.	Klicken Sie auf **Erweitern**, um die Informationen zu übergeben und das Dialogfeld zu schließen. 

Um erweitert werden zu können, muss ein Datenträger den Status **Verfügbar** aufweisen. Nach der Erweiterung des Datenträgers müssen Sie das Dateisystem (z. B. ext4) darüber informieren, dass die Platte durch Ändern der Größe des Dateisystems in eine neue Größe erweitert wurde. 

## Datenträger an virtuellen Server anhängen und wieder abhängen {: #attaching-detaching-volume}
Datenträger werden für virtuelle Server als Geräte mit einem bestimmten Gerätenamen angehängt und abgehängt. Damit ein virtueller Server Daten auf einem Datenträger persistent speichern kann, müssen Sie den Datenträger an den virtuellen Server anhängen.

Führen Sie zum Anhängen eines Datenträgers die folgenden Schritte aus: 

1.  Wählen Sie in der Bluemix-Benutzerschnittstelle die Optionen **Konsole > Speicher** aus.
2.  Wählen Sie die Block Storage-Instanz aus, die Sie bereits bereitgestellt haben.
3.	Wählen Sie einen Datenträger aus der Liste der verfügbaren Datenträger aus.
4.	Klicken Sie im Dropdown-Menü 'Aktionen' auf **Anhängen**.
5.	Wählen Sie im Dialogfeld 'Anhängen' eine Instanz eines virtuellen Servers aus der Dropdown-Liste aus. 
6.	Geben Sie optional das Gerät an, an das dieser Datenträger angehängt werden soll. Wenn Sie das Gerät nicht angegeben, wählt das System automatisch das erste verfügbare Gerät auf dem virtuellen Server aus.
7.	Klicken Sie auf **Anhängen**, um die Informationen zu übergeben und das Dialogfeld zu schließen.

Der Datenträger wird in der Tabelle der angehängten Datenträger mit den Informationen zu der Instanz des virtuellen Servers aufgeführt. 
Der virtuelle Server kann nun das Gerät verwenden, um Daten persistent zu speichern. 

Wenn Sie bereit sind, einen Datenträger abzuhängen, müssen Sie den virtuellen Server für den Abhängevorgang vorbereiten. Stoppen Sie beispielsweise sämtliche Anwendungen, die das Dateisystem nutzen. Hängen Sie außerdem das Gerät von der Instanz des virtuellen Servers ab.

Führen Sie zum Abhängen eines Datenträgers die folgenden Schritte aus: 

1.  Wählen Sie in der Bluemix-Benutzerschnittstelle die Optionen **Konsole > Speicher** aus.
2.  Wählen Sie die Block Storage-Instanz aus, die Sie bereits bereitgestellt haben.
3.	Wählen Sie einen Datenträger aus der Liste der angehängten Datenträger aus. 
4.	Klicken Sie im Dropdown-Menü 'Aktionen' auf **Abhängen**.
5.	Bestätigen Sie das Abhängen im Dialogfeld. 

Nachdem der Datenträger abgehängt wurde, steht er nicht länger für E/A-Operationen in der Instanz des virtuellen Servers zur Verfügung. In der Benutzerschnittstelle des {{site.data.keyword.blockstorageshort}}-Service kann der Datenträger nun an andere virtuelle Server angehängt werden.
