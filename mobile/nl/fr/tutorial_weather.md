---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Tutoriel - Module de démarrage pour le code Weather
{: #tutorial_weather}

Le Module de démarrage pour le code {{site.data.keyword.Bluemix}} Mobile pour Weather utilise un projet modèle de démonstration pour commencer à travailler avec Weather, en utilisant Swift et inclut des points d'intégration avec les fonctions Notifications push et Analyse.


## Configuration requise
{: #tutorial_requirements}

* Un compte [Bluemix](http://bluemix.net)
* Une instance de service [Weather Company Data](https://console.{DomainName}/catalog/services/weather-company-data/) obtenue dans le [catalogue Bluemix](https://console.{DomainName}/catalog/)


## Initiation
{: #tutorial_gs}

Pour être rapidement opérationnel avec le module de démarrage pour le code Weather, procédez comme suit :

1. Créez un projet de tableau de bord Mobile dans {{site.data.keyword.Bluemix_notm}}.

   1. Dans la page **Initiation** du tableau de bord Mobile, cliquez sur **Créer un projet**.

      Vous pouvez également cliquer sur **Nouveau projet** dans la page **Projets**.

   2. Cliquez sur **Modules de démarrage pour le code**.

   3. Sélectionnez **Weather** et cliquez sur **Créer un projet**.

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

5. Procédez à l'extraction de l'archive et suivez les instructions figurant dans le fichier `README.md`.


## Etape suivante
{: #tutorial_next}

[Essayez !](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399){: new_window}
