---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuration d'intégrations d'outils
{: #integrations}

Dernière mise à jour : 18 octobre 2016
{: .last-updated}

Vous pouvez configurer des intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations lors de la création d'une chaîne d'outils, ou bien vous pouvez ajouter et configurer des intégrations d'outils afin de personnaliser une chaîne d'outils existante.  
{:shortdesc}

**Important** : Sur {{site.data.keyword.Bluemix_notm}} public, les chaînes d'outils sont disponibles uniquement dans la région sud des Etats-Unis.

Les intégrations d'outils disponibles pour ajouter et configurer votre chaîne d'outils varient selon que vous utilisez des chaînes d'outils sur {{site.data.keyword.Bluemix_notm}} public ou {{site.data.keyword.Bluemix_notm}} dédié. Si
vous utilisez des chaînes d'outils sur
{{site.data.keyword.Bluemix_notm}} Dedicated, les
Intégrations d'outils qui sont disponibles dépendent de la manière
dont {{site.data.keyword.jazzhub_title}} a été configuré dans
votre environnement spécifique.

*Tableau 1. Intégrations d'outils disponibles pour les chaînes d'outils sur {{site.data.keyword.Bluemix_notm}} public et dédié*

|Intégration d'outil |Disponible sur {{site.data.keyword.Bluemix_notm}} public	|
Disponible sur {{site.data.keyword.Bluemix_notm}} Dedicated
(dépendant de l'environnement)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|Oui	   	|Oui  		|
|{{site.data.keyword.DRA_short}} 		|Oui		|Non			|
|Eclipse Orion {{site.data.keyword.webide}}		|Oui		|Oui			|
|GitHub		|Oui		|Oui		|
|Dedicated GitHub Enterprise			|Non		|Oui		|
|Autre outil			|Oui		|Oui		|
|PagerDuty			|Oui		|Oui		|
|Sauce Labs		|Oui		|Non		|
|Slack			|Oui		|Oui		|

**Conseil** : Si vous souhaitez débuter le développement par votre code source sur {{site.data.keyword.Bluemix_notm}} public, configurez les intégrations d'outils GitHub et GitHub Issues avant de configurer {{site.data.keyword.deliverypipeline}}. 
Si vous souhaitez débuter le développement par votre code source sur
{{site.data.keyword.Bluemix_notm}} dédié, configurez
l'intégration d'outil {{site.data.keyword.ghe_short}} ou
l'intégration d'outil GitHub avant
de configurer {{site.data.keyword.deliverypipeline}}. 


## Configuration du pipeline de distribution
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} automatise le déploiement de vos projets via des séquences d'étapes qui extraient des travaux en entrée et d'exécution tels que des générations, des tests et des déploiements. 

Configurez {{site.data.keyword.deliverypipeline}} afin d'automatiser la génération, le test et le déploiement en continu de vos applications. 

1. Si vous configurez cette intégration d'outil lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Delivery Pipeline**. En fonction du modèle utilisé, des zones différentes peuvent être disponibles. Passez en revue les valeurs de zone par défaut et, si nécessaire, modifiez ces paramètres.
1. Si vous disposez d'une chaîne d'outils sur
{{site.data.keyword.Bluemix_notm}} public et si vous y
ajoutez cette intégration d'outil, depuis le tableau de bord DevOps,
page **Chaînes d'outils**, cliquez sur la chaîne
d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis votre page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. Si vous utilisez une chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} dédié, depuis le tableau de bord, onglet **DEVOPS**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, dans le coin supérieur droit de la page de présentation de l'application, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Delivery Pipeline**.
1. Indiquez un nom pour votre nouveau pipeline.
1. Si vous prévoyez d'utiliser votre pipeline pour déployer une interface utilisateur, sélectionnez la case **Application visualisable**. Toutes les applications créées par votre pipeline sont affichées dans la liste **AFFICHER L'APPLICATION** de la page Intégrations d'outils de la chaîne d'outils.
1. Cliquez sur **Créer une intégration** pour ajouter {{site.data.keyword.deliverypipeline}} à votre chaîne d'outils.
1. Cliquez sur la vignette de {{site.data.keyword.deliverypipeline}} pour afficher le pipeline et le configurer. Pour en savoir plus sur les notions de base et la configuration d'un pipeline, voir [Building and deploying from pipelines (Lien s'ouvrant dans une nouvelle fenêtre)](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Conseil **: Si vous souhaitez déclencher le pipeline lorsque vous envoyez des modifications à votre référentiel GitHub ou {{site.data.keyword.ghe_short}} (repo), vous devez configurer GitHub ou {{site.data.keyword.ghe_short}} pour votre chaîne d'outils avant de définir les étapes du pipeline. Ces étapes requièrent les URL de vos référentiels. Chaque étape de pipeline peut faire référence à un seul des référentiels GitHub ou {{site.data.keyword.ghe_short}} associé à votre chaîne d'outils. Pour des instructions de configuration de GitHub, voir la section [GitHub](#github). Pour des instructions sur la configuration de Dedicated GitHub Enterprise, voir [Getting started with {{site.data.keyword.ghe_long}} (Lien s'ouvrant dans une nouvelle fenêtre)](../services/ghededicated/index.html){: new_window}.
  
1. Facultatif : Si vous utilisez une chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} public et souhaitez que Sauce Labs exécute des tests sur votre application, configurez {{site.data.keyword.deliverypipeline}} pour ajouter un travail de test Sauce Labs. Pour des instructions de configuration du travail de test, voir la section [Configuration d'un travail de test Sauce Labs sur votre pipeline](#config_saucelabs).

### Configuration d'un travail de test Sauce Labs sur votre pipeline
{: #config_saucelabs}

Avant de configurer un travail de test Sauce Labs sur votre pipeline, vous avez besoin d'un pipeline opérationnel qui comporte des étapes pour la génération et le déploiement de votre application, et vous devez configurer Sauce Labs pour votre chaîne d'outils. Pour des instructions de configuration de Sauce Labs, voir la section [Configuration de Sauce Labs](#saucelabs).

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

Pour en savoir plus, voir [Delivery Pipeline (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.


## Ajout de {{site.data.keyword.DRA_short}}
{: #dra}

{{site.data.keyword.DRA_full}} collecte et analyse les résultats provenant de tests unitaires, de tests fonctionnels et d'outils de couverture de code afin de déterminer si votre code satisfait les critères prédéfinis à certains stades de votre processus de déploiement. Si votre code ne satisfait pas ou dépasse les critères, le déploiement est interrompu afin de prévenir tout risque. Vous pouvez utiliser {{site.data.keyword.DRA_short}} comme filet de sécurité pour votre environnement de distribution continue ou comme moyen d'implémenter et d'améliorer les normes qualité. 

 **Remarque** : Cette intégration d'outil est préconfigurée. Elle ne requiert aucun paramètre de configuration et vous ne pouvez pas la reconfigurer.
 
Ajoutez {{site.data.keyword.DRA_short}} afin de gérer et d'améliorer la qualité de votre code dans {{site.data.keyword.Bluemix_notm}} en surveillant vos déploiements afin d'identifier les risques avant la publication.

1. Si vous disposez d'une chaîne d'outils et que vous y
ajoutez cette intégration d'outil, depuis le tableau de bord DevOps,
page **Chaînes d'outils**, cliquez sur la chaîne
d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Deployment Risk Analytics**. 
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette de {{site.data.keyword.DRA_short}}, puis complétez les étapes de mise en route : créez des critères, connectez-les au pipeline, puis exécutez ce dernier. Pour plus d'informations, voir [{{site.data.keyword.DRA_short}} (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.


## Ajout d'Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} est un environnement de développement Web intégré dans lequel vous pouvez créer, éditer, exécuter, déboguer et terminer des tâches de contrôle des sources. Vous pouvez facilement passer de l'édition à l'exécution, à la soumission, puis au développement. 

 **Remarque** : Cette intégration d'outil est préconfigurée. Elle ne requiert aucun paramètre de configuration et vous ne pouvez pas la reconfigurer.
 
Pour effectuer des tâches de contrôle des sources, ajoutez l'intégration d'outil Eclipse Orion {{site.data.keyword.webide}} :

1. Si vous disposez d'une chaîne d'outils sur
{{site.data.keyword.Bluemix_notm}} public et si vous y
ajoutez cette intégration d'outil, depuis le tableau de bord DevOps,
page **Chaînes d'outils**, cliquez sur la chaîne
d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. Si vous utilisez une chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} dédié, depuis le tableau de bord, onglet **DEVOPS**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, dans le coin supérieur droit de la page de présentation de l'application, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**.
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Eclipse Orion Web IDE**. 
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette de la nouvelle intégration Eclipse Orion {{site.data.keyword.webide}}. Votre espace de travail est prérempli avec vos référentiels GitHub ou {{site.data.keyword.ghe_short}}. Les référentiels associés à votre chaîne d'outils en cours sont mis en évidence.

Pour en savoir plus, voir [Edition de code avec Eclipse Orion {{site.data.keyword.webide}} (Lien s'ouvrant dans une nouvelle fenêtre)](../toolchains/web_ide.html){: new_window}.


## Configuration de GitHub
{: #github}

GitHub est un service d'hébergement Web pour les référentiels Git. Vous pouvez avoir des copies en local et à distance de vos référentiels, ce qui simplifie la collaboration. 

GitHub Issues est un outil de suivi qui conserve votre travail et vos plans à un seul et même emplacement. Il est intégré à votre référentiel de développement pour vous permettre de vous concentrer sur les tâches importantes.

Configurez GitHub pour gérer votre code source dans le cloud :

1. Si vous configurez cette intégration d'outil lors de la création de la chaîne d'outils, procédez comme suit :

 a. A la section Intégrations configurables, cliquez sur **GitHub**. 
Si vous créez la chaîne d'outils sur
{{site.data.keyword.Bluemix_notm}} public et si vous n'avez pas
autorisé
{{site.data.keyword.Bluemix_notm}} à accéder à GitHub,
cliquez sur **Autorisation** pour accéder au site
Web GitHub. Si vous n'avez pas de session GitHub active, vous êtes invité à vous connecter. Cliquez sur **Authorize Application** pour autoriser {{site.data.keyword.Bluemix_notm}} à accéder à votre compte GitHub. Si vous disposez d'une session GitHub active mais n'avez pas saisi votre mot de passe récemment, vous êtes invité à entrer votre mot de passe GitHub pour confirmation.
 
 b. Passez en revue les emplacements de référentiel cible par défaut pour les référentiels GitHub. Ces référentiels sont clonés à partir des référentiels exemple. Si nécessaire, modifiez les noms des référentiels cible.
 ![Emplacements de référentiel cible par défaut](images/toolchain_github_config.png)
   
1. Si vous disposez d'une chaîne d'outils et que vous y
ajoutez cette intégration d'outil, depuis le tableau de bord DevOps,
page **Chaînes d'outils**, cliquez sur la chaîne
d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **GitHub**.
1. Si vous disposez d'un référentiel GitHub et souhaitez l'utiliser, entrez son URL. Pour le type de référentiel, cliquez sur **Lier**.
1. Si vous souhaitez utiliser un nouveau référentiel GitHub, indiquez un nom pour le référentiel GitHub, entrez l'URL du référentiel que vous clonez ou déviez, puis sélectionnez le type de référentiel : 

 a. Pour créer un référentiel vide, cliquez sur **Nouveau**. 
 
 b. Pour créer une copie d'un référentiel GitHub, cliquez sur **Cloner**.
 
 c. Pour dévier un référentiel GitHub afin de pouvoir participer aux modifications via des demandes d'extraction, cliquez sur **Dévier**.
 
1. Si vous souhaitez utiliser GitHub Issues pour le suivi des problèmes, sélectionnez la case **Activer GitHub Issues**.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette du référentiel GitHub que vous souhaitez utiliser. Le site Web GitHub s'ouvre ; vous pouvez y afficher le contenu du référentiel.
 
  **Conseil **: Vous pouvez utiliser les outils intégrés de gestion de code source d'Eclipse Orion {{site.data.keyword.webide}} pour éditer le référentiel GitHub et déployer une application depuis votre poste de travail.

1. Si vous avez activé GitHub Issues, cliquez sur la vignette GitHub Issues pour l'ouvrir.

Pour plus d'informations, voir [GitHub (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} et [GitHub Issues (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configuration de Dedicated GitHub Enterprise
{: #configghe}

{{site.data.keyword.ghe_long}} est un service d'hébergement Web sur site pour les référentiels Git. Dedicated GitHub Enterprise est destiné aux clients de {{site.data.keyword.Bluemix_notm}} dédié uniquement. GitHub Issues est un outil de suivi qui conserve votre travail et vos plans à un seul et même emplacement. Il est intégré à votre référentiel de développement pour vous permettre de vous concentrer sur les tâches importantes. Pour plus d'informations sur Dedicated GitHub Enterprise et GitHub Issues, voir [Utilisation de Dedicated GitHub Enterprise (Lien s'ouvrant dans une nouvelle fenêtre)](../services/ghededicated/index.html){: new_window} et [GitHub Issues (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Vous pouvez configurer {{site.data.keyword.ghe_short}} en tan qu'intégration d'outil dans votre chaîne d'outils afin de pouvoir gérer le code source depuis l'instance [{{site.data.keyword.Bluemix_notm}} dédié (Lien s'ouvrant dans une nouvelle fenêtre)](../dedicated/index.html#dedicated){: new_window} de votre société.

1. Si vous configurez cette intégration d'outil lors de la création de la chaîne d'outils, procédez comme suit :

 a. Avant de vous connecter à Dedicated GitHub Enterprise pour la première fois, demandez à l'administrateur régional de votre société d'ajouter votre ID utilisateur à votre instance {{site.data.keyword.Bluemix_notm}} dédié à partir du registre d'utilisateurs de la société, via LDAP. Pour des informations sur la configuration de votre compte {{site.data.keyword.ghe_short}}, voir [Utilisation de Dedicated GitHub Enterprise (Lien s'ouvrant dans une nouvelle fenêtre)](../services/ghededicated/index.html){: new_window}.
 
 b. A la section Intégrations configurables, cliquez sur **{{site.data.keyword.ghe_short}}**.    
 
 c. Vérifiez le nom par défaut pour le nouveau référentiel {{site.data.keyword.ghe_short}}. Si nécessaire, changez le nom du nouveau référentiel. L'image suivante montre un exemple de référentiel cloné à partir d'un référentiel exemple. Vous pouvez utiliser un référentiel existant ou un nouveau référentiel. Pour utiliser un nouveau référentiel, vous pouvez créer un référentiel vide, cloner un référentiel ou dévier un référentiel. 
 ![Emplacements de référentiel par défaut](images/toolchain_ghe_config.png)
   
1. Si vous disposez d'une chaîne d'outils sur
{{site.data.keyword.Bluemix_notm}} public et si vous y
ajoutez cette intégration d'outil, depuis le tableau de bord DevOps,
page **Chaînes d'outils**, cliquez sur la chaîne
d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis votre page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. Si vous utilisez une chaîne d'outils sur {{site.data.keyword.Bluemix_notm}} dédié, depuis le tableau de bord, onglet **DEVOPS**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, dans le coin supérieur droit de la page de présentation de l'application, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**.
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **{{site.data.keyword.ghe_short}}**.
1. Si vous disposez d'un référentiel {{site.data.keyword.ghe_short}} que vous souhaitez utiliser, entrez l'URL du référentiel. Pour le type de référentiel, cliquez sur **Existant**.
1. Si vous souhaitez utiliser un nouveau référentiel {{site.data.keyword.ghe_short}}, indiquez un nom pour le référentiel, entrez l'URL du référentiel que vous clonez ou déviez, puis sélectionnez le type de référentiel : 

 a. Pour créer un référentiel vide, cliquez sur **Nouveau**. 
 
 b. Pour créer une copie d'un référentiel, cliquez sur **Cloner**.
 
 c. Pour dévier un référentiel afin de pouvoir participer aux modifications via des demandes d'extraction, cliquez sur **Dévier**.
 
1. Pour utiliser GitHub Issues pour le suivi des problèmes, sélectionnez la case **Activer GitHub Issues**.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette du référentiel {{site.data.keyword.ghe_short}} à utiliser. L'instance de [{{site.data.keyword.Bluemix_notm}} dédié (Lien s'ouvrant dans une nouvelle fenêtre)](../dedicated/index.html#dedicated){: new_window} de votre société s'ouvre, vous permettant de consulter le contenu du référentiel.
 
  **Conseil **: Vous pouvez utiliser les outils intégrés de gestion de code source d'Eclipse Orion {{site.data.keyword.webide}} pour éditer le référentiel {{site.data.keyword.ghe_short}} et déployer une application depuis votre poste de travail.

1. Si vous avez activé GitHub Issues, cliquez sur la vignette GitHub Issues.

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## Configuration d'un outil personnalisé (autre outil)
{: #othertool}

Si votre équipe utilise un outil qui n'est pas inclus dans la
liste des intégrations de chaîne d'outils, vous pouvez intégrer un
outil personnalisé. 

Configurez un outil personnalisé qui puisse fonctionner avec
les autres outils de votre chaîne d'outils et qui soit disponible
pour votre équipe :
1. Si vous configurez cette intégration d'outil lorsque vous
créez la chaîne d'outils, à la section Intégrations configurables,
cliquez sur **Autre outil**.

1. Si vous disposez d'une chaîne d'outils et que vous y
ajoutez cette intégration d'outil, depuis le tableau de bord DevOps,
page **Chaînes d'outils**, cliquez sur la chaîne
d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**.
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur
**Autre outil**.
1. Saisissez le nom de l'outil.
1. Sélectionnez la phase de cycle de vie qui est le plus
étroitement associée à l'outil. Ce choix détermine la catégorie sous
laquelle est répertorié votre outil dans la page Toolchain Integration.
1. Ajoutez une URL d'icône. Cette icône figurera sur la carte
d'intégration de votre outil.
1. Ajoutez une URL de documentation.
1. Indiquez un nom d'instance d'outil. Par exemple : Outil de
mon équipe.
1. Ajoutez une URL d'instance de l'outil. Un clic sur
la carte de l'outil d'intégration permet d'accéder à l'URL que vous
indiquez pour l'instance d'outil.
1. Ajoutez une description de votre outil. 
1. (Avancé) Ajoutez des propriétés supplémentaires si besoin. Par
exemple, indiquez les informations ou les attributs qui sont
requis pour l'intégration de votre outil aux autres outils de votre
chaîne d'outils.  
1. Cliquez sur **Créer une intégration**.

## Configuration de PagerDuty
{: #pagerduty}

PagerDuty intègre dans une vue unique les données provenant de plusieurs systèmes de surveillance. Quand un problème survient, PagerDuty s'assure que le membre d'équipe le plus à même de le résoudre reçoit une notification. Si le membre d'équipe ne résout pas le problème, il est possible de mettre en place des escalades afin de router le problème vers des ingénieurs de second niveau ou des gestionnaires des opérations.

Configurez PagerDuty pour l'envoi de notifications en cas d'échec d'étape de pipeline afin de pouvoir résoudre les problèmes plus rapidement et de réduire le temps d'indisponibilité.

1. Si vous configurez cette intégration d'outil lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **PagerDuty**.
1. Si vous disposez d'une chaîne d'outils et que vous y
ajoutez cette intégration d'outil, depuis le tableau de bord DevOps,
page **Chaînes d'outils**, cliquez sur la chaîne
d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **PagerDuty**.
1. Entrez le nom du site PagerDuty associé à votre compte PagerDuty. Si vous ne disposez pas d'un compte PagerDuty, [inscrivez-vous (Lien s'ouvrant dans une nouvelle fenêtre)](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Entrez la clé d'accès d'API pour votre compte PagerDuty. Pour des instructions de recherche de la clé, voir [API Authentication (Lien s'ouvrant dans une nouvelle fenêtre)](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Entrez le nom de votre service PagerDuty.
1. Entrez l'adresse électronique du contact PagerDuty principal.
1. Entrez le numéro de téléphone du contact PagerDuty principal.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette PagerDuty pour accéder à pagerduty.com. Vous pouvez afficher les événements associés au service PagerDuty spécifié lors de la configuration de cette intégration d'outil pour votre chaîne d'outils. 

Pour en savoir plus, voir [PagerDuty (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configuration de Sauce Labs
{: #saucelabs}

Sauce Labs exécute des tests unitaires fonctionnels. Quand une suite de tests Sauce Labs est configurée comme travail de test dans {{site.data.keyword.deliverypipeline}}, cette suite de tests peut exécuter des tests en fonction de votre application Web ou mobile dans le cadre de votre processus de distribution continue. Ces tests peuvent fournir un contrôle de flux de valeur pour vos projets, agissant comme des barrières pour empêcher le déploiement de code incorrect.

Configurez Sauce Labs pour l'exécution de tests fonctionnels automatisés sur plusieurs systèmes d'exploitation et navigateurs afin de pouvoir émuler la façon dont un utilisateur peut utiliser un site Web ou une application :

1. Si vous configurez cette intégration d'outil lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Sauce Labs**.
1. Si vous disposez d'une chaîne d'outils et que vous y
ajoutez cette intégration d'outil, depuis le tableau de bord DevOps,
page **Chaînes d'outils**, cliquez sur la chaîne
d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Sauce Labs**.
1. Entrez le nom d'utilisateur associé à votre compte Sauce Labs. Vous pouvez [trouver votre nom d'utilisateur dans le message d’accueil, en haut de la page de votre compte Sauce Labs (Lien s'ouvrant dans une nouvelle fenêtre)](https://saucelabs.com/account){: new_window}.
1. Entrez la clé d'accès de votre compte Sauce Labs. Vous pouvez [trouver la clé sur la page de votre compte Sauce Labs (Lien s'ouvrant dans une nouvelle fenêtre)](https://saucelabs.com/account){: new_window}.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette Sauce Labs pour accéder à saucelabs.com et afficher l'activité de test pour la chaîne d'outils.

 **Conseil **: Si vous avez ajouté un travail de test Sauce Labs à {{site.data.keyword.deliverypipeline}}, vous pouvez sélectionner l'instance de service.

Pour en savoir plus, voir [Sauce Labs (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configuration de Slack
{: #slack}

**Important **: Les notifications postées sur des canaux Slack publics sont visibles de tout membre de l'équipe. N'oubliez pas que vous êtes responsable du contenu de vos articles.

Slack est un système de messagerie et de notification en temps réel, basé sur le cloud. Slack fournit un système de discussion permanente, alternative plus interactive au courrier électronique pour la collaboration des équipes. Vous pouvez communiquer avec votre équipe sur un canal dédié ou sur un ensemble de canaux directement liés à votre travail. Vous pouvez également partager des fichiers et des images via ces canaux, ou dans des messages directs entre deux personnes ou plus. Les communications dans les messages directs ou sur les canaux sont conservées pour que vous puissiez y faire des recherches. 

Configurez Slack pour la réception de notifications concernant votre chaîne d'outils depuis les intégrations d'outils, par exemple les activités de test et de déploiement :

1. Si vous configurez cette intégration d'outil lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Slack**.
1. Si vous disposez d'une chaîne d'outils et que vous y
ajoutez cette intégration d'outil, depuis le tableau de bord DevOps,
page **Chaînes d'outils**, cliquez sur la chaîne
d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**.
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Slack**.
1. Entrez le jeton d'authentification d'API pour votre compte Slack. Vous devez utiliser un jeton d'accès complet généré pour l'authentification avec Slack. Pour des instructions de recherche du jeton, voir [Slack authentication (Lien s'ouvrant dans une nouvelle fenêtre)](https://api.slack.com/web#authentication){: new_window}.
1. Entrez le nom du canal Slack sur lequel vous souhaitez recevoir les notifications. Si le canal spécifié n'existe pas, il est créé. Si le canal a été archivé, il est réactivé.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette Slack. Vous pouvez afficher toutes les activités de votre chaîne d'outils dans le canal Slack configuré.

Pour en savoir plus, voir [Slack (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.








