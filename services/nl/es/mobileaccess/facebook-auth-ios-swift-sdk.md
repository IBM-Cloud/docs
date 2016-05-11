---

copyright:
  años: 2016

---

# Habilitación de la autenticación de Facebook en apps de iOS (SDK de Swift)
{: #facebook-auth-ios}

Para utilizar Facebook como proveedor de identidad en las aplicaciones de iOS, añada y configure la plataforma iOS para la aplicación de Facebook.

## Antes de empezar
{: #facebook-auth-ios-before}

* Debe tener un recurso que esté protegido por {{site.data.keyword.amashort}} y un proyecto de iOS instrumentado con el SDK del cliente de {{site.data.keyword.amashort}}.  Para obtener más información, consulte [Iniciación a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) y [Configuración del SDK de Swift de iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).  
* Proteja manualmente la aplicación de fondo con el SDK del servidor de {{site.data.keyword.amashort}}. Para obtener más información, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* Cree un ID de aplicación de Facebook. Para obtener más información, consulte [Cómo obtener un ID de aplicación de Facebook desde el portal de desarrolladores de Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).

## Configuración de la aplicación de Facebook para la plataforma iOS
{: #facebook-auth-ios-config}

1. Inicie una sesión en el [panel de control de la app de Facebook](https://developers.facebook.com/apps/).

1. Anote el **ID de app** correspondiente a su app. Necesitará este valor cuando configure el proyecto iOS para la autenticación de Facebook.

1. Pulse **Valores > Añadir plataforma > iOS**.

1. Especifique *bundleId* de la aplicación de iOS. Para encontrar *bundleId* de la aplicación de iOS, busque el **Identificador de paquete** en el archivo `info.plist` o el separador **General** del proyecto Xcode.
**Sugerencia**: habilite el sufijo de esquema URL o el inicio de sesión único si tiene pensado utilizar estas características.

1. Pulse **Save Settings**.

## Configuración de {{site.data.keyword.amashort}} para la autenticación de Facebook
{: #facebook-auth-ios-configmca}

Después de haber configurado el ID y la aplicación de Facebook para dar servicio a clientes de iOS, puede habilitar la autenticación de Facebook en {{site.data.keyword.amashort}}.

1. Abra la app en el panel de control de {{site.data.keyword.Bluemix}}.

1. Pulse **Opciones móviles** y anote los valores correspondientes a **Ruta** (*applicationRoute*) y a **Identificador exclusivo global de la app** (*applicationGUID*). Necesitará estos valores cuando inicialice el SDK.

1. Pulse el mosaico de {{site.data.keyword.amashort}}. Se cargará el panel de control de {{site.data.keyword.amashort}}.

1. Pulse el mosaico **Facebook**.

1. Especifique el ID de aplicación de Facebook y haga clic en **Guardar**.

## Configuración del SDK del cliente de {{site.data.keyword.amashort}} para iOS
{: #facebook-auth-ios-sdk}

### Instalación de CocoaPods
{: #facebook-auth-cocoapods}

El SDK del cliente de {{site.data.keyword.amashort}} se distribuye con CocoaPods, un gestor de dependencias para proyectos de iOS. CocoaPods descarga automáticamente los artefactos desde los repositorios y los pone a disposición para la aplicación de iOS.

1. Abra Terminal y ejecute el mandato `pod --version`. Si ya tiene CocoaPods instalado, se muestra el número de versión. Puede omitir la sección siguiente de esta guía de aprendizaje.

1. Instale CocoaPods ejecutando `sudo gem install cocoapods`. Consulte el [sitio web de CocoaPods](https://cocoapods.org/) en caso de necesitar más información.

1. Cierre XCode.

1. Abra Terminal y ejecute `cd` en el directorio del proyecto.

1.  Ejecute `pod init`.

### Instalación del SDK de Swift de cliente de {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. En el proyecto de iOS, edite `Podfile` y añada las líneas siguientes:

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'
	```
 **Consejo:** puede añadir `use_frameworks!` al destino de Xcode en lugar de especificarlo en el archivo Podfile.

1. Guarde `Podfile` y ejecute el mandato `pod install` desde la línea de mandatos. CocoaPods instala las dependencias. Se mostrarán el progreso y los componentes que se han añadido.

 **Importante**: ahora debe abrir el proyecto utilizando el archivo `xcworkspace` que ha generado CocoaPods. El nombre suele ser `{nombre-proyecto}.xcworkspace`.  

1. Ejecute `open {nombre-proyecto}.xcworkspace` desde una línea de mandatos para abrir su espacio de trabajo de iOS.

### Configuración del proyecto de iOS para la autenticación de Facebook
{: #facebook-auth-ios-configproject}

1. Busque el `info.plist` archivo, que normalmente se encuentra bajo `archivos de soporte` carpeta en el proyecto Xcode.

1. Para configurar la integración con Facebook añada las propiedades siguientes al archivo `info.plist`:

   ![imagen](images/ios-facebook-infoplist-settings.png)

   Actualice las propiedades de esquema URL y FacebookappID con el ID de aplicación de Facebook.

   También puede actualizar el archivo `info.plist` si pulsa con el botón de derecho en el mismo, selecciona **Abrir como > Código fuente** y añade el XML siguiente:

   ```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>fb{your-facebook-application-id}</string>
			</array>
		</dict>
	</array>
	<key>FacebookAppID</key>
	<string>{your-facebook-application-id}</string>
	<key>FacebookDisplayName</key>
	<string>{your-faceebook-application-name}</string>
	<key>LSApplicationQueriesSchemes</key>
	<array>
		<string>fbauth</string>
		<string>fbauth2</string>
	</array>
	<key>NSAppTransportSecurity</key>
	<dict>
	    <key>NSExceptionDomains</key>
	    <dict>
	        <key>facebook.com</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>                
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>fbcdn.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	        <key>akamaihd.net</key>
	        <dict>
	            <key>NSIncludesSubdomains</key>
	            <true/>
	            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
	            <false/>
	        </dict>
	    </dict>
	</dict>
```
   Actualice las propiedades de esquema URL y FacebookappID con el ID de aplicación de Facebook. Actualice el valor de FacebookDisplayName con el nombre de la aplicación de Facebook.

    **Importante**: asegúrese de no sustituir las propiedades existentes del archivo `info.plist`. Si hay propiedades solapadas, tendrá que fusionarlas manualmente. Para obtener más información, consulte [Configure Xcode Project](https://developers.facebook.com/docs/ios/getting-started/) y [Preparing Your Apps for iOS9](https://developers.facebook.com/docs/ios/ios9).

## Inicialización del SDK de Swift de cliente de {{site.data.keyword.amashort}}
{: #facebook-auth-ios-initalize-swift}

Inicialice el SDK del cliente pasando los parámetros `applicationGUID` y `applicationRoute`.

Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Obtenga los valores de los parámetros de la aplicación. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}. Pulse **Opciones móviles**. Los valores de `applicationRoute` y `applicationGUID` se muestran en los campos **Ruta** e **Identificador exclusivo global de la app**.

1. Para importar la infraestructura necesaria a la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}, añada las cabeceras siguientes:

 ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. Inicialice el SDK del cliente.	Sustituya los valores de `<applicationRoute>` y `<applicationGUID>` por los valores correspondientes a **Ruta** e **Identificador exclusivo global de la app** que ha obtenido de **Opciones móviles** en el panel de control de {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. Notifique la activación de la app al SDK de Facebook y registre el manejador de autenticación de Facebook añadiendo el código siguiente al método `application:didFinishLaunchingWithOptions` en el delegado de la app. Añada este código justo después de inicializar la instancia de BMSClient y registrar Facebook como gestor de autenticación.

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. Copie el archivo `FacebookAuthenticationManager.swift` de los archivos fuente de pod `BMSFacebookAuthentication` en el directorio del proyecto.

1. Añada el código siguiente al delegado de la app.

 ```Swift
	func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?,annotation: AnyObject) -> Bool {

		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## Prueba de autenticación
{: #facebook-auth-ios-testing}

Después de inicializar el SDK del cliente y registrar el gestor de autenticación de Facebook, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #facebook-auth-ios-testing-before}

Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Si tiene que configurar un punto final `/protected`, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Intente enviar una solicitud al punto final protegido del programa de fondo móvil recién creado en su navegador. Abra el siguiente URL: `{rutaAplicación}/protected`.
Por ejemplo: `http://mi-programa-fondo-móvil.mybluemix.net/protected`
<br/>El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` en el navegador. Este mensaje se devuelve porque solo se puede acceder a este punto final con aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de iOS para realizar una solicitud al mismo punto final.

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

1. Ejecute la aplicación. Aparece una pantalla de inicio de sesión de Facebook.

   ![imagen](images/ios-facebook-login.png)

   Esta pantalla puede ser ligeramente diferente si no ha iniciado una sesión en Facebook.

1. Pulse **Aceptar** para autorizar que {{site.data.keyword.amashort}} utilice su identidad de usuario de Facebook para fines de autenticación.

1. 	Cuando la solicitud se realiza correctamente, se muestra la salida siguiente en la consola de Xcode:

 ```
 "onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = 218227041863639;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = 218227041863639;
 })
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```

1. También puede añadir la funcionalidad de finalización de sesión añadiendo este código: 

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 Si invoca este código después de que el usuario haya iniciado sesión en Facebook y el usuario intenta iniciar sesión de nuevo, se le solicitará que autorice a {{site.data.keyword.amashort}} para utilizar Facebook para llevar a cabo la autenticación. 

 Para cambiar de usuario, debe invocar este código y el usuario debe finalizar su sesión en Facebook desde su navegador. 

 Es opcional pasar ```callBack``` a la función de cierre de sesión. También puede pasar `nil`.
