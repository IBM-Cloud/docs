{:new_window: target="_blank"} 

# Introduzione a {{site.data.keyword.blockstorageshort}} (BETA)

{{site.data.keyword.blockstoragefull}} fornisce l'accesso all'archiviazione a livello di blocchi per i carichi di lavoro e i runtime che utilizzano molte transazioni e che hanno bisogno di un'archiviazione persistente.

Puoi utilizzare IBM {{site.data.keyword.blockstorageshort}} per {{site.data.keyword.Bluemix_notm}} per creare dei volumi {{site.data.keyword.blockstorageshort}} che possono essere collegati alle macchine virtuali. I dati dei volumi di archiviazione blocchi persistono oltre il ciclo di vita delle tue macchine virtuali. IBM {{site.data.keyword.blockstorageshort}} utilizza OpenStack Cinder per gestire il ciclo di vita dei volumi.

I volumi {{site.data.keyword.blockstorageshort}} vengono creati mediante un'istanza del servizio IBM {{site.data.keyword.blockstorageshort}}. Puoi collegare i volumi a una macchina virtuale in uno specifico dispositivo da te fornito oppure il sistema può selezionare automaticamente un nome dispositivo disponibile. La macchina virtuale esegue le sue operazioni I/O direttamente con il dispositivo specificato, indipendentemente dal servizio {{site.data.keyword.blockstorageshort}}.

Puoi anche creare delle istantanee di volumi a livello dei blocchi. Il servizio {{site.data.keyword.blockstorageshort}} non consente la creazione di istantanee mentre il volume è collegato, quindi le istantanee risultanti saranno congruenti con eventuali arresti anomali del sistema. 

## Come creare un'istanza del servizio {{site.data.keyword.blockstorageshort}}
Per creare un'istanza del servizio {{site.data.keyword.blockstorageshort}} nel tuo spazio, attieniti alla seguente procedura:
 
1.	Vai alla scheda {{site.data.keyword.Bluemix_notm}} **Catalogo** e immetti **{{site.data.keyword.blockstorageshort}}** nella
casella di ricerca oppure vai a **Servizi** e seleziona **Archiviazione**. Fai clic sul servizio **{{site.data.keyword.blockstorageshort}}**. 
2.	Immetti un nome di spazio e di servizio. Seleziona il piano e fai clic su **Crea**.
 	
Il servizio {{site.data.keyword.blockstorageshort}} è supportato solo in un contesto senza bind. 

Un'istanza del servizio {{site.data.keyword.blockstorageshort}} viene creata nel tuo spazio. Puoi aprire l'IU {{site.data.keyword.blockstorageshort}} per gestire i volumi in qualsiasi momento facendo clic sull'icona dell'istanza del servizio.

## Interfaccia utente (IU) {{site.data.keyword.blockstorageshort}}
La GUI (graphical user interface) {{site.data.keyword.blockstorageshort}} fornisce una panoramica di alto livello dei tuoi volumi di archiviazione, delle tue istantanee e dell'utilizzo totale dell'archiviazione sia per i volumi che per le istantanee nella parte superiore della finestra. 

L'intestazione include la data e l'ora dell'ultimo aggiornamento dell'IU. Puoi utilizzare l'icona di aggiornamento (un'icona di freccia circolare) per aggiornare l'IU manualmente, se necessario. 

Utilizza la barra di ricerca per trovare i volumi in base alla stringa da te immessa. Le tabelle vengono filtrate man mano che digiti per mostrare solo i volumi che corrispondono alla stringa di ricerca immessa.

Sotto la panoramica ci sono due schede, per i volumi e per le istantanee. La scheda dei volumi è selezionata per impostazione predefinita. Le tabelle in questa scheda elencano informazioni dettagliate sui volumi disponibili e collegati. Ciascuna riga in una tabella mostra le proprietà più importanti di un volume. Ulteriori proprietà sono disponibili quando espandi una riga. I volumi collegati mostrano anche l'istanza di macchina virtuale e il dispositivo a cui è collegato il volume. 

La scheda delle istantanee mostra una tabella di istantanee con proprietà e modalità di funzionamento analoghe. 

Utilizza l'icona Crea sopra le tabelle per creare un nuovo volume o per modificare quelli esistenti. Se crei un volume a partire da un'istantanea, puoi utilizzare anche l'elenco a discesa Azioni.


## Azioni volume

### Crea un volume

