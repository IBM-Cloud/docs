---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}

# Nouveautés du tableau de bord Mobile
{: #what_is_new}

Dernière mise à jour : 18 octobre 2016
{: .last-updated}

La mise à jour d'octobre du tableau de bord
{{site.data.keyword.Bluemix}} Mobile introduit les modifications
suivantes : 

   * Vous pouvez désormais ajouter les fonctions Notifications push et Analyse dans votre projet directement à partir du tableau de bord. 
   * Des [modules de démarrage pour le code](starters.html#Code_Starter) sont maintenant disponibles. 
   * Swift est désormais pris en charge.


### L'analyse
{: #analytics}

   * Le mode démonstration est activé par défaut lorsque vous ajoutez la
fonction Analyse. Vous pouvez désactiver le mode démonstration pour visualiser
l'analyse après l'exécution de votre application. 


### Générateur d'interface graphique
{: #ui_builder}

   * Il est désormais possible d'accéder à la fonction **Notifications push** à partir du projet. 
   * L'onglet **Paramètres du projet** a été renommé
en **Paramètres**.
   * L'onglet **Authentification** a été renommé en **Accès utilisateur**.


### Code
{: #code}

   * Le code Objective-C et Swift généré pour iOS utilise désormais
CocoaPods pour la gestion des dépendances. Cela signifie que vous devez
installer CocoaPods. Pour ce faire, exécutez `sudo gem install cocoapods`. Une
fois CocoaPods installé, exécutez `pod setup` pour le
configurer (si ne l'est pas déjà). Exécutez ensuite `pod
install` pour télécharger et installer les dépendances de projet
requises avant d'ouvrir votre fichier `.xcworkspace` dans Xcode. Vous
trouverez plus de détails dans le fichier `README.md`, dans
l'archive du code téléchargé. Pour plus d'informations, voir
[Outils prérequis pour le développeur](get_code.html#prereq-dev-tools).

Revenez vérifier fréquemment pour être tenu au courant des nouvelles mises à jour.


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
