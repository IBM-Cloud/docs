{:shortdesc: .shortdesc}

# SDK, ejemplos y referencias de API de {{site.data.keyword.amashort}}
Para añadir SDK de {{site.data.keyword.amashort}} a la aplicación, escoja los SDK que desea utilizar y configure el gestor de dependencias para transferir los SDK a la app. 

## Core SDK
{: #coresdk}
Core SDK principal incluye API para la habilitación de la autenticación personalizada, la supervisión y el registro de la app móvil. 

### Android
{: #coresdk-android}
[Repositorio Github](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[referencia de API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Instalación de Core SDK con Gradle
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS
{: #coresdk-ios}

[Repositorio Github](#),
[referencia de API](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Instalación de Core SDK con CocoaPods
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Repositorio Github y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instalación de Core SDK con la CLI de Cordova
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK del cliente de {{site.data.keyword.amashort}} para la autenticación de Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Repositorio Github](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[referencia de API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Instalación del SDK de Facebook con Gradle
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS
{: #facebooksdk-ios}

[Repositorio Github (próximamente)](#),
[Referencia de API](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

#### Instalación del SDK de Facebook con CocoaPods
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Repositorio Github y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instalación del SDK de Facebook con la CLI de Cordova
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK del cliente de {{site.data.keyword.amashort}} para la autenticación de Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Repositorio Github](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[referencia de API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Instalación del SDK de Google+ con Gradle
{: #googlesdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS
{: #googlesdk-ios}

[Repositorio Github (próximamente)](#),
[Referencia de API](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Instalación del SDK de Google+ con CocoaPods
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Repositorio Github y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instalación del SDK de Google+ con la CLI de Cordova
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## SDK del servidor de {{site.data.keyword.amashort}} para servidores de Node.js
{: #serversdk}

[Repositorio Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Instalación del SDK del servidor con npm
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## SDK del servidor de {{site.data.keyword.amashort}} para servidor de Java for Liberty
{: #serverlibertysdk}

[Descargue artefactos TAI](https://imf-tai.{DomainName}/public/TAI.zip)

## SDK de OAuth de {{site.data.keyword.amashort}} para Node.js
{: #serverlibertysdk-github}

[Repositorio Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Instalación del SDK OAuth con npm
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## Ejemplo de proveedor de identidad personalizado
{: #customidprovider}

[Repositorio Github y referencia de API](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)


## IMFURLProtocol
{: #IMFURLProtocol}

[Referencia de API](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Instalación de IMFURLProtocol con CocoaPods
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
