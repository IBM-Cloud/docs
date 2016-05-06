---

copyright:
  años: 2015, 2016

---

# Configuración del SDK del cliente de {{site.data.keyword.amashort}} para Cordova
{: #custom-cordova}
Configure su aplicación de Cordova con autenticación personalizada para que utilice el SDK del cliente de {{site.data.keyword.amashort}} y conecte la aplicación a {{site.data.keyword.Bluemix}}.


## Antes de empezar
{: #before-you-begin}
Debe tener un recurso que esté protegido por una instancia del servicio de {{site.data.keyword.amashort}} que esté configurado para utilizar un proveedor de identidad personalizado.  Su app para móvil debe instrumentarse con el SDK del cliente de {{site.data.keyword.amashort}}.  Para obtener más información,
consulte la siguiente información:
 * [Iniciación a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configuración del SDK de Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [Utilización de un proveedor de identidad personalizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creación de un proveedor de identidad personalizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #custom-cordova-sdk}
Inicialice el SDK pasando los parámetros applicationGUID y applicationRoute.

1. Obtenga los valores de los parámetros de la aplicación. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}. Pulse **Opciones móviles**. Se muestran los valores **Ruta** (`applicationRoute`) e **Identificador exclusivo global de la app** (`applicationGUID`). 
1. Inicialice el SDK del cliente.

	```JavaScript
	BMSClient.initialize(applicationRoute, applicationGUID);

	```
 Sustituya *applicationRoute* y *applicationGUID* por los valores de **Ruta** e **Identificador exclusivo global de la app** del panel **Opciones móviles** de la aplicación en el panel de control de {{site.data.keyword.Bluemix_notm}}. 

## Interfaz de escucha de autenticación
{: #custom-cordva-auth}

El SDK del cliente de {{site.data.keyword.amashort}} proporciona una interfaz de escucha de autenticación para implementar un flujo de autenticación personalizada. Debe añadir los métodos siguientes a los que se llama en diferentes fases de un proceso de autenticación.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

Cada método gestiona una fase diferente de un proceso de autenticación.

### Método onAuthenticationChallengeReceived
{: #onAuthenticationChallengeReceived}
Se llama a este método cuando se recibe un cambio de autenticación personalizada desde el servicio de {{site.data.keyword.amashort}}.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### Argumentos
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext`: proporcionado por el SDK del cliente de {{site.data.keyword.amashort}} para que el desarrollador pueda volver a notificar los errores o las respuestas al cambio de autenticación durante la recopilación de credenciales, como si el usuario cancela una solicitud de autenticación.
* `challenge`: un objeto JSON que contiene un cambio de autenticación personalizada, tal como se devuelve desde un proveedor de identidad personalizado.

Llamando al método `onAuthenticationChallengeReceived`, el SDK del cliente de {{site.data.keyword.amashort}} delega el control al desarrollador. {{site.data.keyword.amashort}} espera las credenciales. El desarrollador debe recopilar las credenciales y volverlas a notificar al SDK del cliente de {{site.data.keyword.amashort}} utilizando uno de los métodos siguientes de la interfaz `authContext`:

```JavaScript
onAuthenticationSuccess: function(info){...}
```

Se llama a este método después de realizarse una autenticación correcta. Los argumentos incluyen un JSONObject opcional que contiene información ampliada sobre el éxito de la autenticación.

```JavaScript
onAuthenticationFailure: function(info){...}
```

Se llama a este método después de un error de autenticación. Los argumentos incluyen un JSONObject opcional que contiene información ampliada sobre el error de la autenticación.

## authenticationContext
{: #custom-cordova-authcontext}

El valor de `authenticationContext` se proporciona como un argumento del método `onAuthenticationChallengeReceived` de una escucha de autenticación personalizada. El desarrollador debe recopilar las credenciales y utilizar los métodos `authenticationContext` para devolver las credenciales al SDK del cliente de {{site.data.keyword.amashort}} o para notificar un error. Utilice uno de los métodos siguientes:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## Implementación de ejemplo de una escucha de autenticación personalizada
{: #custom-cordova-authlisten-sample}

Este ejemplo de escucha de autenticación se ha diseñado para que funcione con un proveedor de identidad personalizado. Puede descargar el proveedor de identidad personalizado desde [este repositorio Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

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

## Registro de una escucha de autenticación personalizada
{: #custom-cordova-authreg}

Después de crear una escucha de autenticación personalizada, regístrela con `BMSClient` antes de empezar a utilizarla. Añada el código siguiente a la aplicación.  Llame a este código antes de enviar solicitudes a los recursos protegidos.

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 Utilice el *realmName* que indicó en el panel de control de {{site.data.keyword.amashort}}.


## Prueba de autenticación
{: #custom-cordova-test}
Después de inicializar el SDK del cliente y registrar una AuthenticationListener personalizada, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #custom-cordova-testing-before}
Debe tener una aplicación que se haya creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y que disponga de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`.


1. Envíe una solicitud al punto final protegido del programa de fondo móvil en su navegador; para ello, abra `{applicationRoute}/protected`, por ejemplo `http://mi-programa-fondo-móvil.mybluemix.net/protected`. El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} está protegido con {{site.data.keyword.amashort}}. Solo pueden acceder al punto final las aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Si no, se muestra un mensaje `Unauthorized` en el navegador.

1. Utilice la aplicación de Cordova para realizar solicitudes al mismo punto final. Añada el código siguiente después de inicializar `BMSClient` y registrar la clase AuthenticationListener personalizada.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. 	Cuando la solicitud se realiza correctamente, se muestra la salida siguiente en la consola de Xcode o LogCat:

	![imagen](images/android-custom-login-success.png)

	![imagen](images/ios-custom-login-success.png)
