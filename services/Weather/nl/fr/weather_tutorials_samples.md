---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Exemples
{: #tutorials_samples}

Apprenez à utiliser le service {{site.data.keyword.weather_short}} à l'aide des exemples ci-après.
{: shortdesc}

## Démonstration {{site.data.keyword.weather_short}}
{: #insights_weather_demo}

Vous pouvez apprendre à extraire des données météorologiques à l'aide du service {{site.data.keyword.weather_short}} en utilisant l'[application de démonstration {{site.data.keyword.weather_short}}](http://weather-company-data-demo.{APPDomain}){: new_window}.
L'application s'ouvre dans votre navigateur et vous demande si vous souhaitez partager votre emplacement en cours avec elle.

L'application de démonstration vous permet de visualiser les conditions météorologiques en cours observées là où vous êtes.

![Image de l'écran principal avec les observations en cours pour Ottawa, Ontario.](images/twctestapp_main_screen.jpg "Image de l'écran principal avec les observations en cours pour Ottawa, Ontario.")

Vous pouvez également visualiser les prévisions heure par heure pour les 48 prochaines heures et les prévisions journalières pour les 10 prochains jours.
La prévision journalière affiche le segment de la journée et le segment de la nuit.
Si vous cliquez sur chacune de ces zones dans l'application de démonstration, vous voyez les résultats des appels d'API au format JSON, avec les métadonnées utilisées pour l'extraction des données.


Dans l'application de démonstration, cliquez sur **Deploy to Bluemix** pour créer une version clonée de l'application ou [clonez l'application directement à partir de GitHub](https://github.com/IBM-Bluemix/weather-company-data-demo).

## Extraction d'une prévision heure par heure
{: #getting_twenty_four_hour_forecast}

Vous pouvez exécuter une opération `GET` dans votre application pour extraire les données des prévisions heure par heure sur 48 heures.

Le nom d'utilisateur (`username`) et le mot de passe (`password`) sont spécifiques à votre application et à votre instance du service.
Ces informations figurent dans les variables d'environnement `VCAP_SERVICES`.

Le service renvoie des réponses au format JSON. Si la demande a abouti, la réponse contient le code 200.
Si la demande a échoué, la réponse contient un code d'erreur.

Par exemple, vous pouvez utiliser la demande `GET` suivante pour extraire les prévisions heure par heure sur 48 heures pour les coordonnées de longitude et de latitude de la ville d'Ottawa, Ontario, au Canada :

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/forecast/hourly/48hour.json?units=m&language=en-US
```
Vous pouvez aussi exécuter une opération `GET` dans votre application pour extraire les données des prévisions heure par heure sur 48 heures pour un code postal.
**Remarque** : Vous pouvez entrer un code postal uniquement pour les codes de pays pris en charge (Etats-Unis (US), Royaume-Uni (GB), France (FR), Allemagne (DE) ou Italie (IT)).

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/location/97229%3A4%3AUS/forecast/hourly/48hour.json?units=m&language=en-US
```

Le corps de la réponse contient des métadonnées et un tableau de prévisions heure par heure pour chacune des 48 prochaines heures. Par exemple, les métadonnées peuvent contenir les données suivantes :

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1467041322756:187065199",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1467041562,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

Chaque prévision heure par heure contient des informations générales qui s'appliquent à l'heure définie par `num`. Par exemple, la prévision heure par heure peut contenir les données suivantes :

```
   {
      "class": "fod_short_range_hourly",
      "expire_time_gmt": 1467041922,
      "fcst_valid": 1467043200,
      "fcst_valid_local": "2016-06-27T22:00:00+0600",
      "num": 1,
      "day_ind": "N",
      "temp": 21,
      "dewpt": 12,
      "hi": 21,
      "wc": 21,
      "feels_like": 21,
      "icon_extd": 2900,
      "wxman": "wx1600",
      "icon_code": 29,
      "dow": "Monday",
      "phrase_12char": "P Cloudy",
      "phrase_22char": "Partly Cloudy",
      "phrase_32char": "Partly Cloudy",
      "subphrase_pt1": "Partly",
      "subphrase_pt2": "Cloudy",
      "subphrase_pt3": "",
      "pop": 0,
      "precip_type": "rain",
      "qpf": 0,
      "snow_qpf": 0,
      "rh": 56,
      "wspd": 11,
      "wdir": 291,
      "wdir_cardinal": "WNW",
      "gust": null,
      "clds": 31,
      "vis": 16,
      "mslp": 1008.73,
      "uv_index_raw": 0,
      "uv_index": 0,
      "uv_warning": 0,
      "uv_desc": "Low",
      "golf_index": null,
      "golf_category": "",
      "severity": 1
    },
```

## Extraction d'une prévision journalière
{: #getting_ten_day_forecast}

Vous pouvez exécuter une opération `GET` dans votre application pour extraire les données des prévisions sur 10 jours.
Par exemple, vous pouvez utiliser la demande `GET` suivante pour extraire les prévisions sur 10 jours pour la ville d'Ottawa, Ontario, au Canada :

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/forecast/daily/10day.json?units=m&language=en-US
```

Le corps de la réponse contient des métadonnées et un tableau de prévisions journalières pour les 10 prochains jours.
Par exemple, les métadonnées peuvent contenir les données suivantes :

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1467041740847:-1868497945",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1467043540,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

Chaque prévision jour par jour contient des informations générales qui s'appliquent à la période de 24 heures correspondant au jour de la semaine (`dow`).
Par exemple, la prévision jour par jour peut contenir les données suivantes :

```
      "class": "fod_long_range_daily",
      "expire_time_gmt": 1467043540,
      "fcst_valid": 1467075600,
      "fcst_valid_local": "2016-06-28T07:00:00+0600",
      "num": 2,
      "max_temp": 29,
      "min_temp": 18,
      "torcon": null,
      "stormcon": null,
      "blurb": null,
      "blurb_author": null,
      "lunar_phase_day": 22,
      "dow": "Tuesday",
      "lunar_phase": "Last Quarter",
      "lunar_phase_code": "LQ",
      "sunrise": "2016-06-28T05:11:23+0600",
      "sunset": "2016-06-28T20:49:39+0600",
      "moonrise": "2016-06-28T00:56:48+0600",
      "moonset": "2016-06-28T13:39:37+0600",
      "qualifier_code": null,
      "qualifier": null,
      "narrative": "Mainly sunny. Highs 28 to 30C and lows 17 to 19C.",
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

Chaque prévision jour par jour contient un segment nuit et un segment jour pour le jour de la semaine spécifié.
Par exemple, ces deux segments peuvent contenir les données prévisionnelles suivantes :

```
      "night": {
        "fcst_valid": 1467118800,
        "fcst_valid_local": "2016-06-28T19:00:00+0600",
        "day_ind": "N",
        "thunder_enum": 0,
        "daypart_name": "Tomorrow night",
        "long_daypart_name": "Tuesday night",
        "alt_daypart_name": "Tuesday night",
        "thunder_enum_phrase": "No thunder",
        "num": 3,
        "temp": 18,
        "hi": 26,
        "wc": 18,
        "pop": 0,
        "icon_extd": 3100,
        "icon_code": 31,
        "wxman": "wx1500",
        "phrase_12char": "Clear",
        "phrase_22char": "Clear",
        "phrase_32char": "Clear",
        "subphrase_pt1": "Clear",
        "subphrase_pt2": "",
        "subphrase_pt3": "",
        "precip_type": "rain",
        "rh": 43,
        "wspd": 15,
        "wdir": 55,
        "wdir_cardinal": "NE",
        "clds": 2,
        "pop_phrase": "",
        "temp_phrase": "Low 18C.",
        "accumulation_phrase": "",
        "wind_phrase": "Winds NE at 10 to 15 km/h.",
        "shortcast": "Clear",
        "narrative": "A mostly clear sky. Low 18C. Winds NE at 10 to 15 km/h.",
        "qpf": 0,
        "snow_qpf": 0,
        "snow_range": "",
        "snow_phrase": "",
        "snow_code": "",
        "vocal_key": "D4:DA09:X3200320043:S320043:TL18:W02R02",
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

## Extraction des conditions en cours
{: #current_conditions}

Vous pouvez exécuter une opération `GET` dans votre application pour extraire les conditions météorologiques en cours.
Par exemple, vous pouvez utiliser la demande `GET` suivante pour extraire les conditions en cours pour la ville d'Ottawa, Ontario, au Canada :

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/observations.json?units=m&language=en-US
```

Le corps de la réponse contient des métadonnées et les données météorologiques en cours observées.
Par exemple, les métadonnées peuvent contenir les données suivantes :

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1467042290443:151881483",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1467051300,
    "status_code": 200
  },
  "observation": {
  }
}
```

Les données d'observations contiennent des informations générales et des valeurs spécifiques aux unités de mesure. Par exemple, les conditions en cours peuvent contenir les données suivantes si l'unité de mesure définie est Metric :

```
  "observation": {
    "key": "36821",
    "class": "observation",
    "expire_time_gmt": 1467051300,
    "obs_id": "36821",
    "obs_name": "Bakanas",
    "valid_time_gmt": 1467039600,
    "day_ind": "N",
    "temp": 21,
    "wx_icon": 27,
    "icon_extd": 2700,
    "wx_phrase": "Mostly Cloudy",
    "pressure_tend": 1,
    "pressure_desc": "Rising",
    "dewPt": 17,
    "heat_index": 21,
    "rh": 74,
    "pressure": 965.2,
    "vis": 50,
    "wc": 21,
    "wdir": 270,
    "wdir_cardinal": "W",
    "gust": null,
    "wspd": 4,
    "max_temp": -4,
    "min_temp": null,
    "precip_total": null,
    "precip_hrly": null,
    "snow_hrly": null,
    "uv_desc": "Low",
    "feels_like": 21,
    "uv_index": 0,
    "qualifier": null,
    "qualifier_svrty": null,
    "blunt_phrase": null,
    "terse_phrase": null,
    "clds": 75
  }
```

## Extraction des alertes
{: #getting_alerts}

Vous pouvez exécuter une opération `GET` dans votre application pour extraire les titres d'alerte météorologique en cours.
Par exemple, vous pouvez utiliser la demande `GET` suivante pour extraire les titres d'alerte météorologique pour la ville de San Bernardino, Californie, aux Etats-Unis :

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/34.12/-117.30/alerts.json?language=en-US
```

Le corps de la réponse contient des métadonnées et les titres d'alerte météorologique en cours.
Par exemple, les métadonnées peuvent contenir les données suivantes :

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1467042764309:-1516467294",
    "version": "1",
    "longitude": "-117.30",
    "latitude": "34.12",
    "expire_time_gmt": 1467042824,
    "status_code": 200
  },
}
```

Les données des titres d'alerte contiennent des informations générales, ainsi qu'une clé qui permet d'extraire les détails de l'alerte météorologique. Par exemple, les données des titres d'alerte peuvent contenir les données suivantes :

```
  "alerts": [
    {
      "key": "cf63821f-9521-3f27-92ec-e1562ccd469b",
      "class": "bulletin",
      "msg_type_cd": 2,
      "msg_type": "Update",
      "pil": "NPW",
      "phenomena": "HT",
      "significance": "Y",
      "etn": "0003",
      "office_cd": "KSGX",
      "office_name": "San Diego",
      "office_st_cd": "CA",
      "office_cntry_cd": "US",
      "event_desc": "Heat Advisory",
      "severity_cd": 3,
      "severity": "Moderate",
      "categories": [
        {
          "category": "Met",
          "category_cd": 2
        }
      ],
      "response_types": [
        {
          "response_type": "Execute",
          "response_type_cd": 4
        }
      ],
      "urgency": "Expected",
      "urgency_cd": 2,
      "certainty": "Likely",
      "certainty_cd": 2,
      "effective_dt_tm_local": null,
      "effective_dt_tm_tz_abbrv": null,
      "expire_dt_tm_local": "2016-06-29T20:00:00-07:00",
      "expire_dt_tm_tz_abbrv": "PDT",
      "expire_time_gmt": 1467255600,
      "onset_dt_tm_local": null,
      "onset_dt_tm_tz_abbrv": null,
      "flood": null,
      "area_type": "Z",
      "lat": 33.48,
      "lon": -117.29,
      "area_id": "CAZ048",
      "area_name": "San Bernardino and Riverside County Valleys",
      "st_cd": "CA",
      "st_name": "California",
      "cntry_cd": "US",
      "cntry_name": "UNITED STATES OF AMERICA",
      "headline_text": "Heat Advisory until 8PM PDT WED",
      "detail_key": "cf63821f-9521-3f27-92ec-e1562ccd469b",
      "source": "National Weather Service",
      "disclaimer": null,
      "issue_dt_tm_local": "2016-06-27T04:38:50-07:00",
      "issue_dt_tm_tz_abbrv": "PDT",
      "identifier": "e234b6f889bf9a91c5d9f309db63eaa0",
      "proc_dt_tm_local": "2016-06-27T04:38:58-07:00",
      "proc_dt_tm_tz_abbrv": "PDT"
    }
  ]
```

La clé contenue dans le corps de réponse des titres d'alerte peut être utilisée pour rechercher des détails d'alerte météorologique.
Par exemple, vous pouvez utiliser la demande `GET` suivante pour extraire les détails d'alerte météorologique correspondant aux titres d'alerte météorologique pour la ville de San Bernardino, Californie, aux Etats-Unis :

```
https://twcservice.mybluemix.net:443/api/weather/v1/alert/cf63821f-9521-3f27-92ec-e1562ccd469b/details.json?language=en-US
```

Le corps de réponse fournit les métadonnées et informations suivantes :

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1467043225642:-1066997140",
    "version": "1",
    "alert_id": "cf63821f-9521-3f27-92ec-e1562ccd469b",
    "expire_time_gmt": 1467043285,
    "status_code": 200
  },
  "alertDetail": {
    "key": "cf63821f-9521-3f27-92ec-e1562ccd469b",
    "class": "bulletin",
    "msg_type_cd": 2,
    "msg_type": "Update",
    "pil": "NPW",
    "phenomena": "HT",
    "significance": "Y",
    "etn": "0003",
    "office_cd": "KSGX",
    "office_name": "San Diego",
    "office_st_cd": "CA",
    "office_cntry_cd": "US",
    "event_desc": "Heat Advisory",
    "severity_cd": 3,
    "severity": "Moderate",
    "categories": [
      {
        "category": "Met",
        "category_cd": 2
      }
    ],
    "response_types": [
      {
        "response_type": "Execute",
        "response_type_cd": 4
      }
    ],
    "urgency": "Expected",
    "urgency_cd": 2,
    "certainty": "Likely",
    "certainty_cd": 2,
    "effective_dt_tm_local": null,
    "effective_dt_tm_tz_abbrv": null,
    "expire_dt_tm_local": "2016-06-29T20:00:00-07:00",
    "expire_dt_tm_tz_abbrv": "PDT",
    "expire_time_gmt": 1467255600,
    "onset_dt_tm_local": null,
    "onset_dt_tm_tz_abbrv": null,
    "flood": null,
    "area_type": "Z",
    "lat": 33.48,
    "lon": -117.29,
    "area_id": "CAZ048",
    "area_name": "San Bernardino and Riverside County Valleys",
    "st_cd": "CA",
    "st_name": "California",
    "cntry_cd": "US",
    "cntry_name": "UNITED STATES OF AMERICA",
    "headline_text": "Heat Advisory until 8PM PDT WED",
    "source": "National Weather Service",
    "disclaimer": null,
    "issue_dt_tm_local": "2016-06-27T04:38:50-07:00",
    "issue_dt_tm_tz_abbrv": "PDT",
    "identifier": "e234b6f889bf9a91c5d9f309db63eaa0",
    "proc_dt_tm_local": "2016-06-27T04:38:58-07:00",
    "proc_dt_tm_tz_abbrv": "PDT",
    "texts": [
      {
        "language_cd": "en-US",
        "description": ".HIGH PRESSURE ALOFT WILL REMAIN IN PLACE THROUGH TUESDAY...THEN\nSLOWLY WEAKEN INTO NEXT WEEKEND. THIS WILL MAKE FOR VERY HOT\nAFTERNOONS IN THE MOUNTAINS...DESERTS...AND INLAND EMPIRE THROUGH\nWEDNESDAY. THE PEAK OF THE HEAT IS EXPECTED TUESDAY.* TEMPERATURE...MID AND HIGH CLOUDS WILL KEEP HIGH TEMPERATURES\n  TODAY SLIGHTLY LESS HOT THAN SUNDAY...THEN WARMING FOR TUESDAY\n  WITH HIGH TEMPERATURES 108 TO 114 IN THE LOWER DESERTS...100 TO\n  106 IN THE UPPER DESERTS...AND 98 TO 105 IN THE INLAND EMPIRE.\n\n* IMPACTS...HEAT ILLNESS POSSIBLE FOR THOSE PEOPLE MOST AT \n  RISK...INCLUDING CHILDREN...THE ELDERLY...AND THOSE WITH \n  CHRONIC ILLNESS. PETS ARE ALSO VULNERABLE TO HEAT ILLNESS.",
        "instruction": "TO REDUCE RISK DURING OUTDOOR WORK THE OCCUPATIONAL SAFETY AND\nHEALTH ADMINISTRATION RECOMMENDS SCHEDULING FREQUENT REST BREAKS\nIN SHADED OR AIR CONDITIONED ENVIRONMENTS. ANYONE OVERCOME BY\nHEAT SHOULD BE MOVED TO A COOL AND SHADED LOCATION.   HEAT STROKE\nIS AN EMERGENCY - CALL 9 1 1.\n\nTAKE EXTRA PRECAUTIONS IF YOU WORK OR SPEND TIME OUTSIDE. WHEN\nPOSSIBLE... RESCHEDULE STRENUOUS ACTIVITIES TO EARLY MORNING OR\nEVENING.  KNOW THE SIGNS AND SYMPTOMS OF HEAT EXHAUSTION AND HEAT\nSTROKE.  WEAR LIGHT WEIGHT AND LOOSE FITTING CLOTHING WHEN\nPOSSIBLE AND DRINK PLENTY OF WATER.\n\n",
        "overview": null
      }
    ],
    "polygon": null
  }
}
```

## Extraction des données d'almanach
{: #getting_almanac_data}

Vous pouvez exécuter une opération `GET` dans votre application pour extraire des données d'almanach journalières ou mensuelles.
Par exemple, vous pouvez utiliser la demande `GET` suivante pour extraire les informations d'almanach journalières pour la ville d'Atlanta, Géorgie, aux Etats-Unis :

```
https://twcservice.mybluemix.net:443/api/weather/v1/geocode/33.40/-83.42/almanac/daily.json?units=e&start=0112&end=0115
```

Le corps de réponse fournit les métadonnées et informations suivantes :

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1467044012413:-416805755",
    "version": "1",
    "latitude": 33.4,
    "longitude": -83.42,
    "units": "e",
    "expire_time_gmt": 1466157922,
    "status_code": 200
  },
  "almanac_summaries": [
    {
      "class": "almanac",
      "station_id": "095988",
      "station_name": "MONTICELLO",
      "almanac_dt": "0112",
      "interval": "D",
      "avg_hi": 56,
      "avg_lo": 28,
      "record_hi": 71,
      "record_hi_yr": 1974,
      "record_lo": 0,
      "record_lo_yr": 1982,
      "mean_temp": 42,
      "avg_precip": 0.13,
      "avg_snow": 0.1,
      "record_period": 30
    },
    {
      "class": "almanac",
      "station_id": "095988",
      "station_name": "MONTICELLO",
      "almanac_dt": "0113",
      "interval": "D",
      "avg_hi": 56,
      "avg_lo": 28,
      "record_hi": 72,
      "record_hi_yr": 1972,
      "record_lo": 13,
      "record_lo_yr": 1981,
      "mean_temp": 42,
      "avg_precip": 0.12,
      "avg_snow": 0,
      "record_period": 30
    },
    {
      "class": "almanac",
      "station_id": "095988",
      "station_name": "MONTICELLO",
      "almanac_dt": "0114",
      "interval": "D",
      "avg_hi": 56,
      "avg_lo": 28,
      "record_hi": 71,
      "record_hi_yr": 2000,
      "record_lo": 14,
      "record_lo_yr": 1956,
      "mean_temp": 42,
      "avg_precip": 0.13,
      "avg_snow": 0,
      "record_period": 30
    },
    {
      "class": "almanac",
      "station_id": "095988",
      "station_name": "MONTICELLO",
      "almanac_dt": "0115",
      "interval": "D",
      "avg_hi": 56,
      "avg_lo": 28,
      "record_hi": 75,
      "record_hi_yr": 1953,
      "record_lo": 11,
      "record_lo_yr": 1964,
      "mean_temp": 42,
      "avg_precip": 0.12,
      "avg_snow": 0,
      "record_period": 30
    }
  ]
}

```

## Utilisation des services de localisation
{: #using_location_services}

### Demande par nom de ville
Pour demander des informations de localisation pour une ville, vous devez entrer au moins un paramètre de requête, tel qu'un nom de ville, et un paramètre `locationType` pour la ville. Vous pouvez également entrer les paramètres `countryCode` et `adminDistrictCode` pour réduire le nombre de localisations uniques qui peuvent être extraites.

Par exemple, la demande suivante extrait les informations de localisation pour la ville d'Atlanta, Géorgie, Etats-Unis :

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/search?query=Atlanta&locationType=city&countryCode=US&adminDistrictCode=GA&language=en-US
```

Le corps de réponse contient les informations de localisation et les métadonnées.
```
{
  "location": [
    {
      "address": "Atlanta, Georgia, United States",
      "adminDistrict": "Georgia",
      "adminDistrictCode": "GA",
      "city": "Atlanta",
      "longitude": -84.3902,
      "postalCode": "30303",
      "latitude": 33.7491,
      "country": "United States",
      "countryCode": "US"
    }
  ],
  "metadata": {
    "transaction_id": null,
    "format": "json",
    "adminDistrictCode": "GA",
    "total_cache_time_secs": 10800,
    "language": "en-US",
    "generated_time": 1467044888246,
    "locationType": "city",
    "status_code": 200,
    "version": "v3",
    "query": "Atlanta",
    "countryCode": "US"
  }
}
```

### Demande par géocode
Pour demander un ensemble de localisations pour un géocode, vous devez entrer une paire latitude/longitude valide.

Par exemple, la demande suivante extrait les informations de localisation pour les coordonnées géographiques de la ville d'Atlanta, Géorgie, Etats-Unis :

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/point?geocode=34.53%2C-84.50&language=en-US
```

### Demande par code postal
Pour demander un ensemble de localisations par code postal, vous devez entrer une clé postale au format suivant : &lt;code postal&gt;:&lt;code de pays&gt;.

Par exemple, la demande suivante extrait les informations de localisation pour un code postal de la ville d'Atlanta, Géorgie, Etats-Unis :

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/point?postalKey=30339%3AUS&language=en-US
```
