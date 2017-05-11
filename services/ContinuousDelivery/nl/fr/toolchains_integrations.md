---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}    

# Configuration d'intégrations d'outils
{: #integrations}

Vous pouvez configurer des intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations lors de la création d'une chaîne d'outils ouverte, ou bien vous pouvez ajouter et configurer des intégrations d'outils afin de personnaliser une chaîne d'outils existante.  
{:shortdesc}

**Important** : Sur {{site.data.keyword.Bluemix_notm}} public, les chaînes d'outils sont disponibles uniquement dans la région sud des Etats-Unis.

Les intégrations d'outils disponibles pour ajouter et configurer votre chaîne d'outils varient selon que vous utilisez des chaînes d'outils sur {{site.data.keyword.Bluemix_notm}} Public ou {{site.data.keyword.Bluemix_notm}} Dédié. Si
vous utilisez des chaînes d'outils sur
{{site.data.keyword.Bluemix_notm}} Dédié, les
intégrations d'outils qui sont disponibles dépendent de la manière
dont {{site.data.keyword.contdelivery_full}} a été configuré dans
votre environnement spécifique.

|Intégration d'outils |Disponible sur {{site.data.keyword.Bluemix_notm}} Public	|Disponible sur {{site.data.keyword.Bluemix_notm}} Dédié
(dépendant de l'environnement)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.alertnotificationshort}}		|Oui		|Non		|
|Artifactory		|Oui		|Non		|
|Availability Monitoring		|Oui		|Non		|
|Cloud Event Management		|Oui		|Non		|
|{{site.data.keyword.deliverypipeline}} 		|Oui	   	|Oui  		|
|{{site.data.keyword.DRA_short}} 		|Oui		|Non			|
|Eclipse Orion {{site.data.keyword.webide}}		|Oui		|Oui			|
|Git Repos and Issue Tracking	|Oui		|Non		|
|GitHub et problèmes		|Oui		|Oui		|
|Dedicated {{site.data.keyword.ghe_short}} and Issues			|Non		|Oui		|
|Jenkins		|Oui		|Non		|
|JIRA		|Oui		|Non		|
|Nexus			|Oui		|Non		|
|Autre outil			|Oui		|Oui		|
|PagerDuty			|Oui		|Oui		|
|Sauce Labs		|Oui		|Non		|
|Slack			|Oui		|Oui		|
{: caption="Table 1. Tool integrations available for toolchains on {{site.data.keyword.Bluemix_notm}} Public et Dédié" caption-side="top"}

**Conseil** : Si vous souhaitez débuter le développement par votre code source sur {{site.data.keyword.Bluemix_notm}} Public, configurez les intégrations d'outils GitHub et Git Repos and Issue Tracking avant de configurer {{site.data.keyword.deliverypipeline}}. Si vous souhaitez débuter le développement par votre code source sur
{{site.data.keyword.Bluemix_notm}} dédié, configurez
l'intégration d'outils {{site.data.keyword.ghe_short}} ou
l'intégration d'outils GitHub avant
de configurer {{site.data.keyword.deliverypipeline}}.


## Configuration d'Alert Notification (expérimental)
{: #alertnotification}

{{site.data.keyword.alertnotificationfull}} est une solution hybride basée sur le cloud, que vous pouvez utiliser pour centraliser et simplifier votre stratégie de notification. Elle fonctionne avec d'autres applications sur site et basées sur le cloud. Les alertes sont envoyées à {{site.data.keyword.alertnotificationshort}} à l'aide d'une API RESTful sécurisée.

Configurez {{site.data.keyword.alertnotificationshort}} pour recevoir des notifications sur les problèmes qui surviennent au cours de votre processus DevOps. 

### Conditions préalables requises

1. Si vous ne disposez pas d'un compte {{site.data.keyword.alertnotificationshort}}, inscrivez-vous pour en obtenir un :

 a. Ouvrez la page [IBM {{site.data.keyword.alertnotificationshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/us-en/marketplace/alert-notification){: new_window} dans IBM Marketplace.

 b. Achetez un abonnement ou inscrivez-vous à l'essai gratuit pendant 90 jours.

1. Une fois que votre compte {{site.data.keyword.alertnotificationshort}} est configuré, ouvrez votre [Tableau de bord IBM![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://myibm.ibm.com/dashboard/){: new_window}.
1. En regard d'IBM {{site.data.keyword.alertnotificationshort}}, cliquez sur **Lancer**.
1. Cliquez sur **Gérer les clés d'API**, puis sur **Créer une clé d'API**.
1. Dans la zone **Créer une clé d'API**, saisissez une description.
1. Cliquez sur **Générer**. Les informations relatives à la nouvelle clé d'API, notamment son nom et son mot de passe, s'affichent. Etant donné que vous aurez besoin de ces informations pour la configuration de l'intégration d'outils, gardez la fenêtre Nouvelle clé d'API ouverte. A des fins de sécurité, vous ne pouvez pas récupérer le mot de passe de la clé d'API ultérieurement. 

### Configuration de l'application Alert Notification

1. Si vous configurez cette intégration d'outils lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **{{site.data.keyword.alertnotificationshort}}**. 
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**. Ensuite, cliquez sur **Vue d'ensemble**.  

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **{{site.data.keyword.alertnotificationshort}}**.

1. Saisissez l'URL de l'API {{site.data.keyword.alertnotificationshort}} que vous souhaitez utiliser. Vous trouverez cette adresse sur la page Gestion des clés d'API du service {{site.data.keyword.alertnotificationshort}} ; par exemple, `https://ibmnotifybm.mybluemix.net/api/alerts/v1`.
1. Saisissez le nom de la clé d'API pour {{site.data.keyword.alertnotificationshort}}. Vous le trouverez dans la fenêtre Nouvelle clé d'API. 
1. Saisissez le mot de passe généré par {{site.data.keyword.alertnotificationshort}} pour la clé d'API. Vous le trouverez dans la fenêtre Nouvelle clé d'API. 
1. Cliquez sur **Créer une intégration**.
1. A partir de votre chaîne d'outils, cliquez sur **{{site.data.keyword.alertnotificationshort}}**.

Pour plus d'informations, voir [IBM {{site.data.keyword.alertnotificationshort}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/manage/tool_alert_notification/){: new_window}.


## Configuration d'Artifactory
{: #artifactory}

Configurez le gestionnaire de référentiels Artifactory afin de stocker les artefacts de génération dans votre référentiel Artifactory : 

1. Si vous configurez cette intégration d'outils lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Artifactory**.
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**. Ensuite, cliquez sur **Vue d'ensemble**.  

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **Artifactory**.

1. Saisissez l'URL du référentiel Artifactory qui doit s'ouvrir lorsque vous cliquez sur la carte Artifactory.
1. Sélectionnez le type de référentiel auquel vous souhaitez vous connecter.
1. Si vous utilisez un registre npm Artifactory, procédez comme suit :

 a. Saisissez l'adresse électronique associée à votre registre.

 b. Saisissez le jeton d'authentification associé à votre registre.

 c. Saisissez l'URL de votre référentiel d'édition Artifactory, qui est votre registre privé sur le serveur Artifactory.

 d. Saisissez l'URL du registre miroir ou public que vous utilisez pour combiner plusieurs registres npm publics et privés. Par exemple, cette URL peut être l'adresse du registre virtuel sur votre serveur Artifactory, qui peut accéder à la fois à votre registre privé et à un cache du registre npm global.

1. Si vous utilisez un référentiel Maven Artifactory, procédez comme suit :

 a. Saisissez l'ID utilisateur associé à votre référentiel.

 b. Saisissez le mot de passe associé à votre référentiel.

 c. Saisissez l'URL de votre référentiel d'édition Artifactory, qui est votre référentiel d'édition privé sur le serveur Artifactory.

 d. Saisissez l'URL de votre référentiel d'image instantanée Artifactory, qui est votre référentiel d'image instantanée privé sur le serveur Artifactory.

 e. Saisissez l' URL du référentiel miroir ou public que vous utilisez pour combiner plusieurs référentiels Maven publics et privés. Par exemple, cette URL peut être l'adresse du référentiel virtuel sur votre serveur Artifactory, qui peut accéder à la fois à vos référentiels privés et à un cache du référentiel Maven central.

1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la carte du référentiel Artifactory à utiliser. Le site Web Artifactory s'ouvre ; vous pouvez y afficher le contenu du référentiel.
1. Facultatif : Si vous utilisez une chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} Public et que vous voulez générez votre application à l'aide d'Artifactory avec npm, configurez votre pipeline pour ajouter un travail de génération npm. Pour des instructions de configuration du travail de génération, voir la section [Configuration d'un travail de génération npm Artifactory sur votre pipeline](#config_artifactory_npm).
1. Facultatif : Si vous utilisez une chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} Public et que vous voulez générer votre application à l'aide d'Artifactory avec Maven, configurez votre pipeline pour ajouter un travail de génération Maven. Pour des instructions de configuration du travail de génération, voir la section [Configuration d'un travail de génération Maven Artifactory sur votre pipeline](#config_artifactory_maven).

### Configuration d'un travail de génération npm Artifactory sur votre pipeline
{: #config_artifactory_npm}

Avant de configurer un travail de génération npm sur votre pipeline, vous devez disposer d'un pipeline opérationnel qui peut utiliser votre référentiel SCM de génération en entrée et vous devez configurer Artifactory pour votre chaîne d'outils. Pour les instructions de configuration d'Artifactory, voir la section [Artifactory](#artifactory). 

Configurez {{site.data.keyword.deliverypipeline}} pour ajouter un travail de génération npm :

1. Créez une étape et définissez l'entrée sur le référentiel SCM approprié.
1. Dans l'étape, ajoutez un travail de génération.
1. Configurez le travail de génération :
  ![travail de génération npm](images/artifactory_npm_job.png)

  a. Pour le type de générateur, sélectionnez **NPM Build**.

  b. Si vous avez configuré plusieurs instances de l'intégration d'outils Artifactory, saisissez le nom de l'intégration d'outils Artifactory pour laquelle vous souhaitez configurer le travail de génération npm. 

  c. Pour le type d'intégration d'outils, sélectionnez **Artifactory**.

  d. Pour la commande de génération, saisissez les commandes permettant de générer votre module npm ou de le publier dans votre registre. Cet exemple montre les commandes de génération ou de publication du module.
     ```
     npm install
     # ou
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Conseil** : Vous pouvez trouver l'URL et les données d'identification de l'utilisateur dont vous vous êtes servi pour vous connecter à votre registre dans les paramètres de configuration pour l'intégration d'outils Artifactory.
  e. Si votre travail de génération est publié dans le registre Artifactory et que le format de votre version de module de noeud est `x.y.z-SNAPSHOT.w`, cochez la case **Increment snapshot module version**. Le travail de génération met automatiquement à jour la version du module avant que le travail ne soit publié dans le registre Artifactory. Le travail sélectionne la version la plus élevée du module à partir du registre npm et du fichier local `package.json`, et incrémente la version du module à l'aide de semver. Le travail de génération ne répercute pas les modifications dans le référentiel SCM. 

1. Cliquez sur **SAUVEGARDER**. Lors de l'exécution de votre pipeline, ce travail de génération utilise les informations de configuration provenant de l'intégration d'outils pour la connexion à votre registre npm. 

### Configuration d'un travail de génération Maven Artifactory sur votre pipeline
{: #config_artifactory_maven}

Avant de configurer un travail de génération Maven sur votre pipeline, vous devez disposer d'un pipeline opérationnel qui peut utiliser votre référentiel SCM de génération en entrée et vous devez configurer Artifactory pour votre chaîne d'outils. Pour les instructions de configuration d'Artifactory, voir la section [Artifactory](#artifactory). 

Configurez {{site.data.keyword.deliverypipeline}} pour ajouter un travail de génération Maven :

1. Créez une étape et définissez l'entrée sur le référentiel SCM approprié.
1. Dans l'étape, ajoutez un travail de génération.
1. Configurez le travail de génération :
  ![travail de génération Maven](images/artifactory_maven_job.png)

  a. Pour le type de générateur, sélectionnez **Maven Build**.

  b. Si vous avez configuré plusieurs instances de l'intégration d'outils Artifactory, saisissez le nom de l'intégration d'outils Artifactory pour laquelle vous souhaitez configurer le travail de génération Maven. 

  c. Pour le type d'intégration d'outils, sélectionnez **Artifactory**.

  d. Pour la commande de génération, saisissez les commandes permettant de générer votre module Maven ou de le publier dans votre registre d'image instantanée. Cet exemple montre les commandes permettant de générer le module ou de le publier dans un registre d'image instantanée.
     ```
     mvn -B clean package
     # ou
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Conseil** : Vous pouvez trouver l'URL et les données d'identification de l'utilisateur dont vous vous êtes servi pour vous connecter à votre registre dans les paramètres de configuration pour l'intégration d'outils Artifactory.
1. Cliquez sur **SAUVEGARDER**. Lors de l'exécution de votre pipeline, ce travail de génération utilise les informations de configuration provenant de l'intégration d'outils pour la connexion à votre référentiel Maven. 

Pour en savoir plus, voir [Artifactory ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/code/tool_artifactory/){: new_window}.


## Ajout d'Availability Monitoring
{: #availabilitymonitoring}

{{site.data.keyword.prf_hublong}} isole les problèmes, identifie les masques et améliore les performances avant que les utilisateurs ne s'en trouvent affectés. Vous pouvez tester votre appli depuis le monde entier, l'intégrer à des pipelines de distribution et gagner en connaissance sur la façon d'optimiser en permanence votre code.

**Remarque** : Cette intégration d'outils est préconfigurée et ne nécessite aucun paramètre de configuration. Vous ne pouvez pas la reconfigurer.

Pour tester, surveiller et améliorer la santé de votre appli au fur et à mesure de sa création, ajoutez l'intégration d'outils {{site.data.keyword.prf_hubshort}}. 

1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, sur la page Chaînes d'outils, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis la page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **{{site.data.keyword.prf_hubshort}}**.

1. Cliquez sur **Créer une intégration**.
1. Cliquez sur **{{site.data.keyword.prf_hubshort}}** pour ouvrir le tableau de bord {{site.data.keyword.prf_hubshort}}, sélectionner une application et configurer sa surveillance. 

Pour en savoir plus, voir [{{site.data.keyword.prf_hublong}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/manage/tool_bluemix_availability_monitoring/){: new_window}.


## Ajout de Cloud Event Management (expérimental)
{: #cloudeventmanagement}

{{site.data.keyword.evtmgt_full}} fournit une vue d'ensemble des problèmes qui surviennent dans vos services, vos applications et votre infrastructure. Vous pouvez configurer la gestion des incidents en temps réel pour résoudre les problèmes plus efficacement.

**Remarque :** Cette intégration d'outils est préconfigurée et ne nécessite aucun paramètre de configuration. Vous ne pouvez pas la reconfigurer.

Pour aider votre équipe DevOps à atteindre des objectifs fiables et opérationnels en matière de santé, de qualité de service et d'amélioration continue, ajoutez Cloud Event Management à votre chaîne d'outils : 

1. Dans le tableau de bord DevOps, sur la page Chaînes d'outils, cliquez sur la chaîne d'outils à ajouter à Cloud Event Management. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **Cloud Event Management**.

1. Cliquez sur **Créer une intégration**.
1. A partir de votre chaîne d'outils, cliquez sur l'une des cartes d'outils suivantes :

 * **Cloud Event Management** pour vous initier à Cloud Event Management.

 * **{{site.data.keyword.alertnotificationshort}}** pour créer des règles qui déterminent le moment où les utilisateurs reçoivent des notifications d'incident.

 * **Runbook Automation** pour gérer votre catalogue de dossiers d'exploitation dans Cloud Event Management.


## Configuration de Delivery Pipeline
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} automatise le déploiement continu de vos projets via des séquences d'étapes qui extraient des travaux en entrée et d'exécution tels que des générations, des tests et des déploiements.

Configurez {{site.data.keyword.deliverypipeline}} afin d'automatiser la génération, le test et le déploiement en continu de vos applications.

1. Si vous configurez cette intégration d'outils lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **{{site.data.keyword.deliverypipeline}}**. En fonction du modèle utilisé, des zones différentes peuvent être disponibles. Passez en revue les valeurs de zone par défaut et, si nécessaire, modifiez ces paramètres.
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **{{site.data.keyword.deliverypipeline}}**.

1. Indiquez un nom pour votre nouveau pipeline.
1. Si vous comptez utiliser votre pipeline pour déployer une interface utilisateur, cochez la case **Afficher les applications dans le menu AFFICHER
L'APPLICATION**. Toutes les applications créées par votre pipeline sont affichées dans la liste **Afficher l'application** de la page
Présentation de la chaîne d'outils.
1. Cliquez sur **Créer une intégration** pour ajouter {{site.data.keyword.deliverypipeline}} à votre chaîne d'outils.
1. Cliquez sur **{{site.data.keyword.deliverypipeline}}** pour afficher le pipeline et le configurer. Pour en savoir plus sur les notions de base et la configuration d'un pipeline, voir [Génération et déploiement de pipelines](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}.

  **Conseil **: Si vous souhaitez déclencher le pipeline lorsque vous envoyez des modifications à votre référentiel GitHub, {{site.data.keyword.ghe_short}} ou Git, vous devez configurer GitHub, {{site.data.keyword.ghe_short}} ou Git Repos and Issue Tracking
pour votre chaîne d'outils avant de définir les étapes du pipeline. Ces étapes requièrent les URL de vos référentiels. Chaque étape de pipeline peut faire référence à un seul des référentiels GitHub, {{site.data.keyword.ghe_short}} ou Git associés à votre chaîne d'outils. Pour
les instructions de configuration de GitHub, voir la section [GitHub](#github). Pour des instructions sur la configuration de {{site.data.keyword.ghe_short}} Dédié, voir [Initiation à {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}. Pour des instructions sur la configuration de Git Repos and Issue Tracking, voir la section [Git Repos and Issue Tracking](##gitbluemix).    

  **Remarque :** Si vous ne disposez pas de privilèges admin pour le référentiel GitHub ou GitHub Enterprise, ni de privilèges Maître ou Propriétaire pour le référentiel Git Repos and Issue Tracking auquel vous vous liez, votre intégration sera limitée car vous ne pouvez pas utiliser d'ancrage Web. Les ancrages Web sont nécessaires pour déclencher automatiquement un pipeline lorsqu'une validation est envoyée par commande push au référentiel. Sans ancrage Web, vous devez démarrer manuellement vos pipelines.

1. Facultatif : Si vous utilisez une chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} public et souhaitez que Sauce Labs exécute des tests sur votre application, configurez {{site.data.keyword.deliverypipeline}} pour ajouter un travail de test Sauce Labs. Pour des instructions de configuration du travail de test, voir la section [Configuration d'un travail de test Sauce Labs sur votre pipeline](#config_saucelabs).

### Configuration d'un travail de test Sauce Labs sur votre pipeline
{: #config_saucelabs}

Avant de configurer un travail de test Sauce Labs sur votre pipeline, vous avez besoin d'un pipeline opérationnel qui comporte des étapes pour la génération et le déploiement de votre application et vous devez configurer Sauce Labs pour votre chaîne d'outils. Pour des instructions de configuration de Sauce Labs, voir la section [Configuration de Sauce Labs](#saucelabs).

Configurez {{site.data.keyword.deliverypipeline}} pour ajouter un travail de test Sauce Labs.

1. Si vous n'avez pas d'étape pour le déploiement d'une version de test de votre application, créez-en une.
1. Dans l'étape, ajoutez un travail de test après le travail de déploiement. Le fait de placer ces travaux dans la même étape leur permet d'accéder au même ensemble de propriétés d'environnement.   
  ![Travail de test](images/toolchain_test_job.png)

1. Configurez l'étape :

  a. Dans l'onglet **PROPRIETES D'ENVIRONNEMENT**, créez trois propriétés : CF_APP_NAME, SAUCE_USERNAME et SAUCE_ACCESS_KEY.

  b. Entrez vos nom d'utilisateur et clé d'accès Sauce Labs. En procédant ainsi, vous externalisez ces valeurs de façon à pouvoir les utiliser dans vos tests.

1. Configurez le travail de déploiement. Dans la zone **Script de déploiement**, ajoutez la commande suivante : `export CF_APP_NAME="$CF_APP"`. Cette commande exporte le nom d'application en tant que propriété d'environnement.
1. Configurez le travail de test. Les valeurs figurant dans l'image suivante sont des exemples. Les zones d'**instance de service**, de **cible**, d'**organisation** et d'**espace** sont renseignées avec les informations Sauce Labs de nom d'utilisateur, région, organisation et espace que vous utilisez.  
![Configuration du travail](images/toolchain_configure_job.png)

  a. Pour le type d'outil de test, sélectionnez **Sauce Labs**.

  b. Pour l'instance de service, sélectionnez le nom d'utilisateur Sauce Labs utilisé lors de la configuration de Sauce Labs pour votre chaîne d'outils.

   **Conseil **: Pour voir le nom d'utilisateur et la clé d'accès que vous avez utilisés lors de la configuration de Sauce Labs pour votre chaîne d'outils, cliquez sur **Configurer**.

  c. Dans la zone de **commande d'exécution de test**, entrez les commandes d'installation des dépendances qui sont requises par vos tests, puis exécutez les tests. Par exemple, pour une application Node.js, vous pourriez entrer les commandes suivantes :
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```

    d. Si vous souhaitez voir vos rapports de test dans les journaux de travail, sélectionnez la case **Activer le rapport de test** et définissez le masque de fichiers de résultats de test sur `test/*.xml`.

1. Cliquez sur **SAUVEGARDER**. A chaque exécution de votre pipeline, vos tests Sauce Labs s'exécuteront.

Pour en savoir plus, voir [Delivery Pipeline ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_delivery_pipeline/){: new_window}.


## Ajout de DevOps Insights (bêta)
{: #dra}

{{site.data.keyword.DRA_full}} collecte et analyse les résultats provenant de tests unitaires, de tests fonctionnels et d'outils de couverture de code afin de déterminer si votre code satisfait les critères prédéfinis à certains stades de votre processus de déploiement. Si votre code ne satisfait pas ou dépasse les critères, le déploiement est interrompu afin de prévenir tout risque. Vous pouvez utiliser {{site.data.keyword.DRA_short}} comme filet de sécurité pour votre environnement de distribution continue ou comme moyen d'implémenter et d'améliorer les normes qualité.

 **Remarque** : Cette intégration d'outils est disponible uniquement sur {{site.data.keyword.Bluemix_notm}} Public. Elle est préconfigurée et ne nécessite aucun paramètre de configuration. Vous ne pouvez pas la reconfigurer.

Ajoutez {{site.data.keyword.DRA_short}} afin de gérer et d'améliorer la qualité de votre code dans {{site.data.keyword.Bluemix_notm}} en surveillant vos déploiements afin d'identifier les risques avant la publication.

1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis la page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **{{site.data.keyword.DRA_short}}**.

1. Cliquez sur **Créer une intégration**.
1. Cliquez sur **{{site.data.keyword.DRA_short}}**, puis complétez les étapes de mise en route : créez des critères, connectez-les au pipeline, puis exécutez ce dernier. 

Pour en savoir plus, voir [{{site.data.keyword.DRA_short}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window}.


## Ajout d'Eclipse Orion Web IDE
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} est un environnement de développement Web intégré dans lequel vous pouvez créer, éditer, exécuter, déboguer et terminer des tâches de contrôle des sources. Vous pouvez facilement passer de l'édition à l'exécution, à la soumission, puis au développement.

 **Remarque** : Cette intégration d'outils est préconfigurée. Elle ne requiert aucun paramètre de configuration et vous ne pouvez pas la reconfigurer.

Pour effectuer des tâches de contrôle des sources, ajoutez l'intégration d'outils Eclipse Orion {{site.data.keyword.webide}} :

1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis la page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **Eclipse Orion Web IDE**.

1. Cliquez sur **Créer une intégration**.
1. Cliquez sur **Eclipse Orion {{site.data.keyword.webide}}**. Votre espace de travail est prérempli avec vos référentiels GitHub ou {{site.data.keyword.ghe_short}}. Les référentiels associés à votre chaîne d'outils en cours sont mis en évidence.

Pour en savoir plus, voir [Edition de code avec Eclipse Orion {{site.data.keyword.webide}}](/docs/services/ContinuousDelivery/web_ide.html){: new_window} et [Eclipse Orion {{site.data.keyword.webide}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/code/tool_eclipse_orion_web_ide/){: new_window}.


## Configuration de Git Repos and Issue Tracking (expérimental)
{: #gitbluemix}

L'intégration d'outils Git Repos and Issue Tracking est basée sur GitLab Community Edition, qui est un service d'hébergement Web pour les référentiels Git. Vous pouvez avoir des copies en local et à distance de vos référentiels. Pour en savoir plus, voir [Git Repos and Issue Tracking (expérimental) ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help){:new_window}.

Si vous configurez Git Repos and Issue Tracking lors de la création de la chaîne d'outils, procédez comme suit :    

1. A la section Intégrations configurables, cliquez sur **Git Repos and Issue Tracking**.
1. Passez en revue les emplacements cible par défaut pour les référentiels Git. Ces référentiels sont clonés à partir des référentiels exemple. Si nécessaire, modifiez les noms des référentiels cible.

Si vous disposez d'une chaîne d'outils et que vous lui ajoutez Git Repos and Issue Tracking, procédez comme suit :    

1. Dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur la chaîne d'outils afin d'ouvrir sa page Vue
d'ensemble. Vous pouvez également, depuis la page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 
1. Cliquez sur **Ajouter un outil**.
1. A la section Intégrations d'outils, cliquez sur **Git Repos and Issue Tracking**.
1. Sélectionnez un type de référentiel :     

  a. Pour créer un référentiel vide, cliquez sur **Nouveau** pour le type de référentiel et saisissez un nom de référentiel.     
  b. Pour dévier un référentiel Git afin de pouvoir participer aux modifications via des demandes de fusion, cliquez sur **Dévier** pour le type de référentiel. Saisissez
l'URL du référentiel source.     
  c. Pour créer une copie d'un référentiel Git, cliquez sur **Cloner** pour le type de référentiel. Saisissez un nouveau nom de référentiel et l'URL du référentiel source.      
  d. Si vous disposez d'un référentiel Git et désirez l'utiliser, cliquez sur **Existant** pour le type de référentiel. Entrez l'adresse URL.    

1. Si vous souhaitez utiliser l'option Problèmes pour le suivi des problèmes, cochez la case **Activer les problèmes**.
1. Si vous voulez suivre le déploiement des modifications du code en créant des étiquettes et des commentaires sur les validations, ainsi que des libellés et des commentaires sur les problèmes référencés par les validations, cochez la case **Suivi du déploiement des modifications du code**. Pour plus d'informations, voir [Suivi de l'emplacement du déploiement du code avec des chaînes d'outils ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la carte du référentiel Git à utiliser. La page de présentation de votre projet s'ouvre.    

**Remarque :** Si vous ne disposez pas de privilèges Maître ou Propriétaire pour le référentiel auquel vous vous liez, votre intégration sera limitée car vous ne pouvez pas utiliser d'ancrage Web. Les ancrages Web sont nécessaires pour déclencher automatiquement un pipeline
lorsqu'une validation est envoyée par commande push au référentiel. Sans ancrage Web, vous devez démarrer manuellement vos pipelines.


## Configuration de GitHub Issues
{: #github}

GitHub est un service d'hébergement Web pour les référentiels Git. Vous pouvez avoir des copies en local et à distance de vos référentiels, ce qui simplifie la collaboration.

GitHub Issues est un outil de suivi qui conserve votre travail et vos plans à un seul et même emplacement. Il est intégré à votre référentiel de développement pour vous permettre de vous concentrer sur les tâches importantes.

Configurez GitHub pour gérer votre code source dans le cloud :

1. Si vous configurez cette intégration d'outils lors de la création de la chaîne d'outils, procédez comme suit :

 a. A la section Intégrations configurables, cliquez sur **GitHub**. Si vous créez la chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} public et si vous n'avez pas autorisé {{site.data.keyword.Bluemix_notm}} à accéder à GitHub, cliquez sur **Autorisation** pour accéder au site Web GitHub. Si vous n'avez pas de session GitHub active, vous êtes invité à vous connecter. Cliquez sur **Authorize Application** pour autoriser {{site.data.keyword.Bluemix_notm}} à accéder à votre compte GitHub. Si vous disposez d'une session GitHub active mais n'avez pas saisi votre mot de passe récemment, vous êtes invité à entrer votre mot de passe GitHub pour confirmation.

 b. Passez en revue les emplacements de référentiel cible par défaut pour les référentiels GitHub. Ces référentiels sont clonés à partir des référentiels exemple. Si nécessaire, modifiez les noms des référentiels cible.
 ![Emplacements de référentiel cible par défaut](images/toolchain_github_config.png)

1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis la page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **GitHub**.

1. Si vous disposez d'un référentiel GitHub et désirez l'utiliser, cliquez sur **Existant** pour le type de référentiel et saisissez l'URL. 
1. Si vous souhaitez utiliser un nouveau référentiel GitHub, indiquez un nom pour le référentiel GitHub, entrez l'URL du référentiel que vous clonez ou déviez, puis sélectionnez le type de référentiel :

 a. Pour créer un référentiel vide, cliquez sur **Nouveau**.

 b. Pour créer une copie d'un référentiel GitHub, cliquez sur **Cloner**.

 c. Pour dévier un référentiel GitHub afin de pouvoir participer aux modifications via des demandes d'extraction, cliquez sur **Dévier**.

1. Si vous souhaitez utiliser GitHub Issues pour le suivi des problèmes, sélectionnez la case **Activer GitHub Issues**.
1. Si vous voulez suivre le déploiement des modifications du code en créant des étiquettes et des commentaires sur les validations, ainsi que des libellés et des commentaires sur les problèmes référencés par les validations, cochez la case **Suivi du déploiement des modifications du code**. Pour plus d'informations, voir [Suivi de l'emplacement du déploiement du code avec des chaînes d'outils ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la carte du référentiel GitHub à utiliser. Le site Web GitHub s'ouvre ; vous pouvez y afficher le contenu du référentiel.

  **Conseil **: Vous pouvez utiliser les outils intégrés de gestion de code source d'Eclipse Orion {{site.data.keyword.webide}} pour éditer le référentiel GitHub et déployer une application depuis votre poste de travail.

1. Si vous avez activé GitHub Issues, cliquez sur **GitHub Issues** pour l'ouvrir. Vous pouvez utiliser cette instance de GitHub Issues pour l'ensemble de votre chaîne d'outils, même si cette dernière contient plusieurs référentiels GitHub.    

**Remarque :** Si vous ne disposez pas de privilèges admin pour le référentiel auquel vous vous liez, votre intégration sera limitée car vous ne pouvez pas utiliser d'ancrage Web. Les ancrages Web sont nécessaires pour déclencher automatiquement un pipeline
lorsqu'une validation est envoyée par commande push au référentiel. Sans ancrage Web, vous devez démarrer manuellement vos pipelines.

Pour plus d'informations, voir [GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} et [GitHub Issues ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configuration de GitHub Enterprise et Issues sur Bluemix Dédié
{: #configghe}

 **Remarque :** Ces instructions s'appliquent à {{site.data.keyword.Bluemix_notm}} Dédié pour {{site.data.keyword.ghe_short}}. Si vous utilisez votre propre version gérée de {{site.data.keyword.ghe_short}}, certaines étapes peuvent varier en fonction de vos procédures internes. 

{{site.data.keyword.ghe_long}} est un service d'hébergement Web sur site pour les référentiels Git. {{site.data.keyword.ghe_short}} Dédié est destiné aux clients {{site.data.keyword.Bluemix_notm}} Dédié uniquement. GitHub Issues est un outil de suivi qui conserve votre travail et vos plans à un seul et même emplacement. Il est intégré à votre référentiel de développement pour vous permettre de vous concentrer sur les tâches importantes. Pour plus d'informations sur {{site.data.keyword.ghe_short}} Dédié et GitHub Issues, voir [Initiation à {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window} et [GitHub Issues ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Vous pouvez configurer {{site.data.keyword.ghe_short}} en tant qu'intégration d'outils dans votre chaîne d'outils afin de pouvoir gérer le code source depuis l'instance de l'environnement [{{site.data.keyword.Bluemix_notm}} Dédié](/docs/dedicated/index.html#dedicated){: new_window} de votre société.

1. Si vous configurez cette intégration d'outils lors de la création de la chaîne d'outils, procédez comme suit :

 a. Avant de vous connecter à {{site.data.keyword.ghe_short}} Dédié pour la première fois, demandez à l'administrateur régional de votre société d'ajouter votre ID utilisateur à votre instance {{site.data.keyword.Bluemix_notm}} Dédié à partir du registre d'utilisateurs de la société, via LDAP. Pour plus d'informations sur la configuration de votre compte {{site.data.keyword.ghe_short}}, voir [Initiation à {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}.

 b. A la section Intégrations configurables, cliquez sur **{{site.data.keyword.ghe_short}}**.    

 c. Vérifiez le nom par défaut pour le nouveau référentiel {{site.data.keyword.ghe_short}}. Si nécessaire, changez le nom du nouveau référentiel. L'image suivante montre un exemple de référentiel cloné à partir d'un référentiel exemple. Vous pouvez utiliser un référentiel existant ou un nouveau référentiel. Pour utiliser un nouveau référentiel, vous pouvez créer un référentiel vide, cloner un référentiel ou dévier un référentiel.
 ![Emplacements de référentiel par défaut](images/toolchain_ghe_config.png)

1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **{{site.data.keyword.ghe_short}}**.

1. Si vous disposez d'un référentiel {{site.data.keyword.ghe_short}} que vous souhaitez utiliser, entrez l'URL du référentiel. Pour le type de référentiel, cliquez sur **Existant**.
1. Si vous souhaitez utiliser un nouveau référentiel {{site.data.keyword.ghe_short}}, indiquez un nom pour le référentiel, entrez l'URL du référentiel que vous clonez ou déviez, puis sélectionnez le type de référentiel :

 a. Pour créer un référentiel vide, cliquez sur **Nouveau**.

 b. Pour créer une copie d'un référentiel, cliquez sur **Cloner**.

 c. Pour dévier un référentiel afin de pouvoir participer aux modifications via des demandes d'extraction, cliquez sur **Dévier**.

1. Pour utiliser GitHub Issues pour le suivi des problèmes, sélectionnez la case **Activer GitHub Issues**.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la carte du référentiel {{site.data.keyword.ghe_short}} à utiliser. Le référentiel {{site.data.keyword.ghe_short}} de votre société s'ouvre.

  **Conseil **: Vous pouvez utiliser les outils intégrés de gestion de code source d'Eclipse Orion {{site.data.keyword.webide}} pour éditer le référentiel {{site.data.keyword.ghe_short}} et déployer une application depuis votre poste de travail.

1. Si vous avez activé GitHub Issues, cliquez sur **GitHub Issues**. Vous pouvez utiliser cette instance de GitHub Issues pour l'ensemble de votre chaîne d'outils, même si cette dernière contient plusieurs référentiels GitHub.    

**Remarque :** Si vous ne disposez pas de privilèges admin pour le référentiel auquel vous vous liez, votre intégration sera limitée car vous ne pouvez pas utiliser d'ancrage Web. Les ancrages Web sont nécessaires pour déclencher automatiquement un pipeline
lorsqu'une validation est envoyée par commande push au référentiel. Sans ancrage Web, vous devez démarrer manuellement vos pipelines.


## Configuration de Jenkins
{: #jenkins}

Jenkins est un outil open source basé sur un serveur, qui génère et teste des logiciels en continu, en prenant en charge les pratiques d'intégration et de distribution continues. 

**Important** : Avant de créer une intégration d'outils Jenkins, vous devez disposer d'un serveur Jenkins.

L'intégration d'outils Jenkins vous permet d'envoyer des notifications de travail Jenkins à d'autres outils de votre chaîne d'outils, comme Slack et PagerDuty. Pour tracer le code dans les déploiements, vous pouvez ajouter des messages de déploiement dans vos validations Git et les problèmes Git ou JIRA associés. Vous pouvez également visualiser vos déploiements dans la page Toolchain Connections. Vous pouvez fournir les résultats de test à {{site.data.keyword.DRA_short}}, ajouter des seuils de qualité automatisés et procéder au suivi des risques de déploiement.

Configurez Jenkins afin d'automatiser la génération, le test et le déploiement en continu de vos applications.

1. Si vous configurez cette intégration d'outils lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Jenkins**.
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**. Ensuite, cliquez sur **Vue d'ensemble**.  

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **Jenkins**.

1. Entrez le nom que vous souhaitez afficher pour cette intégration d'outils sur la carte Jenkins de votre chaîne d'outils.
1. Saisissez l'URL du serveur Jenkins qui doit s'ouvrir lorsque vous cliquez sur la carte Jenkins à partir de votre chaîne d'outils.
1. Copiez l'ancrage Web de chaîne d'outils généré.
1. Dans votre serveur Jenkins, procédez comme suit :

 a. Installez l'[interface de ligne de commande Cloud Foundry  ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window}.

 b. Installez le plug-in IBM Cloud DevOps Cloud Foundry en saisissant l'une de ces commandes :

  * Mac OS : `cf install-plugin https://icd.ng.bluemix.net/icd_darwin_amd64`

  * Linux ou Docker : `cf install-plugin https://icd.ng.bluemix.net/icd_linux_amd64`

 c. Installez et configurez le plug-in IBM Cloud DevOps Jenkins pour DevOps Insights and Notifications. Pour plus d'informations, voir [Installation et configuration du plug-in](/docs/services/DevOpsInsights/insights_risk.html#integrate_jenkins){: new_window}.

 d. Dans chaque travail pour lequel vous souhaitez envoyer des notifications à votre chaîne d'outils, procédez comme suit :

  * Cochez la case **This project is parameterized**.

  * Ajoutez le paramètre de chaîne `ICD_WEBHOOK_URL`.

  * Collez l'ancrage Web de chaîne d'outils généré.
 ![URL d'ancrage Web](images/jenkins_webhook_url.png)

  * Ajoutez une action de post-génération pour IBM Cloud DevOps - Webhook Notification et cochez la case **Job Completed**.
 ![Action de post-génération](images/jenkins_postbuild_action.png)  

 e. Dans vos travaux de déploiement, procédez comme suit :

  * Ajoutez les paramètres de chaîne `ICD_WEBHOOK_URL`, `CF_API`, `CF_ORG`, `CF_SPACE` et `CF_APP`. Ces exemples montrent comment ajouter chacun des paramètres de chaîne.
 ![paramètre de chaîne d'URL d'ancrage Web](images/jenkins_set_webhook_url.png)
 ![paramètre de chaîne CFI API](images/jenkins_set_cfapi.png)
 ![paramètre de chaîne CFI ORG](images/jenkins_set_cforg.png)
 ![paramètre de chaîne CFI SPACE](images/jenkins_set_cfspace.png)
 ![paramètre de chaîne CFI APP](images/jenkins_set_cfapp.png)

  * Configurez vos liaisons pour l'interface de ligne de commande Cloud Foundry à l'aide de la variable de nom d'utilisateur `CF_CREDS_USR` et de la variable de mot de passe `CF_CREDS_PSW`.
 ![Liaisons de l'interface de ligne de commande Cloud Foundry](images/jenkins_config_bindings.png)  

  * Dans la zone **Build**, saisissez ces commandes pour vous connecter et utilisez le plug-in IBM Cloud DevOps Cloud Foundry pour envoyer les mappages déployables de l'application, avec traçabilité de validation Git, à votre chaîne d'outils :
 ![commandes Build](images/jenkins_build_commands.png)    

  * Dans la zone **Build**, saisissez la commande `cf icd --create-connection $ICD_WEBHOOK_URL $CF_APP` pour envoyer les mappages déployables d'application à la chaîne d'outils.    

 f. Enregistrez vos modifications et retournez à la page Configurer l'intégration pour l'intégration d'outils Jenkins.

1. Cliquez sur **Créer une intégration**.
1. A partir de votre chaîne d'outils, cliquez sur **Jenkins** pour afficher le serveur Jenkins.  

Pour plus d'informations, voir [Jenkins ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/deliver/tool_jenkins/){: new_window}.


## Configuration de JIRA
{: #jira}

JIRA est un outil qui assure le suivi des bogues et des problèmes liés à votre logiciel. L'intégration d'outils JIRA met à jour les problèmes de votre projet lorsque Jenkins ou {{site.data.keyword.deliverypipeline}} exécute un déploiement. Pour que l'intégration d'outils JIRA puisse assurer le suivi des problèmes, vous devez utiliser JIRA Smart Commits dans vos messages de validation. Pour en savoir plus sur JIRA Smart Commits, voir [Utilisation de Smart Commits ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://confluence.atlassian.com/fisheye/using-smart-commits-298976812.html){: new_window}.

Configurez JIRA pour planifier, suivre et distribuer un code de qualité :

1. Si vous configurez cette intégration d'outils lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **JIRA**.
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**. Ensuite, cliquez sur **Vue d'ensemble**.  

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **JIRA**.

1. Si vous disposez d'un projet JIRA et que vous voulez vous y connecter, cliquez sur **Existant** pour le type JIRA :

 a. Saisissez la clé de projet JIRA pour le projet JIRA. Vous la trouverez dans l'URL du projet JIRA.

 b. Saisissez l'URL d'API de base pour votre instance JIRA. Vous la trouverez dans l'en-tête de votre instance JIRA. Cliquez sur l'icône **Administration**, puis sur **Système**.

 c. Facultatif : Saisissez votre nom d'utilisateur JIRA. Votre nom d'utilisateur est requis uniquement si vous vous connectez à une instance JIRA privée ou si vous vous connectez à une instance publique et que vous souhaitez recevoir des informations de traçabilité. 

 d. Facultatif : Saisissez votre mot de passe JIRA. Votre mot de passe est requis uniquement si vous vous connectez à une instance JIRA privée ou si vous vous connectez à une instance publique et que vous souhaitez recevoir des informations de traçabilité. 

 Pour suivre le déploiement des modifications du code en créant des libellés et des commentaires pour les problèmes référencés, cochez la case **Suivi du déploiement
des modifications du code**. Assurez-vous que vous utilisez JIRA Smart Commit pour référencer les problèmes JIRA dans vos validations GitHub. Si vous ne sélectionnez pas cette option, l'intégration d'outils JIRA ignore les validations. 

1. Si vous souhaitez créer un projet JIRA, cliquez sur **Nouveau** pour le type JIRA :

 a. Saisissez une clé de projet JIRA à utiliser pour le nouveau projet. Cette clé est utilisée comme identificateur unique dans l'URL du projet.

 b. Saisissez un nom pour le projet JIRA.

 c. Saisissez l'URL d'API de base pour votre instance JIRA. Vous la trouverez dans l'en-tête de votre instance JIRA. Cliquez sur l'icône **Administration**, puis sur **Système**.

 d. Saisissez le nom d'utilisateur du chef de projet JIRA que vous voulez utiliser pour ce projet. La personne que vous spécifiez comme chef de projet JIRA doit disposer de droits de chef de projet dans JIRA.

 e. Saisissez le nom d'utilisateur de l'administrateur pour cette instance de JIRA.

 f. Saisissez le mot de passe de l'administrateur pour cette instance de JIRA.

 g. Pour suivre le déploiement des modifications du code en créant des libellés et des commentaires pour les problèmes référencés, cochez la case **Suivi du déploiement
des modifications du code**. Assurez-vous que vous utilisez JIRA Smart Commit pour référencer les problèmes JIRA dans vos validations GitHub. Si vous ne sélectionnez pas cette option, l'intégration d'outils JIRA ignore les validations. 

1. Cliquez sur **Créer une intégration**.
1. A partir de cette chaîne d'outils, cliquez sur **JIRA** pour afficher le tableau de bord du projet JIRA auquel vous êtes connecté.

Pour en savoir plus, voir [JIRA ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/code/tool_jira/){: new_window}.


## Configuration de Nexus
{: #nexus}

Configurez le gestionnaire de référentiels Nexus pour stocker les artefacts de génération dans votre référentiel Nexus :

1. Si vous configurez cette intégration d'outils lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Nexus**.
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**. Ensuite, cliquez sur **Vue d'ensemble**.  

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **Nexus**.

1. Saisissez un nom pour cette instance de l'intégration d'outils Nexus.
1. Saisissez l'URL du référentiel Nexus qui doit s'ouvrir lorsque vous cliquez sur la carte Nexus à partir de votre chaîne d'outils.
1. Sélectionnez le type de référentiel auquel vous souhaitez vous connecter.
1. Si vous avez sélectionné **Registre npm**, procédez comme suit :

 a. Saisissez l'adresse électronique associée à votre registre.

 b. Saisissez le jeton d'authentification associé à votre registre.

 c. Saisissez l'URL de votre référentiel d'édition Nexus, qui est votre registre privé sur le serveur Nexus.

 d. Saisissez l' URL du registre miroir ou public que vous utilisez pour combiner plusieurs registres npm publics et privés. Par exemple, cette URL peut être l'adresse du registre virtuel sur votre serveur Nexus, qui peut accéder à la fois à votre registre privé et à un cache du registre npm global.

1. Si vous avez sélectionné **Référentiel Maven**, procédez comme suit :

 a. Saisissez l'ID utilisateur associé à votre référentiel.

 b. Saisissez le mot de passe associé à votre référentiel.

 c. Saisissez l'URL de votre référentiel d'édition Nexus, qui est votre référentiel d'édition privé sur le serveur Nexus.

 d. Saisissez l'URL de votre référentiel d'image instantanée Nexus, qui est votre référentiel d'image instantanée privé sur le serveur Nexus.

 e. Saisissez l' URL du référentiel miroir ou public que vous utilisez pour combiner plusieurs référentiels Maven publics et privés. Par exemple, cette URL peut être l'adresse du référentiel virtuel sur votre serveur Nexus, qui peut accéder à la fois à vos référentiels privés et à un cache du référentiel Maven central.

1. Cliquez sur **Créer une intégration**.
1. A partir de votre chaîne d'outils, cliquez sur la carte du référentiel Nexus que vous souhaitez utiliser. Le site Web Nexus s'ouvre ; vous pouvez y afficher le contenu du référentiel.
1. Facultatif : Si vous utilisez une chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} Public et que vous voulez générez votre application à l'aide de Nexus avec npm, configurez votre pipeline pour ajouter un travail de génération npm. Pour des instructions de configuration du travail de génération, voir la section [Configuration d'un travail de génération npm Nexus sur votre pipeline](#config_nexus_npm).
1. Facultatif : Si vous utilisez une chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} Public et que vous voulez générer votre application à l'aide de Nexus avec Maven, configurez votre pipeline pour ajouter un travail de génération Maven. Pour des instructions de configuration du travail de génération, voir la section [Configuration d'un travail de génération Maven Nexus sur votre pipeline](#config_nexus_maven).

### Configuration d'un travail de génération npm Nexus sur votre pipeline
{: #config_nexus_npm}

Avant de configurer un travail de génération npm sur votre pipeline, vous devez disposer d'un pipeline opérationnel qui peut utiliser votre référentiel SCM de génération en entrée et vous devez configurer Nexus pour votre chaîne d'outils. Pour les instructions de configuration de Nexus, voir la section [Nexus](#nexus). 

Configurez {{site.data.keyword.deliverypipeline}} pour ajouter un travail de génération npm :

1. Créez une étape et définissez l'entrée sur le référentiel SCM approprié.
1. Dans l'étape, ajoutez un travail de génération.
1. Configurez le travail de génération :
  ![travail de génération npm](images/nexus_npm_job.png)

  a. Pour le type de générateur, sélectionnez **NPM Build**.

  b. Si vous avez configuré plusieurs instances de l'intégration d'outils Nexus, saisissez le nom de l'intégration d'outils Nexus pour laquelle vous souhaitez configurer le travail de génération npm. 

  c. Pour le type d'intégration d'outils, sélectionnez **Nexus**.

  d. Pour la commande de génération, saisissez les commandes permettant de générer votre module npm ou de le publier dans votre registre. Cet exemple montre les commandes de génération ou de publication du module.
     ```
     npm install
     # ou
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Conseil** : Vous pouvez trouver l'URL et les données d'identification de l'utilisateur dont vous vous êtes servi pour vous connecter à votre registre dans les paramètres de configuration pour l'intégration d'outils Nexus.

  e. Si votre travail de génération est publié dans le registre Nexus et que le format de votre version de module de noeud est `x.y.z-SNAPSHOT.w`, cochez la case **Increment snapshot module version**. Le travail de génération met automatiquement à jour la version du module avant qu'il ne soit publié dans le registre Nexus. Le travail de génération sélectionne la version la plus élevée du module à partir du registre npm et du fichier local `package.json`, et incrémente la version du module à l'aide de semver. Le travail de génération ne répercute pas les modifications dans le référentiel SCM. 

1. Cliquez sur **SAUVEGARDER**. Lors de l'exécution de votre pipeline, ce travail de génération utilise les informations de configuration provenant de l'intégration d'outils Nexus pour la connexion à votre registre npm. 

### Configuration d'un travail de génération Maven Nexus sur votre pipeline
{: #config_nexus_maven}

Avant de configurer un travail de génération Maven sur votre pipeline, vous devez disposer d'un pipeline opérationnel qui peut utiliser votre référentiel SCM de génération en entrée et vous devez configurer Nexus pour votre chaîne d'outils. Pour les instructions de configuration de Nexus, voir la section [Nexus](#nexus). 

Configurez {{site.data.keyword.deliverypipeline}} pour ajouter un travail de génération Maven :

1. Créez une étape et définissez l'entrée sur le référentiel SCM approprié.
1. Dans l'étape, ajoutez un travail de génération.
1. Configurez le travail de génération :
  ![travail de génération Maven](images/nexus_maven_job.png)

  a. Pour le type de générateur, sélectionnez **Maven Build**.

  b. Si vous avez configuré plusieurs instances de l'intégration d'outils Nexus, saisissez le nom de l'intégration d'outils Nexus pour laquelle vous souhaitez configurer le travail de génération Maven. 

  c. Pour le type d'intégration d'outils, sélectionnez **Nexus**.

  d. Pour la commande de génération, saisissez les commandes permettant de générer votre module Maven ou de le publier dans votre registre d'image instantanée. Cet exemple montre les commandes de génération ou de publication du module.
     ```
     mvn -B clean package
     # ou
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Conseil** : Vous pouvez trouver l'URL et les données d'identification de l'utilisateur dont vous vous êtes servi pour vous connecter à votre registre dans les paramètres de configuration pour l'intégration d'outils Nexus.

1. Cliquez sur **SAUVEGARDER**. Lors de l'exécution de votre pipeline, ce travail de génération utilise les informations de configuration provenant de l'intégration d'outils Nexus pour la connexion à votre référentiel Maven. 

Pour plus d'informations, voir [Nexus ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/code/tool_nexus/){: new_window}.


## Configuration d'un outil personnalisé (autre outil)
{: #othertool}

Si votre équipe utilise un outil qui n'est pas inclus dans la liste des intégrations de chaînes d'outils, vous pouvez intégrer un
outil personnalisé.

Configurez un outil personnalisé qui puisse fonctionner avec
les autres outils de votre chaîne d'outils et qui soit disponible
pour votre équipe :

1. Si vous configurez cette intégration d'outils lorsque vous
créez la chaîne d'outils, à la section Intégrations configurables,
cliquez sur **Autre outil**.
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **Autre outil**.

1. Saisissez le nom de l'outil.
1. Sélectionnez la phase de cycle de vie qui est la plus étroitement associée à l'outil. Cette sélection détermine la catégorie sous laquelle votre outil est répertorié sur la page Vue d'ensemble. 
1. Ajoutez une URL d'icône. L'icône s'affiche sur la carte de votre intégration d'outils. 
1. Ajoutez une URL de documentation.
1. Indiquez un nom d'instance d'outil. Par exemple : Outil de
mon équipe.
1. Ajoutez une URL d'instance de l'outil. Cette URL s'ouvre chaque fois que vous cliquez sur la carte d'intégration d'outils. 
1. Ajoutez une description de votre outil.
1. (Avancé) Ajoutez des propriétés supplémentaires si besoin. Par exemple, indiquez les informations ou les attributs qui sont
requis pour l'intégration de votre outil aux autres outils de la chaîne d'outils.  
1. Cliquez sur **Créer une intégration**.

Pour en savoir plus, voir [Présentation de l'intégration d'outils personnalisée pour les chaînes d'outils {{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2016/10/custom-tool-integration-with-bluemix-toolchains/){: new_window}.


## Configuration de PagerDuty
{: #pagerduty}

PagerDuty intègre dans une vue unique les données provenant de plusieurs systèmes de surveillance. Quand un problème survient, PagerDuty s'assure que le membre d'équipe le plus à même de le résoudre reçoit une notification. Si le membre d'équipe ne résout pas le problème, il est possible de mettre en place des escalades afin de router le problème vers des ingénieurs de second niveau ou des gestionnaires des opérations.

Configurez PagerDuty pour l'envoi de notifications en cas d'échec d'étape de pipeline afin de pouvoir résoudre les problèmes plus rapidement et de réduire le temps d'indisponibilité.

1. Si vous configurez cette intégration d'outils lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **PagerDuty**.
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **PagerDuty**.

1. Entrez la clé d'accès d'API pour votre compte PagerDuty. Si vous ne disposez pas d'un compte PagerDuty, [inscrivez-vous pour en obtenir un ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://signup.pagerduty.com/accounts/new){: new_window}. Pour des instructions de recherche de la clé, voir [Génération d'une clé d'API ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://support.pagerduty.com/hc/en-us/articles/202829310-Generating-an-API-Key){: new_window}.
1. Entrez le nom de votre service PagerDuty.
1. Entrez l'adresse électronique du contact PagerDuty principal.
1. Entrez le numéro de téléphone du contact PagerDuty principal.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur **PagerDuty** pour accéder au site pagerduty.com. Vous pouvez afficher les événements associés au service PagerDuty spécifié lors de la configuration de cette intégration d'outils pour votre chaîne d'outils.

Pour en savoir plus, voir [PagerDuty ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configuration de Sauce Labs
{: #saucelabs}

Sauce Labs exécute des tests unitaires fonctionnels. Quand une suite de tests Sauce Labs est configurée comme travail de test dans {{site.data.keyword.deliverypipeline}}, cette suite de tests peut exécuter des tests en fonction de votre application Web ou mobile dans le cadre de votre processus de distribution continue. Ces tests peuvent fournir un contrôle de flux de valeur pour vos projets, agissant comme des barrières pour empêcher le déploiement de code incorrect.

 **Remarque** : Cette intégration d'outils est disponible uniquement sur {{site.data.keyword.Bluemix_notm}} Public. 

Configurez Sauce Labs pour l'exécution de tests fonctionnels automatisés sur plusieurs systèmes d'exploitation et navigateurs afin de pouvoir émuler la façon dont un utilisateur peut utiliser un site Web ou une application :

1. Si vous configurez cette intégration d'outils lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Sauce Labs**.
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis la page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **Sauce Labs**.

1. Entrez le nom d'utilisateur associé à votre compte Sauce Labs. Vous pouvez [trouver votre nom d'utilisateur dans le message d'accueil, en haut de la page de votre compte Sauce Labs ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://saucelabs.com/account){: new_window}.
1. Entrez la clé d'accès de votre compte Sauce Labs. Vous pouvez [trouver la clé sur la page de votre compte Sauce Labs ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://saucelabs.com/account){: new_window}.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur **Sauce Labs** pour accéder à saucelabs.com et afficher l'activité de test pour la chaîne d'outils.

 **Conseil **: Si vous avez ajouté un travail de test Sauce Labs à {{site.data.keyword.deliverypipeline}}, vous pouvez sélectionner l'instance de service.

Pour en savoir plus, voir [Sauce Labs ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configuration de Slack
{: #slack}

**Important **: Les notifications postées sur des canaux Slack publics sont visibles de tout membre de l'équipe. N'oubliez pas que vous êtes responsable du contenu de vos articles.

Slack est un système de messagerie et de notification en temps réel, basé sur le cloud. Slack fournit un système de discussion permanente, alternative plus interactive au courrier électronique pour la collaboration des équipes. Vous pouvez communiquer avec votre équipe sur un canal dédié ou sur un ensemble de canaux directement liés à votre travail. Vous pouvez également partager des fichiers et des images via ces canaux, ou dans des messages directs entre deux personnes ou plus. Les communications dans les messages directs ou sur les canaux sont conservées pour que vous puissiez y faire des recherches.

Configurez Slack pour la réception de notifications concernant votre chaîne d'outils depuis les intégrations d'outils, par exemple les activités de test et de déploiement :

1. Si vous configurez cette intégration d'outils lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Slack**.
1. Si vous disposez d'une chaîne d'outils et lui ajoutez cette intégration d'outils, dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir sa page Vue d'ensemble. Vous pouvez également, depuis votre page de présentation de l'application, sur la carte Continuous delivery, cliquer sur **Afficher la chaîne d'outils**, puis sur **Présentation**. 

 a. Cliquez sur **Ajouter un outil**.

 b. A la section Intégrations d'outils, cliquez sur **Slack**.

1. Entrez l'URL de webhook Slack, qui est générée par Slack en tant que webhook entrant. Vous avez besoin d'une URL d'ancrage Web Slack pour un canal Slack afin de recevoir des notifications concernant votre chaîne d'outils depuis les intégrations d'outils. Pour des instructions sur la création ou la recherche d'ancrage Web, voir [Ancrages Web entrants![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://api.slack.com/incoming-webhooks){: new_window}.

 **Conseil** : Si vous utilisez une clé d'API pour votre canal Slack afin de recevoir des notifications sur votre chaîne d'outils à partir des intégrations d'outils, vous devez mettre à jour votre configuration pour utiliser un ancrage Web à la place. 

1. Entrez le nom du canal Slack sur lequel vous souhaitez recevoir les notifications. Le canal doit déjà exister et être actif dans votre équipe Slack. 
1. Saisissez le nom d'hôte d'URL pour votre équipe Slack, qui est le mot ou l'expression avant `.slack.com` dans l'URL de votre équipe. Par exemple, si l'URL de votre équipe est `https://team.slack.com`, le nom d'hôte est `team`.
1. Cliquez sur **Créer une intégration**.

 **Conseil** : Si l'équipe et le canal Slack que vous avez spécifiés ne sont pas accessibles, l'erreur `Echec de la configuration` s'affiche sur la carte Slack. Survolez le message `Echec de la configuration` et cliquez sur **Reconfigurer**. Assurez-vous que vous utilisez des paramètres de configuration valides pour l'URL d'ancrage Web Slack, le canal Slack et le nom d'hôte d'URL de votre équipe Slack. Mettez à jour les paramètres si nécessaire et cliquez sur **Sauvegarder l'intégration**.

1. Cliquez sur **Slack**. Vous pouvez afficher toutes les activités de votre chaîne d'outils dans le canal Slack configuré.

Pour en savoir plus, voir [Slack ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
