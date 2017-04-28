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

# Tutoriel de bout en bout du module de démarrage BFF Basic
{: #tutorial}

Le tutoriel de bout en bout suivant couvre les étapes de création d'un projet depuis le module de démarrage BFF Basic, y compris les outils que vous devez avoir installés et, par la suite, les étapes pour exécuter le code du projet.

Vous pouvez créer un projet en utilisant la console [{{site.data.keyword.dev_console}}](#create-devex) reposant sur le Web ou le plug-in [{{site.data.keyword.dev_cli_notm}}](#create-cli) géré par commande.

## Installation des outils de développement
{: #dev_tools}

Vérifiez que vous avez installé les [outils prérequis pour le développeur![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](get_code.html#prereq-dev-tools){: new_window}.


## Création d'un projet en utilisant la console {{site.data.keyword.dev_console}}
{: #create-devex}

1. Créez un projet dans la console {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}.

	1. Dans la page de [**mise en route** ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/developer/getting-started/) de la console {{site.data.keyword.dev_console}},  cliquez sur la commande de création de projet..

		Vous pouvez également cliquer sur la commande de création de projet dans la page des projets.

	2. Sélectionnez l'option relative à BFF (Backend for Frontend puis cliquez sur **Suivant**.

	3. Sélectionnez l'option relative à Basic Backend puis cliquez sur **Suivant**.

	4. Entrez le nom de votre projet. Pour ce tutoriel, utilisez `BFFProject`.   

	5. Entrez un nom d'hôte unique. Pour ce tutoriel, utilisez `devhost` 

	6. Sélectionnez votre plateforme de langage. Pour ce tutoriel, utilisez `Node`.
   
	7. Cliquez sur **Créer**.

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

1. Assurez-vous que vous avez bien installé le plug-in [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. Dans votre invite de terminal, accédez au répertoire local de votre choix et exécutez la commande suivante.
  
	```
	bx dev create
	```
	{: codeblock}
	
3. Fournissez les valeurs suivantes, quand vous y êtes invité :

	* Sélectionnez un modèle : 3 (pour Backend for Frontend)
	* Sélectionnez un module de démarrage : 1 (pour Basic Backend)
	* Sélectionnez un langage : 1 (pour Node)
	* Entrez le nom de votre projet : `BFFProjectCLI`
	* Entrez un nom d'hôte pour votre projet : `myhost`

4. Si vous voulez ajouter des services à votre projet, répondez par l'affirmative à la question qui vous est posée puis répondez aux questions suivantes.

5. Une fois votre projet `BFFProjectCLI` correctement sauvegardé, accédez au dossier `BFFProjectCLI`.

6. Ajoutez votre propre code et exécutez le projet.
 
	1. Exécutez votre projet avec la commande suivante :

 		```
		bx dev run
		```
		{: codeblock}


## Exécution d'un projet BFF
{: #running-bff}

### Localement
{: #bff-local}

1. Compilez votre serveur :

  ```
  swift build
  ```
  {: codeblock}

2. Lancez votre application. En supposant que votre application s'appelle `MyServer`, exécutez la commande suivante :

  ```
  .build/debug/MyServer
  ```
  {: codeblock}

3. Vous pouvez exécuter la commande curl sur votre serveur, via `curl http://localhost:8080`.


### Utilisation du plug-in Bluemix
{: #using-blumix}

1. Lancez la compilation :

	```
	bx dev run
	```
	{: codeblock}

2. Vous pouvez exécuter la commande curl sur votre serveur, via :
  
	```
	curl http://localhost:8080
	```
	{: codeblock}
