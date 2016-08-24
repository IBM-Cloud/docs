---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à {{site.data.keyword.iot4auto_short}} (bêta)
{: #getting_started_iotautomotive}

Dernière mise à jour : 29 juillet 2016
{: .last-updated}

{{site.data.keyword.iot4auto_full}} est un service {{site.data.keyword.Bluemix_notm}} que vous pouvez utiliser pour extraire, gérer et analyser les big data en provenance de véhicules connectés. L'analyse effectuée par {{site.data.keyword.iot4auto_short}} fournit des connaissances exploitables et puissantes dans divers domaines liés aux véhicules automobiles : types de conduite, localisation des véhicules ou autres activités et événements intéressants relatifs au domaine automobile.

{:shortdesc}

En utilisant {{site.data.keyword.iot4auto_short}}, vous pouvez effectuer les tâches suivantes :

- Envoyer des données d'exploration de véhicules et des données normalisées vers le magasin de données pour analyse
- Injecter des événéments dans la mappe de contexte et extraire les événements qui affectent des véhicules spécifiques
- Identifier de nouveaux événements à partir de données d'exploration de véhicules
- Extraire des informations relatives aux véhicules connectés
- Gérer des données d'actifs relatifs aux conducteurs, aux véhicules, aux règles d'événement, aux types d'événement et aux fournisseurs


Le service {{site.data.keyword.iot4auto_short}} inclut les services {{site.data.keyword.Bluemix_notm}} suivants, qui sont aussi disponibles séparément dans le catalogue {{site.data.keyword.Bluemix_notm}} :

|Service|Description|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html){:new_window}| Un service qui peut analyser le comportement des conducteurs et identifier les modèles de trajectoire lors d'un trajet à partir des données d'exploration de véhicules et des données contextuelles qui sont extraites d'un véhicule connecté.
|[Context Mapping](../IotMapInsights/index.html){:new_window}| Un service qui fournit des fonctions géospatiales, comme la mise en correspondance des données avec des cartes routières ou la recherche du trajet le plus court sur des réseaux routiers.
*Tableau 1. Services d'{{site.data.keyword.iot4auto_short}}*

Avant de commencer à intégrer au service vos périphériques et applications automobiles, prenez soin d'effectuer la procédure suivante :

1. Prenez connaissance de la rubrique [A propos d'{{site.data.keyword.iot4auto_short}}](iotautomotive_overview.html) pour vous familiariser avec les fonctions et analyses disponibles et prises en charge pour le service.
2. Quand vous ajoutez une instance du service depuis le catalogue [{{site.data.keyword.Bluemix_notm}} ](https://console.ng.bluemix.net/catalog/labs/){:new_window}, assurez-vous qu'elle n'est pas liée à une application et prenez soin de noter les valeurs automatiquement générées d'ID titulaire, de nom d'utilisateur et de mot de passe. Vous aurez besoin de ces valeurs plus tard pour accéder au service via l'API {{site.data.keyword.iot4auto_short}}.
3. En utilisant la console du tableau de bord, configurez les ports, les noms d'hôte cible et d'autres paramètres pour votre service {{site.data.keyword.iot4auto_short}}. Pour plus d'informations, voir [Administration](iotautomotive_admin.html).

Vous pouvez intégrer vos périphériques et applications automobiles à ce service en utilisant les commandes API REST {{site.data.keyword.iot4auto_short}}.

Pour être opérationnel rapidement, procédez comme suit :

1. Injectez des événéments en utilisant la commande de demande API `sendEvent` pour envoyer ces événements afin qu'ils soient analysés.
  - Demande : données d'événement avec position
2. Confirmez que les données d'événement sont stockées et mises en correspondance avec des cartes routières en utilisant la commande de demande API `getEvent` pour extraire l'événement.
  - Demande : données de surface (longitude et latitude des points de départs et d'arrivée)
  - Réponse : données d'événement avec ID de tronçon de route
3.  Envoyez des données d'exploration de véhicules à analyser en utilisant la commande de demande API `sendCarProbe`.
  - Demande : données d'exploration de véhicules avec position
4. Confirmez que les données d'exploration de véhicules sont stockées et mises en correspondance avec des cartes routières en utilisant la commande de demande API `getCarProbe` pour extraire les données.
  - Demande : données de surface (longitude et latitude des points de départs et d'arrivée)
  - Réponse : données d'exploration de véhicules avec ID de tronçon de route
5. Analysez les données de conducteur, Pour plus d'informations, voir [Driver Behavior](../IotDriverInsights/index.html){:new_window}.

# Liens connexes
{: #rellinks}

## Référence d'API
{: #api}
* [{{site.data.keyword.iot4auto_short}}Docs API](http://ibm.biz/IoT4Automotive_APIdoc){:new_window}
* [Interfaces API de service relatives aux cartes contextuelles](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}
* [Interfaces API de service relatives au comportement des conducteurs]( http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}


## Liens connexes
{: #general}
* [Initiation à {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Initiation à {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [Initiation à {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Nouveautés dans les services Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [dW Answers sur IBM developerWorks](https://developer.ibm.com/answers/topics/iot-for-automotive){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-for-automotive){:new_window}
