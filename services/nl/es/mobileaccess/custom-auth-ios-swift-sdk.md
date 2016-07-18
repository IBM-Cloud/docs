---

copyright:
  years: 2016

---

# Configuración del SDK del cliente de {{site.data.keyword.amashort}} para iOS (SDK de Swift)
{: #custom-ios}

Configure su aplicación de iOS con autenticación personalizada para que utilice el SDK del cliente de {{site.data.keyword.amashort}} y conecte la aplicación a {{site.data.keyword.Bluemix}}.  El nuevo SDK de {{site.data.keyword.amashort}} Swift amplia y mejora la funcionalidad proporcionada por el SDK Objetive-C de Mobile Client Access existente. 

**Nota:** Si bien el SDK de Objective-C recibe total soporte y sigue considerándose como SDK principal para {{site.data.keyword.Bluemix_notm}} Mobile Services, está previsto dejar de mantener este SDK a finales del año en favor del nuevo SDK de Swift. 

## Antes de empezar
{: #before-you-begin}

Debe tener un recurso que esté protegido por una instancia del servicio de {{site.data.keyword.amashort}} que esté configurado para utilizar un proveedor de identidad personalizado.  Su app para móvil debe instrumentarse con el SDK del cliente de {{site.data.keyword.amashort}}.  Para obtener más información, consulte la siguiente información:
 * [Iniciación a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/index.html)
 * [Configuración del SDK de Swift de iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [Utilización de un proveedor de identidad personalizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creación de un proveedor de identidad personalizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada
 {: #custom-auth-ios-configmca}

 1. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}.

 1. Pulse **Opciones móviles** y anote los valores correspondientes a **Ruta** (*applicationRoute*) y a **Identificador exclusivo global de la app** (*applicationGUID*). Necesitará estos valores cuando inicialice el SDK.

 1. Pulse el mosaico de {{site.data.keyword.amashort}}. Se cargará el panel de control de {{site.data.keyword.amashort}}.

 1. Pulse el mosaico **Personalizado**.

 1. En **Nombre de reino**, especifique el nombre del reino personalizado.

 1. En **URL**, especifique el valor de applicationRoute.

 1. Pulse **Guardar**.




### Inicialización del SDK del cliente
{: #custom-ios-sdk-initialize}

Para inicializar el SDK, especifique los parámetros `applicationRoute` y `applicationGUID`. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Obtenga los valores de los parámetros de la aplicación. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}. Pulse **Opciones móviles**. Los valores de `applicationRoute` y `applicationGUID` se muestran en los campos **Ruta** e **Identificador exclusivo global de la app**.

1. Importe las infraestructuras necesarias en la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. Inicialice el SDK de cliente de {{site.data.keyword.amashort}}, cambie el gestor de autorización por MCAAuthorizationManager y defina un delegado de autenticación y regístrelo. Sustituya los valores de `<applicationRoute>` y `<applicationGUID>` por los valores correspondientes a **Ruta** e **Identificador exclusivo global de la app** que ha obtenido de **Opciones móviles** en el panel de control de {{site.data.keyword.Bluemix_notm}}. 

  Sustituya `<applicationBluemixRegion>` por la región en la que se aloja su aplicación {{site.data.keyword.Bluemix_notm}}. Para ver la región de {{site.data.keyword.Bluemix_notm}}m pulse en el icono de c ara (![Cara](/face.png "Cara")) que se encuentra en la esquina superior derecha del panel de control. Para `<yourProtectedRealm>`, utilice el **nombre de reino** que ha definido en el título **Custom** del panel de control de {{site.data.keyword.amashort}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<yourProtectedRealm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Delegado de autorización para el manejo del reto personalizado
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <An answer to the challenge sent by the backend (Should be of type [String:AnyObject])>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance

 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("error with register: \(error)")
  }
 return true
 }   
 ```

## Prueba de la autenticación
{: #custom-ios-testing}

Después de inicializar el SDK del cliente y registrar un delegado de autorización personalizado, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #custom-ios-testing-before}

 Debe tener una aplicación que se haya creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y que disponga de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`.

1. Envíe una solicitud al punto final protegido del programa de fondo móvil en su navegador; para ello, abra `{applicationRoute}/protected`, por ejemplo `http://my-mobile-backend.mybluemix.net/protected`. El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} está protegido con {{site.data.keyword.amashort}}. Solo pueden acceder al punto final las aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Si no, se muestra un mensaje `Unauthorized` en el navegador.

1. Utilice la aplicación de iOS para realizar una solicitud al mismo punto final. Añada el código siguiente para inicializar `BMSClient` y registrar el delegado de autorización personalizad:

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

1. 	Cuando las solicitudes se realizan correctamente, verá la siguiente salida en la consola de Xcode:

 ```
 onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
 response:Optional("Hello Don Lon"), no error
 ```

1. También puede añadir la funcionalidad de finalización de sesión añadiendo este código:
```
 MCAAuthorizationManager.sharedInstance.logout(callBack)
 ```  

 Si invoca este código después de que el usuario haya iniciado sesión, la sesión del usuario se cerrará. Cuando el usuario intente iniciar sesión de nuevo, deberá volver a responder a la pregunta que reciba del servidor.

 Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.
