---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Besoins des services
{: #requirements}


##Exigences relatives aux messages de périphérique MQTT

* Le courtier de messages MQTT doit fournir des messages de périphérique au format JSON dans une ou plusieurs rubriques MQTT.
* Les messages de périphérique peuvent contenir un nombre quelconque d'attributs, mais doivent obligatoirement contenir :
	* Un attribut qui identifie le périphérique de manière unique.
	* Un attribut qui spécifie la latitude de la localisation du périphérique.
	* Un attribut qui spécifie la longitude de la localisation du périphérique.
* Deux modes de message sont pris en charge :
	* Un message MQTT peut contenir un objet JSON avec des informations sur un périphérique unique.
	* Un message MQTT peut contenir un objet JSON avec des informations sur un ensemble de périphériques.

##Evénements MQTT et configuration du service

Votre application s'abonne à des messages MQTT et contrôle
{{site.data.keyword.geospatialshort_Geospatial}} via son
[API REST](https://console.ng.bluemix.net/apidocs/246). Les
actions suivantes sont disponibles via des appels d'API REST :

* Configurer et démarrer le service.
* Ajouter et supprimer des régions géographiques à surveiller.
* Extraire des informations sur le statut du service et l'ensemble de régions défini.
* Arrêter le service.
* Redémarrer un service déjà configuré.

