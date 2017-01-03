---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-25"

---
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# {{site.data.keyword.amashort}} Logiciels SDK, exemples et référence d'API
Pour ajouter des SDK {{site.data.keyword.amafull}} à votre appli client, sélectionnez ceux que vous désirez utiliser. Configurez ensuite votre
gestionnaire de dépendances pour intégrer le SDK dans votre application.
{:shortdesc}

**Remarque :** Les sections ultérieures fournissent des informations supplémentaires sur l'installation des
SDK.

## SDK Core
{: #coresdk}

Le SDK de base inclut des API permettant d'activer l'authentification et la journalisation personnalisées.

### Android
{: #coresdk-android}

[Référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Installation du logiciel SDK Core avec Gradle
{: #coresdk-android-gradle}

Ajoutez une dépendance de compilation au fichier `build.gradle` de votre application :

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

[Référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### Installation du logiciel SDK Core avec CocoaPods
{: #coresdk-ios-siwft-cocoapods}
Editez le fichier Podfile en lui ajoutant la ligne suivante vers les cibles requises et exécutez :

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}

### iOS (SDK Objective-C)
{: #coresdk-ios}

Bien que le SDK Objective-C reste complètement pris en charge et soit toujours considéré comme le SDK principal pour
{{site.data.keyword.Bluemix_notm}} Mobile Services, il est envisagé de le retirer plus tard dans l'année et de le remplacer par le nouveau SDK
Swift. (voir
[Configuration du SDK Swift iOS](getting-started-ios-swift-sdk.html)).

[Référentiel Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Installation du logiciel SDK Core avec CocoaPods
{: #coresdk-ios-cocoapods}

Editez le fichier Podfile en lui ajoutant la ligne suivante vers les cibles requises et exécutez :
```Bash
pod 'IMFCore'
```
{: codeblock}

### Cordova
{: #coresdk-cordova}

[Référentiel GitHub et référence d'API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installation du logiciel SDK Core avec l'interface de ligne de commande Cordova
{: #coresdk-cordova-cli}

Installez le plug-in Mobile Client Access Cordova :
```Bash
cordova plugin add bms-core
```
{: codeblock}

## SDK client pour authentification Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Installation du logiciel SDK Facebook avec Gradle
{: #facebooksdk-android-gradle}

Ajoutez une dépendance de compilation au fichier `build.gradle` de votre application :
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

[Référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Installation du logiciel SDK Facebook avec CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

Editez le fichier Podfile en lui ajoutant la ligne suivante vers les cibles requises et exécutez :
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}

### iOS (SDK Objective-C)
{: #facebooksdk-ios}

[Référentiel Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

**Remarque :** Bien que le SDK Objective-C reste totalement pris en charge et soit toujours considéré comme SDK principal pour
{{site.data.keyword.Bluemix_notm}} Mobile Services, il est envisagé de le retirer plus tard cette année et de le remplacer par le nouveau SDK Swift. Dans le cas de nouvelles applications, il est fortement recommandé d'utiliser le SDK Swift (voir Configuration du SDK iOS
Swift).
#### Installation du logiciel SDK Facebook avec CocoaPods
{: #facebooksdk-ios-cocoapods}

Editez le fichier Podfile en lui ajoutant la ligne suivante et exécutez :

```Bash
pod 'IMFFacebookAuthentication'
```
{: codeblock}

### Cordova
{: #facebooksdk-cordova}

[Référentiel GitHub et référence d'API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installez le SDK Facebook avec l'interface CLI Cordova
{: #facebooksdk-cordova-cli}

Installez le plug-in Cordova :

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## SDK client pour authentification Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Installez le SDK Google+ avec Gradle
{: #googlesdk-android-gradle}

Ajoutez une dépendance de compilation au fichier `build.gradle` de votre application :

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

[Référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Installez le SDK Google+ avec CocoaPods
{: #googlesdk-ios-swift-cocoapods}

Editez le fichier Podfile en lui ajoutant la ligne suivante et exécutez :

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}

### iOS (Objective-C SDK - Obsolète)
{: #googlesdk-ios}

[Référentiel Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Installez le SDK Google+ avec CocoaPods
{: #googlesdk-ios-cocoapods}

Editez le fichier Podfile en lui ajoutant la ligne suivante et exécutez :

```Bash
pod 'IMFGoogleAuthentication'
```
{: codeblock}

### Cordova
{: #googlesdk-cordova}

[Référentiel GitHub et référence d'API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installez le SDK Google+ avec l'interface CLI de Cordova
{: #googlesdk-cordova-cli}

Installez le plug-in :

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## SDK serveur pour serveurs Node.js
{: #serversdk}

[Référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Installez le SDK serveur avec npm
{: #serversdk-npm}

Exécutez NPM pour installer le SDK :

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## SDK serveur pour serveur Liberty for Java&trade;
{: #serverlibertysdk}

[Téléchargez les artefacts TAI](https://imf-tai.{DomainName}/public/TAI.zip)

#### Installez le SDK Liberty
{: #libertysdk}

1. Copiez le fichier `com.ibm.worklight.oauth.tai_1.0.0.jar` dans le répertoire
`$<wlp.user.dir>/extensions/lib`.

  **Astuce :** `$<wlp.user.dir>` est
le répertoire utilisateur pour le contexte d'exécution Liberty for Java. So nom par défaut est `usr`.

1. Copiez le répertoire `OAuthTai-1.0.mf` dans le répertoire `$<wlp.user.dir>/extension/lib/features`.


## SDK OAuth Node.js
{: #serverlibertysdk-github}

[Référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Installez le SDK OAuth avec npm
{: #oauthsdk}

Exécutez NPM pour installer le SDK :
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Exemples de fournisseur d'identité personnalisé
{: #customidprovider}

[Exemple simple du référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)

[Exemple avancé du référentiel GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Installez IMFURLProtocol avec CocoaPods
{: #IMFURLProtocol-cocoapods}

Editez le fichier Podfile en lui ajoutant la ligne suivante et exécutez :

```Bash
pod 'IMFURLProtocol'
```
{: codeblock}
