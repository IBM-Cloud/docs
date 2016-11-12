---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilisation d'API REST {{site.data.keyword.weather_short}}
{: #rest_apis}

Vous pouvez utiliser les [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window} pour extraire des données météorologiques. Vous pouvez tester le fonctionnement des API et visualiser immédiatement les résultats pour accélérer la génération de vos applications.
{: shortdesc}

Dans la documentation de référence, cliquez sur **List Operations** pour afficher le détail de chaque opération.
Lorsque vous entrez des paramètres et que vous cliquez sur **Try it out!**, vous pouvez être invité à indiquer vos données d'identification.
Vous devez entrer le nom d'utilisateur et le mot de passe des variables d'environnement
`VCAP_SERVICES`.
Vous trouverez ces informations en ouvrant votre application et en cliquant sur **Environment Variables** dans la table des matières.

**Remarque :** Chaque région est indépendante. Vous ne pouvez pas utiliser les données d'identification qui vous ont été fournies pour le service dans une région pour vous authentifier auprès d'un service d'une autre région.
Si vous n'indiquez pas les données d'identification valides, un message *Unauthorized* (Non autorisé) est généré dans le corps de réponse.

Les API REST vous permettent d'extraire des données météorologiques à partir d'une géolocalisation que vous spécifiez sous forme de coordonnées de longitude et de latitude.
Vous pouvez utiliser les API suivantes.

|**API**                                  |**Description**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location ID}/forecast/hourly/48hour.json`  |Renvoie les prévisions météorologiques heure par heure pour les 48 prochaines heures, pour une géolocalisation, en fonction du format que vous entrez. Vous pouvez entrer une valeur au format `geocode/{latitude}/{longitude}` ou `location/{locationId}`. Les données de prévision heure par heure peuvent contenir jusqu'à 48 prévisions heure par heure pour chaque localisation. Vous devez supprimer toutes les prévisions heure par heure précédentes pour une localisation lorsque vous recevez de nouvelles données.|
|`GET /v1/{geocode or location ID}/forecast/daily/{format}.json`   |Renvoie les prévisions météorologiques jour par jour à 3, 5, 7 ou 10 jours pour une géolocalisation, en fonction du format que vous entrez. Le nombre de jours à extraire est spécifié au format suivant : `3day`, `5day`, `7day` ou `10day`. Vous pouvez entrer une valeur au format `geocode/{latitude}/{longitude}` ou `location/{locationId}`. Chaque prévision journalière peut contenir une prévision diurne, une prévision nocturne et une prévision sous 24 heures. Ces segments sont des objets distincts dans les réponses JSON. Les données de prévision diurne de la prévision journalière ne sont plus disponibles après 15 heures (heure locale). A partir de 15 heures (heure locale), votre application ne doit plus afficher la prévision journalière. |
|`GET /v1/{geocode or location ID}/forecast/intraday/{format}.json`|Renvoie les prévisions météorologiques jour par jour à 3, 5, 7 ou 10 jours par périodes de 6 heures pour une géolocalisation, en fonction du format que vous entrez. Le nombre de jours à extraire est spécifié au format suivant : `3day`, `5day`, `7day` ou `10day`. Vous pouvez entrer une valeur au format `geocode/{latitude}/{longitude}` ou `location/{locationId}`. Chaque prévision journalière peut contenir un segment matin, après-midi, soirée et nuit. Ces segments sont des objets distincts dans les réponses JSON.|
|`GET /v1/{geocode or location ID}/observations.json`              |Renvoie les conditions météorologiques en cours pour une géolocalisation. Vous pouvez entrer une valeur au format `geocode/{latitude}/{longitude}` ou `location/{locationId}`.  Ces observations récentes sont conservées dans la base de données pendant 10 minutes au maximum sur certaines stations d'observation et 24 heures d'observations par station. Les données d'observations sont continuellement mises à jour et remplacées selon la méthode premier entré premier sorti (rotation des données avec l'insertion des dernières observations et le déplacement des observations les plus anciennes dans les archives) sur la base de leur horodatage.|
|`GET /v1/{geocode ou location ID}/observations/timeseries.json`   |Renvoie les observations en cours, et jusqu'à 24 heures d'observations passées, à partir de la date du jour et de l'heure en cours, pour une géolocalisation. Vous pouvez entrer une valeur au format `geocode/{latitude}/{longitude}` ou `location/{locationId}`. Les observations rassemblent des données collectées par des stations d'observation réparties dans le monde et les observations en cours.|
|`GET /v1/{geocode, country code, state, or area}/alerts.json`      |Renvoie des alertes, avertissements, instructions et recommandations d'ordre météorologique émis par National Weather Service (NWS), Environment Canada et MeteoAlarm (Europe), et inclut la traduction des descriptions d'événement, des noms de pays et des titres des alertes dans 49 langues. Vous pouvez indiquer des valeurs au format `geocode/{latitude}/{longitude}`, `country/{countrycode}`, `country/{countrycode}/state/{statecode}`/ ou `country/{countrycode}/area/{areaid}`.|
|`GET /v1/alert/{detail_key}/details.json`                         |Renvoie des alertes, avertissements, instructions et recommandations d'ordre météorologique émis par National Weather Service (NWS), Environment Canada et MeteoAlarm (Europe). Les détails comprennent des informations relatives à l'alerte émise par les autorités météorologiques gouvernementales pour la zone spécifiée et incluent la traduction des descriptions d'événement, des noms de pays et des titres des alertes dans 49 langues. |
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |Renvoie des informations d'almanach journalières (Etats-Unis uniquement) provenant d'observations constatées par des stations météorologiques nationales sur une période qui s'étend de 10 à 30 ans ou plus. Les informations sont collectées et fournies par le National Climatic Data Center (NCDC). Vous pouvez entrer une valeur au format `geocode/{latitude}/{longitude}` ou `location/{PostalLocationId}`.|
|`GET /v1/{geocode or postal code}/almanac/monthly.json`           |Renvoie des informations d'almanach mensuelles (Etats-Unis uniquement) provenant d'observations constatées par des stations météorologiques nationales sur une période qui s'étend de 10 à 30 ans ou plus. Les informations sont collectées et fournies par le National Climatic Data Center (NCDC). Vous pouvez entrer une valeur au format `geocode/{latitude}/{longitude}` ou `location/{PostalLocationId}`.|
|`GET /v3/location/{search or point}`                                  |Offre la possibilité de rechercher un nom de localisation ou un géocode (latitude et longitude) afin d'extraire un ensemble de localisations qui correspondent à la demande. Le service de localisation prend en charge la recherche par nom de ville ou code postal.|
*Tableau 1. {{site.data.keyword.weather_short}} Récapitulatif des API*

## Prévisions journalières et intrajournalières
{: #daily_intraday}
L'API de prévision journalière peut contenir plusieurs jours de prévisions journalières pour chaque localisation.
Chaque jour d'une prévision peut contenir jusqu'à trois prévisions distinctes. Pour n'importe quel jour de prévision donné, l'API peut renvoyer des prévisions de jour, de nuit et sur 24 heures.


L'API de prévision intrajournalière peut contenir plusieurs jours de prévisions journalières pour chaque localisation.
Chaque jour d'une prévision contient quatre prévisions distinctes sur 6 heures pour le matin (de 7h à 13h), l'après-midi (de 13h à 19h), le soir (de 19h à 1h) et la nuit (de 1h à 7h).
La structure de la prévision intrajournalière est semblable à celle de la prévision journalière.

Chaque segment est composé d'un numéro, du jour de la semaine et du segment de la journée. Ainsi, l'exemple suivant illustre l'ordre des zones de données et les valeurs de données pour `num`, `dow` et `daypart_name`, pour une prévision qui est générée par les API un jeudi matin :
* 1, Jeudi, Matin
* 2, Jeudi, Après-midi
* 3, Jeudi, Soir
* 4, Jeudi, Nuit
* 5, Vendredi, Matin
* 6, Vendredi, Après-midi
* 7, Vendredi, Soir
* 8, Vendredi, Nuit

## Conditions en cours et données des séries temporelles observées
{: #time_series}

Les conditions en cours et les données des séries temporelles observées fournissent des informations sur la température, les précipitations, le vent,
la pression barométrique, la visibilité, le rayonnement ultraviolet (UV) et d'autres données d'observation complémentaires, y compris les stations d'observation, l'heure et la date des observations, des icônes et de brèves descriptions. La différence entre les séries temporelles observées et les observations en cours est la période d'observation, la réponse consistant en un ou plusieurs ensembles de données.

Les conditions en cours sont les dernières observations demandées, sans paramètre de temps, pour une localisation. Un seul ensemble de données est renvoyé. Les séries temporelles observées comprennent les observations réalisées pendant les 24 dernières heures au maximum pour la localisation demandée.

Les observations récentes sont conservées dans la base de données principale pendant 48 heures (2 jours) au maximum sur certaines stations. Les données d'observations sont continuellement mises à jour et remplacées selon la méthode premier entré premier sorti (rotation des données avec l'insertion des dernières observations et le déplacement des observations les plus anciennes dans les archives) sur la base de leur horodatage. La quantité de données conservées et disponibles sur une station peut être supérieure à 24 rapports d'observation individuels. Le nombre
d'observations est déterminé par leur type.

## Titres et détails des alertes
{: #alerts_levels}
Les API d'alerte renvoient des titres relatifs à des alertes météorologiques actives concernant des orages, des tornades, des tremblements de terre et des inondations.
Ces API renvoient également des alertes non météorologiques, comme des alertes relatives à des enlèvements d'enfant et des avertissements émis par la police.

**Remarque** : Cette API est disponible uniquement aux Etats-Unis, au Canada et en Europe.

L'API Titres d'alerte fournit une valeur de clé dans l'attribut `detail_key` qui permet d'accéder aux détails de l'alerte dans l'API Détails d'alerte.
Lancez une requête sur l'API Titres d'alerte dans le but d'obtenir la valeur `detail_key`, puis utilisez cette dernière pour extraire la réponse de l'API Détails d'alerte à l'aide de cette valeur.

**Remarque** : Vous devez afficher l'attribution de source de données pour n'importe quelles données d'alerte affichées dans votre application.

Les informations suivantes doivent être affichées lors de la phase d'attribution :

*Emis par <Nom du bureau> - &lt;Code de division administrative du bureau&gt;, &lt;Code de pays du bureau&gt;, &lt;Source&gt;, &lt;Clause de protection&gt;*

Par exemple :
* Emis par National Weather Service - Bismarck, USA
* Emis par Central Institute for Meteorology and Geodynamics, Autriche, EMETNET-Meteoalarm

## Informations d'almanach
{: #almanac_details}
L'API Almanach nécessite un ID de localisation et un type de localisation (ville ou code postal) ou une paire latitude/longitude pour extraire les informations relatives à une localisation spécifique.

Lorsque vous utilisez `location` dans l'URL, la localisation doit inclure un ID de localisation (code postal) avec un type de localisation et un code de pays. Lorsque vous utilisez `geocode` dans l'URL, la localisation recherchée doit être une combinaison latitude/longitude valide.

L'API Almanach utilise des paramètres pour spécifier des données journalières ou mensuelles, une date spécifique ou une plage de dates d'informations, et les unités de mesure dans lesquelles les données renvoyées sont exprimées.

Les paramètres de date sont `start` et `end`. Le paramètre `start` est requis, mais le paramètre `end` est facultatif. Lorsque les paramètres sont utilisés conjointement, la combinaison renvoie une plage de dates à la place d'un mois ou d'un jour de données spécifique.

Le format de date pour l'extraction des résultats d'almanach journaliers est une valeur numérique à quatre chiffres qui représente le mois et le jour des données requises, à savoir, MMJJ. Les jours à un seul chiffre **doivent** être précédés d'un zéro, par exemple, 01.

Le format de date pour l'extraction des résultats d'almanach mensuels représente le mois, à savoir, MM. Les mois à un seul chiffre **doivent** être précédés d'un zéro (0), par exemple, 01. Tout autre format génère une erreur d'API et aucune donnée n'est renvoyée.

**Remarque** : Si vous n'indiquez pas de valeur de date dans la demande, le système renvoie l'erreur Demande incorrecte (400). L'API ne propose pas de valeur par défaut.

## Construction de l'URL
{: #url_construction}

Les API REST utilisent une structure d'URL et des paramètres de requête communs pour demander et filtrer les données météorologiques.
Les URL transmises aux API ont le format suivant :

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/<latitude>/<longitude>/<product group>/<date>/<format>&units={units code}&language={language code}
```

