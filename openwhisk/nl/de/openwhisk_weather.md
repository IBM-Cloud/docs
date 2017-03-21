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

# Weather-Paket verwenden
{: #openwhisk_catalog_weather}

Das Paket `/whisk.system/weather` bietet eine komfortable Methode zum Aufrufen der Weather Company Data for IBM Bluemix-API.

Das Paket enthält die folgende Aktion.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/weather` | Paket | username, password | Services der Weather Company Data for IBM Bluemix-API  |
| `/whisk.system/weather/forecast` | Aktion | latitude, longitude, timePeriod | Vorhersage für angegebenen Zeitraum|

Es wird empfohlen, eine Paketbindung mit den Werten `username` und `password` zu erstellen. Auf diese Weise brauchen Sie die Berechtigungsnachweise nicht jedes Mal anzugeben, wenn Sie die Aktionen im Paket aufrufen.

## Wettervorhersage für einen Standort abrufen
{: #openwhisk_catalog_weather_forecast}

Die Aktion `/whisk.system/weather/forecast` gibt eine Wettervorhersage für einen Standort durch einen Aufruf der API für The Weather Company zurück. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für Weather Company Data for IBM Bluemix, der berechtigt ist, die API für die Vorhersage aufzurufen.
- `password`: Das Kennwort für Weather Company Data for IBM Bluemix, das berechtigt ist, die API für die Vorhersage aufzurufen.
- `latitude`: Die Breitengradkoordinate des Standorts.
- `longitude`: Die Längengradkoordinate des Standorts.
- `timeperiod`: Der Zeitraum für die Vorhersage. Gültige Optionen: '10day' (Standardwert) - Gibt eine tägliche 10-Tage-Vorhersage zurück. '48hour' - Gibt eine stündliche 2-Tage-Vorhersage zurück. 'current' - Gibt die aktuellen Wetterbedingungen zurück. 'timeseries' - Gibt die aktuellen Wetterbeobachtungen und bis zu 24 Stunden zurückliegende Beobachtungen ab dem aktuellen Zeitpunkt (Datum und Uhrzeit) zurück.


Das folgende Beispiel zeigt die Erstellung einer Paketbindung und den anschließenden Abruf einer 10-Tage-Vorhersage.

1. Erstellen Sie eine Paketbindung mit Ihrem API-Schlüssel.
  
  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}
  
2. Rufen Sie die Aktion `forecast` in Ihrer Paketbindung auf, um die Wettervorhersage abzurufen.
  
  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
  ```
  {: pre}
  
  ```json
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  
