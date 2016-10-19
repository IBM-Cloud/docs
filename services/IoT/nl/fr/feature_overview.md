---

copyright :
  2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Présentation des fonctions {{site.data.keyword.iot_short_notm}}
{: #feature_overview}

Dernière mise à jour : 29 juin 2016
{: .last-updated}

{{site.data.keyword.iot_full}} repose sur les fonctionnalités suivantes : 

  1. Connexion - Connexion de terminaux et développement d'applications. 
  2. Gestion des informations - Stockage et révision de données de terminal et intégration de votre {{site.data.keyword.iot_short_notm}} à d'autres services. 
  3. Analyse - Visualisation de données de terminal en temps réel à l'aide du tableau de bord {{site.data.keyword.iot_short_notm}}. 
  4. Gestion des risques - Configuration de la connectivité et de l'architecture sécurisées avec contrôle d'accès pour les utilisateurs et les applications.

## Connexion
{: #connect}

La fonctionnalité de connexion de {{site.data.keyword.iot_short_notm}} est le point de départ de n'importe quel service {{site.data.keyword.iot_short_notm}}. Les opérations de connexion de terminaux, de création d'applications, de contrôle de vos terminaux et d'interaction avec des services de tiers sont toutes disponibles sous la fonctionnalité de connexion de {{site.data.keyword.iot_short_notm}}. 

### Terminaux de passerelle

A l'aide d'une passerelle, vous pouvez connecter des terminaux à {{site.data.keyword.iot_short_notm}}, faute de quoi, ils ne peuvent pas se connecter à Internet. Les terminaux de passerelle combinent la fonction d'un terminal et d'une application. Les passerelles peuvent recevoir des commandes et envoyer des données de terminal de la même manière qu'un terminal, mais elles peuvent aussi envoyer des commandes à d'autres terminaux qui lui sont connectés, tout comme le ferait une application. 

Les terminaux qui ne peuvent pas se connecter directement à Internet peuvent être connectés à un terminal de passerelle et leurs données de terminal peuvent être envoyées au terminal de passerelle, qui peut alors les envoyer à votre service {{site.data.keyword.iot_short_notm}}. 

### Gestion des terminaux

Les fonctions de gestion des terminaux sont fournies via la combinaison d'une API de gestion des terminaux et d'un agent de gestion des terminaux qui est installé sur les terminaux. Les terminaux gérés peuvent effectuer des actions de gestion des terminaux, lesquelles peuvent être déclenchées via le principal tableau de bord {{site.data.keyword.iot_short_notm}}. 

La gestion des terminaux vous offre la possibilité de réamorcer des terminaux, de télécharger et d'installer les mises à jour de microprogramme, et de réinitialiser à distance les terminaux avec les paramètres d'usine, le tout à partir de l'interface utilisateur de {{site.data.keyword.iot_short_notm}}. 

### Intégrations de services de tiers

L'intégration de service de tiers repose sur {{site.data.keyword.iot_short_notm}}, y compris la prise en charge des services d'emplacement de données météorologiques de The Weather Company, qui vous permet de rechercher les données météorologiques en cours pour un emplacement de terminal. 

---

## Gestion des informations
{: #information_management}

La fonctionnalité de gestion des informations de {{site.data.keyword.iot_short_notm}} contrôle les données envoyées par les terminaux une fois qu'elles ont atteint le service {{site.data.keyword.iot_short_notm}}. La fonctinnalité de gestion des informations inclut la transformation et le stockage de données. 

### Dernier cache d'événement de terminal

A l'aide de l'API de dernier cache d'événement {{site.data.keyword.iot_short_notm}}, vous pouvez extraire le dernier événement qui a été envoyé par un terminal. Cela fonctionne alors que le terminal est en ligne ou hors ligne, ce qui vous permet d'extraire le statut de terminal, quel que soit l'emplacement physique ou le statut d'utilisation du terminal. Les données de dernier événement d'un terminal peuvent être extraites pour n'importe quel événement spécifique qui s'est produit au cours des 365 derniers jours. 

### Stockage de données d'événement de terminal

Les données de stockage d'événement de terminal de votre service {{site.data.keyword.iot_short_notm}} peuvent être stockées pour être utilisées ultérieurement. Le stockage de données est une première étape essentielle vers l'exécution d'analyses éclairées destinées à vous permettre d'obtenir des informations à partir de ces données. Par exemple, vous pouvez effectuer le suivi de modifications sur des périodes plus longues et stocker des ensembles de données destinés à être utilisés avec des outils d'analyse puissants, y compris pour une utilisation avec l'API Watson et l'informatique cognitive. 

---

## Analyse
{: #analytics}

### Visualisation de données de terminal en temps réel

Vous pouvez visualiser et afficher des données de terminal en temps réel à l'aide de cartes de tableau de bord. Les cartes de tableau de bord surveillent et affichent des données de terminal en temps réel, ce qui vous permet d'assurer le suivi des principaux terminaux ou des données de terminal. Ces visualisations sont affichées sur le tableau de bord {{site.data.keyword.iot_short_notm}} principal pour vous permettre d'accéder rapidement au contexte et au statut des données de terminal en temps réel. 

---

## Gestion des risques
{: #risk_management}

### Connectivité et architecture sécurisées

L'architecture de {{site.data.keyword.iot_short_notm}} est conçue pour empêcher les terminaux de simuler les droits d'accès d'autres terminaux, garantissant ainsi l'intégrité de vos données de terminal. Les terminaux se connectent à {{site.data.keyword.iot_short_notm}} à l'aide d'une combinaison d'un ID de client et d'un jeton d'authentification connue de vous seul. Une fois les terminaux enregistrés ou les clés d'API générées, le jeton d'authentification est soumis à une opération de hachage et de salage pour garantir la sécurité de vos données d'identification.
La connectivité via TLS v1.2 est entièrement prise en charge. 

---
