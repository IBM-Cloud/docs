---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo del pacchetto Weather
{: #openwhisk_catalog_weather}

Il pacchetto `/whisk.system/weather` offre un pratico modo per richiamare l'API Weather Company Data for IBM Bluemix.

Il pacchetto include la seguente azione.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/weather` | pacchetto | username, password | Servizi dall'API Weather Company Data for IBM Bluemix  |
| `/whisk.system/weather/forecast` | azione | latitude, longitude, timePeriod | Previsione per il periodo di tempo specificato|

Si consiglia di effettuare la creazione di un bind di pacchetto con i valori `username` e `password`. In questo modo, non dovrai specificare le credenziali ogni volta che richiami le azioni nel pacchetto.

## Come ottenere una previsione meteo per una località
{: #openwhisk_catalog_weather_forecast}

L'azione `/whisk.system/weather/forecast` restituisce una previsione meteo per una località, richiamando un'API The Weather Company. I parametri sono i seguenti:

- `username`: nome utente per The Weather Company Data for IBM Bluemix che ha diritto a richiamare l'API delle previsioni.
- `password`: password per The Weather Company Data for IBM Bluemix che ha diritto a richiamare l'API delle previsioni.
- `latitude`: la coordinata della latitudine della località.
- `longitude`: la coordinata della longitudine della località.
- `timeperiod`: periodo di tempo per la previsione. Le opzioni valide sono '10day' - (impostazione predefinita) restituisce una previsione giornaliera per un periodo di 10 giorni, '48hour' - restituisce una previsione oraria per 2 giorni, 'current' - restituisce le condizioni meteorologiche correnti, 'timeseries' - restituisce le rilevazioni in tempo reale e quelle delle ultime 24 ore dalla data/ora corrente.


Di seguito viene riportato un esempio di creazione di un bind di pacchetto e successiva acquisizione di una previsione meteo di 10 giorni.

1. Crea un bind di pacchetto con la tua chiave API.
  
  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}
  
2. Richiama l'azione `forecast` nel tuo bind di pacchetto per ottenere la previsione meteo.
  
  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
  ```
  {: pre}
  
  ```json
  {
      "forecasts": [
          {
              "dow": "Mercoledì",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Possibilità di alcuni rovesci. Massime tra i -2°C e 0°C e minime tra -17°C e -15°C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Giovedì",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Prevalentemente soleggiato. Massime tra -5°C e -3°C e minime tra i -9°C e -7°C.",
              ...
          },
          ...
      ],
  }
  ```
  
