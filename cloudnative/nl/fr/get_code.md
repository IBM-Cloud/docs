---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Obtention du code
{: #Get_Code}

Une fois que vous avez terminé la configuration et l'installation de votre projet avec les fonctionnalités sélectionnées, vous pouvez télécharger le code permettant l'exécution. Le
projet téléchargé est préconfiguré avec les dépendances aux logiciels SDK
requises et les données d'identification de chaque fonction configurée.

Vous devez terminer les données d'identification des services qui ne sont pas configurables dans le projet téléchargé. Le fichier `README.md` du projet du module de démarrage contient les instructions associées. Consultez le fichier `README.md` dans un afficheur Markdown afin de terminer la configuration.

## Outils prérequis pour le développeur
{: #prereq-dev-tools}

Les outils de développement suivants sont nécessaires quand vous utilisez le code généré depuis la console {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} :


### Général
{: #general notoc}

* [Homebrew ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://brew.sh/)
	* Outil de ligne de commande facilitant l'installation d'autres outils, tels que CocoaPods et Carthage, destiné aux développeurs Apple.

* [Docker ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.docker.com/get-docker)
	* Projet open-source offrant une assistance à l'exécution et au débogage des applications dans des conteneurs. Requis uniquement pour les projets non mobiles.

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* Node.js (modules d'exécution Node et npm) facilitant l'exécution d'{{site.data.keyword.apiconnect_short}} Loopback et d'autres outils de productivité {{site.data.keyword.Bluemix_notm}}.

	Pour exécuter les outils {{site.data.keyword.apiconnect_short}}, utilisez Node 5.x :
	
	```
	$ brew install Node5
	```

* [Outils de l'interface de ligne de commande Bluemix ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://clis.ng.bluemix.net/ui/home.html)

   Outils de ligne de commande pour déployer des modules d'exécution Cloud Foundry à partir d'une interface de ligne de commande avec {{site.data.keyword.Bluemix_notm}}.  

* [{{site.data.keyword.dev_cli_notm}} ![Icône de lien externe](../icons/launch-glyph.svg "Icônede lien externe")](dev_cli.html)


	Plug-in d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} pour créer, exécuter, tester et déployer des projets Web et mobiles.
	
* [Plug-in de générateur SDK![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](sdk_cli.html)

	Plug-in d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} pour générer des SDK depuis votre définition d'API REST conforme à la [spécification Open API ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.openapis.org/).

### Android
{: #android notoc}

* [Android Studio 2.2 ou supérieur![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://developer.android.com/studio)
	* Installez le dernier environnement d'exécution [Android 7.0 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.android.com/versions/nougat-7-0/).

### iOS
{: #ios notoc}

* [Xcode 8 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://developer.apple.com/xcode/) (recommandé)

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* [Gestionnaire de dépendances CocoaPods ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cocoapods.org/) pour l'installation des dépendances du SDK iOS. Utilisez la version la plus récente :

	```
	$ sudo gem install cocoapods --pre
	```
* [Gestionnaire de dépendances Carthage ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/Carthage/Carthage) pour l'installation des SDK de {{site.data.keyword.watson}} Developer Cloud.

	```
	$ brew install carthage
	```
