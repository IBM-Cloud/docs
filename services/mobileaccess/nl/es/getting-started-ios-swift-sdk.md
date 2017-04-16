---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configuración del SDK de Swift de iOS
{: #getting-started-ios}

Instrumente su aplicación Swift de iOS con el SDK de {{site.data.keyword.amashort}}, inicialice el SDK y realice solicitudes a recursos protegidos o no protegidos.

{:shortdesc}


## Antes de empezar
{: #before-you-begin}
Debe tener lo siguiente:

* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}}.
* Una instancia de un servicio {{site.data.keyword.amafull}}.
* Su **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse **Opciones móviles**. Los valores `tenantId` (también conocidos como `appGUID`) se muestran en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización de {{site.data.keyword.amashort}}.
* Su **Ruta de aplicación**. Es el URL de la aplicación de programa de fondo. Necesita este valor para enviar solicitudes a sus puntos finales protegidos.
* Su {{site.data.keyword.Bluemix_notm}} **Región**.  Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de región que aparece debe ser uno de los siguientes: `EE.UU. Sur`,  `Sidney` o  `Reino Unido` y debe corresponder con los valores de SDK requeridos en el código: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`.  Necesitará este valor para inicializar el SDK de {{site.data.keyword.amashort}}.
* Un proyecto Xcode. Para obtener más información sobre la configuración del entorno de desarrollo de iOS, consulte el [sitio web de Apple Developer ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.apple.com/support/xcode/ "Icono de enlace externo"){: new_window}.


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
{: codeblock}

Para obtener más información, consulte el [sitio web de CocoaPods ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cocoapods.org/ "Icono de enlace externo"){: new_window}.

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
	{: codeblock}

  **Consejo:** puede añadir `use_frameworks!` al destino de Xcode en lugar de especificarlo en el archivo Podfile.

1. Guarde el archivo `Podfile` y ejecute `pod install` desde la línea de mandatos. CocoaPods instala las dependencias relevantes, y muestra las dependencias y los pods añadidos.<br/>

   **Importante**: CocoaPods genera un archivo `xcworkspace`.  A partir de ahora, debe abrirlo para trabajar en el proyecto.

1. Abra el espacio de trabajo del proyecto de iOS. Abra el archivo `xcworkspace` que ha generado CocoaPods. Por ejemplo, para `{your-project-name}.xcworkspace`, ejecute

	`abra {your-project-name}.xcworkspace`

### Habilitación de Keychain Sharing para iOS
{: #enable_keychain}

Habilite `Keychain Sharing`. Vaya al separador `Capacidades` y `active` `Keychain Sharing` en el proyecto Xcode.

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

 Inicialice el SDK pasando el parámetro `tenantId`. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Importe las infraestructuras necesarias en la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```

1. Inicialice el SDK de cliente de {{site.data.keyword.amashort}}.

 ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, 
	    didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

	let mcaAuthManager = MCAAuthorizationManager.sharedInstance
    mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      // valores posibles para regionName: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney
	BMSClient.sharedInstance.authorizationManager = mcaAuthManager	
	return true
	}
 ```
  {: codeblock}

* Sustituya el `tenantId` por el valor que ha obtenido desde **Opciones móviles**.
* Sustituya `<applicationBluemixRegion>` por la región en la que se aloja su aplicación {{site.data.keyword.Bluemix_notm}}.

Para obtener información sobre estos valores, consulte [Antes de comenzar](#before-you-begin).


## Cómo realizar una solicitud a la aplicación de programa de fondo móvil
{: #request}

Después de inicializar el SDK del cliente de {{site.data.keyword.amashort}}, puede empezar a realizar solicitudes a la aplicación de programa de fondo móvil.

1. Intente enviar una solicitud a un punto final protegido de la aplicación de fondo móvil en el navegador. Abra el siguiente URL: `{applicationRoute}/protected` sustituyendo la `{applicationRoute}` por el valor **applicationRoute** recuperado desde las **Opciones móviles** (consulte [Inicialización del SDK del cliente de Mobile Client Access](#init-mca-sdk-ios)). Por ejemplo:

	`http://my-mobile-backend.mybluemix.net/protected
	`

	Se devuelve un mensaje `Unauthorized` al navegador porque solo se puede acceder a este punto final mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de iOS para realizar una solicitud al mismo punto final. Añada el código siguiente después de inicializar `BMSClient`:

 ```Swift
	let customResourceURL = "<your protected resource absolute path>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
  if error == nil {
       	    print ("response:\(response?.responseText), no error")
     } else {
       	    print ("error: \(error)")
     }
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}

1.  Cuando la solicitud se realiza correctamente, se muestra la salida siguiente en la consola de Xcode:

 ```
 response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
 ```
{: screen}

## Pasos siguientes
{: #next-steps}
Cuando se ha conectado al punto final protegido, no se han necesitado credenciales. Para que los usuarios inicien sesión en la aplicación, debe configurar la autenticación de Facebook, Google o Personalizada.

  * [Facebook](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Personalizada](custom-auth-ios-swift-sdk.html)
