---

Copyright : 2015, 2016

---

{:shortdesc: .shortdesc}

# Logiciels SDK, exemples et référence d'API de {{site.data.keyword.amashort}}
Pour ajouter des SDK {{site.data.keyword.amashort}} à votre appli, sélectionnez ceux que vous voulez utiliser, puis configurez votre gestionnaire de dépendances pour qu'il les insère dans votre appli.

## SDK Core
{: #coresdk}
Le SDK Core comprend des API permettant l'activation de l'authentification personnalisée, de la surveillance et de la journalisation dans les appli mobiles.

### Android
{: #coresdk-android}
[Référentiel Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Installation du logiciel SDK Core avec Gradle
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

[Référentiel Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)

#### Installation du logiciel SDK Core avec CocoaPods
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSCore'
```

### iOS (SDK Objective-C)
{: #coresdk-ios}

[Référentiel Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Installation du logiciel SDK Core avec CocoaPods
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Référentiel Git et référence d'API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installation du logiciel SDK Core avec l'interface de ligne de commande Cordova
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK client de {{site.data.keyword.amashort}} pour l'authentification Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Référentiel Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Installation du logiciel SDK Facebook avec Gradle
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

[Référentiel Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Installation du logiciel SDK Facebook avec CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (SDK Objective-C)
{: #facebooksdk-ios}

[Référentiel Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

#### Installation du logiciel SDK Facebook avec CocoaPods
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Référentiel Github et référence d'API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installation du logiciel SDK Facebook avec l'interface de ligne de commande Cordova
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK client de {{site.data.keyword.amashort}} pour l'authentification Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Référentiel Github](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Installation du logiciel SDK Google+ avec Gradle
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

[Référentiel Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Installation du logiciel SDK Google+ avec CocoaPods
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (SDK Objective-C)
{: #googlesdk-ios}

[Référentiel Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Installation du logiciel SDK Google+ avec CocoaPods
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Référentiel Git et référence d'API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Installation du logiciel SDK Google+ avec l'interface de ligne de commande Cordova
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## Logiciel SDK serveur de {{site.data.keyword.amashort}} pour les serveurs Node.js
{: #serversdk}

[Référentiel Git](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Installation du logiciel SDK serveur avec npm
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## SDK serveur de {{site.data.keyword.amashort}} pour serveur Liberty for Java&trade;
{: #serverlibertysdk}

[Téléchargez les artefacts TAI](https://imf-tai.{DomainName}/public/TAI.zip)

## Logiciel SDK OAuth Node.js de {{site.data.keyword.amashort}}
{: #serverlibertysdk-github}

[Référentiel Git](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Installation du logiciel SDK OAuth avec npm
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## Exemples de fournisseur d'identité personnalisé
{: #customidprovider}

[Simple sample Git repo (Référentiel Git d'exemples
simples)](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[Advanced sample Git repo (Référentiel Git
d'exemples avancés)](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[Référence d'API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Installation d'IMFURLProtocol avec CocoaPods
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
