---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation du package Weather
{: #openwhisk_catalog_weather}

Le package `/whisk.system/weather` offre une méthode pratique pour appeler The Weather Company Data for IBM Bluemix API.

Le package inclut l'action ci-dessous.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/weather` | package | username, password | Services de Weather Company Data for IBM Bluemix API  |
| `/whisk.system/weather/forecast` | action | latitude, longitude, timePeriod | prévision pour la période spécifiée|

Il est recommandé de créer une liaison de package avec les valeurs `username` et `password`. Ainsi, il n'est pas nécessaire de spécifier les données d'identification à chaque fois que vous appelez les actions du package.

## Obtention d'une prévision météorologique pour un lieu
{: #openwhisk_catalog_weather_forecast}

L'action `/whisk.system/weather/forecast` renvoie une prévision météorologique pour un emplacement en appelant une API de The Weather Company. Les paramètres sont les suivants :

- `username` : nom d'utilisateur pour The Weather Company Data for IBM Bluemix qui est autorisé à appeler l'API de prévision.
- `password` : mot de passe pour The Weather Company Data for IBM Bluemix qui est autorisé à appeler l'API de prévision.
- `latitude` : coordonnée de latitude du lieu.
- `longitude` : coordonnée de longitude du lieu.
- `timePeriod`: période sur laquelle porte la prévision. Les options valides sont '10day' - (valeur par défaut) Renvoie une prévision quotidienne sur 10 jours, '48hour' - Renvoie une prévision horaire sur 2 jours, 'current' - Renvoie les conditions météorologiques actuelles, 'timeseries' - Renvoie les observations actuelles et jusqu'à 24 heures d'observations antérieures à partir de la date et de l'heure en cours.


Voici un exemple de création d'une liaison de package, puis d'obtention d'une prévision à 10 jours :

1. Créez une liaison de package avec votre clé d'API.
  
  ```
  wsk package bind /whisk.system/weather myWeather --param username MON_NOM_UTILISATEUR --param password MON_MOT_DE_PASSE
  ```
  {: pre}
  
2. Appelez l'action `forecast` dans votre liaison de package pour obtenir la prévision météorologique.
  
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
  
