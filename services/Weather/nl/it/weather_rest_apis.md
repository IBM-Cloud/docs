---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilizzo delle {{site.data.keyword.weather_short}} API REST
{: #rest_apis}

Puoi utilizzare le [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window}
per richiamare i dati meteo. Puoi verificare le operazioni API e istantaneamente visualizzare i risultati per aiutarti nella generazione delle tue applicazioni più velocemente.
{: shortdesc}

Dalla documentazione di riferimento, fai clic su **Elenco operazioni** per visualizzare i dettagli per ogni operazione.
Quando specifichi i parametri fai clic su **Provalo**, ti potrebbe essere richiesto di fornire le credenziali.
Devi fornire il nome utente e la password dalle tue variabili di ambiente `VCAP_SERVICES`.
Puoi trovare queste informazioni aprendo la tua applicazione e facendo clic su **Variabili di ambiente** dalla tabella dei contenuti.

**Nota:** ogni regione è indipendente. Non puoi utilizzare le credenziali di servizio
che ti sono state fornite in una regione per autenticarti a un servizio in un'altra regione.
La mancata immissione delle credenziali corrette comporterà il ricevimento di un messaggio *Non autorizzato* nel corpo della risposta.

Con le API REST, puoi richiamare i dati meteo fornendo una georilevazione come ad esempio le coordinate di latitudine e longitudine.
Puoi utilizzare le seguenti API.

|**API**                                  |**Descrizione**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location ID}/forecast/hourly/48hour.json`  |Restituisce una previsione meteo oraria per le successive 48 ore per una geoposizione in base al formato che hai fornito. Puoi fornire un `geocode/{latitude}/{longitude}` o una `location/{locationId}`. I dati di previsione oraria possono contenere previsioni fino a 48 ore per ogni ubicazione. È necessario eliminare tutte le precedenti previsioni orarie per un'ubicazione quando si ricevono i nuovi dati.|
|`GET /v1/{geocode or location ID}/forecast/daily/{format}.json`   |Restituisce le previsione meteo giornaliere per 3, 5, 7 o 10 giorni per una geoposizione in base al formato che hai fornito. Il numero di giorni da richiamare viene specificato nel formato `3day`, `5day`, `7day` o `10day`. Puoi fornire un `geocode/{latitude}/{longitude}` o una `location/{locationId}`. Ogni previsione giornaliera può contenere una previsione per il giorno, una per la notte e una di 24 ore. Questi segmenti sono oggetti separati nelle risposte JSON. I dati di previsione per il giorno di una previsione giornaliera non sono più disponibili dopo le 15:00 dell'ora locale. Alle 15:00 ora locale, la tua applicazione non visualizzerà più i dati per la previsione per il giorno.|
|`GET /v1/{geocode or location ID}/forecast/intraday/{format}.json`|Restituisce le previsione meteo giornaliere in periodi di sei ore per 3, 5, 7 o 10 giorni per una geoposizione in base al formato che hai fornito. Il numero di giorni da richiamare viene specificato nel formato `3day`, `5day`, `7day` o `10day`. Puoi fornire un `geocode/{latitude}/{longitude}` o una `location/{locationId}`. Ogni previsione giornaliera può contenere una previsione per la mattina, il pomeriggio, la sera e la notte. Questi segmenti sono oggetti separati nelle risposte JSON.|
|`GET /v1/{geocode or location ID}/observations.json`              |Restituisce le condizioni meteo per una georilevazione. Puoi fornire un `geocode/{latitude}/{longitude}` o una `location/{locationId}`.  Queste osservazioni recenti vengono conservate nel database fino a 10 minuti per le stazioni di segnalazione specifiche e per 24 ore di osservazioni a stazione. I dati sulle osservazioni recenti vengono costantemente aggiornati e sostituiti con una metodologia primo arrivato / primo eliminato (ruotando i dati con le osservazioni più recenti e spostando le più vecchie nella memoria di archiviazione) in base all'indicatore di data/ora delle osservazioni.|
|`GET /v1/{geocode or location ID}/observations/timeseries.json`   |Restituisce le osservazioni correnti e fino a 24 ore di osservazioni passate, dalla data e ora correnti, per una georilevazione. Puoi fornire un `geocode/{latitude}/{longitude}` o una `location/{locationId}`. Le osservazioni meteo vengono raccolte da periferiche fisiche ubicate globalmente e da osservazioni meteo correnti.|
|`GET /v1/{geocode, country code, state, or area}/alerts.json`      |Restituisce gli avvisi, le avvertenze, le istruzioni e gli avvertimenti meteo emessi dal National Weather Service (NWS), Environment Canada e MeteoAlarm (Europa) e include la traduzione della descrizione dell'evento, il nome del paese e le intestazioni dell'avviso in 49 lingue. Puoi fornire un `geocode/{latitude}/{longitude}`, `country/{countrycode}`, `country/{countrycode}/state/{statecode}`/, o `country/{countrycode}/area/{areaid}`.|
|`GET /v1/alert/{detail_key}/details.json`                         |Restituisce gli avvisi, le avvertenze, le istruzioni e gli avvertimenti meteo emessi dal National Weather Service (NWS), Environment Canada e MeteoAlarm (Europa). I dettagli includono informazioni approfondite sull'emissione degli avvisi del governo per l'area specificata e includono la traduzione della descrizione dell'evento, il nome del paese e le intestazioni dell'avviso in 49 lingue.|
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |Restituisce informazioni astronomiche giornaliere (solo Stati Uniti) originate dalle stazioni di osservazione del National Weather Service per un periodo di tempo compreso tra 10 e 30 anni o più. Le informazioni sono raccolte e fornite dal National Climatic Data Center (NCDC). Puoi fornire un `geocode/{latitude}/{longitude}` o `location/{PostalLocationId}`.|
|`GET /v1/{geocode or postal code}/almanac/monthly.json`           |Restituisce informazioni astronomiche mensili (solo Stati Uniti) originate dalle stazioni di osservazione del National Weather Service per un periodo di tempo compreso tra 10 e 30 anni o più. Le informazioni sono raccolte e fornite dal National Climatic Data Center (NCDC). Puoi fornire un `geocode/{latitude}/{longitude}` o `location/{PostalLocationId}`.|
|`GET /v3/location/{search or point}`                                  |Fornisce la capacità di ricercare un nome ubicazione o un codice geografico (latitudine e longitudine) per richiamare una serie di ubicazioni che corrispondono alla richiesta. Il servizio di ubicazione supporta la ricerca per nome città o codice postale.|
*Tabella 1. Riepilogo API di {{site.data.keyword.weather_short}}*

## Previsioni giornaliere e infragiornaliere
{: #daily_intraday}
L'API di previsione giornaliera può contenere più giorni di previsioni giornaliere per ogni ubicazione.
Ogni giorno di previsione può contenere fino a tre previsioni separate. Per ogni giorno di previsione,
l'API può restituire previsioni del giorno, della notte e di 24 ore.

L'API di previsione infragiornaliera può contenere più giorni di previsioni giornaliere per ogni ubicazione.
Ogni giorno di una previsione contiene quattro previsioni separate di sei ore per la mattina (dalle 7 alle 13),
il pomeriggio (dalle 13 alle 19), la sera (dalle 19 all'1) e la notte (dall'1 alle 7). La previsione infragiornaliera
è simile nella struttura alla previsione giornaliera.

Ogni segmento dispone di un numero parte del giorno, un giorno della settimana e un nome parte del giorno. Ad esempio,
il seguente esempio mostra l'ordine del campo dei dati e i valori dei dati per
`num`, `dow` e `daypart_name`, per una previsione generata
dalle API il giovedì mattina:
* 1, giovedì, mattina
* 2, giovedì, pomeriggio
* 3, giovedì, sera
* 4, giovedì, notte
* 5, venerdì, mattina
* 6, venerdì, pomeriggio
* 7, venerdì, sera
* 8, venerdì, notte

## Osservazioni di serie temporali e correnti
{: #time_series}

I dati delle condizioni correnti e delle osservazioni meteo di serie temporali forniscono informazioni su
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

## Dettagli e intestazioni dell'avviso
{: #alerts_levels}
Le API di avviso restituiscono le intestazioni dell'avviso meteo attive correlate a
temporali gravi, tornadi, terremoti e inondazioni.
Queste API inoltre restituiscono avvisi non meteo come gli avvisi di sequestro di bambini e le
avvertenze delle forze dell'ordine.

**Nota**: questa API è disponibile solo per gli Stati Uniti , il Canada e l'Europa.

L'API Alert Headlines fornisce un valore chiave nell'attributo `detail_key`
per accedere ai dettagli dell'avviso nell'API Alert Details.
Esegui la query dell'API Alert Headlines per ottenere il valore `detail_key` e quindi richiama la risposta dell'API
Alert Details con `detail_key`.

**Nota**: devi visualizzare l'attribuzione dell'origine dati per ognuno dei dati dell'avviso visualizzato nella tua applicazione.

La frase di attribuzione deve visualizzare le seguenti informazioni:

*Emesso da <Nome dell'ufficio> - &lt;Codice del distretto di amministrazione dell'avviso&gt;, &lt;Codice del paese dell'ufficio&gt;, &lt;Origine&gt;, &lt;Dichiarazione di non responsabilità&gt;*

Ad esempio:
* Emesso da National Weather Service - Bismarck, US
* Emesso da Central Institute for Meteorology and Geodynamics - Austria, EMETNET-Meteoalarm

## Informazioni astronomiche
{: #almanac_details}
L'API Almanac richiede un ID e un tipo di ubicazione (città o codice postale)
o una coppia di longitudine e latitudine per richiamare le informazioni per un'ubicazione specifica.

Quando utilizzi `location` nell'URL, l'ubicazione deve includere un ID di ubicazione
(codice postale) con un tipo di ubicazione e un
codice del paese. Quando utilizzi `geocode` nell'URL, l'ubicazione di ricerca deve essere una combinazione di
latitudine e longitudine valida.

L'API Almanac utilizza i parametri per specificare i dati giornalieri o mensili,
una data specifica o un intervallo di date delle informazioni e le unità di misura con cui restituire i dati.

I parametri delle date sono `start` e `end`. Il parametro `start` è un parametro obbligatorio
ma il parametro `end` è facoltativo. Quando i parametri vengono utilizzati insieme, la combinazione restituisce
un intervallo di date invece di un mese o un giorno della data.

Il formato della data per richiamare i risultati di Daily Almanac è un valore numerico a quattro cifre che rappresenta
il mese e il giorno per la data richiesta, MMDD. Ogni giorno con un solo numero
**deve** essere preceduto da uno zero, ad esempio, 01.

Il formato della data per richiamare i risultati di Monthly Almanac è il mese, MM. Ogni mese con un solo numero
**deve** essere preceduto da uno zero, ad esempio, 01. Qualsiasi altro formato provoca un errore nell'API
e non saranno restituiti dati.

**Nota**: se non fornisci il valore della data nella richiesta, il sistema restituisce
lo stato 404 (Richiesta non valida). L'API non fornisce un valore predefinito.

## Costruzione URL
{: #url_construction}

Le API REST  utilizzano parametri di query e una struttura URL comuni per richiedere e filtrare i dati meteorologici.
Gli URL passati alle API sono costruiti nel seguente modo:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/<latitude>/<longitude>/<product group>/<date>/<format>&units={units code}&language={language code}
```

