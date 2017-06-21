---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Intégration avec des projets Jenkins à structure libre

Après avoir ajouté {{site.data.keyword.DRA_full}} à une chaîne d'outils ouverte et défini les politiques qu'il surveille, vous pouvez l'intégrer à votre projet Jenkins à structure libre. Les projets Jenkins à structure libre sont configurés et administrés à partir de l'interface Web Jenkins. 

Le plug-in IBM Cloud DevOps pour Jenkins intègre des projets Jenkins à des chaînes d'outils. Une *chaîne d'outils* est un ensemble d'intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations. La puissance collective d'une chaîne d'outils est supérieure à la somme de ses intégrations d'outils individuelles. Les chaînes d'outils ouvertes font partie du service {{site.data.keyword.contdelivery_full}}. Pour en savoir plus sur le service {{site.data.keyword.contdelivery_short}}, voir [la documentation associée](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Après avoir installé le plug-in IBM Cloud DevOps, vous pouvez publier les résultats de test dans {{site.data.keyword.DRA_short}}, ajouter des jalons de qualité automatisés et effectuer le suivi des risques de déploiement. Vous pouvez également envoyer des notifications de travail à d'autres outils de la chaîne d'outils, tels que Slack et PagerDuty. Afin de faciliter le suivi des déploiements, la chaîne d'outils peut ajouter des messages de déploiement aux validations Git, ainsi qu'aux problèmes Git ou JIRA associés. Vous pouvez également afficher vos déploiements sur la page Connexions de votre chaîne d'outils. 

Le plug-in fournit des actions et des interfaces de ligne de commande post-génération pour la prise en charge de l'intégration. {{site.data.keyword.DRA_short}} agrège et analyse les résultats des tests d'unité, des tests fonctionnels, des outils de couvertures de code, des examens du code de sécurité statique et des examens du code de sécurité dynamique afin de déterminer si votre code répond aux politiques prédéfinies aux jalons de votre processus de déploiement. Si votre code ne satisfait pas ou dépasse une politique, le déploiement est interrompu afin de prévenir toute modification à risque. Vous pouvez utiliser {{site.data.keyword.DRA_short}} comme filet de sécurité pour votre environnement de distribution continue en vue d'implémenter et d'améliorer les normes qualité au fil du temps, ainsi que comme outil de visualisation de données pour vous aider à comprendre la santé de votre projet.

## Prérequis
{: #jenkins_prerequisites}

Vous devez avoir accès à un serveur qui exécute un projet Jenkins.

## Création d'une chaîne d'outils
{: #jenkins_create}

Avant de pouvoir intégrer {{site.data.keyword.DRA_short}} à un projet Jenkins, vous devez créer une chaîne d'outils. 

1. Pour créer une chaîne d'outils, accédez à la [page Créer une chaîne d'outils](https://console.ng.bluemix.net/devops/create) et suivez les instructions. 

2. Après avoir créé la chaîne d'outils, ajoutez-y{{site.data.keyword.DRA_short}}. Pour plus d'instructions, voir la [documentation {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

## Installation du plug-in
{: #jenkins_install}

Installez d'abord le plug-in sur votre serveur Jenkins. Ouvrez l'interface du serveur, puis : 

1. Cliquez sur **Manage Jenkins**.
2. Cliquez sur **Manage Plugins**. 
3. Cliquez sur l'onglet **Available**.
4. Activez le filtre en fonction d'`IBM Cloud DevOps`. 
5. Sélectionnez IBM Cloud DevOps.
6. Cliquez sur **Download now and install after restart**. 

Le plug-in est disponible après le redémarrage du serveur.   

## Configuration des travaux Jenkins pour les tableaux de bord Deployment Risk
{: #jenkins_configure}

Une fois le plug-in installé, vous pouvez intégrer {{site.data.keyword.DRA_short}} dans votre projet Jenkins. 

Suivez la procédure ci-après pour utiliser les jalons et le tableau de bord de Deployment Risk avec votre projet.

1. Ouvrez la configuration de n'importe quel travail dont vous disposez, comme une génération, un test ou un déploiement.

2. Ajoutez une action post-génération pour le type correspondant :

   * Pour les travaux de génération, utilisez **Publish build information to IBM Cloud DevOps**.
   
   * Pour les travaux de test, utilisez **Publish test result to IBM Cloud DevOps**.
   
   * Pour les travaux de déploiement, utilisez **Publish deployment information to IBM Cloud DevOps**.
   
3. Renseignez les zones requises. Elles varient selon le type de travail. 

   * Dans la liste **Credentials**, sélectionnez votre ID et votre mot de passe {{site.data.keyword.Bluemix_notm}}. S'ils ne sont pas sauvegardés dans Jenkins, cliquez sur **Add** pour les sauvegarder. Testez votre connexion à {{site.data.keyword.Bluemix_notm}} en cliquant sur **Test Connection**.
   
   * Dans la zone **Build Job Name**, indiquez le nom de votre travail de génération exactement tel qu'il apparaît dans Jenkins. Si la génération s'effectue en même temps que le travail de test, laissez cette zone vide. Si le travail de génération s'effectue hors de Jenkins, cochez la case **Builds are being done outside of Jenkins**, puis indiquez le numéro de version et l'URL de génération.
   
   * Pour l'environnement, si les tests sont exécutés lors de l'étape de génération, ne sélectionnez que l'environnement de génération. Si les tests sont exécutés à l'étape de déploiement, sélectionnez l'environnement de déploiement et indiquez le nom de l'environnement. Deux valeurs sont prises en charge : `STAGING` et `PRODUCTION`.
   
   * Pour la zone **Result File Location**, indiquez l'emplacement du fichier de résultats. Si le test ne génère aucun fichier de résultats, laissez cette zone vide. Le plug-in télécharge un fichier de résultats par défaut en fonction du statut du travail de test en cours.

   Les images suivantes représentent des exemples de configuration :
   
   ![Téléchargement des informations de génération](images/Upload-Build-Info.png "Publication des informations de génération dans DRA") *Publication des informations de génération*
   
   ![Téléchargement des résultats de test](images/Upload-Test-Result.png "Publication des résultats de test dans DRA") *Publication des résultats de test*
   
   ![Téléchargement des informations de déploiement](images/Upload-Deployment-Info.png "Publication des informations de déploiement dans DRA") *Publication des informations de déploiement*

4. Si vous voulez utiliser des jalons de politique {{site.data.keyword.DRA_short}} pour contrôler un travail de déploiement en aval, ajoutez une action post-génération **IBM Cloud DevOps Gate**. Choisissez une politique et indiquez la portée des résultats de test. Pour autoriser les jalons de politique à empêcher les déploiements en aval, cochez la case **Fail the build based on the policy rules**. L'image suivante représente un exemple de configuration :

    ![Jalon DevOps Insights](images/DRA-Gate.png "Jalon DevOps Insights")

5. Exécutez votre travail de génération Jenkins.

6. Affichez le tableau de bord Deployment Risk en accédant à [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops), en sélectionnant votre chaîne d'outils et en cliquant sur **DevOps Insights**.

Le tableau de bord Deployment Risk repose sur la présence d'un jalon après un travail de déploiement de préproduction. Si vous voulez utiliser le tableau de bord, vérifiez qu'il existe un jalon après le déploiement vers l'environnement de préproduction, mais avant le déploiement vers un environnement de production.
    
## Configuration des notifications
{: #jenkins_notifications}

Vous pouvez configurer vos travaux Jenkins pour qu'ils envoient les notifications à des outils tels que Slack ou PagerDuty en suivant les instructions de la [documentation Bluemix](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins).
