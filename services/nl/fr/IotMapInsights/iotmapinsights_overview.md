---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# A propos de {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}

Le service {{site.data.keyword.iotmapinsights_short}} repose
sur les données du réseau routier stockées dans la mémoire cache. Il offre un
accès à haute vitesse aux données statiques du réseau routier, aux
données d'événement dynamiques et aux outils géospatiaux basés sur le réseau routier qui
permettent à votre application d'intégrer des fonctionnalités géospatiales.
{:shortdesc}

## Requête sur les données de carte statiques
{: #static_map_data_query}

Pour accéder aux données d'attribut de tronçon de route, le service
{{site.data.keyword.iotmapinsights_short}} fournit une interface
API REST de requête de tronçon. Cette dernière reçoit un ID de tronçon sous forme de
paramètre pouvant être identifié par une fonction de mise en correspondance de
carte et renvoie des informations détaillées sur le tronçon demandé, comme le
type de route, sa longueur, un tableau précis des points de forme, les noeuds
adjacents, ainsi que les tronçons adjacents. Grâce aux informations
détaillées relatives au tronçon, votre application peut traverser un réseau de
tronçons routiers en observant les informations sur les tronçons adjacents. 

## Données d'événement dynamiques
{: #dynamic_event_data}

Dans le service {{site.data.keyword.iotmapinsights_short}}, un
événement est un modèle d'objet d'événement de circulation placé dynamiquement
sur un tronçon routier spécifique. L'événement est doté des attributs de base
d'un événement de circulation, comme les coordonnées GPS, l'heure, le type, la
durée de l'événement et la longueur concernée. Vous pouvez injecter et
supprimer des événements de manière dynamique. 

## Injection et suppression d'événement
{: #inject_event}

L'interface API REST d'injection d'événement vous permet de stocker un
événement sur une carte. Pour injecter un événement, vous pouvez envoyer les
informations relatives à l'événement à l'interface avec un type d'événement
défini afin de classifier les événements et leurs attributs en fonction de
l'utilisation souhaitée de votre application. L'interface API REST de
suppression d'événement vous permet de supprimer des événements de la carte
afin de pouvoir gérer les événements passés. 

## Requête d'événement
{: #query_event}

L'interface API REST de requête d'événement vous permet de lancer une
requête sur des événements avec des conditions indiquées définies sous forme de
paramètres de demande. Dans une condition de requête, vous pouvez définir la
zone avec une plage de longitudes et de latitudes, ainsi que des attributs
d'événement pour affiner les événements cible renvoyés dans la réponse à la
demande.

## Outils géospatiaux
{: #geospatial_tools}

En guise d'outils géospatiaux, le service
{{site.data.keyword.iotmapinsights_short}} fournit une API REST
pour la mise en correspondance de carte et les fonctions de recherche de
trajet.

## Mise en correspondance de carte
{: #map_matching}

Si les données GPS des périphériques ne sont pas assez précises pour
l'analyse ou la visualisation, ou si les attributs du réseau de tronçons de
route sont requis pour votre application, vous pouvez utiliser l'interface API
REST de mise en correspondance de carte. Cette API permet à votre application
d'adapter un point de données GPS brut à un point mis en correspondance sur le
tronçon de route. Elle reçoit un point défini par des données de coordonnées
GPS de longitude et de latitude et renvoie un point mis en correspondance avec
la carte. Ce point est analysé grâce à l'examen des données d'historique de
chaque véhicule pendant une période donnée qui vise à trouver le point le plus
probable en temps réel. Pour les points dépourvus de données de localisation
historiques, l'interface de mise en correspondance de carte renvoie le point le
plus proche sur le tronçon de route à partir du point GPS demandé. 

## Recherche de trajet
{: #route_search}

Si vous avez besoin d'implémenter une application avec des fonctions
géospatiales, vous devez rechercher le chemin le plus court entre deux points. L'interface
API REST de recherche de trajet du service
{{site.data.keyword.iotmapinsights_short}} calcule le chemin le plus
court entre les coordonnées GPS du point de départ et celles du point
d'arrivée. Les coordonnées reçues sont mises en correspondance avec le tronçon
le plus proche de la carte grâce à la fonction de mise en correspondance de
carte, et le chemin le plus court entre ces points mis en correspondance avec la
carte est calculé. 

## Recherche de tronçon affecté
{: #link_search}

Lorsqu'un événement se produit sur un route, il est susceptible
d'affecter plusieurs tronçons de route. Vous pouvez utiliser des API REST pour
rechercher les tronçons affectés et les tronçons de route sur lesquels les
véhicules risquent de rencontrer l'événement. Cette recherche tient compte de la
distance des véhicules par rapport à l'événement, mais aussi de la topologie du
réseau routier. 

