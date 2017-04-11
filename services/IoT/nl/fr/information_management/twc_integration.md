---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilisation de données provenant de The Weather Company avec vos terminaux
{: #weathercompany}

L'intégration de The Weather Company vous permet de combiner des données météorologiques à vos terminaux {{site.data.keyword.iot_short_notm}} existants.
{:shortdesc}

Les données météorologiques de The Weather Company apparaissent dans la vue de détails du terminal si une demande de mise à jour d'emplacement a été émise par l'API ou si le terminal a déjà défini son emplacement à l'aide d'un message de gestion de terminaux.

**Important :** Seuls les terminaux gérés peuvent définir leurs propres emplacements. Les emplacements de tous les terminaux non gérés doivent être définis manuellement à l'aide de l'API. Pour plus d'informations sur la définition d'un emplacement de terminal, voir [Demandes de mise à jour d'emplacement](../../devices/device_mgmt/index.html#update-location).

### API REST pour The Weather Company
Pour accéder à l'API REST pour The Weather Company, voir la section
Device Location Weather dans la documentation [{{site.data.keyword.iot_short_notm}} HTTP REST API ![Icône de lien externe](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window}.

### Affichage des données météorologiques

Pour afficher les données météorologiques extraites pour un emplacement de terminal : 
1. Cliquez sur le terminal dans le panneau **Terminaux**. 
2. Dans la vue de détails du terminal, faites défiler l'écran jusqu'à la section **Extensions**.  
Les données météorologiques suivantes sont répertoriées :
 - Météo en cours.
 - Température en cours.
 - Températures maximale et minimale prévues.
 - Humidité relative.
 - Pression.
 - Visibilité.
 - Vitesse du vent.
 - Direction du vent.
 - Latitude.
 - Longitude.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
