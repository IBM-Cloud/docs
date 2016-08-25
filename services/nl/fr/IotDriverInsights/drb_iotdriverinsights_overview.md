---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# A propos de l'analyse du type de conduite
{: #iotdriverinsights_overview}
Dernière mise à jour : 16 juin 2016
{: .last-updated}


L'analyse du type de conduite est un service que vous pouvez utiliser pour analyser le comportement d'un conducteur à partir de données contextuelles et de données d'exploration de véhicules.

{:shortdesc}


## Architecture
{: #drb}

Vous pouvez identifier et analyser différents types de conduite en rapport avec la vitesse, les virages et d'autres catégories. Ainsi, vous pouvez déterminer des cas d'accélérations brusques, d'excès de vitesse, de virages serrés, de freinages brusques ou fréquents ou d'autres types de comportement conducteur inapproprié.

## Configuration d'analyse
{: #configurability}  

Les paramètres de seuil d'analyse déterminent la façon dont les différents types de comportement des conducteurs sont détectés et analysés à partir de données contextuelles et de données d'exploration de véhicules qui sont introduites dans le système. Vous pouvez configurer certains des paramètres de seuil pour l'analyse des types de conduite depuis la console d'administration du service {{site.data.keyword.iotdriverinsights_short}}. Ainsi, il vous est possible de configurer la plage de vitesse par type de route ou la plage d'angle des virages.

Pour plus d'informations sur la façon de configurer les paramètres de seuil pour l'analyse des types de conduite, voir [Configuration des paramètres pour le service](drb_iotdriverinsights_admin.html#configureparameters).

### Catégories de types de conduite et activités

Les tableaux suivants répertorient les types de conduite par catégorie qui peuvent être détectés et analysés par le service :

#### Tableau 1 : types de conduite en rapport avec la vitesse

|Comportement|ID|Description|
|--------|:-------:|------|
|Accélération brusque|1|La valeur du seuil d'accélération brusque par rapport à une vitesse donnée est définie de façon interne. Une accélération brusque est détectée si les données d'accélération dépassent la valeur de seuil.|
|Freinage brusque|2|La valeur du seuil de décélération brusque par rapport à une vitesse donnée est définie de façon interne. Un freinage brusque est détecté si les données de freinage pour un trajet dépassent la valeur de seuil.|
|Excès de vitesse|3|La valeur du seuil d'excès de vitesse par type de route est définie. Un excès de vitesse est détecté si les données de vitesse pour le trajet dépassent la valeur de seuil. Vous pouvez configurer le seuil d'excès de vitesse. |
|Arrêts fréquents|4|Un arrêt est détecté quand la vitesse a une valeur zéro. Des arrêts fréquents sont détectés quand de nombreux arrêts sont effectués dans une période définie du trajet.|
|Accélérations fréquentes|5|La valeur du seuil d'accélération par rapport à une vitesse donnée est définie de façon interne. Des accélérations fréquentes sont détectées si le conducteur dépasse fréquemment la valeur de seuil dans une période définie du trajet.|
|Freinages fréquents|6|La valeur du seuil de décélération par rapport à une vitesse donnée est définie de façon interne. Des décélérations fréquentes sont détectées si le conducteur dépasse fréquemment la valeur de seuil dans une période définie du trajet.|

#### Tableau 2 : types de conduite en rapport avec les virages

|Comportement|ID|Description|
|-------|:--------:|-------|
|Virage serré (virage à haute vitesse)|7|La valeur du seuil de vitesse dans les virages est définie. Un virage serré est détecté si le conducteur dépasse la valeur de seuil. Vous pouvez configurer le seuil de virage serré.
|Accélération avant un virage|8|La valeur du seuil d'accélération par rapport à une vitesse donnée est définie de façon interne. Une accélération avant un virage est détectée si le conducteur dépasse la valeur de seuil.
|Freinage excessif avant la sortie d'un virage|9|La valeur du seuil de décélération par rapport à une vitesse donnée est définie de façon interne. Un freinage excessif avant la sortie d'un virage est détecté si le conducteur dépasse la valeur de seuil.
#### Tableau 3 : autres types de conduite

|Comportement|ID|Description|
|-------|:--------:|-------|
|Fatigue au volant|10|La valeur du seuil de décélération par rapport à une vitesse donnée est définie de façon interne. La fatigue chez un conducteur est détectée si la vitesse dépasse la valeur de seuil.|


### Contexte de conduite
|<br/>Catégorie|<br/>ID catégorie|Nom|ID contexte|
|-------|:-----:|--------|:-------:|
|**Plage horaire**|**4**|\-|\-|
|Plage horaire|4|Jour|1|
|Plage horaire|4|Nuit|2|
|Plage horaire|4|Heures de pointe en matinée|3|
|Plage horaire|4|Heures de pointe en soirée|4|
|**Type de route**|**3**|\-|\-|
|Type de route|3|Autoroute|1|
|Type de route|3|Périphérique|2|
|Type de route|3|Axe urbain principal|3|
|Type de route|3|Axe urbain|4|
|Type de route|3|Autres|5|
|**Vitesse effective**|**0**|\-|\-|
|Vitesse effective|0|Trafic fluide|0|
|Vitesse effective|0|Trafic régulier|1|
|Vitesse effective|0|Circulation bloquée|2|
|Vitesse effective|0|Embouteillage|3|
|Vitesse effective|0|Conditions mixtes|4|


## API REST
{: #rest_api}

L'API REST {{site.data.keyword.iotdriverinsights_short}} fournit des demandes que vous pouvez utiliser pour personnaliser et générer vos applications {{site.data.keyword.Bluemix_notm}} :

 1. Commandes de données de véhicule :
   - `sendCarProbeData` envoie les données d'exploration de véhicules à analyser.
   - `getCarProbeDataListAsDate` retourne la liste des données d'exploration de véhicules par date.
   - `deleteCarProbeDataListByDate` supprime les données d'exploration de véhicules
 2. Commandes de travail d'analyse :
   - `sendJobRequest` envoie la demande de travail d'analyse du type de conduite
   - `getJobInfo` retourne les informations du travail spécifié
   - `getJobInfoList` retourne la liste des informations de travail
 3. Commandes de résultat d'analyse :
   - `getAnalyzedTripSummaryList` retourne la liste des informations récapitulatives de trajectoire
   - `getAnalyzedTripInfo` renvoie les informations de la trajectoire analysée spécifiée
   - `deleteJobResult` supprime tous les résultats analysés qui sont liés à un travail

Pour plus d'informations, voir la documentation de l'API [{{site.data.keyword.iotdriverinsights_short}}](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}.

## Infrastructure d'analyse Big Data
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} utilise Hadoop comme infrastructure de back end. La grande extensibilité apportée par Hadoop permet au service {{site.data.keyword.iotdriverinsights_short}} d'extraire et d'analyser de grands volumes de données contextuelles et de données d'exploration de véhicules.
