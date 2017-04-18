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
Dernière mise à jour : 20 juillet 2016
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} est un service sur {{site.data.keyword.Bluemix_notm}} que vous pouvez utiliser pour accès rapide aux
données de réseau routier statique et aux données d'événement dynamiques. {{site.data.keyword.iotmapinsights_short}} fournit également des outils géospatiaux
pour les réseaux routiers, que vous pouvez utiliser pour intégrer des capacités géospatiales dans vos applications.
{:shortdesc}

Le service {{site.data.keyword.iotmapinsights_short}} offre les fonctions suivantes :

- Données de carte statiques
- Données d'événement dynamiques
- Outils géospatiaux

Le service {{site.data.keyword.iotmapinsights_short}} collecte et utilise les données de réseau routier
[OpenStreetMap](http://www.openstreetmap.org/){: new_window} stockées dans le cache du service pour traitement.

Les données d'OpenStreetMap sont rendues disponibles au titre de la licence ODbL (Open Data Common Open Database License) par l'organisme OpenStreetMap
Foundation (OSMF). Pour plus d'informations, voir [OpenStreetMap Copyright and
License](http://www.openstreetmap.org/copyright){: new_window}.

## Données de carte statiques
{: #static_map_data_query}

L'une des caractéristiques principales du produit est la possibilité d'extraire des informations routières détaillées afin de les utiliser dans vos
applications. Utilisez l'interface de l'API REST Link Query pour rechercher des données d'attribut de route de carte statique d'après un ID de lien. Utilisez la
fonction de [mise en correspondance de carte](#map_matching) de {{site.data.keyword.iotmapinsights_short}} pour identifier le paramètre
d'ID de lien requis.

Les données renvoyées incluent les informations suivantes sur l'ID de lien requis :

- Type de route
- Longueur de la route
- Un tableau de formes détaillées par des points
- Des informations sur les noeuds et liens adjacents

En recherchant des informations de liens routiers détaillées, votre application peut sillonner un réseau de liens routiers en utilisant intelligemment
les informations de liens adjacents renvoyées.

## Données d'événement dynamiques
{: #dynamic_event_data}

Outres les données de carte statiques, les conditions de route réelles incluent nécessairement des événements dynamiques tels que les embouteillages et les
travaux. Utilisez {{site.data.keyword.iotmapinsights_short}} pour créer, gérer et incorporer les événements du trafic avec
les [recherches de liens affectés](#link_search) pour planification de l'itinéraire.

### Injection et suppression d'événements
{: #inject_event}

Utilisez l'API REST d'injection d'événement du service {{site.data.keyword.iotmapinsights_short}} pour injecter et supprimer
dynamiquement des événements du trafic sous forme de modèles d'objet de carte placés sur des tronçons routiers spécifiques. Chaque événement inclut des attributs
de base, comme des coordonnées GPS, l'heure de début, le type d'événement, sa durée et la longueur de route affectée.

Utilisez l'interface de l'PI REST de suppression d'événement pour supprimer des événements de la carte lorsqu'ils se sont terminés.

### Requête d'événement
{: #query_event}

Utilisez l'API REST de requête d'événements pour obtenir des informations détaillées sur tous les événements dynamiques affectant une zone géographique
spécifique. Vous pouvez effectuer une recherche sur une zone en indiquant une plage de longitudes et de latitudes, et inclure des attributs d'événement pour
circonscrire le nombre d'événements cible renvoyés.

## Outils géospatiaux
{: #geospatial_tools}

Etoffez votre application avec les fonctions de mise en correspondance de carte et de recherche d'itinéraire fournies par les outils géospatiaux de
{{site.data.keyword.iotmapinsights_short}}.

### Mise en correspondance de carte
{: #map_matching}

Utilisez la fonction de mise en correspondance de carte de l'API REST avec votre application pour mapper les coordonnées GPS effectives
de votre appareil aux données du réseau routier [OpenStreetMap](http://www.openstreetmap.org/){: new_window} afin
d'améliorer la précision de votre position en cas de données GPS imprécises. Vous pouvez également recevoir des informations sur les attributs de route en fonction
de votre emplacement. L'API REST de mise en correspondance de carte permet à votre application d'associer un point de données GPS brut à un point correspondant sur le
lien de route.

Elle reçoit un point défini par des données de coordonnées
GPS de longitude et de latitude et renvoie un point mis en correspondance avec
la carte. Le point mis en correspondance sur la carte est analysé compte tenu de données historiques pour chaque véhicule
sur une période de temps spécifique afin d'identifier le point le plus probable en temps réel. Pour les points dépourvus de données d'emplacement historiques,
l'interface de mise en correspondance de carte renvoie le point le plus proche sur le lien de route à partir du point
GPS demandé.

### Recherche de trajet
{: #route_search}

L'une des caractéristiques élémentaires d'une application dotée de fonctions géospatiales est la capacité d'identifier le chemin le plus court entre deux points.  

L'interface d'API REST de recherche d'itinéraire du service {{site.data.keyword.iotmapinsights_short}} calcule le chemin le plus court entre les
coordonnées de point GPS de départ et d'arrivée. Les coordonnées reçues sont mises en correspondance avec le tronçon
le plus proche de la carte grâce à la fonction de mise en correspondance de
carte, et le chemin le plus court entre ces points mis en correspondance avec la
carte est calculé.

### Recherche de tronçon affecté
{: #link_search}

Lorsqu'un événement se produit sur un route, il est susceptible
d'affecter plusieurs tronçons de route. Vous pouvez utiliser des API REST pour détecter des liens affectés et également pour identifier les tronçons sur
lesquels des véhicules pourraient rencontrer l'événement. La recherche prend en compte la topologie du réseau de liens routiers et non pas seulement la distance des véhicules
à l'événement.
