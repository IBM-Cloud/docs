{:new_window: target="_blank"} 


# Utilizzo dell'istantanea di{{site.data.keyword.blockstorageshort}} {: #using-block-storage-snapshot} 
Ultimo aggiornamento: 07 settembre 2016
{: .last-updated}

Per utilizzare le istantanee, attieniti a questa procedura:  

## Creazione di un'istantanea {: #creating-snapshot} 

1.  Nella IU di Bluemix, seleziona **Console > Archivio**.
2.  Seleziona l'istanza di Block Storage di cui hai precedentemente eseguito il provisioning.
3.	Fai clic nella scheda di gestione.
4.	Nella pagina di gestione, fai clic sulla scheda **Volumi** per ottenere un elenco di volumi.
5.	Seleziona il volume di cui vuoi creare un'istantanea nella colonna dei volumi non collegati. Assicurati che il volume da te selezionato non sia collegato. Il volume selezionato è evidenziato. 
6.	Dal menu a discesa delle azioni, fai clic su **Crea istantanea**.
7.	Dai un nome all'istantanea e fai clic su **Crea**.

**Nota:** 

* Non puoi eliminare un volume mentre ne esistono delle istantanee.  
* La dimensione dell'istantanea viene automaticamente impostata per essere la stessa del volume originale.

## Creazione di un volume da un'istantanea {: #creating-volume-from-snapshot}

1.  Nella IU di Bluemix, seleziona **Console > Archivio**.
2.  Seleziona l'istanza di Block Storage di cui hai precedentemente eseguito il provisioning.
3.	Fai clic nella scheda di gestione.
4.	Nella pagina di gestione, fai clic sulla scheda **Istantanee** per ottenere un elenco di istantanee. 
5.	Seleziona l'istantanea dalla quale vuoi creare un volume. L'istantanea selezionata è evidenziata.
6.	Dal menu a discesa delle azioni, fai clic su **Crea volume**. 
7.	Dai al nuovo volume un nome e, facoltativamente, una nuova dimensione, e fai clic su **Crea**. 

**Nota:** la nuova dimensione del volume deve essere uguale o superiore a quella dell'istantanea. 

## Eliminazione di un'istantanea {: #deleting-snapshot}

1.  Nella IU di Bluemix, seleziona **Console > Archivio**.
2.  Seleziona l'istanza di Block Storage di cui hai precedentemente eseguito il provisioning.
3.	Fai clic nella scheda di gestione.
4.	Nella pagina di gestione, fai clic sulla scheda **Istantanee** per ottenere un elenco di istantanee. 
5.	Seleziona l'istantanea che vuoi eliminare. L'istantanea selezionata è evidenziata.
6.	Dal menu a discesa, fai clic su **Elimina**. 



