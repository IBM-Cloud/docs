---

copyright:
  years: 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Intégration de DevOps Insights avec IBM UrbanCode Deploy - Présentation
{: #uc_insights_overview}

Delivery Insights, un composant de {{site.data.keyword.DRA_short}}, affiche des statistiques et des mesures liées au déploiement, ainsi que d'autres informations sur votre installation IBM UrbanCode Deploy. Il peut ainsi présenter des graphiques concernant la durée du déploiement, les réussites et les échecs, triés par environnements regroupés de manière logique.
{:shortdesc}

Si vous ne disposez pas d'une chaîne d'outils ou de {{site.data.keyword.DRA_short}}, vous devez d'abord configurer {{site.data.keyword.DRA_short}} :
1. Dans le catalogue {{site.data.keyword.Bluemix}}, cliquez sur **{{site.data.keyword.DRA_short}}**, sélectionnez un plan de tarification et cliquez sur **Créer**.
1. Cliquez sur l'onglet **Gérer** et, sous **Démarrez avec Delivery Insights for UrbanCode**, cliquez sur **Commencez ici**. Delivery Insights crée en arrière-plan une chaîne d'outils pour votre organisation. Les chaînes d'outils ouvertes sont des collections d'intégrations d'outil et, dans ce cas, IBM UrbanCode Deploy et {{site.data.keyword.DRA_short}} font partie de votre chaîne d'outils. Pour plus d'informations sur les chaînes d'outils, voir [Utilisation des chaînes d'outils](../ContinuousDelivery/toolchains_working.html).
1. Sur la page **Delivery Insights Setup**, suivez la procédure pour configurer DevOps Connect et connecter vos serveurs IBM UrbanCode Deploy.
<!--  1. Set up a system to run DevOps Connect. See [prerequisites](uc_insights_prereqs.html).
  1. Download DevOps Connect, which is provided in a runnable JAR file.
  1. Copy the script from the **Delivery Insights Setup** page and run it. This command starts DevOps Connect with a token that allows it to connect to your organization on {{site.data.keyword.Bluemix}}.
  1. Connect your IBM UrbanCode Deploy servers to DevOps connect. See [Connecting IBM UrbanCode Deploy servers to Delivery Insights](uc_insights_connect_ucd.html). -->


Si vous disposez déjà d'une chaîne d'outils, procédez comme suit pour ajouter Delivery Insights :
1. Si vous ne disposez pas de l'outil {{site.data.keyword.DRA_short}}, ajoutez-le à votre chaîne d'outils.
1. Sur votre chaîne d'outils, cliquez sur l'outil {{site.data.keyword.DRA_short}}.
1. Sur la page **Delivery Insights Setup**, suivez la procédure pour configurer DevOps Connect et connecter vos serveurs IBM UrbanCode Deploy.

Après avoir configuré Delivery Insights et DevOps Connect, vous pouvez afficher les données des serveurs IBM UrbanCode Deploy dans Delivery Insights. Voir [Connexion de serveurs IBM UrbanCode Deploy à Delivery Insights](uc_insights_connect_ucd.html).

<!-- 
For questions or issues, see the [questions forum](https://developer.ibm.com/answers/?community=urbancode).
--> 

![Deux graphiques représentant des données de démonstration UrbanCode Insights](images/uc_insights_demo_data.gif)

Delivery Insights vous permet de visualiser notamment les informations suivantes :

- Statistiques sur le déploiement, dont la durée et le volume de déploiement dans le temps.
- Statistiques sur le taux d'échec de déploiement par application et par environnement.
- Statistiques sur le déploiement de composant, avec le taux d'échec, l'heure et la durée du déploiement.

## Présentation des systèmes

La topologie de Delivery Insights inclut une ou plusieurs installations sur site d'IBM UrbanCode Deploy <!-- (and optionally IBM UrbanCode Release) --> et l'utilitaire DevOps Connect.

Le diagramme suivant représente une installation typique de ces systèmes.

![Topologie de présentation d'UrbanCode Insights, avec des systèmes sur site client et IBM Cloud Services](images/uc_insights_overview_topology_multi_ucd.png)

- Une installation d'**IBM UrbanCode Deploy** fournit des informations sur les déploiements ayant abouti et les déploiements ayant échoué destinées aux mesures. IBM UrbanCode Deploy requiert un correctif pour communiquer avec IBM Bluemix DevOps Connect.

<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect**, anciennement IBM UrbanCode Sync Utility, coordonne la communication entre des installations sur site d'IBM UrbanCode Deploy <!-- and IBM UrbanCode Release --> et des services hébergés par IBM, tels que UrbanCode Insights. DevOps Connect utilise la communication HTTPS sécurisée vers les serveurs sur site et l'authentification par jeton pour fournir des données à UrbanCode Insights.

  DevOps Connect requiert des plug-in pour se connecter aux autres systèmes de la topologie.

- **Delivery Insights**, un composant de {{site.data.keyword.DRA_short}}, fournit des mesures sur l'activité de déploiement sur IBM UrbanCode Deploy, avec notamment les heures de déploiement et les taux d'échec par groupes d'environnements. L'autorisation est contrôlée par des comptes {{site.data.keyword.Bluemix}}.
