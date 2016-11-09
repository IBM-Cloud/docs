---

copyright:
 years: 2015, 2016

---

# Habilitación de aplicaciones Cordova para recibir notificaciones push
{: #cordova_enable}
Última actualización: 17 de octubre de 2016
{: .last-updated}

Cordova es una plataforma para crear aplicaciones híbridas con JavaScript, CSS y HTML. {{site.data.keyword.mobilepushshort}} soporta el desarrollo de aplicaciones para iOS y Android basadas en Cordova.

Puede habilitar las aplicaciones de Cordova para recibir notificaciones push en sus dispositivos.

## Instalación del plug-in push de Cordova
{: #cordova_install}

Instale y utilice el plug-in push del cliente para seguir desarrollando sus aplicaciones Cordova. Esto también instala el plug-in Core de Cordova, que inicializa la conexión a Bluemix.

### Antes de empezar

1. Descargue las versiones más recientes de Android Studio SDK y Xcode.
1. Configure el emulador. Para Android Studio, utilice un emulador que dé soporte a la API de Google Play.
1. Instale la herramienta de línea de mandatos de Git. Para Windows, asegúrese de que selecciona la opción **Ejecutar Git desde la ventana del indicador de mandatos**. Para obtener información sobre cómo descargar e instalar esta herramienta, consulte [Git](https://git-scm.com/downloads).
1. Instale la herramienta Node.js y NPM (Node Package Manager). La herramienta de línea de mandatos NPM está empaquetada con Node.js. Para obtener información sobre cómo descargar e instalar Node.js, consulte [Node.js](https://nodejs.org/en/download/).
1. Desde la línea de mandatos, instale las herramientas de línea de mandatos de Cordova mediante el mandato **npm install -g cordova**. Esto es necesario para utilizar el plug-in push de Cordova. Para obtener información sobre cómo instalar Cordova y configurar la aplicación de Cordova, consulte [Cordova Apache](https://cordova.apache.org/#getstarted). Para más información, consulte el [Archivo readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push) del plug-in push de Cordova.
1. Vaya a la carpeta en la que desea crear la aplicación de Cordova y ejecute el mandato siguiente para crear una aplicación de Cordova. Si ya tiene una aplicación de Cordova, vaya al paso 3.
```
cordova create your_app_name
	cd your_app_name
```
	{: codeblock}
- Opcional: Puede editar el archivo **config.xml** y cambiar el nombre de la aplicación en el elemento <name> a uno de su elección, en lugar del nombre HelloCordova predeterminado.

Asegúrese de que especifica el ID de paquete correcto. Los siguientes mensajes de error se pueden dar en Xcode, si se especifica un ID de paquete incorrecto.

* El ejecutable se ha firmado con titularidades no válidas.
* Las titularidades especificadas en el archivo Titularidades de firmado de código de la aplicación no coinciden con las especificadas en el perfil de suministro. Para solucionar este problema, especifique el ID de paquete correcto en Xcode o en el archivo **config.xml** de la aplicación de Cordova.

1. Añada la API soportada mínima o la declaración de destino del despliegue al archivo config.xml para la aplicación de Cordova. El valor de minSdkVersion debe ser superior a 15. El valor targetSdkVersion siempre debe reflejar el SDK de Android más reciente disponible desde Google.
	
	* Android: Con el editor, abra el archivo config.xml y actualice el elemento
`<platform name="android">` con versiones SDK de destino y mínimas:

```
< !-- add deployment target declaration --> 
add deployment target declaration <preference name="android-minSdkVersion" value="15" />
  <preference name="android-targetSdkVersion" value="23" />
</platform>
```
    {: codeblock}

   * iOS: Actualice el elemento <platform name="ios"> con una declaración de destino de despliegue:

```
<platform name ="ios">
<preference name=deployment-target" value="8.0" /> <!-- other properties -->
</ platform>
```
	{: codeblock}

1. Desde la interfaz de línea de mandatos (CLI) de Cordova, añada las plataformas iOS, Android o ambas utilizando el siguiente mandato:
```
cordova platform add ios
	cordova platform add android
```
	{: codeblock}

1. Desde el directorio raíz de la aplicación de Cordova, especifique el mandato siguiente para instalar el plug-in push de Cordova: **cordova plugin add ibm-mfp-push**. En función de las plataformas añadidas, podría ver:
```
Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
```
	{: codeblock}

1. Desde *your-app-root-folder*, verifique que los plug-ins Core y Push de Cordova se hayan instalado correctamente; para ello, utilice el mandato **cordova plugin list**. En función de las plataformas añadidas, podría ver:
```
ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
```
	{: codeblock}

1. (Solo iOS): Configure su entorno de desarrollo de iOS.
2. Complete los subpasos siguientes:

 a. Abra el archivo your-app-name.xcodeproj en el directorio *your-app-name***/platforms/ios** con Xcode.

 b. Añada la cabecera de puente. Vaya a **Crear configuración > Compilador de Swift - Generación de códigos > Cabecera puente de Objective-C** y añada la vía de acceso siguiente: *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

 c. Añada el parámetro Frameworks. Vaya a **Crear configuración > Enlaces > Vías de acceso de búsqueda de vías de acceso de ejecución** y añada el parámetro `@executable_path/Frameworks`.

 d. Elimine la marca de comentario de las siguientes sentencias de importación de Push en la cabecera de enlace por puente. Vaya a *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

```
//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
```
	{: codeblock}

 e. Cree y ejecute la aplicación con Xcode.

1. (Solo Android): Cree su proyecto de Android utilizando el mandato siguiente:
**cordova build android**.

	**Nota**: Antes de abrir el proyecto en Android Studio, cree la aplicación de Cordova mediante la CLI de Cordova. De esta forma no se producirán errores de compilación.


## Inicialización del plug-in de Cordova
{: #cordova_initialize}

Para poder utilizar el plug-in de Cordova del servicio {{site.data.keyword.mobilepushshort}}, debe inicializarlo
pasando la ruta de la aplicación y el GUID de aplicaciones. Tras inicializar el plug-in, puede conectarse a la aplicación del servidor que ha creado en el panel de control de Bluemix. El plug-in de Cordova es el continente para los
SDK de cliente de iOS y Android para habilitar a una aplicación de Cordova a comunicarse con los servicios de Bluemix.

1. Inicialice el BMSClient copiando y pegando el siguiente fragmento de código en el archivo JavaScript principal (normalmente ubicado en el directorio **www/js**).

```
BMSClient.initialize("https://myapp.mybluemix.net","App GUID");
```
	{: codeblock}

1. Modifique el fragmento de código para que utilice los parámetros Ruta y appGUID de Bluemix. Pulse el enlace **Opciones móviles** en el panel de control push para obtener la ruta y el GUID de la app y el secreto de cliente. Utilice los valores de Ruta y GUID de la app como parámetros en el fragmento de código `BMSClient.initialize`.

	**Nota**: Si ha creado una app de Cordova utilizando la CLI de Cordova, por ejemplo, el mandato Cordova create app-name, coloque este código Javascript en el archivo **index.js**, después de que la función `app.receivedEvent` dentro de la función `onDeviceReady: function()` inicialice el cliente BMS.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("https://myapp.mybluemix.net","App GUID");
    },
```
	{: codeblock}

## Registro de dispositivos
{: #cordova_register}


Para registrar un dispositivo con el servicio {{site.data.keyword.mobilepushshort}}, llame el método de registro. Copie el siguiente fragmento de código en la aplicación de Cordova para registrar un dispositivo.

```
var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```
	{: codeblock}

### Android
{: #cordova_register_android}
Android no utiliza el parámetro settings. Si solo está creando una aplicación Android, pase un objeto vacío. Por ejemplo:

```
MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```
	{: codeblock}

### iOS
{: #cordova_register_ios}
Para personalizar la alerta, el identificador y las propiedades de sonido, añada el siguiente fragmento de código de JavaScript a la parte web de la aplicación de Cordova.

```
var settings = {
   ios: {
      alert: true,
	       badge: true,
	       sound: true
	   }
}
	MFPPush.registerDevice(settings, success, failure);
```
	{: codeblock}


### JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```
	{: codeblock}

Puede acceder al contenido del parámetro de respuesta de éxito en Javascript utilizando JSON.parse:
**var token = JSON.parse(response).token**


Las claves disponibles son: `token` y `deviceId`.

En el siguiente fragmento de código JavaScript se muestra cómo inicializar el SDK del cliente de Bluemix Mobile Services, cómo registrar un dispositivo con el servicio {{site.data.keyword.mobilepushshort}} y cómo escuchar las notificaciones push. Incluya este código en el archivo Javascript.

```
//Register device token with Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```
	{: codeblock}

```
//Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```
	{: codeblock}
dentro de la **onDeviceReady: function()**.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
     BMSClient.initialize("https://http://myroute_mybluemix.net","my_appGuid");
     var success = function(message) { console.log("Success: " + message); };
     var failure = function(message) { console.log("Error: " + message); };
     var settings = {
     ios: {
         alert: true,
	       badge: true,
	       sound: true
	   }
  };
   MFPPush.registerDevice(settings, success, failure);
   var notification = function(notif){
       alert (notif.message);
    };
    MFPPush.registerNotificationsCallback(notification);
	 }
```
	{: codeblock}

### Objective-C
{: #cordova_register_objective}
Añada el siguiente fragmento de código Objective-C a la clase de delegado de la aplicación

```
// Registre la señal del dispositivo con Bluemix Push Notification Service
	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
// Manejar el error cuando no ha podido registrar la señal del dispositivo con APN
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```
	{: codeblock}

###Swift
{: #cordova_register_swift}
Añada el siguiente fragmento de código de Swift a la clase de delegado de la aplicación.

```
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
//Manejar el error cuando no se pueda registrar la señal del dispositivo con APN
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```
	{: codeblock}

##Pasos siguientes

{: #cordova_register_next}

Cree el proyecto y, a continuación, ejecute el proyecto utilizando los mandatos siguientes:

####Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

####iOS
{: ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

## Recepción de notificaciones push en dispositivos
{: #cordova_receive}

Copie el siguiente fragmento de código para recibir notificaciones push en los dispositivos.

###JavaScript

Añada el siguiente fragmento de código JavaScript a la parte web de la aplicación de Cordova.
```
var notification = function(notification){
    // la notificación es un objeto JSON.
alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```
	{: codeblock}

###Propiedades de notificación de Android

En la sección siguiente se listan las propiedades de notificación de Android:

* message - mensaje de notificación de Push
* payload - objeto JSON que contiene una carga útil de notificación


###Propiedades de notificación de iOS

En la sección siguiente se listan las propiedades de notificación de iOS:

* message - mensaje de notificación de Push
* payload - objeto JSON que contiene una carga útil de notificación
action-loc-key - la serie se utiliza como clave para obtener una serie localizada en la localización actual para que la utilice el título del botón adecuado, en lugar de `Vista`.
* badge - El número que se mostrará como el identificador del icono de app. Si falta esta propiedad, el identificador no se modificará. Para eliminar el identificador, establezca el valor de esta propiedad en 0.
* sound - El nombre de un archivo de sonido del paquete de la app de la carpeta Biblioteca/Sonidos del contenedor de datos de la aplicación.

###Objective-C

Añada los siguientes fragmentos de código de Objective-C en la clase de delegado de la aplicación.

```
// Maneje la recepción de una notificación remota
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {
 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```
	{: codeblock}


```
// Maneje la recepción de una notificación remota al iniciar
		- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
	}
```
	{: codeblock}

###Swift

Añada los siguientes fragmentos de código de Swift a la clase de delegado de la aplicación.
```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){
  CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
	}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
	}
```
	{: codeblock}

## Envío de notificaciones push básicas
{: #push-send-notifications}

Una vez que haya desarrollado sus aplicaciones, puede enviar notificaciones push básicas.

Para ello, realice estos pasos:

1. Seleccione **Enviar notificaciones** y para redactar un mensaje seleccione la opción **Enviar a**. Las opciones admitidas son **Dispositivo por etiqueta**, **ID de dispositivo**, **ID de usuario**, **Dispositivos Android**, **Dispositivos iOS**, **Notificaciones web** y **Todos los dispositivos**.
**Nota**: Cuando seleccione la opción **Todos los dispositivos**, todos los dispositivos suscritos a {{site.data.keyword.mobilepushshort}} recibirán notificaciones.
![pantalla Notificaciones](images/tag_notification.jpg)

2. En el campo **Mensaje**, redacte el mensaje. Elija configurar los valores opcionales según sea necesario.
3. Pulse **Enviar**.
3. Verifique que los dispositivos hayan recibido la notificación.

En la captura de pantalla siguiente se muestra un recuadro de alerta en el que se maneja una {{site.data.keyword.mobilepushshort}}
en el primer plano en un dispositivo Android e iOS.

![Notificación push en primer plano en Android](images/Android_Screenshot.jpg)

![Notificación push en primer plano en iOS](images/iOS_Screenshot.jpg)

   En la siguiente imagen se muestra una {{site.data.keyword.mobilepushshort}} en segundo plano para Android.
![Notificación push en el fondo en Android](images/background.jpg)

## Pasos siguientes
{: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede configurar las notificaciones basadas en código y las opciones avanzadas.

Añada las características del servicio {{site.data.keyword.mobilepushshort}} a la aplicación.
Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html).
Para utilizar opciones de notificaciones avanzadas, consulte [Habilitación de notificaciones push avanzadas](t_advance_badge_sound_payload.html).
