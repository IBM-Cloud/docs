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

# {{site.data.keyword.dev_cli_short}}
{: #developercli}	

Le plug-in {{site.data.keyword.dev_cli_long}} fournit une approche pilotée par commande extensible pour créer, développer et déployer un projet Web avec le plug-in `dev`. Il est idéal pour les développeurs qui souhaitent utiliser un contrôle par ligne de commande tout en développant des applications de microservice de bout en bout.

{: shortdesc}

Le plug-in {{site.data.keyword.dev_cli_notm}} utilise deux conteneurs pour faciliter la génération et le test de votre application. Le premier est le conteneur tools qui contient les utilitaires nécessaires pour générer et tester votre application. Le fichier Dockerfile pour ce conteneur est défini par le paramètre [dockerfile-tools](#command-parameters). Considérez-le comme un conteneur de développement puisqu'il contient les outils normalement utilisés pour le développement d'un environnement d'exécution particulier.

Le second conteneur est le conteneur run. La forme de ce conteneur permet un déploiement pour utilisation, dans {{site.data.keyword.Bluemix}}, par exemple. En conséquence, ce conteneur dispose généralement d'un point d'entrée défini qui démarre votre application. Quand vous choisissez d'exécuter votre application via le plug-in {{site.data.keyword.dev_cli_short}}, ce conteneur est utilisé.Le fichier Dockerfile pour ce conteneur est défini par le paramètre [dockerfile-run](#run-parameters).


## Ajout du plug-in {{site.data.keyword.dev_cli_notm}}
{: #add-cli}


### Prérequis
{: #prereq}

Quelques prérequis sont nécessaires pour explorer complètement et utiliser correctement le plug-in {{site.data.keyword.dev_cli_short}}, puisqu'il est hautement extensible et vous permet de tirer parti de technologies complémentaires gratuites.

1. Installez l'[interface de ligne de commande Cloud Foundry![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/cloudfoundry/cli#getting-started).

2. Installez l'interface de ligne de commande [{{site.data.keyword.Bluemix}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://clis.ng.bluemix.net/ui/home.html).

3. Obtenez un ID [{{site.data.keyword.Bluemix_notm}}](https://www.bluemix.net).

4. Facultatif : si vous prévoyez d'exécuter et de déboguer des applications localement, vous devez aussi installer [Docker ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.docker.com/get-docker) (requis uniquement pour les projets non mobiles).


### Installation
{: #installation}

1. Installez le plug-in [{{site.data.keyword.dev_cli_short}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in){: new_window} en exécutant la commande suivante :
 
	```
	bx plugin install dev -r Bluemix
	```
	{: codeblock}

2. 	Validez l'aboutissement de l'installation en exécutant la commande suivante :  
 
	```
	bx dev
	```
	{: codeblock}
	

### Avant de commencer
{: #before-install}
	
1. Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

	```
	bx login
	```
	{: codeblock}
	
	**Remarque :** si vos données d'identification sont rejetées, vous utilisez peut-être un ID fédéré. Procédez comme suit pour vous authentifier via un ID fédéré.
	
	<!-- 
	POINT TO BLUEMIX CLI LOG IN DOCUMENTATION !!!
	
	This link does not work in production yet --> 
	
	1. Connectez-vous à [{{site.data.keyword.iamshort}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.bluemix.net/iam/#/apikeys){: new_window}.
	2. Sélectionnez la commande  de création d'une clé d'API.
		* Entrez une description et un nom apiKey.
	3. Téléchargez votre clé apiKey.
	4. Ouvrez le fichier et copiez la valeur depuis la zone `apiKey`.
	5. Connectez-vous en utilisant la commande suivante :
	 
		```
		bx login --apikey <value>
		```
		{: codeblock}


## Commandes
{: #commands}

Utilisez les commandes décrites ci-après pour créer un projet, le déployer, le déboguer et le tester.

### Commande build
{: #build}

Vous pouvez générer votre application en utilisant la commande `build`. L'élément de configuration `build-cmd-run` est utilisé pour générer l'application. Les commandes `test`, `debug` et `run` s'exécutent toutes de la même façon que cette commande dans leur fonctionnement normal, l'exécution de cette dernière avant ces commandes n'est pas donc pas nécessaire.

Exécutez la commande suivante dans votre répertoire de projet actuel pour générer votre application :  

```
bx dev build
```
{: codeblock}


[Paramètres de la commande build](#command-parameters)


### Commande code
{: #code}

La commande `code` vous permet de télécharger le code d'application après le déploiement, afin de vous permettre de le réviser localement ou d'y apporter des modifications supplémentaires.

Exécutez la commande suivante pour télécharger le code à partir du projet spécifié.

```
bx dev code <nomProjet>
```
{: codeblock}


### Commande create
{: #create}

La commande create crée un nouveau projet, vous invitant à entrer toutes les informations requises, dont la langue, le nom du projet et le type de modèle d'application. Le projet sera créé dans le répertoire actuel. 

Pour créer un projet dans le répertoire de projet actuel et y associer des services, exécutez la commande suivante :

```
bx dev create
```
{: codeblock}


### Commande debug
{: #debug}

Vous pouvez déboguer votre application via la commande `debug`. Une génération est d'abord effectuée à partir du projet en utilisant l'élément de configuration `build-cmd-debug` comme instruction de génération. Un conteneur est ensuite démarré en exposant un ou plusieurs ports de débogage comme défini dans `container-port-map-debug`. Connectez votre outil de débogage favori au(x) port(s) puis déboguez votre application comme vous le faites normalement.

**Limite** : les projets Swift ne sont pas actuellement disponibles pour le débogage.

Exécutez la commande suivante dans votre répertoire de projet actuel pour déboguer votre application.

```
bx dev debug
```
{: codeblock}	

Pour quitter la session de débogage, utilisez `CTRL-C`.


#### Paramètres de la commande debug
{: #debug-parameters}

Les paramètres suivants, qui sont réservés à la commande `debug`, facilitent le débogage d'une application.

##### `container-port-map-debug`
{: #port-map-debug}

* Mappages de port pour le port de débogage. La première valeur est le port à utiliser dans le système d'exploitation hôte, la seconde est le port dans le conteneur (host:container).
* Syntaxe : `bx dev debug container-port-map-debug [7777:7777]`
 
##### `build-cmd-debug`
{: #build-cmd-debug}

* Utilisé pour générer du code pour DEBUG.
* Syntaxe : `bx dev debug build-cmd-debug build.command.sh`

##### `debug-cmd`
{: #debug-cmd}

* Utilisé pour déboguer le code du conteneur tools. L'utilisation de ce paramètre est facultative si le paramètre `build-cmd-debug` démarre votre application en mode débogage.
* Syntaxe : `bx dev debug debug-cmd /the/debug/command`

#### Débogage d'une application locale
{: #local-app-dev}

Pour plus d'informations sur le débogage d'une application locale, voir [Débogage d'une application locale](docs/cloudnative/dev_cli_local_debug.html#local-debug).


### Commande delete
{: #delete}

Cette commande vous permet de supprimer des projets de votre espace {{site.data.keyword.Bluemix}}.

Exécutez la commande suivante pour supprimer votre projet depuis {{site.data.keyword.Bluemix}} :

```
bx dev delete <nomProjet>
```
{: codeblock}
 

**Remarque** : les services {{site.data.keyword.Bluemix}} ne sont **pas** retirés.


### Commande help
{: #help}

Par défaut, si aucune action ou arguments ne sont transmis, ou si l'action help est fournie, cette commande affiche un texte d'aide général. L'aide générale affichée inclut une description des arguments de base ainsi qu'une liste des actions disponibles.  

Exécutez la commande suivante pour afficher des informations d'aide générales :

```
bx dev help
```
{: codeblock}


### Commande list
{: #list}

Vous pouvez répertorier tous les projets {{site.data.keyword.Bluemix_notm}} d'un espace.

Exécutez la commande suivante pour répertorier vos projets :

```
bx dev list
```
{: codeblock}


<!--
### Editing a project
{: #edit}

You can edit a project, such as changing the name, pattern or starter type, or adding services to your project. Run the following command:

```
bx dev edit
```
{: codeblock}
-->


### Commande run
{: #run}

Vous pouvez exécuter votre application via la commande `run`. Une génération est d'abord effectuée à partir du projet en utilisant l'élément de configuration `build-cmd-run` comme instruction de génération. Le conteneur run qui est ensuite démarré expose les ports comme défini dans `container-port-map`. Le paramètre `run-cmd` peut être utilisé pour invoquer l'application si le conteneur run ne contient pas de point d'entrée pour terminer cette procédure. 

Exécutez la commande suivante dans votre répertoire de projet actuel pour démarrer votre application :

```
bx dev run
```
{: codeblock}

Pour quitter la session, utilisez `CTRL-C`.


#### Paramètres de la commande run
{: #run-parameters}

Les paramètres suivants, qui sont réservés à la commande `run`, facilitent la gestion de votre application avec le conteneur run.

##### `container-name-run`
{: #container-name-run}
	
* Nom de conteneur pour le conteneur run.
* Syntaxe : `bx dev run container-name-run <nomProjet>`

##### `container-path-run`
{: #container-path-run}

* Emplacement dans le conteneur à partager à l'exécution.
* Syntaxe  : `bx dev run container-path-run [/path/to/app]`

##### `host-path-run`
{: #host-path-run}

* Emplacement sur le système hôte à partager dans le conteneur à l'exécution.
* Syntaxe : `bx dev run host-path-run [/path/to/app/bin]`

##### `dockerfile-run`
{: #dockerfile-run}

* Fichier Docker pour le conteneur run.
* Syntaxe : `bx dev run dockerfile-run [/path/to/Dockerfile.yml]`

##### `image-name-run`
{: #image-name-run}

* Image à créer depuis dockerfile-run.
* Syntaxe : `bx dev run image-name-run [/path/to/image-name]`

##### `run-cmd`
{: #run-cmd}

* Paramètre facultatif utilisé pour exécuter le code dans le conteneur run. L'utilisation de ce paramètre est facultative si votre image démarre votre application.
* Syntaxe : `bx dev run run-cmd [/the/run/command]`
	
### Commande status
{: #status}

Vous pouvez effectuer une requête relative au statut des conteneurs utilisés par {{site.data.keyword.dev_cli_short}}, comme défini par `container-name-run` et `container-name-tools`. 

Exécutez la commande suivante dans votre répertoire de projet actuel pour vérifier le statut du conteneur :

```
bx dev status
```
{: codeblock}


[Paramètres de la commande status](#command-parameters)


### Commande stop
{: #stop}

Vous pouvez arrêter un conteneur via la commande `stop`. Le paramètre `container-name` vous permet de spécifier le conteneur à arrêter. Si rien n'est spécifié, la commande stop arrête le conteneur run comme défini par `container-name-run`. 

Exécutez la commande suivante dans votre répertoire de projet actuel pour arrêter un conteneur :

```
bx dev stop
```
{: codeblock}


#### Paramètre stop supplémentaire : 
{: #stop-parameter}

##### `container-name`
{: #container-name}

* Nom de conteneur pour le conteneur tools.
* Syntaxe : `bx dev stop container-name <demo-tools>` 

### Commande Test
{: #test}

Vous pouvez tester votre application via la commande `test`. Une génération est d'abord effectuée à partir du projet en utilisant l'élément de configuration `build-cmd-run` comme instruction de génération. Le conteneur tools est ensuite utilisé pour invoquer `test-cmd` pour l'application.

Exécutez la commande suivante pour tester votre application : 

```
bx dev test
```
{: codeblock}


[Paramètres de la commande test](#command-parameters)


## Paramètres pour les commandes build, debug, run et test
{: #command-parameters}

Les paramètres suivants, qui peuvent être associés aux commandes `build|debug|run|test`, sont spécifiables via une ligne de commande et/ou en mettant à jour directement le fichier `cli-config.yml` du projet. Des paramètres supplémentaires, disponibles pour les commandes [`debug`](#debug-parameters) et [`run`](#run-parameters), sont documentés dans  leurs sections respectives.

**Remarque** : les paramètres de commande entrés dans la ligne de commande sont prioritaires sur ceux du fichier de configuration `cli-config.yml`.

##### `container-name-tools`  
{: #container-name-tools}

* Nom de conteneur pour le conteneur tools.
* Syntaxe : `bx dev <build|debug|run|test> container-name-tools [<demo-tools>]`
 
##### `host-path-tools`
{: #host-path-tools}

* Emplacement sur l'hôte à partager pour les commandes build, debug, test.
* Syntaxe : `bx dev <build|debug|run|test> host-path-tools [/path/to/build/tools]`

##### `container-path-tools`
{: #container-path-tools}

* Emplacement sur le conteneur pour les commandes build, debug, test.
* Syntaxe : `bx dev <build|debug|run|test> container-path-tools [/path/for/build]`

##### `container-port-map`
{: #container-port-map}

* Mappages de port pour le conteneur. La première valeur est le port à utiliser dans le système d'exploitation hôte, la seconde est le port dans le conteneur (host:container).
* Syntaxe : `bx dev <build|debug|run|test> container-port-map [8090:8090,9090,9090]`

##### `dockerfile-tools`
{: #dockerfile-tools}

* Fichier Docker pour le conteneur tools.
* Syntaxe : `bx dev <build|debug|run|test> dockerfile-tools [path/to/dockerfile]`

##### `image-name-tools`
{: #image-name-tools}

* Image à créer depuis dockerfile-tools.
* Syntaxe : `bx dev <build|debug|run|test> image-name-tools [path/to/image-name]`

##### `build-cmd-run`
{: #build-cmd-run}

* Commande pour générer du code pour toute utilisation sauf DEBUG.
* Syntaxe : `bx dev <build|debug|run|test> build-cmd-run [some.build.command]`

##### `test-cmd`
{: #test-cmd}

* Commande pour tester le code du conteneur tools.
* Syntaxe : `bx dev <build|debug|run|test> test-cmd [/the/test/command]`

