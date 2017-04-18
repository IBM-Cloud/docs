---

copyright:
  years: 2015, 2016
lastupdated: "2016-06-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Valeurs par défaut du pack de construction
{: #buildpack_defauts}

Le pack de construction Liberty est mis à jour régulièrement dans Bluemix. Chaque édition peut contenir des correctifs de sécurité ou des
améliorations de fonction.

Le pack de construction possède des valeurs par défaut pour des paramètres tels que la version Java ou le jeu de fonctions Liberty pour les
applications WAR ou EAR. Certaines des valeurs par défaut peuvent changer d'une édition de pack de construction à l'autre, ce qui peut avoir un impact
négatif sur l'application. Pour éviter que l'application ne soit affectée par la modification des valeurs par défaut du pack de construction, configurez
votre application de sorte qu'elle ne s'appuie pas sur les valeurs par défaut du pack de construction.

## Versions de Liberty
{: #liberty_versions}

Le pack de construction fournit deux versions de l'environnement d'exécution Liberty :
1. Edition stable
  * Il s'agit de l'environnement d'exécution Liberty par défaut.
  * Elle ne fournit pas de [fonction bêta](usingBetaFeatures.html).
  * Elle est généralement mise à jour tous les trimestres.

2. Edition mensuelle
  * Elle doit être activée de manière explicite en affectant à la variable d'environnement **JBP_CONFIG_LIBERTY** la valeur **"version: +"**.
  * Elle fournit des [fonctions bêta](usingBetaFeatures.html).
  * Elle est généralement mise à jour tous les mois.

## Fonctions Liberty
{: #liberty_features}

Lorsque vous déployez des fichiers WAR ou EAR, le pack de construction fournit une configuration pour l'application avec le jeu par défaut de fonctions Liberty. Ce jeu par défaut de fonctions Liberty peut changer d'une édition de pack de construction à l'autre, mais cela reste rare. La modification du jeu de fonctions par défaut peut avoir un impact négatif sur l'application. Certaines options permettent de garantir que l'application
ne soit pas affectée par la modification des valeurs par défaut des fonctions.

* Définissez la variable d'environnement JBP_CONFIG_LIBERTY afin de spécifier explicitement la liste des fonctions activées pour l'application. Pour plus d'informations, voir [Applications autonomes](optionsForPushing.html#stand_alone_apps).
* Déployez votre application en tant que [répertoire de serveur](optionsForPushing.html#server_directory)
ou [package de serveur](optionsForPushing.html#packaged_server). Fournissez un fichier server.xml personnalisé qui spécifie le jeu exact de fonctions requises par votre application.

Les applications
qui sont déployées en tant que répertoire de serveur ou package de serveur ne sont pas affectées par la modification des valeurs par défaut des
fonctions Liberty.

## Version Java
{: #java_version}

Le pack de construction met à disposition un environnement d'exécution Java (JRE) par défaut pour
l'application. La version majeure ou mineure de l'environnement d'exécution Java (JRE) peut changer d'une édition de pack de construction à l'autre. La
version mineure de l'environnement d'exécution Java peut être mise à jour souvent alors que la version majeure l'est rarement. La modification de la
version majeure de l'environnement d'exécution Java (JRE) peut avoir un impact négatif sur l'application.

Pour faire en sorte que l'application ne soit pas affectée par la modification de version majeure, affectez à la variable d'environnement la version JRE appropriée, comme indiqué dans la section [Personnalisation de l'environnement d'exécution Java](customizingJRE.html). Pour de meilleurs
résultats, adoptez Java 8 pour vos applications.


# rellinks
{: #rellinks}
## general
{: #general}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
