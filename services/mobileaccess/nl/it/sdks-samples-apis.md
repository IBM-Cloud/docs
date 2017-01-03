---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-25"

---
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# {{site.data.keyword.amashort}} SDK, esempi e guida di riferimento alle API


Per aggiungere delle SDK {{site.data.keyword.amafull}} alla tua applicazione client, scegli quelli che vuoi utilizzare. Quindi configura il tuo gestore dipendenze per inserire gli SDK nella tua applicazione.
{:shortdesc}

**Nota:** le seguenti sezioni forniscono ulteriori informazioni sull'installazione degli SDK.

## SDK Core
{: #coresdk}

L'SDK Core include le API per abilitare l'autenticazione e l'accesso personalizzati.

### Android
{: #coresdk-android}

[Repository GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Installa l'SDK Core con Gradle
{: #coresdk-android-gradle}

Aggiungi una dipendenza di compilazione per il file `build.gradle` della tua applicazione:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (SDK Swift)
{: #coresdk-ios-swift}

[Repository GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### Installa l'SDK Core con CocoaPods
{: #coresdk-ios-siwft-cocoapods}
Modifica il file Podfile e aggiungi la seguente riga alle destinazioni richieste:

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}

### iOS (SDK Objective-C)
{: #coresdk-ios}

Mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix_notm}}, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift (consulta [Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html)).

[Repository Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Installa l'SDK Core con CocoaPods
{: #coresdk-ios-cocoapods}

Modifica il file Podfile e aggiungi la seguente riga alle destinazioni richieste:
```Bash
pod 'IMFCore'
```
{: codeblock}

### Cordova
{: #coresdk-cordova}

[Repository GitHub e Guida di riferimento API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installa l'SDK Core con la CLI Cordova
{: #coresdk-cordova-cli}

Installa il plugin Mobile Client Access Cordova:
```Bash
cordova plugin add bms-core
```
{: codeblock}

## SDK client per l'autenticazione Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Repository GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Installa l'SDK Facebook con Gradle
{: #facebooksdk-android-gradle}

Aggiungi una dipendenza di compilazione per il file `build.gradle` della tua applicazione:
```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (SDK Swift)
{: #facebooksdk-ios-swift}

[Repository GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Installa l'SDK Facebook con CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

Modifica il file Podfile e aggiungi quanto segue alle destinazioni richieste:
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}

### iOS (SDK Objective-C)
{: #facebooksdk-ios}

[Repository Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

**Nota:** mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix_notm}}, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift. Per le nuove applicazioni consigliamo caldamente di utilizzare l'SDK Swift (consulta Configurazione dell'SDK Swift iOS).
#### Installa l'SDK Facebook con CocoaPods
{: #facebooksdk-ios-cocoapods}

Modifica il Podfile, aggiungi la seguente riga ed esegui:

```Bash
pod 'IMFFacebookAuthentication'
```
{: codeblock}

### Cordova
{: #facebooksdk-cordova}

[Repository GitHub e Guida di riferimento API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installa l'SDK Facebook con la CLI Cordova
{: #facebooksdk-cordova-cli}

Installa il plugin Cordova:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## SDK client per l'autenticazione Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Repository GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Installa l'SDK Google+ con Gradle
{: #googlesdk-android-gradle}

Aggiungi una dipendenza di compilazione per il file `build.gradle` della tua applicazione:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (SDK Swift)
{: #googlesdk-ios-swift}

[Repository GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Installa l'SDK Google+ con CocoaPods
{: #googlesdk-ios-swift-cocoapods}

Modifica il Podfile, aggiungi quanto segue ed esegui:

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}

### iOS (SDK Objective-C - obsoleto)
{: #googlesdk-ios}

[Repository Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Installa l'SDK Google+ con CocoaPods
{: #googlesdk-ios-cocoapods}

Modifica il Podfile, aggiungi la seguente riga ed esegui:

```Bash
pod 'IMFGoogleAuthentication'
```
{: codeblock}

### Cordova
{: #googlesdk-cordova}

[Repository GitHub e Guida di riferimento API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installa l'SDK Google+ con la CLI Cordova
{: #googlesdk-cordova-cli}

Installa il plugin:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## SDK server per server Node.js
{: #serversdk}

[Repository GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Installa l'SDK server con npm
{: #serversdk-npm}

Esegui NPM per installare l'SDK:

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## SDK server per il server Liberty for Java&trade;
{: #serverlibertysdk}

[Scarica risorse utente TAI](https://imf-tai.{DomainName}/public/TAI.zip)

#### Installa l'SDK Liberty
{: #libertysdk}

1. Copia il file `com.ibm.worklight.oauth.tai_1.0.0.jar` nella directory `$<wlp.user.dir>/extensions/lib`.

  **Suggerimento: ** `$<wlp.user.dir>` è la directory utente per il runtime Liberty for Java. Il nome directory predefinito è `usr`.

1. Copia la directory `OAuthTai-1.0.mf` nella directory `$<wlp.user.dir>/extension/lib/features`.


## SDK Node.js OAuth
{: #serverlibertysdk-github}

[Repository GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Installa l'SDK OAuth con npm
{: #oauthsdk}

Esegui NPM per installare l'SDK:
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Esempi del provider di identità personalizzato
{: #customidprovider}

[Semplice repository GitHub di esempio](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)

[Avanzato repository GitHub di esempio](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Installa l'IMFURLProtocol con CocoaPods
{: #IMFURLProtocol-cocoapods}

Modifica il Podfile, aggiungi la seguente riga ed esegui:

```Bash
pod 'IMFURLProtocol'
```
{: codeblock}
