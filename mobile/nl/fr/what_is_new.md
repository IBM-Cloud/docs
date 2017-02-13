---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Nouveautés du tableau de bord Mobile
{: #what_is_new}

### Mise à jour d décembre 2016
{: #dec-2016}

La mise à jour de novembre 2016 du tableau de bord {{site.data.keyword.Bluemix}} Mobile comprend les modifications suivantes :

   * Vous pouvez retirer d'un projet un service connecté de sorte à pouvoir le supprimer ou le réutiliser avec un autre projet. 
   * Vous pouvez ajouter un service existant à un projet.
   * Vous pouvez créer ou connecter un service CloudantNoSQL comme source de données lorsque vous utilisez un module de démarrage pour le code.
   * Là où il est pris en charge, vous pouvez créer ou connecter un service Object Storage existant comme source de données de votre projet.
   * Vous pouvez personnaliser la conception de la navigation de l'application que vous créez avec un module de démarrage pour l'interface utilisateur. 
   

### Mise à jour de novembre 2016
{: #nov-2016}

La mise à jour de novembre 2016 du tableau de bord {{site.data.keyword.Bluemix}} Mobile comprend les modifications suivantes :

   * Vous pouvez à présent générer des artefacts SDK pour vos projets depuis la page **Code**.
   * Cordova est à présent pris en charge pour le module de démarrage Basic.
   * Vous pouvez dorénavant [créer un rapport des
événements réseau![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobileanalytics/sdk.html#network-requests "Icône de lien externe"){: new_window} et
[suivre les demandes réseau
![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests "Icône de lien externe"){: new_window} sur la page des
**Demandes réseau** de la console {{site.data.keyword.mobileanalytics_short}}.
   * Vous pouvez dorénavant [exporter des données dans dashDB ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobileanalytics/app-monitoring.html#dashdb "Icône de lien externe"){: new_window} dans la console
{{site.data.keyword.mobileanalytics_short}}.


### Mise à jour de novembre 2016
{: #oct-2016}

La mise à jour d'octobre 2016 du tableau de bord {{site.data.keyword.Bluemix_notm}} Mobile comprend les modifications suivantes :

   * Vous pouvez désormais ajouter directement des fonctionnalités {{site.data.keyword.mobilepushshort}} et Analytics à votre projet
depuis le tableau de bord.
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

   * La fonctionnalité **{{site.data.keyword.mobilepushshort}}** est désormais accessible depuis le projet.
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
