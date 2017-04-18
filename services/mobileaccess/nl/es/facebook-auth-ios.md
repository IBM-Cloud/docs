---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-03"

---
{:shortdesc: .shortdesc}

# Habilitación de la autenticación de Facebook para apps de iOS (SDK de Objective-C)
{: #facebook-auth-ios}

Para utilizar Facebook como proveedor de identidad en las aplicaciones de {{site.data.keyword.amafull}} iOS, añada y configure la plataforma iOS para la aplicación de Facebook.

{:shortdesc}

**Nota:** si bien el SDK de Objective-C sigue recibiendo soporte, y sigue considerándose el SDK principal para {{site.data.keyword.Bluemix}} Mobile Services, está previsto dejar de utilizarlo en unos meses en favor del SDK de Swift (consulte [Configuración de SDK de Swift para iOS](facebook-auth-ios-swift-sdk.html)).

## Antes de empezar
{: #before-you-begin}

Debe tener lo siguiente:
* Un proyecto de iOS configurado para funcionar con CocoaPods.  Para obtener información, consulte **Instalar CocoaPods** en [Configuración del SDK para iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html).  
   **Nota:** no es necesario que instale el SDK de cliente {{site.data.keyword.amashort}} principal antes de proceder.
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de un programa de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* El valor de **AppGUID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `appGUID` (también conocido como `tenantId`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Un ID de aplicación y una aplicación de Facebook. Para obtener más información, consulte [Creación de una aplicación en el sitio web de Facebook for Developers](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).

## Configuración de la aplicación de Facebook para la plataforma iOS
{: #facebook-auth-ios-config}
En el sitio Facebook for Developers:

1. Inicie la sesión en su cuenta en [Facebook for Developers](https://developers.facebook.com). 

1. Asegúrese de que la plataforma iOS se haya añadido a la app. Cuando añada o configure la plataforma iOS, deberá especificar el valor de **bundleId** de la aplicación iOS. Para encontrar **bundleId** de la aplicación de iOS, busque el **Identificador de paquete** en el archivo `info.plist` o el separador **General** del proyecto Xcode.

1. Pulse **Save Settings**.

	**Sugerencia**: habilite el sufijo de esquema URL o el inicio de sesión único si tiene pensado utilizar estas características.

1. Pulse **Save Settings**.

## Configuración de {{site.data.keyword.amashort}} para la autenticación de Facebook
{: #facebook-auth-ios-configmca}

Después de haber configurado el ID y la aplicación de Facebook para dar servicio a clientes de iOS, puede habilitar la autenticación de Facebook en {{site.data.keyword.amashort}}.

1. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}.
1. En el separador **Gestionar**, active **Autorización**.
	1. Expanda la sección **Facebook**.
	1. Añada el **ID de aplicación de Facebook** y pulse **Guardar**.

## Configuración del SDK del cliente de cliente de Facebook de {{site.data.keyword.amashort}} para iOS
{: #facebook-auth-ios-sdk}

### Instalación de CocoaPods
{: #facebook-auth-cocoapods}

El SDK del cliente de {{site.data.keyword.amashort}} se distribuye con CocoaPods, un gestor de dependencias para proyectos de iOS. CocoaPods descarga automáticamente los artefactos desde los repositorios y los pone a disposición para la aplicación de iOS.

1. Abra Terminal y ejecute el mandato `pod --version`. Si ya tiene CocoaPods instalado, se muestra el número de versión. Puede omitir la sección siguiente de esta guía de aprendizaje.

1. Instale CocoaPods ejecutando `sudo gem install cocoapods`. Consulte el [sitio web de CocoaPods](https://cocoapods.org/) en caso de necesitar más información.

### Instalación del SDK del cliente de Facebook de {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-cocoapods}

1. En el proyecto de iOS, edite `Podfile` y la línea siguiente:

	```
	pod 'IMFFacebookAuthentication'
	```
{: codeblock}

1. Guarde `Podfile` y ejecute el mandato `pod install` desde la línea de mandatos. CocoaPods instala las dependencias. Se mostrarán el progreso y los componentes que se han añadido.
 **Importante**: ahora debe abrir el proyecto utilizando el archivo `xcworkspace` que ha generado CocoaPods. El nombre suele ser `{nombre-proyecto}.xcworkspace`.  

1. Ejecute `open {nombre-proyecto}.xcworkspace` desde una línea de mandatos para abrir su espacio de trabajo de iOS.

### Configuración del proyecto de iOS para la autenticación de Facebook
{: #facebook-auth-ios-configproject}

1. Busque el `info.plist` archivo, que normalmente se encuentra bajo `archivos de soporte` carpeta en el proyecto Xcode.

1. Para configurar la integración con Facebook añada las propiedades siguientes al archivo `info.plist`:

	![imagen](images/ios-facebook-infoplist-settings.png)

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
<string>MyApp</string>
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
{: codeblock}

Actualice el esquema de URL y las propiedades de `FacebookappID` con el **ID de aplicación de Facebook**.

 **Importante**: asegúrese de no sustituir las propiedades existentes del archivo `info.plist`. Si hay propiedades solapadas, tendrá que fusionarlas manualmente. Para obtener más información, consulte [Configure Xcode Project](https://developers.facebook.com/docs/ios/getting-started/) y [Preparing Your Apps for iOS9](https://developers.facebook.com/docs/ios/ios9).


## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #facebook-auth-ios-initalize}

Para inicializar el SDK de cliente, especifique la ruta de la app (`applicationRoute`) y el identificador exclusivo global de la app (`applicationGUID`).

Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.


1. Para importar la infraestructura necesaria a la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}, añada las cabeceras siguientes:

	####Objective-C
	{: #framework-objc}

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
	```	

	####Swift
	{: #bridgingheader-swift}

	El SDK del cliente de {{site.data.keyword.amashort}} se implementa utilizando Objective-C; por tanto, es posible que tenga que añadir una cabecera puente al proyecto de Swift.

	1. Pulse el botón derecho del ratón en el proyecto en Xcode y seleccione **Nuevo archivo...**
		1. En la categoría **Origen de iOS**, escoja `Archivo de cabecera`.
		1. Asígnele el nombre `BridgingHeader.h`.
		1. Añada importaciones a la cabecera puente:

			```Objective-C
			#import <IMFCore/IMFCore.h>
			#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
			#import <FacebookSDK/FacebookSDK.h>
			```

	1. Pulse el proyecto en Xcode y seleccione el separador **Crear configuración**.
		1. Busque **Objective-C Bridging Header**.
		1. Defina el valor en la ubicación del archivo `BridgingHeader.h`, por ejemplo:`$(SRCROOT)/MyApp/BridgingHeader.h`.
		1. Asegúrese de que la cabecera puente se selecciona en Xcode al crear el proyecto. No debería ver mensajes de error.

2. Inicialice el SDK del cliente.	Para obtener información sobre cómo obtener los valores `applicationRoute` y `applicationGUID`, consulte [Antes de empezar](#before-you-begin).

	####Objective-C
	{: #approute-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #approute-swift}

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

1. Inicialice `AuthorizationManager` pasando el parámetro `tenantId` del servicio {{site.data.keyword.amashort}}. Consulte [Antes de empezar](#before-you-begin).

	####Objective-C
	{: #authman-objc}

	```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
	```

	####Swift
	{: #authman-swift}

	```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
	```

1. Notifique la activación de la app al SDK de Facebook y registre el manejador de autenticación de Facebook añadiendo el código siguiente al método `application:didFinishLaunchingWithOptions` en el delegado de la app. Añada este código después de inicializar la instancia IMFClient.

	####Objective-C
	{: #activate-objc}

	```Objective-C
		[FBAppEvents activateApp];
		[[IMFFacebookAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	####Swift
	{: #activate-swift}

	```Swift
		FBAppEvents.activateApp()
		IMFFacebookAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. Añada el código siguiente al delegado de la app.

	####Objective-C
	{: #appdelegate-objc}

	```Objective-C
	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
			sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {

		return [FBAppCall handleOpenURL:url sourceApplication:sourceApplication];
	}
	```

	####Swift
	{: #appdelegate-swift}

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FBAppCall.handleOpenURL(url, sourceApplication: sourceApplication)

	}
```


## Prueba de autenticación
{: #facebook-auth-ios-testing}
Después de inicializar el SDK del cliente y registrar el gestor de autenticación de Facebook, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #facebook-auth-ios-testing-before}
Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Si tiene que configurar un punto final `/protected`, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Intente enviar una solicitud al punto final protegido del programa de fondo móvil recién creado en su navegador. Abra el siguiente URL: `{rutaAplicación}/protected`.
Por ejemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` en el navegador. Este mensaje se devuelve porque solo se puede acceder a este punto final con aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de iOS para realizar una solicitud al mismo punto final.

	####Objective-C
	{: #requestpath-objc}

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```

	####Swift
	{: #requestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};
 ```

1. Ejecute la aplicación. Aparece una pantalla de inicio de sesión de Facebook.

	![imagen](images/ios-facebook-login.png)

	Esta pantalla puede ser ligeramente diferente si no tiene instalada la app de Facebook en su dispositivo, o bien si no ha iniciado sesión en Facebook.

1. Pulse **Aceptar** para autorizar que {{site.data.keyword.amashort}} utilice su identidad de usuario de Facebook para fines de autenticación.

1. 	Cuando la solicitud se realiza correctamente, se muestra la salida siguiente en la consola de Xcode:
![image](images/ios-facebook-login-success.png)

	También puede añadir la funcionalidad de finalización de sesión añadiendo este código:

	####Objective-C
	{: #logout-objc}

	```Objective-C
	[[IMFFacebookAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	####Swift
	{: #logout-swift}

	```Swift
	IMFFacebookAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	Si invoca este código después de que el usuario haya iniciado sesión en Facebook y el usuario intenta iniciar sesión de nuevo, se le solicitará que autorice a {{site.data.keyword.amashort}} para utilizar Facebook para llevar a cabo la autenticación.

	Para cambiar de usuario, debe invocar este código y el usuario debe finalizar su sesión en Facebook desde su navegador.

  Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.
