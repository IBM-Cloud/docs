---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Plug-in de générateur SDK
{: #sdk-cli}

Le plug-in de générateur SDK {{site.data.keyword.IBM}} peut être installé dans l'interface de ligne de commande [{{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/cli/reference/bluemix_cli/index.html).

En tant que développeur sous {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser ce plug-in pour générer des SDK depuis votre définition d'API REST conforme à la [spécification Open API ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.openapis.org/). Quand vous apportez des modifications à votre définition d'API REST, vous pouvez utiliser ce plug-in pour ne régénérer que le SDK au lieu de régénérer l'ensemble du projet.

Vous pouvez aussi voir si vos applications Cloud Foundry d'espace donné disposent de définitions d'API REST valides pour la génération SDK. Enfin, vous pouvez utiliser le plug-in de générateur SDK {{site.data.keyword.IBM_notm}} pour valider toutes définitions d'API REST afin de vous assurer qu'elles sont conformes aux exigences du générateur SDK.

Ce plug-in de générateur SDK {{site.data.keyword.IBM_notm}} vous permet d'intégrer facilement vos services de backend à votre application avec un SDK généré. Quand un changement se produit dans une API REST, vous pouvez générer à nouveau le SDK et remplacer l'ancien pour une mise à niveau transparente du SDK. Vous pouvez aussi intégrer l'interface de ligne de commande dans un pipeline DevOps et vous assurer que le SDK est toujours cohérent avec la spécification d'API chaque fois que l'application est générée.

La définition d'API REST doit être valide et hébergée sur un noeud final de serveur opérationnel de votre système. Si la définition d'API REST est hébergée, l'URL relative doit être définie dans la variable d'environnement `OPENAPI_SPEC`.


## Configuration requise
{: #prereqs}

Vérifiez que vous répondez bien aux exigences suivantes.

* Vous disposez d'un compte [{{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net)
* Vous disposez d'une définition d'API valide conforme à la spécification [Open API ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.openapis.org/)


## Installation
{: #installation}

1. [Installez l'interface de ligne de commande {{site.data.keyword.Bluemix}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://clis.ng.bluemix.net/ui/home.html).

2. [Installez le plug-in ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in).

	```
	bx plugin install sdk-gen -r Bluemix
	```
	{: codeblock}


## Commandes
{: #commands}

Utilisez les commandes ci-après pour générer un SDK, valider des fichiers de définition Open API ou répertorier les applications Cloud Foundry.


### Génération d'un SDK
{: #gen}

Utilisez `bluemix sdk generate [arguments...][command options]`.


#### Arguments
{: #gen-args}

* `NOM_APP` - nom de l'application Cloud Foundry dans votre espace actuel
* `EMPLACEMENT_DOC_OPENAPI` - URL ou chemin d'accès relatif au fichier de définition d'API REST brut JSON ou Yaml
* `NOM_SDK_GENERE` (facultatif) - nom du SDK généré


#### Options
{: #gen-options}

* `PLATEFORME` (requis)
   * `--android` - génère un SDK Android
   * `--ios` - generate an iOS Swift SDK
   * `--swift` - generate a Swift server SDK
* `--output "VOTRE_CHEMIN_RELATIF"` (facultatif) - place le SDK généré dans le répertoire qui est spécifié par `VOTRE_CHEMIN_RELATIF` (remplace le SDK existant, le cas échéant)
* `--unzip` (facultatif) - extrait le SDK généré (remplace les artefacts de SDK existants, le cas échéant)


#### Utilisation
{: #gen-usage}

Pour générer un SDK depuis une application Cloud Foundry qui s'exécute dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser le nom de l'application en tant que paramètre dans l'interface de ligne de commande de l'application. La commande suivante utilise le nom de l'application comme `Nom_SDK`.

```
bluemix sdk generate [NOM_APP] [PLATEFORME]
```
{: codeblock}

Pour générer un SDK depuis une URL dans un fichier de définition Open API ou un fichier Yaml ou JSON local, utilisez la commande suivante.

```
bluemix sdk generate [EMPLACEMENT_DOC_OPENAPI] [Nom_SDK] [Plateforme]
```
{: codeblock}


### Validation des définitions Open API
{: #validating}

Utilisez `bluemix sdk validate [argument]`.


#### Arguments
{: #val-args}

* `NOM_APP` - nom de l'application Cloud Foundry dans votre espace actuel
* `EMPLACEMENT_DOC_OPENAPI` - URL ou chemin d'accès relatif au fichier de définition d'API REST brut JSON ou Yaml


#### Utilisation
{: #val-usage}

Pour valider une spécification d'API d'une application Cloud Foundry qui s'exécute dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser le nom de l'application en tant que paramètre dans l'interface de ligne de commande de l'application.

```
bluemix sdk validate [NOM_APP]
```
{: codeblock}

Pour valider un SDK depuis l'URL dans un document de spécification d'API ou un fichier Yaml ou JSON local, utilisez la commande suivante.

```
bluemix sdk validate [EMPLACEMENT_DOC_OPENAPI]
```
{: codeblock}



### Liste des applications (Cloud Foundry)
{: #list-apps}

Utilisez `bluemix sdk list [argument][option]` pour répertorier les applications et valider les spécifications d'API. La variable d'environnement `OPENAPI_SPEC` doit être définie par rapport au chemin d'URL relatif qui héberge votre spécification.


#### Arguments
{: #list-args}

* `NOM_ESPACE` (facultatif) - nom de l'espace Cloud Foundry au sein de votre organisation actuelle dans lequel vous voulez rechercher des applications. Si aucune valeur n'est fournie, l'espace actuel est exploré.


#### Options
{: #list-options}

* `--url` (facultatif) - pour afficher une URL complète dans la définition Open API pour chaque application de la liste.


#### Utilisation
{: #list-usage}

Pour répertorier les applications de l'espace actuel, utilisez la commande suivante.

```
bluemix sdk list
```
{: codeblock}

Pour répertorier les applications de l'espace actuel et afficher L'URL de spécification d'API, utilisez la commande suivante.

```
bluemix sdk list --url
```
{: codeblock}

Pour répertorier les applications d'un espace spécifique, utilisez la commande suivante.

```
bluemix sdk list [NOM_ESPACE]
```
{: codeblock}

Pour répertorier les applications d'un espace spécifique et afficher L'URL de spécification d'API, utilisez la commande suivante.

```
bluemix sdk list [NOM_ESPACE] --url
```
{: codeblock}
