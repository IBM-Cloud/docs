---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"

---

{:screen: .screen}
{:shortdesc: .shortdesc}


# Habilitación de la autenticación de Google para apps Objective C de iOS
{: #google-auth-ios}


Utilice el inicio de sesión de Google para autenticar usuarios en la app de {{site.data.keyword.amafull}} iOS.

**Nota:** Si bien el SDK de Objective-C recibe total soporte y sigue considerándose como SDK principal para {{site.data.keyword.Bluemix_notm}} Mobile Services, está previsto dejar de mantener este SDK a finales del año en favor del nuevo SDK de Swift. Para aplicaciones nuevas, se recomienda utilizar el SDK de Swift. Las instrucciones de esta página se aplican al SDK de Objective-C de cliente de {{site.data.keyword.amashort}}. Para obtener instrucciones sobre el uso de SDK de Swift, consulte [Habilitación de la autenticación de Google en apps de iOS (SDK de Swift)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html).

## Antes de empezar
{: #before-you-begin}
Debe tener lo siguiente:
* Una instancia de un servicio de {{site.data.keyword.amafull}} y una aplicación {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* El URL de la aplicación de programa de fondo (**Ruta de app**). Necesitará estos valores para enviar solicitudes a los puntos finales protegidos de la aplicación de programa de fondo.
* El valor de **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.

## Configuración de un proyecto de Google para la plataforma iOS
{: #google-auth-ios-project}
Para empezar a utilizar Google como proveedor de identidad, cree un proyecto en Google Developers Console para obtener un ID de cliente de Google.  Este ID de cliente es un identificador exclusivo con el que Google sabrá qué aplicación está intentando conectar.   

1. Si no ha creado un proyecto de iOS de Google, siga los pasos del sitio [Consola de desarrollador de Google](https://console.developers.google.com).

1. En la lista **API sociales**, seleccione **API Google+** y pulse **Habilitar**.

1. En la lista **Credenciales**, pulse el botón **Crear credenciales** y elija el **ID de cliente OAuth**.

1. En este punto se le presentará una opción de tipo de aplicación. Seleccione **iOS**.

1. Indique un nombre para el cliente iOS. Especifique el ID de paquete de la aplicación de iOS. Para encontrar el ID de paquete de la aplicación de iOS, busque el **Identificador de paquete** en el archivo `info.plist` o en el separador **General** del proyecto Xcode.

1. Anote el nuevo ID de cliente de iOS de Google. Necesitará este valor cuando configure la aplicación en {{site.data.keyword.Bluemix}}.




## Configuración de {{site.data.keyword.amashort}} para la autenticación de Google
{: #google-auth-ios-config}

Ahora que ya dispone de un ID de cliente de iOS de Google, puede activar la autenticación de Google en el panel de control de {{site.data.keyword.Bluemix_notm}}.

1. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}.
1. En el separador **Gestionar**, active **Autorización**.
1. Expanda la sección **Google**.
1. En **ID de aplicación para iOS**, especifique su ID de cliente Google para iOS.
1. Pulse **Guardar**.


## Configuración del SDK del cliente de {{site.data.keyword.amashort}} para iOS de Google
{: #google-auth-ios-sdk}

### Instalación del SDK del cliente de {{site.data.keyword.amashort}} mediante CocoaPods
{: #google-auth-ios-sdk-cocoapods}

1. Vaya al proyecto de iOS.

1. Edite el archivo `Podfile` para añadir la línea siguiente:

	```
	pod 'IMFGoogleAuthentication'
	```
{: codeblock}

1. Guarde el archivo `Podfile` y ejecute `pod install` desde la línea de mandatos. CocoaPods instala las dependencias. Se mostrarán el progreso y los componentes que se han añadido.

  **Importante**: ahora debe abrir el proyecto utilizando el archivo `xcworkspace` que ha generado CocoaPods. El nombre suele ser `{nombre-proyecto}.xcworkspace`.  

1. Ejecute `open {nombre-proyecto}.xcworkspace` desde la línea de mandatos para abrir su espacio de trabajo del proyecto de iOS.

### Configuración del proyecto de iOS para la autenticación de Google
{: #google-auth-ios-googleauth}
Para configurar la integración de Google, actualice el archivo `info.plist`. El archivo `info.plist` suele estar en la carpeta `Archivos de soporte` del proyecto Xcode. Puede editar el archivo en el editor de la lista de propiedades o con un editor de texto.

* Configure la integración de Google añadiendo los siguientes esquemas de URL al archivo `info.plist`.
	![Archivo info.plist](images/ios-google-infoplist-settings.png)

	El primer esquema de URL es una versión invertida del ID de cliente de Google Developer Console.  Por ejemplo, si el ID de cliente es `123123-abcabc.apps.googleusercontent.com`, el esquema de URL es: `com.googleusercontent.apps.123123-abcabc`.

	El segundo esquema de URL es el ID de paquete de la aplicación.

* Utilice un editor de texto. Pulse con el botón derecho del ratón en `info.plist` y seleccione **Abrir como > Código fuente**. Añada el siguiente código XML al archivo:

	```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.googleusercontent.apps.123123-abcabc</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.ibm.HelloWorld</string>
			</array>
		</dict>
	</array>

	```
{: codeblock}

	Actualice ambos esquemas de URL.

	**Importante**: no sustituya las propiedades existentes del archivo `info.plist`. Si hay propiedades solapadas, tendrá que fusionarlas manualmente. Para obtener más información, consulte la sección [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start).

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #google-auth-ios-initialize}

Para utilizar el SDK del cliente de {{site.data.keyword.amashort}}, inicialícelo pasando los parámetros TenantID y Ruta de app.

Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Importe las infraestructuras necesarias en la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}. Añada las siguientes cabeceras:

	#### Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
{: codeblock}

	#### Swift:

	El SDK del cliente de {{site.data.keyword.amashort}} se ha implementado con Objective-C. Es posible que necesite añadir una cabecera puente al proyecto de Swift para utilizar el SDK.

	1. Pulse el botón derecho del ratón en el proyecto en Xcode y seleccione **Nuevo archivo...**

	2. En la categoría **Origen de iOS**, escoja **Archivo de cabecera**.

	3. Asígnele el nombre `BridgingHeader.h`.

	4. Añada las siguientes importaciones a la cabecera puente:
		
	   `#import <IMFCore/IMFCore.h>`
		
	   `#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>`
	
	5. Pulse el proyecto en Xcode y seleccione el separador **Crear configuración**.

	6. Busque `Objective-C Bridging Header`.

	7. Defina el valor en la ubicación del archivo `BridgingHeader.h`, por ejemplo:`$(SRCROOT)/MyApp/BridgingHeader.h`.

	8. Asegúrese de que la cabecera puente se selecciona en Xcode al crear el proyecto.

3. Utilice el código siguiente para inicializar el SDK del cliente.  Sustituya `<applicationRoute>` y `<TenantID>` por sus valores de **Ruta** y **TenantID**.

	#### Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"<applicationRoute>"
			backendGUID:@"<TenantID>"];
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("<applicationRoute>",
	 							backendGUID: "<TenantID>")
	```
{: codeblock}

1. Inicialice `AuthorizationManager` pasando el parámetro `tenantId` del servicio {{site.data.keyword.amashort}}. 
  ####Objective-C
	
  ```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
  ```
 {: codeblock}

  ####Swift

  ```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
  ```
 {: codeblock}

1. Registre el manejador de autenticación de Google añadiendo el código siguiente al método `application:didFinishLaunchingWithOptions` en el delegado de la app. Añada este código inmediatamente después de inicializar IMFClient:

	#### Objective-C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```
{: codeblock}

1. Añada el código siguiente al delegado de la app.

	#### Objective-C:

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url
					sourceApplication:sourceApplication annotation:annotation];

		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```
{: codeblock}

	#### Swift:

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance()
							.handleOpenURL(shouldHandleGoogleURL)

		return shouldHandleGoogleURL;
	}
```
{: codeblock}

## Prueba de autenticación
{: #google-auth-ios-testing}
Después de inicializar el SDK del cliente, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #google-auth-ios-testing-before}
Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Si tiene que configurar un punto final `/protected`, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Intente enviar una solicitud al punto final protegido del programa de fondo móvil en su navegador de escritorio; para ello, abra `{applicationRoute}/protected`. Por ejemplo, `http://mi-programa-fondo-móvil.mybluemix.net/protected`.

1. El punto final `/protected` de un programa de fondo móvil creado con el contenedor modelo de MobileFirst Services está protegido con {{site.data.keyword.amashort}}; por tanto, solo se puede acceder al mismo mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Como resultado, verá `Unauthorized` en el navegador de escritorio.

1. Utilice la aplicación de iOS para realizar solicitudes al mismo punto final.

	#### Objective-C:

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
{: codeblock}

	#### Swift:

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
{: codeblock}

1. Ejecute la aplicación. Verá la pantalla de inicio de sesión de Google.

	![imagen](images/ios-google-login.png)

	Esta pantalla puede ser ligeramente diferente si no tiene instalada la app de Facebook en su dispositivo, o bien si no ha iniciado sesión en Facebook.

1. Si pulsa **Aceptar** está autorizando que {{site.data.keyword.amashort}} utilice su identidad de usuario de Google para fines de autenticación.

1. 	Su solicitud debería realizarse correctamente. Debería ver la salida siguiente en LogCat.

	![imagen](images/ios-google-login-success.png)
		
	También puede añadir la funcionalidad de finalización de sesión añadiendo este código:

	#### Objective C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	Si invoca este código después de que el usuario haya iniciado sesión en Google y el usuario intenta iniciar sesión de nuevo, se le solicitará que autorice a {{site.data.keyword.amashort}} para utilizar Google para llevar a cabo la autenticación. En este punto, el usuario puede pulsar el nombre de usuario <!--in the upper-right corner of the screen--> para seleccionar otro usuario para iniciar sesión.

	Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.
