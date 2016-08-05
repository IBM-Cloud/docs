{:new_window: target="_blank"} 

# Introduzione a {{site.data.keyword.blockstorageshort}} (Beta)

*Ultimo aggiornamento: 15 luglio 2016*
{: .last-updated}

{{site.data.keyword.blockstoragefull}} fornisce l'accesso all'archiviazione a livello di blocchi per i carichi di lavoro e i runtime che utilizzano molte transazioni e che hanno bisogno di un'archiviazione persistente.

Puoi utilizzare IBM {{site.data.keyword.blockstorageshort}} per {{site.data.keyword.Bluemix_notm}} per creare dei volumi {{site.data.keyword.blockstorageshort}} che possono essere collegati ai server virtuali. I dati dei volumi di archiviazione blocchi persistono oltre il ciclo di vita dei tuoi server virtuali. IBM {{site.data.keyword.blockstorageshort}} utilizza OpenStack Cinder per gestire il ciclo di vita dei volumi.

I volumi {{site.data.keyword.blockstorageshort}} vengono creati mediante un'istanza del servizio IBM {{site.data.keyword.blockstorageshort}}. Puoi collegare i volumi a un server virtuale in uno specifico dispositivo da te fornito oppure il sistema può selezionare automaticamente un nome dispositivo disponibile. Il server virtuale esegue le sue operazioni I/O direttamente con il dispositivo specificato, indipendentemente dal servizio {{site.data.keyword.blockstorageshort}}.

Puoi anche creare delle istantanee di volumi a livello dei blocchi. Il servizio {{site.data.keyword.blockstorageshort}} non consente la creazione di istantanee mentre il volume è collegato, quindi le istantanee risultanti saranno congruenti con eventuali arresti anomali del sistema. 


## Come creare un'istanza del servizio {{site.data.keyword.blockstorageshort}}
Per creare un'istanza del servizio {{site.data.keyword.blockstorageshort}} nel tuo spazio, attieniti alla seguente procedura:
 
1.	Vai alla scheda {{site.data.keyword.Bluemix_notm}} **Catalogo** e immetti **{{site.data.keyword.blockstorageshort}}** nella
casella di ricerca oppure vai a **Servizi** e seleziona **Archiviazione**. Fai clic sul servizio **{{site.data.keyword.blockstorageshort}}**. 
2.	Immetti un nome di spazio e di servizio. Seleziona il piano e fai clic su **Crea**.
 	
Il servizio {{site.data.keyword.blockstorageshort}} è supportato solo in un contesto senza bind. 

Un'istanza del servizio {{site.data.keyword.blockstorageshort}} viene creata nel tuo spazio. Puoi aprire l'IU {{site.data.keyword.blockstorageshort}} per gestire i volumi in qualsiasi momento facendo clic sull'icona dell'istanza del servizio.



## Utilizzo dell'interfaccia utente (IU) {{site.data.keyword.blockstorageshort}} {: #using-block-storage-ui}
La GUI (graphical user interface) {{site.data.keyword.blockstorageshort}} fornisce una panoramica di alto livello dei tuoi volumi di archiviazione, delle tue istantanee e dell'utilizzo totale dell'archiviazione sia per i volumi che per le istantanee nella parte superiore della finestra. 

L'intestazione include la data e l'ora dell'ultimo aggiornamento dell'IU. Puoi utilizzare l'icona di aggiornamento (un'icona di freccia circolare) per aggiornare l'IU manualmente, se necessario. 

Utilizza la barra di ricerca per trovare i volumi in base alla stringa da te immessa. Le tabelle vengono filtrate man mano che digiti per mostrare solo i volumi che corrispondono alla stringa di ricerca immessa.

Sotto la panoramica ci sono due schede, per i volumi e per le istantanee. La scheda dei volumi è selezionata per impostazione predefinita. Le tabelle in questa scheda elencano informazioni dettagliate sui volumi disponibili e collegati. Ciascuna riga in una tabella mostra le proprietà più importanti di un volume. Ulteriori proprietà sono disponibili quando espandi una riga. I volumi collegati mostrano anche l'istanza di server virtuale e il dispositivo a cui è collegato il volume. 

La scheda delle istantanee mostra una tabella di istantanee con proprietà e modalità di funzionamento analoghe. 

Utilizza l'icona Crea sopra le tabelle per creare un nuovo volume o per modificare quelli esistenti. Se crei un volume a partire da un'istantanea, puoi utilizzare anche l'elenco a discesa Azioni.




## Collegamento di un volume a un server virtuale {: #attaching-detaching-volume}
I volumi sono collegati e scollegati ai/dai server virtuali come dispositivi con uno specifico nome dispositivo. Per consentire a un server virtuale di memorizzare in modo persistente i dati su un volume, devi collegare il volume al server virtuale.

Per collegare un volume, attieniti a questa procedura: 

1.	Seleziona un volume dall'elenco di volumi disponibili.
2.	Fai clic su **Collega**.
3.	Nella finestra di dialogo Collega, seleziona un'istanza di un server virtuale dall'elenco a discesa. 
4.	Facoltativamente, specifica il dispositivo da utilizzare per collegare questo volume. Se non specifichi il dispositivo, il sistema seleziona automaticamente il primo dispositivo disponibile sul server virtuale.
5.	Fai clic su **Collega** per inoltrare le informazioni e chiudere la finestra di dialogo.

Il volume è elencato nella tabella di volumi collegati con le informazioni sull'istanza del server virtuale.
Il server virtuale può ora utilizzare il dispositivo per salvare in modo permanente i dati. 


# Link correlati
{: #rellinks}

## Guida di riferimento API
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

