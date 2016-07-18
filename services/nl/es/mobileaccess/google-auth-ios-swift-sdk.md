 ---

copyright:
  years: 2016

---
{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Habilitación de la autenticación de Google en apps para iOS (SDK de Swift)
{: #google-auth-ios}
Utilice el inicio de sesión de Google para autenticar usuarios en su app Swift de {{site.data.keyword.amashort}} iOS. El nuevo SDK de {{site.data.keyword.amashort}} Swift amplia y mejora la funcionalidad proporcionada por el SDK Objetive-C de Mobile Client Access existente. 

**Nota:** Si bien el SDK de Objective-C recibe total soporte y sigue considerándose como SDK principal para {{site.data.keyword.Bluemix_notm}} Mobile Services, está previsto dejar de mantener este SDK a finales del año en favor del nuevo SDK de Swift. 



## Antes de empezar
{: #google-auth-ios-before}
Debe tener lo siguiente: 

* Un proyecto de iOS en Xcode. No es necesario que esté instrumentado con el SDK del cliente {{site.data.keyword.amashort}}.   
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de un programa de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).


## Preparación de la app para el inicio de sesión de Google
{: #google-sign-in-ios}

Prepare su app para el inicio de sesión de Google siguiendo las instrucciones que proporciona Google en [Inicio de sesión de Google para iOS](https://developers.google.com/identity/sign-in/ios/start-integrating). 

Este proceso: 
* Prepara un nuevo proyecto en el sitio para desarrolladores de Google 
* Crea el archivo `GoogleService-Info.plist` y el valor `REVERSE_CLIENT_ID` para añadir el proyecto de Xcode
* Crea el **ID de cliente de Google** para añadir la aplicación de fondo {{site.data.keyword.Bluemix_notm}}. 

En los pasos siguientes se ofrece una breve descripción de las tareas necesarias para preparar su app.  

**Nota:** no es necesario añadir `Google/SignIn` CocoaPod. El SDK necesario se añade mediante `BMSGoogleAuthentication` CocoaPod a continuación. 

1. Anote el **identificador del paquete** en su proyecto Xcode de la sección **Identity** de la pestaña **General** del destino principal. Lo necesita para crear el proyecto de inicio de sesión de Google. 

1. Cree un proyecto en Google Developer para el inicio de sesión de Google para iOS en https://developers.google.com/mobile/add?platform=ios. 

2. Añada el servicio de inicio de sesión de Google en el proyecto. 

3. Recupere `GoogleService-Info.plist`.

  **Importante:** cuando obtenga el archivo `GoogleService-Info.plist`, ábralo y anote el valor de `CLIENT_ID`. Necesitará este valor más adelante para configurar la aplicación de fondo {{site.data.keyword.amashort}}. 

1. Añada el archivo `GoogleService-Info.plist` al proyecto de Xcode. Para obtener más información, consulte [Añadir el archivo de configuración al proyecto](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config).

1. Actualice los esquemas de URL del proyecto de Xcode con el valor de `REVERSE_CLIENT_ID` y el identificador del paquete. Para obtener más información, consulte el apartado sobre [Añadir esquemas de URL al proyecto](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project)


1. Actualice el archivo project-Bridging-Header.h de la app con el siguiente código:

 ```
 #import <Google/SignIn.h>
 ```

 Para obtener más información sobre cómo actualizar el archivo de cabecera de puente, consulte el paso 1 del apartado sobre [Habilitar el inicio de sesión](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in).

## Configuración de {{site.data.keyword.amashort}} para la autenticación de Google
{: #google-auth-ios-config}

Ahora que ya dispone de un ID de cliente de iOS, puede activar la autenticación de Google en el panel de control de {{site.data.keyword.Bluemix}}.

1. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}.

1. Pulse **Opciones móviles** y anote los valores correspondientes a **Ruta** (*applicationRoute*) y a **Identificador exclusivo global de la app** (*applicationGUID*). Necesitará estos valores cuando inicialice el SDK.

1. Pulse el mosaico de {{site.data.keyword.amashort}}. Se cargará el panel de control de {{site.data.keyword.amashort}}.

1. Pulse el mosaico **Google**.

1. En **ID de aplicación para iOS**, especifique el valor de `CLIENT_ID` del archivo `GoogleService-Info.plist` que ha obtenido anteriormente y pulse **Guardar**.

## Configuración del SDK del cliente de {{site.data.keyword.amashort}} para iOS
{: #google-auth-ios-sdk}

### Instalación de CocoaPods
{: #install-cocoapods}

1. Abra Terminal y ejecute el mandato **pod --version**. Si ya tiene CocoaPods instalado, se muestra el número de versión. Puede omitir la sección siguiente para instalar el SDK.

1. Si CocoaPods no está instalado, ejecute:
```
sudo gem install cocoapods
```
Para obtener más información, consulte el [sitio web de CocoaPods](https://cocoapods.org/).

### Instalación del SDK de Swift de cliente de {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Si no tiene `Podfile` en su proyecto iOS, ejecute `pod init` para crear el archivo. 

1. Edite `Podfile` y añada las líneas siguientes en el destino relevante: 

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 
 **Nota:** si ya ha instalado el SDK principal de {{site.data.keyword.amashort}}, puede eliminar la línea: `pod 'BMSSecurity'`. El pod `BMSGoogleAuthentication` instala todas las infraestructuras necesarias. 
	
 **Consejo:** puede añadir `use_frameworks!` al destino de Xcode en lugar de especificarlo en el archivo Podfile.

1. Guarde el archivo `Podfile` y ejecute `pod install` desde la línea de mandatos. CocoaPods instala las dependencias. Se mostrarán el progreso y los componentes que se han añadido.

 **Importante**: ahora debe abrir el proyecto utilizando el archivo `xcworkspace` que ha generado CocoaPods. El nombre suele ser `{nombre-proyecto}.xcworkspace`.  

1. Ejecute `open {nombre-proyecto}.xcworkspace` desde la línea de mandatos para abrir su espacio de trabajo del proyecto de iOS.

1. Copie el archivo `GoogleAuthenticationManager.swift` de los archivos fuente de pod `BMSGoogleAuthentication` en el directorio del proyecto.

## Inicialización del SDK de Swift de cliente de {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Para utilizar el SDK del cliente de {{site.data.keyword.amashort}}, inicialícelo pasando los parámetros `applicationGUID` y `applicationRoute`.

Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Obtenga los valores de los parámetros de la aplicación. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}. Pulse **Opciones móviles**. Los valores de `applicationRoute` y `applicationGUID` se muestran en los campos **Ruta** e **Identificador exclusivo global de la app**.

1. Importe las infraestructuras necesarias en la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}. Añada las siguientes cabeceras:

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. Utilice el código siguiente para inicializar el SDK del cliente. Sustituya los valores de `<applicationRoute>` y `<applicationGUID>` por los valores correspondientes a **Ruta** e **Identificador exclusivo global de la app** que ha obtenido de **Opciones móviles** en el panel de control de {{site.data.keyword.Bluemix_notm}}.  Sustituya `<applicationBluemixRegion>` por la región en la que se aloja su aplicación {{site.data.keyword.Bluemix_notm}}. Para ver la región de {{site.data.keyword.Bluemix_notm}}m pulse en el icono de c ara (![Cara](/face.png "Cara")) que se encuentra en la esquina superior derecha del panel de control.  

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Inicialice el SDK del cliente.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 GoogleAuthenticationManager.sharedInstance.register()
      return true
 }

 // [START openurl]
      func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?,annotation: AnyObject) -> Bool {
             return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(app: UIApplication, openURL url: NSURL, options: [String : AnyObject]) -> Bool {
 return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```

## Prueba de autenticación
{: #google-auth-ios-testing}

Después de inicializar el SDK del cliente y registrar el gestor de autenticación de Google, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #google-auth-ios-testing-before}

Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Si tiene que configurar un punto final `/protected`, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Intente enviar una solicitud al punto final protegido del programa de fondo móvil en su navegador de escritorio; para ello, abra `{applicationRoute}/protected`. Por ejemplo, `http://my-mobile-backend.mybluemix.net/protected`.

1. El punto final `/protected` de un programa de fondo móvil creado con el contenedor modelo de MobileFirst Services está protegido con {{site.data.keyword.amashort}}; por tanto, solo se puede acceder al mismo mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Como resultado, verá `Unauthorized` en el navegador de escritorio.

1. Utilice la aplicación de iOS para realizar solicitudes al mismo punto final.

 ```Swift
 let protectedResourceURL = "<Your protected resource URL>" // any protected resource
 let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
 if error == nil {
    print ("response:\(response?.responseText), no error")
 } else {
    print ("error: \(error)")
 }
 }

 request.sendWithCompletionHandler(callBack)
	```

1. Ejecute la aplicación. Verá la pantalla de inicio de sesión de Google.

 ![imagen](images/ios-google-login.png)

1. Si inicia la sesión y pulsa **Aceptar**, está autorizando que {{site.data.keyword.amashort}} utilice su identidad de usuario de Google para fines de autenticación.

1. 	Su solicitud debería realizarse correctamente. Debería ver la salida siguiente en el registro.

 ```
 onAuthenticationSuccess info = Optional({attributes = {};
     deviceId = 105747725068605084657;
     displayName = "donlonqwerty@gmail.com";
     isUserAuthenticated = 1;
     userId = 105747725068605084657;
 })
 response:Optional("Hello, this is a protected resource!"), no error
 ```
{: screen}

1. También puede añadir la funcionalidad de finalización de sesión añadiendo este código:

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Si invoca este código después de que el usuario haya iniciado sesión en Google y el usuario intenta iniciar sesión de nuevo, se le solicitará que autorice a {{site.data.keyword.amashort}} para utilizar Google para llevar a cabo la autenticación. En este punto, el usuario puede pulsar el nombre de usuario que aparece en la esquina superior derecha de la pantalla para seleccionar otro usuario para iniciar sesión.

   Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.
