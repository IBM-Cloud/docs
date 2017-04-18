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
{:note:.deprecated}

# Nouveautés de la console {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}
{: #what-is-new}


## Mise à jour de mars 2017
{: #mar-2017}

La mise à jour de mars 2017 de la console {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} comprend les modifications suivantes :

   * Le tableau de bord {{site.data.keyword.Bluemix_notm}} Mobile est devenu la console {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}.
   * La procédure de création de projets a été modifiée pour inclure les types de modèle de serveur Application Web, BFF et Microservice avec prise en charge de Node.js, Java et Swift.
   * L'intégration au nouveau service optimisé {{site.data.keyword.appid_full}} fournit une authentification pour les projets Web et mobiles.
   * Vous pouvez maintenant générer des SDK pour vos projets en utilisant le [plug-in de générateur SDK](sdk_cli.html). La génération de SDK dans la console {{site.data.keyword.dev_console}} n'est disponible que pour les projets mobiles.
   * Il vous est désormais possible de créer des projets en utilisant le plug-in [{{site.data.keyword.dev_cli_short}}](dev_cli.html).


## Mise à jour de janvier 2017
{: #jan-2017}

La mise à jour de janvier 2017 du tableau de bord {{site.data.keyword.Bluemix_notm}} Mobile comprend les modifications suivantes :

   * Au 31 janvier, les modules de démarrage pour l'interface utilisateur deviennent obsolètes. Les projets existants qui ont été crées depuis un module de démarrage pour l'interface utilisateur peuvent être utilisés jusqu'au 30 avril 2017. Pour plus d'informations sur les étapes de migration et les dates de retrait, voir l'[article de blogue de l'annonce de dépréciation![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-mobile-dashboard-update/).
{: deprecated}
   * Vous pouvez maintenant mettre à jour votre type de module de démarrage de projet au lieu de supprimer votre projet et d'en créer un nouveau.
   * Vous pouvez désormais créer votre projet avec un module de démarrage pour le code [Watson Conversation](tutorial_conversation.html).
   * Là où il est pris en charge, vous pouvez maintenant générer un SDK pour votre projet.
   * Vous pouvez désormais ajouter vos instances de calcul et générer des SDK client à ajouter à votre projet.


## Mise à jour de décembre 2016
{: #dec-2016}

La mise à jour de novembre 2016 du tableau de bord {{site.data.keyword.Bluemix_notm}} Mobile comprend les modifications suivantes :

   * Vous pouvez maintenant retirer d'un projet un service connecté de façon à pouvoir le supprimer ou le réutiliser avec un autre projet. 
   * Vous pouvez désormais ajouter un service existant à un projet.
   * Vous pouvez maintenant créer ou connecter un service CloudantNoSQL existant en tant que source de données quand vous utilisez un module de démarrage pour le code.
   * Là où il est pris en charge, vous pouvez désormais créer ou connecter un service Object Storage existant comme source de données pour votre projet.
   * Vous pouvez maintenant personnaliser la conception de la navigation de l'application que vous créez avec un module de démarrage pour l'interface utilisateur. 
   

## Mise à jour de novembre 2016
{: #nov-2016}

La mise à jour de novembre 2016 du tableau de bord {{site.data.keyword.Bluemix_notm}} Mobile comprend les modifications suivantes :

   * Vous pouvez à présent générer des artefacts SDK pour vos projets depuis la page **Code**.
   * Cordova est à présent pris en charge pour le module de démarrage Basic.
   * Vous pouvez dorénavant [créer un rapport des événements réseau ![Icône de lien externe](../icons/launch-glyph.svg "External link icon")](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window} et [suivre les demandes réseau ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window} sur la page relative aux demandes réseau de la console {{site.data.keyword.mobileanalytics_short}}.
   * Vous pouvez désormais [exporter des données dans dashDB ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window} dans la console {{site.data.keyword.mobileanalytics_short}}.


## Mise à jour de novembre 2016
{: #oct-2016}

La mise à jour d'octobre 2016 du tableau de bord {{site.data.keyword.Bluemix_notm}} Mobile comprend les modifications suivantes :

   * Vous pouvez désormais ajouter directement des fonctionnalités {{site.data.keyword.mobilepushshort}} et Analytics à votre projet
depuis le tableau de bord.
   * Des [modules de démarrage pour le code](starters.html#Code_Starter) sont maintenant disponibles.
   * Vous pouvez ajouter l'authentification aux projets que vous avez créés à partir d'un module de démarrage de code.
   * Swift est désormais pris en charge.


### L'analyse
{: #analytics notoc}

   * Le mode démonstration est activé par défaut lorsque vous ajoutez la
fonction Analyse. Vous pouvez désactiver le mode démonstration pour visualiser
l'analyse après l'exécution de votre application.


### Générateur d'interface graphique
{: #ui_builder notoc}

   * La fonctionnalité **{{site.data.keyword.mobilepushshort}}** est désormais accessible depuis le projet.
   * L'onglet **Paramètres du projet** a été renommé
en **Paramètres**.
   * L'onglet **Authentification** a été renommé en **Accès utilisateur**.


### Code
{: #code notoc}

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
