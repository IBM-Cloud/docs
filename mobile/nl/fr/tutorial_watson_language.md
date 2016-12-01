---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Tutoriel - Module de démarrage pour le code Watson Language
{: #tutorial_watson_language}

Le module de démarrage pour le code {{site.data.keyword.Bluemix}} Mobile pour Watson Language utilise les services Text To Speech et Language Translation de Watson, et vous donne des points d'intégration pour chacun des services {{site.data.keyword.Bluemix_notm}} Mobile.


## Configuration requise
{: #tutorial_requirements}

* Un compte [Bluemix](http://bluemix.net)
* Des instances de service [Language Translator](https://console.{DomainName}/catalog/services/language-translator/) et [Text to Speech](https://console.{DomainName}/catalog/services/text-to-speech/) obtenues à partir du [catalogue Bluemix](https://console.{DomainName}/catalog/)


## Initiation
{: #tutorial_gs}

Pour être rapidement opérationnel avec le module de démarrage pour le code Watson Language, procédez comme suit :

1. Créez un projet de tableau de bord Mobile dans {{site.data.keyword.Bluemix_notm}}.

   1. Dans la page **Initiation** du tableau de bord Mobile, cliquez sur **Créer un projet**.

      Vous pouvez également cliquer sur **Créer un projet** dans la page **Projets**.

   2. Cliquez sur **Modules de démarrage pour le code**.

   3. Sélectionnez **Watson Language** et cliquez sur **Créer un projet**.

   4. Entrez le nom de votre projet et cliquez sur **Créer**.

2. Facultatif : ajoutez la fonction Notifications push.

   1. Cliquez sur **Ajouter** pour **Notifications push** dans la page **Présentation du projet**.

      Vous pouvez également cliquer sur **Créer** dans la page **Notifications push**.

   2. Entrez le nom de votre service et cliquez sur **Créer**.

   3. Pour iOS, [configurez Apple Push Notification Service](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Pour Android, [configurez Google Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
3. Facultatif : ajoutez la fonction Analyse.

   1. Cliquez sur **Ajouter** pour **Analyse** dans la page **Présentation du projet**.

      Vous pouvez également cliquer sur **Créer** dans la page **Analyse**.

   2. Entrez le nom de votre service et cliquez sur **Créer**.
   
   3. Désactivez le **Mode démonstration** pour afficher vos données analytiques après avoir exécuté votre application.

4. Facultatif : ajoutez la fonction Authentification.

   1. Cliquez sur **Ajouter** pour **Authentification** dans la page **Présentation du projet**.

      Vous pouvez également sélectionner **Créer** dans la page **Authentification**.

   2. Entrez le nom de votre service et cliquez sur **Créer**.
   
   3. Activez **Authentification**.
   
   4. Sélectionnez votre fournisseur d'identité et saisissez les informations requises pour le configurer. Vous pouvez activer un seul fournisseur d'identité.

   5. Voir [Initiation à Mobile Client Access](/docs/services/mobileaccess/index.html){: new_window} pour plus d'informations sur la configuration de l'authentification.

5. Téléchargez votre projet.

   1. Cliquez sur **Code** et sélectionnez votre langage préféré.

   2. Cliquez sur **Télécharger le code**.

6. Procédez à l'extraction de l'archive et affichez le fichier `README.md` dans un afficheur Markdown afin de terminer la configuration.


## Etape suivante
{: #tutorial_next}

[Essayez !](http://console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375){: new_window}
