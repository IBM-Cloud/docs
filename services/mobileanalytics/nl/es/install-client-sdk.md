---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Instalación de los {{site.data.keyword.mobileanalytics_short}}SDK de cliente
{: #mobileanalytics_sdk}

Los SDK de cliente de {{site.data.keyword.mobileanalytics_short}}
están disponibles para Android, iOS, WatchOS y Cordova.
{: #shortdesc}

## Instalación del SDK de cliente de Android
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)(https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)]

El SDK de cliente de {{site.data.keyword.mobileanalytics_short}} se distribuye con Gradle, un gestor de dependencias para proyectos de Android. Gradle descarga de forma automática artefactos de los repositorios y los pone a disposición de la aplicación de Android.

1. Cree un proyecto de [Android Studio](http://developer.android.com/sdk/index.html) o abra uno existente.

2. Abra el archivo `build.gradle` que se encuentra en el **módulo de la app**.

  **Sugerencia**: Es posible que su proyecto de Android tenga dos archivos `build.gradle`: uno para el proyecto y otro para el módulo de la aplicación. Asegúrese de utilizar el archivo del **módulo de la aplicación**.

3. Busque la sección `Dependencias` del archivo `build.gradle` y añada una dependencia de compilación para el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}. La sentencia de los repositorios debería parecerse al siguiente código de ejemplo:

	```
      dependencies {
        compile 'com.ibm.mobilefirstplatform.clientsdk.android:analytics:1.+'
    	// other dependencies  
      }
  	```
  	{: codeblock}

4. Sincronice el proyecto con Gradle; para ello, pulse **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Abra el archivo `AndroidManifest.xml` del proyecto de Android. Puede encontrar este archivo en **app > manifests**. Añada permiso de acceso a Internet en el elemento `<manifest>`:

	```
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}
   
6. Ahora ha instalado el SDK de cliente de Android. A continuación, [importe e inicialice](sdk.html#initalize-ma-sdk) el SDK de cliente de Analytics.   

## Instalación del SDK de Swift
{: #installing-sdk-ios}

![CocoaPods Compatible](https://img.shields.io/cocoapods/v/BMSAnalytics.svg)

El SDK de {{site.data.keyword.mobileanalytics_full}} le permite preparar su aplicación para móvil. El SDK de Swift está disponible para iOS y watchOS.

### Antes de empezar
{: #before-you-begin-ios}

Asegúrese de configurar Xcode correctamente. Para obtener información sobre cómo configurar el entorno de desarrollo de iOS, consulte el [sitio web para desarrolladores de Apple](https://developer.apple.com/support/xcode/). Obtenga más información sobre los [requisitos de Xcode](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements) para Client SDK Swift Analytics.

El SDK de {{site.data.keyword.mobileanalytics_short}} se distribuye con [CocoaPods](https://cocoapods.org/) y [Carthage](https://github.com/Carthage/Carthage#getting-started), unos gestores de dependencias para proyectos de Cocoa. CocoaPods y Carthage descargan artefactos de forma automática de los repositorios y los ponen a disposición de la aplicación. Seleccione CocoaPods o Carthage:

#### CocoaPods
{: #cocoapods}

1. Siga las [{{site.data.keyword.Bluemix_notm}}instrucciones del Swift SDK de Mobile Services](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods) en GitHub para instalar `BMSAnalytics` utilizando Cocoapods y añádalo al perfil. 
	
2. Tras instalar el SDK del cliente de iOS, [importe e inicialice](sdk.html#initalize-ma-sdk) el SDK del cliente de Analytics.   

#### Carthage
{: #carthage}

Si no utiliza CocoaPods, puede añadir infraestructuras al proyecto mediante [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Siga las [instrucciones de instalación de Carthage](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage) en GitHub para instalar `BMSAnalytics`.

2. Tras instalar el SDK del cliente de iOS, [importe e inicialice](sdk.html#initalize-ma-sdk) el SDK del cliente de Analytics.

## Instalación del plugin de Cordova
{: #installing-sdk-cordova}

El plugin de Cordova de {{site.data.keyword.mobileanalytics_full}} le permite preparar la aplicación para móvil. 

1. Añada las plataformas Android e iOS a la aplicación Cordova. Ejecute uno, o ambos, de los siguientes mandatos desde la línea de mandatos:
   
   Android:

	 ```
	 cordova platform add android
	 ```
	 {: codeblock}
	
   iOS:
   	
	```
	cordova platform add ios
	```
   {: codeblock}
	
2. Si ha añadido la plataforma Android, debe añadir el nivel mínimo soportado de API al archivo `config.xml` de la aplicación Cordova. Abra el archivo `config.xml` y añada la línea siguiente al elemento `<platform name="android">`:

	```
	<platform name="android">  
  	<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	<!-- add minimum and target Android API level declaration -->
  	</platform>
	```
   {: codeblock}

 El valor *minSdkVersion* debe ser mayor que `15`. Consulte la [Guía de la plataforma Android](https://cordova.apache.org/docs/en/latest/guide/platforms/android/) para obtener información actualizada sobre el valor soportado de *targetSdkVersion* para el SDK Android.

3. Si ha añadido el sistema operativo iOS, actualice el elemento `<platform name="ios">` con una declaración de destino:

	```
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  	</platform>
	```
	{: codeblock}

4. Instale el plugin de Cordova de {{site.data.keyword.mobileanalytics_short}}. Actualmente, se da soporte a Cordova-CLI V6.3.0 o anterior:

 	```
	cordova platform add android@5.2.2
	```
	{: codeblock}

5. Verifique que el plugin se ha instalado correctamente con el siguiente mandato:
	
	```
	cordova plugin list
	```
	{: codeblock}
	
6. Ya ha instalado el plugin de Cordova. A continuación, [importe e inicialice](sdk.html#initalize-ma-sdk) el SDK de cliente de Analytics.

# rellinks

## SDK
* [SDK de Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK de iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova Plugin Core SDK](https://www.npmjs.com/package/bms-core){: new_window}

## Referencia de API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
