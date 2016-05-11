# Initialisation du logiciel SDK Push pour les applications iOS
{: #enable-push-ios-notifications-install}

Pour un projet Xcode existant, vous pouvez configurer le logiciel SDK du client Bluemix Mobile Services à l'aide de l'outil de gestion des dépendances CocoaPods. Vous pouvez aussi installer le logiciel SDK manuellement.

**Remarque** : Pour afficher le fichier Readme Swift Push, accédez à https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master

##Installation de CocoaPods

1. Installez CocoaPods en exécutant la commande suivante sur votre terminal Mac :
```
$ sudo gem install cocoapods
```
2. Entrez la commande ci-dessous dans le terminal pour initialiser CocoaPods. Prenez soin d'exécuter cette commande dans le répertoire où se trouve votre Xcode. La commande `pod init` permet de créer un titre de fichier.
```
$ pod init
```
3. Dans le fichier Pod généré, ajoutez les dépendances de logiciel SDK dont vous avez besoin. Copiez le fichier Pod suivant :

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copiez la liste suivante en l'état et supprimez les dépendances dont vous n'avez pas besoin
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copiez la liste suivante en l'état et supprimez les dépendances dont vous n'avez pas besoin.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. Depuis le terminal, accédez au dossier de votre projet et installez des dépendances avec la commande suivante :
```
$ pod update
```
Cette commande installe vos dépendances et crée un espace de travail Xcode.  **Remarque** : Prenez soin de toujours ouvrir le nouvel espace de travail Xcode au
lieu du fichier de projet Xcode d'origine : 

	```
	$ open App.xcworkspace
	```
Cet espace de travail contient votre projet d'origine et le projet Pods contenant vos dépendances. Si
vous voulez modifier un dossier source Bluemix Mobile Services, vous le trouverez dans votre projet
Pods, sous `Pods/yourImportedSourceFolder`. Par exemple :`Pods/IMFGoogleAuthentication`.

##Utilisation d'infrastructures et de dossiers source importés

Référencez le logiciel SDK dans votre code.


### Objective-C

Ecrivez des directives #import pour les en-têtes pertinents, par exemple :

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Remarque** : La mise à jour de votre projet Pods à l'aide des commandes CocoaPods `pod install` ou `pod update` peut remplacer les dossiers source Bluemix Mobile Services. Si
vous voulez conserver vos versions personnalisées des fichiers d'origine, prenez soin de les sauvegarder avant d'entrer l'une de ces commandes.

###Swift

**Eléments prérequis**

- iOS 8.0 ou version ultérieure
- Xcode 7


Ecrivez des directives #import pour les en-têtes pertinents, par exemple :

```
//swift
import BMSCore
import BMSPush
```


##Paramètres de génération

Accédez à **Xcode > Build Settings > Build Options** et affectez à l'option Set Enable Bitcode la valeur **No**.

**Attention** : Depuis iOS 9, des modifications apportées à la fonction App Transport Security (ATS) peuvent avoir un impact sur la façon dont vous gérez le processus d'authentification. Les articles de blogue suivants contiennent d'autres informations sur les modifications : [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) et [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)
