---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Instalación de los {{site.data.keyword.mobileanalytics_short}}SDK de cliente
{: #mobileanalytics_sdk}

Los SDK de cliente de {{site.data.keyword.mobileanalytics_short}}
están disponibles para Android, iOS, WatchOS y Cordova.
{: shortdesc}

## Instalación del SDK de cliente de Android
{: #install-sdk-android}

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.ibm.mobilefirstplatform.clientsdk.android/analytics)

El SDK de cliente de {{site.data.keyword.mobileanalytics_short}} se distribuye con Gradle, un gestor de dependencias para proyectos de Android. Gradle descarga de forma automática artefactos de los repositorios y los pone a disposición de la aplicación de Android.

1. Cree un proyecto de [Android Studio ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://developer.android.com/sdk/index.html){: new_window} o abra uno existente.

2. Abra el archivo `build.gradle` que se encuentra en el **módulo de la app**.

  **Sugerencia**: Es posible que su proyecto de Android tenga dos archivos `build.gradle`: uno para el proyecto y otro para el módulo de la app. Asegúrese de utilizar el archivo del **módulo de la app**.

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
{: #before-you-begin-ios notoc}

Asegúrese de configurar Xcode correctamente. Para obtener información sobre cómo configurar el entorno de desarrollo de iOS, consulte el [sitio web de desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com/support/xcode/){: new_window}. Obtenga más información sobre los [requisitos de Xcode ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#requirements){: new_window} para Client SDK Swift Analytics.

El SDK de {{site.data.keyword.mobileanalytics_short}} se distribuye con [CocoaPods ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://cocoapods.org/){: new_window} y [Carthage ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/Carthage/Carthage#getting-started){: new_window}, unos gestores de dependencias para proyectos de Cocoa. CocoaPods y Carthage descargan artefactos de forma automática de los repositorios y los ponen a disposición de la aplicación. Seleccione CocoaPods o Carthage:

#### CocoaPods
{: #cocoapods notoc}

1. Siga las [instrucciones del Swift SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#cocoapods){: new_window} en GitHub para instalar `BMSAnalytics` utilizando Cocoapods y añádalo al Podfile. 
	
2. Tras instalar el SDK del cliente de iOS, [importe e inicialice](sdk.html#initalize-ma-sdk) el SDK del cliente de Analytics.   

#### Carthage
{: #carthage notoc}

Si no utiliza CocoaPods, puede añadir infraestructuras al proyecto mediante [Carthage ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}.

1. Siga las [instrucciones de instalación de Carthage ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics/tree/development#carthage){: new_window} en GitHub para instalar `BMSAnalytics`.

2. Tras instalar el SDK del cliente de iOS, [importe e inicialice](sdk.html#initalize-ma-sdk) el SDK del cliente de Analytics.

## Instalación del plugin de Cordova
{: #installing-sdk-cordova}

El plugin de Cordova de {{site.data.keyword.mobileanalytics_full}} le permite preparar la aplicación para móvil. 

1. Cree un proyecto de [Cordova ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://cordova.apache.org/#getstarted){: new_window} o abra uno existente.

2. Añada las plataformas Android e iOS a la aplicación Cordova. Ejecute uno, o ambos, de los siguientes mandatos desde la línea de mandatos. Actualmente, se da soporte a Cordova-CLI V6.3.0 o anterior:
   
   Android:

	 ```
	 cordova platform add android@5.2.2
	 ```
	 {: codeblock}
	
   iOS:
   	
	```
	cordova platform add ios
	```
   {: codeblock}
	
3. Si ha añadido la plataforma Android, debe añadir el nivel mínimo soportado de API al archivo `config.xml` de la aplicación Cordova. Abra el archivo `config.xml` y añada la línea siguiente al elemento `<platform name="android">`:

	```
	<platform name="android">  
  	 <preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
  	 <!-- add minimum and target Android API level declaration -->
  	</platform>
	```
   {: codeblock}

 El valor *minSdkVersion* debe ser la versión `15` o superior. Consulte la [Guía de la plataforma Android ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window} para obtener información actualizada sobre el valor soportado de *targetSdkVersion* para el SDK de Android.

4. Si ha añadido el sistema operativo iOS, actualice el elemento `<platform name="ios">` con una declaración de destino:

	```
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
     <!-- add deployment target declaration -->
  	</platform>
	```
	{: codeblock}

5. Añada el plugin `bms-core`.
 	
	 ```
	 cordova plugin add bms-core
	 ```
	 {: codeblock}

6. Verifique que el plugin se ha instalado correctamente con el siguiente mandato:
	
	```
	cordova plugin list
	```
	{: codeblock}
	
7. [Configure el entorno de Android e iOS ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://www.npmjs.com/package/bms-core#4-configuring-your-platform){: new_window}.

8. Ya ha instalado el plugin de Cordova y ha configurado sus entornos. A continuación, [importe e inicialice](sdk.html#initalize-ma-sdk) el SDK de cliente de Analytics.

# Enlaces relacionados
{: #rellinks notoc}

## SDK
{: #sdk notoc}
* [SDK de Android ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK de iOS ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [Cordova Plugin Core SDK ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://www.npmjs.com/package/bms-core){: new_window}

## Referencia de API
{: #api notoc}
* [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
