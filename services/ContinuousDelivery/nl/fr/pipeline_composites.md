---

copyright:
  years: 2017
lastupdated: "2017-4-5"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilisation de pipelines composites (expérimental)
{: #deliverypipeline_create_composite}

La fonction de pipeline composite pour {{site.data.keyword.deliverypipeline}} vous permet de gérer des processus reproductibles d'intégration continue et de distribution continue pour des applications logicielles connexes.
{:shortdesc}

Vous pouvez créer des pipelines composites pour gérer les applications dans une chaîne d'outils. Si votre chaîne d'outils contient des applications déployées par {{site.data.keyword.deliverypipeline}}, elle est mise à jour dynamiquement lorsque vous lui ajoutez des pipelines de distribution ou que vous en supprimez. Vous pouvez également ajouter des applications au pipeline composite à partir de sources externes.

## Création d'un pipeline composite
{: #compositepipeline_create_for_toolchain}

1. Dans le menu en regard du logo Bluemix, cliquez sur **Services > DevOps**.

1. Dans la barre de navigation de gauche, cliquez sur **Pipelines**.

2. Activez la fonction de pipeline composite en cliquant sur **En savoir plus**, puis sur **Activer**. Le pipeline composite étant activé pour chaque utilisateur, seuls les membres de votre organisation (org) qui ont adhéré à la fonction expérimentale voient les pipelines composites que vous créez.

2. Cliquez sur **Créer** > **Pipeline composite**.

3. Saisissez un nom pour le pipeline composite. Vous pouvez également modifier la description du pipeline.

4. Dans la liste **Chaîne d'outils**, sélectionnez une chaîne d'outils.

    1. Pour créer une chaîne d'outils vide et un pipeline composite, sélectionnez **Nouveau**.

    2. Pour créer un pipeline composite pour l'une de vos chaînes d'outils, sélectionnez son nom.

5. Si vous créez une chaîne d'outils vide, sélectionnez **Ajouter des environnements par défaut**. Utilisez ces environnements logiques par défaut pour contrôler l'exécution de processus via le pipeline composite.

6. Cliquez sur **Créer**.

Les étapes que vous avez configurées sont automatiquement mappées à l'espace approprié dans votre organisation et un plan de déploiement est créé pour le pipeline composite.

Si vous avez créé le pipeline composite pour une chaîne d'outils contenant des pipelines de distribution, les applications pour tous les pipelines de la chaîne d'outils sont ajoutées au pipeline composite. Les étapes que vous avez configurées dans les pipelines de distribution sont automatiquement mappées aux espaces appropriés dans votre organisation et leur statut s'affiche.
Pour visualiser le statut de chaque travail dans une application, développez l'application.

Un plan de déploiement est également créé pour le pipeline composite. Par défaut, les travaux de toutes les applications s'exécutent en parallèle pour un espace, mais vous pouvez modifier l'ordre de déploiement de vos applications dans le plan.

Si vous avez créé le pipeline composite pour une nouvelle chaîne d'outils, un plan de déploiement est créé pour que vous le personnalisiez.

![Développez chaque application pour visualiser chaque travail dans son pipeline](images/composite_view.png "expand each app")

## Modification du plan de déploiement
{: #compositepipeline_modify_dp}

Par défaut, un plan de déploiement est créé pour un pipeline composite. Ce plan de déploiement capture toutes les informations relatives aux étapes dans les pipelines de distribution de la chaîne d'outils. Vous pouvez afficher et modifier le plan de déploiement pour chaque étape.

Dans l'étape dont vous souhaitez modifier le plan de déploiement, cliquez sur le menu, puis sur **Plan de déploiement**.

![Ouvrez le plan de déploiement](images/open_deployment_plan.png "open the deployment plan")

La liste des tâches de déploiement pour votre environnement s'affiche.

![Plan de déploiement par défaut pour un pipeline composite contenant trois pipelines individuels](images/composite_deploy_plan.png)

Pour plus d'informations sur la modification du plan de déploiement, voir [Personnalisation des plans de déploiement pour les pipelines composites](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html).

## Modification de pipelines individuels
{: #compositepipeline_add_job}

Vous pouvez modifier des pipelines individuels à partir du pipeline composite.

1. Développez l'application.

2. Dans le menu de l'étape, cliquez sur **Configurer**.

3. Ajoutez, modifiez ou supprimez des travaux dans l'étape. Pour des instructions détaillées, voir [Ajout d'un travail à une étape](pipeline_build_deploy.html#deliverypipeline_add_job).

## Exécution de travaux dans un pipeline composite
{: #compositepipeline_run_jobs}

Après avoir développé une application pour afficher ses travaux, vous pouvez exécuter manuellement tous ses travaux dans une étape. Cliquez sur l'icône **Déployer dans *étape*** dans l'espace d'une application.

![Exécution d'une étape dans une seule application](images/composite_run_stage.png)

Pour exécuter tous les travaux de toutes les applications d'un espace, cliquez sur l'icône **Déployer dans *espace*** dans l'espace du pipeline composite.

![Exécution d'une étape dans toutes les applications](images/composite_run_space.png)

Les travaux s'exécutent selon le plan de déploiement du plan directeur composite.

## Affichage des journaux
{: #compositepipeline_view_logs}

Pour afficher les journaux d'un travail, développez l'application qui contient le travail, puis cliquez sur le travail.

## Utilisation d'IBM Bluemix DevOps Connect pour l'intégration à IBM UrbanCode Deploy
{: #compositepipeline_devops_connect}

IBM Bluemix DevOps Connect coordonne les communications entre votre installation IBM UrbanCode Deploy sur site et {{site.data.keyword.contdelivery_short}}. Après avoir installé DevOps Connect, vous pouvez créer des intégrations que vous pouvez utiliser pour gérer des applications IBM UrbanCode Deploy avec des pipelines composites.

**Conditions préalables requises**

   * Pour enregistrer DevOps Connect, vous devez disposer d'un IBMid.

   * Assurez-vous que [Java Runtime Environment version 8 mise à jour 121 ou suivante ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://java.com/en/download/){:new_window} se trouve sur le système hôte et que la variable système PATH est définie sur son emplacement.

   * Vous avez besoin d'un jeton d'autorisation administrateur d'IBM UrbanCode Deploy.

Pour utiliser DevOps Connect pour l'intégration à IBM UrbanCode Deploy, procédez comme suit :

1. Installez DevOps Connect et utilisez-le pour intégrer votre organisation à IBM UrbanCode Deploy.

  1. Dans un pipeline composite, cliquez sur **Ajouter une application**. Dans la liste **Gérée par**, sélectionnez **IBM UrbanCode Deploy**.

  1. Affichez les étapes d'intégration. Si vous voyez une liste d'applications, cliquez d'abord sur l'icône d'information (![Icône d'information](/images/info.png)) par **Applis**, puis cliquez sur **Configurer IBM UrbanCode Deploy pour cette organisation**.

  1. Dans la fenêtre de configuration de l'intégration UrbanCode Deploy, cliquez sur **Télécharger** pour télécharger DevOps Connect. Placez le fichier JAR sur un ordinateur disposant d'un accès à IBM UrbanCode Deploy.

  1. A partir de la fenêtre, copiez le script d'installation DevOps Connect. Ce script contient la commande permettant de démarrer DevOps Connect et les informations d'identification requises pour l'identification de votre service {{site.data.keyword.contdelivery_short}}.

  1. Sur l'ordinateur où vous avez placé DevOps Connect, ouvrez un interpréteur de commandes et collez-y le script copié.

  1. Exécutez le script. DevOps Connect affiche des messages de démarrage.

1. Enregistrez DevOps Connect.

  1.  Sur l'ordinateur où vous avez placé DevOps Connect, utilisez un navigateur Web pour ouvrir le tableau de bord DevOps Connect. L'URL par défaut est https://localhost:8443. Pour modifier l'URL et en savoir plus sur les autres options de démarrage, consultez la [documentation DevOps Connect ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/urbancode/plugindoc/urbancode-sync/ibm-urbancode-sync-utility/1-2/){:new_window}.


1. Sur la page "Sign-in to IBM", saisissez votre IBMid et votre mot de passe, puis cliquez sur **Sign In**. Vous vous connectez chaque fois que vous démarrez DevOps Connect.

1. Avec DevOps Connect, utilisez le plug-in IBM UrbanCode Deploy for DevOps Connect pour créer une intégration entre votre organisation et IBM UrbanCode Deploy.

    1. Sur la page Integrations, cliquez sur **Add New**.

    1. Dans la zone **Name**, saisissez un nom pour l'intégration.

    1. Dans la liste **Integration Type**, sélectionnez **IBM UrbanCode Deploy for DevOps Connect**.

    1. Dans la zone **Server URI**, saisissez l'URL publique du serveur IBM UrbanCode Deploy ; par exemple, `https://my_UCD.example.com:8443`.

    1. Dans la zone **Authentication Token**, saisissez ou collez le jeton d'authentification généré par IBM UrbanCode Deploy.

    1. Dans la zone **Admin User Email**, saisissez votre adresse électronique.

    1. Pour confirmer que l'intégration a abouti, cliquez sur **Run Integration**. DevOps Connect se connecte à l'instance IBM UrbanCode Deploy qui est spécifiée dans la zone **Server URI**. DevOps Connect est autorisé par le jeton qui est collé dans la zone **Authentication Token**.

    1. Cliquez sur **Save**.

Si votre intégration a abouti, vous pouvez ajouter des applications IBM UrbanCode Deploy à vos pipelines composites. Pour plus d'informations, voir [Ajout d'applications à partir d'IBM UrbanCode Deploy](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_add_apps).


## Ajout d'applications à partir d'IBM UrbanCode Deploy
{: #compositepipeline_add_apps}

Si vous êtes membre d'une organisation intégrée à IBM UrbanCode Deploy via DevOps Connect, vous pouvez ajouter les applications auxquelles vous pouvez accéder dans IBM UrbanCode Deploy au pipeline composite. Pour obtenir des instructions d'installation, voir [Utilisation d'IBM Bluemix DevOps Connect pour l'intégration à IBM UrbanCode Deploy](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_devops_connect).

Si vous êtes membre d'une organisation qui est connectée à IBM UrbanCode Deploy, vous pouvez ajouter des applications UrbanCode Deploy à des pipelines composites, sélectionner les processus d'application à inclure dans le plan de déploiement et personnaliser le déploiement des applications.

1. A partir du pipeline composite, cliquez sur **Ajouter une application**.

2. Dans la liste **Gérée par**, sélectionnez **IBM UrbanCode Deploy**. Si vous avez intégré {{site.data.keyword.contdelivery_short}} récemment à IBM UrbanCode Deploy, vous devrez peut-être actualiser votre navigateur pour voir votre serveur.

3. Sélectionnez les applications à ajouter et cliquez sur **Continuer**. Tous les processus d'application qui sont disponibles pour les applications IBM UrbanCode Deploy sont affichés. Les entrées permettant d'exécuter les processus que vous avez sélectionnés sont ajoutées au plan de déploiement.

4. Sélectionnez les processus d'application à utiliser pour les applications. Utilisez les options de recherche et de filtrage pour localiser les processus.

5. Cliquez sur **Sauvegarder**. Chaque application IBM UrbanCode Deploy que vous avez sélectionnée s'affiche sous forme d'appli dans le pipeline composite.

6. Mappez les environnements des applications IBM UrbanCode Deploy aux environnements logiques du pipeline composite :

    1. A partir du menu situé en regard du nom d'un environnement logique, sélectionnez **Gérer les environnements logiques**.

    ![Sélection de l'option Gérer les environnements logiques](images/composite_logical_env.png)

    2. Pour chaque application du pipeline composite, sélectionnez les environnements que vous avez définis dans IBM UrbanCode Deploy. Les processus d'application que vous avez sélectionnés s'exécutent uniquement dans les environnements de cette application.

    3. Cliquez sur **Sauvegarder**.

    4. Répétez ces étapes pour chaque environnement logique que vous utilisez.
