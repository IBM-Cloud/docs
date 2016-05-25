---

copyright:
  años: 2015, 2016

---

# Configuración del SDK del cliente de {{site.data.keyword.amashort}} para Android
{: #custom-android}
Configure su aplicación de Android con autenticación personalizada para que utilice el SDK del cliente de {{site.data.keyword.amashort}} y conecte la aplicación a {{site.data.keyword.Bluemix}}.

## Antes de empezar
{: #before-you-begin}
Debe tener un recurso que esté protegido por una instancia del servicio de {{site.data.keyword.amashort}} que esté configurado para utilizar un proveedor de identidad personalizado.  Su app para móvil debe instrumentarse con el SDK del cliente de {{site.data.keyword.amashort}}.  Para obtener más información, consulte la siguiente información:
 * [Iniciación a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configuración del SDK de Android](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)
 * [Utilización de un proveedor de identidad personalizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Creación de un proveedor de identidad personalizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #custom-android-initialize}
1. En el proyecto de Android en Android Studio, abra el archivo `build.gradle` del módulo de la app.
<br/>**Sugerencia:** es posible que el proyecto de Android tenga dos archivos `build.gradle`: para el proyecto y para el módulo de la aplicación. Utilice el archivo del módulo de la aplicación.

1. En el archivo `build.gradle`, busque la sección `dependencies` y compruebe la siguiente dependencia de compilación. Añada esta dependencia si todavía no existe.

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// otras dependencias  
	}
	```

1. Sincronice el proyecto con Gradle. Pulse **Tools > Android > Sync Project with Gradle Files**.

1. Abra el archivo `AndroidManifest.xml` del proyecto de Android.
Añada el permiso de acceso a Internet al elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```

1. Inicialice el SDK.  
Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `onCreate` de la actividad principal de la aplicación de Android.
Sustituya *applicationRoute* y *applicationGUID* por los valores de **Ruta** e **Identificador exclusivo global de la app** que se obtienen al pulsar **Opciones móviles** en la app en el panel de control de {{site.data.keyword.Bluemix_notm}}.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");					
	```

## Interfaz AuthenticationListener
{: #custom-android-authlistener}

El SDK del cliente de {{site.data.keyword.amashort}} proporciona la interfaz `AuthenticationListener` para poder implementar un flujo de autenticación personalizada. La interfaz `AuthenticationListener` expone tres métodos a los que se llama en distintas fases del proceso de autenticación.

### Método onAuthenticationChallengeReceived
{: #custom-onAuth}
Llame a este método cuando se reciba un cambio de autenticación personalizada desde el servicio de {{site.data.keyword.amashort}}.

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
#### Argumentos
{: #custom-android-onAuth-arg}

* `AuthenticationContext`: proporcionado por el SDK del cliente de {{site.data.keyword.amashort}} para que pueda volver a notificar los errores o las respuestas al cambio de autenticación durante la recopilación de credenciales.  Por ejemplo, cuando un usuario cancela la autenticación.
* `JSONObject`: contiene un cambio de autenticación personalizada, tal como se devuelve desde un proveedor de identidad personalizado.
* `Context`: una referencia al contexto de Android utilizado cuando se envió la solicitud. Normalmente este argumento representa una actividad de Android.

Al llamar al método `onAuthenticationChallengeReceived`, el SDK del cliente de {{site.data.keyword.amashort}} delega el control al desarrollador.  El servicio espera las credenciales. El desarrollador debe recopilar las credenciales y notificarlas al SDK del cliente de {{site.data.keyword.amashort}} utilizando uno de los métodos de la interfaz `AuthenticationContext`.

### Método onAuthenticationSuccess
{: #custom-android-authlistener-onsuccess}
Llame a este método después de una autenticación satisfactoria. Los argumentos incluyen el contexto de Android y un JSONObject opcional que contiene información ampliada sobre el éxito de la autenticación.
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```

### Método onAuthenticationFailure
{: #custom-android-authlistener-onfail}
Llame a este método después de un error en la autenticación. Los argumentos incluyen el contexto de Android y un JSONObject opcional que contiene información ampliada sobre el error en la autenticación.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```

## Interfaz AuthenticationContext
{: #custom-android-authcontext}

`AuthenticationContext` se proporciona como un argumento del método `onAuthenticationChallengeReceived` de una `AuthenticationListener` personalizada. Debe recopilar las credenciales y utilizar los métodos `AuthenticationContext` para devolver las credenciales al SDK del cliente de {{site.data.keyword.amashort}} o para notificar un error. Utilice uno de los métodos siguientes:

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
```Java
void submitAuthenticationFailure (JSONObject info);
```

## Implementación de ejemplo de una AuthenticationListener personalizada
{: #custom-android-samplecustom}

Este ejemplo de AuthenticationListener está diseñado para que funcione con un proveedor de identidad personalizado. Puede descargar este ejemplo del [repositorio Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {
	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// En este ejemplo, AuthenticationListener devuelve inmediatamente un conjunto de
		// credenciales codificadas. En una situación real es donde el desarrollador vería una
	// pantalla de inicio de sesión, recopilaría las credenciales e invocaría la API
	// authContext.submitAuthenticationChallengeAnswer()

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// En caso de que se produzca un error al recopilar las credenciales, tendrá
	// que notificarlo a AuthenticationContext. De lo contrario, el SDK del cliente Mobile
	// Client Access permanecerá siempre en estado de espera
	// de las credenciales

			log("This should never happen...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}

	@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```

## Registro de una clase AuthenticationListener personalizada
{: #custom-android-register}

Después de crear una clase AuthenticationListener personalizada, regístrela con `BMSClient` antes de empezar a utilizar la escucha. Añada el código siguiente a la aplicación. Debe llamarse a este código antes de enviar solicitudes a los recursos protegidos.

```Java
BMSClient.getInstance().registerAuthenticationListener(realmName,
									new CustomAuthenticationListener());
```

Utilice el valor de *realmName* que indicó en el panel de control de {{site.data.keyword.amashort}}.


## Prueba de autenticación
{: #custom-android-testing}
Después de inicializar el SDK del cliente y registrar una AuthenticationListener personalizada, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #custom-android-testing-before}
Debe tener una aplicación que se haya creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y que disponga de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`.


1. Envíe una solicitud al punto final protegido del programa de fondo móvil en su navegador; para ello, abra `{applicationRoute}/protected`, por ejemplo `http://mi-programa-fondo-móvil.mybluemix.net/protected`.

1. El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de {{site.data.keyword.mobilefirstbp}} está protegido con {{site.data.keyword.amashort}}. Solo pueden acceder al punto final las aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Si no, se muestra un mensaje `Unauthorized` en el navegador.

1. Utilice la aplicación de Android para realizar solicitudes al mismo punto final. Añada el código siguiente después de inicializar `BMSClient` y registrar la clase AuthenticationListener personalizada.

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
```

1. 	Cuando la solicitud se realiza correctamente, se muestra la siguiente salida en la herramienta LogCat:

	![imagen](images/android-custom-login-success.png)

1. También puede añadir la funcionalidad de finalización de sesión añadiendo este código: 

 ```Java
 AuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Si invoca este código después de que el usuario haya iniciado sesión, la sesión del usuario se cerrará. Cuando el usuario intente iniciar sesión de nuevo, deberá volver a responder a la pregunta que reciba del servidor. 

 El valor para `listener` que se pasa a la función de cierre de sesión puede ser nulo. 
