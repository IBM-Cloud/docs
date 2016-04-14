---

copyright:
  años: 2016

---

# Configuración del SDK de Swift de iOS
{: #getting-started-ios}

Instrumente su aplicación de iOS con el SDK de {{site.data.keyword.amashort}}, inicialice el SDK y realice solicitudes a recursos protegidos o no protegidos.

## Antes de empezar
{: #before-you-begin}
* Debe tener una instancia de un programa de fondo móvil que esté protegida por el servicio de {{site.data.keyword.amashort}}. Para obtener más información sobre cómo crear un programa de fondo móvil, consulte [Cómo empezar](getting-started.html).
* Asegúrese de que ha configurado Xcode correctamente. Para ver más información sobre la configuración del entorno de desarrollo de iOS, consulte el [sitio web de Apple Developer](https://developer.apple.com/support/xcode/).


## Instalación del SDK del cliente de {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
El SDK de {{site.data.keyword.amashort}} se distribuye con CocoaPods, un gestor de dependencias para proyectos de iOS. CocoaPods descarga automáticamente los artefactos desde los repositorios y los pone a disposición para la aplicación de iOS.


### Instalación de CocoaPods
{: #install-cocoapods}
1. Abra Terminal y ejecute el mandato **pod --version**. Si ya tiene CocoaPods instalado, se muestra el número de versión. Puede omitir la sección siguiente para instalar el SDK.

1. Si CocoaPods no está instalado, ejecute: ```
sudo gem install cocoapods
```
Para obtener más información, consulte el [sitio web de CocoaPods](https://cocoapods.org/).

### Instalación del SDK del cliente de {{site.data.keyword.amashort}} con CocoaPods
{: #install-sdk-cocoapods}

1. En Terminal, navegue hasta el directorio raíz del proyecto de iOS.

1. Si aún no ha inicializado el espacio de trabajo para CocoaPods, ejecute el mandato `pod init`.<br/>
 CocoaPods crea un archivo `Podfile`, que es donde debe definir las dependencias para el proyecto de iOS.

1. Edite el archivo `Podfile` y añada la siguiente línea a los destinos necesarios:

	```
  use_frameworks!
	pod 'BMSSecurity'
	```
  **Consejo:** puede añadir `use_frameworks!` al destino de Xcode en lugar de especificarlo en el archivo Podfile.

1. Guarde el archivo `Podfile` y ejecute `pod install` desde la línea de mandatos. <br/>Cocoapods instala las dependencias añadidas. Puede ver el progreso y qué componentes se van añadiendo.<br/>
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

1. Inicialice el SDK de cliente de {{site.data.keyword.amashort}}. Sustituya los valores de `<applicationRoute>` y `<applicationGUID>` por los valores correspondientes a **Ruta** e **Identificador exclusivo global de la app** que ha obtenido de **Opciones móviles** en el panel de control de {{site.data.keyword.Bluemix_notm}}.  

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Inicialice el SDK del cliente.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
 }
 ```

## Cómo realizar una solicitud al programa de fondo móvil
{: #request}

Después de inicializar el SDK del cliente de {{site.data.keyword.amashort}}, puede empezar a realizar solicitudes al programa de fondo móvil.

1. Intente enviar una solicitud a un punto final protegido del programa de fondo móvil en el navegador. Abra el siguiente URL: `{rutaAplicación}/protected`. Por ejemplo: `http://mi-programa-fondo-móvil.mybluemix.net/protected`
<br/>El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` al navegador porque solo se puede acceder a este punto final mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de iOS para realizar una solicitud al mismo punto final. Añada el código siguiente después de inicializar `BMSClient`

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:MfpCompletionHandler = {(response: Response?, error: NSError?) in
     if error == nil {
         print ("response:\(response?.responseText), no error")
     } else {
         print ("error: \(error)")
     }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1.  Cuando la solicitud se realiza correctamente, verá la siguiente salida en la consola de Xcode:

 ```
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```

## Próximos pasos
{: #next-steps}
Cuando se ha conectado al punto final protegido, no se han necesitado credenciales. Para que los usuarios inicien sesión en la aplicación, debe configurar la autenticación de Facebook, Google o Personalizada.
  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Personalizada](custom-auth-ios-swift-sdk.html)
