
{:new_window: target="_blank"}


# Collegamento di volumi {{site.data.keyword.blockstorageshort}} a un server virtuale
{: #attaching-block-storage-volume}

Ultimo aggiornamento: 29 luglio 2016
{: .last-updated}

I volumi sono collegati e scollegati ai/dai server virtuali come dispositivi con uno specifico nome dispositivo. Per consentire a un server virtuale di memorizzare in modo persistente i dati su un volume, devi collegare il volume al server virtuale.

Per collegare un volume, attieniti a questa procedura:

1.	Seleziona un volume dall'elenco di volumi disponibili.
2.	Fai clic su **Collega**.
3.	Nella finestra di dialogo Collega, seleziona un'istanza di un server virtuale dall'elenco a discesa.
4.	Facoltativamente, specifica il dispositivo da utilizzare per collegare questo volume. Se non specifichi il dispositivo, il sistema seleziona automaticamente il primo dispositivo disponibile sul server virtuale.
5.	Fai clic su **Collega** per inoltrare le informazioni e chiudere la finestra di dialogo.

Il volume è elencato nella tabella di volumi collegati con le informazioni sull'istanza del server virtuale.
Il server virtuale può ora utilizzare il dispositivo per salvare in modo permanente i dati. 

Operazioni successive

Dopo aver creato il volume e averlo collegato a un server virtuale, consulta [Preparazione dei volumi](../BlockStorage/blockstorage_preparingvolume.html) per prepararlo all'utilizzo.
