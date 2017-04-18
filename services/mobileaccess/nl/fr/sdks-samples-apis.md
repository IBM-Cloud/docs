---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


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

[Référentiel GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "Icône de lien externe"){: new_window}

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

[Référentiel GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security "Icône de lien externe"){: new_window}

#### Installation du logiciel SDK Core avec CocoaPods
{: #coresdk-ios-siwft-cocoapods}
Editez le fichier Podfile en lui ajoutant la ligne suivante vers les cibles requises et exécutez :

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}


### Cordova
{: #coresdk-cordova}

[Référence du référentiel GitHub et d'API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core "Icône de lien externe"){: new_window}

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

[Référentiel GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication "Icône de lien externe "){: new_window},

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

[Référentiel GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication "Icône de lien externe"){: new_window}

#### Installation du logiciel SDK Facebook avec CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

Editez le fichier Podfile en lui ajoutant la ligne suivante vers les cibles requises et exécutez :
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}


### Cordova
{: #facebooksdk-cordova}

[Référence du référentiel GitHub et d'API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core "Icône de lien externe"){: new_window}

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

[Référentiel GitHub r![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication "Icône de lien externe "){: new_window},


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

[Référentiel GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication "Icône de lien externe"){: new_window}

#### Installez le SDK Google+ avec CocoaPods
{: #googlesdk-ios-swift-cocoapods}

Editez le fichier Podfile en lui ajoutant la ligne suivante et exécutez :

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}


### Cordova
{: #googlesdk-cordova}

[Référence du référentiel GitHub et d'API![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core "Icône de lien externe"){: new_window}

#### Installez le SDK Google+ avec l'interface CLI de Cordova
{: #googlesdk-cordova-cli}

Installez le plug-in :

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## SDK serveur pour serveurs Node.js
{: #serversdk}

[Référentiel GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy "Icône de lien externe"){: new_window}

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

[Référentiel GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk "Icône de lien externe"){: new_window}

#### Installez le SDK OAuth avec npm
{: #oauthsdk}

Exécutez NPM pour installer le SDK :
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Exemples de fournisseur d'identité personnalisé
{: #customidprovider}

[Exemple simple de référentiel GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Icône de lien externe"){: new_window}

[Exemple avancé de référentiel GitHub ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "Icône de lien externe"){: new_window}


