---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configuration de chaînes d'outils personnalisées (expérimental)
{: #toolchains-custom}
Dernière mise à jour : 27 avril 2016
{: .last-updated}

La création d'une chaîne d'outils personnalisée peut vous aider à optimiser votre flux de travaux DevOps. Vous pouvez démarrer rapidement avec l'un des modèles
de chaîne d'outils existants ou bien personnaliser l'un des modèles afin de créer une chaîne d'outils plus adaptée avec laquelle débuter. {:shortdesc}

Vous pouvez [créer et déployer une chaîne d'outils](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window} de plusieurs manières. Ce
guide décrit les étapes de création d'une chaîne d'outils personnalisée pouvant être déployée via un bouton [Déployer dans {{site.data.keyword.Bluemix_notm}}](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window}. Après quelques étapes de configuration, vous pourrez partager sans difficulté un projet GitHub avec une chaîne d'outils déployable dans {{site.data.keyword.Bluemix_notm}}.


## Initiation
{: #toolchains_custom_gettingstarted}

Pour créer une chaîne d'outils personnalisée, nous commencerons par cloner un modèle de chaîne d'outils. Le clonage d'un modèle existant vous offre un point de départ rapide depuis lequel entamer votre personnalisation.

1. En utilisant le client Git de votre choix, entrez la commande suivante afin de cloner le modèle [Simple Toolchain](https://github.com/open-toolchain/simple-toolchain){: new_window} dans GitHub.

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 Ce modèle déploie une application Hello World élémentaire depuis un unique référentiel GitHub et inclut une chaîne d'outils simple préconfigurée pour la distribution continue, le contrôle des sources, le suivi des problèmes et l'édition en ligne.

2. (**Facultatif)** : Si vous préférez démarrer avec un modèle de chaîne d'outils plus complexe, vous pouvez commencer par cloner le modèle [Cloud-native Toolchain for Microservices](https://github.com/open-toolchain/toolchain-demo){: new_window}.

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 Ce modèle déploie un magasin en ligne composé de trois microservices, chacun étant contenu dans son propre référentiel GitHub. Une chaîne d'outils plus complexe préconfigurée pour la distribution continue, le contrôle des sources, les déploiements Blue-Green, les tests fonctionnels, le suivi des problèmes, l'édition en ligne et la messagerie, est également incluse.

Quel que soit le modèle sélectionné, les directives décrites dans ce guide pour la création d'une chaîne d'outils personnalisée seront similaires.

Après avoir cloné le modèle, vous disposerez d'un référentiel GitHub élémentaire comportant un fichier *Readme* et un répertoire `.bluemix` contenant tous les fichiers de configuration requis pour le fonctionnement de votre chaîne d'outils. Au minimum, le répertoire `.bluemix` doit contenir les éléments suivants :

* toolchain.yml
* deploy.json
* pipeline.yml

Chacun de ces fichiers est décrit dans les sections suivantes, ainsi que diverses configurations supplémentaires devant être ajoutées avec l'évolution de votre chaîne d'outils.

## Présentation des fichiers de configuration
{: #toolchains_custom_config_files}

Les fichiers de configuration de modèle de chaîne d'outils sont composés essentiellement de fichiers au format YAML.
Chaque fichier contient des métadonnées décrivant différents aspects de la chaîne d'outils. Ceci inclut une description générale de la chaîne d'outils, les référentiels GitHub à inclure, des informations sur la façon dont le code doit être construit et sur l'emplacement où il doit être déployé et des informations de configuration pour les divers outils que vous désirez inclure dans la chaîne d'outils.
Au fur et à mesure que votre chaîne d'outils gagne en complexité, il en va de même pour les fichiers de configuration. Il est important que les fichiers conservent un format correct afin de réduire le risque d'introduction d'erreurs.

Quelques recommandations à garder à l'esprit lors de l'utilisation d'un fichier YAML :

* Les tabulations ne sont pas autorisées. Vous ne devez utiliser que des espaces.
* Toutes les propriétés et les listes doivent figurer avec un retrait d'un ou de plusieurs espaces.
* Toutes les clés et les propriétés sont sensibles à la casse.

Pour vérifier votre travail, vous pouvez utiliser un validateur YAML simple comme [YAML Parser](http://wiki.ess3.net/yaml/){: new_window} pour éviter de telles erreurs.

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

Le fichier `toolchain.yml` est le coeur de la chaîne d'outils. Les détails de votre chaîne d'outils, y-compris des référentiels où les
intégrer et des services à inclure, sont tous décrits dans ce fichier. Pour clarifier son contenu, il peut être décomposé en plusieurs sections.

1\. **Informations de présentation de la chaîne d'outils :**

 Cette section fournit des informations simples sur la chaîne d'outils qui sont présentées à l'utilisateur sur la page de création de la chaîne d'outils. Vous devriez inclure le nom de votre chaîne d'outils, ainsi qu'une description expliquant son objet ou son action une fois déployée. Une image peut également être incluse pour afficher un logo ou une représentation visuelle de votre chaîne d'outils.

 Outre la présentation de votre chaîne d'outils, cette section comporte également une clé nommé `required` qui définit les intégrations d'outils pouvant être configurées au moment de la création de la chaîne d'outils sur la page à cet effet. En permettant de configurer un outil au moment de la création, vous pouvez créer une chaîne d'outils pouvant facilement être réutilisée ou réorientée. Pour chaque outil pouvant être configuré sur la page de création de la chaîne d'outils, ajoutez la clé parente de l'outil telle que définie dans le fichier `toolchain.yml` en tant que propriété de la clé `required`.

 Le fragment ci-dessous est un exemple de cette section :

 ```
 ---
 name: "Simple Toolchain"
 description: "This Hello World application uses Node.js and includes a toolchain that is preconfigured for continuous delivery, source control, issue tracking, and
online editing.\n\nTo get started, click **Create**."
 version: 0.1
 # Generate base64 representation of image at http://www.askapache.com/online-tools/base64-image-converter/
 image: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAA...
 required:
  - deploy
  - hello-world-repo
  ```
 {: codeblock}

 **Remarque :** Les images doivent d'abord être converties en leur représentation en base 64 à l'aide d'un outil tel que [AskApache](http://www.askapache.com/online-tools/base64-image-converter/).

2\. **Définitions de référentiel GitHub :**

 Une chaîne d'outils peut assurer une distribution continue pour un nombre quelconque de référentiels GitHub. Cette section du fichier `toolchain.yml` est celle où chaque référentiel doit être défini.

 Pour commencer, pour chaque référentiel GitHub qui sera ajouté à la chaîne d'outils, ajoutez une clé parente représentant le nom de votre référentiel GitHub avec les propriétés suivantes :

| Elément | Clé/Propriété | Valeur | Description |
|------|--------------|-------|-------------|
| repo-name | clé |  | Nom référentiel |
| service_id | propriété | <`githubpublic` , `githubprivate`> | Type de référentiel GitHub |
| parameters: | clé |  |  |
| repo_name | propriété |  | **COMMENTAIRE :  comment ceci doit être défini** |
| repo_url | propriété |  | URL du référentiel GitHub |
| type | propriété | <`new` , `fork` , `clone` , `link`> | Comment le référentiel doit être créé |
| has_issues | propriété | <`true` , `false`> | Utiliser des problèmes GitHub |

 **Remarque :** Si vous définissez plusieurs référentiels et les configurez avec `has_issues: true`, une instance unique de
dispositif de suivi GitHub Issue sera ajoutée à la chaîne d'outils pour suivi des problèmes de tous les référentiels pour lesquels `true` a
été
défini.

 Le fragment ci-dessous est un exemple de cette section :

 ```
 # Github repos
 hello-world-repo:
   service_id: githubpublic
   parameters:
 	repo_name: "hello-world-{{name}}"
 	repo_url: https://github.com/open-toolchain/node-hello-world
 	type: clone
 	has_issues: true
 ```
 {: codeblock}

3\. **Informations sur le pipeline :**

 La distribution continue est rendue possible avec le pipeline. Cette section décrit les informations de configuration utilisées pour construire et
déployer le code dans chacun de vos référentiels GitHub.

 Pour commencer, pour chaque référentiel GitHub défini dans votre chaîne d'outils, ajoutez une clé parente représentant le nom de son pipeline. Il est souhaitable de dériver cette clé à partir du nom de votre référentiel. Ajoutez les propriétés suivantes :

| Elément | Clé/Propriété | Valeur | Description |
|------|--------------|-------|-------------|
| pipeline-name | clé |  | Nom du pipeline |
| service_id | propriété | <`pipeline`> | Nom du service à utiliser |
| paramètres  | clé |  |  |
| name | propriété | <`nom_référentiel`> | Identique au nom défini dans la section #Github repos pour |
| ui-pipeline | propriété | <`true` , `false`> |  |
| configuration | clé |  |  |
| content | propriété | <`$file(pipeline.yml)`> | Fichier contenant votre définition du pipeline |
| env | clé |  |  |
| REPO_NAME | clé | <`clé-nom-référentiel`> | Nom identique à votre clé parente de référentiel GitHub |
| CF_APP_NAME |  propriété | <`"{{deploy.parameters.repo-name-key}}"`> | Nom utilisé par Cloud Foundry. Doit inclure votre nom de clé parente de référentiel GitHub |
| PROD_SPACE_NAME | propriété | <`"{{deploy.parameters.prod-space}}"`> | Nom de l'espace {{site.data.keyword.Bluemix_notm}} où effectuer le déploiement |
| PROD_ORG_NAME | propriété | <`"{{deploy.parameters.prod-organization}}"`> | Nom de l'organisation
{{site.data.keyword.Bluemix_notm}} dans laquelle effectuer le déploiement |
| PROD_REGION_ID | propriété | <`"{{deploy.parameters.prod-region}}"`> | Nom de la région {{site.data.keyword.Bluemix_notm}} dans laquelle effectuer le déploiement |
| execute | propriété | <`true` , `false`> | Lancer le pipeline après la création |
| services | propriété | <`clé-nom-référentiel`> |  Clé parente du référentiel GitHub |
| hidden | propriété | <`[form, description]`> |  |

 Les informations concernant la création d'un fichier `pipeline.yml` figurent dans une [section ultérieure.](#toolchains_custom_pipeline_yml)

 Le fragment ci-dessous est un exemple de cette section :

 ```
 # Pipelines
 hello-world-build:
   service_id: pipeline
   parameters:
 	name: "hello-world-{{name}}"
 	ui-pipeline: true
 	configuration:
 	 content: $file(hello-world.pipeline.yml)
 	 env:
 	  HELLO_WORLD_REPO: "hello-world-repo"
 	  CF_APP_NAME: "{{deploy.parameters.hello-world-name}}"
 	  PROD_SPACE_NAME: "{{deploy.parameters.prod-space}}"
 	  PROD_ORG_NAME: "{{deploy.parameters.prod-organization}}"
 	  PROD_REGION_ID: "{{deploy.parameters.prod-region}}"
 	 execute: true
 	services: ["hello-world-repo"]
   hidden: [form, description]
 ```
 {: codeblock}

4\. **Détails du déploiement :**

 Dans le cadre du processus de distribution continue, une chaîne d'outils peut être configurée afin de déployer votre application dans n'importe quelle région, organisation ou espace {{site.data.keyword.Bluemix_notm}} auquel a également accès l'utilisateur qui déploie la chaîne d'outils. Vous pouvez sélectionner spécifiquement où déployer votre application sur la page de création de la chaîne d'outils.  

 ![Paramètres de configuration de Delivery Pipeline](images/deploy_configuration.png)

 Cette section du fichier `toolchain.yml` définit les étapes de pipeline disponibles pour configuration depuis la page de création de la chaîne d'outils.

 Pour commencer, la clé parente `deploy` est utilisée pour identifier les propriétés de configuration du déploiement.
Le reste de la section est constitué des propriétés suivantes :

| Elément | Clé/Propriété | Valeur | Description |
|------|--------------|-------|-------------|
| deploy | clé |  | Nom de la section du déploiement |
| schema | propriété | <`deploy.json`> | Fichier qui définit l'agencement de l'interface graphique pour configuration des informations de déploiement |
| service-category | propriété | <`pipeline`> | Service qui utilisera les configurations de déploiement |
| parameters | clé |  |  |
| prod-region | propriété | <`"{{region}}"`> | Définit la région {{site.data.keyword.Bluemix_notm}} pour la phase de production |
| prod-organization | propriété | <`"{{organization}}"`> | Définit l'organisation {{site.data.keyword.Bluemix_notm}} pour la phase de production |
| prod-space | propriété | <`prod`> | Définit l'espace {{site.data.keyword.Bluemix_notm}} pour la phase de production |
| github-repo-name | propriété | <`"{{repo-name-key.parameters.repo_name}}"`> | Variable servant à transférer le nom de référentiel GitHub à la page de création de la chaîne d'outils |

 Les informations concernant la création d'un fichier `deploy.json` figurent dans une [section ultérieure.](#toolchains_custom_deploy_json)

 L'exemple ci-après définit une seule phase avec déploiement dans un environnement de production.

 ```
 #Deployment
 deploy:
   schema: deploy.json
   service-category: pipeline
   parameters:
 	prod-region: "{{region}}"
 	prod-organization: "{{organization}}"
 	prod-space: prod
 	hello-world-name: "{{hello-world-repo.parameters.repo_name}}"
 ```
 {: codeblock}

 Cet exemple de code peut être utilisé essentiellement tel quel et ne requiert qu'une modification mineure. Pour personnaliser cette section, `github-repo-name` doit être mis à jour pour correspondre à votre nom de référentiel. Les informations du fichier [`deploy.json`](#toolchains_custom_deploy_json) devront également être mises à jour.

 Pour créer un pipeline plus complexe incluant une phase dev, QA et Prod, les propriétés suivantes peuvent être implantées sous la clé `parameters`.

 ```
   parameters:
 	dev-region: "{{region}}"
 	qa-region: "{{region}}"
 	prod-region: "{{region}}"
 	dev-organization: "{{organization}}"
 	qa-organization: "{{organization}}"
 	prod-organization: "{{organization}}"
 	dev-space: dev
 	qa-space: qa
 	prod-space: prod
 ```
 {: codeblock}

5\. **Configurations d'outils**

 Après avoir configuré les composants cruciaux de votre chaîne d'outils, vous pouvez commencer à inclure d'autres intégrations d'outils destinés à ajouter des fonctionnalités et à augmenter l'utilité de votre chaîne d'outils.  Tous les outils comportent une entrée devant être ajoutée au fichier `toolchain.yml` et certains nécessitent également un fichier de configuration YAML distinct devant être créé dans le répertoire `.bluemix`.

 * **Slack**

	toolchain.yml
	```
	messaging:
	  service_id: slack
	  include: slack.yml
	```
	{: codeblock}
	
	slack.yml
	```
	---
	parameters:
	  api_token: ""
	  channel_name: ""
	```
	{: codeblock}
	
 * **Sauce Labs**

	toolchain.yml
	```
	test:
	  service_id: saucelabs
	  include: saucelabs.yml
	```
	{: codeblock}
	
	saucelabs.yml
	```
	---
	parameters:
	  username: ""
	  key: ""
	```
	{: codeblock}
	
 * **PagerDuty**

	toolchain.yml
	```
	alerting:
	  service_id: pagerduty
	  include: pagerduty.yml
	```
	{: codeblock}

	pagerduty.yml
	```
	---
	parameters:
	  site_name: ""
	  api_key: ""
	  service_name: ""
	  user_email: ""
	  user_phone: ""
	```
	{: codeblock}
	
 * **Eclipse Orion Web IDE**

	toolchain.yml
	```
	webide:
	  service_id: orion
	```
	{: codeblock}


## pipeline.yml
{: #toolchains_custom_pipeline_yml}

Le fichier `pipeline.yml` contient toutes les informations de configuration des phases de votre pipeline. Le fichier `pipeline.yml` peut être créé de deux manières différentes.

1. Vous pouvez créer le fichier `pipeline.yml` manuellement. Les instructions et la syntaxe pour la création du fichier
`pipeline.yml` figurent sur le site [Sharing text-based pipelines in DevOps Services sample projects](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}.

2. Vous pouvez générer le fichier `pipeline.yml` à partir d'un projet DevOps Services existant. Pour ce faire, procédez comme suit.
	
	1. Créez un nouveau [projet DevOps Services](https://hub.jazz.net/create){: new_window}.
	
	2. Ouvrez le projet et cliquez sur **Générer & Déployer**
	
	3. Configurez toutes les phases requises pour votre pipeline.
	
	4. Dans la barre d'adresse de votre navigateur, ajoutez `/yaml` à l'URL du projet et appuyez sur la touche Entrée.
	
	5. Enregistrez le fichier `pipeline.yml` résultant dans le répertoire `.bluemix` de votre référentiel GitHub.

Si votre chaîne d'outils contient plusieurs pipelines, attribuez un nom unique à chaque fichier `pipeline.yml`.

Ci-dessous figure un exemple de fichier `pipeline.yml` :

```
---
stages:
- name: BUILD
  inputs:
  - type: git
	branch: master
	service: ${HELLO_WORLD_REPO}
  triggers:
  - type: commit
  jobs:
  - name: Build
	type: builder
- name: DEPLOY
  inputs:
  - type: job
	stage: BUILD
	job: Build
  triggers:
  - type: stage
  properties:
  - name: CF_APP_NAME
	value: undefined
	type: text
  - name: APP_URL
	value: undefined
	type: text
  jobs:
  - name: Deploy
	type: deployer
	target:
	  region_id: ${PROD_REGION_ID}
	  organization: ${PROD_ORG_NAME}
	  space: ${PROD_SPACE_NAME}
	  application: ${CF_APP_NAME}
	script: |
	  #!/bin/bash
	  # Push app
	  export CF_APP_NAME="$CF_APP"
	  cf push "${CF_APP_NAME}"
	  export APP_URL=http://$(cf app $CF_APP_NAME | grep urls: | awk '{print $2}')
	  # View logs
	  #cf logs "${CF_APP_NAME}" --recent
```
{: codeblock}		


## deploy.json
{: #toolchains_custom_deploy_json}

Sur la page de création de la chaîne d'outils, lorsque Delivery Pipeline est sélectionné dans la section Intégrations configurables, cette section est développée et affiche les éléments suivants que vous pouvez configurer pour l'outil concerné :

	* Nom des applications
	* Région, organisation et espace dans lesquels vos phases de pipeline seront déployées.

![Paramètres de configuration de Delivery Pipeline](images/deploy_configuration.png)

L'agencement de cette section dans l'interface utilisateur est défini par le schéma `deploy.json`.

Dans le schéma, les propriétés suivantes doivent être mises à jour afin de concorder avec les informations de votre application :

	* Titre
	* Description
	* LongDescription
	* Toutes les instances de `hello-world-name` et les informations associées doivent être mises à jour afin de concorder avec celles de votre application.

Ci-dessous figure un exemple de fichier `deploy.json` :

```
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "Hello World Deploy Stage",
    "description": "hello-world simple toolchain",
    "longDescription": "The Delivery Pipeline for Devops Services allows you to automate your continuous deployment setup hello-world.",
    "type": "object",
    "properties": {
        "prod-region": {
            "description": "The bluemix region",
            "type": "string"
        },
        "prod-organization": {
            "description": "The bluemix org",
            "type": "string"
        },
       "prod-space": {
            "description": "The bluemix space",
            "type": "string"
        },
       "hello-world-name": {
            "description": "hello world app name",
            "type": "string"
        }
    },
    "required": ["prod-region", "prod-organization", "prod-space", "hello-world-name"],
    "form": [
       {
          "type": "validator",
          "url": "/devops/setup/bm-helper/helper.html"
       },        
        {
          "type": "text",
          "readonly": false,
          "title": "Hello World App Name",
          "key": "hello-world-name"
        },
        {
            "type": "table",
            "columnCount": 4,
            "widths": ["15%", "28%", "28%", "28%"],
            "items": [
                {
                  "type": "label",
                  "title": ""
                },
                {
                  "type": "label",
                  "title": "Region"
                },
                {
                  "type": "label",
                  "title": "Organization"
                },
                {
                  "type": "label",
                  "title": "Space"
                },
                {
                  "type": "label",
                  "title": "Prod Stage"
                },
                {
                  "type": "select",
                  "key": "prod-region"
                },
                {
                  "type": "select",
                  "key": "prod-organization"
                },
                {
                  "type": "select",
                  "key": "prod-space",
                  "readonly": false
                }
            ]
        }
    ]
}
```
{: codeblock}
