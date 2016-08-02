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

*Dernière mise à jour : 17 juin 2016*
{: .last-updated}

Vous pouvez configurer des intégrations d'outils prenant en charge des tâches de développement, de déploiement et d'opérations lors de la création d'une chaîne d'outils, ou bien vous pouvez ajouter et configurer des intégrations d'outils afin de personnaliser une chaîne d'outils existante.  
{:shortdesc}

**Important **: Cette fonction est expérimentale. Les chaînes d'outils peuvent être instables et faire l'objet de modifications entraînant leur incompatibilité avec des versions antérieures. Elles ne sont pas recommandées pour une utilisation dans des environnements de production. Pour utiliser des chaînes d'outils, vous devez adresser une [demande d'accès](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} à usage unique.  Les chaînes d'outils sont disponibles uniquement dans la région sud des Etats-Unis. 

**Conseil **: Si vous souhaiter débuter le développement par votre code source, assurez-vous de configurer les intégrations des outils GitHub et GitHub Issues avant de configurer {{site.data.keyword.deliverypipeline}}.

## Configuration du pipeline de distribution
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} automatise le déploiement de vos projets via des séquences d'étapes qui extraient des travaux en entrée et d'exécution tels que des générations, des tests et des déploiements.  

Configurez {{site.data.keyword.deliverypipeline}} afin d'automatiser la génération, le test et le déploiement en continu de vos applications.  

1. Si vous configurez cette intégration d'outil lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Delivery Pipeline**. En fonction du modèle utilisé, des zones différentes peuvent être disponibles. Passez en revue les valeurs de zone par défaut et, si nécessaire, modifiez ces paramètres. 
1. Si vous disposez d'une chaîne d'outils et que vous y ajoutez cette intégration d'outil, depuis le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Delivery Pipeline**.
1. Indiquez un nom pour votre nouveau pipeline.
1. Si vous prévoyez d'utiliser votre pipeline pour déployer une interface utilisateur, sélectionnez la case **Application visualisable**. Toutes les applications créées par votre pipeline sont affichées dans la liste **AFFICHER L'APPLICATION** de la page Intégrations d'outils de la chaîne d'outils. 
1. Cliquez sur **Créer une intégration** pour ajouter {{site.data.keyword.deliverypipeline}} à votre chaîne d'outils. 
1. Cliquez sur la vignette de {{site.data.keyword.deliverypipeline}} pour afficher le pipeline et le configurer. Pour en savoir plus sur les notions de base et la configuration d'un pipeline, voir [Génération et déploiement de pipelines](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Conseil **: Si vous souhaitez déclencher le pipeline lorsque vous envoyez des modifications par commande push à votre référentiel GitHub (repo), vous devez configurer GitHub pour votre chaîne d'outils avant de définir les étapes du pipeline. Ces étapes requièrent les URL de vos référentiels GitHub. Chaque étape de pipeline peut faire référence à un seul référentiel GitHub associé à votre chaîne d'outils. Pour des instructions de configuration de GitHub, voir la section [Configuration de GitHub et GitHub Issues](#github). 
  
