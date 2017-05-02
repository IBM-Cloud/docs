---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Installazione degli SDK client {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Gli SDK client {{site.data.keyword.mobileanalytics_short}}
sono attualmente disponibili per Android, iOS, WatchOS e Cordova.
{: shortdesc}

## Installazione dell'SDK client Android
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

L'SDK client {{site.data.keyword.mobileanalytics_short}} viene distribuito con Gradle, un gestore dipendenze per i progetti Android. Gradle scarica automaticamente le risorse dai repository e le rende disponibili alla tua applicazione Android.

1. Crea un progetto [Android Studio ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://developer.android.com/sdk/index.html){: new_window} o apri un progetto esistente.

2. Apri il file `build.gradle` che si trova nel tuo **modulo dell'applicazione**.

  **Suggerimento**: il tuo progetto Android potrebbe avere due file `build.gradle`: uno per il progetto e uno per il modulo dell'applicazione. Accertati di utilizzare il file del **modulo dell'applicazione**.

3. Trova la sezione `Dependencies` del file `build.gradle` e aggiungi una dipendenza di compilazione per l'SDK client {{site.data.keyword.mobileanalytics_short}}. La tua istruzione relativa ai repository dovrebbe essere simile a questo esempio di codice:

	```
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// altre dipendenze
      }
  	```
  	{: codeblock}

4. Sincronizza il tuo progetto con Gradle facendo clic su **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Apri il file `AndroidManifest.xml` per il tuo progetto Android. Puoi trovare questo file in **app > manifests**. Aggiungi l'autorizzazione di accesso a Internet sotto l'elemento `<manifest>`:

	```
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
   
6. Hai ora installato l'SDK client Android. Successivamente, [importa e inizializza](sdk.html#initalize-ma-sdk) l'SDK client Analytics.   

## Installazione dell'SDK Swift
{: #installing-sdk-ios}

![CocoaPods Compatible](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

L'SDK {{site.data.keyword.mobileanalytics_full}} ti consente di strumentare la tua applicazione mobile. L'SDK Swift è disponibile per iOS e watchOS.

### Prima di iniziare
{: #before-you-begin-ios notoc}

Accertati di avere impostato correttamente Xcode. Per informazioni su come impostare il tuo ambiente di sviluppo iOS, visita il [sito Web Apple Developer ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/support/xcode/){: new_window}. Leggi le informazioni sui [requisiti Xcode ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements){: new_window} per Client SDK Swift Analytics.

L'SDK {{site.data.keyword.mobileanalytics_short}} viene distribuito con [CocoaPods ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://cocoapods.org/){: new_window} e [Carthage ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage#getting-started){: new_window}, che sono dei gestori delle dipendenze per i progetti Cocoa. CocoaPods e Carthage scaricano automaticamente le risorse dai repository e le rendono disponibili alla tua applicazione. Seleziona CocoaPods o Carthage:

#### CocoaPods
{: #cocoapods notoc}

1. Segui le istruzioni [{{site.data.keyword.Bluemix_notm}} Mobile Services Swift SDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods){: new_window} su GitHub per installare `BMSAnalytics` utilizzando Cocoapods e aggiungerlo al tuo Podfile. 
	
2. Dopo aver installato l'SDK client iOS, [importa e inizializza](sdk.html#initalize-ma-sdk) l'SDK client Analytics.   

#### Carthage
{: #carthage notoc}

Se non stai utilizzando CocoaPods, puoi aggiungere i framework al tuo progetto utilizzando [Carthage ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}.

1. Segui le istruzioni di installazione [Carthage ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage){: new_window} su GitHub per installare `BMSAnalytics`.

2. Dopo aver installato l'SDK client iOS, [importa e inizializza](sdk.html#initalize-ma-sdk) l'SDK client Analytics.

## Installazione del plug-in Cordova
{: #installing-sdk-cordova}

Il plug-in Cordova {{site.data.keyword.mobileanalytics_full}} ti consente di strumentare la tua applicazione mobile. 

1. Crea un progetto [Cordova ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://cordova.apache.org/#getstarted){: new_window} o apri un progetto esistente.

2. Aggiungi le piattaforme Android e iOS alla tua applicazione Cordova. Esegui uno o entrambi i seguenti comandi dalla riga di comando. Al momento, è supportata la CLI Cordova V6.3.0 o precedente:
   
   Android:

	 ```
	 cordova platform add android@5.2.2
	 ```
	 {: codeblock}
	
   iOS:
   	
	```
	cordova platform add ios
	```
   {: codeblock}
	
3. Se hai aggiunto la piattaforma Android, devi aggiungere il livello API minimo supportato al file `config.xml` della tua applicazione Cordova. Apri il file `config.xml` e aggiungi la seguente riga all'elemento `<platform name="android">`:

	```
	<platform name="android">  
  	 <preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	 <!-- add minimum and target Android API level declaration -->
  	</platform>
	```
   {: codeblock}

 Il valore *minSdkVersion* deve essere alla versione `15` o successiva. Fai riferimento alla [Android Platform Guide ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window} per restare aggiornato sulla *targetSdkVersion* supportata per l'SDK Android.

4. Se hai aggiunto il sistema operativo iOS, aggiorna l'elemento `<platform name="ios">` con una dichiarazione di destinazione:

	```
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  	</platform>
	```
	{: codeblock}

5. Aggiungi il plugin `bms-core`.
 	
	 ```
	 cordova plugin add bms-core
	 ```
	 {: codeblock}

6. Verifica che il plug-in sia stato installato correttamente eseguendo il seguente comando:
	
	```
	cordova plugin list
	```
	{: codeblock}
	
7. [Configura il tuo ambiente Android e iOS ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.npmjs.com/package/bms-core#4-configuring-your-platform){: new_window}.

8. Hai ora installato il plug-in Cordova e configurato i tuoi ambienti. Successivamente, [importa e inizializza](sdk.html#initalize-ma-sdk) l'SDK client Analytics.

# Link correlati
{: #rellinks notoc}

## SDK
{: #sdk notoc}
* [SDK Android ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova Plugin Core SDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.npmjs.com/package/bms-core){: new_window}

## Riferimento API
{: #api notoc}
* API REST [ ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
