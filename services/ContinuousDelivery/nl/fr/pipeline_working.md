---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-6"

---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Utilisation de {{site.data.keyword.deliverypipeline}} {: #pipeline-working}

Pour automatiser vos générations et déploiements dans {{site.data.keyword.Bluemix}}, utilisez
{{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Avec {{site.data.keyword.deliverypipeline}}, vous pouvez choisir entre plusieurs types de génération. Vous fournissez le script de génération et {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} l'exécute ; il n'est pas nécessaire de configurer des systèmes de génération. Ensuite, en un clic, vous pouvez déployer automatiquement votre application dans un ou plusieurs espaces {{site.data.keyword.Bluemix_notm}}, sur un ou plusieurs serveurs Cloud Foundry publics, ou dans un ou plusieurs
conteneurs Docker dans IBM Containers for {{site.data.keyword.Bluemix_notm}}.

Les travaux de génération compilent et assemblent en package le code source de votre application depuis les référentiels Git. Ils génèrent des artefacts pouvant être déployés,
tels que des fichiers WAR ou des conteneurs Docker pour IBM Containers. De plus, vous pouvez
exécuter des tests unitaires dans votre génération automatiquement. Vous pouvez configurer les travaux de génération de sorte que chaque fois qu'une validation est
envoyée, une génération est déclenchée.

Un travail de déploiement prend la sortie d'un travail de génération et la déploie sur des serveurs IBM Containers ou Cloud Foundry tels que {{site.data.keyword.Bluemix_notm}}.

Vous pouvez effectuer le déploiement dans une ou plusieurs régions et dans un ou plusieurs services. Par exemple, vous pouvez configurer votre {{site.data.keyword.deliverypipeline}} en vue d'utiliser un ou plusieurs services, le tester dans une région, et le déployer en production dans plusieurs régions. Pour plus d'informations, voir
[Régions](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}.

Si vous utilisez plusieurs pipelines dans une chaîne d'outils ouverte, vous pouvez créer un pipeline composite pour gérer le déploiement de tous les pipelines à partir d'un emplacement unique. 

Il existe plusieurs manières de créer un pipeline,
comme l'ajout d'un pipeline à une application existante et la
création d'un pipeline sans aucune application existante. Si vous ne disposez pas encore d'un
service {{site.data.keyword.deliverypipeline}} dans votre organisation,
accédez au catalogue, cliquez sur {{site.data.keyword.deliverypipeline}}, puis sur Créer.

Procédez comme suit pour configurer un
{{site.data.keyword.deliverypipeline}} pour une
application existante :

1. Dans la tableau de bord d'applications {{site.data.keyword.Bluemix_notm}}, cliquez sur votre application.
1. Dans le menu en hamburger sur la barre de menus {{site.data.keyword.Bluemix_notm}}, cliquez sur
**Services**, puis sur **DevOps**.
1. Cliquez sur **Pipelines**, puis sur **Créer un pipeline**.

Pour [créer un pipeline ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} configuré pour déployer une application Cloud Foundry, procédez comme suit : 

1. Cliquez sur **Cloud Foundry**.
1. Si vous désirez utiliser un nom différent pour le pipeline, modifiez son nom par défaut.
1. Si vous désirez utiliser un nom différent pour l'application, modifiez son nom par défaut. Ce nom est celui de l'application où est déployé le pipeline.
1. Si vous n'avez pas de chaînes d'outils, une chaîne d'outils portant le nom par défaut est créée pour vous. Si vous désirez utiliser un autre nom pour la chaîne d'outils, modifiez son nom. Grâce à la chaîne d'outils, vous pouvez étendre les capacités de votre pipeline par une intégration avec d'autres outils et services. Pour plus d'informations sur les chaînes d'outils, voir [Utilisation des chaînes d'outils](/docs/services/ContinuousDelivery/toolchains_working.html){: new_window}.

 **Conseil **: les pipelines et les chaînes d'outils appartiennent à des organisations (orgs). Si vous appartenez à une organisation disposant de chaînes d'outils, vous pouvez être ajouté à la liste de contrôle d'accès de l'une de ses chaînes d'outils associées. Une fois que vous êtes ajouté à la liste de contrôle d'accès d'une chaîne d'outils,vous pouvez utiliser cette chaîne d'outils et ses pipelines associés, même si vous ne les avez pas créés. Pour plus d'informations sur le contrôle d'accès pour les chaînes d'outils,  voir [Gestion de l'accès](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}.

1. Sélectionnez la chaîne d'outils que vous désirez utiliser ou entrez le nom de la nouvelle chaîne d'outils à créer.
1. Sélectionnez votre fournisseur Git.

 **Conseil **: Si vous n'avez pas autorisé {{site.data.keyword.Bluemix_notm}} à accéder à GitHub, vous êtes invité à cliquer sur **Autoriser** pour accéder au site Web GitHub. Si vous n'avez pas de session GitHub active, vous êtes invité à vous connecter. Cliquez sur **Authorize Application** pour autoriser {{site.data.keyword.Bluemix_notm}} à accéder à votre compte GitHub. Si vous disposez d'une session GitHub active mais n'avez pas saisi votre mot de passe récemment, vous êtes invité à entrer votre mot de passe GitHub pour confirmation.

   * Si vous disposez d'un référentiel et désirez l'utiliser, sélectionnez **Lien** pour le type de référentiel. Recherchez l'emplacement du référentiel ou sélectionnez le référentiel dans la liste des référentiels disponibles.

   * Si vous désirez créer un référentiel vide, sélectionnez **Nouveau** pour le type de référentiel. Entrez un nom pour le référentiel.

   * Si vous désirez créer un clone d'un référentiel, sélectionnez **Copie** pour le type de référentiel. Recherchez l'emplacement du référentiel ou sélectionnez le référentiel dans la liste des référentiels disponibles.

   * Si vous désirez dévier un référentiel pour pouvoir contribuer à des modifications via des demandes d'extraction, sélectionnez **Déviation**. Recherchez l'emplacement du référentiel ou sélectionnez le référentiel dans la liste des référentiels disponibles.

1. Sélectionnez un référentiel ou entrez une URL de référentiel.
1. Cliquez sur **Créer**. Le pipeline est créé, configuré et affiché sur la page Présentation de la chaîne d'outils.
 ![Carte du pipeline](images/cd_pipeline.png)
1. Si vous avez créé un pipeline dans une chaîne d'outils contenant un pipeline composite, le nouveau pipeline est ajouté au pipeline composite. Modifiez le plan de déploiement pour inclure des tâches de déploiement pour le nouveau pipeline. Voir [Création de tâches Delivery Pipeline](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_pipelineCD){: new_window}.

Pour créer un [pipeline vide ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} sans étapes préconfigurées :

1. Cliquez sur **Personnalisé**.
1. Si vous désirez utiliser un nom différent pour le pipeline, modifiez son nom par défaut.
1. Si vous n'avez pas de chaînes d'outils, une chaîne d'outils portant le nom par défaut est créée pour vous. Si vous désirez utiliser un autre nom pour la chaîne d'outils, modifiez son nom. Grâce à la chaîne d'outils, vous pouvez étendre les capacités de votre pipeline par une intégration avec d'autres outils et services.
1. Sélectionnez la chaîne d'outils que vous désirez utiliser ou entrez le nom de la nouvelle chaîne d'outils à créer.
1. Cliquez sur **Créer**. Un pipeline vide est créé et représenté sous forme de carte sur la page Présentation de la chaîne d'outils.

A partir de {{site.data.keyword.deliverypipeline}}, modifiez votre configuration, vérifiez le statut des générations, l'application déployée et les déploiements récents, examinez les journaux les plus récents et les détails du déploiement, ou supprimez votre pipeline.
