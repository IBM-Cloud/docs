{:new_window: target="_blank"} 

# Einführung in {{site.data.keyword.blockstorageshort}} (Beta)

Letzte Aktualisierung: 29. Juli 2016
{: .last-updated}

{{site.data.keyword.blockstoragefull}} stellt Zugriff auf Speicher auf Blockebene für transaktionsintensive Arbeitslasten und Laufzeiten bereit, die persistenten Speicher benötigen. Über den {{site.data.keyword.blockstorageshort}}-Service können Sie Lebenszyklen von Datenträgern verwalten, Datenträger an Ihre virtuelllen IBM Server anhängen und Momentaufnahmen Ihrer Blockspeicherdatenträger erstellen. 

Beachten Sie vor Beginn die folgenden Informationen. 

* Der {{site.data.keyword.blockstorageshort}}-Service wird nur in einem nicht gebundenen Kontext unterstützt.  
* Sie müssen virtuelle Server mit IBM {{site.data.keyword.virtualmachinesshort}} erstellt haben, um Blockspeicherdatenträger anhängen zu können. Weitere Informationen zur Verwendung von Blockspeicherdatenträgern mit IBM {{site.data.keyword.virtualmachinesshort}} finden Sie unter [Blockspeicherdatenträger und IBM Virtual Servers](../../virtualmachines/vm_create.html#storage_BS).  

Führen Sie die folgenden Schritte aus, um die Arbeit mit {{site.data.keyword.blockstorageshort}} zu beginnen: 

1. Erstellen Sie einen Datenträger. 
   
   a. Öffnen Sie den {{site.data.keyword.blockstorageshort}}-Service. 

   b. Klicken Sie auf **Erstellen**, um das Dialogfeld **Datenträger erstellen** aufzurufen. 

   c.	Geben Sie die gewünschte Größe des Datenträgers an. Dezimalzahlen sind nicht zulässig. Die Größe wird durch das Kontingent begrenzt, das Ihrer Organisation zugewiesen ist.
   
   d.	Geben Sie einen Namen an. Der Name ist nur zu Anzeigezwecken gedacht.
   
   e.	(Optional) Geben Sie eine ausführlichere Beschreibung des Datenträgers an. 
   
   f.	Klicken Sie auf **Erstellen**, um die Informationen zu übergeben und das Dialogfeld zu schließen. 

  Das Erstellen eines Datenträgers kann etwas Zeit dauern. 

2. Hängen Sie einen Datenträger an einen virtuellen Server an. 

   a. Öffnen Sie den {{site.data.keyword.blockstorageshort}}-Service. 
   
   b. Wählen Sie einen Datenträger aus der Liste der verfügbaren Datenträger aus. 
   
   c.	Klicken Sie auf **Anhängen**. 
   
   d.	Wählen Sie im Dialogfeld 'Anhängen' eine Instanz eines virtuellen Servers aus der Dropdown-Liste aus.  
   
   e.	Geben Sie optional das Gerät an, an das dieser Datenträger angehängt werden soll. Wenn Sie das Gerät nicht angegeben, wählt das System automatisch das erste verfügbare Gerät auf dem virtuellen Server aus.
   
   f.	Klicken Sie auf **Anhängen**, um die Informationen zu übergeben und das Dialogfeld zu schließen. 
   
   Der Datenträger wird in der Tabelle der angehängten Datenträger mit den Informationen zu der Instanz des virtuellen Servers aufgeführt. Der virtuelle Server kann nun das Gerät verwenden, um Daten persistent zu speichern.  
 
Nächste Schritte

Bereiten Sie den Datenträger zur Verwendung vor. Weitere Informationen finden Sie unter [Datenträger vorbereiten](../BlockStorage/blockstorage_preparingvolume.html). 

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{:id="samples"}

* [Verwendung von IBM Block Storage for Bluemix mit IBM Virtual Servers](https://developer.ibm.com/bluemix/2016/02/24/use-block-storage-for-bluemix-with-virtual-servers/){: new_window}
* [Einführung in IBM Block Storage for Bluemix](https://developer.ibm.com/bluemix/2016/02/15/getting-started-with-block-storage/){: new_window}
* [IBM Block Storage for Bluemix - Demo](https://www.youtube.com/watch?v=3gCIHYKU1rE&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm&index=45){: new_window}

## API-Referenz
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

