{:new_window: target="_blank"} 

# Introduzione a {{site.data.keyword.blockstorageshort}} (Beta)

Ultimo aggiornamento: 29 luglio 2016
{: .last-updated}

{{site.data.keyword.blockstoragefull}} fornisce l'accesso all'archiviazione a livello di blocchi per i carichi di lavoro e i runtime che utilizzano molte transazioni e che hanno bisogno di un'archiviazione persistente. Puoi utilizzare il servizio {{site.data.keyword.blockstorageshort}} per gestire i cicli di vita del volume, collegare i volumi ai tuoi server virtuali IBM e creare istantanee dei tuoi volumi di archiviazione blocchi.

Prima di iniziare, rivedi le seguenti informazioni.

* Il servizio {{site.data.keyword.blockstorageshort}} è supportato solo in un contesto senza bind.  
* Devi disporre di IBM {{site.data.keyword.virtualmachinesshort}} creato per collegare i volumi di archiviazione blocchi. Per informazioni sull'utilizzo del volumi di archiviazione blocchi con {{site.data.keyword.virtualmachinesshort}}, consulta [Volumi di archiviazione blocchi e server virtuali IBM](../../virtualmachines/vm_create.html#storage_BS). 

Completa questa procedura per iniziare ad utilizzare {{site.data.keyword.blockstorageshort}}:

1. Crea un volume. 
   
   a. Apri il servizio {{site.data.keyword.blockstorageshort}}.

   b. Fai clic su **Crea** per avviare la finestra di dialogo **Crea volume**.

   c.	Fornisci la dimensione del volume che desideri. I numeri decimali non sono accettati. La dimensione è limitata dalla quota assegnata alla tua organizzazione.
   
   d.	Fornisci un nome. Il nome serve solo per finalità di visualizzazione.
   
   e.	Facoltativamente, fornisci una descrizione più dettagliata del volume.
   
   f.	Fai clic su **Crea** per inoltrare le informazioni e chiudere la finestra di dialogo.

  La creazione di un volume può richiedere qualche minuto.

2. Collega un volume a un server virtuale.

   a. Apri il servizio {{site.data.keyword.blockstorageshort}}.
   
   b. Seleziona un volume dall'elenco di volumi disponibili.
   
   c.	Fai clic su **Collega**.
   
   d.	Nella finestra di dialogo Collega, seleziona un'istanza di un server virtuale dall'elenco a discesa. 
   
   e.	Facoltativamente, specifica il dispositivo da utilizzare per collegare questo volume. Se non specifichi il dispositivo, il sistema seleziona automaticamente il primo dispositivo disponibile sul server virtuale.
   
   f.	Fai clic su **Collega** per inoltrare le informazioni e chiudere la finestra di dialogo.
   
   Il volume è elencato nella tabella di volumi collegati con le informazioni sull'istanza del server virtuale. Il server virtuale può ora utilizzare il dispositivo per salvare in modo permanente i dati. 
 
Operazioni successive

Prepara il volume per l'utilizzo. Per ulteriori informazioni, consulta [Preparazione dei volumi](../BlockStorage/blockstorage_preparingvolume.html).

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{:id="samples"}

* [How to Use IBM Block Storage for Bluemix with IBM Virtual Servers](https://developer.ibm.com/bluemix/2016/02/24/use-block-storage-for-bluemix-with-virtual-servers/){: new_window}
* [Getting Started with IBM Block Storage for Bluemix](https://developer.ibm.com/bluemix/2016/02/15/getting-started-with-block-storage/){: new_window}
* [IBM Block Storage for Bluemix Demo](https://www.youtube.com/watch?v=3gCIHYKU1rE&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm&index=45){: new_window}

## Guida di riferimento API
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

