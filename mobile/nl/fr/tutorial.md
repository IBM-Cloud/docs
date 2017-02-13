---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Tutoriel de bout en bout du Module de démarrage pour le code Basic
{: #tutorial}

Le didacticiel de bout en bout suivant couvre les étapes de création d'un projet depuis le module de démarrage pour le code Basic, y-compris les outils que
vous devez avoir installés et, après quoi, la marche à suivre pour exécuter ce module dans Xcode et Android Studio.


### Installation des outils de développement
{: #dev_tools}

Vérifiez que vous avez installé les [outils prérequis pour le développeur![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](get_code.html#prereq-dev-tools "Icône de lien externe"){: new_window}.


### Création d'un projet à partir du Module de démarrage pour le code Basic
{: #create_project}

1. Créez un projet de tableau de bord Mobile dans {{site.data.keyword.Bluemix}}.

   1. Dans la page **Initiation** du tableau de bord Mobile, cliquez sur **Créer un projet**.

      Vous pouvez également cliquer sur **Créer un projet** dans la page **Projets**.

   2. Cliquez sur **Modules de démarrage pour le code**.

   3. Sélectionnez **De base** et cliquez sur **Créer un projet**.

   4. Entrez le nom de votre projet. Pour ce tutoriel, utilisez `BasicProject`.
   
   5. Cliquez sur **Créer**.

2. Facultatif : Ajoutez la fonctionnalité {{site.data.keyword.mobilepushshort}}.

   1. Cliquez sur **Ajouter** pour **{{site.data.keyword.mobilepushshort}}** sur la page **Présentation
du projet**.

      Vous pouvez également cliquer sur **Créer** sur la page **{{site.data.keyword.mobilepushshort}}**.

   2. Entrez le nom de votre service et cliquez sur **Créer**.

   3. Pour iOS, [configurez le service de notification push d'Apple![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobilepush/t_push_provider_ios.html "Icône de lien externe"){: new_window}.

   4. Pour Android, [configurez Firebase Cloud Messaging![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobilepush/t_push_provider_android.html "Icône de lien externe"){: new_window}.
   
3. Facultatif : ajoutez la fonction Analyse.

   1. Cliquez sur **Ajouter** pour **Analyse** dans la page **Présentation du projet**.

      Vous pouvez également cliquer sur **Créer** dans la page **Analyse**.

   2. Entrez le nom de votre service et cliquez sur **Créer**.
   
   3. Désactivez le **Mode démonstration** pour afficher vos données analytiques après avoir exécuté votre application.
   
   4. Voir [Initiation à {{site.data.keyword.mobileanalytics_short}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobileanalytics/index.html "Icône de lien externe"){: new_window} pour plus d'informations sur la configuration d'Analytics.
  
4. Facultatif : ajoutez la fonction Authentification.

   1. Cliquez sur **Ajouter** pour **Authentification** dans la page **Présentation du projet**.

      Vous pouvez également sélectionner **Créer** dans la page **Authentification**.

   2. Entrez le nom de votre service et cliquez sur **Créer**.
   
   3. Activez **Authentification**.
   
   4. Sélectionnez votre fournisseur d'identité et saisissez les informations requises pour le configurer. Vous pouvez activer un seul fournisseur d'identité.

   5. Voir [Initiation à {{site.data.keyword.amashort}} ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobileaccess/index.html "Icône de lien externe"){: new_window} pour plus d'informations sur la configuration du service Authentication.

5. Générer votre code de projet.

   1. Cliquez sur **Obtenir le code** sur la page **Présentation du projet** pour sélectionner votre plateforme et votre langue.
   
      Vous pouvez également cliquer sur la page **Code**.
      
   2. Pour Objective-C, cliquez sur **iOS Obj-C**.

   3. Pour Swift, cliquez sur **iOS Swift**.
   
   4. Pour Cordova, cliquez sur **Cordova**.

   5. Pour Android, cliquez sur **Android**.
   
   6. Lorsque la génération du code du projet est terminée, cliquez sur **Télécharger le code** pour télécharger l'archive du projet.


### Exécution de votre projet Objective-C dans Xcode
{: #run_obj-c}

1. Décompressez le fichier `BasicProject-ObjC.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour examiner les étapes de configuration de votre projet.

   1. Ouvrez votre Terminal et accédez à votre dossier de projet.
   
      1. Exécutez `pod setup` si vous devez configurer votre référentiel CocoaPods.
      
      2. Exécutez `pod update`  si vous devez mettre à jour les nacelles existantes.
      
      3. Exécutez `pod install` pour installer les nacelles requises pour votre projet.
      
   2. Ouvrez votre espace de travail Xcode `BasicProject.xcworkspace`.
      
3. Exécutez votre application.


### Exécution de votre projet Swift dans Xcode
{: #run_swift}

1. Décompressez le fichier `BasicProject-Swift.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour examiner les étapes de configuration de votre projet.

   1. Ouvrez votre Terminal et accédez à votre dossier de projet.
   
      1. Exécutez `pod setup` si vous devez configurer votre référentiel CocoaPods.
      
      2. Exécutez `pod update`  si vous devez mettre à jour les nacelles existantes.
      
      3. Exécutez `pod install` pour installer les nacelles requises pour votre projet.
      
   3. Ouvrez votre espace de travail Xcode `BasicProject.xcworkspace`.
      
3. Exécutez votre application.


### Exécution de votre projet Cordova dans Xcode
{: #run_cordova_xcode}

1. Décompressez le fichier `BasicProject-Cordova.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour configurer votre projet.

   1. Ouvrez votre projet `platforms/ios` dans Xcode.
      
3. Exécutez votre application.


### Exécution de votre projet Cordova dans Android Studio
{: #run_cordova_studio}

1. Décompressez le fichier `BasicProject-Cordova.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour configurer votre projet.

   1. Ouvrez votre projet `platforms/android` dans Android Studio.
      
3. Exécutez votre application.


### Exécution de votre projet Android dans Android Studio
{: #run_android}

1. Décompressez le fichier `BasicProject-Android.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour configurer votre projet.

   1. Ouvrez votre projet `BasicProject-Android` dans Android Studio.
      
3. Exécutez votre application.


## Etape suivante
{: #what_next}

Consultez d'autres tutoriels.


### Tutoriels du module de démarrage pour l'interface utilisateur
{: #tutorials_UI}

* [Tutoriel - Catalogue magasin](tutorial_store_catalog.html)


### Tutoriels du module de démarrage pour le code
{: #tutorials_Code}

* [Tutoriel - Cloudant Sync](tutorial_cloudant_synd.html)
* [Tutoriel - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutoriel - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutoriel - Watson Language](tutorial_watson_language.html)
* [Tutoriel - Weather](tutorial_weather.html)
