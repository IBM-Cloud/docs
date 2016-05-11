<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# Cómo empezar con el ejemplo HelloWorld
{: #gettingstarted-ios}
*Última actualización: 28 de enero de 2016*
Si desea empezar a trabajar con una aplicación para iOS nueva, puede utilizar la app HelloWorld. Esta app muestra cómo conectar con el programa de fondo de {{site.data.keyword.Bluemix}} desde una app para móvil sin autenticación. La app la tiene instalado el SDK. Cuando esté listo, puede obtener las bibliotecas específicas que desee utilizar en la app.

1. Cree el programa de fondo móvil en {{site.data.keyword.Bluemix_notm}}.
<ol>
	<li>En la sección Contenedores modelo del catálogo de {{site.data.keyword.Bluemix_notm}}, pulse **MobileFirst Services Starter**.</li>
    <li>Especifique un nombre y un host para la app y pulse **Crear**.</li>
    <li>Pulse **Finalizar**. </li>
</ol>
2. Obtenga el proyecto de GitHub.
En el sistema, abra el terminal y escriba el siguiente mandato:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. Inicialice el proyecto.
Para inicializar el SDK, copie el siguiente código en el método `didFinishLaunchingWithOptions` de la aplicación delegada.
   * Objective-C:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift:
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. Ejecute el ejemplo en el entorno de desarrollo.
En Xcode, pulse **Producto&gt;Ejecutar**. Se inicia un simulador de iOS.
En el simulador, pulse **Ping
                {{site.data.keyword.Bluemix_notm}}**. La app de ejemplo obtiene la cabecera de autorización del servicio de Mobile Client Access. Si ping se ejecuta correctamente, el texto del simulador se actualiza.
<br/>Cuando se conecte correctamente a {{site.data.keyword.Bluemix_notm}} desde la app para móviles de Xcode, se mostrará un mensaje parecido al siguiente: "¡Se ha conectado!":<br/>
![La aplicación Hello World se ha conectado correctamente a {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. La aplicación Hello World se ha conectado correctamente a {{site.data.keyword.Bluemix_notm}}") <br/>
Si se ha conectado correctamente, el Xcode de inicio de sesión de depuración contiene el mensaje siguiente:
```Se ha conectado a {{site.data.keyword.Bluemix_notm}} correctamente```
5. Resuelva cualquier problema.
Si la conexión falla, se muestra un mensaje parecido al siguiente: "Algo salió mal". Se incluye más información sobre el error.<br/>
![Aplicación Hello World no conectada a {{site.data.keyword.Bluemix_notm}}](images/bummer_android.jpg "Figura 2. Aplicación Hello World no conectada a Bluemix")
<br/>Compruebe que ha pegado correctamente la ruta y los valores de GUID:
   * Objective-C:
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift:
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


También puede consultar el registro de depuración para obtener más información.

## Pasos siguientes:
{: #next}
Para obtener información sobre cómo obtener el SDK e integrarlo en la app para móviles, consulte la información sobre la configuración de los servicios de {{site.data.keyword.Bluemix}}.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Ejemplo HelloWorld](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## api
   *
[API principal](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
