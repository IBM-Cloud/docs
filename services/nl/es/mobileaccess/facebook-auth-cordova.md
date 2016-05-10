---

copyright:
  años: 2015, 2016

---

# Habilitación de la autenticación de Facebook en apps de Cordova
{: #facebook-auth-cordova}
Para configurar aplicaciones de Cordova para la integración de la autenticación de Facebook, debe realizar cambios en el código nativo de la aplicación de Cordova en Java, Objective-C o Swift. Configure cada plataforma de forma separada. Utilice el entorno de desarrollo nativo para realizar cambios en el código nativo; por ejemplo, en Android Studio o Xcode.

## Antes de empezar
{: #facebook-auth-before}
* Debe tener un recurso que esté protegido por {{site.data.keyword.amashort}} y un proyecto de Cordova instrumentado con el SDK del cliente de {{site.data.keyword.amashort}}.  Para obtener más información, consulte [Iniciación a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) y [Configuración del plug-in de Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).
* Proteja manualmente la aplicación de fondo con el SDK del servidor de {{site.data.keyword.amashort}}. Para obtener más información, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* Cree un ID de aplicación de Facebook. Para obtener más información, consulte [Cómo obtener un ID de aplicación de Facebook desde el portal de desarrolladores de Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).
* (opcional) Familiarícese con las secciones siguientes:
   * [Habilitación de la autenticación de Facebook en apps de Android](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html)
   * [Habilitación de la autenticación de Facebook en apps de iOS](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html)


## Configuración de la plataforma Android
{: #facebook-auth-cordova-android}

Los pasos necesarios para configurar la plataforma Android de una aplicación de Cordova para la integración de la autenticación de Facebook son muy parecidos a los pasos necesarios para las aplicaciones de Android nativas. Para obtener más información, consulte [Habilitación de la autenticación de Facebook en apps de Android](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html). Siga los pasos siguientes:

* Configuración de una aplicación de Facebook para la plataforma Android
* Configuración de {{site.data.keyword.amashort}} para la autenticación de Facebook
* Configuración del SDK del cliente de {{site.data.keyword.amashort}} para Android

La única diferencia que existe cuando se configuran aplicaciones de Cordova es que se debe inicializar el SDK del cliente de {{site.data.keyword.amashort}} en código JavaScript en lugar de código Java. La API `FacebookAuthenticationManager` debe registrarse en código nativo.

## Configuración de la plataforma iOS
{: #facebook-auth-cordova-ios}

Los pasos necesarios para configurar la plataforma iOS de una aplicación de Cordova para la integración de la autenticación de Facebook son muy parecidos a los pasos necesarios para las aplicaciones de iOS nativas. La principal diferencia es que la CLI actualmente no admite el gestor de dependencias de CocoaPods. Debe añadir manualmente los archivos necesarios para la integración con la autenticación de Facebook. Para obtener más información, consulte [Habilitación de la autenticación de Facebook en apps de iOS](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Siga los pasos siguientes:

* Configuración de una aplicación de Facebook para la plataforma iOS
* Configuración de {{site.data.keyword.amashort}} para la autenticación de Facebook

### Instalación manual del SDK de {{site.data.keyword.amashort}} para la autenticación de Facebook y el SDK de Facebook
{: #facebook-auth-cordova-ios-sdk}
1. Descargue el archivo que contiene el [SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services para iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).

1. Vaya al directorio `Sources/Authenticators/IMFFacebookAuthentication` y copie (arrastre y suelte) todos los archivos al proyecto de iOS en Xcode. Copie los archivos siguientes:
	* IMFDefaultFacebookAuthenticationDelegate.h
  * IMFDefaultFacebookAuthenticationDelegate.m
	* IMFFacebookAuthenticationDelegate.h
	* IMFFacebookAuthenticationHandler.h
	* IMFFacebookAuthenticationHandler.m

	Cuando Xcode lo solicite, seleccione **Copiar archivos...**.

1. Descargue e instale [Facebook SDK v3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg).

1. El SDK de Facebook se instalará en el directorio `~/Documents/FacebookSDK`. Navegue a ese directorio y copie (arrastre y suelte) el archivo `FacebookSDK.framework` al proyecto de iOS en Xcode.

1. 	Pulse la raíz de proyecto en el panel izquierdo de Xcode y seleccione **Crear fases**.

1. Añada el archivo `FacebookSDK.framework` a la lista de bibliotecas enlazadas en **Enlace binario con bibliotecas**.

 Consulte el apartado sobre [Configuración de la plataforma iOS para la autenticación de Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Registre la API `IMFFacebookAuthenticationHandler` en código nativo, tal como se describe en la sección **Inicialización del SDK de cliente de {{site.data.keyword.amashort}}**. No inicialice `IMFClient` en código nativo.

Añada la línea siguiente al método `application:openURL:sourceApplication:annotation` del delegado de la aplicación. Este código garantiza que todos los plug-ins de Cordova reciban notificación de los sucesos correspondientes.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #facebook-auth-cordova-init}

Utilice el siguiente código JavaScript en la aplicación de Cordova para inicializar el SDK del cliente de {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

Sustituya *applicationRoute* y *applicationGUID* por los valores correspondientes a **Ruta** e **Identificador exclusivo global de la app** obtenidos en **Opciones móviles**.

## Prueba de autenticación
{: #facebook-auth-cordova-test}
Después de inicializar el SDK del cliente y registrar el gestor de autenticación de Facebook, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Para obtener más información, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Intente enviar una solicitud al punto final protegido del programa de fondo móvil recién creado en su navegador. Abra el siguiente URL: `{rutaAplicación}/protected`. Por ejemplo: `http://mi-programa-fondo-móvil.mybluemix.net/protected`
<br/>El punto final `/protected` de un programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` en el navegador. Este mensaje se devuelve porque solo se puede acceder a este punto final con aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de Cordova para realizar solicitudes al mismo punto final. Añada el siguiente código después de inicializar `BMSClient`.

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

1. Ejecute la aplicación. Aparece una pantalla de inicio de sesión de Facebook:

	![imagen](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![imagen](images/ios-facebook-login.png)

	> Esta pantalla puede ser ligeramente diferente si no tiene instalada la app de Facebook en su dispositivo, o bien si no ha iniciado sesión en Facebook.

1. Pulse **Aceptar** para autorizar que {{site.data.keyword.amashort}} utilice su identidad de usuario de Facebook para fines de autenticación.

1. 	Cuando la solicitud se realiza correctamente, se muestra la salida siguiente en la consola de Xcode o del programa de utilidad LogCat:

	![Mensaje de realización de la autenticación de Facebook para Android](images/android-facebook-login-success.png)

	![Mensaje de realización de la autenticación de Facebook para iOS](images/ios-facebook-login-success.png)
