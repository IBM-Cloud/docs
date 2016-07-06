---

copyright:
  years: 2015, 2016

---

# Instalación de {{site.data.keyword.mobileanalytics_short}}
SDK de cliente
{: #mobileanalytics_sdk}
*Última actualización: 21 de abril de 2016*
{: .last-updated}

Los SDK de cliente de {{site.data.keyword.mobileanalytics_short}}
están disponibles para Android, iOS y WatchOS.
{: #shortdesc}

## Instalación del SDK de cliente de Android
{: #install-sdk-android}

El SDK de cliente de {{site.data.keyword.mobileanalytics_short}} se distribuye con Gradle, un gestor de dependencias para proyectos de Android. Gradle descarga de forma automática artefactos de los repositorios y los pone a disposición de la aplicación de Android.

1. Cree un proyecto de [Android Studio](http://developer.android.com/sdk/index.html) o abra uno existente.

2. Abra el archivo `build.gradle` que se encuentra en el módulo de la aplicación.

  **Sugerencia**: Es posible que su proyecto de Android tenga dos archivos `build.gradle`: uno para el proyecto y otro para el módulo de la aplicación. Asegúrese de utilizar el archivo del **módulo de la aplicación**.

3. Busque la sección `Dependencias` del archivo `build.gradle` y añada una dependencia de compilación para el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}, como se indica a continuación:

  ```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
      name:'analytics',
      version: '1.+',
      ext: 'aar',
      transitive: true
  ```
  {: codeblock}

  La sentencia de los repositorios debería parecerse al siguiente código de ejemplo:

	```Gradle
      dependencies {
        compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
          name:'analytics',
          version: '1.+',
          ext: 'aar',
          transitive: true
    	// other dependencies  
      }
  ```
  {: screen}

4. Sincronice el proyecto con Gradle; para ello, pulse **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Abra el archivo `AndroidManifest.xml` del proyecto de Android y añada permiso de acceso a Internet en el elemento `<manifest>`:

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}


## Instalación del SDK de Swift
{: #installing-sdk-ios}

El SDK de {{site.data.keyword.mobileanalytics_full}} le permite preparar su aplicación móvil. El SDK de Swift está disponible para iOS y watchOS.

### Antes de empezar
{: #before-you-begin-ios}

Asegúrese de configurar Xcode correctamente. Para obtener información sobre cómo configurar el entorno de desarrollo de iOS, consulte el [sitio web para desarrolladores de Apple](https://developer.apple.com/support/xcode/).

El SDK de {{site.data.keyword.mobileanalytics_short}} se distribuye con [Cocoapods](https://cocoapods.org/) y [Carthage](https://github.com/Carthage/Carthage#getting-started), unos gestores de dependencias para proyectos de Cocoa. CocoaPods y Carthage descargan artefactos de forma automática de los repositorios y los ponen a disposición de la aplicación.

#### Cocoapods
{: #cocoapods}
1. Si no tiene instalado CocoaPods, ejecute lo siguiente:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}

2. Si todavía no ha inicializado el espacio de trabajo para CocoaPods, ejecute el mandato `pod init` en el directorio raíz del proyecto. CocoaPods crea automáticamente un archivo `Podfile`, que es donde se definen las dependencias del proyecto de Xcode.

3. Añada el pod `BMSAnalytics` al destino en el archivo de pod, como, por ejemplo:

	### iOS

  ```
  use_frameworks!

  target 'MyApp' do
     platform :ios, '8.0'
     pod 'BMSAnalytics'
  end
  ```

4. Guarde el archivo `Podfile` y ejecute `pod install` desde la línea de mandatos.

5. Abra el espacio de trabajo del proyecto de Xcode utilizando el archivo `.xcworkspace` generado por CocoaPods.

#### Carthage
{: #carthage}

Añada infraestructuras al proyecto mediante [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos).

1. Añada infraestructuras de `BMSAnalytics` al archivo Cartfile:
  ```
  github "ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics"
  ```
2. Ejecute el mandato `carthage update`. Cuando haya finalizado la compilación, arrastre `BMSAnalytics.framework`, `BMSCore.framework` y `BMSAnalyticsAPI.framework` al proyecto de Xcode.
3. Siga las instrucciones del sitio de [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) para llevar a cabo la integración.

# rellinks

## SDK
* [SDK de Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK de iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Referencia de API
{: #api}
* [API REST](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
