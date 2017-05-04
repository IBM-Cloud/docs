---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Importante: El servicio {{site.data.keyword.amafull}} se sustituye por el servicio {{site.data.keyword.appid_full}}.**

# Habilitación de la autenticación de Google en apps para iOS (SDK de Swift)
{: #google-auth-ios}

Utilice el inicio de sesión de Google para autenticar usuarios en la app Swift de iOS de {{site.data.keyword.amafull}}.


## Antes de empezar
{: #before-you-begin}

Debe tener lo siguiente:

* Una instancia de un servicio de {{site.data.keyword.amafull}} y una aplicación {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* El URL de la aplicación de programa de fondo (**Ruta de app**). Necesitará estos valores para enviar solicitudes a los puntos finales protegidos de la aplicación de programa de fondo.
* El valor de **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su {{site.data.keyword.Bluemix_notm}} **Región**. Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de la región que aparece debería ser uno de los siguientes: **EE.UU. sur**, **Reino Unido** o **Sídney**, y se corresponde con los valores necesarios en el código: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, o `BMSClient.Region.sydney`.
* Un proyecto de iOS en Xcode. No es necesario que esté instrumentado con el SDK del cliente {{site.data.keyword.amashort}}.  


## Preparación de la app para el inicio de sesión de Google
{: #google-sign-in-ios}

Prepare su app para el inicio de sesión de Google siguiendo las instrucciones que proporciona Google en [Inicio de sesión de Google para iOS ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developers.google.com/identity/sign-in/ios/start-integrating){: new_window}.

Este proceso:

* Prepara un nuevo proyecto en el sitio para desarrolladores de Google.
* Crea el archivo `GoogleService-Info.plist` y el valor `REVERSE_CLIENT_ID` para añadir el proyecto de Xcode.
* Crea el **ID de cliente de Google** para añadir la aplicación de fondo {{site.data.keyword.Bluemix_notm}}.

En los pasos siguientes se ofrece una breve descripción de las tareas necesarias para preparar su app.

**Nota:** No es necesario añadir Google Sign-In CocoaPod. El SDK necesario se añade mediante `BMSGoogleAuthentication` CocoaPod.

1. Anote el **identificador del paquete** en su proyecto Xcode de la sección **Identity** del separador **General** del destino principal. Lo necesita para crear el proyecto de inicio de sesión de Google.

1. Cree un proyecto para el Inicio de sesión de Google para iOS en el [Sitio de Google Developer ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developers.google.com/mobile/add?platform=ios){: new_window}.

1. Añada la API de inicio de sesión de Google al proyecto.

1. Recupere `GoogleService-Info.plist`.

   **Importante:** cuando obtenga el archivo `GoogleService-Info.plist`, ábralo y anote el valor de `CLIENT_ID`. Necesitará este valor más adelante para configurar la aplicación de fondo {{site.data.keyword.amashort}}.

1. Añada el archivo `GoogleService-Info.plist` al proyecto de Xcode. Para obtener más información, consulte [Añadir el archivo de configuración al proyecto ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config){: new_window}.

1. Actualice los esquemas de URL del proyecto de Xcode con el valor de `REVERSE_CLIENT_ID` y el identificador del paquete. Para obtener más información, consulte [Añadir esquemas de URL al proyecto ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project){: new_window}.

1. Actualice el archivo `project-Bridging-Header.h` de la app con el siguiente código:

	```
	#import <Google/SignIn.h>
	```
	{: codeblock}

	Para obtener más información sobre la actualización del archivo de cabecera de puente, consulte [Habilitar el inicio de sesión ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in){: new_window}.

## Configuración de Mobile Client Access para la autenticación de Google
{: #google-auth-ios-config}

Ahora que ya dispone de un ID de cliente de iOS, puede activar la autenticación de Google en el servicio de {{site.data.keyword.amashort}}.

1. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}.
1. En el separador **Gestionar**, active **Autorización**.
1. Expanda la sección **Google**.
1. En **ID de aplicación para iOS**, especifique el valor de `CLIENT_ID` que ha obtenido del archivo `GoogleService-Info.plist`.
1. Pulse **Guardar**.

## Configuración del SDK del cliente para iOS
{: #google-auth-ios-sdk}

### Instalación de CocoaPods
{: #install-cocoapods}

1. Abra Terminal y ejecute el mandato **pod --version**. Si ya tiene CocoaPods instalado, se muestra el número de versión. Puede omitir la sección siguiente para instalar el SDK.

1. Si CocoaPods no está instalado, ejecute:

	```
	sudo gem install cocoapods
	```
	{: codeblock}

Para obtener más información, consulte el [sitio web de CocoaPods ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://cocoapods.org/){: new_window}.

### Instalación del SDK de Swift de cliente de {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Si no tiene `Podfile` en su proyecto iOS, ejecute `pod init` para crear el archivo.

1. Edite `Podfile` y añada las líneas siguientes en el destino relevante:

	```
	use_frameworks!
	pod 'BMSGoogleAuthentication'
	```
	{: codeblock}

	**Nota:** si ya ha instalado el SDK principal de {{site.data.keyword.amashort}}, puede eliminar la línea: `pod 'BMSSecurity'`. El pod `BMSGoogleAuthentication` instala todas las infraestructuras necesarias.

	**Consejo:** puede añadir `use_frameworks!` al destino de Xcode en lugar de especificarlo en el archivo Podfile.

1. Guarde el archivo `Podfile` y ejecute `pod install` desde la línea de mandatos. CocoaPods instala las dependencias. Se mostrarán el progreso y los componentes que se han añadido.

	**Importante**: ahora debe abrir el proyecto utilizando el archivo `xcworkspace` que ha generado CocoaPods. El nombre suele ser `{nombre-proyecto}.xcworkspace`.  

1. Ejecute `open {nombre-proyecto}.xcworkspace` desde la línea de mandatos para abrir su espacio de trabajo del proyecto de iOS.

1. Copie el archivo `GoogleAuthenticationManager.swift` de los archivos fuente de pod `BMSGoogleAuthentication` en el directorio del proyecto.

### Habilitación de Keychain Sharing para iOS
{: #enable_keychain}

Habilite `Keychain Sharing`. Vaya al separador `Capacidades` y `active` `Keychain Sharing` en el proyecto Xcode.


## Inicialización del SDK de Swift de cliente de {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Para utilizar el SDK del cliente de {{site.data.keyword.amashort}}, inicialícelo pasando el parámetro `tenantID`.

Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Importe las infraestructuras necesarias en la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}. Añada las siguientes cabeceras:

	```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
		//the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	    func application(_ application: UIApplication,
			     open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
			return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

	@available(iOS 9.0, *)
	func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }

	```
	{: codeblock}

	En el código:

      * Sustituya `<serviceTenantID>` por el valor recuperado desde las **Opciones móviles**.
      * Sustituya `<applicationBluemixRegion>` por su **Región** de {{site.data.keyword.Bluemix_notm}}.

	Para obtener más información sobre cómo obtener estos valores, consulte [Antes de empezar](#before-you-begin).


## Prueba de autenticación
{: #google-auth-ios-testing}

Después de inicializar el SDK del cliente y registrar el gestor de autenticación de Google, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #google-auth-ios-testing-before}

Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Si tiene que configurar un punto final `/protected`, consulte [Protección de recursos](protecting-resources.html).

1. Intente enviar una solicitud al punto final protegido de la aplicación de programa de fondo móvil en su navegador de escritorio abriendo `{applicationRoute}/protected`.  Por ejemplo `http://my-mobile-backend.mybluemix.net/protected`.

1. El punto final `/protected` de una aplicación de programa de fondo móvil creado con MobileFirst Services Boilerplate está protegido con {{site.data.keyword.amashort}}; por tanto, solo se puede acceder al mismo mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Como resultado, verá `Unauthorized` en el navegador de escritorio.

1. Utilice la aplicación de iOS para realizar solicitudes al mismo punto final.

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

1. Ejecute la aplicación. Verá la pantalla de inicio de sesión de Google.

 ![imagen](images/ios-google-login.png)

1. Si inicia la sesión y pulsa **Aceptar**, está autorizando que {{site.data.keyword.amashort}} utilice su identidad de usuario de Google para fines de autenticación.

1. Su solicitud debería realizarse correctamente. Aparecerá la siguiente salida en el registro.

	```
	response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error
	```
	{: screen}

1. También puede añadir la funcionalidad de finalización de sesión añadiendo este código:

	```
	GoogleAuthenticationManager.sharedInstance.logout(callBack)
	```
	{: codeblock}

	Si invoca este código después de que el usuario haya iniciado sesión en Google y el usuario intenta iniciar sesión de nuevo, se le solicitará que autorice a {{site.data.keyword.amashort}} para utilizar Google para llevar a cabo la autenticación. En este punto, el usuario puede pulsar el nombre de usuario <!--in the upper-right corner of the screen--> para seleccionar otro usuario para iniciar sesión.

	Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.
