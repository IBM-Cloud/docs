---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# A propos d'{{site.data.keyword.iot4auto_short}} (bêta)
{: #iotautomotive_overview}

Dernière mise à jour : 29 juillet 2016
{: .last-updated}

{{site.data.keyword.iot4auto_full}} est un service sous {{site.data.keyword.Bluemix_notm}} que vous pouvez utiliser pour afficher et analyser les big data en provenance des véhicules.

En utilisant le service {{site.data.keyword.iot4auto_short}}, vous pouvez collecter et traiter de gros volumes de données tirés de ces véhicules. L'analyse effectuée par {{site.data.keyword.iot4auto_short}} fournit des connaissances exploitables et puissantes dans divers domaines liés aux véhicules automobiles : types de conduite, localisation des véhicules ou autres activités et événements intéressants relatifs au domaine automobile.
{:shortdesc}

## Architecture
{: #architecture}
{{site.data.keyword.iot4auto_short}} est une plateforme d'infrastructure en temps réel fondamentale pour les applications automobiles et les périphériques de véhicules connectés. Le service est aussi conçu pour prendre en charge les fonctionnalités de conduite autonomes émergentes du futur.

![Architecture {{site.data.keyword.iot4auto_full}}](images/architecture_iotautomotive.png "Architecture {{site.data.keyword.iot4auto_full}}")

Le service {{site.data.keyword.iot4auto_short}} inclut les services {{site.data.keyword.Bluemix_notm}} suivants, qui sont aussi disponibles séparément dans le catalogue {{site.data.keyword.Bluemix_notm}} :

|Service|Description|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html)| Un service qui peut analyser le comportement des conducteurs et identifier les modèles de trajectoire d'un déplacement à partir des données d'exploration de véhicules et des données contextuelles qui sont extraites d'un véhicule connecté.
|[Context Mapping](../IotMapInsights/index.html)| Un service qui fournit des fonctions géospatiales, comme la mise en correspondance des données avec des cartes routières ou la recherche du trajet le plus court sur des réseaux routiers.
*Tableau 1. Services {{site.data.keyword.iot4auto_short}}*

## Fonctions
{: #features}

{{site.data.keyword.iot4auto_short}} prend en charge les fonctions et options ci-après pour des solutions fournissant des données d'exploration de véhicules depuis des périphériques de véhicules connectés :

### Extraction de données depuis des périphériques {{site.data.keyword.iot4auto_short}}

- Prend en charge les protocoles et modèles de données suivants :
   - TPEG
   - ITS
   - Normes automobiles ISO
- Prend en charge d'autres capteurs et périphériques non automobiles

### Stockage et normalisation des données

- Identifie et filtre les données d'anomalie
- Mappe, convertit et formate les données dans le modèle de données standard pour analyse
- Place les données dans l'un des magasins de données ci-dessous selon le volume, le temps d'attente et l'utilisation de l'application ou du service:
   -  Magasin de données Hadoop pour analyse big data
   -  Magasin de données d'agent pour analyse en temps réel

### Service à base de cartes géospatiales

- Mise en correspondance en temps réel
- Service d'événements
- Injection dynamique d'événements depuis des véhicules et des sources externes
- Recherche prenant en compte une topologie à base de noeuds ou de liens
- Prise en charge de cartes contextuelles disposant de données météo intégrées

### Plateforme d'analyse en temps réel hautement évolutive et à faible temps d'attente

- Technologie à base d'agent
- Analyse personnalisée
- Analyse souple reposant sur des règles

### Analyse MOMA (Moving Object Map Analysis)

- Analyse par lots (big data) en utilisant les données d'un véhicule
- Analyse du comportement du conducteur
- Profilage des conducteurs
- Analyse des modèles de trajectoire

### Service de fournisseur de données

- Interfaces API pour services et applications tiers

### Intégration à la gestion des actifs

- Système de gestion des actifs de véhicule

## API REST
{: #api}

L'API [{{site.data.keyword.iot4auto_short}}](http://ibm.biz/IoT4Automotive_APIdoc) fournit des commandes vous permettant de personnaliser {{site.data.keyword.iot4auto_short}} afin de l'adapter à vos besoins.

En utilisant les commandes API REST, vous pouvez personnaliser votre instance de service {{site.data.keyword.iot4auto_short}}.

- Injecter des événements spécifiques dans le système
- Stocker les données d'exploration normalisées extraites d'un véhicule dans le magasin de données d'analyse préféré
- Extraire les événements intéressants en temps réel en même temps que l'emplacement géographique du véhicule

### Commandes API REST

|  Objectif                             |Commande API |Description |
|:------------------------------------|:------------|:-----------|
|Injecter un événément|`sendEvent`|Envoie le trafic ou d'autres événements vers la plateforme.|
|Envoyer données exploration véhicules|`sendCarProbe`|Envoie les données de capteur d'emplacement provenant du véhicule et extrait les événements affectés pour le véhicule en fonction du résultat de l'analyse en temps réel.|
|Créer des données de véhicule|`createVehicle`|Crée un enregistrement de véhicule en tant qu'actif. Ces informations sont utilisées pour l'authentification, l'inventaire et d'autres tâches.|
|Interfaces API de carte|Non disponible|Pour plus d'informations, voir [Interfaces API de service relatives aux cartes contextuelles](http://ibm.biz/IoTContextMapping_APIdoc).|
|Interfaces API d'analyse|Non disponible|Pour plus d'informations, voir [Interfaces API de service relatives au comportement des conducteurs]( http://ibm.biz/IoTDriverBehavior_APIdoc).|
|Obtenir des données d'exploration de véhicules|`getCarProbe`|Obtient les dernières données d'exploration d'un véhicule qui ont été envoyées par la commande API `sendCarProbe`.|
|Obtenir des événements de carte|`getEvent` |Obtient les événements sur la carte qui ont été envoyés par la commande API `sendEvent`.|
|Obtenir des données d'actifs de véhicule|`getVehicle`| Obtient les données de véhicule en tant qu'actif depuis la commande API `createVehicle`.|
*Tableau 2. Commandes API REST {{site.data.keyword.iot4auto_short}}*
