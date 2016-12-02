---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

# Installation des logiciels SDK du client {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Actuellement, les logiciels SDK du client
{{site.data.keyword.mobileanalytics_short}} sont disponibles pour Android, iOS, WatchOS et Cordova.
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
6. Vous avez installé le logiciel SDK client Android. A présent, [importez et initialisez](sdk.html#initalize-ma-sdk) le logiciel SDK client d'analyse.    

## Installation du logiciel SDK du client Swift
{: #installing-sdk-ios}

![Compatible avec CocoaPods](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

Le logiciel SDK de {{site.data.keyword.mobileanalytics_full}} vous permet d'instrumenter votre application mobile. Le logiciel SDK de Swift est disponible pour iOS et watchOS.

### Avant de commencer
{: #before-you-begin-ios}

Vérifiez que Xcode est correctement configuré. Pour savoir comment configurer votre environnement de développement iOS, voir le [site Web Apple Developer](https://developer.apple.com/support/xcode/). Lisez la documentation relative aux [exigences Xcode](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements) pour Client SDK Swift Analytics.

Le logiciel SDK {{site.data.keyword.mobileanalytics_short}} est distribué avec [CocoaPods](https://cocoapods.org/) et  [Carthage](https://github.com/Carthage/Carthage#getting-started), lesquels sont des gestionnaires de dépendance pour des projets Cocoa. CocoaPods et Carthage téléchargent automatiquement des artefacts depuis des référentiels et les met à la disposition de votre application. Sélectionnez CocoaPods ou Carthage :

#### CocoaPods
{: #cocoapods}

1. Appliquez les [{{site.data.keyword.Bluemix_notm}}instructions relatives à Mobile Services Swift SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods) contenues sur GitHub pour installer `BMSAnalytics` en utilisant Cocoapods et l'ajouter à votre Podfile. 
	
2. Après avoir installé le logiciel SDK client iOS, [importez et initialisez](sdk.html#initalize-ma-sdk) le logiciel SDK client d'analyse.    

#### Carthage
{: #carthage}

Si vous n'utilisez pas CocoaPods, vous pouvez ajouter des infrastructures à votre projet en utilisant [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Suivez les [instructions d'installation de Carthage](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage) contenues sur GitHub pour installer `BMSAnalytics`.

2. Après avoir installé le logiciel SDK client iOS, [importez et initialisez](sdk.html#initalize-ma-sdk) le logiciel SDK client d'analyse. 

## Installation du plug-in Cordova
{: #installing-sdk-cordova}

Le plug-in Cordova de {{site.data.keyword.mobileanalytics_full}}<!--SDK-->vous permet d'instrumenter votre application mobile.  

1. Ajoutez les plateformes Android et iOS à votre application Cordova. Exécutez l'une des commandes suivantes ou les deux à partir de la ligne de commande :

	```Bash
	cordova platform add android
	```
	
	```Bash
	cordova platform add ios
	```
	
2. Si vous avez ajouté la plateforme Android, vous devez ajouter le niveau d'API minimal pris en charge au fichier `config.xml` de votre application Cordova. Ouvrez le fichier `config.xml` et ajoutez la ligne suivante à l'élément `<platform name="android">` :

	```XML
	<platform name="android">  
  	<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
  </platform>
```
La valeur de *minSdkVersion* doit être supérieure à `15`. Reportez-vous à [Android Platform Guide](https://cordova.apache.org/docs/en/latest/guide/platforms/android/) pour rester informé sur la version *targetSdkVersion* prise en charge pour le SDK Android.

3. Si vous avez ajouté le système d'exploitation iOS, déclarez une cible dans l'élément `<platform name="ios">` :

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  </platform>
```

4. Installez le plug-in Cordova de {{site.data.keyword.mobileanalytics_short}} :

 	```Bash
	cordova plugin add bms-core
	```

5. Vérifiez que le plug-in a été installé correctement à l'aide de la commande suivante :
	```Bash
	cordova plugin list
	```
	
6. Vous avez installé le plug-in Cordova. A présent, [importez et initialisez](sdk.html#initalize-ma-sdk) le logiciel SDK client d'analyse. 

# rellinks

## SDK
* [Logiciel SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [Logiciel SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Logiciel SDK de base du plug-in Cordova](https://www.npmjs.com/package/bms-core){: new_window}

## Référence d'API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
