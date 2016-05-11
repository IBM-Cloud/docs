---

copyright:
  años: 2015, 2016

---

# Configuración del SDK del cliente de {{site.data.keyword.amashort}} para iOS
{: #custom-ios}

Configure su aplicación de iOS con autenticación personalizada para que utilice el SDK del cliente de {{site.data.keyword.amashort}} y conecte la aplicación a {{site.data.keyword.Bluemix}}.

**Consejo:** si está desarrollando su app iOS en Swift, tenga en cuenta la posibilidad de utilizar el SDK de Swift de cliente de {{site.data.keyword.amashort}}. Las instrucciones de esta página se aplican al SDK de Objective-C de cliente de {{site.data.keyword.amashort}}. Para ver instrucciones sobre cómo utiliza el SDK de Swift, consulte el apartado sobre [Configuración del SDK de cliente de {{site.data.keyword.amashort}} para iOS (SDK de Swift)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html)

## Antes de empezar
{: #before-you-begin}
Debe tener un recurso que esté protegido por una instancia del servicio de {{site.data.keyword.amashort}} que esté configurado para utilizar un proveedor de identidad personalizado.  Su app para móvil debe instrumentarse con el SDK del cliente de {{site.data.keyword.amashort}}.  Para obtener más información, consulte la siguiente información:
 * [Iniciación a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configuración del SDK de Objective-C de iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [Utilización de un proveedor de identidad personalizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creación de un proveedor de identidad personalizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)



## Instalación del SDK del cliente con CocoaPods
{: #custom-ios-sdk-cocoapods}
Utilice el gestor de dependencias CocoaPods para instalar el SDK del cliente de {{site.data.keyword.amashort}}.

1. Abra Terminal y navegue hasta el directorio raíz del proyecto de iOS.

1. Edite el archivo `Podfile` y añada la línea siguiente.

	```
	pod 'IMFCore'
	```

1. Desde la línea de mandatos, ejecute `pod install`.
CocoaPods instala las dependencias añadidas. Se mostrarán el progreso y los componentes que se han añadido.

**Importante**: ahora debe abrir el proyecto con un archivo xcworkspace que ha generado CocoaPods. El nombre suele ser `{nombre-proyecto}.xcworkspace`.

1. Ejecute `open {nombre-proyecto}.xcworkspace` desde una línea de mandatos para abrir su espacio de trabajo de iOS.



### Inicialización del SDK del cliente
{: #custom-ios-sdk-initialize}

Para inicializar el SDK, especifique los parámetros de ruta de la aplicación (`applicationRoute`) y GUID (`applicationGUID`). Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Obtenga los valores de los parámetros de la aplicación. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}. Pulse **Opciones móviles** para ver los valores correspondientes a **Ruta** (`applicationRoute`) y a **Identificador exclusivo global de la app** (`applicationGUID`).

1. Importe la infraestructura `IMFCore` a la clase en la que desea utilizar el SDK del cliente.

	Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift:

	El SDK del cliente de {{site.data.keyword.amashort}} se ha implementado con Objective-C. Es posible que necesite añadir una cabecera puente al proyecto de Swift para utilizar el SDK.

	* Pulse el botón derecho del ratón en el proyecto en Xcode y seleccione **Nuevo archivo...**
	* En la categoría **Origen de iOS**, escoja **Archivo de cabecera**. Asígnele el nombre `BridgingHeader.h`.
	* Añada `#import <IMFCore/IMFCore.h>` a la cabecera puente.
	* Pulse el proyecto en Xcode y seleccione el separador **Crear configuración**.
	* Busque `Objective-C Bridging Header`.
	* Defina el valor en la ubicación del archivo `BridgingHeader.h`, por ejemplo: `$(SRCROOT)/MyApp/BridgingHeader.h`
	* Verifique que la cabecera puente se selecciona en Xcode al crear el proyecto.

1. Inicialice el SDK del cliente. Sustituya applicationRoute y applicationGUID por los valores correspondientes a **Ruta** (`applicationRoute`) e **Identificador exclusivo global de la app** (`applicationGUID`) que ha obtenido de **Opciones móviles**.

	Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```


## Delegado IMFAuthenticationHandler
{: #custom-ios-sdk-authhandler}


El SDK del cliente de {{site.data.keyword.amashort}} proporciona la interfaz `IMFAuthenticationHandler` para implementar un flujo de autenticación personalizada. `IMFAuthenticationHandler` expone tres métodos a los que se llama en distintas fases del proceso de autenticación.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

Se llama a este método cuando se recibe un cambio de autenticación personalizada desde el servicio de {{site.data.keyword.amashort}}. Los argumentos incluyen

* El protocolo `IMFAuthenticationContext` se proporciona desde el SDK del cliente de {{site.data.keyword.amashort}} para que el desarrollador pueda volver a notificar las respuestas del cambio de autenticación o el error durante la recopilación de credenciales (por ejemplo, cancelación del usuario).
* `NSDictionary` que contiene un cambio de autenticación personalizada tal como lo devuelve un proveedor de identidad personalizado

Al llamar al método `authenticationContext:didReceiveAuthenticationChallenge`, el SDK del cliente de {{site.data.keyword.amashort}} delega el control al desarrollador y pasa a modo de espera de las credenciales. Es responsabilidad del desarrollador recopilar las credenciales y volverlas a notificar al SDK del cliente de {{site.data.keyword.amashort}} utilizando uno de los métodos `IMFAuthenticationContext`, tal como se describe a continuación.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

Se llama a este método después de realizarse una autenticación correcta. Los argumentos incluyen IMFAuthenticationContext y NSDictionary opcional con información ampliada sobre la autenticación correcta.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

Se llama a este método después de un error de autenticación. Los argumentos incluyen IMFAuthenticationContext y NSDictionary opcional con información ampliada sobre el error de autenticación.

## Protocolo IMFAuthenticationContext
{: #custom-ios-sdk-authcontext}


`IMFAuthenticationContext` se proporciona como argumento para el método `authenticationContext:didReceiveAuthenticationChallenge` de un `IMFAuthenticationHandler` personalizado. El desarrollador se encargará de recopilar las credenciales y utilizar los métodos `IMFAuthenticationContext` para devolver las credenciales al SDK del cliente de {{site.data.keyword.amashort}} o informar de un error. Utilice uno de los métodos siguientes

```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## Implementación de ejemplo de un IMFAuthenticationDelegate personalizado
{: #custom-ios-sdk-sample}


El ejemplo de IMFAuthenticationDelegate se ha diseñado como ejemplo del proveedor de identidad personalizado. Puede descargar el ejemplo del [repositorio Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

Objective-C:

``` Objective-C
CustomAuthenticationDelegate.h
-----------------------------------
#import <Foundation/Foundation.h>

@import IMFCore;
@interface CustomAuthenticationDelegate : NSObject <IMFAuthenticationDelegate>
@end


CustomAuthenticationDelegate.m
-----------------------------------
#import "CustomAuthenticationDelegate.h"

@implementation CustomAuthenticationDelegate

-(void) authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge {

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// En este ejemplo, IMFAuthenticationDelegate devuelve inmediatamente un conjunto de
	// credenciales codificadas. En una situación real es donde el desarrollador vería una
	// pantalla de inicio de sesión, recopilaría las credenciales e invocaría la API
	// [context submitAuthenticationChallengeAnswer:]

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// En caso de que se produzca un error al recopilar las credenciales, tendrá
	// que notificarlo a IMFAuthenticationContext. De lo contrario, el SDK del cliente Mobile
	// Client Access permanecerá siempre en estado de espera
	// de las credenciales
	}

-(void) authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationSuccess:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationSuccess");


}

-(void) authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationFailure:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationFailure");

}

@end
```

Implementación de Swift:

```Swift
import Foundation

class CustomAuthenticationDelegate : NSObject, IMFAuthenticationDelegate{

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

		NSLog("didReceiveAuthenticationChallenge :: %@", challenge)

		// En este ejemplo, IMFAuthenticationDelegate devuelve inmediatamente un conjunto de
	// credenciales codificadas. En una situación real es donde el desarrollador vería una
	// pantalla de inicio de sesión, recopilaría las credenciales e invocaría la API
	// context.submitAuthenticationChallengeAnswer()

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// En caso de que se produzca un error al recopilar las credenciales, tendrá
	// que notificarlo a IMFAuthenticationContext. De lo contrario, el SDK del cliente Mobile
	// Client Access permanecerá siempre en estado de espera de las credenciales
	}


	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## Registro de IMFAuthenticationDelegate personalizado

Después de crear un IMFAuthenticationDelegate personalizado, regístrelo con `IMFClient`. Llame al código siguiente en su aplicación antes de enviar solicitudes a los recursos protegidos. Utilice el valor de realmName que indicó en el panel de control de {{site.data.keyword.amashort}}.

Aplicaciones Objective-C:

```Objective-C
[[IMFClient sharedInstance]
				registerAuthenticationDelegate:[CustomAuthenticationDelegate new]
										forRealm:realmName];
```

Aplicaciones Swift:
```Swift
IMFClient.sharedInstance().registerAuthenticationDelegate(CustomAuthenticationDelegate(),
									forRealm: realmName)
```




## Prueba de autenticación
{: #custom-ios-testing}
Después de inicializar el SDK del cliente y registrar un `IMFAuthenticationDelegate` personalizado, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #custom-ios-testing-before}
 Debe tener una aplicación que se haya creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y que disponga de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`.

1. Envíe una solicitud al punto final protegido del programa de fondo móvil en su navegador; para ello, abra `{applicationRoute}/protected`, por ejemplo `http://mi-programa-fondo-móvil.mybluemix.net/protected`.
  El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} está protegido con {{site.data.keyword.amashort}}. Solo pueden acceder al punto final las aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Si no, se muestra un mensaje `Unauthorized` en el navegador.
1. Utilice la aplicación de iOS para realizar solicitudes al mismo punto final. Añada el código siguiente para inicializar `BMSClient` y registrar el `IMFAuthenticationDelegate` personalizado:

	Objective-C:

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

	Swift:

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
1. 	Cuando las solicitudes se realizan correctamente, verá la siguiente salida en la consola de Xcode:

	![imagen](images/ios-custom-login-success.png)
	
	
	
	También puede añadir la funcionalidad de finalización de sesión añadiendo este código: 

	Objective C: 

	```Objective-C
	[[IMFAuthorizationManager sharedInstance] logout : callBack]
	```
	Swift: 

	```Swift
	IMFAuthorizationManager.sharedInstance().logout(callBack)
	```

Si invoca este código después de que el usuario haya iniciado sesión, la sesión del usuario se cerrará. Cuando el usuario intente iniciar sesión de nuevo, deberá volver a responder a la pregunta que reciba del servidor. Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.

