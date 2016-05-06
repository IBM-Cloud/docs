---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}
*Dernière mise à jour : 16 mars 2016*

Le contexte d'exécution PHP dans {{site.data.keyword.Bluemix}} repose sur le pack php_buildpack.
Le pack php_buildpack fournit un environnement d'exécution complet pour les applis PHP.
{: shortdesc}

Le pack php_buildpack est utilisé dans les conditions suivantes :
* votre appli contient un fichier composer.json, ou
* votre appli contient un fichier *.php, ou
* votre appli définit une variable ${WEBDIR} dans son fichier [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) et cette variable a pour valeur un répertoire existant dans votre appli.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage PHP.  L'application de démarrage PHP est une appli PHP simple qui fournit un modèle que vous pouvez utiliser pour votre appli. Vous pouvez expérimenter cette application et effectuer des modifications puis les envoyer par commande push vers l'environnement {site.data.keyword.Bluemix}}.  Voir [Utilisation des applications de démarrage](../../cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions de contexte d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de PHP que votre application doit utiliser en utilisant le fichier composer.json. Par exemple :

```
{
    "version": "1.5"
}
```
{: codeblock}
Pour plus
d'informations, voir [Composer
Platform packages](https://getcomposer.org/doc/02-libraries.md#platform-packages).

Si aucune version n'est indiquée, la version 5.5.30 est choisie par défaut.

### Versions disponibles :
{: #available_versions}

Les versions de PHP suivantes sont disponibles dans le [pack de construction PHP](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5) qui est installé dans {{site.data.keyword.Bluemix}} :

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.14

Si votre application requiert une version de PHP qui n'est pas répertoriée, vous pouvez
utiliser le [pack de construction PHP](https://github.com/cloudfoundry/php-buildpack.git) externe pour
la déployer.

# rellinks
## Exemples
* [Build and deploy a REST API](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Build and deploy a mobile-friendly calorie counter ](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## general
* [Cloud Foundry buildpack for PHP](https://github.com/cloudfoundry/php-buildpack.git)
