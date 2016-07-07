---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# SDK, ejemplos y referencias de API de {{site.data.keyword.amashort}}
*Última actualización: 30 de abril de 2016*
{: .last-updated}

Para añadir SDK de {{site.data.keyword.amashort}} a la aplicación, escoja los SDK que desea utilizar y configure el gestor de dependencias para transferir los SDK a la app.
{:shortdesc}

## Core SDK
{: #coresdk}
Core SDK principal incluye API para la habilitación de la autenticación personalizada, la supervisión y el registro de la app móvil.

### Android
{: #coresdk-android}
[Repositorio Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Instalación de Core SDK con Gradle
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (SDK de Swift)
{: #coresdk-ios-swift}

[Repositorio Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### Instalación de Core SDK con CocoaPods
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSSecurity'
```

### iOS (SDK de Objective-C)
{: #coresdk-ios}

Si bien el SDK de Objective-C recibe total soporte, y sigue considerándose el SDK principal para {{site.data.keyword.Bluemix_notm}} Mobile Services, está previsto que se deje de utilizar dentro de unos meses en favor del nuevo SDK de Swift (consulte [Configuración del SDK de Swift de iOS](getting-started-ios-swift-sdk.html)).

[Repositorio Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Instalación de Core SDK con CocoaPods
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Repositorio Git y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instalación de Core SDK con la CLI de Cordova
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK del cliente de {{site.data.keyword.amashort}} para la autenticación de Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Repositorio Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Instalación del SDK de Facebook con Gradle
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (SDK de Swift)
{: #facebooksdk-ios-swift}

[Repositorio Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Instalación del SDK de Facebook con CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (SDK de Objective-C)
{: #facebooksdk-ios}

[Repositorio Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

*Nota:* Si bien el SDK de Objective-C recibe total soporte y sigue considerándose como SDK principal para {{site.data.keyword.Bluemix_notm}} Mobile Services, está previsto dejar de mantener este SDK a finales del año en favor del nuevo SDK de Swift. Para las nuevas aplicaciones se recomienda utilizar el SDK de Swift (consulte Configuración del SDK de Swift para iOS).
#### Instalar el SDK de Facebook con CocoaPods
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Repositorio Github y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)
#### Instalar el SDK de Facebook con la CLI de Cordova
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK de cliente {{site.data.keyword.amashort}} para autenticación de Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Repositorio Github](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Instalar el SDK de Google+ con Gradle
{: #googlesdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (SDK de Swift)
{: #googlesdk-ios-swift}

[Repositorio Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Instalar el SDK de Google+ con CocoaPods
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (SDK de Objective-C, en desuso)
{: #googlesdk-ios}

[Repositorio Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Instalar el SDK de Google+ con CocoaPods
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Repositorio Git y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)
#### Instalar el SDK de Google+ con la CLI de Cordova
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK de servidor {{site.data.keyword.amashort}} para servidores Node.js
{: #serversdk}

[Repositorio Git](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Instalar el SDK de servidor con npm
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## SDK de servidor {{site.data.keyword.amashort}} para Liberty para servidor Java&trade;
{: #serverlibertysdk}

[Descargar artefactos TAI](https://imf-tai.{DomainName}/public/TAI.zip)

## SDK de OAuth para {{site.data.keyword.amashort}} Node.js
{: #serverlibertysdk-github}

[Repositorio Git](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Instalar el SDK de OAuth con npm
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## Ejemplos de proveedores de identidad personalizados
{: #customidprovider}

[Simple sample Git repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[Advanced sample Git repo](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Instalar IMFURLProtocol con CocoaPods
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
