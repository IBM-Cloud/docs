---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-18"

---

# Installazione degli SDK client {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Ultimo aggiornamento: 18 ottobre 2016
{: .last-updated}

Gli SDK client {{site.data.keyword.mobileanalytics_short}}
sono attualmente disponibili per Android, iOS e WatchOS.
{: #shortdesc}

## Installazione dell'SDK client Android
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)(https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)]

L'SDK client {{site.data.keyword.mobileanalytics_short}} viene distribuito con Gradle, un gestore dipendenze per i progetti Android. Gradle scarica automaticamente le risorse dai repository e le rende disponibili alla tua applicazione Android.

1. Crea un progetto [Android Studio](http://developer.android.com/sdk/index.html) o apri un progetto esistente.

2. Apri il file `build.gradle` che si trova nel tuo **modulo dell'applicazione**.

  **Suggerimento**: il tuo progetto Android potrebbe avere due file `build.gradle`: uno per il progetto e uno per il modulo dell'applicazione. Accertati di utilizzare il file del **modulo dell'applicazione**. 

3. Trova la sezione `Dependencies` del file `build.gradle` e aggiungi una dipendenza di compilazione per l'SDK client {{site.data.keyword.mobileanalytics_short}}. La tua istruzione relativa ai repository dovrebbe essere simile a questo esempio di codice:

	```Gradle
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// altre dipendenze
      }
  ```
  {: codeblock}

4. Sincronizza il tuo progetto con Gradle facendo clic su **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Apri il file `AndroidManifest.xml` per il tuo progetto Android. Puoi trovare questo file in **app > manifests**. Aggiungi l'autorizzazione di accesso a Internet sotto l'elemento `<manifest>`: 

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
6. Hai ora installato l'SDK client Android. Successivamente, [Importa e inizializza](sdk.html#initalize-ma-sdk-android) l'SDK client Analytics.   

## Installazione dell'SDK Swift
{: #installing-sdk-ios}

![CocoaPods Compatible](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

L'SDK {{site.data.keyword.mobileanalytics_full}} ti consente di strumentare la tua applicazione mobile. L'SDK Swift è disponibile per iOS e watchOS.

### Prima di iniziare
{: #before-you-begin-ios}

Accertati di avere impostato correttamente Xcode. Per informazioni su come impostare il tuo ambiente di sviluppo iOS, visita il [sito web per gli sviluppatori Apple](https://developer.apple.com/support/xcode/). Leggi ulteriori informazioni sui [Xcode requirements](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements) per l'SDK client Swift Analytics.

L'SDK {{site.data.keyword.mobileanalytics_short}} viene distribuito con [CocoaPods](https://cocoapods.org/) e [Carthage](https://github.com/Carthage/Carthage#getting-started), che sono gestori dipendenze per i progetti Cocoa. CocoaPods e Carthage scaricano automaticamente le risorse dai repository e le rendono disponibili alla tua applicazione.

#### CocoaPods
{: #cocoapods}

1. Se CocoaPods non è installato, esegui:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}
    
    Per Xcode 8: `sudo gem install cocoapods --pre`
    
   Assicurati di disporre dell'ultima versione di `BMSAnalytics` aggiornando il tuo repository CocoaPods locale, nel seguente modo:
   
    ```
    pod repo update master
    ```
    {: codeblock}

2. Segui le istruzioni [{{site.data.keyword.Bluemix_notm}} Mobile Services Swift SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods) in GitHub.
	
3. Dopo aver installato l'SDK client iOS, [Importa e inizializza](sdk.html#init-ma-sdk-ios) l'SDK client Analytics.   

#### Carthage
{: #carthage}

Aggiungi i framework al tuo progetto utilizzando [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Segui le istruzioni di installazione [Carthage](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage) in GitHub.

2. Dopo aver installato l'SDK client iOS, [Importa e inizializza](sdk.html#init-ma-sdk-ios) l'SDK client Analytics.

# rellinks

## SDK
* [SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Riferimento API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
