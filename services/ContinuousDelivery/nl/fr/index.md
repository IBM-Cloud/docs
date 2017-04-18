---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation à {{site.data.keyword.contdelivery_short}}
{: #cd_getting_started}

Dernière mise à jour : 18 novembre 2016
{: .last-updated}  

Adoptez une approche DevOps en utilisant {{site.data.keyword.contdelivery_full}}, lequel inclut des chaînes d'outils qui automatisent la construction et le déploiement d'applications. Vous
pouvez commencer en créant une chaîne d'outils de déploiement simple qui prend en charge les tâches de développement, de déploiement et les opérations.
{: shortdesc}

Après avoir créé une instance de {{site.data.keyword.contdelivery_short}} en sélectionnant la vignette de ce service dans le catalogue {{site.data.keyword.Bluemix_notm}}, vous pouvez choisir la manière dont vous souhaitez démarrer avec le service.
 ![Page d'accueil de Continuous Delivery](images/cd_landing_page.png)

 * Pour commencer rapidement et déployer votre application à l'aide d'un pipeline automatisé, dans la section
"Démarrage avec un pipeline", cliquez sur **[Commencer ici](#starting_with_a_pipeline)**. Vous pourrez ajouter d'autres outils ultérieurement. 
 * Pour créer et configurer une chaîne d'outils de distribution continue depuis un modèle, dans la section "Démarrage depuis un modèle de chaîne d'outils", cliquez sur **[Commencer ici](#starting_from_a_toolchain_template)**. La chaîne d'outils intègre des outils destinés à la planification, au développement, au déploiement de pipelines et à la gestion de vos applications. Vous pouvez toujours ajouter ou retirer des outils dans vos chaînes d'outils.

 * Si vous disposez déjà de chaînes d'outils, dans la section "Démarrage depuis un modèle de chaîne d'outils", cliquez sur **Afficher vos chaînes
d'outils**. Pour plus d'informations sur l'utilisation des chaînes d'outils, voir [Utilisation de chaînes d'outils sur Bluemix Public](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}.

## Démarrage avec un pipeline
{: #starting_with_a_pipeline}

Les pipelines automatisent les générations, les déploiements, etc. Pour commencer avec un pipeline automatisé, sélectionnez un modèle et indiquez l'emplacement de votre référentiel GitHub (repo).

Pour [créer un pipeline (ce lien ouvre une nouvelle fenêtre)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} configuré pour déployer une application Cloud Foundry, procédez comme suit :

1. Cliquez sur **Cloud Foundry**.
1. Si vous désirez utiliser un nom différent pour le pipeline, modifiez son nom par défaut. Le nom du pipeline l'identifie dans {{site.data.keyword.Bluemix_notm}}. 
1. Si vous désirez utiliser un nom différent pour l'application, modifiez son nom par défaut. Le nom de l'application l'identifie dans {{site.data.keyword.Bluemix_notm}}. Ce nom est celui de l'application où est déployé le pipeline. 
1. Si vous n'avez pas de chaînes d'outils, une chaîne d'outils portant le nom par défaut est créée pour vous. Si vous désirez utiliser un autre nom pour la chaîne d'outils, modifiez son nom. Les pipelines sont gérés par des chaînes d'outils. Grâce à la chaîne d'outils, vous pouvez étendre les capacités de votre pipeline par une intégration avec d'autres outils et services. 

 **Conseil **: les pipelines et les chaînes d'outils appartiennent à des organisations (orgs). Si vous appartenez à une organisation disposant de chaînes d'outils, vous pouvez utiliser ces chaînes d'outils même si vous ne les avez pas créées.
 
1. Sélectionnez la chaîne d'outils que vous désirez utiliser ou entrez le nom de la nouvelle chaîne d'outils à créer.
1. Indiquez l'emplacement de votre référentiel GitHub.

 **Conseil **: Si vous n'avez pas autorisé {{site.data.keyword.Bluemix_notm}} à accéder à GitHub, vous êtes invité à cliquer sur **Autoriser** pour accéder au site Web GitHub. Si vous n'avez pas de session GitHub active, vous êtes invité à vous connecter. Cliquez sur **Authorize Application** pour autoriser {{site.data.keyword.Bluemix_notm}} à accéder à votre compte GitHub. Si vous disposez d'une session GitHub active mais n'avez pas saisi votre mot de passe récemment, vous êtes invité à entrer votre mot de passe GitHub pour confirmation.

   * Si vous disposez d'un référentiel GitHub et désirez l'utiliser, sélectionnez **Lien** pour le type de référentiel. Recherchez l'emplacement du référentiel ou sélectionnez le référentiel dans la liste des référentiels disponibles.
   
   * Si vous désirez créer un référentiel GitHub vide, sélectionnez **Nouveau** pour le type de référentiel. Entrez un nom pour le référentiel.
   
   * Si vous désirez créer un clone d'un référentiel GitHub, sélectionnez **Copie** pour le type de référentiel. Recherchez l'emplacement du référentiel ou sélectionnez le référentiel dans la liste des référentiels disponibles.
   
   * Si vous désirez dévier un référentiel GitHub pour pouvoir contribuer des modifications via des demandes d'extraction, sélectionnez **Déviation**. Recherchez l'emplacement du référentiel ou sélectionnez le référentiel dans la liste des référentiels disponibles.
 
1. Cliquez sur **Créer**. Le pipeline est créé, configuré et affiché sur la page Présentation de la chaîne d'outils. ![Vignette de pipeline](images/cd_pipeline.png)
 
Pour créer un [pipeline vide (ce lien ouvre une nouvelle fenêtre)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} sans étapes préconfigurées :

1. Cliquez sur **Personnalisé**.
1. Si vous désirez utiliser un nom différent pour le pipeline, modifiez son nom par défaut. Le nom du pipeline l'identifie dans {{site.data.keyword.Bluemix_notm}}. 
1. Si vous n'avez pas de chaînes d'outils, une chaîne d'outils portant le nom par défaut est créée pour vous. Si vous désirez utiliser un autre nom pour la chaîne d'outils, modifiez son nom. Les pipelines sont gérés par des chaînes d'outils. Grâce à la chaîne d'outils, vous pouvez étendre les capacités de votre pipeline par une intégration avec d'autres outils et services.
1. Sélectionnez la chaîne d'outils que vous désirez utiliser ou entrez le nom de la nouvelle chaîne d'outils à créer.
1. Cliquez sur **Créer**. Un pipeline vide est créé et représenté sous forme de vignette de la page Présentation de la chaîne d'outils.

## Démarrage depuis un modèle de chaîne d'outils
{: #starting_from_a_toolchain_template}

Pour créer et configurer une chaîne d'outils de distribution continue depuis un [modèle (ce lien ouvre une nouvelle fenêtre)](https://console.ng.bluemix.net/devops/create){: new_window} :

1. Sur la page **Créer une chaîne d'outils**, cliquez sur un modèle de chaîne d'outils.  
1. Examinez le diagramme de la chaîne d'outils que vous être sur le point de créer. Ce diagramme montre chaque intégration d'outil dans sa phase de cycle de vie au sein de la chaîne d'outils. L'image suivante fournit un exemple de diagramme. Lorsque vous créez une chaîne d'outils, le diagramme représente chaque intégration d'outil faisant partie de la chaîne d'outils.
 ![Diagramme de chaîne d'outils](images/toolchain_diagram.png)
1. Passez en revue les informations par défaut des paramètres de chaîne d'outils. Le nom de la chaîne d'outils l'identifie dans {{site.data.keyword.Bluemix_notm}}. Si vous désirez utiliser un nom différent, modifiez le nom de la chaîne d'outils.
1. A la section Intégrations configurables, sélectionnez chaque intégration d'outil à configurer pour votre chaîne d'outils. Quelques intégrations d'outils ne nécessitent pas de configuration. Pour des informations sur la configuration des intégrations d'outils, voir [Configuration d'intégrations d'outils](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Cliquez sur **Créer**. Plusieurs étapes s'exécutent automatiquement pour configurer votre chaîne d'outils.

 * La chaîne d'outils est créée.
 * Si vous avez configuré l'intégration de l'outil Delivery Pipeline, les pipelines sont créés et déclenchés.
 * Si vous avez configuré l'intégration de l'outil Sauce Labs, celui-ci est configuré pour ajouter des travaux aux pipelines et exécuter des tests.
 * Si vous avez configuré l'intégration de l'outil PagerDuty, PagerDuty est configuré pour envoyer des notifications d'alerte au service que vous avez spécifié. 
 * Si vous avez configuré l'intégration de l'outil Slack, Slack est configuré pour envoyer au canal que vous avez spécifié des notifications sur le statut de déploiement. 
 * Si vous avez configuré l'intégration d'outil GitHub, le référentiel exemple GitHub est cloné dans votre compte GitHub. 

# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}

* [Créer et utiliser votre première chaîne d'outils (ce lien ouvre une nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Créer une chaîne d'outils personnalisée (ce lien ouvre une nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Créer une application avec trois microservices (ce lien ouvre une nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}

## Liens connexes
{: #general}

* [Chaîne d'outils de microservices (ce lien ouvre une nouvelle fenêtre)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Chaîne d'outils simple (ce lien ouvre une nouvelle fenêtre)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method){:new_window}
