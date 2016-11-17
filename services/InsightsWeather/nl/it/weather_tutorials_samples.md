---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Esempi
{: #tutorials_samples}

Impara come utilizzare il servizio Insights for Weather con i seguenti esempi.
{: shortdesc}

## Demo di Insights for Weather
{: #insights_weather_demo}

Puoi utilizzare un'applicazione di esempio per visualizzare i dati meteo utilizzando il servizio Insights for Weather.
L'applicazione è accessibile andando all'indirizzo [http://insights-for-weather-demo.mybluemix.net/](http://insights-for-weather-demo.mybluemix.net/).
L'applicazione si apre nel tuo browser e ti chiede se desideri condividere la tua ubicazione corrente con essa.

Dall'applicazione di esempio, puoi visualizzare le condizioni osservate correnti per il meteo nella tua ubicazione.

![Immagine della schermata principale con le osservazioni correnti per Ottawa, ON.](images/twctestapp_main_screen.jpg "Immagine della schermata principale con le osservazioni correnti per Ottawa, ON.")

Puoi inoltre visualizzare la previsione oraria per le successive 24 ore e la previsione giornaliera per i successivi 10 giorni.
Se passi il puntatore del mouse su ognuna di queste aree nell'esempio, puoi visualizzare i risultati della chiamata API nel formato JSON,
che include i metadati che sono stati utilizzati per richiamare i dati.

Nell'applicazione demo, fai clic su **Distribuisci a Bluemix** per creare una versione clonata dell'applicazione o
[clona l'applicazione direttamente da GitHub](https://github.com/IBM-Bluemix/insights-for-weather-demo).

## Introduzione a una previsione di 10 giorni standard
{: #getting_ten_day_forecast}

Puoi immettere un'operazione `GET` nella tua applicazione per richiamare i dati della previsione di 10 giorni.
Ad esempio, puoi utilizzare la seguente richiesta `GET` per richiamare la previsione di 10 giorni per Ottawa, ON, Canada:

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/forecast/daily/10day?units=m&geocode=45.42%2C75.69&language=en-US
}
```

Il `username` e la `password` sono univoci per la tua applicazione e l'istanza di servizio.
Puoi trovare queste informazioni nelle variabili di ambiente `VCAP_SERVICES`.

Il servizio restituisce le risposte nel formato JSON. Se la risposta ha esito positivo, viene restituito un codice di stato 200.
Se la risposta ha esito negativo, viene restituito un codice di errore.

Il corpo della risposta include i metadati e l'array delle previsioni giornaliere per ognuno dei successivi 10 giorni.
Ad esempio, i metadati possono contenere i seguenti dati:

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1443712484194:-1546029161",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1443714284,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

Ogni previsione giornaliera contiene le informazioni generali che applica al periodo di 24 ore per il giorno della settimana specificato (`dow`).
Ad esempio, la previsione giornaliera può contenere i seguenti dati:

```
    {
      "class": "fod_long_range_daily",
      "expire_time_gmt": 1443714284,
      "fcst_valid": 1444525200,
      "fcst_valid_local": "2015-10-11T07:00:00+0600",
      "num": 11,
      "max_temp": 14,
      "min_temp": 4,
      "torcon": null,
      "stormcon": null,
      "blurb": null,
      "blurb_author": null,
      "lunar_phase_day": 28,
      "dow": "Sunday",
      "lunar_phase": "Waning Crescent",
      "lunar_phase_code": "WNC",
      "sunrise": "2015-10-11T07:07:25+0600",
      "sunset": "2015-10-11T18:19:57+0600",
      "moonrise": "2015-10-11T05:17:47+0600",
      "moonset": "2015-10-11T17:40:49+0600",
      "qualifier_code": null,
      "qualifier": null,
      "narrative": "Times of sun and clouds. Highs 13 to 15C and lows 3 to 5C.",
      "qpf": 0,
      "snow_qpf": 0,
      "snow_range": "",
      "snow_phrase": "",
      "snow_code": "",
      "night": {
      },
      "day": {
      }
    }
```

Ogni previsione giornaliera contiene una parte per la notte e una per il giorno per il giorno della settimana specificato.
Ad esempio, entrambe le parti possono contenere i seguenti dati di previsione:

```
      "night": {
        "fcst_valid": 1444568400,
        "fcst_valid_local": "2015-10-11T19:00:00+0600",
        "day_ind": "N",
        "thunder_enum": 0,
        "daypart_name": "Sunday night",
        "long_daypart_name": "Sunday night",
        "alt_daypart_name": "Sunday night",
        "thunder_enum_phrase": "No thunder",
        "num": 21,
        "temp": 4,
        "hi": 10,
        "wc": 3,
        "pop": 10,
        "icon_extd": 2900,
        "icon_code": 29,
        "wxman": "wx1650",
        "phrase_12char": "P Cloudy",
        "phrase_22char": "Partly Cloudy",
        "phrase_32char": "Partly Cloudy",
        "subphrase_pt1": "Partly",
        "subphrase_pt2": "Cloudy",
        "subphrase_pt3": "",
        "precip_type": "precip",
        "rh": 65,
        "wspd": 10,
        "wdir": 98,
        "wdir_cardinal": "E",
        "clds": 40,
        "pop_phrase": "",
        "temp_phrase": "Low 4C.",
        "accumulation_phrase": "",
        "wind_phrase": "Winds E at 10 to 15 km/h.",
        "shortcast": "Partly cloudy",
        "narrative": "A few clouds. Low 4C. Winds E at 10 to 15 km/h.",
        "qpf": 0,
        "snow_qpf": 0,
        "snow_range": "",
        "snow_phrase": "",
        "snow_code": "",
        "vocal_key": "D22:DA05:X3000300044:S300042:TL4:W04R02",
        "qualifier_code": null,
        "qualifier": null,
        "uv_index_raw": 0,
        "uv_index": 0,
        "uv_warning": 0,
        "uv_desc": "Low",
        "golf_index": null,
        "golf_category": ""
      },
```

## Introduzione a una previsione di 24 ore standard
{: #getting_twenty_four_hour_forecast}

Puoi immettere un'operazione `GET` nella tua applicazione per richiamare i dati della previsione di 24 ore.
Ad esempio, puoi utilizzare la seguente richiesta `GET` per richiamare la previsione di 24 ore per Ottawa, ON, Canada:

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/forecast/hourly/24hour?units=m&geocode=45.42%2C75.69&language=en-US
```

Il corpo della risposta include i metadati e l'array delle previsioni orarie
per ognuna delle successive 24 ore. Ad esempio, i metadati possono contenere i seguenti dati:

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1443722945280:-1956318185",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1443723545,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

Ogni previsione oraria contiene le informazioni generali che applica
all'ora specificata da `num`. Ad esempio, la previsione oraria può contenere i seguenti dati:

```
    {
      "class": "fod_short_range_hourly",
      "expire_time_gmt": 1443723545,
      "fcst_valid": 1443726000,
      "fcst_valid_local": "2015-10-02T01:00:00+0600",
      "num": 1,
      "day_ind": "N",
      "temp": 12,
      "dewpt": 1,
      "hi": 12,
      "wc": 11,
      "feels_like": 11,
      "icon_extd": 3100,
      "wxman": "wx1550",
      "icon_code": 31,
      "dow": "Friday",
      "phrase_12char": "Clear",
      "phrase_22char": "Clear",
      "phrase_32char": "Clear",
      "subphrase_pt1": "Clear",
      "subphrase_pt2": "",
      "subphrase_pt3": "",
      "pop": 0,
      "precip_type": "rain",
      "qpf": 0,
      "snow_qpf": 0,
      "rh": 48,
      "wspd": 15,
      "wdir": 208,
      "wdir_cardinal": "SSW",
      "gust": null,
      "clds": 17,
      "vis": 16.1,
      "mslp": 1018.6,
      "uv_index_raw": 0,
      "uv_index": 0,
      "uv_warning": 0,
      "uv_desc": "Low",
      "golf_index": null,
      "golf_category": "",
      "severity": 1
    },
```

## Come ottenere le condizioni correnti
{: #current_conditions}

Puoi immettere un'operazione `GET` nella tua applicazione per richiamare le condizioni meteo correnti.
Ad esempio, puoi utilizzare la seguente richiesta `GET` per richiamare le condizioni correnti per Ottawa, ON, Canada:

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/observations/current?units=m&geocode=45.42%2C75.69&language=en-US
```

Il corpo della risposta include i metadati e i dati meteo osservati correntemente.
Ad esempio, i metadati possono contenere i seguenti dati:

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1443724606672:1993259329",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1443725206,
    "status_code": 200
  },
  "observation": {
  }
}
```

I dati delle osservazioni contengono le informazioni generali e i valori specifici
delle unità di misura. Ad esempio, le condizioni correnti potrebbero contenere i seguenti dati
se le unità di misure specificate sono metriche:

```
  "observation": {
    "class": "observation",
    "expire_time_gmt": 1443725206,
    "obs_time": 1443724606,
    "obs_time_local": "2015-10-02T00:36:46+0600",
    "wdir": 210,
    "icon_code": 33,
    "icon_extd": 3300,
    "sunrise": "2015-10-02T06:55:47+0600",
    "sunset": "2015-10-02T18:36:42+0600",
    "day_ind": "N",
    "uv_index": 0,
    "uv_warning": 0,
    "wxman": "wx1550",
    "obs_qualifier_code": null,
    "ptend_code": 2,
    "dow": "Friday",
    "wdir_cardinal": "SSW",
    "uv_desc": "Low",
    "phrase_12char": "Fair",
    "phrase_22char": "Fair",
    "phrase_32char": "Fair",
    "ptend_desc": "Falling",
    "sky_cover": "Partly Cloudy",
    "clds": "FEW",
    "obs_qualifier_severity": null,
    "vocal_key": "OT53:OX3300",
    "metric": {
      "wspd": 13,
      "gust": null,
      "vis": 16.09,
      "mslp": 1018.7,
      "altimeter": 1018.63,
      "temp": 12,
      "dewpt": 3,
      "rh": 54,
      "wc": 11,
      "hi": 12,
      "temp_change_24hour": -16,
      "temp_max_24hour": 19,
      "temp_min_24hour": 6,
      "pchange": -1.02,
      "feels_like": 11,
      "snow_1hour": 0,
      "snow_6hour": 0,
      "snow_24hour": 0,
      "snow_mtd": null,
      "snow_season": null,
      "snow_ytd": null,
      "snow_2day": null,
      "snow_3day": null,
      "snow_7day": null,
      "ceiling": null,
      "precip_1hour": 0,
      "precip_6hour": 0,
      "precip_24hour": 0,
      "precip_mtd": null,
      "precip_ytd": null,
      "precip_2day": null,
      "precip_3day": null,
      "precip_7day": null,
      "obs_qualifier_100char": null,
      "obs_qualifier_50char": null,
      "obs_qualifier_32char": null
    }
  }
```






