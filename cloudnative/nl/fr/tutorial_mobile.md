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

# Tutoriel de bout en bout du module de démarrage Mobile Basic
{: #tutorial}

Le tutoriel de bout en bout suivant couvre les étapes de création d'un projet depuis le module de démarrage Mobile Basic, y compris les outils que vous devez avoir installés et, par la suite, les étapes pour exécuter le projet sous Xcode et Android Studio.


## Installation des outils de développement
{: #dev_tools}

Vérifiez que vous avez installé les [outils prérequis pour le développeur![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](get_code.html#prereq-dev-tools){: new_window}.


## Création d'un projet en utilisant la console {{site.data.keyword.dev_console}}
{: #create-devex}

1. Créez un projet {{site.data.keyword.dev_console}} dans {{site.data.keyword.Bluemix}}.

   1. Dans la page de mise en route de la console {{site.data.keyword.dev_console}}, cliquez sur la commande de création de projet.

      Vous pouvez également cliquer sur la commande de création de projet dans la page des projets.

   2. Sélectionnez l'option relative à l'application mobile puis cliquez sur **Suivant**.

   3. Sélectionnez l'option relative à **Basic** puis cliquez sur **Suivant**.

   4. Entrez le nom de votre projet. Pour ce tutoriel, utilisez `MobileBasicProject`.

   5. Sélectionnez votre plateforme. Pour ce tutoriel, utilisez `Swift`.
   
   6. Cliquez sur **Créer**.

2. Facultatif : ajoutez la fonction Authentification.

   1. Cliquez sur **Ajouter** pour **Authentification** dans la page **Présentation du projet**.

      Vous pouvez aussi sélectionner les commandes de création ou d'ajout d'une fonctionnalité existante sur la page des fonctionnalités relatives à l'authentification.

   2. Entrez le nom de votre service et cliquez sur
**Créer**.
   
   3. Activez **Authentification**.
   
   4. Sélectionnez votre fournisseur d'identité et saisissez les informations requises pour le configurer. Vous pouvez activer un seul fournisseur d'identité.
   
   5. Voir la rubrique relative à la [configuration des fournisseurs d'identité} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/appid/identity-providers.html){: new_window} pour plus d'informations sur la configuration de l'authentification.

3. Facultatif : ajoutez la fonction Analyse.

   1. Cliquez sur **Ajouter** pour **Analyse** dans la page **Présentation du projet**.

      Vous pouvez aussi sélectionner les commandes de création ou d'ajout d'une fonctionnalité existante sur la page des fonctionnalités relatives à l'analyse.

   2. Entrez le nom de votre service et cliquez sur
**Créer**.
   
   3. Désactivez le **Mode démonstration** pour afficher vos données analytiques après avoir exécuté votre application.
   
   4. Voir [Initiation à {{site.data.keyword.mobileanalytics_short}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobileanalytics/index.html){: new_window} pour plus d'informations sur la configuration du service Analytics.

4. Facultatif : Ajoutez la fonctionnalité {{site.data.keyword.mobilepushshort}}.

   1. Cliquez sur **Ajouter** pour **{{site.data.keyword.mobilepushshort}}** sur la page
**Présentation du projet**.

      Vous pouvez aussi cliquer sur les commandes de création ou d'ajout d'une fonctionnalité existante sur la page des fonctionnalités relatives à {{site.data.keyword.mobilepushshort}}.

   2. Entrez le nom de votre service et cliquez sur
**Créer**.

   3. Pour iOS, [configurez Apple Push Notification Service ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Pour Android, [configurez Firebase Cloud Messaging ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.

5. Facultatif : ajoutez la fonctionnalité Données.

   1. Cliquez sur **Afficher** pour **Données** sur la page **Présentation du projet**.

      Vous pouvez également sélectionner **Créer** sur la page **Données**.
      
   2. Choisissez **{{site.data.keyword.cloudant_short_notm}}** ou **{{site.data.keyword.objectstorageshort}}**.

   3. Entrez le nom de votre service et cliquez sur
**Créer**.

   4. Voir [Initiation à {{site.data.keyword.cloudant_short_notm}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/Cloudant/index.html){: new_window} pour plus d'informations sur la configuration de {{site.data.keyword.cloudant_short_notm}}.

   5. Voir [Initiation à {{site.data.keyword.objectstorageshort}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/ObjectStorage/index.html){: new_window} pour plus d'informations sur la configuration d'{{site.data.keyword.objectstorageshort}}.

6. Générez votre code de projet.

   1. Cliquez sur  la commande relative à l'obtention du code sur la page de présentation du projet pour sélectionner votre langue.
   
      Vous pouvez également cliquer sur la page **Code**.
      
   2. Cliquez sur la commande relative à la génération Swift.
   
   3. Quand la génération du code du projet est terminée, cliquez sur la commande de téléchargement Swift pour télécharger l'archive du projet.

7. Facultatif : [mettez à jour votre projet](project_overview_page.html#update_language) pour générer un nouveau langage.


## Création d'un projet en utilisant le plug-in {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Assurez-vous que vous avez bien installé le plug-in [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. Dans votre invite de terminal, accédez au répertoire local de votre choix et exécutez la commande suivante.

	```
	bx dev create
	```
	{: codeblock}
	
3. Fournissez les valeurs suivantes, quand vous y êtes invité :

	* Sélectionnez un modèle : 2 (pour Mobile)
	* Sélectionnez un module de démarrage : 1 (pour Basic)
	* Sélectionnez une plateforme : 3 (pour iOS Swift)
	* Entrez le nom de votre projet : `MobileBasicProjectCLI`

4. Si vous voulez ajouter des services à votre projet, répondez par l'affirmative à la question qui vous est posée puis répondez aux questions suivantes.

5. Une fois votre projet `MobileBasicProjectCLI` correctement sauvegardé, accédez au dossier `MobileBasicProjectCLI/MobileBasicProjectCLI-Swift`.


## Exécution de votre projet Swift dans Xcode
{: #run_swift}

1. Extrayez le fichier `MobileBasicProject-Swift.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour examiner les étapes de configuration de votre projet.

   1. Ouvrez votre Terminal et accédez à votre dossier de projet.
   
      1. Exécutez `pod setup` si vous devez configurer votre référentiel CocoaPods.
      
      2. Exécutez `pod update` si vous devez mettre à jour les nacelles existantes.
      
      3. Exécutez `pod install` pour installer les nacelles requises pour votre projet.
      
   3. Ouvrez votre espace de travail Xcode `BasicProject.xcworkspace`.
      
3. Exécutez votre application.


## Exécution de votre projet Cordova dans Xcode
{: #run_cordova_xcode}

1. Extrayez le fichier `MobileBasicProject-Cordova.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour configurer votre projet.

   1. Ouvrez votre projet `platforms/ios` dans Xcode.
      
3. Exécutez votre application.


## Exécution de votre projet Cordova dans Android Studio
{: #run_cordova_studio}

1. Décompressez le fichier `BasicProject-Cordova.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour configurer votre projet.

   1. Ouvrez votre projet `platforms/android` dans Android Studio.
      
3. Exécutez votre application.


## Exécution de votre projet Android dans Android Studio
{: #run_android}

1. Extrayez le fichier `MobileBasicProject-Android.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour configurer votre projet.

   1. Ouvrez votre projet `BasicProject-Android` dans Android Studio.
      
3. Exécutez votre application.
