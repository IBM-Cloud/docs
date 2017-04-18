---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Fonctionnement du service
{{site.data.keyword.iotinsurance_full}} crée un flux permettant de collecter,
de gérer et d'analyser des données provenant des assurés connectés.
{:shortdesc}

L'assureur crée une instance d'{{site.data.keyword.iotinsurance_short}} dans l'organisation {{site.data.keyword.Bluemix_notm}}. Des capteurs, qui sont connectés au cloud du
fournisseur de capteurs, sont installés chez les clients. Depuis leurs terminaux mobiles, les clients autorisent le service {{site.data.keyword.iotinsurance_short}} à recevoir des données de capteur. Le transformateur {{site.data.keyword.iotinsurance_short}} se connecte au cloud du fournisseur de capteurs et extrait les données pour chaque utilisateur,
puis les
envoie au serveur {{site.data.keyword.iot_short_notm}}. Si le capteur indique que les critères spécifiés dans les boucliers de l'assureur sont remplis chez le client, des
notifications sont envoyées dans le tableau de bord de l'assureur et au terminal du client.

Un capteur connecté détecte un événement, par exemple, une fuite d'eau, et envoie ces informations à un fournisseur à domicile intelligent, tel que Wink.  {{site.data.keyword.iotinsurance_short}} détecte le signal via sa connexion au cloud du fournisseur à domicile intelligent et crée un contenu d'alerte. Le contenu est envoyé via MQTT au moteur de bouclier {{site.data.keyword.iotinsurance_short}} pour être traité. Le moteur de bouclier vérifie si le contenu correspond aux critères définis par les règles de bouclier. Si tel est le cas, le moteur de bouclier émet un contenu de risque via MQTT et l'envoie au moteur des actions {{site.data.keyword.iotinsurance_short}}. Ce dernier exécute les actions qui sont définies par le bouclier pour ce type de risque, telles que l'envoi d'un message texte au propriétaire du logement.

{{site.data.keyword.iotinsurance_short}} repose sur {{site.data.keyword.iot_full}} pour la transmission de contenus d'alerte et de risque entre ses composants. Un système opérationnel complet nécessite des utilisateurs, des boucliers et des associations entre les utilisateurs et les boucliers.

![Processus {{site.data.keyword.iotinsurance_short}}. Ce
diagramme est décrit dans le corps principal de la rubrique.](images/IoT4I_process.svg "{{site.data.keyword.iotinsurance_short}} process")
