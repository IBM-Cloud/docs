{:new_window: target="_blank"} 


# {{site.data.keyword.blockstorageshort}}-Momentaufnahme verwenden {: #using-block-storage-snapshot} 
Letzte Aktualisierung: 07. September 2016
{: .last-updated}

Führen Sie für die Verwendung von Momentaufnahmen die folgenden Schritte aus:

## Momentaufnahme erstellen {: #creating-snapshot} 

1.  Wählen Sie in der Bluemix-Benutzerschnittstelle die Optionen **Konsole > Speicher** aus.
2.  Wählen Sie die Block Storage-Instanz aus, die Sie bereits bereitgestellt haben.
3.	Klicken Sie auf die Registerkarte 'Verwalten'.
4.	Klicken Sie auf der Seite 'Verwalten' auf die Registerkarte **Datenträger**, um eine Liste der Datenträger abzurufen.
5.	Wählen Sie in der Spalte mit den nicht angehängten Datenträgern den Datenträger aus, von dem Sie eine Momentaufnahme erstellen möchten. Stellen Sie sicher, dass der von Ihnen ausgewählte Datenträger nicht angehängt ist. Der ausgewählte Datenträger wird hervorgehoben. 
6.	Klicken Sie im Dropdown-Menü 'Aktionen' auf **Momentaufnahme erstellen**.
7.	Geben Sie der Momentaufnahme einen Namen und klicken Sie auf **Erstellen**.

**Anmerkung:** 

* Wenn Momentaufnahmen für einen Datenträger vorhanden sind, kann dieser Datenträger nicht gelöscht werden. 
* Die Größe der Momentaufnahme wird automatisch auf die Größe der Momentaufnahme des ursprünglichen Datenträgers gesetzt.

## Datenträger aus einer Momentaufnahme erstellen {: #creating-volume-from-snapshot}

1.  Wählen Sie in der Bluemix-Benutzerschnittstelle die Optionen **Konsole > Speicher** aus.
2.  Wählen Sie die Block Storage-Instanz aus, die Sie bereits bereitgestellt haben.
3.	Klicken Sie auf die Registerkarte 'Verwalten'.
4.	Klicken Sie auf der Seite 'Verwalten' auf die Registerkarte **Momentaufnahme**, um eine Liste der Momentaufnahmen abzurufen.
5.	Wählen Sie die Momentaufnahme aus, von der Sie einen Datenträger erstellen möchten. Die ausgewählte Momentaufnahme wird hervorgehoben.
6.	Klicken Sie im Dropdown-Menü 'Aktionen' auf **Datenträger erstellen**.
7.	Geben Sie dem neuen Datenträger einen Namen und optional eine neue Größe und klicken Sie auf **Erstellen**. 

**Hinweis:** Die neue Größe des Datenträgers muss gleich der oder größer als die Momentaufnahmengröße sein. 

## Momentaufnahme löschen {: #deleting-snapshot}

1.  Wählen Sie in der Bluemix-Benutzerschnittstelle die Optionen **Konsole > Speicher** aus.
2.  Wählen Sie die Block Storage-Instanz aus, die Sie bereits bereitgestellt haben.
3.	Klicken Sie auf die Registerkarte 'Verwalten'.
4.	Klicken Sie auf der Seite 'Verwalten' auf die Registerkarte **Momentaufnahme**, um eine Liste der Momentaufnahmen abzurufen.
5.	Wählen Sie die Momentaufnahme aus, die gelöscht werden soll. Die ausgewählte Momentaufnahme wird hervorgehoben.
6.	Klicken Sie im Dropdown-Menü 'Aktionen' auf **Löschen**. 



