---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Obtention du code
{: #Get_Code}

Une fois que vous avez terminé la configuration de votre projet mobile
avec les fonctions Notifications push, Analyse et Authentification, vous pouvez
télécharger le code qui vous permet d'exécuter le code dans Xcode ou Android Studio. Le
projet téléchargé est préconfiguré avec les dépendances aux logiciels SDK
requises et les données d'identification de chaque fonction configurée. 

Vous devez terminer les données d'identification des services services
qui ne sont pas configurables dans le projet téléchargé. Le fichier
`README.md` du projet du module de démarrage contient les
instructions associées. Consultez le fichier `README.md` dans
un afficheur Markdown afin de terminer la configuration. 

### Outils prérequis pour le développeur
{: prereq-dev-tools}

Les outils de développement suivants sont nécessaires lorsque vous
utilisez du code généré à partir du tableau de bord {{site.data.keyword.Bluemix_notm}} Mobile :

#### Android
* [Android Studio 2.2](https://developer.android.com/studio)
	* Installez la dernière version [Android 7.0](https://www.android.com/versions/nougat-7-0/).

#### iOS
* Xcode 8.0 (recommandé)
	* Installez la dernière version [iOS 10](http://www.apple.com/ios/ios-10/).
* [Homebrew](http://brew.sh/)
	* Outil de ligne de commande facilitant l'installation d'autres outils, tels que CocoaPods et Carthage, destiné aux développeurs Apple.
* Gestionnaire de
dépendances [CocoaPods](https://cocoapods.org/) pour
l'installation des dépendances aux logiciels SDK iOS. Utilisez la version la plus récente : 

	```
	$ sudo gem install cocoapods --pre
	```
* Gestionnaire de dépendances
[Carthage](https://github.com/Carthage/Carthage) pour
l'installation des logiciels SDK Watson Developer Cloud.

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* NodeJS (modules d'exécution Node et NPM) facilitant l'exécution d'API Connect
Loopback et d'autres outils de productivité Bluemix.

	Pour exécuter les outils API Connect en local, utilisez Node 5.x : 
	```
	$ brew install Node5
	```

* [Outils de l'interface de ligne de commande Bluemix](http://clis.ng.bluemix.net/ui/home.html).
Outils de ligne de commande facilitant le déploiement des modules d'exécution
Cloud Foundry à partir d'une interface de ligne de commande avec Bluemix.  
