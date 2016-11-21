---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}

# Tutoriel - Module de démarrage pour le code Weather
{: #tutorial_weather}

Dernière mise à jour : 13 octobre 2016
{: .last-updated}

Le Module de démarrage pour le code {{site.data.keyword.Bluemix}}
Mobile pour Weather utilise un projet modèle de démonstration pour
commencer à travailler avec Weather, en utilisant Swift et inclut des points
d'intégration avec les fonctions Notifications push et Analyse.


## Configuration requise
{: #tutorial_requirements}

* Un compte [Bluemix](http://bluemix.net)
* Une instance de service
[Weather
Company Data](https://console.{DomainName}/catalog/services/weather-company-data/) obtenue dans le
[catalogue Bluemix](https://console.{DomainName}/catalog/)


## Initiation
{: #tutorial_gs}

Pour être rapidement opérationnel avec le module de démarrage pour le code
Weather, procédez comme suit : 

1. Créez un projet de tableau de bord Mobile dans {{site.data.keyword.Bluemix_notm}}.

   1. Dans la page **Initiation** du tableau de bord
Mobile, cliquez sur **Créer un projet**.

      Vous pouvez également cliquer sur **Nouveau
projet** dans la page **Projets**.

   2. Cliquez sur **Modules de démarrage pour le code**.

   3. Sélectionnez **Weather** et cliquez sur **Créer un projet**.

   4. Entrez le nom de votre projet et cliquez sur
**Créer**.

2. Facultatif : ajoutez la fonction Notifications push.

   1. Cliquez sur **Ajouter** pour
**Notifications push** dans la page **Présentation du projet**.

      Vous pouvez également cliquer sur **Créer**
dans la page **Notifications push**.

   2. Entrez le nom de votre service et cliquez sur
**Créer**.

   3. Pour iOS,
[configurez Apple Push Notification Service](../services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Pour Android,
[configurez Google Cloud Messaging](../services/mobilepush/t_push_provider_android.html){: new_window}.

3. Facultatif : ajoutez d'autres services.

   1. Cliquez sur **Ajouter** pour le service dans la
page **Présentation du projet**.

   2. Entrez le nom de votre service et cliquez sur
**Créer**.

   3. Suivez les instructions de configuration du service. 

4. Téléchargez votre projet.

   1. Cliquez sur **Code** et sélectionnez votre
langage préféré. 

   2. Cliquez sur **Télécharger le code**.

5. Procédez à l'extraction de l'archive et suivez les instructions
figurant dans le fichier `README.md`.


## Etape suivante
{: #tutorial_next}

[Essayez !](http://new-console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399){: new_window}


# Liens connexes
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Articles de blogue
{: #general}
* [Article de blogue : Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Article de blogue : Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [Article de blogue : Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [Article de blogue : Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Article de blogue : Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Tutoriels et exemples
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
