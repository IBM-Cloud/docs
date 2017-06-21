---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à DevOps Insights (Bêta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} applique l'analyse du développeur, de l'équipe et de déploiement à vos projets DevOps les plus actifs. Il vous permet de savoir dans quelle mesure votre équipe se conforme aux pratiques DevOps et du développeur, de gérer les risques du codebase et d'appliquer des normes de qualité dans des projets de distribution continue.
{:shortdesc}

{{site.data.keyword.DRA_short}} comprend plusieurs groupes de fonctionnalités :

   * Developer Insights fournit une méthode globale permettant d'explorer la maturité de développement de votre projet. Vous pouvez identifier les fichiers présentant une prédisposition élevée aux erreurs et obtenir une vue de conformité du projet par rapport aux pratiques du développeur.

   * Team Dynamics utilise l'analyse du codage social pour vous aider à déterminer comment votre équipe collabore et à comprendre ce qui peut être modifié pour un meilleur fonctionnement.

   * Deployment Risk est comparable à un filet de sécurité pour votre pipeline de distribution continue. Il analyse les résultats provenant des tests d'unité, tests fonctionnels, examens d'application et outils de couverture du code à des jalons spécifiques de votre processus de déploiement, et empêche la publication des changements risqués.

   * Delivery Insights affiche des statistiques et des mesures liées au déploiement, ainsi que d'autres informations sur votre installation IBM UrbanCode Deploy. Il peut ainsi présenter des graphiques concernant la durée du déploiement, les réussites et les échecs, triés par environnements regroupés de manière logique. Voir
[Intégration de DevOps Insights avec IBM UrbanCode Deploy](/docs/services/DevOpsInsights/uc_insights_overview.html).

{{site.data.keyword.DRA_short}} est une intégration figurant dans le catalogue des chaînes d'outils ouvertes Bluemix. Pour plus d'informations sur les chaînes d'outils, voir [Utilisation des chaînes d'outils](/docs/services/ContinuousDelivery/toolchains_working.html).

Pour utiliser {{site.data.keyword.DRA_short}}, vous devez l'ajouter à une chaîne d'outils. De nombreux modèles de chaîne d'outils incluent déjà {{site.data.keyword.DRA_short}}. Veillez à également [l'ajouter à votre organisation {{site.data.keyword.Bluemix_notm}} en tant que service](/docs/services/reqnsi.html) pour pouvoir visualiser des informations sur {{site.data.keyword.DRA_short}} et accéder à certains modèles de chaîne d'outils qui l'incluent à partir de votre tableau de bord {{site.data.keyword.Bluemix_notm}}.  

## Ajout de DevOps Insights à une chaîne d'outils
{: #catalog}

{{site.data.keyword.DRA_short}} fait partie de {{site.data.keyword.contdelivery_short}}. Vous pouvez ajouter {{site.data.keyword.DRA_short}} à n'importe quelle chaîne d'outils en sélectionnant cette dernière dans le catalogue des intégrations d'outil.

{{site.data.keyword.DRA_short}} est également inclus dans de nombreux modèles de chaîne d'outils. Si vous créez une chaîne d'outils à partir d'un modèle qui comprend {{site.data.keyword.DRA_short}}, veillez à ce que {{site.data.keyword.DRA_short}} soit défini sur **Avancé**. Créez ensuite la chaîne d'outils et passez à [Utilisation de DevOps Insights](/docs/services/DevOpsInsights/index.html#using).

Pour ajouter {{site.data.keyword.DRA_short}} à une chaîne d'outils :

1. Cliquez sur **Ajouter un outil**.

2. Cliquez sur **{{site.data.keyword.DRA_short}}**.

3. Cliquez sur **Créer une intégration**.

{{site.data.keyword.DRA_short}} est maintenant disponible sur la page de présentation de votre chaîne d'outils. Une recherche de données est automatiquement effectuée sur votre référentiel et votre système de suivi des problèmes. 

## Utilisation de DevOps Insights
{: #using}

Si votre chaîne d'outils inclut GitHub, GitLab ou JIRA, {{site.data.keyword.DRA_short}} vous fournit automatiquement des informations sur votre codebase et votre équipe après un premier rassemblement et une analyse initiale des données. Si votre chaîne d'outils n'inclut aucune de ces intégrations, ajoutez-en une, puis procédez comme suit :

1. Sur la page de présentation de votre chaîne d'outils, cliquez sur **{{site.data.keyword.DRA_short}}**.

2. Cliquez sur **Team Dynamics** ou sur **Developer Insights**, puis choisissez une catégorie de données.  

3. Explorez les données de votre projet en affichant les tableaux de bord dans la catégorie de données. Si vous voulez en savoir plus sur un graphique ou savoir ce que vous pouvez faire de ces informations, cliquez sur **Informations** ou sur **Conseils**.

Après avoir exploré Team Dynamics et Developer Insights, [configurez Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html) pour faciliter l'application de la qualité du code. Deployment Risk est compatible à la fois avec le pipeline {{site.data.keyword.contdelivery_short}} et Jenkins.   
