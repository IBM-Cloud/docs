---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:codeblock:.codeblock}

El servicio {{site.data.keyword.amafull}} se sustituye por el servicio {{site.data.keyword.appid_full}}.

# Configuración de la autenticación personalizada para la app {{site.data.keyword.amashort}} iOS (Swift SDK)
{: #custom-ios}

Configure su aplicación de iOS con autenticación personalizada para que utilice el SDK del cliente de {{site.data.keyword.amafull}} y conecte la aplicación a {{site.data.keyword.Bluemix}}.  


## Antes de empezar
{: #before-you-begin}

Antes de empezar, debe tener:

* Un recurso protegido mediante una instancia del servicio {{site.data.keyword.amashort}} configurado para que utilice un proveedor de identidad personalizado (consulte [Configuración de la autenticación personalizada](custom-auth-config-mca.html)).  
* El valor de **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su nombre de **Dominio**. Es el valor que ha especificado en el campo **Nombre de dominio** de la sección **Personalizado** del separador **Gestión** del panel de control de {{site.data.keyword.amashort}}.
* El URL de la aplicación de programa de fondo (**Ruta de app**). Necesitará estos valores para enviar solicitudes a los puntos finales protegidos de la aplicación de programa de fondo.
* Su {{site.data.keyword.Bluemix_notm}} **Región**. Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de la región que aparece debería ser uno de los siguientes: **EE.UU. sur**, **Reino Unido** o **Sídney**, y se corresponde con las constantes necesarias en el código: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, o `BMSClient.Region.sydney`.

Para obtener más información, consulte la siguiente información:
 * [Iniciación a {{site.data.keyword.amashort}}](index.html)
 * [Configuración del SDK de Swift de iOS](getting-started-ios-swift-sdk.html)
 * [Utilización de un proveedor de identidad personalizado](custom-auth.html)
 * [Creación de un proveedor de identidad personalizado](custom-auth-identity-provider.html)
 * [Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada](custom-auth-config-mca.html)

### Habilitación de Keychain Sharing para iOS
{: #enable_keychain}

Habilite `Keychain Sharing`. Vaya al separador `Capacidades` y `active` `Keychain Sharing` en el proyecto Xcode.


### Inicialización del SDK del cliente
{: #custom-ios-sdk-initialize}

Inicialice el SDK pasando el parámetro `applicationGUID` (**TenantId**). Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Importe las infraestructuras necesarias en la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}.

	```Swift
	import UIKit
	import BMSCore
	import BMSSecurity
	```
	{: codeblock}

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
{: codeblock}

En el código:
* Sustituya `MCAServiceTenantId` por el valor de **TenantId** y `<applicationBluemixRegion>` por su **Región** de {{site.data.keyword.amashort}} (consulte [Antes de empezar](##before-you-begin)).
* Utilice el valor de `realmName` que indicó en el panel de control de {{site.data.keyword.amashort}} (consulte [Configuración de la autenticación personalizada](custom-auth-config-mca.html)).
* Sustituya `<applicationBluemixRegion>` por la región en la que se aloja su aplicación {{site.data.keyword.Bluemix_notm}}. Para ver la región de {{site.data.keyword.Bluemix_notm}}, pulse el icono de Avatar ![Icono de Avatar](images/face.jpg "Icono de Avatar") en la barra de menús para abrir el widget **Cuenta y soporte**.  El valor de la región que aparece debería ser uno de los siguientes: **EE.UU. sur**, **Reino Unido** o **Sídney**, y se corresponde con las constantes necesarias en el código: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, o `BMSClient.Region.sydney`.


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
     {: codeblock}

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
	 {: codeblock}

1. También puede añadir la funcionalidad de finalización de sesión añadiendo este código:

	 ```
	 MCAAuthorizationManager.sharedInstance.logout(callBack)
	 ```
	 {: codeblock}

 Si invoca este código después de que el usuario haya iniciado sesión, la sesión del usuario se cerrará. Cuando el usuario intente iniciar sesión de nuevo, deberá volver a responder a la pregunta que reciba del servidor.

 Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.
