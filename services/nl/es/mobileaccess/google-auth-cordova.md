---

copyright:
  años: 2015, 2016

---

# Habilitación de la autenticación de Google en apps de Cordova
{: #google-auth-cordova}
Para configurar aplicaciones de Cordova para la integración de la autenticación de Google, debe realizar cambios en el código nativo de la aplicación de Cordova; por ejemplo, en Java, Objective-C o Swift. Debe configurar cada plataforma por separado. Utilice el entorno de desarrollo nativo para realizar cambios en el código nativo; por ejemplo, en Android Studio o Xcode.

## Antes de empezar
{: #before-you-begin}
* Debe tener un recurso que esté protegido por {{site.data.keyword.amashort}} y un proyecto de Cordova instrumentado con el SDK del cliente de {{site.data.keyword.amashort}}.  Para obtener más información, consulte [Iniciación a {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) y [Configuración del plug-in de Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* Proteja manualmente la aplicación de fondo con el SDK del servidor de {{site.data.keyword.amashort}}. Para obtener más información, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* (opcional) Familiarícese con las secciones siguientes:
   * [Habilitación de la autenticación de Google en apps de Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Habilitación de la autenticación de Google en apps de iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## Configuración de la plataforma Android
{: #google-auth-cordova-android}

Los pasos necesarios para configurar la plataforma Android de una aplicación de Cordova para la integración de la autenticación de Google son muy parecidos a los pasos necesarios para las aplicaciones nativas. Para obtener más información, consulte [Habilitación de la autenticación de Google en apps de Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html). Configure los fragmentos siguientes:

* Configuración de un proyecto de Google para la plataforma Android
* Configuración de {{site.data.keyword.amashort}} para la autenticación de Google
* Configuración del SDK del cliente de {{site.data.keyword.amashort}} para Android

La única diferencia que existe cuando se configuran aplicaciones de Cordova es que se debe inicializar el SDK del cliente de {{site.data.keyword.amashort}} en código JavaScript en lugar de código Java. La API `GoogleAuthenticationManager` debe registrarse en código nativo.

## Configuración de la plataforma iOS
{: #google-auth-cordova-ios}

Los pasos necesarios para configurar la plataforma iOS de una aplicación de Cordova para la integración de la autenticación de Google son muy parecidos a los pasos para las aplicaciones nativas. La principal diferencia es que la CLI actualmente no admite el gestor de dependencias de CocoaPods.  Debe añadir manualmente los archivos necesarios para la integración con la autenticación de Google. Para obtener más información, consulte [Habilitación de la autenticación de Google en apps de iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Siga los pasos siguientes:

* Configuración de un proyecto de Google para la plataforma iOS
* Configuración de {{site.data.keyword.amashort}} para la autenticación de Google

### Instalación manual del SDK de {{site.data.keyword.amashort}} para la autenticación de Google y el SDK de Google
{: #google-auth-cordova-ios-sdk}
1. Descargue el archivo que contiene el [SDK de {{site.data.keyword.Bluemix}} Mobile Services para iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)

1. Vaya al directorio `Sources/Authenticators/IMFGoogleAuthentication` y copie (arrastre y suelte) todos los archivos al proyecto de iOS en Xcode. Los archivos que debe copiar son:

	> * IMFDefaultGoogleAuthenticationDelegate.h
	> * IMFDefaultGoogleAuthenticationDelegate.m
	> * IMFGoogleAuthenticationDelegate.h
	> * IMFGoogleAuthenticationHandler.h
	> * IMFGoogleAuthenticationHandler.m

Seleccione el recuadro **Copiar archivos...**.

1. Descargue e instale el [SDK de Google+ para iOS](http://goo.gl/9cTqyZ).

1. Siga el paso 2 de la guía de aprendizaje [Iniciar la integración de Google+ en su app de iOS ](https://developers.google.com/+/mobile/ios/getting-started) para integrar el SDK de Google+ para iOS en el proyecto Xcode.

Continúe en la sección **Configuración del proyecto de iOS para la autenticación de Google** de [Configuración de la plataforma iOS para la autenticación de Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Registre `IMFGoogleAuthenticationHandler` en código nativo tal como se describe en la sección `Inicialización del SDK del cliente de {{site.data.keyword.amashort}}`. No es necesario para inicializar `IMFClient` en el código nativo, esto se realizará en código JavaScript en breve.

Añada la línea siguiente al método `application:openURL:sourceApplication:annotation` del delegado de la aplicación. Esta línea garantiza que todos los plug-ins de Cordova reciban notificación de los sucesos correspondientes.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #google-auth-cordova-initialize}

Utilice el siguiente código JavaScript en la aplicación de Cordova para inicializar el SDK del cliente de {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

Sustituya los valores *applicationRoute* y *applicationGUID* por los valores de **Ruta** e **Identificador exclusivo global de la app** que ha obtenido de la sección **Opciones móviles** de la aplicación en el panel de control. 

## Prueba de autenticación
{: #google-auth-cordova-test}
Después de inicializar el SDK del cliente, puede empezar a realizar solicitudes al programa de fondo móvil.

### Antes de empezar
{: #google-auth-cordova-testing-before}
Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Si tiene que configurar un punto final `/protected`, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Intente enviar una solicitud al punto final protegido del programa de fondo móvil en su navegador de escritorio; para ello, abra `{applicationRoute}/protected`. Por ejemplo, `http://mi-programa-fondo-móvil.mybluemix.net/protected`.


1. El punto final `/protected` de un programa de fondo móvil creado con el contenedor modelo de MobileFirst Services está protegido con {{site.data.keyword.amashort}}; por tanto, solo se puede acceder al mismo mediante aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}. Como resultado, verá `Unauthorized` en el navegador de escritorio.

1. Utilice la aplicación de Cordova para realizar solicitudes al mismo punto final. Añada el código siguiente después de inicializar `BMSClient`

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


1. Ejecute la aplicación. Aparece una pantalla de inicio de sesión de Google.

	![imagen](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-google-login.png)
	Esta pantalla puede ser ligeramente diferente si no tiene instalada la app de Facebook en su dispositivo, o bien si no ha iniciado sesión en Facebook.
1. Si pulsa **Aceptar** está autorizando que {{site.data.keyword.amashort}} utilice su identidad de usuario de Google para fines de autenticación.

1. 	Su solicitud debería realizarse correctamente. Según la plataforma que esté utilizando, debería ver la salida siguiente en la consola de LogCat/Xcode.

	![imagen](images/android-google-login-success.png)

	![imagen](images/ios-google-login-success.png)
