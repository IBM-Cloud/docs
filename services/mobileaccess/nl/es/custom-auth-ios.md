---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-07"

---

# Configuración del SDK del cliente de {{site.data.keyword.amashort}} para iOS (Objective-C)
{: #custom-ios}


Configure su aplicación de iOS con autenticación personalizada para que utilice el SDK del cliente de {{site.data.keyword.amafull}} y conecte la aplicación a {{site.data.keyword.Bluemix}}.

**Nota:** si está desarrollando su app iOS en Swift, tenga en cuenta la posibilidad de utilizar el SDK de Swift de cliente de {{site.data.keyword.amashort}}. Las instrucciones de esta página se aplican al SDK de Objective-C de cliente de {{site.data.keyword.amashort}}. Para ver instrucciones sobre cómo utiliza el nuevo SDK de Swift, consulte el apartado sobre [Configuración del SDK de cliente de {{site.data.keyword.amashort}} para iOS (SDK de Swift)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html).

## Antes de empezar
{: #before-you-begin}
Debe tener lo siguiente:

* Un recurso protegido mediante una instancia del servicio {{site.data.keyword.amashort}} configurado para que utilice un proveedor de identidad personalizado (consulte [Configuración de la autenticación personalizada](https://console.stage1.ng.bluemix.net/docs/services/mobileaccess/custom-auth-config-mca.html)).  
* El valor de **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su nombre de **Dominio**. Es el valor que ha especificado en el campo **Nombre de dominio** de la sección **Personalizado** del separador **Gestión** del panel de control de {{site.data.keyword.amashort}} (consulte [Configuración de la autenticación personalizada](https://console.stage1.ng.bluemix.net/docs/services/mobileaccess/custom-auth-config-mca.html)).
* El URL de la aplicación de programa de fondo (**Ruta de app**). Necesitará estos valores para enviar solicitudes a los puntos finales protegidos de la aplicación de programa de fondo.
* Su {{site.data.keyword.Bluemix_notm}} **Región**. Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de región que aparece debe ser uno de los siguientes: `EE.UU. Sur`, `Reino Unido` o `Sidney` y debe corresponder con los valores de SDK necesarios en el código Javascript de WebView: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` o `BMSClient.REGION_SYDNEY`. Necesitará este valor para inicializar el cliente {{site.data.keyword.amashort}}.

Para obtener más información, consulte la siguiente información:
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

Inicialice el SDK pasando los parámetros **Ruta de app** (`applicationRoute`) y **TenantID** (`tenantID`) parameters. 

Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

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

1. Inicialice el SDK del cliente. Sustituya los valores **Ruta de app** (`applicationRoute`) y **TenantID** (`tenantID`) por otros valores. Para obtener más información sobre cómo obtener estos valores, consulte [Antes de empezar](##before-you-begin).

	Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"tenantID"];
	```

	Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "tenantID")
	```

## Inicialización de AuthorizationManager
Inicialice AuthorizationManager pasando el parámetro `tenantId` del servicio {{site.data.keyword.amashort}}. 


### Objective-C:

```Objective-
 [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
```

### Swift:

```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
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

Al llamar al método `authenticationContext:didReceiveAuthenticationChallenge`, el SDK del cliente de {{site.data.keyword.amashort}} está delegando el control al desarrollador y pasa a modo de espera de las credenciales. Es responsabilidad del desarrollador recopilar las credenciales y volverlas a notificar al SDK de cliente de {{site.data.keyword.amashort}} utilizando uno de los siguientes métodos de protocolo `IMFAuthenticationContext`:

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

Se llama a este método después de realizarse una autenticación correcta. Los argumentos incluyen `IMFAuthenticationContext` y un `NSDictionary` opcional que contiene información ampliada sobre el éxito de la autenticación.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

Se llama a este método después de un error de autenticación. Los argumentos incluyen `IMFAuthenticationContext` y un `NSDictionary` opcional que contiene información ampliada sobre el éxito de la autenticación.

## Protocolo IMFAuthenticationContext
{: #custom-ios-sdk-authcontext}


El protocolo `IMFAuthenticationContext` se proporciona como un argumento para el método `authenticationContext:didReceiveAuthenticationChallenge` de un `IMFAuthenticationHandler` personalizado. El desarrollador se encargará de recopilar las credenciales y utilizar los métodos `IMFAuthenticationContext` para devolver las credenciales al SDK de cliente de {{site.data.keyword.amashort}} o informar de un error. 
```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## Implementación de ejemplo de un IMFAuthenticationDelegate personalizado
{: #custom-ios-sdk-sample}


El ejemplo de IMFAuthenticationDelegate se ha diseñado como ejemplo del proveedor de identidad personalizado. Puede descargar el ejemplo del [repositorio GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

Objective-C:

``` Objective-C
CustomAuthenticationDelegate.h
-----------------------------------
# import <Foundation/Foundation.h>

@import IMFCore;
@interface CustomAuthenticationDelegate : NSObject <IMFAuthenticationDelegate>
@end


CustomAuthenticationDelegate.m
-----------------------------------
# import "CustomAuthenticationDelegate.h"

@implementation CustomAuthenticationDelegate

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge{

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// En este ejemplo, IMFAuthenticationDelegate inmediatamente devuelve un conjunto
	// de credenciales codificadas. En una situación real, el desarrollador
	// mostraría una pantalla de inicio de sesión, recopilaría las credenciales e invocaría
	// la API [context submitAuthenticationChallengeAnswer:]

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// En caso de que se produzca un error al recopilar las credenciales, notifíquelo
	// a IMFAuthenticationContext. De lo contrario, el SDK del cliente Mobile Client
	// Access permanecerá siempre en un estado de espera
	// de las credenciales
}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationSuccess:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationSuccess");


}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
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

		// En este ejemplo, IMFAuthenticationDelegate inmediatamente devuelve un conjunto
	// de credenciales codificadas. En una situación real, un desarrollador mostraría
		// una pantalla de inicio de sesión, recopilaría las credenciales e invocaría la API
		// context.submitAuthenticationChallengeAnswer()

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// En caso de que se produzca un error al recopilar las credenciales, notifíquelo
		// a IMFAuthenticationContext. De lo contrario, el SDK del cliente de
		// Mobile Client Access permanece en un estado permanente de espera
		// de credenciales
	}


	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## Registro de IMFAuthenticationDelegate personalizado

Después de crear un `IMFAuthenticationDelegate` personalizado, regístrelo con `IMFClient`. Llame al código siguiente en su aplicación antes de enviar solicitudes a los recursos protegidos. Utilice el valor de `realmName` que indicó en el panel de control de {{site.data.keyword.amashort}}.

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
Después de inicializar el SDK del cliente y registrar un `IMFAuthenticationDelegate` personalizado, puede empezar a realizar solicitudes a la aplicación de fondo móvil.

### Antes de empezar
{: #custom-ios-testing-before}
 Debe tener una aplicación que se haya creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y que disponga de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`.

1. Envíe una solicitud al punto final protegido del programa de fondo móvil en su navegador; para ello, abra `{applicationRoute}/protected`, por ejemplo `http://my-mobile-backend.mybluemix.net/protected`.
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

 Si invoca este código después de que el usuario haya iniciado sesión, la sesión del usuario se cerrará. Cuando el usuario intente iniciar sesión de nuevo, deberá volver a responder a la pregunta que reciba del servidor.

 Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.
