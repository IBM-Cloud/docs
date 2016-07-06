---

copyright:
  years: 2015, 2016

---

# Installation du système {{site.data.keyword.mobileanalytics_short}}
SDK client
{: #mobileanalytics_sdk}
*Dernière mise à jour : 21 avril 2016*
{: .last-updated}

Actuellement, les logiciels SDK du client {{site.data.keyword.mobileanalytics_short}} sont disponibles pour Android, iOS et WatchOS.
{: #shortdesc}

## Installation du logiciel SDK du client Android
{: #install-sdk-android}

Le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}} est distribué avec Gradle, un gestionnaire de dépendances pour les projets Android. Gradle
télécharge automatiquement les artefacts à partir des référentiels et les met à la disposition de votre application Android.

1. Créez un projet [Android Studio](http://developer.android.com/sdk/index.html) ou ouvrez un projet existant.

2. Ouvrez le fichier `build.gradle` qui se trouve dans votre module d'application.

  **Astuce** : votre projet Android peut comporter deux fichiers `build.gradle`, l'un est destiné au projet et l'autre au module d'application. Prenez soin d'utiliser le fichier destiné au **module d'application**.

3. Localisez la section `Dependencies` dans le fichier `build.gradle` et ajoutez une dépendance de compilation pour le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}}, comme suit :

  ```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
      name:'analytics',
      version: '1.+',
      ext: 'aar',
      transitive: true
  ```
  {: codeblock}

  Votre instruction de référentiels doit se présenter comme suit :

	```Gradle
      dependencies {
        compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
          name:'analytics',
          version: '1.+',
          ext: 'aar',
          transitive: true
    	// other dependencies  
      }
  ```
  {: screen}

4. Synchronisez votre projet avec Gradle en cliquant sur **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Ouvrez le fichier `AndroidManifest.xml` de votre projet Android et ajoutez des droits d'accès à Internet sous l'élément `<manifest>` :

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}


## Installation du logiciel SDK du client Swift
{: #installing-sdk-ios}

Le logiciel SDK de {{site.data.keyword.mobileanalytics_full}} vous permet d'instrumenter votre application mobile. Le logiciel SDK de Swift est disponible pour iOS et watchOS.

### Avant de commencer
{: #before-you-begin-ios}

Vérifiez que Xcode est correctement configuré. Pour savoir comment configurer votre environnement de développement iOS, voir le [site Web Apple Developer](https://developer.apple.com/support/xcode/).

Le logiciel SDK de {{site.data.keyword.mobileanalytics_short}} est distribué avec [Cocoapods](https://cocoapods.org/) et [Carthage](https://github.com/Carthage/Carthage#getting-started), qui sont des gestionnaires de dépendances pour les projets Cocoa. CocoaPods et Carthage téléchargent automatiquement des artefacts depuis des référentiels et les met à la disposition de votre application.

#### Cocoapods
{: #cocoapods}
1. Si CocoaPods n'est pas installé, exécutez la commande suivante :

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}

2. Si vous n'avez pas encore initialisé votre espace de travail pour CocoaPods, exécutez la commande `pod init` dans le répertoire racine de votre projet. CocoaPods crée pour vous un `fichier Pod` dans lequel vous définissez les dépendances de votre projet Xcode.

3. Ajoutez `BMSAnalytics` à la cible dans votre fichier Pod, par exemple :

	### iOS

  ```
  use_frameworks!

  target 'MyApp' do
     platform :ios, '8.0'
     pod 'BMSAnalytics'
  end
  ```

4. Sauvegardez le `fichier Pod` et exécutez `pod install` à partir de la ligne de commande.

5. Ouvrez votre espace de travail de travail Xcode à l'aide du fichier `.xcworkspace` qui a été généré par CocoaPods.

#### Carthage
{: #carthage}

Ajoutez des infrastructures à votre projet à l'aide de [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Ajoutez des infrastructures `BMSAnalytics` à votre fichier Cart :
  ```
  github "ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics"
  ```
2. Exécutez la commande `carthage update`. A la fin de la génération, faites glisser `BMSAnalytics.framework`, `BMSCore.framework` et `BMSAnalyticsAPI.framework` dans votre projet Xcode.
3. Suivez les instructions décrites sur le site [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) pour finaliser l'intégration.

# rellinks

## SDK
* [Logiciel SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [Logiciel SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Référence pour l'API
{: #api}
* [API REST](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
