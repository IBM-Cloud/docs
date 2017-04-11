---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Tableau de bord d'administration du service
{: #service-dashboard}


Vous pouvez consulter le statut de votre instance de service {{site.data.keyword.geospatialshort_Geospatial}} et l'arrêter ou la redémarrer depuis le tableau de bord d'administration du service. Vous pouvez accéder au tableau de bord d'administration du service en cliquant sur le volet {{site.data.keyword.geospatialshort_Geospatial}} dans votre tableau de bord {{site.data.keyword.geospatialshort_Geospatial}}. Si vous utilisez le modèle d'application et que votre instance de service atteint la limite d'événements et s'arrête, vous pouvez redémarrer le service. L'arrêt du service supprime la limite d'événements. Le service continue de recevoir des événements jusqu'à ce que vous l'arrêtiez. Le tableau de bord d'administration du service affiche également le statut de votre instance de service et des statistiques.
{:shortdesc}

##Vérifications de région {{site.data.keyword.geospatialshort_Geospatial}}

{{site.data.keyword.geospatialshort_Geospatial}} surveille les périphériques depuis la plateforme Internet of Things. Chaque périphérique surveillé envoie des messages de périphérique contenant un identificateur unique ainsi que sa position actuelle, dont la latitude et la longitude. La position du périphérique est vérifiée par rapport aux coordonnées de chaque région géographique définie. Le service produit alors des événements quand les périphériques entrent dans une région spécifique, la quittent ou y restent.

Une vérification de région est utilisée comme unité pour mesurer l'utilisation d'{{site.data.keyword.geospatialfull}}. Pour chaque message de périphérique, une vérification de région est effectuée en cas de spécification d'une détection d'entrée, de sortie, ou d'entrée et de sortie pour la région. Pour chaque message de périphérique, une vérification de région est exécutée si une détection de stagnation est spécifiée pour la région. Si aucune région n'est définie, pour chaque message de périphérique, une vérification de région est comptée comme si une région existait, ce qui signifie que si la vérification de régions (entrée, sortie et stagnation) est définie sur 100 régions, un message de périphérique unique produira 200 vérifications de région.
