---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilisation des API REST d'Insights for Weather
{: #rest_apis}

*Dernière mise à jour : 6 avril 2016*

Vous pouvez utiliser les [API REST d'Insights for Weather](https://twcservice.{APPDomain}/rest-api/){:new_window} pour extraire des données météorologiques. Vous pouvez tester le fonctionnement des API et visualiser immédiatement les résultats pour accélérer la génération de vos applications.

Dans la documentation de référence, cliquez sur **List Operations** pour afficher le détail de chaque opération.
Lorsque vous entrez des paramètres et que vous cliquez sur **Try it out!**, vous pouvez être invité à indiquer vos données d'identification.
Vous devez entrer le nom d'utilisateur et le mot de passe des variables d'environnement
`VCAP_SERVICES`.
Vous trouverez ces informations en ouvrant votre application et en cliquant sur **Environment Variables** dans la table des matières.

**Remarque :** Chaque région est indépendante. Vous ne pouvez pas utiliser les données d'identification qui vous ont été fournies pour le service dans une région pour vous authentifier auprès d'un service d'une autre région.
Si vous n'indiquez pas les données d'identification valides, un message "Unauthorized" (Non autorisé) est généré dans le corps de réponse.

Les API d'Insights for Weather vous permettent d'extraire des données météorologiques à partir d'une géolocalisation que vous spécifiez sous forme de coordonnées de longitude et de latitude.
Vous pouvez utiliser les API suivantes.

|**API**                                  |**Description**              |
|-----------------------------------------|-----------------------------|
|`GET /v2/forecast/daily/10day`           |Renvoie les prévisions météorologiques relatives à la journée en cours et aux neufs prochains jours pour une géolocalisation. Chaque prévision jour par jour peut contenir une prévision diurne et une prévision nocturne. Ces segments sont des objets distincts dans les réponses JSON. Les données de prévision diurne de la prévision jour par jour ne sont plus disponibles après 15 heures (heure locale). A partir de 15 heures (heure locale), votre application ne doit plus afficher la prévision jour par jour.|
|`GET /v2/forecast/hourly/24hour`         |Renvoie une prévision heure par heure relative à la journée en cours et aux neufs prochains jours pour une géolocalisation. Les données heure par heure comprennent jusqu'à 24 heures de prévisions pour un lieu donné. Vous devez supprimer toutes les précédentes prévisions heure par heure pour un lieu lorsque vous en recevez de nouvelles.|
|`GET /v2/observations/current`           |Renvoie les conditions météorologiques en cours pour une géolocalisation. Ces observations récentes sont conservées dans la base de données pendant 10 minutes au maximum sur certaines stations d'observation et 24 heures d'observations par station. Les données d'observations sont continuellement mises à jour et remplacées selon la méthode premier entré premier sorti (rotation des données avec l'insertion des dernières observations et le déplacement des observations les plus anciennes dans les archives) sur la base de leur horodatage.|
|`GET /v2/observations/timeseries/24hour` |Renvoie les observations en cours, et jusqu'à 24 heures d'observations passées, à partir de la date du jour et de l'heure en cours, pour une géolocalisation. Les observations rassemblent des données collectées par des stations d'observation réparties dans le monde et les observations en cours.|
*Tableau 1. Récapitulatif des API D'Insights for Weather*

## Séries temporelles observées
{: #time_series}

Les données des séries temporelles observées fournissent des informations sur la température, les précipitations, le vent,
la pression barométrique, la visibilité, le rayonnement ultraviolet (UV) et d'autres données d'observation complémentaires, y compris les stations d'observation, l'heure et la date des observations, des icônes et de brèves descriptions. La différence entre les séries temporelles observées et les observations en cours est la période d'observation, la réponse consistant en un ou plusieurs ensembles de données.

Les conditions en cours sont les dernières observations demandées, sans paramètre de temps, pour un lieu. Un seul ensemble de données est renvoyé. Les séries temporelles observées comprennent les observations réalisées pendant les 24 dernières heures au maximum pour un lieu donné.

Les observations récentes sont conservées dans la base de données principale pendant 48 heures (2 jours) au maximum sur certaines stations. Les données d'observations sont continuellement mises à jour et remplacées selon la méthode premier entré premier sorti (rotation des données avec l'insertion des dernières observations et le déplacement des observations les plus anciennes dans les archives) sur la base de leur horodatage. La quantité de données conservées et disponibles sur une station peut être supérieure à 24 rapports d'observation individuels. Le nombre
d'observations est déterminé par leur type.

## Construction de l'URL
{: #url_construction}

Les API d'Insights for Weather utilisent une structure d'URL et des paramètres de requête communs pour demander et filtrer les données météorologiques.
Les URL transmises aux API d'Insights for Weather ont le format suivant :

```
https://twcservice.mybluemix.net/api/weather/v2/<product group>/&format={format type}&geocode={latitude,longitude}&language={language code}&units={units code}

```

|**Attribut**     |**Description**                                    |
|------------------|---------------------------------------------------|
|`hostname`        |Chemin URL de l'hôte (par exemple,
`https://twcservice.mybluemix.net:443/api/weather`)|
|`version`         |Itération en cours (par exemple, "v2")|
|`product group`   |Produit (par exemple, "observations" ou "prévision")|
|`geocode`         |Latitude et longitude (par exemple, "45.4214,75.6919" représente Ottawa, au Canada). Si vous entrez des coordonnées géographique, l'API renvoie des données pour le lieu disponible le plus proche. Les points sont des séparateurs décimaux et les virgules servent à séparer la latitude et la longitude. Si vous entrez un géocode, la latitude et la longitude effectivement utilisées sont renvoyées dans les métadonnées de la réponse.|
|`language`        |La langue dans laquelle la réponse doit être renvoyée. La valeur par défaut est en-US. La langue par défaut ou demandée est renvoyée dans le paramètre de langue des métadonnées de la réponse.|
|`units`           |(Facultatif) Unité qui doit être utilisée dans la réponse. L'API prend en charge les unités de mesure suivantes : English (e), Metric (m) et UK-Hybrid (h). Si vous entrez le paramètre d'unité de mesure sans définir sa valeur, l'API renvoie les données dans l'unité qui correspond au code de langue. L'unité de mesure par défaut ou demandée est renvoyée dans le paramètre d'unité des métadonnées de la réponse.|
*Tableau 2. Détails d'URL*

## Unités de mesure
{: #units_measure}

Lors de l'utilisation des API d'Insights for Weather, il n'est pas nécessaire de transmettre explicitement une unité de mesure. Par défaut, elles utilisent l'unité de mesure associée au code de langue dans l'URL. Cependant, si vous souhaitez utiliser une unité de mesure différente de celle par défaut, l'unité transmise remplace celle par défaut.

* Pour le code en-US ou en, l'unité de mesure par défaut est English/Imperial. Le code d'unité est "e".
* Pour en-GB, l'unité de mesure par défaut est Hybrid-UK. Le code d'unité est "h".
* Pour tout le reste, l'unité de mesure par défaut est Metric. Le code d'unité est "m".

## Traduction dans différentes langues
{: #language_translation}

Les API d'Insights for Weather traduisent le texte et les unités de mesure. Lorsque vous créez une URL de demande, vous devez choisir une langue valide.
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
|`sky_cover`         | Description de la couverture nuageuse basée sur son pourcentage|
|`ptend_desc`        | Description de la tendance de la pression atmosphérique sur les 3 dernières heures|
*Tableau 3. Zones de réponse traduites*

## Gestion des zones dont les données sont null ou manquantes dans la réponse des API
{: #handling_null_or_missing}

Si une zone de données est null car les données ne sont pas disponibles, les API d'Insights for Weather renvoient les balises de la zone avec le mot "null", ou elles ne renvoient pas la zone.

## Gestion des erreurs
{: #handling_errors}

Les codes d'erreur suivants sont communs à toutes les API :

|**Erreur** |**Description**                                    |
|----------|---------------------------------------------------|
|400       |Demande non valide. La demande n'a pas été comprise par le serveur à cause d'une erreur de syntaxe. Ce code d'erreur est implémenté pour toutes les API. En cas de paramètres non valides, l'API rejette la demande.|
|401       |Non autorisé. La demande nécessite une authentification.|
|403       |Interdit. Le serveur a compris la demande mais refuse de la traiter.|
|404       |Introuvable. En l'absence d'un paramètre requis dans la demande d'API, une erreur MissingParameterException avec un code d'erreur 404 est renvoyée.|
|405       |Méthode non autorisée. Par exemple, l'envoi de POST au lieu de GET.|
|406       |Non accepté. Par exemple, les réponses compressées au format gzip ne sont pas acceptées.|
|408       |Dépassement du délai d'attente de la demande. Le client n'a pas envoyé la demande pendant la période d'attente du serveur.|
|500       |Erreur interne du serveur. Une condition inattendue s'est produite sur le serveur et l'a empêché de traiter la demande.|
|502-504   |Service indisponible ou problème de passerelle. Ces codes d'erreur sont renvoyés si le service est temporairement indisponible.|
*Tableau 4. Code de réponse d'erreur*

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