1. Facultatif : Si vous souhaitez que Sauce Labs exécute des tests sur votre application, configurez {{site.data.keyword.deliverypipeline}} pour ajouter un travail de test Sauce Labs. Pour des instructions de configuration du travail de test, voir la section [Configuration d'un travail de test Sauce Labs sur votre pipeline](#config_saucelabs). 

### Configuration d'un travail de test Sauce Labs sur votre pipeline
{: #config_saucelabs}

Avant de configurer un travail de test Sauce Labs sur votre pipeline, vous avez besoin d'un pipeline opérationnel qui comporte des étapes pour la génération et le déploiement de votre application, et vous devez configurer Sauce Labs pour votre chaîne d'outils. Pour des instructions de configuration de Sauce Labs, voir la section [Configuration de Sauce Labs](#saucelabs). 

Configurez {{site.data.keyword.deliverypipeline}} pour ajouter un travail de test Sauce Labs. 

1. Si vous n'avez pas d'étape pour le déploiement d'une version de test de votre application, créez-en une. 
1. Dans l'étape, ajoutez un travail de test après le travail de déploiement. Le fait de placer ces travaux dans la même étape leur permet d'accéder au même ensemble de propriétés d'environnement. ![Travail de test](images/toolchain_test_job.png) 

1. Configurez l'étape :  

  a. Dans l'onglet **PROPRIETES D'ENVIRONNEMENT**, créez trois propriétés : CF_APP_NAME, SAUCE_USERNAME et SAUCE_ACCESS_KEY.
  
  b. Entrez vos nom d'utilisateur et clé d'accès Sauce Labs. En procédant ainsi, vous externalisez ces valeurs de façon à pouvoir les utiliser dans vos tests.
  
1. Configurez le travail de déploiement. Dans la zone **Script de déploiement**, ajoutez la commande suivante : export CF_APP_NAME="$CF_APP". Cette commande exporte le nom d'application en tant que propriété d'environnement. 
1. Configurez le travail de test. Les valeurs figurant dans l'image suivante sont des exemples. Les zones d'**instance de service**, de **cible**, d'**organisation** et d'**espace** sont renseignées avec les informations Sauce Labs de nom d'utilisateur, région, organisation et espace que vous utilisez actuellement.
![Configuration du travail](images/toolchain_configure_job.png)

  a. Pour le type d'outil de test, sélectionnez **Sauce Labs**.
  
  b. Pour l'instance de service, sélectionnez le nom d'utilisateur Sauce Labs utilisé lors de la configuration de Sauce Labs pour votre chaîne d'outils.  
  
   **Conseil **: Pour voir le nom d'utilisateur et la clé d'accès que vous avez utilisés lors de la configuration de Sauce Labs pour votre chaîne d'outils, cliquez sur **Configurer**. 
  
  c. Dans la zone de **commande d'exécution de test**, entrez les commandes d'installation des dépendances qui sont requises par vos tests, puis exécutez les tests. Ainsi, pour une application hypothétique Node.js app, vous pourriez entrer : 
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Si vous souhaitez voir vos rapports de test dans les journaux de travail, sélectionnez la case **Activer le rapport de test** et définissez le masque de fichiers de résultats de test sur `test/*.xml`.
  
1. Cliquez sur **SAUVEGARDER**. Désormais, à chaque exécution de votre pipeline, vos tests Sauce Labs s'exécuteront. 

Pour en savoir plus, voir [Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.

## Ajout de Deployment Risk Analytics
{: #dra}

{{site.data.keyword.DRA_full}} collecte et analyse les résultats provenant de tests unitaires, de tests fonctionnels et d'outils de couverture de code afin de déterminer si votre code satisfait les critères prédéfinis à certains stades de votre processus de déploiement. Si votre code ne satisfait pas ou dépasse les critères, le déploiement est interrompu afin de prévenir tout risque. Vous pouvez utiliser Deployment Risk Analytics comme filet de sécurité pour votre environnement de distribution continue ou comme moyen d'implémenter et d'améliorer les normes qualité.  

 **Conseil **: Cette intégration d'outil est préconfigurée. Elle ne requiert aucun paramètre de configuration et vous ne pouvez pas la reconfigurer. 
 
Ajoutez Deployment Risk Analytics afin de gérer et d'améliorer la qualité de votre code dans Bluemix en surveillant vos déploiements afin d'identifier les risques avant la publication. 

1. Si vous disposez d'une chaîne d'outils et que vous y ajoutez cette intégration d'outil, depuis le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Deployment Risk Analytics**. 
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette de Deployment Risk Analytics, puis complétez les étapes de mise en route : créez des critères, connectez-les au pipeline, puis exécutez ce dernier. Pour plus d'informations, voir [Deployment Risk Analytics](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.

## Ajout d'Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} est un environnement de développement Web intégré dans lequel vous pouvez créer, éditer, exécuter, déboguer et terminer des tâches de contrôle des sources. Vous pouvez facilement passer de l'édition à l'exécution à la soumission puis au développement.  

 **Conseil **: Cette intégration d'outil est préconfigurée. Elle ne requiert aucun paramètre de configuration et vous ne pouvez pas la reconfigurer. 
 
Ajoutez l'outil d'intégration Eclipse Orion {{site.data.keyword.webide}} pour terminer les tâches de contrôle des sources. 

1. Si vous disposez d'une chaîne d'outils et que vous y ajoutez cette intégration d'outil, depuis le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Eclipse Orion Web IDE**. 
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette de la nouvelle intégration Eclipse Orion Web IDE. Votre espace de travail est prérempli avec vos référentiels GitHub. Les référentiels associés à votre chaîne d'outils en cours sont mis en évidence. 

Pour en savoir plus, voir [Web IDE](https://www.ibm.com/devops/method/content/code/tool_web_ide/){: new_window}.


## Configuration de GitHub et GitHub Issues
{: #github}

GitHub est un service d'hébergement Web pour les référentiels Git. Vous pouvez avoir des copies en local et à distance de vos référentiels, ce qui simplifie la collaboration.  

GitHub Issues est un outil de suivi qui conserve votre travail et vos plans à un seul et même emplacement. Il est intégré à votre référentiel de développement pour vous permettre de vous concentrer sur les tâches importantes. 

Configurez GitHub et GitHub Issues pour gérer votre code source dans le cloud :

1. Si vous configurez cette intégration d'outil lors de la création de la chaîne d'outils, procédez comme suit :

 a. A la section Intégrations configurables, cliquez sur **GitHub**. Si vous n'avez pas autorisé {{site.data.keyword.Bluemix}} à accéder à GitHub, cliquez sur **Autorisation** pour accéder au site Web GitHub. Si vous n'avez pas de session GitHub active, vous êtes invité à vous connecter. Cliquez sur **Authorize Application** pour autoriser {{site.data.keyword.Bluemix}} à accéder à votre compte GitHub. Si vous disposez d'une session GitHub active mais n'avez pas saisi votre mot de passe récemment, vous êtes invité à entrer votre mot de passe GitHub pour confirmation. 
 
 b. Passez en revue les emplacements de référentiel cible par défaut pour les référentiels GitHub. Ces référentiels sont clonés à partir des référentiels exemple. Si nécessaire, modifiez les noms des référentiels cible.
![Emplacements de référentiel cible par défaut](images/toolchain_github_config.png)
   
1. Si vous disposez d'une chaîne d'outils et que vous y ajoutez cette intégration d'outil, depuis le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **GitHub**.
1. Si vous disposez d'un référentiel GitHub et souhaitez l'utiliser, entrez son URL. Pour le type de référentiel, cliquez sur **Lier**.
1. Si vous souhaitez utiliser un nouveau référentiel GitHub, indiquez un nom pour le référentiel GitHub, entrez l'URL du référentiel que vous clonez ou déviez, puis sélectionnez le type de référentiel :  

 a. Pour créer un référentiel vide, sélectionnez **Nouveau**. 
 
 b. Pour créer une copie d'un référentiel GitHub, sélectionnez **Cloner**.
 
 c. Pour dévier un référentiel GitHub afin de pouvoir participer aux modifications via des demandes pull, sélectionnez **Dévier**.
 
1. Si vous souhaitez utiliser GitHub Issues pour le suivi des problèmes, sélectionnez la case **Activer GitHub Issues**. 
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette du référentiel GitHub que vous souhaitez utiliser pour accéder à github.com et afficher le contenu du référentiel. 
 
  **Conseil **: Vous pouvez utiliser les outils intégrés de gestion de code source d'Eclipse Orion Web IDE pour éditer le référentiel GitHub et déployer une application depuis votre poste de travail. 

1. Si vous avez activé GitHub Issues, cliquez sur la vignette GitHub Issues pour accéder à GitHub Issues.

Pour en savoir plus, voir [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} et [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.    

##Utilisation de Dedicated {{site.data.keyword.ghe_short}}
{: #ghe}

{{site.data.keyword.ghe_long}} est la version entièrement géré et hébergée par IBM Cloud de {{site.data.keyword.ghe_short}}, disponible pour les environnements Dedicated Bluemix. GitHub fournit l'expérience de codage social chère aux développeurs. [{{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#dedicated){: new_window} fournit un environnement Cloud Computing sur du matériel isolé physiquement qui est intégré à votre réseau.

Dedicated {{site.data.keyword.ghe_short}} est destiné aux clients {{site.data.keyword.Bluemix_notm}} Dedicated uniquement. 

### Configuration de votre compte 

{{site.data.keyword.ghe_short}} inclut une connexion unique à {{site.data.keyword.Bluemix_notm}} Dedicated. Pour vous connecter à {{site.data.keyword.ghe_short}}, collez dans un navigateur l'URL fourni par votre administrateur de région ou provenant de votre courrier électronique de bienvenue. L'URL doit suivre le masque suivant : `github.nom-dédié-votre-société.bluemix.net`. Connectez-vous avec vos ID utilisateur et mot de passe {{site.data.keyword.Bluemix_notm}} Dedicated, et votre compte {{site.data.keyword.ghe_short}} est automatiquement créé. 

**Remarque :** Si un message indique que votre ID utilisateur n'existe pas, demandez à votre administrateur régional de l'ajouter au registre d'utilisateurs {{site.data.keyword.Bluemix_notm}} Dedicated. Si vous êtes l'administrateur de région, voir [Gestion des utilisateurs et des droits {{site.data.keyword.Bluemix_notm}} Dedicated](https://new-console.stage1.ng.bluemix.net/docs/admin/index.html#oc_useradmin){: new_window}.

Dans la plupart des cas, votre nom d'utilisateur GitHub correspond à votre nom abrégé d'adresse électronique, sauf si votre nom abrégé inclut des caractères non pris en charge par GitHub, comme les points. Dans ce cas, les caractères non pris en charge sont remplacés par des tirets.      

### Ajout d'une adresse électronique à votre compte 

Vous devez ajouter votre adresse électronique à vos paramètres de compte {{site.data.keyword.ghe_short}} pour recevoir les notifications. Après avoir ajouté votre adresse électronique, vous pouvez tirer parti des fonctions de codage social (social coding) de {{site.data.keyword.ghe_short}}.    
 
Pour ajouter votre adresse électronique à votre compte Dedicated {{site.data.keyword.ghe_short}}, procédez comme suit :     
1. Dans le coin supérieur droit d'une page GitHub, cliquez sur votre icône de profil, puis cliquez sur **Settings**.    
2. Dans la barre de navigation, cliquez sur **Emails**.    
3. Ajoutez votre adresse électronique puis cliquez sur **Add**.     

{: #ghe_auth}
### Création d'un jeton d'accès personnel ou d'une clé SSH pour l'authentification

Pour effectuer des opérations Git à distance, telles que `clone` ou `push`, depuis votre référentiel Git local, vous devez utiliser un jeton d'accès personnel ou une clé SSH pour vous authentifier auprès de {{site.data.keyword.ghe_short}}. L'authentification via HTTPS est prise en charge uniquement avec l'utilisation d'un jeton d'accès ; vous ne pouvez pas utiliser vos ID utilisateur et mot de passe pour cloner ou envoyer par commande push depuis un référentiel local. Les demandes d'API requièrent également un jeton d'accès personnel. 

**Remarque :** Pour utiliser un jeton d'accès personnel ou une clé SSH pour l'authentification, vous devez configurer Git en local. Pour des instructions, voir [Set Up Git](https://help.github.com/enterprise/2.6/user/articles/set-up-git/){: new_window}.    

Pour créer un jeton d'accès personnel, procédez comme suit :     
   1. Dans le coin supérieur droit d'une page GitHub, cliquez sur votre icône de profil, puis cliquez sur **Settings**.    
   2. Dans la barre de navigation, cliquez sur **Personal access tokens**.   
   3. Cliquez sur **Generate new token**.
   4. Ajoutez une description du jeton et cliquez sur **Generate token**.
   5. Copiez le jeton dans un emplacement sécurisé ou une application de gestion des mots de passe.
     **Remarque :** Pour des raisons de sécurité, une fois que vous avez quitté la page, vous ne pouvez plus réafficher le jeton.    

Utilisez votre jeton d'accès personnel à la place d'un mot de passe pour l'accès par ligne de commande via HTTPS. 


Pour créer une clé SSH, procédez comme suit : 
   1. Ouvrez Git Bash (Windows) ou une nouvelle fenêtre de terminal (Linux et Mac).    
   2. Collez le texte suivant, en indiquant l'adresse électronique que vous avez ajoutée à votre compte {{site.data.keyword.ghe_short}} :
   
     ``
     ssh-keygen -t rsa -b 4096 -C "votre_email@exemple.com"
     # Creates a new ssh key, using the provided email as a label
     Generating public/private rsa key pair.
     ``

   3. Lorsque vous êtes invité à indiquer un fichier dans lequel sauvegarder la clé, appuyez sur Entrée pour accepter l'emplacement par défaut. 
   4. A l'invite, entrez une phrase passe sécurisée. Pour plus d'informations, voir [Working with SSH key passphrases](https://help.github.com/enterprise/2.6/user/articles/working-with-ssh-key-passphrases/){: new_window}.   

Ajoutez votre clé SSH à l'agent ssh-agent :    
   1. Assurez-vous que ssh-agent est activé. A l'aide de Git Bash, entrez la commande suivant pour activer ssh-agent :
      ``
      # start the ssh-agent in the background
      $ eval "$(ssh-agent -s)"
      Agent pid 59566
      ``    
  
   2. Ajoutez votre clé SSH à l'agent ssh-agent en entrant la commande suivante :
      ``
      $ ssh-add ~/.ssh/id_rsa
      ``    
   3. Ajoutez la clé SSH à votre compte GitHub. Pour plus d'informations, voir [Adding a new SSH key to your GitHub account](https://help.github.com/enterprise/2.6/user/articles/adding-a-new-ssh-key-to-your-github-account/){: new_window}.    
   

### Configuration d'organisations, d'équipes et de référentiels GitHub    

La configuration d'organisations GitHub permet de créer des groupes d'utilisateurs distincts travaillant sur des projets ou des tâches similaires. L'organisation d'équipes au sein d'une organisation présente l'avantage supplémentaire de contrôler l'accès aux référentiels. Pour plus d'informations, voir [Organizations and teams](https://help.github.com/enterprise/2.6/admin/guides/user-management/organizations-and-teams/){: new_window}.

**Remarque :** Les organisations GitHub ne sont pas identiques aux organisations Bluemix. 

Configurez le projet de votre équipe en procédant comme suit : 

   1. [Créez une organisation (org)](https://help.github.com/enterprise/2.6/user/articles/creating-a-new-organization-account/){: new_window}.
   2. [Créez un référentiel pour votre organisation](https://help.github.com/enterprise/2.6/user/articles/create-a-repo/){: new_window}.
   3. [Invitez des utilisateurs à rejoindre votre organisation](https://help.github.com/enterprise/2.6/user/articles/inviting-users-to-join-your-organization/){: new_window}.
   4. [Sélectionnez soigneusement au moins un membre d'équipe qui aura les droits de propriétaire dans votre organisation](https://help.github.com/enterprise/2.6/user/articles/changing-a-person-s-role-to-owner/){: new_window}.    
   
  **Remarque :** Pour que vous puissiez inviter des utilisateurs dans votre organisation, ceux-ci doivent se connecter à {{site.data.keyword.ghe_short}} au moins une fois ou bien leurs comptes {{site.data.keyword.ghe_short}} ne seront pas disponibles pour invitation.
   
### Obtention du support
Pour obtenir des réponses immédiate, soumettez vos questions sur le site [Stack Overflow](http://stackoverflow.com/questions/ask?tags=ibm-bluemix_github-enterprise){: new_window}. 

Pour une assistance supplémentaire, utilisez les ressources suivantes :     
   1. Complétez le formulaire à l'adresse https://ibm.biz/bluemixsupport.   
   2. Soumettez un nouveau ticket via le portail Client Success Portal à l'adresse https://support.ibmcloud.com/ics/support/mylogin.asp?login=bluemix.    


## Configuration de PagerDuty
{: #pagerduty}

PagerDuty intègre dans une vue unique les données provenant de plusieurs systèmes de surveillance. Quand un problème survient, PagerDuty s'assure que le membre d'équipe le plus à même de le résoudre reçoit une notification. Si le membre d'équipe ne résout pas le problème, il est possible de mettre en place des escalades afin de router le problème vers des ingénieurs de second niveau ou des gestionnaires des opérations.

Configurez PagerDuty pour l'envoi de notifications en cas d'échec d'étape de pipeline afin de pouvoir résoudre les problèmes plus rapidement et de réduire le temps d'indisponibilité. 

1. Si vous configurez cette intégration d'outil lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **PagerDuty**. 
1. Si vous disposez d'une chaîne d'outils et que vous y ajoutez cette intégration d'outil, depuis le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **PagerDuty**.
1. Entrez le nom du site PagerDuty associé à votre compte PagerDuty. Si vous ne disposez pas d'un compte PagerDuty, [inscrivez-vous](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Entrez la clé d'accès d'API pour votre compte PagerDuty. Pour savoir comment trouver la clé, voir [API Authentication](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Entrez le nom de votre service PagerDuty. 
1. Entrez l'adresse électronique du contact PagerDuty principal. 
1. Entrez le numéro de téléphone du contact PagerDuty principal. 
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette PagerDuty pour accéder à pagerduty.com. Vous pouvez afficher les événements associés au service PagerDuty spécifié lors de la configuration de cette intégration d'outil pour votre chaîne d'outils.  

Pour en savoir plus, voir [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configuration de Sauce Labs
{: #saucelabs}

Sauce Labs exécute des tests unitaires fonctionnels. Quand une suite de tests Sauce Labs est configurée comme travail de test dans {{site.data.keyword.deliverypipeline}}, cette suite de tests peut exécuter des tests en fonction de votre application Web ou mobile dans le cadre de votre processus de distribution continue. Ces tests peuvent fournir un contrôle de flux de valeur pour vos projets, agissant comme des barrières pour empêcher le déploiement de code incorrect. 

Configurez Sauce Labs pour l'exécution de tests fonctionnels automatisés sur plusieurs systèmes d'exploitation et navigateurs afin de pouvoir émuler la façon dont un utilisateur peut utiliser un site Web ou une application :

1. Si vous configurez cette intégration d'outil lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Sauce Labs**. 
1. Si vous disposez d'une chaîne d'outils et que vous y ajoutez cette intégration d'outil, depuis le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**. 
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Sauce Labs**.
1. Entrez le nom d'utilisateur associé à votre compte Sauce Labs. Vous pouvez [trouver votre nom d'utilisateur dans le message d'accueil situé en haut de votre page de compte Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Entrez la clé d'accès de votre compte Sauce Labs. Vous pouvez [trouver la clé dans le coin inférieur gauche de votre page de compte Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette Sauce Labs pour accéder à saucelabs.com et afficher l'activité de test pour la chaîne d'outils.

 **Conseil **: Si vous avez ajouté un travail de test Sauce Labs à {{site.data.keyword.deliverypipeline}}, vous pouvez sélectionner l'instance de service. 

Pour en savoir plus, voir [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configuration de Slack
{: #slack}

**Important **: Les notifications postées sur des canaux Slack publics sont visibles de tout membre de l'équipe. N'oubliez pas que vous êtes responsable du contenu de vos articles. 

Slack est un système de messagerie et de notification en temps réel, basé sur le cloud. Slack fournit un système de discussion permanente, alternative plus interactive au courrier électronique pour la collaboration des équipes. Vous pouvez communiquer avec votre équipe sur un canal dédié ou sur un ensemble de canaux directement liés à votre travail. Vous pouvez également partager des fichiers et des images via ces canaux, ou dans des messages directs entre deux personnes ou plus. Les communications dans les messages directs ou sur les canaux sont conservées pour que vous puissiez y faire des recherches.  

Configurez Slack pour la réception de notifications concernant votre chaîne d'outils depuis les intégrations d'outils, par exemple les activités de test et de déploiement : 

1. Si vous configurez cette intégration d'outil lorsque vous créez la chaîne d'outils, à la section Intégrations configurables, cliquez sur **Slack**. 
1. Si vous disposez d'une chaîne d'outils et que vous y ajoutez cette intégration d'outil, depuis le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur la chaîne d'outils pour ouvrir sa page Intégrations d'outils. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**.
1. Cliquez sur le bouton d'ajout (+).
1. A la section Intégrations d'outils, cliquez sur **Slack**.
1. Entrez le jeton d'authentification d'API pour votre compte Slack. Vous devez utiliser un jeton d'accès complet généré pour l'authentification avec Slack. Pour savoir comment trouver le jeton, voir [Slack authentication](https://api.slack.com/web#authentication){: new_window}.
1. Entrez le nom du canal Slack sur lequel vous souhaitez recevoir les notifications. Si le canal spécifié n'existe pas, il est créé. Si le canal a été archivé, il est réactivé. 
1. Cliquez sur **Créer une intégration**.
1. Cliquez sur la vignette Slack. Vous pouvez afficher toutes les activités de votre chaîne d'outils dans le canal Slack configuré. 

Pour en savoir plus, voir [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
