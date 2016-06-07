---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Informazioni su Insights for Weather
{: #about_weather}

*Ultimo aggiornamento: 19 maggio 2016*

Utilizza {{site.data.keyword.weatherfull}} per incorporare i dati meteo da
The Weather Company (TWC) nelle tue applicazioni {{site.data.keyword.Bluemix}}.
{:shortdesc}

Puoi aggiungere osservazioni e previsioni sul meteo alla tua applicazione {{site.data.keyword.Bluemix_notm}} e visualizzare i dati meteo
per un'area specificata da una georilevazione utilizzando le [API REST Insights for Weather](https://twcservice.{APPDomain}/rest-api/){:new_window}.
La Weather Company è il provider più completo di dati meteo
di previsioni e cronologici. Vengono catturati dati per tutte le forme meteo, precipitazioni, pressione barometrica, vento e
temporali.

Puoi utilizzare le API REST per richiamare le seguenti informazioni:

* Una previsione meteo oraria per le prossime 24 ore che si avvia nel momento in cui viene specificata una georilevazione.
* Una previsione meteo giornaliera per i prossimi 10 giorni che include le previsioni per i segmenti giorno e notte per una georilevazione specificata. Questa previsione include la stringa di testo descrittivo della previsione fino a 256 caratteri con le appropriate unità di misura per l'ubicazione e nella lingua richiesta.
* I dati meteo osservati correntemente per la georilevazione specificata. Questi dati meteo includono temperatura, precipitazioni, direzione e velocità del vento, umidità, pressione barometrica, punto di condensazione, visibilità e radiazioni ultraviolette (UV).
* I dati meteo osservati per una georilevazione e un intervallo di tempo specificati. Questi dati sono originati dalle stazioni di osservazione fisiche. Questa API restituisce le osservazioni per le condizioni correnti e le osservazioni passate fino ad includere le precedenti 24 ore.

Per ulteriori informazioni sulle icone e frasi meteo di The Weather Company, consulta [Icon Code, Phrases and Images](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window}.
Puoi inoltre [scaricare una serie di icone](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} da utilizzare nella tua applicazione.

## Modello di prezzi
{: #pricing_models}

Il modello di prezzi si basa su chiamate giornaliere alle API di Insights for Weather
che vengono addebitate al cliente mensilmente. Puoi verificare i dati meteo nella tua applicazione
per ogni area geografica, tipo di previsione o osservazioni di serie temporali con solo una
restrizione sul numero di chiamate. I piani Gratuito, Di base e Premium possono essere acquistati
senza un contratto. Questi piani consentono alla tua applicazione di effettuare rispettivamente 500, 5,000 o 50,000 chiamate API al giorno.

Possono inoltre essere acquistati i piani Multiple Premium per ogni istanza di servizio
distribuita durante il periodo di fatturazione. Se la tua applicazione utilizza più di 50,000 chiamate al giorno
o più di 1,000 chiamate al minuto, avrai bisogno di un contratto con IBM per il provisioning in uscita dei servizi.

Quando la tua applicazione raggiunge il limite consentito di chiamate API, in base al piano che hai selezionato,
la successiva chiamata API effettuata non andrà a buon fine
finché alla tua applicazione non sarà consentito di richiedere ulteriori chiamate API.

Ad esempio, se stai utilizzando il piano Di base, la tua applicazione può effettuare 500 chiamate API
in un minuto anche se supera il limite del piano, ma la successiva chiamata API
non sarà consentita nei successivi 5 minuti. Pertanto, l'utente potrebbe riscontrare un ritardo nell'aggiornamento
dei dati meteo nella propria applicazione. Devi assicurarti di sviluppare la tua applicazione in modo da
gestire questi limiti e non richiedere una raffica di chiamate API. Invece, puoi monitorare
l'utilizzo della chiamata API della tua applicazione. Puoi verificare se la tua applicazione raggiunge il limite
del suo piano controllando il numero di elementi restituiti dalla chiamata API.

## Feedback e supporto
{: #feedback_support}

Se hai domande tecniche sulla creazione di un'applicazione con Insights for Weather,
invia la tua domanda a [Stack Overflow](http://stackoverflow.com/search?q=weather+bluemix){:new_window}
 e contrassegna la tua domanda con **bluemix** e **weather**.

Se stai riscontrando dei problemi con questo servizio, utilizza il [IBM developerWorks Answers forum](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}.
Includi le tag **insights-weather** e **bluemix** per consentire a IBM di aiutarti nel miglior modo.

Per informazioni sulla risoluzione dei problemi con Bluemix, vedi [Risoluzione dei problemi](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
Per informazioni dettagliate su come cercare informazioni e fare domande tramite i forum e su come contattare l'assistenza, vedi [Richiesta di assistenza clienti](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}.
