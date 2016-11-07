---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-18"

---

# Instalación de los {{site.data.keyword.mobileanalytics_short}}SDK de cliente
{: #mobileanalytics_sdk}

Última actualización: 18 de octubre de 2016
{: .last-updated}

Los SDK de cliente de {{site.data.keyword.mobileanalytics_short}}
están disponibles para Android, iOS y WatchOS.
{: #shortdesc}

## Instalación del SDK de cliente de Android
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)(https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)]

El SDK de cliente de {{site.data.keyword.mobileanalytics_short}} se distribuye con Gradle, un gestor de dependencias para proyectos de Android. Gradle descarga de forma automática artefactos de los repositorios y los pone a disposición de la aplicación de Android.

1. Cree un proyecto de [Android Studio](http://developer.android.com/sdk/index.html) o abra uno existente.

2. Abra el archivo `build.gradle` que se encuentra en el **módulo de la app**.

  **Sugerencia**: Es posible que su proyecto de Android tenga dos archivos `build.gradle`: uno para el proyecto y otro para el módulo de la aplicación. Asegúrese de utilizar el archivo del **módulo de la aplicación**.

3. Busque la sección `Dependencias` del archivo `build.gradle` y añada una dependencia de compilación para el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}. La sentencia de los repositorios debería parecerse al siguiente código de ejemplo:

	```Gradle
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  ```
  {: codeblock}

4. Sincronice el proyecto con Gradle; para ello, pulse **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Abra el archivo `AndroidManifest.xml` del proyecto de Android. Puede encontrar este archivo en **app > manifests**. Añada permiso de acceso a Internet en el elemento `<manifest>`:

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
6. Ahora ha instalado el SDK de cliente de Android. A continuación, [Importe e inicialice](sdk.html#initalize-ma-sdk-android) el SDK de cliente de Analytics.   

## Instalación del SDK de Swift
{: #installing-sdk-ios}

![CocoaPods Compatible](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

El SDK de {{site.data.keyword.mobileanalytics_full}} le permite preparar su aplicación móvil. El SDK de Swift está disponible para iOS y watchOS.

### Antes de empezar
{: #before-you-begin-ios}

Asegúrese de configurar Xcode correctamente. Para obtener información sobre cómo configurar el entorno de desarrollo de iOS, consulte el [sitio web para desarrolladores de Apple](https://developer.apple.com/support/xcode/). Obtenga más información sobre los [requisitos de Xcode](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements) para Client SDK Swift Analytics.

El SDK de {{site.data.keyword.mobileanalytics_short}} se distribuye con [CocoaPods](https://cocoapods.org/) y [Carthage](https://github.com/Carthage/Carthage#getting-started), unos gestores de dependencias para proyectos de Cocoa. CocoaPods y Carthage descargan artefactos de forma automática de los repositorios y los ponen a disposición de la aplicación.

#### CocoaPods
{: #cocoapods}

1. Si no tiene instalado CocoaPods, ejecute lo siguiente:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}
    
    Para Xcode 8: `sudo gem install cocoapods --pre`
    
   Asegúrese de que tenga la versión más reciente de `BMSAnalytics` actualizando el repositorio local de CocoaPods, de la forma siguiente:
   
    ```
    pod repo update master
    ```
    {: codeblock}

2. Siga las [{{site.data.keyword.Bluemix_notm}}instrucciones del Swift SDK de Mobile Services](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods) en GitHub.
	
3. Tras instalar el SDK del cliente de iOS, [Importe e inicialice](sdk.html#init-ma-sdk-ios) el SDK del cliente de Analytics.   

#### Carthage
{: #carthage}

Añada infraestructuras al proyecto mediante [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Siga las [instrucciones de instalación de Carthage](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage) en GitHub.

2. Tras instalar el SDK del cliente de iOS, [Importe e inicialice](sdk.html#init-ma-sdk-ios) el SDK del cliente de Analytics.

# rellinks

## SDK
* [SDK de Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK de iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Referencia de API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
