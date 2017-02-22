---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Monitoraggio delle applicazioni con {{site.data.keyword.mobileanalytics_short}} 
{: #monitoringapps}

{{site.data.keyword.mobileanalytics_full}} fornisce il monitoraggio e l'analisi per le tue applicazioni mobili. Puoi registrare i log applicazione e monitorare i dati con l'SDK client {{site.data.keyword.mobileanalytics_short}}. Gli sviluppatori possono controllare quando inviare questi dati al
servizio {{site.data.keyword.mobileanalytics_short}}. Quando i dati vengono distribuiti a {{site.data.keyword.mobileanalytics_short}}, puoi utilizzare la console {{site.data.keyword.mobileanalytics_short}} per ottenere delle approfondite informazioni di analisi delle applicazioni mobili, dei dispositivi e dei log applicazione.
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for app logs
{: #custom-charts-client-logs}

You can create a custom chart for app logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use app log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

* Specific data
  * Log level
* Message data
  * Timestamp
* Device OS contextual data
  * Application name
  * Application version
  * Device OS
* Device contextual data
  * Device ID
  * Device model
  * Device OS version


1. Make sure that you have an application that is collecting device logs or gathering analytics.
2. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab on the **Dashboard** page. You can create a chart that is based on the analytics messages that were sent to the server.
3. Click **Create Chart** to create a new custom chart and provide the following values:
  * Chart Title: Application and Log Levels
  * Event Type: App Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your application name
7. Click **Save**

### Exporting custom data
{: #export-custom-data}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom}

You can import and export custom chart definitions programmatically or manually in the {{site.data.keyword.mobileanalytics_short}} Dashboard.

Ensure that you have at least one custom chart in the {{site.data.keyword.mobileanalytics_short}} Dashboard.
In this example, you manually export and import custom chart definitions.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab in the **Dashboard** page.
2. To export the custom chart definitions, click **Export Charts**. This action displays a dialog to save a `customChartsDefinition.json` file.
3. Choose a location to save the file.
4. Click the **Delete Chart** icon next to each custom chart to delete all custom charts.
5. To import a custom chart definition, click **Import Charts**. This action displays a dialog to choose a file.
6. Choose the `customChartsDefinition.json` file that you previously exported to open.

You can also export and import custom chart definitions programmatically by using your HTTP client of choice (for example, CURL or postman):
* The GET endpoint for export is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* The POST endpoint for import is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Note**: If you import a custom chart definition that exists, you end up with duplicate definitions, which also means that the {{site.data.keyword.mobileanalytics_short}} Dashboard shows duplicate custom charts.

-->

## Impostazione di avvisi
{: #alerts}

Puoi impostare delle soglie nelle definizioni di avviso nella console {{site.data.keyword.mobileanalytics_short}} per monitorare meglio le tue attività. 

Puoi configurare delle soglie che, se vengono superate, attivano degli avvisi di segnalazione al monitoraggio della console {{site.data.keyword.mobileanalytics_short}}. Gli avvisi attivati possono essere visualizzati sulla console oppure gli avvisi possono essere gestiti da webhook personalizzato. <!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.--> Questa funzione fornisce un modo proattivo per rilevare gli errori log applicazione, gli arresti anomali dell'applicazione e gli errori di log server. Delle soglie e degli avvisi reattivi ti evitano di dover esaminare accuratamente i tuoi dati e impostare delle soglie a un ampio spettro di granularità.

### Creazione di una definizione di avviso per i log applicazione 
{: #alert-def-client-logs}

Puoi creare una definizione di avviso basata sui log applicazione. 

In questo esempio, utilizzi i dati di log applicazione per creare una definizione di avviso. L'avviso monitora tutti i log applicazione ricevuti negli ultimi 5 minuti e continua a controllare ogni 5 minuti, finché la definizione di avviso non viene disabilitata o eliminata. Un avviso viene attivato per ciascun dispositivo che ha inviato 3 o più log di errori applicazione con gli stessi nome applicazione e versione. 

1. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic su **Definizioni** per andare alla pagina delle definizioni di avviso. 
2. Fai clic su **Crea avviso** per creare un avviso.
3. Fornisci i seguenti valori:
	* Nome avviso: Avviso per i log applicazione
	* messaggio: Avviso di messaggio di errore
	* Frequenza query: 5 minuti
	* Tipo di evento: Log applicazione 
		* Proprietà: Livello di log
			* Valore: Errore
			* Soglia
				* Tipo di soglia: Totale per l'istanza dell'applicazione

					**Nota**: se scegli l'opzione Media per applicazione, per i log applicazione viene calcolata la media in base al numero di dispositivi. Ad esempio, se hai due dispositivi, e un dispositivo invia sei log applicazione mentre l'altro ne invia tre, la media è 4,5 log applicazione. 
				* Operatore: è maggiore di o uguale a 3
	<!-- insert alert definition tab image? -->

4. Fai clic su **Avanti** e fornisci il seguente valore:
	* Metodo: Solo console Analytics

		**Nota**: scegli l'opzione Console Analytics e POST di rete se desideri inviare anche un messaggio POST con un payload JSON al tuo URL personalizzato. Se scegli questa opzione, sono disponibili i seguenti campi:
		* URL POST di rete
        * Intestazioni
        * Tipo di autenticazione
5. Fai clic su **Salva**.

Hai creato una definizione di avviso per attivare un avviso alla fine di ogni intervallo di 5 minuti se il numero di log applicazione ha raggiunto la tua soglia di 3 o più log di errori.

### Creazione di una definizione di avviso per gli arresti anomali delle applicazioni 
{: #alert-def-app-crash}

Puoi creare una definizione di avviso basata sugli arresti anomali delle applicazioni. 

In questo esempio, utilizzi i dati relativi agli arresti anomali delle applicazioni per creare una definizione di avviso. L'avviso monitora tutti gli arresti anomali di applicazioni negli ultimi 2 minuti e continua a controllare ogni 2 minuti finché la definizione di avviso non viene disabilitata o eliminata. Un avviso viene attivato per ogni applicazione per cui si è verificato un arresto anomalo 5 o più volte. Per ulteriori informazioni sugli arresti anomali delle applicazioni, vedi [Arresti anomali delle applicazioni](#app_crash). 

1. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic su **Definizioni** per visualizzare la pagina delle definizioni dell'avviso. 
2. Fai clic su **Crea avviso**.
3. Fornisci i seguenti valori:
	* Nome avviso: Avviso per arresti anomali delle applicazioni 
	* Messaggio: Avviso di arresto anomalo dell'applicazione
	* Frequenza query: Arresti anomali dell'applicazione
		* Frequenza query: 2 minuti
	* Tipo di evento: Arresti anomali dell'applicazione
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

1. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic su **Log**. Questa azione apre la pagina Log avvisi.
2. Facoltativo: attiva/disattiva la casella di spunta sotto la colonna **Abilitato** per abilitare o disabilitare una specifica definizione di avviso.
3. Facoltativo: fai clic sull'icona **Duplica** se vuoi creare una copia di una definizione di avviso e modificare qualche valore.
4. Facoltativo: fai clic sull'icona che rappresenta una **matita** se vuoi modificare una definizione di avviso.
5. Facoltativo: fai clic sull'icona che rappresenta un **cestino** se vuoi eliminare una definizione di avviso.

### Visualizzazione di dettagli dell'avviso
{: #viewing-alert-details}

In questo esempio, visualizzi i dettagli dei tuoi avvisi attivati dalla pagina Log avvisi.

1. Nella console {{site.data.keyword.mobileanalytics_short}}, fai clic su **Log**. Questa azione visualizza la pagina Log avvisi.
2. Fai clic sull'icona **+** per uno qualsiasi degli avvisi. Questa azione visualizza le sezioni **Definizione di avviso** e **Istanze avviso**.

    **Nota**: se la definizione di avviso corrispondente non era stata eliminata o modificata, puoi modificare la definizione di avviso
facendo clic su **Modifica avviso**. Altrimenti, il pulsante **Modifica avviso** non è disponibile e viene visualizzato il seguente messaggio:

    `This alert definition has since been modified or deleted.`

3. Facoltativo: seleziona un avviso e fai clic sull'icona che rappresenta un **cestino** per eliminare l'avviso.

## Monitoraggio degli arresti anomali delle applicazioni 
{: #monitor-app-crash}

Puoi visualizzare le informazioni sugli arresti anomali delle tue applicazioni nella console {{site.data.keyword.mobileanalytics_short}} per monitorare meglio e risolvere più facilmente i problemi delle tue applicazioni. 

### Monitoraggio degli arresti anomali delle applicazioni 
{: #app-crash}

Nella pagina **Arresti anomali**, la tabella **Panoramica arresti anomali** mostra le seguenti colonne di dati:

* Applicazione: il nome dell'applicazione
* Arresti anomali: il numero totale di arresti anomali per l'applicazione
* Totale utilizzi: il numero di volte per cui un utente apre e chiude l'applicazione
* Frequenza di arresti anomali: percentuale di arresti anomali per utilizzo

Puoi visualizzare rapidamente le informazioni sugli arresti anomali delle tue applicazioni nella tabella **Arresti anomali**. <!--In the **Overview** page of the **Dashboard** section,--> Il grafico a barre **Arresti anomali** visualizza un istogramma degli arresti anomali nel tempo.

Puoi visualizzare i dati relativi agli arresti anomali in due modi: 

1. Visualizza frequenza arresti anomali: frequenza degli arresti anomali nel tempo
2. Visualizza totale arresti anomali: totale arresti anomali nel tempo

### Risoluzione dei problemi di arresto anomalo delle applicazioni
{: #app-crash-troubleshooting}

La pagina **Risoluzione dei problemi** nella console <!-- **Applications** section of the --> {{site.data.keyword.mobileanalytics_short}} offre una vista granulare degli arresti anomali della tua applicazione, utilizzando la tabella **Riepilogo arresti anomali**.

La tabella **Riepilogo arresti anomali** è ordinabile e include le seguenti colonne di dati:

* Arresti anomali
* Dispositivi
* Ultimo arresto anomalo
* Applicazione
* Sistema operativo
* Messaggio

Fai clic sull'icona + accanto a qualsiasi voce per visualizzare la tabella **Dettagli dell'arresto anomalo**, che include le seguenti colonne: 

* Data/ora arresto anomalo
* Versione applicazione 
* Versione sistema operativo
* Modello dispositivo
* ID dispositivo
* Download: link per scaricare i log che portavano all'arresto anomalo

Espandi qualsiasi voce nella tabella **Dettagli dell'arresto anomalo** per ottenere ulteriori dettagli, compresa una traccia di stack. 

**Nota:**: i dati per la tabella **Riepilogo dell'arresto anomalo** viene compilata eseguendo delle query dei log applicazione a livello di errore irreversibile. Se la tua applicazione non raccoglie i log applicazione a livello di errore irreversibile, non è disponibile alcun dato. 

## Monitoraggio delle richieste di rete
{: #monitor-network-requests}


Visualizza i dati della richiesta di rete per le tue applicazioni nella console {{site.data.keyword.mobileanalytics_short}}.  

I dati sono disponibili per le seguenti misurazioni:
	
* Tempo di round trip - definisce la durata, misurata in ms, che la tua applicazione impiega ad effettuare richieste di rete.
* Conteggio richiesta - visualizza quando spesso un'applicazione effettua richieste di rete. I dati sono anche visualizzati come una media.

## Esportazione dei dati a dashDB
{: #dashdb}

Le metriche che visualizzi nella console {{site.data.keyword.mobileanalytics_short}} sono soltanto un esempio delle informazioni approfondite che puoi raccogliere dai dati del dispositivo mobile. Puoi automaticamente passare i dati del dispositivo mobile al data warehouse dashDB {{site.data.keyword.IBM}}, dove puoi personalizzare le tue analisi, aggregare i tuoi dati con altre origini dati pubbliche e private e applicare le analisi edge principali per ottenere informazioni approfondite, dettagliate e sofisticate per aiutarti nella comprensione e la gestione del tuo business.

Configura dashDB nella console {{site.data.keyword.mobileanalytics_short}} facendo clic su **DashDB** nella pagina **Esportazione**. Dopo aver completato la configurazione, i nuovi dati vengono inviati a {{site.data.keyword.mobileanalytics_short}} e anche inoltrati a dashDB in 1-2 ore. 

<!--
If you have existing DashDB instances, those instances will no longer accept new data because the incoming data no longer matches the schema. Manually add columns for the new data to resume incoming data. Modifying {{site.data.keyword.mobileanalytics_short}} collection tables by adding new columns also breaks the stream of incoming data.
-->

