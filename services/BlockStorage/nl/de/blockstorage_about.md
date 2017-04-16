{:new_window: target="_blank"}


# Informationen zu {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Letzte Aktualisierung: 07. September 2016
{: .last-updated}

Mit dem IBM {{site.data.keyword.blockstorageshort}}-Service können Sie persistenten Speicher an einen virtuellen Server anhängen.  Um den Speicher zu verwenden, hängen Sie Blockdatenträger an Ihre virtuellen Server. Die Daten in Block Storage-Datenträgern (Blockspeicherdatenträgern) bleiben über den Lebenszyklus Ihres virtuellen Servers hinaus erhalten. Dies bedeutet, dass Sie die Datenträger von einer Serverinstanz abhängen und wieder an eine andere Serverinstanz anhängen können, und zwar ohne Änderungen Ihrer Daten. In {{site.data.keyword.blockstorageshort}} wird OpenStack Cinder zur Verwaltung des Lebenszyklus von Datenträgern verwendet. 

Auf den Speicher wird auf einer Blockeinheit zugegriffen, die Sie partitionieren und formatieren und an die Sie Komponenten anhängen können, z. B. /dev/vdb. Die Daten bleiben so lange bestehen, bis Sie sie löschen. 

## Datenträger 
{: #using-volumes-concept}

{{site.data.keyword.blockstorageshort}}-Datenträger werden durch eine {{site.data.keyword.blockstorageshort}}-Serviceinstanz erstellt. Sie können die Datenträger auf die folgenden Weisen an einen virtuellen Server anhängen:
  

* Sie können ein bestimmtes Gerät angeben, das Sie bereitstellen. 
* Sie können angeben, dass das System automatisch einen verfügbaren Gerätenamen auswählt. 

Der virtuelle Server führt seine E/A-Operationen direkt mit dem angegebenen Gerät unabhängig vom {{site.data.keyword.blockstorageshort}}-Service aus.

## Momentaufnahmen 
{: #using-snapshots-concept}

Sie können auch Momentaufnahmen von Datenträgern auf Blockebene erstellen. Bei einer Momentaufnahme werden zu einem bestimmten Zeitpunkt Daten auf dem Block Storage-Datenträger erfasst. Mithilfe von Momentaufnahmen können Sie inkrementelle Sicherungen Ihrer Daten erstellen. D. h., die Momentaufnahmen sind in demselben Speicher vorhanden wie der ursprüngliche Datenträger. Aus diesem Grund sind Momentaufnahmen keine ausreichende Strategie zur Disaster-Recovery.

**Anmerkung**: Es können keine Momentaufnahmen erstellt werden, solange ein Datenträger an eine Serverinstanz angehängt ist. 

Wenn Sie einen Datenträger auf Basis einer Momentaufnahme erstellen, wird ein neuer Datenträger erstellt, der denselben Status aufweist wie der ursprüngliche Datenträger zum Zeitpunkt der Momentaufnahmeerstellung. 

Die Erstellung eines Datenträgers auf Basis einer Momentaufnahme hat folgende Auswirkungen:

* Vorhandene Datenträger werden nicht entfernt.
* Daten, die nach Erstellung der relevanten Momentaufnahme erstellt, geändert oder gelöscht werden, werden nicht in den neuen Datenträger aufgenommen.

Nächste Schritte

Erstellen Sie einen Datenträger. Weitere Informationen finden Sie unter [Datenträger erstellen](../BlockStorage/blockstorage_creatingvolume.html).
