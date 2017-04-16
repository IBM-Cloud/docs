---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuración de la autenticación personalizada para la app {{site.data.keyword.amashort}} Cordova
{: #custom-cordova}

Prepare la aplicación Cordova para que utilice la autenticación personalizada y el SDK del cliente de {{site.data.keyword.amafull}} para acceder a la aplicación protegida.

## Antes de empezar
{: #before-you-begin}
* Un recurso protegido mediante una instancia del servicio {{site.data.keyword.amashort}} configurado para que utilice un proveedor de identidad personalizado (consulte [Configuración de la autenticación personalizada](custom-auth-config-mca.html)).  
* El valor de **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su nombre de **Dominio**. Es el valor que ha especificado en el campo **Nombre de dominio** de la sección **Personalizado** del separador **Gestión** del panel de control de {{site.data.keyword.amashort}}.
* Su {{site.data.keyword.Bluemix_notm}} **Región**. Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de la región que aparece debe ser uno de los siguientes: `EE.UU. Sur`, `Reino Unido` o `Sidney`. La sintaxis exacta de las constantes correspondientes de SDK se proporcionan en los ejemplos de código.

Para obtener más información,
consulte la siguiente información:

 * [Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada](custom-auth-config-mca.html). Muestra cómo configurar el servicio {{site.data.keyword.amashort}} para la autenticación personalizada. Aquí puede definir el valor de **Dominio**.
 * [Configuración del SDK de Cordova](getting-started-cordova.html). Information sobre cómo configurar la app del cliente Cordova.
 * [Utilización de un proveedor de identidad personalizado](custom-auth.html). Cómo autenticar usuarios con un proveedor de identidad personalizado.
 * [Creación de un proveedor de identidad personalizado](custom-auth-identity-provider.html). Algunos ejemplos de cómo funciona un proveedor de identidad personalizado.

## Configure su código Cordova WebView
### Inicialización del SDK del cliente de {{site.data.keyword.amashort}} en Cordova WebView
{: #custom-cordova-sdk}
Para inicializar el SDK, pase el parámetro `<applicationBluemixRegion>` en el archivo `index.js`.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Sustituya `<applicationBluemixRegion>` por su región (consulte [Antes de empezar](#before-you-begin)).


### Interfaz de escucha de autenticación
{: #custom-cordva-auth}

El SDK del cliente de {{site.data.keyword.amashort}} proporciona una interfaz de escucha de autenticación para implementar un flujo de autenticación personalizada. Debe añadir los métodos siguientes a los que se llama en diferentes fases de un proceso de autenticación.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```
{: codeblock}

Cada método gestiona una fase diferente de un proceso de autenticación.

### Método onAuthenticationChallengeReceived
{: #onAuthenticationChallengeReceived}
Se llama a este método cuando se recibe un cambio de autenticación personalizada desde el servicio de {{site.data.keyword.amashort}}.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```
{: codeblock}

* `authenticationContext`: proporcionado por el SDK del cliente de {{site.data.keyword.amashort}} para que el desarrollador pueda volver a notificar los errores o las respuestas al cambio de autenticación durante la recopilación de credenciales, como si el usuario cancela una solicitud de autenticación.
* `challenge`: un objeto JSON que contiene un cambio de autenticación personalizada, tal como se devuelve desde un proveedor de identidad personalizado.

Llamando al método `onAuthenticationChallengeReceived`, el SDK del cliente de {{site.data.keyword.amashort}} delega el control al desarrollador. {{site.data.keyword.amashort}} espera las credenciales. El desarrollador debe recopilar las credenciales y volverlas a notificar al SDK del cliente de {{site.data.keyword.amashort}} utilizando uno de los métodos siguientes de la interfaz `authContext`:

```JavaScript
onAuthenticationSuccess: function(info){...}
```
{: codeblock}

Se llama a este método después de realizarse una autenticación correcta. Los argumentos incluyen un objeto JSON opcional que contiene información ampliada sobre el éxito de la autenticación.

```JavaScript
onAuthenticationFailure: function(info){...}
```
{: codeblock}

Se llama a este método después de un error de autenticación. Los argumentos incluyen un objeto JSON opcional que contiene información ampliada sobre el error de la autenticación.

### authenticationContext
{: #custom-cordova-authcontext}

El valor de `authenticationContext` se proporciona como un argumento del método `onAuthenticationChallengeReceived` de una escucha de autenticación personalizada. El desarrollador debe recopilar las credenciales y utilizar los métodos `authenticationContext` para devolver las credenciales al SDK del cliente de {{site.data.keyword.amashort}} o para notificar un error. Utilice uno de los métodos siguientes:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);
```
{: codeblock}

```JavaScript
authenticationContext.submitAuthenticationFailure(info);
```
{: codeblock}

El código siguiente muestra cómo una escucha de autenticación de un cliente puede recopilar credenciales, enfrentarse a desafíos y proporcionar respuestas de autenticación.

## Implementación de ejemplo de un flujo de trabajo de escucha de autenticación personalizada
{: #custom-cordova-authlisten-sample}

Este ejemplo de escucha de autenticación se ha diseñado para que funcione con un proveedor de identidad personalizado. Puede descargar el proveedor de identidad personalizado desde [este repositorio de Github ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Icono de enlace externo"){: new_window}.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// En este ejemplo, la escucha de autenticación devuelve inmediatamente un conjunto de
	// credenciales codificadas. En una situación real es donde el desarrollador vería una
	// pantalla de inicio de sesión, recopilaría las credenciales e invocaría la API
	// authenticationContext.submitAuthenticationChallengeAnswer()

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// En caso de que se produzca un error al recopilar las credenciales, tendrá
	// que notificarlo a authenticationContext. De lo contrario, el SDK del cliente Mobile
	// Client Access permanecerá siempre en estado de espera de las credenciales

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){
		console.log("onAuthenticationFailure :: ", info);
	}
}
```
{: codeblock}

## Registro de una escucha de autenticación personalizada en Cordova WebView
{: #custom-cordova-authreg}

Después de crear una escucha de autenticación personalizada, debe registrarla con `BMSClient` antes de empezar a utilizarla. Añada el código siguiente a la aplicación.  Llame a este código antes de enviar solicitudes a los recursos protegidos.

```Java
BMSClient.registerAuthenticationListener(<realmName>, customAuthenticationListener);
```
{: codeblock}
 Utilice el `realmName` que indicó en el panel de control de {{site.data.keyword.amashort}}.

## Establezca el gestor de autorización en el código nativo

El gestor de autorización de {{site.data.keyword.amashort}} debe estar registrado en el código de la plataforma nativa.

**Android** (añádalo a `onCreate` en la actividad principal)

```
String tenantId = "<tenantId>";
MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}

**iOS Objective-C** (añádalo a `AppDelegate.m`)

Registre el gestor de autorización de acuerdo con su versión de Xcode.

```
#import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions

{  

    //[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
 }
```
{: codeblock}

Nota: Para el nombre de archivo de cabecera correcto de Swift, sustituya `your_module_name` por el nombre del módulo del proyecto, por ejemplo, si el nombre del módulo es `Cordova`, debería especificar `#import "Cordova-Swift.h"`. Para buscar el nombre del módulo, vaya a **Crear configuración > Paquete > Nombre del módulo del producto**.

**Nota:** Sustituya `tenantId` por el id de arrendatario que encontrará en el botón **Opciones móviles** del panel de control del servicio {{site.data.keyword.amashort}}.


## Habilitación de Keychain Sharing para iOS

Para habilitar `Keychain Sharing`, vaya al separador `Capacidades` y `active` `Keychain Sharing` en el proyecto Xcode.


## Prueba de autenticación
{: #custom-cordova-test}
Después de inicializar el SDK del cliente y registrar una `AuthenticationListener` personalizada, puede empezar a realizar solicitudes a la aplicación de fondo móvil.

### Antes de empezar
{: #custom-cordova-testing-before}
Debe tener una aplicación que se haya creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y que disponga de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`.


1. Envíe una solicitud al punto final protegido del programa de fondo móvil en su navegador; para ello, abra `{applicationRoute}/protected`, por ejemplo `http://my-mobile-backend.mybluemix.net/protected`.
 El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} está protegido con {{site.data.keyword.amashort}}. Solo pueden acceder al punto final las aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Si no, se muestra un mensaje `Unauthorized` en el navegador.

1. Utilice la aplicación de Cordova para realizar solicitudes al mismo punto final. Añada el código siguiente después de inicializar `BMSClient` y registrar la clase AuthenticationListener personalizada.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

	Sustituya `<your-application-route>` por el URL de la aplicación de programa de fondo (consulte [Antes de empezar](#before-you-begin)).

1. 	Cuando la solicitud se realiza correctamente, se muestra la salida siguiente en la consola de Xcode o `LogCat`:

	![imagen](images/android-custom-login-success.png)

	![imagen](images/ios-custom-login-success.png)
