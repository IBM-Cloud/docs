{:new_window: target="_blank"}


# Preparazione dei volumi {{site.data.keyword.blockstorageshort}} 
{: #preparing-block-storage-volume}

Ultimo aggiornamento: 29 luglio 2016
{: .last-updated}

  Dopo aver creato il tuo volume a averlo collegato a un server virtuale, devi montare e preparare il volume per poterlo utilizzare.
  
  **Nota**: i comandi pertinenti possono variare a seconda del sistema operativo specifico. Per ulteriori informazioni, consulta la documentazione sul sistema operativo. I seguenti passi sono stati verificati utilizzando un server virtuale CentOS.
  
  Per preparare un volume, attieniti a questa procedura: 

1. Accedi al server virtuale.  

   <pre><code>ssh -i security_key_name.pem ibmcloud@xxx.xx.xx.xx</pre></code>

   **Nota:** per trovare l'ID utente, il nome della chiave di sicurezza e il tuo indirizzo IP pubblico predefiniti, visualizza la scheda della panoramica del server virtuale. L'ID utente predefinito è *ibmcloud*. Per informazioni sull'accesso al server virtuale utilizzando SSH, consulta [Accesso a un'istanza del server virtuale da un terminale Linux](../../virtualmachines/vm_manage_instances.html#vm_login). 

2. Verifica che il volume sia collegato.  

   <pre><code>sudo su -</pre></code>
   
   **Nota:** se il comando *sudo su* non funziona per il tuo sistema operativo, utilizza *sudo* prima di ogni comando. Ad esempio, *sudo fdisk -l*.
   
   <pre><code>fdisk -l</pre></code>

   Le informazioni sul volume vengono elencate alla fine del testo informativo. Ad esempio, *Disk /dev/vdb: 10.7 GB, 10737418240 bytes*.

3. Partizionamento del disco.

   a. Avvia fdisk e crea una nuova partizione.
    
     <pre><code>fdisk /dev/vdb</pre></code>

   b. Immetti **n** per creare una nuova partizione.
   
   c. Immetti **p** per specificare la partizione primaria.
   
   d. Per creare una partizione, immetti **1**.
   
   e. A meno che tu non abbia dei requisiti specifici, seleziona i valori predefiniti nelle rimanenti richieste e premi Invio.

   f. Immetti **w** per scrivere nella partizione.
   
   g. Verifica che il nuovo disco sia stato creato.
   
     <pre><code>fdisk -l</pre></code>

     **Nota:** il nome del nuovo disco è normalmente il nome della partizione su cui è stato creato, con l'aggiunta di un numero incrementale, come 1. Ad esempio, *vdb1*.

4. Formatta il volume. 

   Devi formattare il volume in modo che archivi le informazioni. Questo esempio utilizza ext4; tuttavia, puoi utilizzare qualsiasi file system supportato.

   <pre><code>mkfs -t ext4 /dev/vdb1</pre></code>

    **Nota:** il passo per scrivere le informazioni di account del file system e dei superblocchi può richiedere ulteriore tempo per il completamento. Quando il processo è terminato, visualizzerai *eseguito* come stato.

5. Monta il volume. 

   a. Devi montare il volume per utilizzarlo.

      <pre><code>mkdir -p /mnt/myvolume</pre></code>
      
      <pre><code>mount /dev/vdb1 /mnt/myvolume</pre></code>

      dove *myvolume* è un nome cartella di tua scelta.

   b. Controlla che il tuo volume sia elencato e pronto.

      <pre><code>df -h</pre></code>

6. (Facoltativo) Monta il volume in modo permanente. 

   Potresti voler montare il volume in modo permanente, così da non dover ripetere il montaggio dopo un riavvio.

   a. Individua l'UUID per il tuo volume.

      <pre><code>blkid</pre></code>

   b. Copia l'UUID elencato.

   c. Modifica le informazioni della tabella dei file system.

      <pre><code>nano /etc/fstab</pre></code>      

   d. Incolla la seguente riga, incluso il tuo UUID specifico, alla fine del file e salva.
   
      <pre><code>UUID=xxxxxx /mnt/myvolume ext4 defaults  0 2</pre></code>

   e. Per verificare che il volume sia montato in modo permanente, riavvia il server virtuale.

      <pre><code>reboot</pre></code>

  Quando il server virtuale è nuovamente in esecuzione, accedi al server virtuale e modifica le directory nella nuova cartella che hai creato. Ad esempio vai a **cd /mnt/myvolume**.

  Puoi ora utilizzare il volume.
