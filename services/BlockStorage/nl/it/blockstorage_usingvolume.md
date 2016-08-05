{:new_window: target="_blank"} 

# Utilizzo del volume {{site.data.keyword.blockstorageshort}}  {: #using-block-storage-volume} 

*Ultimo aggiornamento: 20 giugno 2016*
{: .last-updated}

## Creazione di un volume {: #creating-volume} 

1.	Fai clic su **Crea** per avviare la finestra di dialogo **Crea volume**.
2.	Fornisci la dimensione del volume che desideri. I numeri decimali non sono accettati. La dimensione è limitata dalla quota assegnata alla tua organizzazione.
3.	Fornisci un nome. Il nome serve solo per finalità di visualizzazione.
4.	Facoltativamente, fornisci una descrizione più dettagliata del volume. 
5.	Fai clic su **Crea** per inoltrare le informazioni e chiudere la finestra di dialogo. 

La creazione di un volume può richiedere qualche minuto. 

## Eliminazione di un volume {: #deleting-volume}

1.	Seleziona il volume che vuoi eliminare.
2.	Fai clic su **Elimina**.
3.	Conferma l'eliminazione di questo volume.

Non puoi eliminare un volume collegato a un server virtuale. Devi prima scollegare il volume.

## Estensione di un volume {: #extending-volume}
Puoi aumentare la dimensione del volume fino a 10 volte la dimensione originale mediante l'azione**Estendi**. Non puoi ridurre la dimensione di un volume.

1.	Seleziona il volume da estendere.
2.	Fai clic su **Estendi**.
3.	Seleziona la nuova dimensione del volume. Fornisci la nuova dimensione totale del volume.
4.	Fai clic su **Estendi** per inoltrare le informazioni e chiudere la finestra di dialogo. 

Per essere esteso, un volume deve essere nello stato **Disponibile**. 

## Collegamento e scollegamento di un volume a un server virtuale {: #attaching-detaching-volume}
I volumi sono collegati e scollegati ai/dai server virtuali come dispositivi con uno specifico nome dispositivo. Per consentire a un server virtuale di memorizzare in modo persistente i dati su un volume, devi collegare il volume al server virtuale.

Per collegare un volume, attieniti a questa procedura: 

1.	Seleziona un volume dall'elenco di volumi disponibili.
2.	Fai clic su **Collega**.
3.	Nella finestra di dialogo Collega, seleziona un'istanza di un server virtuale dall'elenco a discesa. 
4.	Facoltativamente, specifica il dispositivo da utilizzare per collegare questo volume. Se non specifichi il dispositivo, il sistema seleziona automaticamente il primo dispositivo disponibile sul server virtuale.
5.	Fai clic su **Collega** per inoltrare le informazioni e chiudere la finestra di dialogo.

Il volume è elencato nella tabella di volumi collegati con le informazioni sull'istanza del server virtuale.
Il server virtuale può ora utilizzare il dispositivo per salvare in modo permanente i dati. 

Per scollegare un volume, attieniti a questa procedura: 

1.	Seleziona un volume dall'elenco di volumi collegati. 
2.	Fai clic su **Scollega**.
3.	Conferma lo scollegamento nella finestra di dialogo. 

Dopo essere stato scollegato, il volume non è più disponibile per le operazioni I/O nell'istanza del server virtuale. Nell'IU del servizio {{site.data.keyword.blockstorageshort}}, il volume è ora disponibile per essere collegato ad altri server virtuali.
