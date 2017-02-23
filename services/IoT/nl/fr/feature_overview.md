---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Présentation des fonctions {{site.data.keyword.iot_short_notm}}
{: #feature_overview}

{{site.data.keyword.iot_full}} repose sur les fonctionnalités suivantes :

  1. Connexion - Connexion de terminaux et développement d'applications.
  2. Gestion des informations - Stockage et révision de données de terminal et intégration de votre {{site.data.keyword.iot_short_notm}} à d'autres services.
  3. Analyse - Visualisation de données de terminal en temps réel à l'aide du tableau de bord {{site.data.keyword.iot_short_notm}}.
  4. Gestion des risques - Configuration de la connectivité et de l'architecture sécurisées avec contrôle d'accès pour les utilisateurs et les applications.

## Connexion
{: #connect}

La fonctionnalité de connexion de {{site.data.keyword.iot_short_notm}} est le point de départ de n'importe quel service {{site.data.keyword.iot_short_notm}}. Les opérations de connexion de terminaux, de création d'applications, de contrôle de vos terminaux et d'interaction avec des services de tiers sont toutes disponibles sous la fonctionnalité de connexion de {{site.data.keyword.iot_short_notm}}.

### Terminaux de passerelle

A l'aide d'une passerelle, vous pouvez connecter des terminaux à {{site.data.keyword.iot_short_notm}}, faute de quoi, ils ne peuvent pas se connecter à Internet. Les passerelles ont toutes les fonctions d'un terminal, mais peuvent également publier et s'abonner pour le compte des terminaux qui y sont connectés. Les terminaux de passerelle permettent à des groupes de capteurs qui ne peuvent pas se connecter à Internet de se connecter à votre {{site.data.keyword.iot_short_notm}} en envoyant leurs données à une passerelle. Pour plus d'informations, voir la rubrique relative au [développement pour les passerelles](https://console.ng.bluemix.net/docs/services/IoT/gateways/gw_dev_index.html).

### Gestion des terminaux

Les fonctions de gestion des terminaux sont fournies via une API de gestion des terminaux et un agent de gestion des terminaux qui est installé sur les terminaux. Les terminaux avec un agent de gestion de terminaux peuvent effectuer des actions de gestion des terminaux, lesquelles peuvent être déclenchées via le principal tableau de bord {{site.data.keyword.iot_short_notm}} ou l'API de gestion des terminaux. Les actions de gestion des terminaux comprennent le réamorçage, le téléchargement et l'installation des mises à jour du microcode et la réinitialisation des terminaux aux paramètres d'usine. La gestion des terminaux peut également être étendue pour inclure des actions personnalisées de gestion de terminaux. Pour plus d'informations, voir la [documentation sur la gestion des terminaux](https://console.ng.bluemix.net/docs/services/IoT/devices/device_mgmt/index.html).

### Extensions et intégrations de services

Les extensions et l'intégration de services permettent d'ajouter des services externes et des extensions définies par l'utilisateur de services de base à une instance de {{site.data.keyword.iot_short_notm}}. Les services externes qui peuvent être intégrés à {{site.data.keyword.iot_short_notm}} comprennent les services de localisation météorologiques de The Weather Company, vous permettant de trouver la météo en cours dans la zone géographique d'un terminal, les données Jasper SIM et {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}. Pour plus d'informations sur les extensions et les intégrations de services tiers, reportez-vous à la section relative à l'[intégration de services externes](https://console.ng.bluemix.net/docs/services/IoT/reference/extensions/index.html).

---

## Gestion des informations
{: #information_management}

La fonctionnalité de gestion des informations de {{site.data.keyword.iot_short_notm}} contrôle les données envoyées par les terminaux une fois qu'elles ont atteint le service {{site.data.keyword.iot_short_notm}}. La fonctionnalité de gestion des informations inclut la transformation et le stockage de données.

### Dernier cache d'événement de terminal

A l'aide de l'API de dernier cache d'événement {{site.data.keyword.iot_short_notm}}, vous pouvez extraire le dernier événement qui a été envoyé par un terminal. Cela fonctionne alors que le terminal est en ligne ou hors ligne, ce qui vous permet d'extraire le statut de terminal, quel que soit l'emplacement physique ou le statut d'utilisation du terminal. Les données de dernier événement d'un terminal peuvent être extraites pour n'importe quel événement spécifique qui s'est produit au cours des 365 derniers jours.

### Stockage de données d'événement de terminal

Les données de stockage d'événement de terminal de votre service {{site.data.keyword.iot_short_notm}} peuvent être stockées pour être utilisées ultérieurement. Le stockage de données est une première étape essentielle vers l'exécution d'analyses éclairées destinées à vous permettre d'obtenir des informations à partir de ces données.  Par exemple, vous pouvez effectuer le suivi de modifications sur des périodes plus longues et stocker des ensembles de données destinés à être utilisés avec des outils d'analyse puissants, y compris pour une utilisation avec l'API Watson et l'informatique cognitive. Pour plus d'informations, voir la rubrique relative à la [connexion d'un service historique {{site.data.keyword.cloudant_short_notm}}](https://console.ng.bluemix.net/docs/services/IoT/cloudant_connector.html) ou à la [connexion d'un service historique {{site.data.keyword.messagehub}}](https://console.ng.bluemix.net/docs/services/IoT/message_hub.html).

---

## Analyse
{: #analytics}

### Visualisation de données de terminal en temps réel

Vous pouvez visualiser et afficher des données de terminal en temps réel à l'aide de cartes de tableau de bord. Les cartes de tableau de bord surveillent et affichent des données de terminal en temps réel, ce qui vous permet d'assurer le suivi des principaux terminaux ou des données de terminal. Ces visualisations sont affichées sur le tableau de bord {{site.data.keyword.iot_short_notm}} principal pour vous permettre d'accéder rapidement au contexte et au statut des données de terminal en temps réel. Pour plus d'informations, voir la rubrique relative à la [visualisation des données en temps réel](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html).

### Edge Analytics et Cloud Analytics

En utilisant {{site.data.keyword.iot_short_notm}} Cloud Analytics, vous spécifiez des conditions de règle qui sont basées sur les données de terminal en temps réel et qui déclenchent des alertes et des actions facultatives lorsqu'elles sont réunies. Par exemple, vous pouvez créer une règle garantissant que lorsque le terminal est supprimé ou que la température du terminal augmente, une alerte est envoyée au tableau de bord du terminal de l'utilisateur et un courrier électronique est envoyé à l'administrateur. Pour plus d'informations, voir la [documentation Cloud Analytics](https://console.ng.bluemix.net/docs/services/IoT/cloud_analytics.html).

Avec Edge Analytics, le processus d'analyse déclenché par des règles depuis le cloud est remplacé par une passerelle sur laquelle Edge Analytics est activé. Cela peut vous permettre de réduire considérablement la quantité de données de terminal envoyées vers le cloud car le traitement des analyses est exécutée à proximité du terminal. Pour plus d'informations, voir la [documentation Edge Analytics](https://console.ng.bluemix.net/docs/services/IoT/edge_analytics.html).

---

## Gestion des risques
{: #risk_management}

### Connectivité et architecture sécurisées

L'architecture de {{site.data.keyword.iot_short_notm}} est conçue pour empêcher les terminaux de simuler les droits d'accès d'autres terminaux, garantissant ainsi l'intégrité de vos données de terminal. Les terminaux se connectent à {{site.data.keyword.iot_short_notm}} à l'aide d'une combinaison d'un ID de client et d'un jeton d'authentification connue de vous seul. Une fois les terminaux enregistrés ou les clés d'API générées, le jeton d'authentification est soumis à une opération de hachage et de salage pour garantir la sécurité de vos données d'identification.

Le module complémentaire de Gestion des risques et de la sécurité vous permet d'améliorer la sécurité de {{site.data.keyword.iot_short_notm}} pour vous assurer que tous les points de connexion entre le serveur et les terminaux sont authentifiés avec des données d'identification certifiées. Avec ce module complémentaire, les certificats et l'authentification TLS (Transport Layer security) sont utilisés, en plus des ID utilisateur et des jetons utilisés par {{site.data.keyword.iot_short_notm}}. Lors de la communication entre les terminaux et le serveur, tous les terminaux ne disposant pas de certificats valides avec accès au serveur, tels que configurés dans le module complémentaire Gestion des risques et de la sécurité, se voient refuser l'accès, même s'ils utilisent des ID utilisateur et des mots de passe valides.

---
