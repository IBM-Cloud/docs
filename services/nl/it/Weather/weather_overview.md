---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Informazioni su {{site.data.keyword.weather_short}}
{: #about_weather}

*Ultimo aggiornamento: 01 luglio 2016*
{: .last-updated}

Utilizza {{site.data.keyword.weatherfull}} per incorporare i dati meteo da
The Weather Company (TWC) nelle tue applicazioni {{site.data.keyword.Bluemix}}.
{:shortdesc}

Puoi aggiungere osservazioni e previsioni sul meteo alla tua applicazione {{site.data.keyword.Bluemix_notm}} e visualizzare i dati meteo
per un'area specificata da una georilevazione utilizzando le [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window}.
La Weather Company è il provider più completo di dati meteo
di previsioni e cronologici. Vengono catturati dati per tutte le forme meteo, precipitazioni, pressione barometrica, vento e
temporali.

Puoi utilizzare le API REST per richiamare le seguenti informazioni:

* Una previsione meteorologica oraria per le successive 48 ore a partire dall'ora corrente, per una geoposizione specificata.
* Una previsione giornaliera per ognuno dei successivi 3, 5, 7 o 10 giorni a partire dal giorno corrente, incluse le previsioni per i segmenti diurno e notturno per una georilevazione specificata. Questa previsione include la stringa di testo descrittivo della previsione fino a 256 caratteri con le appropriate unità di misura per l'ubicazione e nella lingua richiesta.
* Una previsione giornaliera per ognuno dei successivi 3, 5, 7 o 10 giorni a partire dal giorno corrente, che divide ogni previsione giornaliera in segmenti per la mattina, il pomeriggio, la sera e la notte.
* I dati meteo osservati correntemente per la georilevazione specificata. Questi dati meteo includono temperatura, precipitazioni, direzione e velocità del vento, umidità, pressione barometrica, punto di condensazione, visibilità e radiazioni ultraviolette (UV).
* I dati meteo osservati per una georilevazione specificata fino ad includere le precedenti 24 ore. Questi dati sono originati dalle stazioni di osservazione fisiche.
* Gli avvisi meteo emessi dal governo, incluse le osservazioni meteo, le avvertenze, le istruzioni e gli avvertimenti emessi dal National Weather Service (US), Environment Canada e MeteoAlarm (Europa).
* I servizi astronomici che forniscono dati meteo giornalieri e mensili cronologici originati dalle stazioni di osservazione del National Weather Service per un periodo di tempo compreso tra 10 e 30 anni o più.
* I servizi di associazione dell'ubicazione che forniscono la capacità di ricercare un nome ubicazione o un codice geografico (latitudine e longitudine) per richiamare una serie di ubicazioni che corrispondono alla tua richiesta.

Puoi [scaricare una serie di icone](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} da utilizzare nella tua applicazione.

## Modello di prezzi
{: #pricing_models}

Il modello dei prezzi si basa sul numero di chiamate al minuto delle API
REST. L'addebito al client viene eseguito mensilmente. I piani Gratuito e Di base ti consentono
di effettuare un massimo di 10 chiamate API al minuto. I piani Standard e Premium di consentono di effettuare
rispettivamente 150 e 375 chiamate API al minuto. Ogni piano dispone di un numero di chiamate API
consentito.

Puoi verificare i dati meteo nella tua applicazione
per ogni area geografica, tipo di previsione o osservazioni di serie temporali con solo una
restrizione sul numero di chiamate. I piani Gratuito, Di base, Standard e Premium possono essere acquistati
senza un contratto. Il piano Gratuito consente alla tua applicazione di effettuare 1.000 chiamate. I piani
rimanenti consentono alla tua applicazione di effettuare rispettivamente 150.000, 2 milioni
o 5 milioni di chiamate API al mese.

Possono inoltre essere acquistati più piani a pagamento per ogni istanza di servizio
distribuita durante il periodo di fatturazione. Se la tua applicazione utilizza più di 10.000 chiamate,
è necessario stipulare un contratto con IBM per la fornitura continua di servizi.

Quando la tua applicazione raggiunge il limite consentito di chiamate API al minuto, in base al piano che hai selezionato,
la successiva chiamata API effettuata non andrà a buon fine
finché alla tua applicazione non sarà consentito di richiedere ulteriori chiamate API.

Ad esempio, se stai utilizzando il piano Standard, la tua applicazione *può*  effettuare 500 chiamate API
in un minuto anche se supera il limite del piano (150 chiamate al minuto), ma la successiva chiamata API
non sarà consentita nei successivi 5 minuti. Pertanto, l'utente potrebbe riscontrare un ritardo nell'aggiornamento
dei dati meteo nella propria applicazione.
Devi assicurarti di sviluppare la tua applicazione in modo da
gestire questi limiti e non richiedere una raffica di chiamate API. Invece, puoi monitorare
l'utilizzo della chiamata API della tua applicazione.
Puoi verificare se la tua applicazione raggiunge il limite
del suo piano controllando il numero di elementi restituiti dalla chiamata API.

Quando la tua applicazione raggiunge il limite consentito di chiamate API al mese, in base al piano che hai selezionato,
alla successiva chiamata API effettuata sarà addebitata una tariffa generale di
$1.70 per 10.000 chiamate API.

## Feedback e supporto
{: #feedback_support}

In caso di domande tecniche sulla creazione di una applicazione con {{site.data.keyword.weather_short}}, pubblicare
la domanda in [Stack
Overflow](https://stackoverflow.com/questions/tagged/ibm-bluemix+weather){:new_window} e aggiungere i tag ibm-bluemix e
**weather**. 

Se stai riscontrando dei problemi con questo servizio, utilizza il [IBM developerWorks Answers forum](https://developer.ibm.com/answers/topics/weather/?smartspace=bluemix){:new_window}.
Includi le tag **bluemix** e **weather** per permettere a IBM di fornire un migliore supporto.

Se hai domande sulla migrazione della tua applicazione da Insights for Weather a {{site.data.keyword.weather_short}},
contattaci all'indirizzo [IBM developerWorks](http://www.ibm.com/developerworks){:new_window}.

Per informazioni sulla risoluzione di problemi con Bluemix, consulta [Risoluzione dei problemi](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
Per i dettagli sulla ricerca di informazioni e le domande nei forum e su come contattare il supporto, consulta [Richiesta di assistenza clienti](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}.
