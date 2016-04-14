---

copyright:
  años: 2015, 2016

---

# Configuración del SDK de Objective-C de iOS
{: #getting-started-ios}

Instrumente su aplicación de iOS con el SDK de {{site.data.keyword.amashort}}, inicialice el SDK y realice solicitudes a recursos protegidos o no protegidos.

**Consejo:** si está desarrollando su app iOS en Swift, tenga en cuenta la posibilidad de utilizar el SDK de Swift de cliente de {{site.data.keyword.amashort}}. Para obtener más información, consulte el apartado sobre [Configuración del SDK de Swift de iOS](getting-started-ios-swift-sdk.html)

## Antes de empezar
{: #before-you-begin}
* Debe tener una instancia de un programa de fondo móvil que esté protegida por el servicio de {{site.data.keyword.amashort}}. Para obtener más información sobre cómo crear un programa de fondo móvil, consulte [Cómo empezar](getting-started.html).
* Asegúrese de que ha configurado Xcode correctamente. Para ver más información sobre la configuración del entorno de desarrollo de iOS, consulte el [sitio web de Apple Developer](https://developer.apple.com/support/xcode/).


## Instalación del SDK del cliente de {{site.data.keyword.amashort}}
{: #install-mca-sdk-ios}
El SDK de {{site.data.keyword.amashort}} se distribuye con CocoaPods, un gestor de dependencias para proyectos de iOS. CocoaPods descarga automáticamente los artefactos desde los repositorios y los pone a disposición para la aplicación de iOS.


### Instalación de CocoaPods
{: #install-cocoapods}
1. Abra Terminal y ejecute el mandato **pod --version**. Si ya tiene CocoaPods instalado, se muestra el número de versión. Puede omitir la sección siguiente para instalar el SDK.

1. Si CocoaPods no está instalado, ejecute: ```
sudo gem install cocoapods
```
Para obtener más información, consulte el [sitio web de CocoaPods](https://cocoapods.org/).

### Instalación del SDK del cliente de {{site.data.keyword.amashort}} con CocoaPods
{: #install-sdk-cocoapods}

1. En Terminal, navegue hasta el directorio raíz del proyecto de iOS.

1. Si aún no ha inicializado el espacio de trabajo para CocoaPods, ejecute el mandato `pod init`.<br/>
 CocoaPods crea un archivo `Podfile`, que es donde debe definir las dependencias para el proyecto de iOS.

1. Edite el archivo `Podfile` y añada la siguiente línea a los destinos necesarios:

	```
	pod 'IMFCore'
	```

1. Guarde el archivo `Podfile` y ejecute `pod install` desde la línea de mandatos. <br/>Cocoapods instala las dependencias añadidas. Puede ver el progreso y qué componentes se van añadiendo.<br/>
**Importante**: CocoaPods genera un archivo `xcworkspace`.  A partir de ahora, debe abrirlo para trabajar en el proyecto.

1. Abra el espacio de trabajo del proyecto de iOS. Abra el archivo `xcworkspace` que ha generado CocoaPods. Por ejemplo: `{nombre-proyecto}.xcworkspace`. Ejecute `open {nombre-proyecto}.xcworkspace`.

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #init-mca-sdk-ios}

Para poder utilizar el SDK de cliente de {{site.data.keyword.amashort}}, debe inicializar el SDK; para ello, especifique los parámetros **Ruta** (`applicationRoute`) e **Identificador exclusivo global de la app** (`applicationGUID`). 


1. Desde la página principal del panel de control de {{site.data.keyword.Bluemix_notm}}, haga clic en la aplicación. Pulse **Opciones móviles**. Necesita los valores **Ruta** e **Identificador exclusivo global de la app** para inicializar el SDK. 

1. Importe la infraestructura `IMFCore` en la clase en la que desea utilizar el SDK de cliente de {{site.data.keyword.amashort}} añadiendo la siguiente cabecera: 

	**Objective-C:**
	 ```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	**Swift:**

	El SDK del cliente de {{site.data.keyword.amashort}} se ha implementado con Objective-C. Es posible que necesite añadir una cabecera puente al proyecto de Swift:

	1. Pulse el botón derecho del ratón en el proyecto en Xcode y seleccione **Nuevo archivo...**
	1. En la categoría **Origen de iOS**, pulse **Archivo de cabecera**. Asígnele el nombre `BridgingHeader.h`.
	1. Añada la siguiente línea a la cabecera puente: `#import <IMFCore/IMFCore.h>`
	1. Pulse el proyecto en Xcode y seleccione el separador **Crear configuración**.
	1. Busque `Objective-C Bridging Header`.
	1. Defina el valor en la ubicación del archivo `BridgingHeader.h`, por ejemplo:`$(SRCROOT)/MyApp/BridgingHeader.h`.
	1. Asegúrese de que la cabecera puente se selecciona en Xcode al crear el proyecto. No debería ver mensajes de error.

1. Utilice el código siguiente para inicializar el SDK del cliente de {{site.data.keyword.amashort}}.  Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación. <br/>
Sustituya *applicationRoute* y *applicationGUID* por los valores de **Opciones móviles** en el panel de control de {{site.data.keyword.Bluemix_notm}}.

	**Objective-C:**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift:**

	```Swift
IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## Cómo realizar una solicitud al programa de fondo móvil
{: #request}

Después de inicializar el SDK del cliente de {{site.data.keyword.amashort}}, puede empezar a realizar solicitudes al programa de fondo móvil.

1. Intente enviar una solicitud a un punto final protegido del programa de fondo móvil en el navegador. Abra el siguiente URL: `{rutaAplicación}/protected`. Por ejemplo: `http://mi-programa-fondo-móvil.mybluemix.net/protected`
<br/>El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` al navegador porque solo se puede acceder a este punto final mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de iOS para realizar una solicitud al mismo punto final. Añada el código siguiente después de inicializar `IMFClient`

	**Objective-C:**

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

	**Swift:**

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

## Próximos pasos
{: #next-steps}
Cuando se ha conectado al punto final protegido, no se han necesitado credenciales. Para que los usuarios inicien sesión en la aplicación, debe configurar la autenticación de Facebook, Google o Personalizada.
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [Personalizada](custom-auth-ios.html)
