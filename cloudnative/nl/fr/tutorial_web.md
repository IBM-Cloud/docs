---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Tutoriel de bout en bout du module de démarrage Web Basic
{: #tutorial}

Le tutoriel de bout en bout suivant couvre les étapes de création d'un projet depuis le module de démarrage Web Basic, y compris les outils que vous devez avoir installés et, par la suite, les étapes pour exécuter le code du projet.

## Installation des outils de développement
{: #dev_tools}

Vérifiez que vous avez installé les [outils prérequis pour le développeur![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](get_code.html#prereq-dev-tools){: new_window}.


## Création d'un projet en utilisant la console {{site.data.keyword.dev_console}}
{: #create-devex}

1. Créez un projet dans la console {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}.

	1. Dans la page de mise en route de la console {{site.data.keyword.dev_console}}, cliquez sur la commande de création de projet.

		Vous pouvez également cliquer sur la commande de création de projet dans la page des projets.

	2. Sélectionnez l'option relative à l'application Web puis cliquez sur **Suivant**.

	3. Sélectionnez l'option relative à **Basic Web** puis cliquez sur **Suivant**.

	4. Entrez le nom de votre projet. Pour ce tutoriel, utilisez `WebBasicProject`.   

	5. Entrez un nom d'hôte. Pour ce tutoriel, utilisez `devhost` 

	6. Sélectionnez votre plateforme de langage. Pour ce tutoriel, utilisez `Swift`.
   
	7. Cliquez sur **Créer**.

2. Facultatif : ajoutez la fonctionnalité Données.

	1. Cliquez sur **Afficher** pour **Données** sur la page **Présentation du projet**.

      Vous pouvez aussi sélectionner les commandes de création ou d'ajout d'une fonctionnalité existante sur la page des fonctionnalités relatives aux données.

   2. Entrez le nom de votre service et cliquez sur
**Créer**.


3. Générez votre code de projet.

	1. Cliquez sur  la commande relative à l'obtention du code sur la page de présentation du projet pour sélectionner votre langue.
   
		Vous pouvez également cliquer sur la page **Code**.
      
	2. Cliquez sur la commande de génération de code.
   
	3. Lorsque la génération du code du projet est terminée, cliquez sur **Télécharger le code** pour télécharger l'archive du projet.

4. Facultatif : [mettez à jour votre projet](project_overview_page.html#update_language) pour générer un nouveau langage.


## Création d'un projet en utilisant le plug-in {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Assurez-vous que vous avez bien installé le plug-in [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. Dans votre invite de terminal, accédez au répertoire local de votre choix et exécutez la commande suivante.
  
	```
	bx dev create
	```
	{: codeblock}


3. Fournissez les valeurs suivantes, quand vous y êtes invité :

	* Sélectionnez un modèle : 1 (pour Web)
	* Sélectionnez un module de démarrage : 1 (pour Basic Web)
	* Sélectionnez un langage : 2 (pour Swift)
	* Entrez le nom de votre projet : `WebBasicProjectCLI`
	* Entrez un nom d'hôte pour votre projet : `myhost`

4. Si vous voulez ajouter des services à votre projet, répondez par l'affirmative à la question qui vous est posée puis répondez aux questions suivantes.

5. Une fois votre projet `WebBasicProjectCLI` correctement sauvegardé, accédez au dossier `WebBasicProjectCLI`.

6. Ajoutez votre propre code, générez le projet ou exécutez-le.
 
	1. Générez le projet avec la commande suivante :
   
		```
 		bx dev build
 		```     
		{: codeblock}

	2. Exécutez le projet avec la commande suivante :
 
		```
		bx dev run
		```
		{: codeblock}


## Exécution d'un projet Web
{: #run}

### Localement
{: #local notoc}

1. Installez vos dépendances de noeud :

  ```
  npm install
  ```
  {: codeblock}

2. Incluez votre code frontend dans un module :

  ```
  node_modules/.bin/gulp
  ```
  {: codeblock}

3. Compilez votre serveur :

  ```
  swift build
  ```
  {: codeblock}

4. Exécutez votre application :

  ```
  .build/debug/WebBasicProjectCLI
  ```
  {: codeblock}

5. Accédez, dans votre navigateur, à l'URL `http://localhost:8080`.


### Utilisation du plug-in {{site.data.keyword.dev_cli_short}}
{: #dev notoc}

1. Installez les dépendances de noeud :

  ```
  npm install
  ```
  {: codeblock}

2. Incluez votre code frontend dans un module :

  ```
  gulp
  ```
  {: codeblock}

3. Lancez la compilation :

  ```
  bx dev run
  ```
  {: codeblock}

4. Accédez, dans votre navigateur, à l'URL `http://localhost:8080`.


## Exécution de votre projet dans Xcode
{: #Xcode}

1. Créez un projet Xcode.

	Avant de pouvoir développer dans Xcode, vous devez utiliser le gestionnaire de package Swift pour générer un projet Xcode.
	
	```
	swift project generate-xcodeproj
	```
	{: codeblock}

2. Rendez exécutable votre cible active :

	Ouvrez votre projet sous Xcode et assurez-vous que votre cible active est exécutable. Vous pouvez maintenir enfoncée la touche d'option tout en cliquant sur le menu déroulant pour sélectionner l'exécutable actif voulu.

3. Appuyez sur **run**.

4. Accédez, dans votre navigateur, à l'URL `http://localhost:8080`.

