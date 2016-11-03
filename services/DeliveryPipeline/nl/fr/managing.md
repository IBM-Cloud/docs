---

copyright:
  years: 2016

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

# Gestion des pipelines
{: #deliverypipeline_managing}
Dernière mise à jour : 30 août 2016
{: .last-updated}

Vous pouvez administrer, configurer et étendre les intégrations IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}.
{:shortdesc}

Pour administrer, configurer et étendre un pipeline, procédez comme suit :

## Contrôle d'accès
{: #deliverypipeline_access}

Vous pouvez restreindre les personnes habilitées à exécuter des étapes ou à modifier un pipeline. Pour cela, accédez à la page Paramètres de pipeline en cliquant sur l'icône **Configuration de l'étape** sur la page Pipeline : toutes les étapes.

![Icône représentant un engrenage dans les paramètres de pipeline](./images/pipeline_settings.png)

## Propriétés et ressources d'environnement
{: #deliverypipeline_envprop}

Vous pouvez utiliser des propriétés d'environnement et des ressources pré-installées pour interagir avec le service {{site.data.keyword.deliverypipeline}}. Par exemple, vous souhaiterez peut-être les intégrer dans un script de travail oui une commande de test. Pour plus d'informations, voir [Propriétés et ressources d'environnement pour le service {{site.data.keyword.deliverypipeline}}](./deploy_var.html).

Vous pouvez ajouter vos propres propriétés d'environnement à une étape à partir de son onglet **PROPRIETES D'ENVIRONNEMENT**. Des propriétés d'environnement sont disponibles pour chaque travail d'une étape.

Vous pouvez ajouter quatre types de propriété à partir de votre onglet Propriétés d'environnement :
* **Texte** : Clé de propriété avec une valeur monoligne.
* **Zone de texte** : Clé de propriété avec une valeur multiligne.
* **Sécurisé** : Clé de propriété avec une valeur monoligne. La valeur apparaît sous la forme d'astérisques.
* **Propriétés** : Fichier dans le référentiel du projet. Ce fichier peut contenir plusieurs propriétés. Chaque propriété doit figurer sur sa propre ligne. Pour distinguer des paires clé-valeur, utilisez le signe égal (=).

## Extension des fonctions de votre pipeline
{: #deliverypipeline_extend}

Vous pouvez étendre les fonctions du pipeline Build & Deploy en configurant vos travaux pour qu'ils utilisent des services pris en charge. Par exemple, les travaux de test peuvent exécuter des analyses de code statique et les travaux de génération peuvent globaliser des chaînes.

Pour plus d'informations sur l'extension des fonctions d'un pipeline, voir [Extension des fonctions du service {{site.data.keyword.deliverypipeline}}](./deliverypipeline_extension.html).

<!-- [1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
[2]: https://www.ng.bluemix.net/docs/#services/DeliveryPipeline/index.html#getstartwithCD
[3]: http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push
[4]: https://console.ng.bluemix.net/?ace_base=true/#/pricing/cloudOEPaneId=pricing
[5]: ./images/open_logs.png
[6]: #manifests
[7]: ./images/runbar-annotated-dark.png
[8]: ./images/input_tab_only_execute.png
[9]: ./images/deploy_to.png
[10]: ./images/view_logs_and_history.png
[11]: ./images/play_button.png
[12]: ./images/basicAnimate.gif
[13]: ./images/AddStage.png
[14]: ./images/AddJob.png
[15]: ./images/jobs.png
[16]: ./images/RunStage.png
[17]: https://www.ng.bluemix.net/docs/starters/container_pipeline.html#container_pipeline
[18]: ../../../tutorials/basicbuild
[19]: #add_stage
[20]: #add_job
[21]: ../deploy_ext
[22]: ./images/pipeline_settings_icon.png
[23]: ./images/pipeline_settings.png
[24]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[25]: ../deploy_var
[26]: ./images/click_stage_run_number.png
[27]: ./images/diagram.jpg -->
