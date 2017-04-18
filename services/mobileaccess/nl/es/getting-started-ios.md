---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"

---
{:shortdesc: .shortdesc}

# Configuración del SDK de Objective-C de iOS
{: #getting-started-ios}

Instrumente su aplicación de iOS con el SDK de {{site.data.keyword.amafull}}, inicialice el SDK, y realice solicitudes a los recursos protegidos y no protegidos.

{:shortdesc}

**Importante:** Si bien el SDK de Objective-C recibe total soporte y sigue considerándose como SDK principal para {{site.data.keyword.Bluemix_notm}} Mobile Services, está previsto dejar de mantener este SDK a finales del año en favor del nuevo SDK de Swift. Para aplicaciones nuevas, se recomienda utilizar el SDK de Swift (consulte [Configuración del SDK de Swift para iOS](getting-started-ios-swift-sdk.html)).

## Antes de empezar
{: #before-you-begin}
Debe tener lo siguiente:
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* Su **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse **Opciones móviles**. Los valores `tenantId` (también conocidos como `appGUID`) se muestran en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización de {{site.data.keyword.amashort}}.
* Su **Ruta de aplicación**. Es el URL de la aplicación de programa de fondo. Necesita este valor para enviar solicitudes a sus puntos finales protegidos.
* Un proyecto Xcode.  


## Instalación del SDK del cliente de {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
El SDK de {{site.data.keyword.amashort}} se distribuye con CocoaPods, un gestor de dependencias para proyectos de iOS. CocoaPods descarga automáticamente los artefactos desde los repositorios y los pone a disposición para la aplicación de iOS.


### Instalación de CocoaPods
{: #install-cocoapods}

1. Abra Terminal y ejecute el mandato **pod --version**. Si ya tiene CocoaPods instalado, se muestra el número de versión. Vaya a la siguiente sección para instalar el SDK.

1. Si CocoaPods no está instalado, ejecute:

```
sudo gem install cocoapods
```

Para obtener más información, consulte el [sitio web de CocoaPods](https://cocoapods.org/).

### Instalación del SDK del cliente de {{site.data.keyword.amashort}} con CocoaPods
{: #install-sdk-cocoapods}

1. En Terminal, navegue hasta el directorio raíz del proyecto de iOS.

1. Si aún no ha inicializado el espacio de trabajo para CocoaPods, ejecute el mandato `pod init`.<br/>
 CocoaPods crea un archivo `Podfile`, que es donde debe definir las dependencias para el proyecto de iOS.

1. Edite el archivo `Podfile` y añada la línea siguiente a los destinos necesarios:


	`pod 'IMFCore'`

1. Guarde el archivo `Podfile` y ejecute `pod install` desde la línea de mandatos. <br/>Cocoapods instala dependencias añadidas y visualiza los componentes añadidos.<br/>

	**Importante**: CocoaPods genera un archivo `xcworkspace`.  A partir de ahora, debe abrirlo para trabajar en el proyecto.

1. Abra el espacio de trabajo del proyecto de iOS. Abra el archivo `xcworkspace` que ha generado CocoaPods. Por ejemplo: `{nombre-proyecto}.xcworkspace`. Ejecute `open {nombre-proyecto}.xcworkspace`.

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

1. Importe la infraestructura `IMFCore` en la clase en la que desea utilizar el SDK de cliente de {{site.data.keyword.amashort}} añadiendo la siguiente cabecera:

	####Objective-C
	{: #imfcore-objc}

	```Objective-C
	  #import <IMFCore/IMFCore.h>
	```

	####Swift
	{: #sdk-swift}

	El SDK del cliente de {{site.data.keyword.amashort}} se ha implementado con Objective-C. Es posible que necesite añadir una cabecera puente al proyecto de Swift:
	1. Pulse el botón derecho del ratón en el proyecto en Xcode, y seleccione **Nuevo archivo**.
	1. En la categoría **Origen de iOS**, pulse **Archivo de cabecera**. Asígnele el nombre `BridgingHeader.h`.
	1. Añada la siguiente línea a la cabecera puente: `#import <IMFCore/IMFCore.h>`.
	1. Pulse el proyecto en Xcode, y seleccione el separador **Crear configuración**.
	1. Busque `Objective-C Bridging Header`.
	1. Defina el valor en la ubicación del archivo `BridgingHeader.h`, por ejemplo:`$(SRCROOT)/MyApp/BridgingHeader.h`.
	1. Asegúrese de que la cabecera puente se selecciona en Xcode al crear el proyecto. No debería ver mensajes de error.

1. Utilice el código siguiente para inicializar el SDK del cliente de {{site.data.keyword.amashort}}.  Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación. <br/>
Para obtener información sobre cómo obtener los valores `applicationRoute` y `applicationGUID`, consulte [Antes de empezar](#before-you-begin). 

	####Objective-C
	{: #sharedinstance-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #sharedinstance-swift}
	```Swift
 		MFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## Inicialización de AuthorizationManager
Inicialice `AuthorizationManager` pasando el parámetro `tenantId` del servicio {{site.data.keyword.amashort}}. Para obtener información sobre cómo obtener estos valores, consulte [Antes de empezar](#before-you-begin). 

####Objective-C

```Objective-C
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"<tenantId>"];
```

####Swift

```Swift
IMFAuthorizationManager.sharedInstance().initializeWithTenantId("<tenantId>")
```

	
## Cómo realizar una solicitud a la aplicación de programa de fondo móvil
{: #request}

Después de inicializar el SDK del cliente de {{site.data.keyword.amashort}}, puede empezar a realizar solicitudes a la aplicación de programa de fondo móvil.

1. Intente enviar una solicitud a un punto final protegido de la aplicación de fondo móvil en el navegador. Abra el siguiente URL: `{rutaAplicación}/protected`. Por ejemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>El punto final `/protected` de una aplicación de programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` al navegador porque solo se puede acceder a este punto final mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de iOS para realizar una solicitud al mismo punto final. Añada el código siguiente después de inicializar `IMFClient`

	####Objective-C
	{: #nsstring-objc}

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
		}
	}];
	```

	####Swift
	{: #imfclientrequestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
		}
	};

	```

1.  Cuando la solicitud se realiza correctamente, verá la siguiente salida en la consola de Xcode:

	![imagen](images/getting-started-ios-success.png)

## Pasos siguientes
{: #next-steps}
Cuando se ha conectado al punto final protegido, no se han necesitado credenciales. Para que los usuarios inicien sesión en la aplicación, debe configurar la autenticación de Facebook, Google o Personalizada.
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [Personalizada](custom-auth-ios.html)
