---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Initiation à {{site.data.keyword.iotmapinsights_short}}
{: #iotdriverinsights_index}
Dernière mise à jour : 22 juin 2016
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} est un service sur {{site.data.keyword.Bluemix}} que vous pouvez utiliser pour activer dans vos applications des fonctions géospatiales telles que la mise en correspondance de carte et la recherche du chemin le plus court sur des réseaux routiers à travers le globe.  
{:shortdesc}

Les fonctions suivantes sont disponibles via l'API REST de {{site.data.keyword.iotmapinsights_short}} :

|Fonction|Utilisation...|
|:---|:---|
|Mise en correspondance de carte à haute précision|Mise en correspondance de votre position GPS avec le réseau routier réel cartographié|
|Extraction des données de géométrie de route|Extraction du réseau routier cartographié pour dessin de formes de route sur une carte|
|Recherche dynamique de l'itinéraire le plus court|Recherche de l'itinéraire le plus court en intégrant les événements en temps réel tels que le trafic|
|Manipulation des événements du trafic en temps réel|Ajout à la carte d'événements en temps réel (par exemple, des conditions de circulation), pour améliorer la planification d'itinéraire|

## Avant de commencer
{: #byb}

1. Lorsque vous ajoutez une instance du service depuis le [catalogue {{site.data.keyword.Bluemix_notm}}](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}, vérifiez qu'il n'est pas lié à une application et notez les valeurs de l'ID de locataire, de nom d'utilisateur et de mot de passe générés automatiquement. Vous en aurez besoin plus tard pour accéder au service via l'API {{site.data.keyword.iotmapinsights_short}}.

2. Familiarisez-vous avec [OpenStreetMap](http://www.openstreetmap.org/){: new_window}.  

 Le service {{site.data.keyword.iotmapinsights_short}} utilise les données du réseau routier, sous forme de coordonnées WGS84, extraites depuis [OpenStreetMap](http://www.openstreetmap.org/){: new_window}. Seules les routes sur lesquelles une voiture peut circuler sont utilisées pour l'analyse.  

 Les régions cartographiques suivantes sont prises en charge :

|Région|ID de carte|
|:---|:---|
|Europe|map_id=1|
|Afrique|map_id=2|
|Asie|map_id=3|
|Australie - Océanie|map_id=4|
|Amérique du Nord|map_id=5|
|Amérique Centrale|map_id=6|
|Amérique du Sud|map_id=7|

## Mise en correspondance de carte
{: #map_matching}
Pour mapper des coordonnées GPS brutes à des coordonnées cartographiées, procédez comme suit :

1. Préparez un ensemble de coordonnées GPS brutes à analyser. 
2. Envoyez les cordonnées GPS brutes à l'aide de la commande `mapMatching`. Vous pouvez, si vous le désirez, définir un cap en degrés depuis chaque position pour spécifier la direction du déplacement.
 - Requête : données GPS brutes
 - Réponse : données GPS cartographiées, ID de lien
3. Facultatif : obtention du type de route à l'aide de la commande d'API `getLinkInformation`. Vous pouvez extraire les données de forme de
route correspondantes sous forme d'une série de coordonnées via l'API REST `getLinkInformation`.
 - Requête : ID de lien
 - Réponse : type de route

## Recherche d'itinéraire
{: #route_searching}

Extrayez les informations de l'itinéraire le plus court entre les coordonnées d'origine et de destination spécifiées en procédant comme suit :

1. Déterminez une position de départ et d'arrivée pour l'itinéraire le plus court.
2. Envoyez les coordonnées de départ et d'arrivée via l'API REST `routeSearch`.
Indiquez, si vous le désirez, un cap en degrés depuis chaque position pour spécifier la direction du déplacement.
 - Requête : coordonnées de l'origine et de la destination
 - Réponse : itinéraire le plus court cartographié

Utilisez les données de la forme de lien renvoyée pour tracer la forme de l'itinéraire identifié sur une carte.

## Ajout d'événements de trafic
{: #traffic_events}

Pour ajouter des informations d'événements de trafic au service {{site.data.keyword.iotmapinsights_short}}, procédez comme suit :

1. Choisissez le type et la position de l'événement de trafic que vous désirez créer.
2. Injectez l'événement via la commande d'API `createEvent`.
Envoyez les informations de l'événement de trafic au service {{site.data.keyword.iotmapinsights_short}}.
 - Requête : informations d'événement
 - Réponse : ID d'événement
3. Recherchez des événements via la commande d'API REST `queryEvent`.
Recherchez des événements de trafic survenus dans une zone rectangulaire donnée, et éventuellement correspondant à un événement de trafic spécifique.
 - Requête : informations de zone.
 - Réponse : informations d'événements.  
4. Facultatif : supprimez un événement de trafic qui n'est plus valide à l'aide de la commande d'API `deleteEvent`.
5. Facultatif : identifiez une zone sur la route affectée par un événement de trafic à l'aide de la commande d'API
`getAffectedLinksInformation`.

# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}

* [Tutoriel - Partie 1 - {{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}}](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [Tutoriel - Partie Z - {{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}}](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive Starter Application](https://iot-automotive-starter.mybluemix.net){:new_window}

## Référence d'API
{: #api}

* [Documentation des API](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## Liens connexes
{: #general}

* [Initiation à {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Initiation à {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [dW Answers sur IBM developerWorks](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Dépassement de pile](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [Nouveautés dans les services Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}
* [&copy; OpenStreetMap contributors](http://www.openstreetmap.org/copyright){:new_window}
* [Open Data Commons Open Database License (ODbL)](http://opendatacommons.org/licenses/odbl/){:new_window}
