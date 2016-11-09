---

copyright:
  years: 2016
lastupdated: "2016-10-09"
---

# Configuración de la autenticación personalizada para la app {{site.data.keyword.amashort}} iOS (Swift SDK)
{: #custom-ios}

Configure su aplicación de iOS con autenticación personalizada para que utilice el SDK del cliente de {{site.data.keyword.amafull}} y conecte la aplicación a {{site.data.keyword.Bluemix}}.  El nuevo SDK de {{site.data.keyword.amashort}} Swift amplía y mejora la funcionalidad proporcionada por el SDK Objetive-C de Mobile Client Access existente.

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

 1. Abra el panel de control de servicio.
 
 1. Pulse **Opciones móviles** y anote **Ruta** (*applicationRoute*) y **GUID de app / TenantId** (*serviceTenantID*). Necesitará estos valores cuando inicialice el SDK, y cuando envíe solicitudes a la aplicación de fondo.

 1. Pulse el icono de {{site.data.keyword.amashort}}. Se cargará el panel de control de {{site.data.keyword.amashort}}.

 1. Pulse el icono **Personalizado**.

 1. En **Nombre de reino**, especifique el nombre del reino personalizado.

 1. En **URL**, especifique el valor de applicationRoute.

 1. Pulse **Guardar**.




### Inicialización del SDK del cliente
{: #custom-ios-sdk-initialize}

Inicialice el SDK pasando el parámetro `applicationGUID` (tenantId). Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Importe las infraestructuras necesarias en la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}.

	```Swift
	import UIKit
	import BMSCore
	import BMSSecurity
	```

1. Inicialice el SDK de cliente de {{site.data.keyword.amashort}}, cambie el gestor de autorización por `MCAAuthorizationManager` y defina y registre un delegado de autenticación.

```Swift

	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>
	let customRealm = "<yourProtectedRealm>"

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
	    		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
	 //el regionName debería ser una de las siguientes constantes de BMSClient.Region: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom o BMSClient.Region.sydney
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager

	//Delegado de autorización para el manejo del reto personalizado
 class MyAuthDelegate : AuthenticationDelegate {
		func onAuthenticationChallengeReceived(_ authContext: AuthenticationContext, challenge: AnyObject){
		    print("onAuthenticationChallengeReceived")
		    let answer = try? Utils.parseJsonStringtoDictionary( "{\"userName\":\"" + "test" + "\",\"password\":\"" + "test" + "\"}")
			authContext.submitAuthenticationChallengeAnswer(answer)
		}

		func onAuthenticationSuccess(_ info: AnyObject?) {
		    print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

		func onAuthenticationFailure(_ info: AnyObject?){
		     print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
	     }

	     let delegate = MyAuthDelegate()
	     mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)

	     return true
      }


```

En el código:

* Sustituya `<applicationBluemixRegion>` por la región en la que se aloja su aplicación {{site.data.keyword.Bluemix_notm}}. Para ver la región de {{site.data.keyword.Bluemix_notm}}, pulse el icono de Avatar ![Icono de Avatar](images/face.jpg "Icono de Avatar") en la barra de menús para abrir el widget **Cuenta y soporte**. El valor de la región que aparece debería ser uno de los siguientes: **EE.UU. sur**, **Reino Unido** o **Sídney**, y se corresponde con las constantes necesarias en el código: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, o `BMSClient.Region.sydney`.
* Sustituya `"<yourProtectedRealm>"` por el valor **Nombre de dominio** que ha definido en el mosaico **Personalizado** del panel de control de {{site.data.keyword.amashort}}. 
* Sustituya `"<serviceTenantID>"` por el valor **tenantId** recuperado desde **Opciones móviles**. Consulte [Configuración de Mobile Client Access para la autenticación personalizada](#custom-auth-ios-configmca).

### Inicialización del SDK del cliente
{: #custom-ios-sdk-initialize}
   
  
## Prueba de autenticación
{: #custom-ios-testing}

Después de inicializar el SDK del cliente y registrar un delegado de autorización personalizado, puede empezar a realizar solicitudes a la aplicación de programa de fondo móvil.

### Antes de empezar
{: #custom-ios-testing-before}

 Debe tener una aplicación que se haya creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y que disponga de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`.

1. Envíe una solicitud al punto final protegido del programa de fondo móvil en su navegador; para ello, abra `{applicationRoute}/protected`. Sustituya la `{applicationRoute}` por el valor recuperado desde las **Opciones móviles** (consulte [Configuración de Mobile Client Access para la autenticación personalizada](#custom-auth-ios-configmca)). Por ejemplo `http://my-mobile-backend.mybluemix.net/protected`.

 El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} está protegido con {{site.data.keyword.amashort}}. Solo pueden acceder al punto final las aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Si no, se muestra un mensaje `Unauthorized` en el navegador.

1. Utilice la aplicación de iOS para realizar solicitudes al mismo punto final. Añada el código siguiente para inicializar `BMSClient` y registrar el delegado de autorización personalizad:

	```Swift

	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
  if error == nil {
	       print ("response:\(response?.responseText), no error")
  } else {
	       print ("error: \(error)")
  }
	}

	request.send(completionHandler: callBack)
	 ```

1. Cuando las solicitudes se realizan correctamente, verá la siguiente salida en la consola de Xcode:

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
