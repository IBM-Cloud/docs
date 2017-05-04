---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

L'environnement d'exécution PHP dans {{site.data.keyword.Bluemix}} repose sur le pack php_buildpack.
Le pack php_buildpack fournit un environnement d'exécution complet pour les applis PHP.
{: shortdesc}

Le pack php_buildpack est utilisé dans les conditions suivantes :
* votre appli contient un fichier composer.json, ou
* votre appli contient un fichier *.php, ou
* votre appli définit une variable ${WEBDIR} dans son fichier [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) et cette variable a pour valeur un répertoire existant dans votre appli.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage PHP.  L'application de démarrage PHP est une appli PHP simple qui fournit un modèle que vous pouvez utiliser pour votre appli. Vous pouvez expérimenter cette application et effectuer des modifications puis les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix}}.  Voir [Utilisation des applications de démarrage](/docs/cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions d'environnement d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de PHP que votre application doit utiliser en utilisant le fichier composer.json. Par exemple :

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
Pour plus d'informations, voir les [liens Composer Package![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://getcomposer.org/doc/04-schema.md#package-links).

Si aucune version n'est spécifiée, la version 5.5.34 est choisie par défaut.

### Versions disponibles :
{: #available_versions}

Les versions de PHP suivantes sont disponibles dans le [pack de construction PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.10) qui est installé dans {{site.data.keyword.Bluemix}} :

* 5.5.33
* 5.5.34
* 5.6.19
* 5.6.20
* 7.0.4
* 7.0.5

Si votre application requiert une version de PHP qui n'est pas répertoriée, vous pouvez
utiliser le [pack de construction PHP](https://github.com/cloudfoundry/php-buildpack.git) externe pour
la déployer.

# rellinks
{: #rellinks notoc}
## Tutoriels et exemples
{: #samples notoc}
* [Build and deploy a REST API](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Build and deploy a mobile-friendly calorie counter ](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## general
{: #general notoc}
* [Cloud Foundry buildpack for PHP](https://github.com/cloudfoundry/php-buildpack.git)
