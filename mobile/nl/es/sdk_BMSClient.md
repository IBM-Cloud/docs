---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-07"

---
{:new_window: target="_blank"}
{:codeblock:.codeblock}

# Inicialización de BMSClient
{: #sdk_BMSClient}

`BMSCore` proporciona la infraestructura HTTP que utilizan los otros SDK de cliente de servicios de {{site.data.keyword.Bluemix}} Mobile con sus correspondientes servicios de {{site.data.keyword.Bluemix_notm}}. 


## Inicialización de la aplicación Android
{: #init-BMSClient-android}

Puede descargar e importar el paquete `BMSCore` en su proyecto Android Studio o puede utilizar Gradle.

1. Importe el SDK de cliente añadiendo la siguiente sentencia `import` al principio del archivo del proyecto: 

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
  ```
  {: codeblock}

2. Inicialice el SDK `BMSCore` en la aplicación Android añadiendo el código de inicialización del método `onCreate` de la actividad principal a la aplicación Android o en la ubicación que mejor se ajuste a su proyecto. 

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Asegúrese de apuntar a su región
	```
	{: codeblock}

  Debe inicializar `BMSClient` con el parámetro **bluemixRegion**. En el inicializador, el valor **bluemixRegion** especifica el despliegue de {{site.data.keyword.Bluemix_notm}} que está utilizando, por ejemplo `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`.


## Inicialización de la aplicación iOS
{: #init-BMSClient-ios}

Puede utilizar [CocoaPods](https://cocoapods.org){: new_window} o [Carthage](https://github.com/Carthage/Carthage){: new_window} para obtener el paquete `BMSCore`. 

1. Para instalar `BMSCore` mediante CocoaPods, añada las siguientes líneas a Podfile. Si el proyecto aún no tiene un Podfile, utilice el mandato `pod init`. 

  ```Swift
  use_frameworks!

  target 'MyApp' do
    pod 'BMSCore'
  end
  ```
  {: codeblock}

  Luego ejecute el mandato `pod install` y abra el archivo `.xcworkspace` generado. Para actualizar a un release posterior de `BMSCore`, utilice `pod update BMSCore`.

  Para obtener más información sobre cómo utilizar CocoaPods, consulte las [Guías de CocoaPods](https://guides.cocoapods.org/using/index.html){: new_window}.

2. Para instalar `BMSCore` mediante Carthage, siga estas [instrucciones](https://github.com/Carthage/Carthage#getting-started){: new_window}.

  1. Añada la siguiente línea a Cartfile:

      ```
      github "ibm-bluemix-mobile-services/bms-clientsdk-swift-core"
      ```
      {: codeblock}

  2. Ejecute el mandato `carthage update`. 

  3. Una vez finalizada la compilación, añada `BMSCore.framework` al proyecto siguiendo el [Paso 3](https://github.com/Carthage/Carthage#getting-started) de las instrucciones de Carthage. 

  Para aplicaciones compiladas con Swift 2.3, utilice el mandato `carthage update --toolchain com.apple.dt.toolchain.Swift_2_3`. De lo contrario, utilice el mandato `carthage update`. 

3. Importe el módulo. 

  ```Swift
  import BMSCore
  ```
  {: codeblock}

4. Inicialice la clase `BMSClient` con el código siguiente. 

  Coloque el código de inicialización en el método `application(_:didFinishLaunchingWithOptions:)` de delegado de la aplicación o en la ubicación que mejor se ajuste a su proyecto. 

    ```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Asegúrese de apuntar a su región
    ```
   {: codeblock}

    Para utilizar el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}, debe inicializar `BMSClient` con el parámetro **bluemixRegion**. En el inicializador, el valor **bluemixRegion** especifica el despliegue de {{site.data.keyword.Bluemix_notm}} que está utilizando, por ejemplo `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`.
