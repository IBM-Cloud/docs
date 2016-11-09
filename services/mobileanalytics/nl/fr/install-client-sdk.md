---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-18"

---

# Installation des logiciels SDK du client {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Dernière mise à jour : 18 octobre 2016
{: .last-updated}

Actuellement, les logiciels SDK du client {{site.data.keyword.mobileanalytics_short}} sont disponibles pour Android, iOS et WatchOS.
{: #shortdesc}

## Installation du logiciel SDK du client Android
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

Le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}} est distribué avec Gradle, un gestionnaire de dépendances pour les projets Android. Gradle télécharge automatiquement les artefacts à partir des référentiels et les met à la disposition de votre application Android.

1. Créez un projet [Android Studio](http://developer.android.com/sdk/index.html) ou ouvrez un projet existant.

2. Ouvrez le fichier `build.gradle` qui se trouve dans votre **module d'application**.

  **Astuce** : votre projet Android peut comporter deux fichiers `build.gradle`, l'un est destiné au projet et l'autre au module d'application. Prenez soin d'utiliser le fichier destiné au **module d'application**. 

3. Localisez la section `Dependencies` dans le fichier `build.gradle` et ajoutez une dépendance de compilation pour le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}}. Votre instruction de référentiels doit se présenter comme suit :

	```Gradle
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  ```
  {: codeblock}

4. Synchronisez votre projet avec Gradle en cliquant sur **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Ouvrez le fichier `AndroidManifest.xml` pour votre projet Android. Ce fichier se trouve dans **app > manifests**. Ajoutez des droits d'accès à Internet sous l'élément `<manifest>` :

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
6. Vous avez installé le logiciel SDK client Android. A présent, [importez et initialisez ](sdk.html#initalize-ma-sdk-android) le logiciel SDK client d'analyse.    

## Installation du logiciel SDK du client Swift
{: #installing-sdk-ios}

![Compatible avec CocoaPods](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

Le logiciel SDK de {{site.data.keyword.mobileanalytics_full}} vous permet d'instrumenter votre application mobile. Le logiciel SDK de Swift est disponible pour iOS et watchOS.

### Avant de commencer
{: #before-you-begin-ios}

Vérifiez que Xcode est correctement configuré. Pour savoir comment configurer votre environnement de développement iOS, voir le [site Web Apple Developer](https://developer.apple.com/support/xcode/). Lisez la documentation relative aux [exigences Xcode](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements) pour Client SDK Swift Analytics.

Le logiciel SDK {{site.data.keyword.mobileanalytics_short}} est distribué avec [CocoaPods](https://cocoapods.org/) et  [Carthage](https://github.com/Carthage/Carthage#getting-started), lesquels sont des gestionnaires de dépendance pour des projets Cocoa. CocoaPods et Carthage téléchargent automatiquement des artefacts depuis des référentiels et les met à la disposition de votre application.

#### CocoaPods
{: #cocoapods}

1. Si CocoaPods n'est pas installé, exécutez la commande suivante :

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}
    
    Pour Xcode 8 : `sudo gem install cocoapods --pre`
    
   Vérifiez que vous disposez de la dernière version de `BMSAnalytics` en mettant à jour votre référentiel CocoaPods local, comme suit :
   
    ```
    pod repo update master
    ```
    {: codeblock}

2. Appliquez les [{{site.data.keyword.Bluemix_notm}}instructions relatives à Mobile Services Swift SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods) contenues sur GitHub.
	
3. Après avoir installé le logiciel SDK client iOS, [importez et initialisez](sdk.html#init-ma-sdk-ios) le logiciel SDK client d'analyse.    

#### Carthage
{: #carthage}

Ajoutez des infrastructures à votre projet à l'aide de [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Suivez les [instructions d'installation de Carthage](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage) contenues sur GitHub.

2. Après avoir installé le logiciel SDK client iOS, [importez et initialisez](sdk.html#init-ma-sdk-ios) le logiciel SDK client d'analyse. 

# rellinks

## SDK
* [Logiciel SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [Logiciel SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Référence d'API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
