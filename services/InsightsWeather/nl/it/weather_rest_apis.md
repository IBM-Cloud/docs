---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilizzo delle API REST di Insights for Weather
{: #rest_apis}

Puoi utilizzare le [API REST di Insights for Weather](https://twcservice.{APPDomain}/rest-api-deprecated/){:new_window}
per richiamare i dati meteo. Puoi verificare le operazioni API e istantaneamente visualizzare i risultati per aiutarti nella generazione delle tue applicazioni più velocemente.

Dalla documentazione di riferimento, fai clic su **Elenco operazioni** per visualizzare i dettagli per ogni operazione.
Quando specifichi i parametri fai clic su **Provalo**, ti potrebbe essere richiesto di fornire le credenziali.
Devi fornire il nome utente e la password dalle tue variabili di ambiente `VCAP_SERVICES`.
Puoi trovare queste informazioni aprendo la tua applicazione e facendo clic su **Variabili di ambiente** dalla tabella dei contenuti.

**Nota:** ogni regione è indipendente. Non puoi utilizzare le credenziali di servizio
che ti sono state fornite in una regione per autenticarti a un servizio in un'altra regione.
La mancata immissione delle credenziali corrette comporterà il ricevimento di un messaggio "Non autorizzato" nel corpo della risposta.

Con le API di Insights for Weather, puoi richiamare i dati meteo fornendo una georilevazione come ad esempio le coordinate di latitudine e longitudine.
Puoi utilizzare le seguenti API.

|**API**                                  |**Descrizione**              |
|-----------------------------------------|-----------------------------|
|`GET /v2/forecast/daily/10day`           |Restituisce le previsioni meteo per il giorno corrente e i successivi 9 giorni per una georilevazione. Ogni previsione giornaliera può contenere una previsione per il giorno e una per la notte. Questi segmenti sono oggetti separati nelle risposte JSON. I dati di previsione per il giorno di una previsione giornaliera non sono più disponibili dopo le 15:00 dell'ora locale. Alle 15:00 ora locale, la tua applicazione non visualizzerà più i dati per la previsione per il giorno.|
|`GET /v2/forecast/hourly/24hour`         |Restituisce una previsione oraria per il giorno corrente e le successive 24 ore per una georilevazione. I dati di previsione oraria possono contenere fino a 24 previsioni orarie per ogni ubicazione. Devi scartare tutte le previsioni orarie precedenti per un'ubicazione quando vengono ricevuti i nuovi dati.|
|`GET /v2/observations/current`           |Restituisce le condizioni meteo per una georilevazione. Queste osservazioni recenti vengono conservate nel database fino a 10 minuti per le stazioni di segnalazione specifiche e per 24 ore di osservazioni a stazione. I dati sulle osservazioni recenti vengono costantemente aggiornati e sostituiti con una metodologia primo arrivato / primo eliminato (ruotando i dati con le osservazioni più recenti e spostando le più vecchie nella memoria di archiviazione) in base all'indicatore di data/ora delle osservazioni.|
|`GET /v2/observations/timeseries/24hour` |Restituisce le osservazioni correnti e fino a 24 ore di osservazioni passate, dalla data e ora correnti, per una georilevazione. Le osservazioni meteo vengono raccolte da periferiche fisiche ubicate globalmente e da osservazioni meteo correnti.|
*Tabella 1. Riepilogo API di Insights for Weather*

## Osservazioni di serie temporali
{: #time_series}

I dati delle osservazioni meteo di serie temporali forniscono informazioni su
temperatura. precipitazioni, vento, pressione barometrica, visibilità, radiazioni ultraviolette (UV)
e altri elementi di osservazione, inclusi la stazione di osservazione,
la data/ora di osservazione, i codici le frasi dell'icona meteo. La differenza tra
le osservazioni di serie temporali e le osservazioni correnti è il periodo di tempo dell'osservazione,
il cui risultato sono una o più serie di dati di osservazione.

Le condizioni correnti sono le osservazioni più recenti per l'ubicazione
richiesta senza un parametro di tempo. Viene restituita una serie di dati. Le osservazioni di serie temporali
includono le osservazioni passate verificatisi fino a quel momento e includono
le ultime 24 ore per l'ubicazione richiesta.

Le osservazioni recenti vengono conservate nel database principale fino a 48 ore (2 giorni)
sulle stazioni di segnalazione specifiche. I dati sulle osservazioni recenti vengono costantemente aggiornati
con una metodologia primo arrivato/primo eliminato (ruotando i dati con
le osservazioni più recenti e spostando le più vecchie nella memoria di archiviazione)
in base all'indicatore di data/ora delle osservazioni. La quantità di dati conservata e disponibile da ogni
stazione può essere maggiore di 24
report di osservazione individuali. Il numero di osservazioni è determinato
dal tipo di osservazione.

## Costruzione URL
{: #url_construction}

Le API di Insights for Weather utilizzano una struttura URL comune e i parametri di query per richiedere e filtrare i dati meteo.
Gli URL trasmessi alle API di Insights for Weather sono strutturati come segue:

```
https://twcservice.mybluemix.net/api/weather/v2/<product group>/&format={format type}&geocode={latitude,longitude}&language={language code}&units={units code}

```

|**Attributo**     |**Descrizione**                                    |
|------------------|---------------------------------------------------|
|`hostname`        |Il percorso URL ospitante (ad esempio, `https://twcservice.mybluemix.net:443/api/weather`)|
|`version`         |L'iterazione corrente (ad esempio, "v2")|
|`product group`   |Il prodotto (ad esempio, "observations" o "forecast")|
|`geocode`         |La latitudine o la longitudine facoltative, ad esempio, "45.4214,75.6919" rappresenta Ottawa, Canada. Se fornisci una coordinata di georilevazione, l'API restituisce i dati per l'ubicazione disponibile più vicina. I punti sono utilizzati come separatori decimali e le virgole sono utilizzate per separare i valori di latitudine e longitudine. Se fornisci un codice geografico, i valori di latitudine e longitudine attuali che stanno venendo utilizzati sono restituiti nei metadati della risposta.|
|`language`        |La lingua in cui restituire la risposta. L'impostazione predefinita è en-US. La lingua di traduzione richiesta o predefinita viene restituita nel parametro language nei metadati della risposta.|
|`units`           |Le unità di misura facoltative con cui restituire la risposta. L'API supporta le unità di misura English (e), Metric (m) e UK-Hybrid (h). Se fornisci le unità di misura ma non un valore, l'API restituisce i dati nell'unità di misura che corrisponde al codice della lingua. L'unità di misura richiesta o predefinita viene restituita nel parametro units nei metadati della risposta.|
*Tabella 2. Dettagli URL*

## Unità di misura
{: #units_measure}

Quando utilizzi le le API di Insights for Weather, non hai bisogno di trasmettere esplicitamente un'unità di misura. Le API di Insights for Weather utilizzano per impostazione predefinita l'unità di misura associata con il codice della lingua nell'URL. Tuttavia, se desideri fornire un'unità di misura diversa dalla predefinita, puoi passare a un'unità di misura che sovrascrive la predefinita.

* Per en-US o en, il codice di unità di misura predefinito è English/Imperial. Il codice di unità è "e".
* Per en-GB, l'unità di misura predefinita è Hybrid-UK. Il codice di unità è "h".
* Per tutte le altre, l'unità di misura predefinita è Metric. Il codice di unità è "m".

## Traduzione in un'altra lingua
{: #language_translation}

Le API di Insights for Weather traducono le frasi e le unità di misura. Quando crei una richiesta URL, devi fornire una lingua valida.
I seguenti campi sono tradotti:

|**Campo**           |**Descrizione**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |La previsione descrittiva per il periodo di 24 ore|
|`dow`               |Il giorno della settimana|
|`wind_phrase`       |La frase che descrive la direzione e la velocità del vento per una separazione giornaliera di 12 ore|
|`wdir_cardinal`     |La direzione del vento media giornaliera nell'annotazione cardinale|
|`daypart_name`      |Il nome della separazione giornaliera di 12 ore non includendo i nomi del giorno nelle prime 48 ore|
|`temp_phrase`       |La frase breve che contiene la più elevata o bassa temperatura prevista in un periodo di previsione di 12 ore|
|`shortcast`         |Una porzione meteo ponderata abbreviata della previsione descrittiva|
|`long_daypart_name` |L'intervallo di tempo denominato per la previsione meteo valida in un formato espanso. L'intervallo di tempo denominato può essere nei periodi di 12 o 24 ore.|
|`golf_category`     |La categoria di indice per il golf che viene espressa come un frase per le condizioni meteo per giocare a golf.|
|`phrase_nnchar`     |La frase meteo sensibile al giorno|
|`lunar_phrase`      |Un codice breve di tre caratteri per le fasi lunari|
|`uv_desc`           |La descrizione dell'indice UV, che completa il valore di indice UV fornendo un livello associato di rischio di danno alla pelle a causa dell'esposizione|
|`sky_cover`         | La copertura del cielo descrittiva in base alla percentuale di copertura delle nuvole|
|`ptend_desc`        | Il testo descrittivo della tendenza per la pressione nelle ultime 3 ore|
*Tabella 3. Campi di risposta tradotti*

## Gestione dei campi dati mancanti o null nella risposta API
{: #handling_null_or_missing}

Se un campo dati è null perché i dati non sono disponibili, le API di Insights for Weather restituiscono le tag del campo appropriate con la parola "null" o non restituiscono il campo affatto.

## Gestione errori
{: #handling_errors}

I seguenti codici di errore sono comuni per tutte le API:

|**Errore** |**Descrizione**                                    |
|----------|---------------------------------------------------|
|400       |Richiesta non valida. La richiesta non è comprensibile per il server a causa di una sintassi malformata. Questo codice di errore è implementato per tutte le API. L'API rifiuta la richiesta se vengono forniti dei parametri non validi.|
|401       |Non autorizzato. La richiesta richiede l'autenticazione.|
|403       |Non consentito. Il server comprende la richiesta ma si rifiuta di soddisfarla.|
|404       |Non trovato. Se un parametro obbligatorio non è presente nella richiesta API, viene restituito un errore MissingParameterException con un codice di errore 404.|
|405       |Metodo non consentito. Ad esempio, invio di un POST invece di un GET.|
|406       |Non accettabile. Ad esempio, non vengono accettate le risposte compresse gzip.|
|408       |Timeout della richiesta. Il client non produce la richiesta nell'intervallo in cui il server è disponibile per l'attesa.|
|500       |Errore server interno. Il server ha riscontro una condizione inattesa che gli impedisce di soddisfare la richiesta.|
|502-504   |Servizio non disponibile o problema con il gateway. Questi codici di errore vengono restituiti se il servizio è temporaneamente non disponibile.|
*Tabella 4. Codice di risposta di errore*

La risposta sull'errore è sempre la stessa. Più codici di errore possono essere restituiti in una risposta.
Ad esempio, un risposta di errore JSON potrebbe restituire quanto segue:

```
{
  metadata: {
    transaction_id: "1411496413365:-1880721071"
  },
  success: false,
  errors: [
    {
      error: {
        code: "NDF-0001",
        message: "There was no data found for your product query."
      }
    }
}
```
