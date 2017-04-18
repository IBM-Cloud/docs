{:new_window: target="_blank"}


# Informazioni su {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Ultimo aggiornamento: 07 settembre 2016
{: .last-updated}

Il servizio IBM {{site.data.keyword.blockstorageshort}} ti consente di collegare un archivio persistente a un server virtuale.  Per utilizzare l'archivio, devi collegare i volumi di blocco ai tuoi server virtuali. I dati dei volumi di archiviazione blocchi persistono oltre il ciclo di vita del tuo server virtuale. Ciò significa che puoi scollegare i volumi da un'istanza del server e riallegarli a un'altra istanza del server, senza alcuna modifica ai dati. {{site.data.keyword.blockstorageshort}} utilizza OpenStack Cinder per gestire il ciclo di vita dei volumi. 

È possibile accedere all'archivio da un'unità di blocco che puoi partizionare, formattare e montare, come /dev/vdb. I dati sono conservati finché non li elimini. 

## Volumi 
{: #using-volumes-concept}

I volumi {{site.data.keyword.blockstorageshort}} vengono creati mediante un'istanza del servizio {{site.data.keyword.blockstorageshort}}. Puoi collegare i volumi a un server virtuale nei seguenti modi:
  

* Specifica un dispositivo particolare che hai fornito. 
* Specifica che il sistema seleziona automaticamente un nome dispositivo disponibile. 

Il server virtuale esegue le sue operazioni I/O direttamente con il dispositivo specificato, indipendentemente dal servizio {{site.data.keyword.blockstorageshort}}.

## Istantanee 
{: #using-snapshots-concept}

Puoi anche creare delle istantanee di volumi a livello dei blocchi. Un'istantanea acquisisce i dati nel volume di archiviazione dei blocchi in una temporizzazione specifica. Puoi utilizzare le istantanee per eseguire backup incrementali dei tuoi dati. Il che significa che le istantanee sono nello stesso archivio del volume originale. Pertanto, le istantanee non sono una strategia di ripristino di emergenza sufficiente.

**Nota**: non puoi creare le istantanee mentre un volume viene collegato a un'istanza del server. 

Quando crei un volume da un'istantanea, viene creato un nuovo volume nello stesso stato in cui era il volume originale nel momento in cui hai acquisito l'istantanea. 

La creazione di un volume da un'istantanea ha il seguente impatto: 

* I volumi esistenti non vengono rimossi.
* I dati creati, modificati o eliminati dopo l'acquisizione dell'istantanea pertinente non sono inclusi nel nuovo volume.

Operazioni successive

Crea un volume. Per ulteriori informazioni, consulta [Creazione di volumi](../BlockStorage/blockstorage_creatingvolume.html).
