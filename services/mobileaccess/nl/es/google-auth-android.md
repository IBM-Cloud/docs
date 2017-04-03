---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

El servicio {{site.data.keyword.amafull}} se sustituye por el servicio {{site.data.keyword.appid_full}}.

# Habilitación de la autenticación de Google para apps de Android
{: #google-auth-android}

Utilice Google para autenticar usuarios para la aplicación Android de {{site.data.keyword.amafull}}. Añada la funcionalidad de seguridad de {{site.data.keyword.amashort}}.

## Antes de empezar
{: #before-you-begin}

Debe tener lo siguiente:

* Una instancia de un servicio de {{site.data.keyword.amafull}} y una aplicación {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* El URL de la aplicación de programa de fondo (**Ruta de app**). Necesitará estos valores para enviar solicitudes a los puntos finales protegidos de la aplicación de programa de fondo.
* El valor de **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su {{site.data.keyword.Bluemix_notm}} **Región**. Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de región que aparece debe ser uno de los siguientes: `EE.UU. Sur`, `Reino Unido` o `Sidney` y debe corresponder con los valores de SDK necesarios en el código Javascript de WebView: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` o `BMSClient.REGION_UK`. Necesitará este valor para inicializar el cliente {{site.data.keyword.amashort}}.
* Un proyecto Android configurado para funcionar con Gradle. No es necesario instrumentar el proyecto con el SDK de cliente de {{site.data.keyword.amashort}}.  

Para configurar la autenticación de Google para su app Android {{site.data.keyword.amashort}} necesitará realizar otros pasos de configuración:

* De la aplicación {{site.data.keyword.Bluemix_notm}}
* De su proyecto de Android Studio

## Creación de un proyecto en Google Developer Console
{: #create-google-project}

Para empezar a utilizar Google como proveedor de identidad, cree un proyecto en la [Google Developer Console ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://console.developers.google.com){: new_window}.
Parte de la creación de un proyecto consiste en obtener un ID de cliente de Google.  El ID de cliente de Google es un identificador exclusivo para su aplicación que se utiliza en la autenticación de Google y se necesita para configurar el servicio {{site.data.keyword.amashort}}.

Desde la consola:

1. Cree un proyecto mediante la API de **Google+**.
2. Añada el acceso de usuario **OAuth**.
3. Antes de añadir las credenciales, debe elegir la plataforma (Android).
4. Añada las credenciales.

Para completar el proceso de creación de credenciales, debe añadir **la huella dactilar del certificado de firma**.


### Configuración del certificado de firma
{: #signing_cert}

Para que Google verifique la autenticidad de la aplicación, debe especificar una huella dactilar del certificado para firmas.

El sistema operativo Android necesita que todas las aplicaciones instaladas en un dispositivo Android estén firmadas con un certificado de desarrollador. Una aplicación de Android se puede compilar con dos modos: depuración y publicación. Normalmente se recomienda tener certificados diferentes para los modos de depuración y publicación.  Los certificados que se utilizan para firmar aplicaciones de Android en modo de depuración se empaquetan con el SDK de Android.  Android Studio suele instalar automáticamente el SDK de Android. Cuando quiera publicar su aplicación en la tienda Google Play deberá firmar la app con otro certificado, que normalmente genera usted mismo. Para obtener más información, consulte [firma de sus aplicaciones Android ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}.

Un almacén de claves con un certificado para entornos de desarrollo se almacena en un archivo `~/.android/debug.keystore`. La contraseña del almacén de claves por defecto es `android`. Este certificado se utiliza para compilar aplicaciones en modo de depuración.

1. Recupere la huella dactilar del certificado de firma de su entorno de desarrollo de cliente:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	{: codeblock}

	También puede utilizar la misma sintaxis para recuperar el hash de clave de su certificado de modo de depuración. Sustituya el alias y la vía de acceso al almacén de claves en el mandato.

1. En el diálogo Credenciales de la consola de Google, busque la línea que empieza por `SHA1` en **Huellas dactilares de certificados**. Copie en el recuadro de texto el valor de huella dactilar obtenido al ejecutar el mandato **keytool**.

###Nombre del paquete

1. En el diálogo Credenciales, introduzca el nombre del paquete de su aplicación Android.

	Para encontrar el nombre de paquete de la aplicación de Android, abra el archivo `AndroidManifest.xml` en Android Studio y busque:

	```
	<manifest package="{your-package-name}">
	```
	{: codeblock}

1. Cuando haya terminado, haga clic en **Crear**. De este modo finaliza el proceso de creación de credenciales.

###ID de cliente de Google
{: #google-client-id}

Una vez que las credenciales se han creado correctamente, la página de credenciales muestra su ID de cliente de Google. Anote este valor. Debe registrar este valor en la aplicación {{site.data.keyword.Bluemix}}.


## Configuración de {{site.data.keyword.amashort}} para la autenticación de Google
{: #google-auth-android-config}

Ahora que ya tiene un ID de cliente de Google para Android, puede habilitar la autenticación de Google en el panel de instrumentos de {{site.data.keyword.amashort}}.

1. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}.
1. En el separador **Gestionar**, active **Autorización**.
1. Expanda la sección **Google**.
1. En **ID de cliente para Android**, especifique su ID de cliente de Google para Android y pulse **Guardar**.

## Configuración del SDK del cliente de {{site.data.keyword.amashort}} para Android
{: #google-auth-android-sdk}

Desde el proyecto Android Studio.

1. Abra el archivo `build.gradle` del módulo de la app.

	Es posible que el proyecto de Android tenga dos archivos `build.gradle`: uno para el proyecto y otro para el módulo de la aplicación. Utilice el del módulo de la aplicación.

	Busque la sección de dependencias y añada una nueva dependencia de compilación para el SDK del cliente:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// otras dependencias
	}
	```
	{: codeblock}

	**Nota:** puede eliminar la dependencia del módulo `core` del grupo `com.ibm.mobilefirstplatform.clientsdk.android` si lo tiene. El módulo `googleauthentication` se descarga automáticamente. El módulo `googleauthentication` descarga e instala Google+ SDK en su proyecto Android.

1. Sincronice el proyecto con Gradle pulsando **Tools > Android > Sync Project with Gradle Files**.

1. Abra el archivo `AndroidManifest.xml` del proyecto de Android.

1. Añada el permiso de acceso a Internet al elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```
	{: codeblock}

1. Para utilizar el SDK del cliente de {{site.data.keyword.amashort}}, debe inicializarlo pasando los parámetros **context** y **region**.

	Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `onCreate` de la actividad principal de la aplicación de Android.

1. Inicialice el SDK del cliente y registre el gestor de autenticación de Google.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	GoogleAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

	* Sustituya `BMSClient.REGION_UK` por su **Región** de {{site.data.keyword.Bluemix_notm}}.
	* Sustituya `<MCAServiceTenantId>` por el valor **TenantId**.

	Para obtener más información sobre cómo obtener estos valores, consulte [Antes de empezar](##before-you-begin).

	**Nota:** Si su aplicación Android está dirigida a Android versión 6.0 (nivel de API 23) o superior, deberá asegurarse de que la aplicación tenga una llamada `android.permission.GET_ACCOUNTS` antes de llamar al `registro`. Para obtener más información, consulte [Solicitud de permisos en Android ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.android.com/training/permissions/requesting.html){: new_window}.

1. Añada el código siguiente a la actividad:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## Prueba de autenticación
{: #google-auth-android-test}

Después de inicializar el SDK del cliente y registrar el gestor de autenticación de Google, puede empezar a realizar solicitudes al programa de fondo.

Antes de empezar a realizar pruebas, debe disponer de una aplicación de fondo móvil que se haya creado con el contenedor modelo **MobileFirst Services Starter**, y que tenga un recurso protegido por el punto final {{site.data.keyword.amashort}} `/protected`. Para obtener más información, consulte [Protección de recursos](protecting-resources.html).

1. Intente enviar una solicitud al punto final protegido del programa de fondo móvil en su navegador de escritorio; para ello, abra `{applicationRoute}/protected`. Por ejemplo, `http://my-mobile-backend.mybluemix.net/protected`.  Para obtener información sobre cómo obtener el valor `{applicationRoute}`, consulte [Antes de comenzar](#before-you-begin).

	El punto final `/protected` de un programa de fondo móvil creado con un contenedor modelo de MobileFirst Services está protegido con {{site.data.keyword.amashort}}. Por eso, solo las aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}} pueden acceder a él. Como resultado, verá `Unauthorized` en el navegador de escritorio.

1. Utilice la aplicación de Android para realizar solicitudes al mismo punto final protegido. Añada el código siguiente después de inicializar la instancia `BMSClient` y registrar `GoogleAuthenticationManager`.

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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
	{: codeblock}

1. Ejecute la aplicación. Aparece una pantalla de inicio de sesión de Google. Después de iniciar sesión, la aplicación solicita permisos para acceder a recursos:

	![imagen](images/android-google-login.png)

	En función del dispositivo Android y si ha iniciado sesión en Google, es posible que tenga una IU diferente.

	Si pulsa **Aceptar** está autorizando que {{site.data.keyword.amashort}} utilice su identidad de usuario de Google para fines de autenticación.

1. 	Después de que la solicitud se haya completado correctamente, se mostrará la siguiente salida en la herramienta LogCat:

	![imagen](images/android-google-login-success.png)

	También puede añadir la funcionalidad de finalización de sesión añadiendo este código:

	```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	Si invoca este código después de que un usuario haya iniciado sesión en Google, dicha sesión se cerrará. Cuando el usuario intente iniciar sesión de nuevo, deberá seleccionar una cuenta de Google para poder hacerlo. Si el usuario intenta iniciar sesión con un ID de Google con el que haya iniciado sesión anteriormente, no se le pedirán de nuevo las credenciales. Para pedir de nuevo las credenciales, el usuario debe eliminar su cuenta de Google del dispositivo Android.

	El valor para `listener` que se pasa a la función de cierre de sesión puede ser `null`.
