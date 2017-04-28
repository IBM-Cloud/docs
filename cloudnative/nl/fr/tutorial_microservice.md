---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Tutoriel de bout en bout du module de démarrage Microservice Basic
{: #tutorial}

Le tutoriel de bout en bout suivant couvre les étapes de création d'un projet depuis le module de démarrage Microservice Basic, ce qui inclut l'installation des outils prérequis et la procédure d'exécution du code de projet.

Vous pouvez créer un projet en utilisant la console [{{site.data.keyword.dev_console}}](#create-devex) reposant sur le Web ou le plug-in [{{site.data.keyword.dev_cli_notm}}](#create-cli) géré par commande.

## Installation des outils de développement
{: #dev_tools}

Prenez soin d'installer les [outils prérequis pour le développeur![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](get_code.html#prereq-dev-tools){: new_window}.


## Création d'un projet en utilisant la console {{site.data.keyword.dev_console}}
{: #create-devex}

1. Créez un projet dans la console {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}.

	1. Dans la page de [**mise en route** ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/developer/getting-started/) de la console {{site.data.keyword.dev_console}},  cliquez sur la commande de création de projet..

		Vous pouvez également cliquer sur la commande de création de projet dans la page des projets.

	2. Sélectionnez l'option relative au microservice puis cliquez sur **Suivant**.

	3. Sélectionnez l'option relative à **Basic** puis cliquez sur **Suivant**.

	4. Entrez le nom de votre projet. Pour ce tutoriel, utilisez `MicroserviceProject`.   

	5. Entrez un nom d'hôte unique. Pour ce tutoriel, utilisez `devhost` 
   
	6. Cliquez sur **Créer**.

2. Facultatif : ajoutez la fonctionnalité Données.

	1. Cliquez sur **Afficher** pour **Données** sur la page **Présentation du projet**.

      Vous pouvez aussi sélectionner les commandes de création ou d'ajout d'une fonctionnalité existante sur la page des fonctionnalités relatives aux données.

   2. Entrez le nom de votre service et cliquez sur
**Créer**.

3. Générez votre code de projet :

	1. Cliquez sur  la commande relative à l'obtention du code sur la page de présentation du projet pour sélectionner votre langue.
   
		Vous pouvez également cliquer sur la page **Code**.
      
	2. Cliquez sur la commande de génération de code.
   
	3. Lorsque la génération du code du projet est terminée, cliquez sur **Télécharger le code** pour télécharger l'archive du projet.

4. Commencez à utiliser le projet que vous avez téléchargé :

	1. Développez le fichier archivé.
	
	2. Accédez au nouveau répertoire de projet.
	
	3. Utilisez la console {{site.data.keyword.dev_cli_notm}} pour poursuivre.

5. Facultatif : [mettez à jour votre projet](project_overview_page.html#update_language) pour générer un nouveau langage.


## Création d'un projet en utilisant le plug-in {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Prenez soin d'installer le plug-in [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. Dans votre invite de terminal, accédez au répertoire local de votre choix et exécutez la commande suivante.
  
	```
	bx dev create
	```
	{: codeblock}

3. Fournissez les valeurs suivantes, quand vous y êtes invité :

	* Sélectionnez un modèle : 4 (pour Microservices)
	* Sélectionnez un module de démarrage : 1 (pour Basic)
	* Sélectionnez une plateforme : 3 (pour Java)
	* Entrez le nom de votre projet : `MicroserviceProjectCLI`

4. Si vous voulez ajouter des services à votre projet, répondez par l'affirmative à la question qui vous est posée puis répondez aux questions suivantes.

5. Une fois votre projet `MicroserviceProjectCLI` correctement sauvegardé, accédez au dossier `MicroserviceProjectCLI`.

6. Vous pouvez ajouter votre propre code et générer ou exécuter le projet.
 
 
## Exécution du projet en utilisant le plug-in {{site.data.keyword.dev_cli_notm}}
{: #running-dev-plugin}

1. Pour générer le projet dans votre répertoire de projet actuel, entrez la commande suivante : 

	```
	bx dev build
	```     
	{: codeblock}

2. Pour générer et exécuter le projet dans votre répertoire de projet actuel, entrez la commande suivante :

	```
	bx dev run
	```
	{: codeblock}	

3. Vous pouvez accéder à l'application en utilisant `curl` sur votre serveur :

	```
	curl http://localhost:8080	
	```
	{: codeblock}
