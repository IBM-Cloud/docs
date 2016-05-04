---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}
*Dernière mise à jour : 16 mars 2016*

Le contexte d'exécution Python dans {{site.data.keyword.Bluemix}} repose sur le pack python_buildpack.
Le pack python_buildpack fournit un environnement d'exécution complet pour les applis Python.
{: shortdesc}

Le pack python_buildpack sera utilisé si le répertoire racine de votre appli contient un fichier requirements.txt ou setup.py.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage Python.  L'application de démarrage Python est une appli Python simple qui fournit un modèle que vous pouvez utiliser pour votre appli. Vous pouvez expérimenter cette application et effectuer des modifications puis les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix}}.  Voir [Utilisation des applications de démarrage](../../cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions de contexte d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de Python à utiliser par votre appli en définissant python-versionnumber dans le fichier runtime.txt se trouvant à la racine de votre application. Par exemple :

```
python-3.4.3
```
{: codeblock}

Si aucune version n'est spécifiée, la version 2.7.10 est choisie par défaut.

### Versions disponibles :
{: #available_versions}

Les versions de Python suivantes sont disponibles dans le [pack de construction Python](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1) qui est installé dans {{site.data.keyword.Bluemix}} :

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

Si votre application requiert une version de Python qui n'est pas répertoriée, vous pouvez
utiliser le [pack de construction Python](https://github.com/cloudfoundry/python-buildpack) externe pour
la déployer.

# rellinks
## general
* [Cloud Foundry buildpack for Python](https://github.com/cloudfoundry/python-buildpack)
