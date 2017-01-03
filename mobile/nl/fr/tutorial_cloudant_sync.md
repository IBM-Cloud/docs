---

copyright:
  years: 2016
lastupdated: "2016-12-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Tutoriel de bout en bout du Module de démarrage pour le code Cloudant Sync
{: #tutorial}

Le didacticiel de bout en bout suivant couvre les étapes de création d'un projet depuis le module de démarrage pour le code
Cloudant Sync, y-compris les outils que vous devez avoir installés et, après quoi, la marche à suivre pour exécuter ce module dans Android Studio.


### Installation des outils de développement
{: #dev_tools}

Assurez-vous que vous avez installé les [outils de développement requis](get_code.html#prereq-dev-tools){: new_window}.


### Création d'un projet à partir du module de démarrage de Cloudant Sync
{: #create_project}

1. Créez un projet de tableau de bord Mobile dans {{site.data.keyword.Bluemix}}.

   1. Dans la page **Initiation** du tableau de bord Mobile, cliquez sur **Créer un projet**.

      Vous pouvez également cliquer sur **Créer un projet** dans la page **Projets**.

   2. Cliquez sur **Modules de démarrage pour le code**.

   3. Sélectionnez **Cloudant Sync** et cliquez sur **Créer un projet**.

   4. Entrez le nom de votre projet. Pour ce tutoriel, utilisez `CloudantSyncProject`.
   
   5. Cliquez sur **Créer**.

2. Ajoutez la fonctionnalité Données. Vous pouvez créer une nouvelle instance {{site.data.keyword.cloudant}} ou ajouter une instance de service
existant.

   1. Cliquez sur **Ajouter** pour **Données** sur la page **Présentation du projet**.

      Vous pouvez également cliquer sur **Créer** ou sur **Ajouter un projet existant** depuis la page
**Données**.
      
   2. Facultatif : si vous choisissez de créer une nouvelle instance de service, entrez le nom de votre service et cliquez sur
**Créer**.

   3. Facultatif : si vous choisissez d'ajouter une instance de service existante, sélectionnez-la dans la liste et cliquez sur
**Ajouter**.

   4. Cliquez sur l'icône **Menu** dans la vignette de votre service et sélectionnez **Lancer...** pour lancer votre
instance de service.

      1. Cliquez sur **Lancer** pour lancer votre console {{site.data.keyword.cloudant}}.

      2. Cliquez sur **Créer une base de données**, entrez le nom de votre base de données et cliquez sur
**Créer**.

      3. Cliquez sur l'icône **+** en regard de **Tous les documents** pour ajouter des documents.

3. Facultatif : ajoutez la fonction Notifications push.

   1. Cliquez sur **Ajouter** pour **Notifications push** dans la page **Présentation du projet**.

      Vous pouvez également cliquer sur **Créer** dans la page **Notifications push**.

   2. Entrez le nom de votre service et cliquez sur **Créer**.

   3. Pour Android, [configurez Firebase Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
4. Facultatif : ajoutez la fonction Analyse.

   1. Cliquez sur **Ajouter** pour **Analyse** dans la page **Présentation du projet**.

      Vous pouvez également cliquer sur **Créer** dans la page **Analyse**.

   2. Entrez le nom de votre service et cliquez sur **Créer**.
   
   3. Désactivez le **Mode démonstration** pour afficher vos données analytiques après avoir exécuté votre application.
   
   4. Voir [Initiation à {{site.data.keyword.mobileanalytics_short}}](/docs/services/mobileanalytics/index.html){: new_window} pour plus d'informations sur la configuration de l'analyse.
  
5. Facultatif : ajoutez la fonction Authentification.

   1. Cliquez sur **Ajouter** pour **Authentification** dans la page **Présentation du projet**.

      Vous pouvez également sélectionner **Créer** dans la page **Authentification**.

   2. Entrez le nom de votre service et cliquez sur **Créer**.
   
   3. Activez **Authentification**.
   
   4. Sélectionnez votre fournisseur d'identité et saisissez les informations requises pour le configurer. Vous pouvez activer un seul fournisseur d'identité.

   5. Voir [Initiation à {{site.data.keyword.amashort}}](/docs/services/mobileaccess/index.html){: new_window} pour plus d'informations sur la configuration de l'authentification.

6. Générer votre code de projet.

   1. Cliquez sur **Obtenir le code** sur la page **Présentation du projet** pour sélectionner votre plateforme et votre langue.
   
      Vous pouvez également cliquer sur la page **Code**.
      
   2. Pour Android, cliquez sur **Android**.
   
   3. Lorsque la génération du code du projet est terminée, cliquez sur **Télécharger le code** pour télécharger l'archive du projet.


### Exécution de votre projet Android dans Android Studio
{: #run_android}

1. Décompressez le fichier `CloudantSyncProject-Android.zip`.

2. Ouvrez le fichier `README.md` dans un lecteur Markdown pour configurer votre projet.

   1. Ouvrez votre projet `CloudantSyncProject-Android` dans Android Studio.

   2. Ajoutez vos données d'identification Cloudant.

      1. Sur la page **Données**, cliquez sur l'icône **Menu** dans la vignette de votre service
et sélectionnez **Lancer...** pour lancer votre instance de service.

         1. Cliquez sur **Lancer** pour lancer votre console {{site.data.keyword.cloudant}}.

         2. Cliquez sur le nom de votre base de données, puis sur **Autorisations**.

         3. Entrez le nom de votre base de données dans la chaîne `nom_BD_cloudant` dans le fichier
`res/values/cloudant_credentials.xml`.

         4. Cliquez sur **Générer une clé d'API**.

             1. Copiez la valeur de **Clé** et collez-la dans la chaîne `cloudant_api_key` dans le fichier
`res/values/cloudant_credentials.xml`.

             2. Copiez la valeur de **Mot de passe** et collez-la dans la chaîne `cloudant_api_password` dans le
fichier
`res/values/cloudant_credentials.xml`.

             3. Sélectionnez l'autorisation **_admin**.
      
3. Exécutez votre application.


## Etape suivante
{: #what_next}

Consultez d'autres tutoriels.


### Tutoriels du module de démarrage pour l'interface utilisateur
{: #tutorials_UI}

* [Tutoriel - Catalogue magasin](tutorial_store_catalog.html)


### Tutoriels du module de démarrage pour le code
{: #tutorials_Code}

* [Tutoriel - Basic](tutorial.html)
* [Tutoriel - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutoriel - Watson Language](tutorial_watson_language.html)
* [Tutoriel - Weather](tutorial_weather.html)
