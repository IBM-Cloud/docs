---

copyright:
  years: 2015, 2016

---

# Installazione di {{site.data.keyword.mobileanalytics_short}}
SDK client
{: #mobileanalytics_sdk}
*Ultimo aggiornamento: 21 aprile 2016*
{: .last-updated}

Gli SDK client {{site.data.keyword.mobileanalytics_short}}
sono attualmente disponibili per Android, iOS e WatchOS.
{: #shortdesc}

## Installazione dell'SDK client Android
{: #install-sdk-android}

L'SDK client {{site.data.keyword.mobileanalytics_short}} viene distribuito con Gradle, un gestore dipendenze per i progetti Android. Gradle scarica automaticamente le risorse dai repository e le rende disponibili alla tua applicazione Android.

1. Crea un progetto [Android Studio](http://developer.android.com/sdk/index.html) o apri un progetto esistente.

2. Apri il file `build.gradle` che si trova nel tuo modulo dell'applicazione.

  **Suggerimento**: il tuo progetto Android potrebbe avere due file `build.gradle`: uno per il progetto e uno per il modulo dell'applicazione. Accertati di utilizzare il file del **modulo dell'applicazione**.

3. Trova la sezione `Dependencies` del file `build.gradle` e aggiungi una dipendenza di compilazione per l'SDK
client {{site.data.keyword.mobileanalytics_short}} nel seguente modo:

  ```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
      name:'analytics',
      version: '1.+',
      ext: 'aar',
      transitive: true
  ```
  {: codeblock}

  La tua istruzione relativa ai repository dovrebbe essere simile a questo esempio di codice:

	```Gradle
      dependencies {
        compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
          name:'analytics',
          version: '1.+',
          ext: 'aar',
          transitive: true
    	// altre dipendenze  
      }
  ```
  {: screen}

4. Sincronizza il tuo progetto con Gradle facendo clic su **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Apri il file `AndroidManifest.xml` per il tuo progetto Android e aggiungi l'autorizzazione di accesso a Internet sotto
l'elemento `<manifest>`:

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}


## Installazione dell'SDK Swift
{: #installing-sdk-ios}

L'SDK {{site.data.keyword.mobileanalytics_full}} ti consente di strumentare la tua applicazione mobile. L'SDK Swift è disponibile per iOS e watchOS.

### Prima di iniziare
{: #before-you-begin-ios}

Accertati di avere impostato correttamente Xcode. Per informazioni su come impostare il tuo ambiente di sviluppo iOS, visita il [sito web per gli sviluppatori Apple](https://developer.apple.com/support/xcode/).

L'SDK {{site.data.keyword.mobileanalytics_short}} viene distribuito con [Cocoapods](https://cocoapods.org/) e [Carthage](https://github.com/Carthage/Carthage#getting-started), che sono gestori dipendenze per i progetti Cocoa. CocoaPods e Carthage scaricano automaticamente le risorse dai repository e le rendono disponibili alla tua applicazione.

#### Cocoapods
{: #cocoapods}
1. Se CocoaPods non è installato, esegui:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}

2. Se non hai già inizializzato il tuo spazio di lavoro per CocoaPods, esegui il comando `pod init` nella directory root del tuo progetto. CocoaPods crea un file `Podfile` per tuo conto, che è dove definisci le dipendenze per il tuo progetto Xcode.

3. Aggiungi il pod `BMSAnalytics` alla destinazione nel tuo Podfile, ad esempio:

	### iOS

  ```
  use_frameworks!

  target 'MyApp' do
     platform :ios, '8.0'
     pod 'BMSAnalytics'
  end
  ```

4. Salva il file `Podfile` ed esegui `pod install` dalla riga di comando.

5. Apri lo spazio di lavoro del tuo progetto Xcode utilizzando il file `.xcworkspace` che era stato generato da CocoaPods.

#### Carthage
{: #carthage}

Aggiungi i framework al tuo progetto utilizzando [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Aggiungi i framework `BMSAnalytics` al tuo Cartfile:
  ```
  github "ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics"
  ```
2. Esegui il comando `carthage update`. Al termine della build, trascina `BMSAnalytics.framework`, `BMSCore.framework` e `BMSAnalyticsAPI.framework` nel tuo progetto Xcode.
3. Attieniti alle istruzioni sul sito di [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) per completare
l'integrazione.

# rellinks

## SDK
* [SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Riferimento API
{: #api}
* [API REST](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
