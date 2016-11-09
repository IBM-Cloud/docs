---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"
---
{:screen: .screen}
{:shortdesc: .shortdesc}

# Habilitación de la autenticación de Google para apps de Cordova
{: #google-auth-cordova}


Para configurar las aplicaciones de Cordova de {{site.data.keyword.amafull}} para la integración de la autenticación de Google, debe realizar cambios en el código nativo de la aplicación de Cordova (Java, Objective-C o Swift). Debe configurar cada plataforma por separado. Utilice el entorno de desarrollo nativo para realizar cambios en el código nativo; por ejemplo, en Android Studio o Xcode.

## Antes de empezar
{: #before-you-begin}
Debe tener lo siguiente:
* Un proyecto Cordova que esté instrumentado con el SDK de cliente {{site.data.keyword.amashort}}.  Para obtener más información, consulte [Configuración del plugin de Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).  
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* (opcional) Familiarícese con las secciones siguientes:
   * [Habilitación de la autenticación de Google para apps de Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html)
   * [Habilitación de la autenticación de Google para apps de iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html)


## Configuración de la plataforma Android
{: #google-auth-cordova-android}

Los pasos necesarios para configurar la plataforma Android de una aplicación de Cordova para la integración de la autenticación de Google son muy parecidos a los pasos necesarios para las aplicaciones nativas. Consulte [Habilitación de la autenticación de Google para apps de Android](https://console.{DomainName}/docs/services/mobileaccess/google-auth-android.html) y configure lo siguiente:

* Configuración de un proyecto de Google para la plataforma Android
* Configuración de {{site.data.keyword.amashort}} para la autenticación de Google

### Configure el SDK de cliente {{site.data.keyword.amashort}} para Android Cordova


2. En la carpeta del proyecto de Android, abra el archivo `build.gradle` para el módulo de aplicación (**no** el archivo `build.gradle` del proyecto).
Busque la sección de dependencias y añada una nueva dependencia de compilación para el SDK del cliente:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

2. Sincronice el proyecto con Gradle pulsando **Tools > Android > Sync Project with Gradle Files**.

3. Para aplicaciones de Cordova, inicialice el SDK del cliente de {{site.data.keyword.amashort}} en código JavaScript en lugar de código Java. La API `GoogleAuthenticationManager` debe registrarse en código nativo. Añada este código al método `onCreate` de la actividad principal: 

	```Java
	GoogleAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

1. Añada el código siguiente a la actividad:
 
 	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	     super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
	         .onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## Configuración de la plataforma iOS
{: #google-auth-cordova-ios}

Los pasos necesarios para configurar la plataforma iOS de una aplicación de Cordova para la integración de la autenticación de Google son muy parecidos a los pasos para las aplicaciones nativas. La principal diferencia es que la CLI actualmente no admite el gestor de dependencias de CocoaPods.  Debe añadir manualmente los archivos necesarios para la integración con la autenticación de Google. Para obtener más información, consulte [Habilitación de la autenticación de Google en apps de iOS](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Siga los pasos siguientes:

* Configuración de un proyecto de Google para la plataforma iOS
* Configuración de {{site.data.keyword.amashort}} para la autenticación de Google

### Instalación manual del SDK de {{site.data.keyword.amashort}} para la autenticación de Google y el SDK de Google
{: #google-auth-cordova-ios-sdk}
1. Descargue el archivo que contiene el SDK de [{{site.data.keyword.Bluemix}} Mobile Services para iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).

1. Vaya al directorio `Sources/Authenticators/IMFGoogleAuthentication` y copie (arrastre y suelte) todos los archivos al proyecto de iOS en Xcode. Los archivos que debe copiar son:

	* IMFDefaultGoogleAuthenticationDelegate.h
	* IMFDefaultGoogleAuthenticationDelegate.m
	* IMFGoogleAuthenticationDelegate.h
	* IMFGoogleAuthenticationHandler.h
	* IMFGoogleAuthenticationHandler.m

	Seleccione el recuadro **Copiar archivos...**.

1. Descargue e instale el [SDK de Google+ para iOS](http://goo.gl/9cTqyZ).

1. Siga el paso 2 de la guía de aprendizaje [Iniciar la integración de Google+ en su app de iOS ](https://developers.google.com/+/mobile/ios/getting-started) para integrar el SDK de Google+ para iOS en el proyecto Xcode.

Continúe en la sección **Configuración del proyecto de iOS para la autenticación de Google** de [Configuración de la plataforma iOS para la autenticación de Google](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios.html). Registre `IMFGoogleAuthenticationHandler` en código nativo tal como se describe en la sección `Inicialización del SDK del cliente de {{site.data.keyword.amashort}}`. No inicialice `IMFClient` en el código nativo (el cliente se inicializa en JavaScript en la sección siguiente).

Añada esta línea al método `application:openURL:sourceApplication:annotation` del delegado de la aplicación. Esto garantiza que todos los plug-ins de Cordova reciban notificación de los sucesos correspondientes.

```
[[NSNotificationCenter defaultCenter] postNotification:[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```
{: codeblock}

## Inicialización del SDK del cliente de {{site.data.keyword.amashort}}
{: #google-auth-cordova-initialize}

Utilice el siguiente código JavaScript en la aplicación de Cordova para inicializar el SDK del cliente de {{site.data.keyword.amashort}}.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

Sustituya los valores de `applicationRoute` y `applicationGUID` por los valores **Ruta** e **Identificador exclusivo global de la app**. Puede encontrar estos valores pulsando el botón **Opciones móviles** desde dentro de la página de la aplicación en el panel de control.
	



##Inicialización de {{site.data.keyword.amashort}} AuthorizationManager
Utilice el siguiente código JavaScript en la aplicación de Cordova para inicializar el AuthorizationManager de {{site.data.keyword.amashort}}.

```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
```
{: codeblock}

Sustituya el valor de `tenantId` por el `tenantId` del servicio de {{site.data.keyword.amashort}}. Puede encontrar este valor pulsando el botón **Mostrar credenciales** en el icono del servicio {{site.data.keyword.amashort}}.





## Prueba de autenticación
{: #google-auth-cordova-test}
Después de inicializar el SDK del cliente, puede empezar a realizar solicitudes a la aplicación de programa de fondo móvil.

### Antes de empezar
{: #google-auth-cordova-testing-before}
Debe disponer de una aplicación de programa de fondo protegida por {{site.data.keyword.amashort}} en el punto final `/protected`. Si tiene que configurar un punto final `/protected`, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Intente enviar una solicitud al punto final protegido de su aplicación de fondo móvil en su navegador de escritorio abriendo `{applicationRoute}/protected`, por ejemplo `http://my-mobile-backend.mybluemix.net/protected`.

1. El punto final `/protected` de una aplicación móvil de fondo creada con MobileFirst Services Boilerplate está protegido con {{site.data.keyword.amashort}}; por tanto, solo se puede acceder al mismo mediante aplicaciones móviles instrumentadas con el SDK del cliente {{site.data.keyword.amashort}}. Como resultado, verá `Unauthorized` en el navegador de escritorio.

1. Utilice la aplicación de Cordova para realizar una solicitud al mismo punto final. Añada el siguiente código después de inicializar `BMSClient`.

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
{: codeblock}

1. Ejecute la aplicación. Se visualiza una pantalla de inicio de sesión de Google.

	![Pantalla de inicio de sesión de Google](images/android-google-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![Pantalla de inicio de sesión de Google](images/ios-google-login.png)
	
	Esta pantalla puede ser ligeramente diferente si no tiene instalada la app de Facebook en su dispositivo, o bien si no ha iniciado sesión en Facebook.
1. Si pulsa **Aceptar** está autorizando que {{site.data.keyword.amashort}} utilice su identidad de usuario de Google para fines de autenticación.

1. Su solicitud debería realizarse correctamente. Según la plataforma que utilice, verá la salida siguiente en la consola LogCat/Xcode:

	![Fragmento de código en android](images/android-google-login-success.png)

	![Fragmento de código en iOS](images/ios-google-login-success.png)
