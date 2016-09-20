---

copyright:
  years: 2016

---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Configuración del SDK de Swift de iOS
{: #getting-started-ios}

Última actualización: 1 de agosto de 2016
{: .last-updated}

{{site.data.keyword.amashort}} ha lanzado un nuevo SDK de Swift que añade y mejora la funcionalidad proporcionada por el SDK de Objective-C de {{site.data.keyword.amashort}} existente, lo que facilita la autenticación de la app y proporciona más protección para los recursos de fondo. Instrumente su aplicación Swift de iOS con el SDK de {{site.data.keyword.amashort}}, inicialice el SDK y realice solicitudes a recursos protegidos o no protegidos.
{:shortdesc}

**Nota:** el SDK de Objective-C notifica los datos de supervisión al servicio de consola de supervisión de {{site.data.keyword.amashort}}. Si confía en la funcionalidad de supervisión del servicio {{site.data.keyword.amashort}}, debe seguir utilizando el SDK de Objective-C.

Si bien el SDK de Objective-C recibe total soporte y sigue considerándose como SDK principal para {{site.data.keyword.Bluemix_notm}} Mobile Services, está previsto dejar de mantener este SDK de Objective-C a finales de este año en favor del nuevo SDK de Swift. 






## Antes de empezar
{: #before-you-begin}
Debe tener lo siguiente:
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* Un proyecto Xcode. Para ver más información sobre la configuración del entorno de desarrollo de iOS, consulte el [sitio web de Apple Developer](https://developer.apple.com/support/xcode/).


## Instalación del SDK del cliente de {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
El SDK de {{site.data.keyword.amashort}} se distribuye con CocoaPods, un gestor de dependencias para proyectos de iOS. CocoaPods descarga automáticamente los artefactos desde los repositorios y los pone a disposición para la aplicación de iOS.


### Instalación de CocoaPods
{: #install-cocoapods}

1. En una ventana de terminal, ejecute el mandato **pod --version**. Si ya tiene CocoaPods instalado, se muestra el número de versión y puede saltar a la siguiente sección para instalar el SDK.

1. Si CocoaPods no está instalado, ejecute:
```
sudo gem install cocoapods
```
Para obtener más información, consulte el [sitio web de CocoaPods](https://cocoapods.org/).

### Instalación del SDK del cliente de {{site.data.keyword.amashort}} con CocoaPods
{: #install-sdk-cocoapods}

1. En una ventana de terminal, navegue hasta el directorio raíz del proyecto de iOS.

1. Si aún no ha inicializado el espacio de trabajo para CocoaPods, ejecute el mandato `pod init`.<br/>
 CocoaPods crea un archivo `Podfile`, que es donde debe definir las dependencias para el proyecto de iOS.

1. Edite el archivo `Podfile` y añada la siguiente línea a los destinos necesarios:

	```
  use_frameworks!
  pod 'BMSSecurity'
	```
  **Consejo:** puede añadir `use_frameworks!` al destino de Xcode en lugar de especificarlo en el archivo Podfile.

1. Guarde el archivo `Podfile` y ejecute `pod install` desde la línea de mandatos. CocoaPods instala las dependencias relevantes, y muestra las dependencias y los pods añadidos.<br/>

   **Importante**: CocoaPods genera un archivo `xcworkspace`.  A partir de ahora, debe abrirlo para trabajar en el proyecto.

1. Abra el espacio de trabajo del proyecto de iOS. Abra el archivo `xcworkspace` que ha generado CocoaPods. Por ejemplo: `{nombre-proyecto}.xcworkspace`. Ejecute `open {nombre-proyecto}.xcworkspace`.

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

 Para inicializar el SDK, especifique los parámetros `applicationRoute` y `applicationGUID`. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Obtenga los valores de los parámetros de la aplicación. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}. Pulse **Opciones móviles**. Los valores de `applicationRoute` y `applicationGUID` se muestran en los campos **Ruta** e **Identificador exclusivo global de la app**.

1. Importe las infraestructuras necesarias en la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```  

1. Inicialice el SDK de cliente de {{site.data.keyword.amashort}}. Sustituya los valores de `<applicationRoute>` y `<applicationGUID>` por los valores correspondientes a **Ruta** e **Identificador exclusivo global de la app** que ha obtenido de **Opciones móviles** en el panel de control de {{site.data.keyword.Bluemix_notm}}. Sustituya `<applicationBluemixRegion>` por la región en la que se aloja su aplicación {{site.data.keyword.Bluemix_notm}}. Para ver la región de {{site.data.keyword.Bluemix_notm}}, pulse el icono del **Avatar**  ![icono de Avatar](images/face.jpg "icono de Avatar") en la barra de menú para abrir el widget **Cuenta y soporte**


 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Inicialice el SDK del cliente.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
 }
 ```

## Cómo realizar una solicitud a la aplicación de programa de fondo móvil
{: #request}

Después de inicializar el SDK del cliente de {{site.data.keyword.amashort}}, puede empezar a realizar solicitudes a la aplicación de programa de fondo móvil.

1. Intente enviar una solicitud a un punto final protegido de la aplicación de fondo móvil en el navegador. Abra el siguiente URL: `{rutaAplicación}/protected`. Por ejemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>El punto final `/protected` de una aplicación de programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` al navegador porque solo se puede acceder a este punto final mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de iOS para realizar una solicitud al mismo punto final. Añada el código siguiente después de inicializar `BMSClient`

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
  if error == nil {
         print ("response:\(response?.responseText), no error")
     } else {
         print ("error: \(error)")
     }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1.  Cuando la solicitud se realiza correctamente, se muestra la salida siguiente en la consola de Xcode:

 ```
 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
{: screen}
 
## Próximos pasos
{: #next-steps}
Cuando se ha conectado al punto final protegido, no se han necesitado credenciales. Para que los usuarios inicien sesión en la aplicación, debe configurar la autenticación de Facebook, Google o Personalizada.
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Personalizada](custom-auth-ios-swift-sdk.html)
