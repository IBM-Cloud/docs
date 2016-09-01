{:new_window: target="_blank"}


# Informationen zu {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Letzte Aktualisierung: 01. August 2016
{: .last-updated}

## Datenträger 
{: #using-volumes-concept}

Mit IBM {{site.data.keyword.blockstorageshort}} können Sie Datenträger erstellen und diese an virtuelle Server anhängen. Standardmäßig verfügen virtuelle Server von IBM {{site.data.keyword.virtualmachinesshort}} nicht über persistenten Speicher und kehren zum Standardimage zurück, wenn sie erneut gestartet werden. {{site.data.keyword.blockstorageshort}} stellt persistenten Speicher für Ihren virtuellen Server zur Verfügung. Die Daten in Block Storage-Datenträgern (Blockspeicherdatenträgern) bleiben über den Lebenszyklus Ihres virtuellen Servers hinaus erhalten. In {{site.data.keyword.blockstorageshort}} wird OpenStack Cinder zur Verwaltung des Lebenszyklus von Datenträgern verwendet. 

{{site.data.keyword.blockstorageshort}}-Datenträger werden durch eine {{site.data.keyword.blockstorageshort}}-Serviceinstanz erstellt. Sie können die Datenträger auf die folgenden Weisen an einen virtuellen Server anhängen: 
  

* Sie können ein bestimmtes Gerät angeben, das Sie bereitstellen.  
* Sie können angeben, dass das System automatisch einen verfügbaren Gerätenamen auswählt.  

Der virtuelle Server führt seine E/A-Operationen direkt mit dem angegebenen Gerät unabhängig vom {{site.data.keyword.blockstorageshort}}-Service aus. 

## Momentaufnahmen 
{: #using-snapshots-concept}

Sie können auch Momentaufnahmen von Datenträgern auf Blockebene erstellen. Sie können keine Momentaufnahmen erstellen, während der Datenträger angehängt ist, sodass die resultierenden Momentaufnahmen über Ausfälle hinweg konsistent sind.  

Nächste Schritte

Erstellen Sie einen Datenträger. Weitere Informationen finden Sie unter [Datenträger erstellen](../BlockStorage/blockstorage_creatingvolume.html). 
