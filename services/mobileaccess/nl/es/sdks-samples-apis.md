---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

El servicio {{site.data.keyword.amafull}} se sustituye por el servicio {{site.data.keyword.appid_full}}.

# {{site.data.keyword.amashort}} SDK, ejemplos y referencia de API
Para añadir SDK de {{site.data.keyword.amafull}} a la app de cliente, escoja los SDK que desea utilizar. A continuación, configure el gestor de dependencia para extraer los SDK en la aplicación.
{:shortdesc}

**Nota:** En las secciones siguientes se proporciona información adicional sobre la instalación de los SDK.

## Core SDK
{: #coresdk}

Core SDK incluye las API necesarias para la habilitación de la autenticación y el registro personalizados.

### Android
{: #coresdk-android}

[Repositorio de GitHub ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}

#### Instalación de Core SDK con Gradle
{: #coresdk-android-gradle}

Añada una dependencia de compilación al archivo `build.gradle` de la app:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```
{: codeblock}

### iOS (SDK de Swift)
{: #coresdk-ios-swift}

[Repositorio de GitHub ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security){: new_window}

#### Instalación de Core SDK con CocoaPods
{: #coresdk-ios-siwft-cocoapods}
Edite el Podfile y añada la siguiente línea a los destinos necesarios y ejecute:

```
use_frameworks!
pod 'BMSSecurity'
```
{: codeblock}


### Cordova
{: #coresdk-cordova}

[Repositorio de GitHub y referencia de la API ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Instalación de Core SDK con la CLI de Cordova
{: #coresdk-cordova-cli}

Instale el plug-in de Cordova Mobile Client Access:
```Bash
cordova plugin add bms-core
```
{: codeblock}

## SDK del cliente para la autenticación de Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Repositorio de GitHub ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication){: new_window},

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
{: codeblock}

### iOS (SDK de Swift)
{: #facebooksdk-ios-swift}

[Repositorio de GitHub ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication){: new_window}

#### Instalación del SDK de Facebook con CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

Edite el Podfile y añada lo siguiente a los destinos necesarios y ejecute:
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```
{: codeblock}


### Cordova
{: #facebooksdk-cordova}

[Repositorio de GitHub y referencia de la API ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Instalación del SDK de Facebook con la CLI de Cordova
{: #facebooksdk-cordova-cli}

Instalación del plug-in de Cordova:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## SDK del cliente para la autenticación de Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Repositorio de GitHub ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication){: new_window},


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
{: codeblock}

### iOS (SDK de Swift)
{: #googlesdk-ios-swift}

[Repositorio de GitHub ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication){: new_window}

#### Instalación del SDK de Google+ con CocoaPods
{: #googlesdk-ios-swift-cocoapods}

Edite el Podfile y añada lo siguiente y ejecute:

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```
{: codeblock}


### Cordova
{: #googlesdk-cordova}

[Repositorio de GitHub y referencia de la API ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}

#### Instalación del SDK de Google+ con la CLI de Cordova
{: #googlesdk-cordova-cli}

Instalación del plug-in:

```Bash
cordova plugin add ibm-mfp-core
```
{: codeblock}

## SDK del servidor para servidores de Node.js
{: #serversdk}

[Repositorio de GitHub ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy){: new_window}

#### Instalación del SDK del servidor con npm
{: #serversdk-npm}

Ejecute NPM para instalar el SDK:

```Bash
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

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

[Repositorio de GitHub ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk){: new_window}

#### Instalación del SDK OAuth con npm
{: #oauthsdk}

Ejecute NPM para instalar el SDK:
```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Ejemplos de proveedor de identidad personalizado
{: #customidprovider}

[Repositorio de GitHub de ejemplo sencillo ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}

[Repositorio de GitHub de ejemplo avanzado ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}
