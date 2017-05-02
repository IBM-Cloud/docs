---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Installation des logiciels SDK du client {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Actuellement, les logiciels SDK du client {{site.data.keyword.mobileanalytics_short}} sont disponibles pour Android, iOS, WatchOS et Cordova.
{: shortdesc}

## Installation du logiciel SDK du client Android
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

Le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}} est distribué avec Gradle, un gestionnaire de dépendances pour les projets Android. Gradle télécharge automatiquement les artefacts à partir des référentiels et les met à la disposition de votre application Android.

1. Créez un projet [Android Studio ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/sdk/index.html){: new_window} ou ouvrez un projet existant.

2. Ouvrez le fichier `build.gradle` qui se trouve dans votre **module d'application**.

  **Astuce** : votre projet Android peut comporter deux fichiers `build.gradle`, l'un est destiné au projet et l'autre au module d'application. Prenez soin d'utiliser le fichier destiné au **module d'application**.

3. Localisez la section `Dependencies` dans le fichier `build.gradle` et ajoutez une dépendance de compilation pour le logiciel SDK du client {{site.data.keyword.mobileanalytics_short}}. Votre instruction de référentiels doit se présenter comme suit :

	```
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  	```
  	{: codeblock}

4. Synchronisez votre projet avec Gradle en cliquant sur **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Ouvrez le fichier `AndroidManifest.xml` pour votre projet Android. Ce fichier se trouve dans **app > manifests**. Ajoutez des droits d'accès à Internet sous l'élément `<manifest>` :

	```
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
   
6. Vous avez installé le logiciel SDK client Android. A présent, [importez et initialisez](sdk.html#initalize-ma-sdk) le logiciel SDK client d'analyse.   

## Installation du logiciel SDK du client Swift
{: #installing-sdk-ios}

![Compatible avec CocoaPods](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

Le logiciel SDK de {{site.data.keyword.mobileanalytics_full}} vous permet d'instrumenter votre application mobile. Le logiciel SDK de Swift est disponible pour iOS et watchOS.

### Avant de commencer
{: #before-you-begin-ios notoc}

Vérifiez que Xcode est correctement configuré. Pour savoir comment configurer votre environnement de développement iOS, voir le [site Web Apple Developer ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/support/xcode/){: new_window}. Consultez les [exigences Xcode ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements){: new_window} pour le logiciel SDK client Swift Analytics.

Le logiciel SDK {{site.data.keyword.mobileanalytics_short}} est distribué avec [CocoaPods ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://cocoapods.org/){: new_window} et [Carthage ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#getting-started){: new_window}, qui sont des gestionnaires de dépendances pour les projets Cocoa. CocoaPods et Carthage téléchargent automatiquement des artefacts depuis des référentiels et les mettent à la disposition de votre application. Sélectionnez CocoaPods ou Carthage :

#### CocoaPods
{: #cocoapods notoc}

1. Suivez les [instructions du logiciel SDK {{site.data.keyword.Bluemix_notm}} Mobile Services Swift ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods){: new_window} sur GitHub pour installer `BMSAnalytics` à l'aide de Cocoapods et l'ajouter à votre fichier Pod. 
	
2. Après avoir installé le logiciel SDK client iOS, [importez et initialisez](sdk.html#initalize-ma-sdk) le logiciel SDK client d'analyse.   

#### Carthage
{: #carthage notoc}

Si vous n'utilisez pas CocoaPods, vous pouvez ajouter des infrastructures à votre projet à l'aide de [Carthage ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}.

1. Suivez les [instructions d'installation de Carthage ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage){: new_window} sur GitHub pour installer `BMSAnalytics`.

2. Après avoir installé le logiciel SDK client iOS, [importez et initialisez](sdk.html#initalize-ma-sdk) le logiciel SDK client d'analyse.

## Installation du plug-in Cordova
{: #installing-sdk-cordova}

Le plug-in Cordova {{site.data.keyword.mobileanalytics_full}} vous permet d'instrumenter votre application mobile. 

1. Créez un projet [Cordova ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://cordova.apache.org/#getstarted){: new_window} ou ouvrez un projet existant.

2. Ajoutez les plateformes Android et iOS à votre application Cordova. Exécutez l'une des commandes suivantes ou les deux à partir de la ligne de commande. Actuellement, Cordova-CLI version 6.3.0, ou antérieure, est pris en charge  :
   
   Android :

	 ```
	 cordova platform add android@5.2.2
	 ```
	 {: codeblock}
	
   iOS :
   	
	```
	cordova platform add ios
	```
   {: codeblock}
	
3. Si vous avez ajouté la plateforme Android, vous devez ajouter le niveau d'API minimal pris en charge au fichier `config.xml` de votre application Cordova. Ouvrez le fichier `config.xml` et ajoutez la ligne suivante à l'élément `<platform name="android">` :

	```
	<platform name="android">  
  	 <preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	 <!-- add minimum and target Android API level declaration -->
  	</platform>
	```
   {: codeblock}

 La valeur *minSdkVersion* doit être la version `15` ou une version ultérieure. Reportez-vous au manuel [Android Platform Guide ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window} pour connaître la version *targetSdkVersion* actuelle prise en charge pour le SDK Android.

4. Si vous avez ajouté le système d'exploitation iOS, déclarez une cible dans l'élément `<platform name="ios">` :

	```
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  	</platform>
	```
	{: codeblock}

5. Ajoutez le plug-in `bms-core`.
 	
	 ```
	 cordova plugin add bms-core
	 ```
	 {: codeblock}

6. Vérifiez que le plug-in a été installé correctement à l'aide de la commande suivante :
	
	```
	cordova plugin list
	```
	{: codeblock}
	
7. [Configurez votre environnement Android et iOS ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com/package/bms-core#4-configuring-your-platform){: new_window}.

8. Vous avez maintenant installé le plug-in Cordova et configuré vos environnements. A présent, [importez et initialisez](sdk.html#initalize-ma-sdk) le logiciel SDK client d'analyse.

# Liens connexes
{: #rellinks notoc}

## Logiciel SDK
{: #sdk notoc}
* [Logiciel SDK Android ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [Logiciel SDK iOS ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Logiciel SDK Core du plug-in Cordova ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.npmjs.com/package/bms-core){: new_window}

## Référence d'API
{: #api notoc}
* [API REST ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
