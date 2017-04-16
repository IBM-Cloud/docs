
{:new_window: target="_blank"}


# {{site.data.keyword.blockstorageshort}}-Datenträger an virtuelle Server anhängen
{: #attaching-block-storage-volume}

Letzte Aktualisierung: 13. September 2016
{: .last-updated}

Datenträger werden für virtuelle Server als Geräte mit einem bestimmten Gerätenamen angehängt und abgehängt. Damit ein virtueller Server Daten auf einem Datenträger persistent speichern kann, müssen Sie den Datenträger an den virtuellen Server anhängen.

Führen Sie zum Anhängen eines Datenträgers die folgenden Schritte aus:

1.  Wählen Sie in der Bluemix-Benutzerschnittstelle die Optionen **Konsole > Speicher** aus.
2.  Wählen Sie die Block Storage-Instanz aus, die Sie bereits bereitgestellt haben.
3.	Wählen Sie einen Datenträger aus der Liste der verfügbaren Datenträger aus.
4.	Klicken Sie auf **Anhängen**.
5.	Wählen Sie im Dialogfeld 'Anhängen' eine Instanz eines virtuellen Servers aus der Dropdown-Liste aus.
6.	Geben Sie optional das Gerät an, an das dieser Datenträger angehängt werden soll. 
    
    **Anmerkung**: Wenn Sie das Gerät nicht angegeben, wählt das System automatisch das erste verfügbare Gerät auf dem virtuellen Server aus.

7.	Klicken Sie auf **Anhängen**, um die Informationen zu übergeben und das Dialogfeld zu schließen.

Der Datenträger wird in der Tabelle der angehängten Datenträger mit den Informationen zu der Instanz des virtuellen Servers aufgeführt.
Der virtuelle Server kann nun das Gerät verwenden, um Daten persistent zu speichern. 

Nächste Schritte

Wenn der Datenträger erstellt und an einen virtuellen Server angehängt wurde, finden Sie Informationen zu seiner Verwendung unter [Datenträger vorbereiten](../BlockStorage/blockstorage_preparingvolume.html).
