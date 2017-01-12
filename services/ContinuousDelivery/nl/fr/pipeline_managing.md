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
Dernière mise à jour : 17 novembre 2016
{: .last-updated}

Vous pouvez administrer, configurer et étendre les intégrations IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}.
{:shortdesc}

Pour administrer, configurer et étendre un pipeline, procédez comme suit :

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

Vous pouvez étendre les capacités de votre pipeline en configurant vos travaux afin d'utiliser les services pris en charge. Par exemple, les travaux de test peuvent exécuter des analyses de code statique et les travaux de génération peuvent globaliser des chaînes.

Pour plus d'informations sur l'extension des fonctions d'un pipeline, voir [Extension des fonctions du service {{site.data.keyword.deliverypipeline}}](./deliverypipeline_extension.html).

