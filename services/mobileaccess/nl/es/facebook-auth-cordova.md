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

# Habilitación de la autenticación de Facebook para apps de Cordova
{: #facebook-auth-cordova}

Para configurar aplicaciones de Cordova de {{site.data.keyword.amafull}} para la integración de la autenticación de Facebook, configure cada plataforma por separado. La aplicación Cordova debe estar ya preparada con el SDK de {{site.data.keyword.amashort}}.

Tanto la plataforma nativa como el código Javascript de Cordova requieren cambios para habilitar la autenticación de Facebook.

Utilice el entorno de desarrollo nativo para realizar cambios en el código nativo; por ejemplo, en Android Studio o Xcode.
{:shortdesc}

## Antes de empezar
{: #facebook-auth-before}

Debe tener lo siguiente:
* Un proyecto Cordova (Android o iOS) instrumentado con el SDK de cliente {{site.data.keyword.amashort}}; consulte [Configuración del plugin Cordova](getting-started-cordova.html#getting-started-cordova-plugin).
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de un servicio de programa de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* La ruta de la aplicación. Es el URL de la aplicación de programa de fondo.
* El valor de `tenantId`. Abra el panel de control del servicio de {{site.data.keyword.amashort}}. Pulse **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará estos valores para inicializar el SDK y para enviar solicitudes al servicio del programa de fondo.
*  Busque la región en la que se aloja su servicio {{site.data.keyword.Bluemix_notm}}. Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar") en la barra de menús. El valor de región debe ser uno de los siguientes: **EE.UU. sur**, **Sídney** o **Reino Unido**. Los valores constantes de SDK exactos que se corresponden con estos nombres se indican en los ejemplos de código.
* Un ID de aplicación y una aplicación de Facebook. Para obtener más información, consulte [Creación de una aplicación en el sitio web de Facebook for Developers](facebook-auth-overview.html#facebook-appID).



## Configuración de la plataforma Android
{: #facebook-auth-cordova-android}

Los pasos necesarios para configurar la plataforma Android de una aplicación de Cordova para la integración de la autenticación de Facebook son muy parecidos a los pasos necesarios para las aplicaciones de Android nativas. Para obtener más información, consulte [Habilitación de la autenticación de Facebook en apps de Android](facebook-auth-android.html). Siga los pasos siguientes:

* [Configuración de la aplicación Facebook para la plataforma Android](facebook-auth-android.html#facebook-auth-android-config). Configura la autenticación de Facebook en el sitio de Facebook Developers para apps Android.
* [Configuración de MCA para la autenticación de Facebook](facebook-auth-android.html#facebook-auth-android-mca). Configura el servicio {{site.data.keyword.amashort}} en el servidor {{site.data.keyword.Bluemix}} para la autenticación de Facebook de Android.


### Configuración del SDK del cliente de Facebook de {{site.data.keyword.amashort}} para la plataforma Android
{: #configure_android}

El SDK del cliente de Facebook de {{site.data.keyword.amashort}} se debe añadir mediante Gradle en el proyecto nativo de la app Android.

1. En la carpeta del proyecto de Android, abra el archivo `build.gradle` para el módulo de aplicación (**no** el archivo `build.gradle` del proyecto). Busque la sección de dependencias y añada una nueva dependencia de compilación para el SDK del cliente:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

2. Pulse **Tools > Android > Sync Project with Gradle Files** para sincronizar el proyecto con Gradle.

3. Abra el archivo `android/res/values/strings.xml` y añada una serie `<facebook_app_id>` que contenga el ID de aplicación de Facebook.

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">"<facebook_app_id>"</string>
	</resources>
	```
	{: codeblock}

4. En el archivo `AndroidManifest.xml` del proyecto de Android (`android/manifests/AndroidManifest.xml`):

	* Añada los metadatos necesarios para el SDK de Facebook al elemento <application>:

    ```XML
    <application .......>
    <meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

    <activity ...../>
    <activity ...../>
    </application>
    ```
    {: codeblock}

   * Añada el elemento de actividad de Facebook en las actividades existentes:

    ```XML
    <application .....>
        <activity ...../>
		<activity ...../>

        <activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name"
        />
    </application>
    ```
    {: codeblock}

5. Añada lo siguiente al código de Activity Java.

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	   super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
	      .onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

### Inicialice el gestor de autorización en el código Android nativo
{: #initialize_android}

La API `FacebookAuthenticationManager` debe registrarse en código nativo. Añada este código al método `onCreate` de la actividad principal utilizando `<tenantId>` (consulte [Antes de empezar](#before-you-begin)).

```
String tenantId = "<tenantId>";
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
```
{: codeblock}


## Configuración de la plataforma iOS
{: #facebook-auth-cordova-ios}

Los pasos necesarios para configurar la plataforma iOS de una aplicación de Cordova para la integración de la autenticación de Facebook son muy parecidos a los pasos necesarios para las aplicaciones de iOS Swift nativas (los archivos de cabecera son necesarios para utilizar el código Objective-C con el SDK de Swift). La principal diferencia es que la CLI actualmente no admite el gestor de dependencias de CocoaPods. Debe añadir manualmente los archivos necesarios para la integración del cliente {{site.data.keyword.amashort}} con la autenticación de Facebook. Para obtener más información, consulte [Habilitación de la autenticación de Facebook en apps de iOS (Swift SDK)](facebook-auth-ios-swift-sdk.html). Siga los pasos siguientes:

* [Configuración de la aplicación Facebook para la plataforma iOS](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-config). Configura el servicio de autenticación de Facebook en el sitio de Facebook Developers.
* [Configuración de MCA para la autenticación de Facebook](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-configmca). Configura el servicio {{site.data.keyword.amashort}} en el servidor {{site.data.keyword.Bluemix}}.
* [Configuración del SDK del cliente Facebook de MCA para iOS](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-sdk). Instala el SDK de {{site.data.keyword.amashort}} iOS Swift para la autorización de Facebook mediante CocoaPods.


### Habilitación de Keychain Sharing para iOS
{: #enable_keychain}

Habilite `Keychain Sharing`. Vaya al separador `Capacidades` y `active` `Keychain Sharing` en el proyecto Xcode.

### Inicialice el gestor de autorización de {{site.data.keyword.amashort}} en Objective-C
{: #initialize_objc}

El gestor de autorización debe estar inicializado en el código Objective-C en el archivo `app-delegate.m`, de acuerdo con su versión de Xcode.

```
	#import "<your_module_name>-Swift.h"

	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[FacebookAuthenticationManager sharedInstance] register];

	    self.viewController = [[MainViewController alloc] init];

	    [[FacebookAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];


	    return [super application:application didFinishLaunchingWithOptions:launchOptions];
	}


	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

	   return [[FacebookAuthenticationManager sharedInstance] onOpenURLWithApplication:application
	   		url:url sourceApplication:sourceApplication annotation:annotation];
	}

```
{: codeblock}

**Nota:** el nombre del archivo de cabecera importado se compone del nombre del módulo concatenado con la serie `-Swift.h`, por ejemplo, si el nombre del módulo es `Cordova`, la línea de importación debería ser `#import "Cordova-Swift.h"` Para encontrar el nombre del módulo, vaya a `Crear configuración` > `Paquete` > `Nombre del módulo del producto`.

Sustituya `<tenantId>` por su id de arrendatario (consulte [Antes de empezar](#facebook-auth-before)).


##Inicialización del SDK del cliente de {{site.data.keyword.amashort}} en Cordova WebView
{: #initialize_webview}

Para todas las plataformas, utilice el siguiente código JavaScript en Cordova Javascript WebView para inicializar el SDK del cliente de {{site.data.keyword.amashort}}.

```javascript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

Sustituya `<applicationBluemixRegion>` por su región (consulte [Antes de empezar](#facebook-auth-before)).

## Prueba de autenticación
{: #facebook-auth-cordova-test}

Después de inicializar el SDK del cliente y de registrar el gestor de autenticación de Facebook, puede empezar a realizar solicitudes al servicio de programa de fondo móvil.

### Antes de empezar
{: #testing_auth_before}

Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Para obtener más información, consulte [Protección de recursos](protecting-resources.html).

1. Intente enviar una solicitud al punto final protegido de la aplicación de programa de fondo móvil desde su navegador. Abra el siguiente URL: `{rutaAplicación}/protected`. Por ejemplo: `http://my-mobile-backend.mybluemix.net/protected`.

	El valor del punto final `/protected` de cualquier punto final protegido de un servicio de programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` en el navegador. Este mensaje se devuelve porque solo se puede acceder a este punto final con aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de Cordova para realizar solicitudes al mismo punto final. Añada el código siguiente después de inicializar `BMSClient`:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new BMSRequest("<applicationRoute}/protected>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

1. Ejecute la aplicación. Aparece una pantalla de inicio de sesión de Facebook:

	![imagen](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![imagen](images/ios-facebook-login.png)

	Esta pantalla puede ser ligeramente diferente si no tiene instalada la app de Facebook en su dispositivo, o bien si no ha iniciado sesión en Facebook.

1. Pulse **Aceptar** para autorizar que {{site.data.keyword.amashort}} utilice su identidad de usuario de Facebook para fines de autenticación.

1. 	Cuando la solicitud se realiza correctamente, se muestra la salida siguiente en la consola de Xcode o del programa de utilidad LogCat:

	![Mensaje de realización de la autenticación de Facebook para Android](images/android-facebook-login-success.png)

	![Mensaje de realización de la autenticación de Facebook para iOS](images/ios-facebook-login-success.png)
