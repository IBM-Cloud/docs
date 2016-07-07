---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Cómo empezar con el ejemplo de Hello Bluemix for iOS
{: #gettingstarted-android}
*Última actualización: 1 de junio de 2016*
{: .last-updated}  

Si desea empezar a trabajar con una aplicación para iOS nueva, puede utilizar la app HelloWorld. Esta app muestra cómo conectar con el programa de fondo de {{site.data.keyword.Bluemix}} desde una app para móvil sin autenticación. La app la tiene instalado el SDK. Cuando esté listo, puede obtener las bibliotecas específicas que desee utilizar en la app.

1. Cree el programa de fondo móvil en {{site.data.keyword.Bluemix_notm}}.
    1. En la sección Contenedores modelo del catálogo de {{site.data.keyword.Bluemix_notm}}, pulse MobileFirst Services Starter.
    2. Especifique un nombre y un host para la app y pulse **Crear**.
    3. Pulse **Finalizar**.
2. Obtenga el proyecto de GitHub. De forma opcional, utilice el mandato git clone para obtener el proyecto. En el sistema, abra el terminal y, a continuación, escriba el siguiente mandato:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld.git
    ```

3. Inicialice el proyecto. Para inicializar el SDK, copie el siguiente código en el método `didFinishLaunchingWithOptions` de la aplicación delegada.

	###Ojbective-C
	{: initializeobjc}

	**Importante**: Mientras el SDK de Objective-C permanezca completamente soportado, y se sigue considerando el SDK primario para {{site.data.keyword.Bluemix}} Mobile Services, está pensado que se debe de utilizar más tarde este año en favor del nuevo SDK de Swift.

	El SDK de Objective-C informa de datos de supervisión a la Monitoring Console del servicio de {{site.data.keyword.amashort}}. Si se basa en las funciones de supervisión del servicio de {{site.data.keyword.amashort}}, continúe para utilizar el SDK de Objective-C.

	```
	// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
	```

	###Swift
	{: initializeswift}
	```
	// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
	```

4. Ejecute el ejemplo en el entorno de desarrollo. En Xcode, pulse **Producto&gt;Ejecutar**. Se inicia un simulador de iOS.
5. En el simulador, pulse **Ping
                {{site.data.keyword.Bluemix_notm}}**. La app de ejemplo obtiene la cabecera de autorización del servicio de Mobile Client Access. Si ping se ejecuta correctamente, el texto del simulador se actualiza.

  Cuando se conecte correctamente a {{site.data.keyword.Bluemix_notm}} desde la app móvil de Xcode, se mostrará el siguiente mensaje:

  `Yay! You are connected`
  {: screen}

  ![Aplicación Hello World conectada correctamente a {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. Aplicación Hello World conectada correctamente a Bluemix")

  Si la conexión falla, verá:
  `Bummer. Something went wrong`
  {: screen}

  ![Aplicación Hello World no conectada a Bluemix](images/bummer_android.jpg "Figura 2. Aplicación Hello World no conectada a Bluemix")

	Puede resolver los problemas de la conexión fallida de la forma siguiente:
	* Compruebe que ha pegado correctamente los valores de ruta y de GUID:
		####Objective-C
		{: #objcvals}
		```
		[imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
		```

		####Swift
		{: #swiftvals}
		```
		IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
		```

	* Revise el registro de depuración para obtener más información.


## Pasos siguientes:
{: #next}
Para obtener información sobre cómo obtener el SDK e integrarlo en la app para móvil, consulte la información sobre la configuración de los servicios de Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Ejemplo de Hello Bluemix](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API principal](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
