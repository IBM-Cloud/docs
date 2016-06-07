---

copyright:
  années : 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# A propos de {{site.data.keyword.iotdriverinsights_short}}
{: #iotdriverinsights_overview}

Vous pouvez utiliser {{site.data.keyword.iotdriverinsights_full}} pour analyser le comportement du conducteur à partir de données de détection de véhicules et de données contextuelles.
{:shortdesc}

## Analyse du comportement du conducteur
{: #driver_behavior_analysis}
A partir des données de détection de véhicules et des données contextuelles, vous pouvez analyser le comportement d'un conducteur, et plus particulièrement ce type d'actions : accélérations ou freinages brusques, freinages fréquents, excès de vitesse, virages serrés et autres actions similaires.

Les activités et contextes suivants sont inclus :
 - Types de conduite 
    - Relatifs à la vitesse
       - Accélération brusque
       - Freinage brusque
       - Excès de vitesse
       - Arrêts fréquents
       - Accélérations fréquentes
       - Freinages fréquents
    - Relatifs aux virages
       - Virage serré (virage à haute vitesse)
       - Accélération avant un virage
       - Freinage excessif dans un virage
    - Autres
       - Fatigue au volant
 - Contexte de conduite
    - Plage horaire
       - Heures de pointe en matinée
       - Heures de pointe en soirée
       - Jour
       - Nuit
    - Type de route
       - Autoroute
       - Périphérique
       - Axe urbain principal
       - Axe urbain
       - Autres
    - Vitesse effective selon les types de route
       - Trafic fluide
       - Trafic régulier
       - Embouteillage
       - Circulation bloquée
       - Conditions mixtes

## Infrastructure d'analyse Big Data
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} utilise Hadoop comme infrastructure de back end. Bénéficiant ainsi d'une grande extensibilité, {{site.data.keyword.iotdriverinsights_short}} peut analyser des données de détection de véhicules et des données contextuelles.

## API REST
{: #rest_api}
Les développeurs peuvent extraire les résultats d'analyse via l'API REST et les utiliser dans l'application {{site.data.keyword.Bluemix_notm}}.
 1. Données de véhicule
   - `sendCarProbeData` envoie les données de détection de véhicules à analyser.
   - `getCarProbeDataListAsDate` renvoie la liste de données de détection de véhicules par date.
   - `deleteCarProbeDataListByDate` supprime les données de détection de véhicules.
 2. Travail d'analyse
   - `sendJobRequest` envoie la demande de travail d'analyse du type de conduite.
   - `getJobInfo` renvoie les informations relatives au travail spécifié.
   - `getJobInfoList` retourne la liste des informations relatives au travail.
 3. Résultats d'analyse 
   - `getAnalyzedTripSummaryList` retourne la liste des informations récapitulatives de trajectoire.
   - `getAnalyzedTripInfo` renvoie les informations de la trajectoire analysée spécifiée.
   - `deleteJobResult` supprime tous les résultats analysés relatifs à un travail.

## Configurabilité
{: #configurability}
Certains des paramètres de seuil d'analyse (comme la plage de vitesses par type de route ou celles des angles de virage, par exemple) peuvent être configurés depuis l'interface utilisateur.
