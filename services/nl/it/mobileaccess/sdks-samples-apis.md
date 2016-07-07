---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# SDK {{site.data.keyword.amashort}}, esempi e guida di riferimento API
*Ultimo aggiornamento: 30 aprile 2016*
{: .last-updated}

Per aggiungere degli SDK {{site.data.keyword.amashort}} alla tua applicazione, scegli quelli che vuoi utilizzare e configura quindi il tuo gestore dipendenze per inserire gli SDK nella tua applicazione.
{:shortdesc}

## SDK Core
{: #coresdk}
L'SDK Core include le API per abilitare l'autenticazione personalizzata, il monitoraggio e la registrazione in log nella tua applicazione mobile.

### Android
{: #coresdk-android}
[Repository Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Installa l'SDK Core con Gradle
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (SDK Swift)
{: #coresdk-ios-swift}

[Repository Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### Installa l'SDK Core con CocoaPods
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSSecurity'
```

### iOS (SDK Objective-C)
{: #coresdk-ios}

Mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix_notm}}, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift (consulta [Configurazione dell'SDK Swift iOS](getting-started-ios-swift-sdk.html)).

[Repository Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Installa l'SDK Core con CocoaPods
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Repository Git e guida di riferimento API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installa l'SDK Core con la CLI Cordova
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK client {{site.data.keyword.amashort}} per l'autenticazione Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Repository Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Installa l'SDK Facebook con Gradle
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (SDK Swift)
{: #facebooksdk-ios-swift}

[Repository Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Installa l'SDK Facebook con CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (SDK Objective-C)
{: #facebooksdk-ios}

[Repository Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

*Nota:* mentre la SDK Objective-C SDK rimane completamente supportata ed è ancora considerata la SDK primaria per i servizi mobili {{site.data.keyword.Bluemix_notm}}, è pianificato di abbandonarla più avanti questo anno in favore della nuova SDK Swift. Per le nuove applicazioni consigliamo caldamente di utilizzare l'SDK Swift (consulta Configurazione dell'SDK Swift iOS).
#### Installa l'SDK Facebook con CocoaPods
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Repository Github e Guida di riferimento API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installa l'SDK Facebook con la CLI Cordova
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK client {{site.data.keyword.amashort}} per l'autenticazione Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Repository Github](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Installa l'SDK Google+ con Gradle
{: #googlesdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (SDK Swift)
{: #googlesdk-ios-swift}

[Repository Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Installa l'SDK Google+ con CocoaPods
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (SDK Objective-C - obsoleto)
{: #googlesdk-ios}

[Repository Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Installa l'SDK Google+ con CocoaPods
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Repository Git e guida di riferimento API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installa l'SDK Google+ con la CLI Cordova
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK server {{site.data.keyword.amashort}} per server Node.js
{: #serversdk}

[Repository Git](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Installa l'SDK server con npm
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## SDK server {{site.data.keyword.amashort}} per il server Liberty for Java&trade;
{: #serverlibertysdk}

[Scarica risorse utente TAI](https://imf-tai.{DomainName}/public/TAI.zip)

## SDK OAuth Node.js {{site.data.keyword.amashort}}
{: #serverlibertysdk-github}

[Repository Git](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Installa l'SDK OAuth con npm
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## Esempi di provider di identità personalizzato
{: #customidprovider}

[Semplice repository Git di esempio](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[Avanzato repository Git di esempio](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[Guida di riferimento API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Installa IMFURLProtocol con CocoaPods
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
