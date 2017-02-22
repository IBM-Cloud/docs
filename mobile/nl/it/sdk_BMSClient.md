---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:codeblock:.codeblock}

# Inizializzazione di BMSClient
{: #sdk_BMSClient}

`BMSCore` fornisce l'infrastruttura HTTP che le altre SDK client dei servizi {{site.data.keyword.Bluemix}} Mobile utilizzano per comunicare con i loro servizi {{site.data.keyword.Bluemix_notm}} corrispondenti.


## Inizializzazione della tua applicazione Android
{: #init-BMSClient-android}

Puoi sia scaricare che importare il pacchetto `BMSCore` del tuo progetto Android Studio o utilizzare Gradle.

1. Importa l'SDK client aggiungendo la seguente istruzione `import` all'inizio del file del progetto:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
  ```
  {: codeblock}

2. Inizializza l'SDK `BMSClient` nella tua applicazione Android aggiungendo il codice di inizializzazione nel metodo `onCreate` dell'attività principale nell'applicazione Android o in un'ubicazione che ritieni più adatta per il tuo progetto.

  ```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Assicurati che punti alla tua regione
  ```
  {: codeblock}

  Devi inizializzare il `BMSClient` con il parametro **bluemixRegion**. Nel programma di inizializzazione, il valore **bluemixRegion** specifica quale distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`.


## Inizializzazione della tua applicazione iOS
{: #init-BMSClient-ios}

Puoi utilizzare [CocoaPods](https://cocoapods.org){: new_window} o [Carthage](https://github.com/Carthage/Carthage){: new_window} per ottenere il pacchetto `BMSCore`.

1. Per installare `BMSCore` utilizzando CocoaPods, aggiungi le seguenti linee al tuo Podfile. Se il tuo progetto non dispone ancora di un Podfile, utilizza il comando `pod init`.

  ```Swift
  use_frameworks!

  target 'MyApp' do
    pod 'BMSCore'
  end
  ```
  {: codeblock}

  Quindi esegui il comando `pod install` e apri il file `.xcworkspace` generato. Per l'aggiornamento a una release più recente di `BMSCore`, utilizza `pod update BMSCore`.

  Per ulteriori informazioni sull'utilizzo di CocoaPods, consulta [CocoaPods Guides ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://guides.cocoapods.org/using/index.html "Icona link esterno"){: new_window}.

2. Per installare `BMSCore` utilizzando Carthage, segui queste [istruzioni ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Carthage/Carthage#getting-started "Icona link esterno"){: new_window}.

  1. Aggiungi la seguente linea al tuo Cartfile:

      ```
      github "ibm-bluemix-mobile-services/bms-clientsdk-swift-core"
      ```
      {: codeblock}

  2. Esegui il comando `carthage update`.

  3. Dopo aver terminato la build, aggiungi `BMSCore.framework` al tuo progetto seguendo il [Passo 3 ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/Carthage/Carthage#getting-started "Icona link esterno") nelle istruzioni Carthage.

      Per le applicazioni che sono generate con Swift 2.3, utilizza il comando `carthage update --toolchain com.apple.dt.toolchain.Swift_2_3`. Altrimenti, utilizza il comando `carthage update`.

3. Importa il modulo.

  ```Swift
  import BMSCore
  ```
  {: codeblock}

4. Inizializza la classe `BMSClient`, utilizzando il seguente codice.

  Posiziona il codice di inizializzazione nel metodo `application(_:didFinishLaunchingWithOptions:)` nel tuo delegato dell'applicazione o in un'ubicazione che ritieni più adatta per il tuo progetto.

  ```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Assicurati che punti alla tua regione
  ```
  {: codeblock}

  Devi inizializzare il `BMSClient` con il parametro **bluemixRegion**. Nel programma di inizializzazione, il valore **bluemixRegion** specifica quale distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`.


## Inizializzazione della tua applicazione Cordova
{: #init-BMSClient-cordova}

1. Aggiungi il plugin Cordova eseguendo questo comando dalla directory root della tua applicazione Cordova:

  ```
  cordova plugin add bms-core
  ```
  {: codeblock}

2. Inizializza la classe `BMSClient` nella tua applicazione Cordova aggiungendo il codice di inizializzazione nel file JavaScript principale o in un'ubicazione che ritieni più adatta per il tuo progetto.

  ```
  BMSClient.initialize(BMSClient.REGION_US_SOUTH);
  ```
  {: codeblock}
	
  Devi inizializzare il `BMSClient` con il parametro **bluemixRegion**. Nel programma di inizializzazione, il valore **bluemixRegion** specifica quale distribuzione {{site.data.keyword.Bluemix_notm}} stai utilizzando, ad esempio `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`.


# Link correlati
{: #rellinks}

## Link correlati
{: #general}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova Plugin](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
