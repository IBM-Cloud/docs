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
{: #gettingstartedtemplate}
*Dernière mise à jour : 13 mai 2016*

{{site.data.keyword.iotmapinsights_full}} permet aux développeurs
d'activer facilement leurs applications en vue de l'utilisation de fonctions
géospatiales, comme l'utilisation des données d'une carte et la recherche du
chemin le plus court basée sur les réseaux routiers du monde entier.
{:shortdesc}

Vous pouvez utiliser les fonctions suivantes grâce à l'API REST de
{{site.data.keyword.iotmapinsights_short}} :

- Mise en correspondance de carte haute précision qui utilise la
géométrie du réseau routier
- Manipulation des événements en temps réel sur une carte, comme la
circulation 
- Recherche dynamique du chemin le plus court (recherche de trajet) en
tenant compte des événements en temps réel comme la circulation 
- Extraction des données de géométrie de route qui peuvent être
utilisées pour le dessin des formes de route sur une carte 

Le service {{site.data.keyword.iotmapinsights_short}}
utilise les données du réseau routier, en coordonnées WGS84, qui sont extraites
d'OpenStreetMap. Seules les routes pouvant être empruntées par un véhicule sont
utilisées pour l'analyse. 

Les régions de carte prises en charge sont les suivantes :

- Europe (map_id=1)
- Afrique (map_id=2)
- Asie (map_id=3)
- Australie-Océanie (map_id=4)
- Amérique du Nord (map_id=5)
- Amérique Centrale (map_id=6)
- Amérique du Sud (map_id=7)


Suivez la procédure ci-après pour utiliser les fonctions analytiques du
service {{site.data.keyword.iotmapinsights_short}}.

## Utilisation de {{site.data.keyword.iotmapinsights_short}}
pour la mise en correspondance de carte

1. Préparez un ensemble de données de coordonnées GPS brutes à analyser. 
2. Envoyez les données de coordonnées GPS brutes dans l'ordre d'une série
temporelle au service {{site.data.keyword.iotmapinsights_short}} via l'API
REST `mapMatching`. Vous pouvez, si vous le
souhaitez, définir un angle de tête de chaque position en degrés (Nord = 0,
angle dans le sens horaire) pour indiquer la direction du trajet.
3. Recevez les coordonnées mises en correspondance avec la carte et
les informations sur les tronçons de route en réponse à l'appel de l'API
REST `mapMatching`.
4. Vous pouvez, si vous le souhaitez, extraire les données de
forme de route du tronçon de route mis en correspondance avec la carte à l'aide
de l'API `getLinkInformation`. Appelez l'API REST
`getLinkInformation` avec un ID de tronçon pour obtenir une
série de coordonnées qui constituent une forme de route. 

## Utilisation de {{site.data.keyword.iotmapinsights_short}}
pour la recherche de trajet

1. Déterminez des positions de début et de fin pour lesquelles vous
souhaitez obtenir le chemin le plus court.
2. Envoyez les données de début et de fin au service
{{site.data.keyword.iotmapinsights_short}} à l'aide de l'API REST
`routeSearch`. Vous pouvez, si vous le souhaitez, définir un
angle de tête de chaque position en degrés (Nord = 0, angle dans le sens
horaire) pour indiquer la direction du trajet.
3. Recevez une liste de tronçons de route en réponse à l'appel de
l'API REST `routeSearch`. Vous pouvez dessiner la forme du
chemin trouvé sur une carte en utilisant les données de forme incluses dans les
données du résultat. 

## Utilisation de {{site.data.keyword.iotmapinsights_short}}
pour la manipulation d'événement de circulation 

1. Déterminez un type et une position d'un événement de circulation à
créer. 
2. Envoyez les informations relatives à cet événement de circulation au
service {{site.data.keyword.iotmapinsights_short}} à l'aide de
l'API REST `createEvent`.
3. Recevez un ID de l'événement de circulation créé en
réponse à l'appel de l'API REST `createEvent`.
4. Recherchez les événements de circulation dans une zone rectangulaire
spécifique et éventuellement avec un type d'événement de circulation donné à
l'aide de l'API REST `queryEvent`.

- Si vous le souhaitez, supprimez un événement de circulation qui n'est
plus valide à l'aide de l'API REST `deleteEvent`.
- Si vous le souhaitez, procédez à l'extraction d'une zone sur la route
affectée par un événement de circulation à l'aide de l'API REST `getAffectedLinksInformation`.


# Liens connexes
{: #rellinks}
## Tutoriels et exemples
{: #samples}
* [Tutoriel - Partie 1 - {{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}}](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [Tutoriel - Partie Z - {{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}}](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

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