Par exemple :

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/33.40/83.42/forecast/daily/3day.json?units=m&language=en-US
```

|**Attribut**     |**Description**                                    |
|------------------|---------------------------------------------------|
|`hostname`        |Chemin de l'URL hébergée. For example, `https://twcservice.mybluemix.net:443/api/weather`.|
|`version`         |Itération actuelle. Par exemple, `v1`.|
|`location`        |Géocode ou ID de localisation. Le groupe de localisation peut être `geocode` ou `location`. Par exemple, `geocode/45.4214/75.6919` représente Ottawa, Canada. Si vous entrez des coordonnées géographique, l'API renvoie des données pour la localisation disponible la plus proche. Les points sont des séparateurs décimaux et les virgules servent à séparer la latitude et la longitude. Si vous entrez un géocode, la latitude et la longitude effectivement utilisées sont renvoyées dans les métadonnées de la réponse.|
|`product group`   |Produit. Par exemple, `observations` ou `forecast`. Un sous-groupe de produit, par exemple, `historical`, est facultatif.|
|`date`            |Type de date. Par exemple, `daily` ou `monthly`.|
|`format`          |Format. Par exemple, `3day`, `5day`, `7day` ou `10day`.|
|`units`           |(Facultatif) Unité qui doit être utilisée dans la réponse. L'API prend en charge les unités de mesure suivantes : English (e), Metric (m) et UK-Hybrid (h). Si vous entrez le paramètre d'unité de mesure sans définir sa valeur, l'API renvoie les données dans l'unité qui correspond au code de langue. L'unité de mesure par défaut ou demandée est renvoyée dans le paramètre d'unité des métadonnées de la réponse.|
|`language`        |La langue dans laquelle la réponse doit être renvoyée. La valeur par défaut est en-US. La langue par défaut ou demandée est renvoyée dans le paramètre de langue des métadonnées de la réponse.|
*Tableau 2. Détails d'URL*

