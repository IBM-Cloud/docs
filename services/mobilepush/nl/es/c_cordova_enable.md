---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Habilitación de aplicaciones Cordova para recibir notificaciones push
{: #cordova_enable}
Última actualización: 18 de enero de 2017
{: .last-updated}

Cordova es una plataforma para crear aplicaciones híbridas con JavaScript, CSS y HTML. El servicio de {{site.data.keyword.mobilepushshort}} da soporte al desarrollo de aplicaciones para iOS y Android basadas en Cordova.

Puede habilitar las aplicaciones de Cordova para recibir notificaciones push en sus dispositivos.

## Instalación del plug-in push de Cordova
{: #cordova_install}

Instale y utilice el plug-in push del cliente para seguir desarrollando sus aplicaciones Cordova. Esto también instala el plug-in Core de Cordova, que inicializa la conexión a Bluemix.

### Antes de empezar

1. Descargue las versiones más recientes de Android Studio SDK y Xcode.
1. Configure el emulador. Para Android Studio, utilice un emulador que dé soporte a la API de Google Play.
1. Instale la herramienta de línea de mandatos de Git. Para Windows, asegúrese de que selecciona la opción **Ejecutar Git desde la ventana del indicador de mandatos**. Para obtener información sobre cómo descargar e instalar esta herramienta, consulte [Git ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://git-scm.com/downloads){: new_window}.
1. Instale la herramienta Node.js y NPM (Node Package Manager). La herramienta de línea de mandatos NPM está empaquetada con Node.js. Para obtener información sobre cómo descargar e instalar Node.js, consulte [Node.js ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://nodejs.org/en/download/){: new_window}.
1. Desde la línea de mandatos, instale las herramientas de línea de mandatos de Cordova mediante el mandato **npm install -g cordova**. Esto es necesario para utilizar el plug-in push de Cordova. Para obtener información sobre cómo instalar Cordova y configurar la app de Cordova, consulte [Cordova Apache ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://cordova.apache.org/#getstarted){: new_window}. Para obtener más información, consulte [archivo Readme ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window} del plug-in de push de Cordova.
1. Vaya a la carpeta en la que desea crear la aplicación de Cordova y ejecute el mandato siguiente para crear una aplicación de Cordova. Si ya tiene una aplicación de Cordova, vaya al paso 3.
```cordova create your_app_name
cd your_app_name
```
	{: codeblock}
- Opcional: Puede editar el archivo **config.xml** y cambiar el nombre de la aplicación en el elemento <name> a uno de su elección, en lugar del nombre HelloCordova predeterminado.

Asegúrese de que especifica el ID de paquete correcto. Los siguientes mensajes de error se pueden dar en Xcode, si se especifica un ID de paquete incorrecto.

* El ejecutable se ha firmado con titularidades no válidas.
* Las titularidades especificadas en el archivo Titularidades de firmado de código de la aplicación no coinciden con las especificadas en el perfil de suministro. Para solucionar este problema, especifique el ID de paquete correcto en Xcode o en el archivo **config.xml** de la aplicación de Cordova.

1. Añada la API soportada mínima o la declaración de destino del despliegue al archivo config.xml para la aplicación de Cordova. El valor de minSdkVersion debe ser superior a 15. El valor targetSdkVersion siempre debe reflejar el SDK de Android más reciente disponible desde Google.
	
	* Android: Con el editor, abra el archivo **config.xml** y actualice el elemento
`<platform name="android">` con versiones SDK de destino y mínimas:

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS: Actualice el elemento <platform name="ios"> con una declaración de destino de despliegue:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. Desde la interfaz de línea de mandatos (CLI) de Cordova, añada las plataformas iOS, Android o ambas utilizando el siguiente mandato:
```
cordova platform add ios
	cordova platform add android
```
	{: codeblock}

1. Desde el directorio raíz de la aplicación de Cordova, especifique el mandato siguiente para instalar el plug-in push de Cordova: **cordova plugin add bms-push**. En función de las plataformas añadidas, podría ver:
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. Desde your-app-root-folder, verifique que los plug-ins Core y Push de Cordova se hayan instalado correctamente; para ello, utilice el mandato **cordova plugin list**. En función de las plataformas añadidas, podría ver:
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. Configure su entorno de desarrollo de iOS.
2. Cree y ejecute la aplicación con Xcode.
1. Descargue `google-services.json` de Firebase para android y colóquelos en la carpeta raíz del proyecto Cordova, en `[your-app-name]/platforms/android.
	1. Vaya a `[your-app-name]/platforms/android`.
	2. Abra el archivo `build.gradle` (Vía de acceso : plataforma > android > build.gradle).
	3. Busque el texto `buildscript` en el archivo `build.gradle`.
	4. Después de la línea classpath, añada la línea classpath 'com.google.gms:google-services:3.0.0'
	5. Busque "dependencies". Seleccione las dependencias que contengan el texto `compile` y el fin de dichas dependencias; después de las mismas, añada esta línea:apply plugin: 'com.google.gms.google-services'.
	6. Prepare y compile el proyecto Cordova Android.
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**Nota**: Antes de abrir el proyecto en Android Studio, cree la aplicación de Cordova mediante la CLI de Cordova. De esta forma no se producirán errores de compilación.

## Inicialización del plug-in de Cordova
{: #cordova_initialize}

Para poder utilizar el plug-in de Cordova del servicio {{site.data.keyword.mobilepushshort}}, debe inicializarlo
pasando la ruta de la aplicación y el GUID de aplicaciones. Tras inicializar el plug-in, puede conectarse a la aplicación del servidor que ha creado en el panel de control de Bluemix. El plug-in de Cordova es el continente para los
SDK de cliente de iOS y Android para habilitar a una aplicación de Cordova a comunicarse con los servicios de Bluemix.

1. Inicialice el BMSClient copiando y pegando el siguiente fragmento de código en el archivo JavaScript principal (normalmente ubicado en el directorio **www/js**).

```
onDeviceReady: function() {
	app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

Pase la región para la aplicación. Se proporcionan las siguientes constantes:

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

Por ejemplo:

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**Nota**: Si ha creado una app de Cordova utilizando la CLI de Cordova, por ejemplo, el mandato Cordova create app-name, coloque este código Javascript en el archivo index.js, después de que la función app.receivedEvent dentro de la función onDeviceReady: function() inicialice el `BMSClient`. 


## Registro de dispositivos
{: #cordova_register}


Para registrar un dispositivo con el servicio {{site.data.keyword.mobilepushshort}}, llame el método de registro. Copie el siguiente fragmento de código en la aplicación de Cordova para registrar un dispositivo.

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

En el siguiente fragmento de código JavaScript se muestra cómo inicializar el SDK del cliente de Bluemix Mobile Services, cómo registrar un dispositivo con el servicio {{site.data.keyword.mobilepushshort}} y cómo escuchar las notificaciones push. Incluya este código en el archivo Javascript.

Dentro de la **onDeviceReady: function()**.

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure); 
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

Añada el siguiente fragmento de código de Swift a la clase de delegado de la aplicación.

```
// Registre la señal del dispositivo con Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Maneje el error cuando no haya podido registrar la señal del dispositivo con APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

## Pasos siguientes

{: #cordova_register_next}

Cree el proyecto y, a continuación, ejecute el proyecto utilizando los mandatos siguientes:

#### Android
{: android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
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

### JavaScript

Añada el siguiente fragmento de código JavaScript a la parte web de la aplicación de Cordova.
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

### Propiedades de notificación de Android

En la sección siguiente se listan las propiedades de notificación de Android:

* **message** - mensaje de notificación de Push
* **payload** - objeto JSON que contiene una carga útil de notificación


### Propiedades de notificación de iOS

En la sección siguiente se listan las propiedades de notificación de iOS:

* **message** - mensaje de notificación de Push
* **payload** - objeto JSON que contiene una carga útil de notificación
action-loc-key - la serie se utiliza como clave para obtener una serie localizada en la localización actual para que la utilice el título del botón adecuado, en lugar de `Vista`.
* **badge** - El número que se mostrará como el identificador del icono de app. Si falta esta propiedad, el identificador no se modificará. Para eliminar el identificador, establezca el valor de esta propiedad en 0.
* **sound** - El nombre de un archivo de sonido del paquete de la app de la carpeta Biblioteca/Sonidos del contenedor de datos de la aplicación.


Añada los siguientes fragmentos de código de Swift a la clase de delegado de la aplicación.
```
// Maneje la recepción de una notificación remota
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Maneje la recepción de una notificación remota al iniciar
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
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

Añada las características de servicio de {{site.data.keyword.mobilepushshort}} a la app. Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html).
Para utilizar opciones de notificaciones avanzadas, consulte [Habilitación de notificaciones push avanzadas](t_advance_badge_sound_payload.html).