Ad esempio:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/33.40/83.42/forecast/daily/3day.json?units=m&language=en-US
```

|**Attributo**     |**Descrizione**                                    |
|------------------|---------------------------------------------------|
|`hostname`        |Il percorso dell'URL ospitante. Ad esempio, `https://twcservice.mybluemix.net:443/api/weather`.|
|`version`         |L'iterazione corrente. Ad esempio, `v1`.|
|`location`        |Il codice geografico o l'ID di ubicazione. Il gruppo di ubicazione può essere `geocode` o `location`. Ad esempio, `geocode/45.4214/75.6919` rappresenta Ottawa, Canada. Se fornisci una coordinata di georilevazione, l'API restituisce i dati per l'ubicazione disponibile più vicina. I punti sono utilizzati come separatori decimali e le virgole sono utilizzate per separare i valori di latitudine e longitudine. Se fornisci un codice geografico, i valori di latitudine e longitudine attuali che stanno venendo utilizzati sono restituiti nei metadati della risposta.|
|`product group`   |Il prodotto. Ad esempio, `observations` o `forecast`. Un gruppo secondario del prodotto, ad esempio, `historical`, è facoltativo.|
|`data`            |Il tipo di data. Ad esempio, `daily` o `monthly`.|
|`format`          |Il formato. Ad esempio, `3day`, `5day`, `7day` o `10day`.|
|`units`           |Le unità di misura facoltative con cui restituire la risposta. L'API supporta le unità di misura English (e), Metric (m) e UK-Hybrid (h). Se fornisci le unità di misura ma non un valore, l'API restituisce i dati nell'unità di misura che corrisponde al codice della lingua. L'unità di misura richiesta o predefinita viene restituita nel parametro units nei metadati della risposta.|
|`language`        |La lingua in cui restituire la risposta. L'impostazione predefinita è en-US. La lingua di traduzione richiesta o predefinita viene restituita nel parametro language nei metadati della risposta.|
*Tabella 2. Dettagli URL*