1.	Fai clic su **Crea** per avviare la finestra di dialogo **Crea volume**.
2.	Fornisci la dimensione del volume che desideri. I numeri decimali non sono accettati. La dimensione è limitata dalla quota assegnata alla tua organizzazione.
3.	Fornisci un nome. Il nome serve solo per finalità di visualizzazione.
4.	Facoltativamente, fornisci una descrizione più dettagliata del volume. 
5.	Fai clic su **Crea** per inoltrare le informazioni e chiudere la finestra di dialogo. 

La creazione di un volume può richiedere qualche minuto. 

### Elimina un volume

1.	Seleziona il volume che vuoi eliminare.
2.	Fai clic su **Elimina**.
3.	Conferma l'eliminazione di questo volume.

Non puoi eliminare un volume collegato a una macchina virtuale. Devi prima scollegare il volume.

### Estendi un volume
Puoi aumentare la dimensione del volume mediante l'azione **Estendi**. Non puoi ridurre la dimensione di un volume.

1.	Seleziona il volume da estendere.
2.	Fai clic su **Estendi**.
3.	Seleziona la nuova dimensione del volume. Fornisci la nuova dimensione totale del volume.
4.	Fai clic su **Estendi** per inoltrare le informazioni e chiudere la finestra di dialogo. 

Per essere esteso, un volume deve essere nello stato **Disponibile**. 

### Collega e scollega un volume a/da una macchina virtuale
I volumi sono collegati e scollegati alle/dalle macchine virtuali come dispositivi con uno specifico nome dispositivo. Per consentire a una macchina virtuale di memorizzare in modo persistente i dati su un volume, devi collegare il volume alla macchina virtuale.

Per collegare un volume, attieniti a questa procedura: 

1.	Seleziona un volume dall'elenco di volumi disponibili.
2.	Fai clic su **Collega**.
3.	Nella finestra di dialogo Collega, seleziona un'istanza di una macchina virtuale dall'elenco a discesa. 
4.	Facoltativamente, specifica il dispositivo da utilizzare per collegare questo volume. Se non specifichi il dispositivo, il sistema seleziona automaticamente il primo dispositivo disponibile sulla macchina virtuale.
5.	Fai clic su **Collega** per inoltrare le informazioni e chiudere la finestra di dialogo.

Il volume è elencato nella tabella di volumi collegati con le informazioni sull'istanza della macchina virtuale. 
La macchina virtuale può ora utilizzare il dispositivo per salvare in modo permanente i dati. 

Per scollegare un volume, attieniti a questa procedura: 

1.	Seleziona un volume dall'elenco di volumi collegati. 
2.	Fai clic su **Scollega**.
3.	Conferma lo scollegamento nella finestra di dialogo. 

Dopo essere stato scollegato, il volume non è più disponibile per le operazioni I/O nell'istanza della macchina virtuale. Nell'IU del servizio {{site.data.keyword.blockstorageshort}}, il volume è ora disponibile per essere collegato ad altre macchine virtuali.

## Azioni relative alle istantanee

### Crea un'istantanea

1.	Seleziona la scheda **Volumi** per ottenere un elenco di volumi.
2.	Seleziona il volume di cui vuoi creare un'istantanea nella colonna dei volumi non collegati. Assicurati che il volume da te selezionato non sia collegato. Il volume selezionato è evidenziato. 
3.	Fai clic su **Azioni** e seleziona **Crea istantanea** dall'elenco a discesa.
4.	Dai un nome all'istantanea e fai clic su **Crea**.

**Nota:** non puoi eliminare un volume mentre ne esistono delle istantanee. 

### Crea un volume da un'istantanea.

1.	Seleziona la scheda **Istantanee** per ottenere un elenco di istantanee.
2.	Seleziona l'istantanea dalla quale vuoi creare un volume. L'istantanea selezionata è evidenziata.
3.	Fai clic su **Azioni** e seleziona **Crea volume** dall'elenco a discesa.
4.	Dai al nuovo volume un nome e, facoltativamente, una nuova dimensione, e fai clic su **Crea**. 

**Nota:** la nuova dimensione del volume deve essere uguale o superiore a quella dell'istantanea. 

### Elimina un'istantanea

1.	Seleziona la scheda **Istantanee** per ottenere un elenco di istantanee.
2.	Seleziona l'istantanea che vuoi eliminare. L'istantanea selezionata è evidenziata.
3.	Fai clic su **Azioni** e seleziona **Elimina**. 



># Link correlati {:class="linklist"}
>## Guida di riferimento API {:id="api"}
>* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}
>
>{:elementKind="article" id="rellinks"}
