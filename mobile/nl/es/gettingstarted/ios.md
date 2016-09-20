---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Cómo empezar con el ejemplo de Hello Bluemix for iOS
{: #gettingstarted-android}
Última actualización: 1 de junio de 2016
{: .last-updated}  

Si desea empezar a trabajar con una aplicación para iOS nueva, puede utilizar la app Hello Bluemix. Esta app muestra cómo conectar con el programa de fondo de {{site.data.keyword.Bluemix}} desde una app para móvil sin autenticación. Cuando esté listo, puede obtener las bibliotecas específicas que desee utilizar en la app.

1. Cree el programa de fondo móvil en {{site.data.keyword.Bluemix_notm}}.
    1. En la sección Contenedores modelo del catálogo de {{site.data.keyword.Bluemix_notm}}, pulse MobileFirst Services Starter.
    2. Especifique un nombre y un host para la app y pulse **Crear**.
    3. Pulse **Finalizar**.
2. Ejecute la aplicación de ejemplo Hello Bluemix:
	1. Obtenga el proyecto de GitHub. De forma opcional, utilice el mandato git clone para obtener el proyecto. En el sistema, abra el terminal y, a continuación, escriba el siguiente mandato:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. Ejecute el mandato `pod install` desde dentro del directorio `bms-samples-swift-hellobluemix`, donde se ha clonado el proyecto. Si no tiene Cocoapods instalado, obténgalo de [https://cocoapods.org](https://cocoapods.org).
	3. Abra el espacio de trabajo de Xcode con el mandato `open HelloBluemix.xcworkspace`.
	4. En el archivo `AppDelegate.swift`, actualice los valores appRoute y appGuid a los obtenidos desde el programa de fondo de Bluemix que ha creado anteriormente.

3. Ejecute el ejemplo en el entorno de desarrollo. En Xcode, pulse **Producto&gt;Ejecutar**. Se inicia un simulador de iOS.

	**Importante:** La appRoute debe utilizar un protocolo `https` y no `http`, o podría obtener un error de conexión, debido a los valores de seguridad del transporte de la app. Puede obtener más información sobre estos valores en la publicación del blog [Conecte la app de iOS 9 a Bluemix ahora mismo](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).
	
4. En el simulador, pulse **Ping
                {{site.data.keyword.Bluemix_notm}}**. La app de ejemplo obtiene la cabecera de autorización del servicio de Mobile Client Access. Si ping se ejecuta correctamente, el texto del simulador se actualiza.

  Cuando se conecte correctamente a {{site.data.keyword.Bluemix_notm}} desde la app móvil en Xcode, verá:
  `¡Se ha conectado!`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  Si la conexión falla, verá:
  `Bummer. Something went wrong`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

	Puede resolver los problemas de la conexión fallida de la forma siguiente:
	* Compruebe que ha pegado correctamente los valores de ruta y de GUID:
	* Revise el registro de depuración para obtener más información.


## Pasos siguientes:
{: #next}
Para obtener información sobre cómo obtener el SDK e integrarlo en la app para móvil, consulte la información sobre la configuración de los servicios de Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Ejemplo de Hello Bluemix (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API principal](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
