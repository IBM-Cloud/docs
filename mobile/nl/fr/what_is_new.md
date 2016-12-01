---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Nouveautés du tableau de bord Mobile
{: #what_is_new}

La mise à jour d'octobre du tableau de bord
{{site.data.keyword.Bluemix}} Mobile introduit les modifications
suivantes :

   * Vous pouvez désormais ajouter les fonctions Notifications push et Analyse dans votre projet directement à partir du tableau de bord.
   * Des [modules de démarrage pour le code](starters.html#Code_Starter) sont maintenant disponibles.
   * Vous pouvez ajouter l'authentification aux projets que vous avez créés à partir d'un module de démarrage de code.
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