**Remarque** : Les API REST utilisent la norme ISO 3166 pour les codes de pays. Pour plus d'informations, voir
[ISO Standard Online Browsing Platform](https://www.iso.org/obp/ui/#search/code/){:new_window}.
Les API utilisent le système de référence de coordonnées géographiques WGS84. Pour plus d'informations, voir
[Basic Geo Vocabulary](https://www.w3.org/2003/01/geo/){:new_window}.

## Codes et images d'icône
{: #icon_code_images}

Lorsque les API REST {{site.data.keyword.weather_short}} renvoient un code d'icône dans la réponse, vous pouvez utiliser ce code pour déterminer l'image d'icône à afficher dans votre application.
Il existe une relation un-à-un entre le code d'icône dans la réponse d'API et le nom de fichier de l'image d'icône.
Par exemple, si la réponse d'API contient un `code_icône` égal à 1, vous pouvez utiliser le nom de fichier `01.png` pour afficher l'image d'icône correspondante.


Dans votre code, vous pouvez créer une fonction qui utilise le `code_icône` pour déterminer l'URL de l'image d'icône.
Par exemple :

```
function getIconURL(code) {
    return "images/weathericons/icon" + code + ".png";
}
```

Le tableau ci-après contient des codes, des descriptions et des images d'icône qui peuvent être utilisés avec les API REST {{site.data.keyword.weather_short}}. Le tableau indique si une icône est utilisée dans les API Prévision ou Observation et si l'icône est disponible dans les segments de prévision nuit ou jour.


|**Code**|**Description**|**Image**|**Syntaxe d'API** |**Nuit ou jour**|
|----|--------------------------|------------|------------|--------------------|
| 0  | Tornade                  | <img src="images/00.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Nuit et jour |
| 1  | Tempête tropicale           | <img src="images/01.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 2  | Ouragan                | <img src="images/02.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Nuit et jour |
| 3  | Fortes tempêtes            | <img src="images/03.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Nuit et jour |
| 4  | Tonnerre et grêle         | <img src="images/04.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 5  | Pluie à averses de neige     | <img src="images/05.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 6  | Pluie/Grésil             | <img src="images/06.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 7  | Mélange neige/grésil hivernal  | <img src="images/07.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 8  | Bruine verglaçante         | <img src="images/08.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 9  | Bruine                  | <img src="images/09.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 10 | Pluie givrante            | <img src="images/10.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 11 | Pluie légère               | <img src="images/11.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 12 | Pluie                     | <img src="images/12.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 13 | Averses éparses       | <img src="images/13.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 14 | Neige légère               | <img src="images/14.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 15 | Poudrerie basse/élevée  | <img src="images/15.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 16 | Neige                     | <img src="images/16.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 17 | Grêle                     | <img src="images/17.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 18 | Neige fondue                    | <img src="images/18.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 19 | Tourbillons de poussière/Tempête de sable | <img src="images/19.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 20 | Brumeux                    | <img src="images/20.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 21 | Brouillard/Venteux             | <img src="images/21.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 22 | Brume/Venteux            | <img src="images/22.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 23 | Légèrement venteux                   | <img src="images/23.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Nuit et jour |
| 24 | Embruns/Venteux    | <img src="images/24.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 25 | Froid/Crystaux de glace    | <img src="images/25.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 26 | Nuageux                   | <img src="images/26.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 27 | Plutôt nuageux            | <img src="images/27.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 28 | Plutôt nuageux            | <img src="images/28.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Jour          |
| 29 | Partiellement nuageux            | <img src="images/29.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit       |
| 30 | Partiellement nuageux            | <img src="images/30.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Jour          |
| 31 | Clair                    | <img src="images/31.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit       |
| 32 | Ensoleillé                     | <img src="images/32.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Jour          |
| 33 | Beau/Plutôt clair      | <img src="images/33.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit       |
| 34 | Beau/Plutôt ensoleillé      | <img src="images/34.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Jour          |
| 35 | Mélangde de pluie et de grêle        | <img src="images/35.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Jour          |
| 36 | Chaud                      | <img src="images/36.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Jour          |
| 37 | Orages isolés   | <img src="images/37.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Jour          |
| 38 | Orages            | <img src="images/38.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 39 | Averses éparses        | <img src="images/39.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Jour          |
| 40 | Forte pluie               | <img src="images/40.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 41 | Averses de neige éparses   | <img src="images/41.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Jour          |
| 42 | Neige abondante               | <img src="images/42.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
| 43 | Tempête de neige                 | <img src="images/43.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Nuit et jour |
| 44 | Non disponible (N/A)      | <img src="images/44.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Nuit et jour |
| 45 | Averses éparses        | <img src="images/45.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Nuit       |
| 46 | Averses de neige éparses   | <img src="images/46.png " width="100" height="100" alt="Image d'icône."/>| Prévision                | Nuit       |
| 47 | Orages épars  | <img src="images/47.png " width="100" height="100" alt="Image d'icône."/>| Prévision et Observations | Nuit et jour |
*Tableau 3. Codes et images d'icône*

Vous pouvez télécharger cet ensemble d'icônes météorologiques sous la forme de fichiers [PNG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_png.zip){:new_window}
ou [SVG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_svg.zip){:new_window} et les utiliser dans votre application. 

Vous pouvez également télécharger l'[ensemble d'icônes](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} utilisé par
l'[application de démonstration {{site.data.keyword.weather_short}}](http://weather-company-data-demo.{APPDomain}){: new_window}. 

## Unités de mesure
{: #units_measure}

Lors de l'utilisation des API REST, il n'est pas nécessaire de transmettre explicitement une unité de mesure. Par défaut, elles utilisent l'unité de mesure associée au code de langue dans l'URL. Cependant, si vous souhaitez utiliser une unité de mesure différente de celle par défaut, l'unité transmise remplace celle par défaut.

* Pour le code en-US ou en, l'unité de mesure par défaut est English/Imperial. Le code d'unité est `e`.
* Pour en-GB, l'unité de mesure par défaut est Hybrid-UK. Le code d'unité est `h`.
* Pour tout le reste, l'unité de mesure par défaut est Metric. Le code d'unité est `m`.

## Traduction dans différentes langues
{: #language_translation}

Les API REST traduisent le texte et les unités de mesure. Lorsque vous créez une URL de demande, vous devez choisir une langue valide.
Les zones suivantes font l'objet d'une traduction :

|**Zone**           |**Description**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |Bulletin pour une période de 24 heures|
|`dow`               |Jour de la semaine|
|`wind_phrase`       |Brève description de la direction et de la vitesse du vent pour une période de 12 heures|
|`wdir_cardinal`     |Direction cardinale moyenne du vent pendant la journée|
|`daypart_name`      |Nom d'une période de 12 heures, sans le jour de la semaine, pour les 48 premières heures|
|`temp_phrase`       |Brève description comprenant les températures minimale et maximale prévues pour une période de 12 heures|
|`shortcast`         |Eléments climatiques du bulletin sous forme condensée|
|`long_daypart_name` |Nom de la période de la prévision météorologique valide, sous forme développée. La période peut être de 12 ou de 24 heures.|
|`golf_category`     |Phrase indiquant la catégorie de l'index à prendre en compte pour le golf, calculée à partir des conditions météorologiques|
|`phrase_nnchar`     |Brève description des éléments climatiques de la journée|
|`lunar_phrase`      |Code à trois caractères correspondant aux phases de la lune|
|`uv_desc`           |Description de l'indice UV, apportant des informations complémentaires par rapport à l'indice seul, en lui associant un niveau de risque cutané en cas d'exposition|
|`wx_phrase`         |Description des conditions météorologiques observées par la station.|
|`pressure_desc`     |Phrase qui décrit le changement constaté sur le relevé de pression barométrique au cours de l'heure qui vient de s'écouler.|
|`headline_text`     |Texte du titre d'un événement pour la localisation.|
|`event_desc`        |Description d'un événement.|
|`cntry_name`        |Nom du pays dans lequel un événement s'est produit, indiqué en majuscules et en minuscules.|
*Tableau 4. Zones de réponse traduites*

## Gestion des zones dont les données sont null ou manquantes dans la réponse des API
{: #handling_null_or_missing}

Si une zone de données est null car les données ne sont pas disponibles, les API REST renvoient les balises de la zone avec le mot `null`, ou elles ne renvoient pas la zone. 

## Gestion des erreurs
{: #handling_errors}

Les codes d'erreur suivants sont communs à toutes les API :

|**Erreur** |**Description**                                    |
|----------|---------------------------------------------------|
|400       |Demande non valide. La demande n'a pas été comprise par le serveur à cause d'une erreur de syntaxe. Ce code d'erreur est implémenté pour toutes les API. En cas de paramètres non valides, l'API rejette la demande.|
|401       |Non autorisé. La demande nécessite une authentification.|
|403       |Interdit. Le serveur a compris la demande mais refuse de la traiter.|
|404       |Introuvable. En l'absence d'un paramètre requis dans la demande d'API, une erreur MissingParameterException avec un code d'erreur 404 est renvoyée.|
|500       |Erreur interne du serveur. Une condition inattendue s'est produite sur le serveur et l'a empêché de traiter la demande.|
*Tableau 5. Code de réponse d'erreur*

La réponse en cas d'erreur est toujours la même. Une seule réponse peut contenir plusieurs codes d'erreur.
Exemple de réponse renvoyée pour une erreur JSON :

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
