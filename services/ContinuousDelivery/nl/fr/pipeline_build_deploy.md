---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-16"
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

# Génération et déploiement
{: #deliverypipeline_build_deploy}

Le service IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} vous permet d'implémenter un processus de distribution continue et d'intégration continue reproductibles.
{:shortdesc}

Pour créer et configurer un pipeline, procédez comme suit :

## Ajout d'une étape
{: #deliverypipeline_add_stage}

1. Sur la page Pipeline, cliquez sur **Ajouter une étape**. La page Configuration d'étape s'ouvre.
2. Configurez l'étape.
  1. Sur l'onglet **Entrée**, sélectionnez une entrée pour l'étape.
  2. Sur l'onglet **Travaux**, ajoutez et configurez au moins un travail. Généralement, la première étape comporte au moins un travail de génération.
3. Cliquez sur **SAUVEGARDER**.

## Ajout d'un travail à une étape
{: #deliverypipeline_add_job}

1. Sur l'étape, cliquez sur l'icône **Configuration de l'étape**, puis sur **Configurer l'étape**.
2. Cliquez sur l'onglet **Travaux**.
3. Cliquez sur **Ajouter un travail**. Sélectionnez le type de travail à ajouter.
4. Configurez le travail.
5. Cliquez sur **SAUVEGARDER**.

![Ajout d'un travail à une étape](images/AddJob2.png)

## Exécution d'une étape
{: #deliverypipeline_run_stage}

Vous pouvez lancer manuellement une étape en cliquant sur l'icône **Exécuter une étape** sur la page Pipeline.

![Clic sur l'icône Exécuter une étape dans une étape](images/RunStage.png)

Vous pouvez également demander des générations et des déploiements à la demande depuis la page de l'historique de génération de l'une des deux façons suivantes :
* Faites glisser une génération vers la zone située sous une étape configurée.
* En regard d'une génération, cliquez sur l'icône **Envoyer à**, puis sélectionnez un espace dans lequel effectuer le déploiement.
  ![Etape d'exécution avec cette icône de génération](images/deploy_to.png)

Pour annuler une étape d'exécution, sur l'étape, cliquez sur **Afficher les journaux et l'historique**. Dans la liste de travaux, cliquez sur le numéro du travail en cours d'exécution, puis cliquez sur **ANNULER**. Vous pouvez également annuler des travaux individuellement en cliquant sur un travail, puis en cliquant sur **ANNULER** ou en cliquant sur l'icône **Arrêter** en regard d'un travail sur son étape.

## Déploiement d'une application
{: #deliverypipeline_deploy}

Un travail de déploiement correctement configuré déploie votre application sur votre cible chaque fois que le travail est exécuté. Pour exécuter manuellement un travail de déploiement, cliquez sur l'icône **Exécuter une étape** de l'étape dans laquelle se trouve le travail.

###Révisions d'entrée
Lorsque vous exécutez une étape manuellement, ou si elle s'exécute car l'étape qui la précède est terminée, l'étape en cours d'exécution sélectionne sa révision d'entrée. Généralement, la révision d'entrée est un numéro de version. Pour
sélectionner la révision d'entrée, l'étape suit les conditions ci-après :

* Si une révision spécifique est sélectionnée, utilisez-la.
* Si aucune révision n'est spécifiée, recherchez les étapes précédentes jusqu'à ce qu'une étape utilisant la même entrée soit trouvée. Recherchez et utilisez la dernière révision d'exécution réussie de cette entrée.
* Si aucune révision n'est spécifiée ni aucune autre étape, utilisez la source indiquée comme entrée, utilisez la révision la plus récente comme entrée.

**Astuce :** Vous pouvez déployer une version précédente. A l'étape qui contient la version, cliquez sur **Afficher les journaux et l'historique**. Sur la page qui s'ouvre, cliquez pour développer le numéro d'exécution, puis cliquez sur le travail de génération. Cliquez sur **ENVOYER A** et sélectionnez une cible.

###Ajout de services à des applications
Vous pouvez ajouter des services à vos applications et gérer ces services à partir de votre tableau de bord Bluemix ou de l'interface de ligne de commande Cloud Foundry. Vous pouvez également exécuter des commandes d'interface de ligne de commande Cloud Foundry dans des scripts pour les travaux de pipeline. Par exemple, vous pouvez ajouter un service à une application dans le script d'un travail de déploiement. Pour plus d'informations sur l'ajout de services, voir [Ajout d'un service à votre application](/docs/services/reqnsi.html#add_service).

## Affichage des journaux
{: #deliverypipeline_view_logs}

Vous pouvez afficher les journaux de travaux et consulter les étapes à mesure qu'elles s'exécutent sur la page Historique des étapes.

Pour afficher le journal d'un travail, cliquez sur celui-ci. Sinon, sur une étape, cliquez sur **Afficher les journaux et l'historique**.

Pour afficher le journal d'exécution d'une application déployée, cliquez sur **Afficher le journal d'exécution**.

![Zones d'une vignette d'étape dans lesquelles l'utilisateur peut cliquer pour ouvrir les journaux concernés](images/view_logs_and_history.png)

Outre les journaux des travaux, vous pouvez afficher les résultats de tests unitaires, les artefacts générés et les modifications de code pour n'importe quel travail de génération.

Vous pouvez également exécuter, annuler ou configurer une étape à partir de la page Historique des étapes. Cliquez sur **EXECUTER** pour exécuter une étape ou sur **CONFIGURER** pour configurer une étape. Pendant qu'une étape est en exécution,
vous pouvez l'annuler en cliquant sur son numéro, puis sur **Annuler**.
