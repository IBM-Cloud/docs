---

copyright:
  years: 2015, 2016

---
# Monitoraggio delle applicazioni con {{site.data.keyword.mobileanalytics_short}}
{: #monitoringapps}
*Ultimo aggiornamento: 6 maggio 2016*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} fornisce il monitoraggio e l'analisi per le tue applicazioni mobili. Puoi registrare i log client e monitorare i dati con
l'SDK client {{site.data.keyword.mobileanalytics_short}}. Gli sviluppatori possono controllare quando inviare questi dati al
servizio {{site.data.keyword.mobileanalytics_short}}. Quando i dati vengono distribuiti a {{site.data.keyword.mobileanalytics_short}}, puoi utilizzare il
dashboard {{site.data.keyword.mobileanalytics_short}} per ottenere delle approfondite informazioni di analisi delle applicazioni mobili, dei dispositivi e dei log client.
{: shortdesc}

## Visualizzazione dei dati con i grafici personalizzati
{: #custom-charts}

Puoi visualizzare i dati di analisi raccolti nel tuo repository di analisi. Questa visualizzazione è un modo efficace per ispezionare i dati per specifici casi d'uso. Puoi creare dei grafici con i dati già raccolti da Operational Analytics, in aggiunta ai dati personalizzati da te notificati.

### Creazione di grafici personalizzati per i log client
{: #custom-charts-client-logs}

Puoi creare un grafico personalizzato per i log client che contengono le informazioni di log inviate con l'API Logger per la piattaforma. Le informazioni di log includono anche le informazioni contestuali sul dispositivo, compresi ambiente, nome dell'applicazione e versione dell'applicazione.

In questo esempio, utilizzi i dati dei log client per creare un diagramma di flusso. Il grafico finale mostra la distribuzione dei livelli di log in una specifica applicazione. Hai anche a tua disposizione i seguenti dati da visualizzare in un grafico:

* Dati specifici
  * Livello di log
* Dati messaggio
  * Data/Ora
* Dati contestuali del sistema operativo del dispositivo
  * Nome applicazione
  * Versione applicazione
  * Sistema operativo dispositivo
* Dati di contesto del dispositivo
  * ID dispositivo
  * Modello dispositivo
  * Versione del sistema operativo del dispositivo


1. Accertati di disporre di un'applicazione che stia raccogliendo i log dispositivo o l'analisi.
2. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic sulla scheda **Grafici personalizzati** nella pagina **Dashboard**. Puoi creare un grafico basato sui messaggi di analisi inviati al server.
3. Fai clic su **Crea grafico** per creare un nuovo grafico personalizzato e fornisci i seguenti valori:
  * Titolo grafico: Applicazione e livelli di log
  * Tipo di evento: Log client
  * Tipo di grafico: Diagramma di flusso
5. Fai clic sulla scheda **Definizione grafico** e fornisci i seguenti valori:
  * Origine: Nome applicazione
  * Destinazione: Livello di log
  * Proprietà: il tuo nome applicazione
7. Fai clic su **Salva**

### Esportazione di dati personalizzati
{: #export-custom-data}

Puoi esportare i dati da ciascun grafico personalizzato in formato JSON, XML o CSV.

La struttura dei dati esportati dipende dal grafico in fase di esportazione. Per esportare i dati, fai clic sull'icona di esportazione nell'angolo superiore destro del grafico personalizzato.



### Esportazione ed importazione di definizioni di grafico personalizzato
{: #export-import-custom}

Puoi importare ed esportare definizioni di grafico personalizzato in modo programmatico oppure manualmente nel dashboard {{site.data.keyword.mobileanalytics_short}}.

Accertati di disporre di almeno un grafico personalizzato nel dashboard {{site.data.keyword.mobileanalytics_short}}.
In questo esempio, esporti ed importi manualmente delle definizioni di grafico personalizzate.

1. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic sulla scheda **Grafici personalizzati** nella pagina **Dashboard**.
2. Per esportare le definizioni di grafico personalizzato, fai clic su **Esporta grafici**. Questa azione visualizza
una finestra di dialogo per salvare un file `customChartsDefinition.json`.
3. Scegli un'ubicazione per salvare il file.
4. Fai clic sull'icona **Elimina grafico** accanto a ciascun grafico personalizzato per eliminare tutti i grafici personalizzati.
5. Per importare una definizione di grafico personalizzato, fai clic su **Importa grafici**. Questa azione visualizza una finestra di dialogo per scegliere un file.
6. Scegli il file `customChartsDefinition.json` da te precedentemente esportato da aprire.

Puoi anche esportare e importare definizioni di grafico personalizzato in modo programmatico utilizzando il client HTTP che preferisci (ad esempio CURL o postman):
* L'endpoint GET per l'esportazione è `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* L'endpoint POST per l'importazione è `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Nota:**: se importi una definizione di grafico personalizzato esistente, finisci con il duplicare delle definizioni, il che significa anche che il
dashboard {{site.data.keyword.mobileanalytics_short}} mostra dei grafici personalizzati duplicati.

## Impostazione di avvisi
{: #alerts}

Puoi impostare delle soglie nelle definizioni di avviso nella console {{site.data.keyword.mobileanalytics_short}} per monitorare meglio le tue attività.

Puoi configurare delle soglie che, se vengono superate, attivano degli avvisi di segnalazione al monitoraggio della console {{site.data.keyword.mobileanalytics_short}}. Gli avvisi attivati possono essere visualizzati sulla console oppure gli avvisi possono essere gestiti da un webhook personalizzato. Questa funzione fornisce un modo proattivo per rilevare gli errori log client e log server, i periodi estesi di latenza di rete e i malfunzionamenti dell'autenticazione. Delle soglie e degli avvisi reattivi ti evitano di dover esaminare accuratamente i tuoi dati e impostare delle soglie a un ampio spettro di granularità.

### Creazione di una definizione di avviso per i log client
{: #alert-def-client-logs}

Puoi creare una definizione di avviso basata sui log client.

In questo esempio, utilizzi i dati di log client per creare una definizione di avviso. L'avviso monitora tutti i log client ricevuti negli ultimi 5 minuti e continua a controllare ogni 5 minuti, finché la definizione di avviso non viene disabilitata o eliminata. Un avviso viene attivato per ciascun dispositivo che ha inviato 3 o più log di errori client con gli stessi nome applicazione e versione.

1. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic sull'icona a forma di campana per andare alla pagina **Log avvisi**.
2. Vai alla pagina **Gestione avvisi** e fai clic su **Crea avviso**.
3. Fornisci i seguenti valori:
	* Nome avviso: Avviso per i log client
	* messaggio: Avviso di messaggio di errore
	* Frequenza query: 5 minuti
	* Tipo di evento: Log client
		* Proprietà: Livello di log
			* Valore: Errore
			* Soglia
				* Tipo di soglia: Totale per l'istanza dell'applicazione

					**Nota**: se scegli l'opzione Media per applicazione, per i log client viene calcolata la media in base al numero di dispositivi. Ad esempio, se hai due dispositivi, e un dispositivo invia sei log client mentre l'altro ne invia tre, la media è 4,5 log client.
				* Operatore: è maggiore di o uguale a 3
	<!-- insert alert definition tab image? -->

4. Fai clic su **Avanti** o sulla scheda **Metodo di distribuzione** e fornisci il seguente valore:
	* Metodo: Solo console Analytics

		Nota: scegli l'opzione Console Analytics e POST di rete se desideri inviare anche un messaggio POST con un payload JSON al tuo URL personalizzato. Se scegli questa opzione, sono disponibili i seguenti campi:
		* URL POST di rete
        * Intestazioni
        * Tipo di autenticazione
5. Fai clic su **Salva**.

Hai creato una definizione di avviso per attivare un avviso alla fine di ogni intervallo di 5 minuti se il numero di log client ha raggiunto la tua soglia di 3 o più log di errori.

### Creazione di una definizione di avviso per gli arresti anomali delle applicazioni
{: #alert-def-app-crash}

Puoi creare una definizione di avviso basata sugli arresti anomali delle applicazioni.

In questo esempio, utilizzi i dati relativi agli arresti anomali delle applicazioni per creare una definizione di avviso. L'avviso monitora tutti gli arresti anomali di applicazioni negli ultimi 2 minuti e continua a controllare ogni 2 minuti finché la definizione di avviso non viene disabilitata o eliminata. Un avviso viene attivato per ogni applicazione per cui si è verificato un
arresto anomalo 5 o più volte. Per ulteriori informazioni sugli arresti anomali delle applicazioni, vedi [Arresti anomali delle applicazioni](app_crash/c_op_analytics_crashes.html).

1. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic sull'icona **Avvisi**. Questa azione visualizza la pagina Log avvisi.
2. Fai clic sulla scheda **Gestione avvisi** e fai clic su **Crea avviso**.
3. Fornisci i seguenti valori:
	* Nome avviso: Avviso per arresti anomali delle applicazioni
	* Messaggio: Avviso di arresto anomalo dell'applicazione
	* Frequenza query: Arresti anomali dell'applicazione
		* Nome applicazione: Qualsiasi applicazione
		* Versione applicazione: Qualsiasi versione
    * Soglia
      * Tipo di soglia: Conteggio arresti anomali
      * Operatore: è maggiore di o uguale a 5
4. Fai clic sulla scheda **Metodo di distribuzione** e fornisci il seguente valore:
  * Metodo: Solo console Analytics

    **Nota**: scegli l'opzione **Console Analytics e POST di rete** se desideri inviare anche un messaggio POST con un payload JSON al tuo URL personalizzato. Se scegli questa opzione, sono disponibili i seguenti campi:
      * URL POST di rete (obbligatorio)
      * Intestazioni (facoltativo)
      * Tipo di autenticazione (obbligatorio)
5. Fai clic su **Salva**.

### Gestione delle definizioni di avviso
{: #managing-alert-definitions}

In questo esempio, gestisci le definizioni di avviso dalla pagina Gestione avvisi.

1. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic sull'icona **Avvisi**. Questa azione apre la pagina Log avvisi.
2. Fai clic sulla scheda **Gestione avvisi**.
3. Facoltativo: attiva/disattiva la casella di spunta sotto la colonna **Abilitato** per abilitare o disabilitare una specifica definizione di avviso.
4. Facoltativo: fai clic sull'icona **Duplica** se vuoi creare una copia di una definizione di avviso e modificare qualche valore.
5. Facoltativo: fai clic sull'icona che rappresenta una **matita** se vuoi modificare una definizione di avviso.
6. Facoltativo: fai clic sull'icona che rappresenta un **cestino** se vuoi eliminare una definizione di avviso.

### Visualizzazione di dettagli dell'avviso
{: #viewing-alert-details}

In questo esempio, visualizzi i dettagli dei tuoi avvisi attivati dalla pagina Log avvisi.

1. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic sull'icona **Avvisi**. Questa azione visualizza la pagina Log avvisi.
2. Fai clic sull'icona **+** per uno qualsiasi degli avvisi. Questa azione visualizza le sezioni **Definizione di avviso** e **Istanze avviso**.

    **Nota**: se la definizione di avviso corrispondente non era stata eliminata o modificata, puoi modificare la definizione di avviso
facendo clic su **Modifica avviso**. Altrimenti, il pulsante **Modifica avviso** non è disponibile e viene visualizzato il seguente messaggio:

    `This alert definition has since been modified or deleted.`

3. Facoltativo: seleziona un avviso e fai clic sull'icona che rappresenta un **cestino** per eliminare l'avviso.

## Arresti anomali delle applicazioni
{: #monitor-app-crash}

Puoi visualizzare le informazioni sugli arresti anomali delle tue applicazioni nella console {{site.data.keyword.mobileanalytics_short}} per monitorare meglio e risolvere più facilmente i problemi delle tue applicazioni.

### Monitoraggio degli arresti anomali delle applicazioni
{: #app-crash}

Puoi visualizzare rapidamente le informazioni sugli arresti anomali delle tue applicazioni nella sezione **Dashboard** della console {{site.data.keyword.mobileanalytics_short}}.

Nella pagina **Panoramica** della sezione **Dashboard**, il grafico a barre **Arresti anomali** mostra un istogramma degli arresti anomali nel corso del tempo.

Puoi visualizzare i dati in due modi:

1. Visualizza frequenza arresti anomali: frequenza degli arresti anomali nel tempo
2. Visualizza totale arresti anomali: totale arresti anomali nel tempo


### Risoluzione dei problemi di arresto anomalo delle applicazioni
{: #app-crash-troubleshooting}

Puoi visualizzare la pagina **Arresti anomali** nella sezione **Applicazioni** della console {{site.data.keyword.mobileanalytics_short}} per amministrare meglio le tue applicazioni.

La tabella **Panoramica arresti anomali** mostra le seguenti colonne di dati:

* Applicazione: nome applicazione
* Arresti anomali: il numero totale di arresti anomali per l'applicazione
* Totale utilizzi: il numero di volte per cui un utente apre e chiude l'applicazione
* Frequenza di arresti anomali: percentuale di arresti anomali per utilizzo

La tabella **Riepilogo arresti anomali** è ordinabile e include le seguenti colonne di dati:

* Arresti anomali
* Dispositivi
* Ultimo arresto anomalo
* Applicazione
* Sistema operativo
* Messaggio

Puoi fare clic sull'icona + accanto a qualsiasi voce per visualizzare la tabella **Dettagli dell'arresto anomalo**, che include le seguenti colonne:

* Data/ora arresto anomalo
* Versione applicazione
* Versione sistema operativo
* Modello dispositivo
* ID dispositivo
* Download: link per scaricare i log che portavano all'arresto anomalo

Puoi espandere qualsiasi voce nella tabella **Dettagli dell'arresto anomalo** per ottenere ulteriori dettagli, compresa una traccia di stack.

**Nota:**: i dati per la tabella **Riepilogo dell'arresto anomalo** viene compilata eseguendo delle query dei log client a livello di errore irreversibile. Se la tua applicazione non raccoglie i log client a livello di errore irreversibile, non è disponibile alcun dato.