**Nota**: le API REST utilizzano lo standard ISO 3166 per i codici del paese. Per ulteriori informazioni, consulta
[ISO Standard Online Browsing Platform](https://www.iso.org/obp/ui/#search/code/){:new_window}.
Le API utilizzano il sistema di riferimento delle coordinate del codice geografico WGS84. Per ulteriori informazioni, consulta
[Basic Geo Vocabulary](https://www.w3.org/2003/01/geo/){:new_window}.

## Immagini e codici dell'icona
{: #icon_code_images}

Quando le API REST {{site.data.keyword.weather_short}} restituiscono un codice dell'icona nella risposta,
puoi utilizzarlo per determinare quale immagine dell'icona visualizzare nella tua applicazione.
Esiste una relazione uno-a-uno tra il codice dell'icona nella risposta dell'API e il nome del file dell'immagine dell'icona.
Ad esempio, se la risposta dell'API contiene un `icon_code` di 1, puoi utilizzare il nome del file `01.png`
per visualizzare l'immagine dell'icona corrispondente.

Nel tuo codice, puoi creare una funzione che utilizza il `icon_code`
per determinare l'URL dell'immagine dell'icona. Ad esempio:

```
function getIconURL(code) {
    return "images/weathericons/icon" + code + ".png";
}
```

La seguente tabella contiene le immagini, le descrizioni e i codici dell'icona che possono essere utilizzati
con le API REST {{site.data.keyword.weather_short}}. La tabella indica se un'icona
è utilizzata nelle API di osservazione o di previsione e se l'icona è disponibile nelle
parti della previsione del giorno o della notte.

|**Codice**|**Descrizione**|**Immagine**|**Utilizzo API** |**Notte o giorno**|
|----|--------------------------|------------|------------|--------------------|
| 0  | Tornado                  | <img src="images/00.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Notte e giorno |
| 1  | Tempesta tropicale           | <img src="images/01.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 2  | Uragano                | <img src="images/02.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Notte e giorno |
| 3  | Forti tempeste            | <img src="images/03.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Notte e giorno |
| 4  | Tuoni e grandine         | <img src="images/04.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 5  | Rovesci da pioggia a neve     | <img src="images/05.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 6  | Pioggia / Nevischio             | <img src="images/06.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 7  | Freddo misto a neve / Nevischio  | <img src="images/07.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 8  | Pioggerella gelida         | <img src="images/08.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 9  | Pioggerella                  | <img src="images/09.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 10 | Pioggia gelida            | <img src="images/10.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 11 | Pioggia leggera               | <img src="images/11.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 12 | Pioggia                     | <img src="images/12.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 13 | Spruzzate di neve sparse       | <img src="images/13.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 14 | Neve leggera               | <img src="images/14.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 15 | Ventoso / Raffica di neve  | <img src="images/15.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 16 | Neve                     | <img src="images/16.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 17 | Grandine                     | <img src="images/17.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 18 | Nevischio                    | <img src="images/18.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 19 | Vento con sabbia / Tempesta di sabbia | <img src="images/19.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 20 | Nebbioso                    | <img src="images/20.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 21 | Foschia / Ventoso             | <img src="images/21.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 22 | Fumo / Ventoso            | <img src="images/22.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 23 | Ventilato                   | <img src="images/23.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Notte e giorno |
| 24 | Vento con nebbia / Ventoso    | <img src="images/24.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 25 | Glaciale / Cristalli di ghiaccio    | <img src="images/25.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 26 | Nuvoloso                   | <img src="images/26.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 27 | Generalmente nuvoloso            | <img src="images/27.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 28 | Generalmente nuvoloso            | <img src="images/28.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Giorno         |
| 29 | Parzialmente nuvoloso            | <img src="images/29.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte       |
| 30 | Parzialmente nuvoloso            | <img src="images/30.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Giorno         |
| 31 | Sereno                    | <img src="images/31.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte       |
| 32 | Soleggiato                    | <img src="images/32.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Giorno         |
| 33 | Bello / Generalmente sereno      | <img src="images/33.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte       |
| 34 | Bello / Generalmente soleggiato      | <img src="images/34.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Giorno         |
| 35 | Misto pioggia & grandine        | <img src="images/35.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Giorno         |
| 36 | Caldo                      | <img src="images/36.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Giorno         |
| 37 | Temporali isolati   | <img src="images/37.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Giorno         |
| 38 | Temporali            | <img src="images/38.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 39 | Rovesci sparsi        | <img src="images/39.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Giorno         |
| 40 | Forte pioggia               | <img src="images/40.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 41 | Rovesci nevosi sparsi   | <img src="images/41.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Giorno         |
| 42 | Forte nevicata               | <img src="images/42.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
| 43 | Tormenta                 | <img src="images/43.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Notte e giorno |
| 44 | Non disponibile (N/D)      | <img src="images/44.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Notte e giorno |
| 45 | Rovesci sparsi        | <img src="images/45.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Notte       |
| 46 | Rovesci nevosi sparsi   | <img src="images/46.png " width="100" height="100" alt="Immagine icona."/>| Previsione                | Notte       |
| 47 | Temporali sparsi  | <img src="images/47.png " width="100" height="100" alt="Immagine icona."/>| Previsione e osservazioni | Notte e giorno |
*Tabella 3. Immagini e codici dell'icona*

Puoi scaricare questa serie di icone meteo come [PNG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_png.zip){:new_window}
o [SVG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_svg.zip){:new_window} e utilizzarli nella tua applicazione. 

Puoi ance scaricare la [serie di icone](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} che utilizza l'applicazione demo
[{{site.data.keyword.weather_short}}](http://weather-company-data-demo.{APPDomain}){: new_window}.

## Unità di misura
{: #units_measure}

Quando utilizzi le API, non è necessario passare esplicitamente un'unità di misura. Le API utilizzano per impostazione predefinita l'unità di misura associata al codice di lingua nell'URL. Tuttavia, se desideri fornire un'unità di misura diversa dalla predefinita, puoi passare a un'unità di misura che sovrascrive la predefinita.

* Per en-US o en, il codice di unità di misura predefinito è English/Imperial. Il codice di unità è `e`.
* Per en-GB, l'unità di misura predefinita è Hybrid-UK. Il codice di unità è `h`.
* Per tutte le altre, l'unità di misura predefinita è Metric. Il codice di unità è `m`.

## Traduzione in un'altra lingua
{: #language_translation}

Le API traducono frasi e unità di misura. Quando crei una richiesta URL, devi fornire una lingua valida.
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
|`wx_phrase`         |Una descrizione di testo delle condizioni meteo osservate alla stazione di segnalazione.|
|`pressure_desc`     |Una frase che descrive i cambiamenti nella lettura della pressione barometrica nell'ultima ora.|
|`headline_text`     |Il testo dell'intestazione di un evento per l'ubicazione.|
|`event_desc`        |Una descrizione dell'evento.|
|`cntry_name`        |Il nome del paese in cui si è verificato l'evento, fornito in lettere maiuscole e minuscole.|
*Tabella 4. Campi di risposta tradotti*

## Gestione dei campi dati mancanti o null nella risposta API
{: #handling_null_or_missing}

Se un campo di dati è null perché i dati on sono disponibili, le API REST restituiscono i tag campo appropriati con la parola `null` o non restituiscono affatto il campo. 

## Gestione errori
{: #handling_errors}

I seguenti codici di errore sono comuni per tutte le API:

|**Errore** |**Descrizione**                                    |
|----------|---------------------------------------------------|
|400       |Richiesta non valida. La richiesta non è comprensibile per il server a causa di una sintassi malformata. Questo codice di errore è implementato per tutte le API. L'API rifiuta la richiesta se vengono forniti dei parametri non validi.|
|401       |Non autorizzato. La richiesta richiede l'autenticazione.|
|403       |Non consentito. Il server comprende la richiesta ma si rifiuta di soddisfarla.|
|404       |Non trovato. Se un parametro obbligatorio non è presente nella richiesta API, viene restituito un errore MissingParameterException con un codice di errore 404.|
|500       |Errore server interno. Il server ha riscontro una condizione inattesa che gli impedisce di soddisfare la richiesta.|
*Tabella 5. Codice di risposta di errore*

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
