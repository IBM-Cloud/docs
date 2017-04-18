{:new_window: target="_blank"} 

# Utilizzo del volume {{site.data.keyword.blockstorageshort}} 
{: #using-block-storage-volume} 
Ultimo aggiornamento: 07 settembre 2016
{: .last-updated}

Per utilizzare i volumi, attieniti a questa procedura: 

## Eliminazione di un volume {: #deleting-volume}

1.  Nella IU di Bluemix, seleziona **Console > Archivio**.
2.  Seleziona l'istanza di Block Storage di cui hai precedentemente eseguito il provisioning.
3.	Seleziona il volume che vuoi eliminare.
4.	Dal menu a discesa delle azioni, fai clic su **Elimina**. 
5.	Conferma l'eliminazione di questo volume.

Non puoi eliminare un volume collegato a un server virtuale. Devi prima scollegare il volume. L'eliminazione del volume rende il volume inaccessibile per un utilizzo futuro e i dati in esso vanno persi. Inoltre, non puoi eliminare i volumi con istantanee associate.

## Estensione di un volume {: #extending-volume}
Puoi aumentare la dimensione del volume fino a 10 volte la dimensione originale mediante l'azione**Estendi**. Non puoi ridurre la dimensione di un volume.

1.  Nella IU di Bluemix, seleziona **Console > Archivio**.
2.  Seleziona l'istanza di Block Storage di cui hai precedentemente eseguito il provisioning.
3.	Seleziona il volume da estendere.
4.	Dal menu a discesa delle azioni, fai clic su **Estendi**.
5.	Seleziona la nuova dimensione del volume. Fornisci la nuova dimensione totale del volume.
6.	Fai clic su **Estendi** per inoltrare le informazioni e chiudere la finestra di dialogo. 

Per essere esteso, un volume deve essere nello stato **Disponibile**. Dopo aver esteso il volume, devi inviare una notifica al file system (come ad esempio ext4) che il disco è stato esteso ridimensionando il file system con una nuova dimensione. 

## Collegamento e scollegamento di un volume a un server virtuale {: #attaching-detaching-volume}
I volumi sono collegati e scollegati ai/dai server virtuali come dispositivi con uno specifico nome dispositivo. Per consentire a un server virtuale di memorizzare in modo persistente i dati su un volume, devi collegare il volume al server virtuale.

Per collegare un volume, attieniti a questa procedura: 

1.  Nella IU di Bluemix, seleziona **Console > Archivio**.
2.  Seleziona l'istanza di Block Storage di cui hai precedentemente eseguito il provisioning.
3.	Seleziona un volume dall'elenco di volumi disponibili.
4.	Dal menu a discesa delle azioni, fai clic su **Allega**.
5.	Nella finestra di dialogo Collega, seleziona un'istanza di un server virtuale dall'elenco a discesa. 
6.	Facoltativamente, specifica il dispositivo da utilizzare per collegare questo volume. Se non specifichi il dispositivo, il sistema seleziona automaticamente il primo dispositivo disponibile sul server virtuale.
7.	Fai clic su **Collega** per inoltrare le informazioni e chiudere la finestra di dialogo.

Il volume è elencato nella tabella di volumi collegati con le informazioni sull'istanza del server virtuale. 
Il server virtuale può ora utilizzare il dispositivo per salvare in modo permanente i dati. 

Quando sei pronto per scollegare un volume, devi preparare il server virtuale per lo scollegamento. Ad esempio, arresta tutte le applicazioni che stanno utilizzando il file system. Inoltre, annulla il montaggio dall'interno dell'istanza del server virtuale.

Per scollegare un volume, attieniti a questa procedura: 

1.  Nella IU di Bluemix, seleziona **Console > Archivio**.
2.  Seleziona l'istanza di Block Storage di cui hai precedentemente eseguito il provisioning.
3.	Seleziona un volume dall'elenco di volumi collegati. 
4.	Dal menu a discesa delle azioni, fai clic su **Scollega**.
5.	Conferma lo scollegamento nella finestra di dialogo. 

Dopo essere stato scollegato, il volume non è più disponibile per le operazioni I/O nell'istanza del server virtuale. Nell'IU del servizio {{site.data.keyword.blockstorageshort}}, il volume è ora disponibile per essere collegato ad altri server virtuali.
