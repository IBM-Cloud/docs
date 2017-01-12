---

copyright:
  years: 2016
lastupdated: "2016-12-01"

---
{:new_window: target="_blank"}

# Nouveautés du tableau de bord Mobile
{: #what_is_new}


### Mise à jour de novembre 2016
{: #nov-2016}

La mise à jour de novembre 2016 du tableau de bord {{site.data.keyword.Bluemix}} Mobile comprend les modifications suivantes :

   * Vous pouvez à présent générer des artefacts SDK pour vos projets depuis la page **Code**.
   * Cordova est à présent pris en charge pour le module de démarrage Basic.
   * Vous pouvez à présent [créer un rapport des événements
réseau](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window} et
[suivre les demandes réseau](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window}
dans la page **Demandes réseau** de la console {{site.data.keyword.mobileanalytics_short}}.
   * Vous pouvez à présent [exporter des données dans dashDB](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window}
depuis la console {{site.data.keyword.mobileanalytics_short}}.


### Mise à jour de novembre 2016
{: #oct-2016}

La mise à jour d'octobre 2016 du tableau de bord {{site.data.keyword.Bluemix_notm}} Mobile comprend les modifications suivantes :

   * Vous pouvez désormais ajouter les fonctions Notifications push et Analyse dans votre projet directement à partir du tableau de bord.
   * Des [modules de démarrage pour le code](starters.html#Code_Starter) sont maintenant disponibles.
   * Vous pouvez ajouter l'authentification aux projets que vous avez créés à partir d'un module de démarrage de code.
   * Swift est désormais pris en charge.


#### L'analyse
{: #analytics}

   * Le mode démonstration est activé par défaut lorsque vous ajoutez la
fonction Analyse. Vous pouvez désactiver le mode démonstration pour visualiser
l'analyse après l'exécution de votre application.


#### Générateur d'interface graphique
{: #ui_builder}

   * Il est désormais possible d'accéder à la fonction **Notifications push** à partir du projet.
   * L'onglet **Paramètres du projet** a été renommé
en **Paramètres**.
   * L'onglet **Authentification** a été renommé en **Accès utilisateur**.


#### Code
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
