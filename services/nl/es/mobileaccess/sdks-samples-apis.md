---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDK, ejemplos y referencia de API
*Última actualización: 17 de julio de 2016*
{: .last-updated}

Para añadir SDK de {{site.data.keyword.amashort}} a la aplicación, escoja los SDK que desea utilizar. A continuación, configure el gestor de dependencia para extraer los SDK en la aplicación.
{:shortdesc}

**Nota:** En las secciones siguientes se proporciona información adicional sobre la instalación de los SDK.

## Core SDK
{: #coresdk}

Core SDK incluye API para la habilitación de la autenticación personalizada, el registro y la supervisión de la app móvil.

### Android
{: #coresdk-android}

[Repositorio GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Instalación de Core SDK con Gradle
{: #coresdk-android-gradle}

Añada una dependencia de compilación al archivo `build.gradle` de la app:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (SDK de Swift)
{: #coresdk-ios-swift}

[Repositorio GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### Instalación de Core SDK con CocoaPods
{: #coresdk-ios-siwft-cocoapods}
Edite el Podfile y añada la siguiente línea a los destinos necesarios y ejecute:

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

Edite el Podfile y añada la siguiente línea a los destinos necesarios y ejecute:
```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Repositorio GitHub y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instalación de Core SDK con la CLI de Cordova
{: #coresdk-cordova-cli}

Instale el plug-in de Cordova Mobile Client Access:
```Bash
cordova plugin add ibm-mfp-core
```

## SDK del cliente para la autenticación de Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Repositorio GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Instalación del SDK de Facebook con Gradle
{: #facebooksdk-android-gradle}

Añada una dependencia de compilación al archivo `build.gradle` de la app:
```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (SDK de Swift)
{: #facebooksdk-ios-swift}

[Repositorio GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Instalación del SDK de Facebook con CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

Edite el Podfile y añada lo siguiente a los destinos necesarios y ejecute:
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (SDK de Objective-C)
{: #facebooksdk-ios}

[Repositorio Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

*Nota:* Si bien el SDK de Objective-C recibe total soporte y sigue considerándose como SDK principal para {{site.data.keyword.Bluemix_notm}} Mobile Services, está previsto dejar de mantener este SDK a finales del año en favor del nuevo SDK de Swift. Para las nuevas aplicaciones se recomienda utilizar el SDK de Swift (consulte Configuración del SDK de Swift para iOS).
#### Instalación del SDK de Facebook con CocoaPods
{: #facebooksdk-ios-cocoapods}

Edite el Podfile y añada la siguiente línea y ejecute:

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Repositorio GitHub y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instalación del SDK de Facebook con la CLI de Cordova
{: #facebooksdk-cordova-cli}

Instalación del plug-in de Cordova:

```Bash
cordova plugin add ibm-mfp-core
```

## SDK del cliente para la autenticación de Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Repositorio GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Instalación del SDK de Google+ con Gradle
{: #googlesdk-android-gradle}

Añada una dependencia de compilación al archivo `build.gradle` de la app:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (SDK de Swift)
{: #googlesdk-ios-swift}

[Repositorio GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Instalación del SDK de Google+ con CocoaPods
{: #googlesdk-ios-swift-cocoapods}

Edite el Podfile y añada lo siguiente y ejecute:

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (SDK de Objective-C, en desuso)
{: #googlesdk-ios}

[Repositorio Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Instalación del SDK de Google+ con CocoaPods
{: #googlesdk-ios-cocoapods}

Edite el Podfile y añada la siguiente línea y ejecute:

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Repositorio GitHub y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instalación del SDK de Google+ con la CLI de Cordova
{: #googlesdk-cordova-cli}

Instalación del plug-in:

```Bash
cordova plugin add ibm-mfp-core
```

## SDK del servidor para servidores de Node.js
{: #serversdk}

[Repositorio GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Instalación del SDK del servidor con npm
{: #serversdk-npm}

Ejecute NPM para instalar el SDK:

```Bash
npm install -save bms-mca-token-validation-strategy
```

## SDK de servidor para servidor de Liberty for Java&trade;
{: #serverlibertysdk}

[Descargue artefactos TAI](https://imf-tai.{DomainName}/public/TAI.zip)

#### Instalación del SDK de Liberty
{: #libertysdk}
1. Copie el archivo `com.ibm.worklight.oauth.tai_1.0.0.jar` en el directorio `$<wlp.user.dir>/extensions/lib`.

**Sugerencia:** `$<wlp.user.dir>` es el directorio de usuario para el tiempo de ejecución de Liberty for Java. El nombre por defecto del directorio es `usr`.

1. Copie el directorio `OAuthTai-1.0.mf` en el directorio `$<wlp.user.dir>/extension/lib/features`.


## SDK de OAuth de Node.js
{: #serverlibertysdk-github}

[Repositorio GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Instalación del SDK OAuth con npm
{: #oauthsdk}

Ejecute NPM para instalar el SDK:
```Bash
npm install -save bms-mca-oauth-sdk
```

## Ejemplos de proveedor de identidad personalizado
{: #customidprovider}

[Repositorio GitHub de ejemplo simple](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[Repositorio GitHub de ejemplo avanzado](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[Referencia de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Instalación de IMFURLProtocol con CocoaPods
{: #IMFURLProtocol-cocoapods}

Edite el Podfile y añada la siguiente línea y ejecute:

```Bash
pod 'IMFURLProtocol'
```
