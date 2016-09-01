{:new_window: target="_blank"}


# Informazioni su {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Ultimo aggiornamento: 01 agosto 2016
{: .last-updated}

## Volumi 
{: #using-volumes-concept}

Puoi utilizzare IBM {{site.data.keyword.blockstorageshort}} per creare volumi e collegarli ai server virtuali. Per impostazione predefinita, IBM {{site.data.keyword.virtualmachinesshort}} non dispone di archivio persistente e torna all'immagine predefinita quando vengono riavviati. {{site.data.keyword.blockstorageshort}} fornisce archivio persistente per il tuo server virtuale. I dati dei volumi di archiviazione blocchi persistono oltre il ciclo di vita del tuo server virtuale. {{site.data.keyword.blockstorageshort}} utilizza OpenStack Cinder per gestire il ciclo di vita dei volumi.

I volumi {{site.data.keyword.blockstorageshort}} vengono creati mediante un'istanza del servizio {{site.data.keyword.blockstorageshort}}. Puoi collegare i volumi a un server virtuale nei seguenti modi:
  

* Specifica un dispositivo particolare che hai fornito. 
* Specifica che il sistema seleziona automaticamente un nome dispositivo disponibile. 

Il server virtuale esegue le sue operazioni I/O direttamente con il dispositivo specificato, indipendentemente dal servizio {{site.data.keyword.blockstorageshort}}. 

## Istantanee 
{: #using-snapshots-concept}

Puoi anche creare delle istantanee di volumi a livello dei blocchi. Non puoi creare le istantanee mentre il volume è collegato, quindi le istantanee risultanti saranno congruenti con eventuali arresti anomali del sistema.  

Operazioni successive

Crea un volume. Per ulteriori informazioni, consulta [Creazione di volumi](../BlockStorage/blockstorage_creatingvolume.html).
