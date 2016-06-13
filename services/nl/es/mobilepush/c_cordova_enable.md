---

copyright:
 years: 2015, 2016

---

# Habilitación de aplicaciones Cordova para recibir notificaciones push
{: #cordova_enable}

Cordova es una plataforma para crear aplicaciones híbridas con JavaScript, CSS y HTML. {{site.data.keyword.mobilepushshort}} soporta el desarrollo de aplicaciones para iOS y Android basadas en Cordova.

Habilite las aplicaciones Cordova para recibir notificaciones push y enviar notificaciones push a
     sus dispositivos.




## Instalación del plug-in Push de Cordova
{: #cordova_install}

Instale y utilice el plug-in Push del cliente para seguir desarrollando sus aplicaciones Cordova. Esto también instala el plug-in Core de Cordova, que inicializa
          la conexión a Bluemix.

### Antes de empezar

1. Descargue las versiones más recientes de Android Studio SDK y Xcode.
1. Configure el emulador. Para Android Studio, utilice un emulador que dé soporte a la API de Google Play.
1. Instale la herramienta de línea de mandatos de Git. Para Windows, asegúrese de que selecciona la opción **Ejecutar Git desde la ventana del indicador de mandatos**. Para obtener información sobre cómo descargar e instalar esta herramienta, consulte [Git](https://git-scm.com/downloads).

1. Instale la herramienta Node.js y NPM (Node Package Manager). La herramienta de línea de mandatos NPM está empaquetada con Node.js. Para obtener información sobre cómo descargar e instalar Node.js, consulte [Node.js](https://nodejs.org/en/download/).
1. Desde la línea de mandatos, instale las herramientas de línea de mandatos de Cordova mediante el mandato **npm install -g cordova**. Esto es necesario para utilizar el plug-in Push de Cordova. Para obtener información sobre cómo instalar Cordova y configurar la aplicación de Cordova, consulte [Cordova Apache](https://cordova.apache.org/#getstarted).

 **Nota**: Para ver el archivo readme del plug-in Push de Cordova, vaya a [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)

1. Vaya a la carpeta en la que desea crear la aplicación de Cordova y ejecute el mandato siguiente para crear una aplicación de Cordova. Si ya tiene una aplicación de Cordova, vaya al paso 3.

 ```
cordova create your_app_name
	cd your_app_name
```
1. Opcional: (Opcional) Edite el archivo **config.xml** y cambie el nombre de la aplicación en el elemento <name> a uno de su elección, en lugar del nombre HelloCordova predeterminado.

	**Nota**: Asegúrese de que especifica el ID de paquete correcto. Si no lo hace, se visualizarán los siguientes mensajes de error en Xcode.
	* El ejecutable se ha firmado con titularidades no válidas.
	* Las titularidades especificadas en el archivo Titularidades de firmado de código de la aplicación no coinciden con las especificadas en el perfil de suministro.

	Para solucionar este problema, especifique el ID de paquete correcto en Xcode o en el archivo **config.xml** de la aplicación de Cordova.

1. Añada la API soportada mínima o la declaración de destino del despliegue al archivo config.xml para la aplicación de Cordova. El valor de minSdkVersion debe ser superior a 15. El valor targetSdkVersion siempre debe reflejar el SDK de Android más reciente disponible desde Google.
	* **Android**: Con el editor, abra el archivo config.xml y actualice el
   elemento ```<platform name="android">``` con las versiones SDK de destino y mínimas:

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS**: Actualice el elemento <platform name="ios"> con una declaración de destino de despliegue:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Desde la interfaz de línea de mandatos (CLI) de Cordova, añada las plataformas iOS, Android, o ambas utilizando los mandatos siguientes:

	```
	cordova platform add ios@3.9.0
	cordova platform add android
	```
1. Desde el directorio raíz de la aplicación de Cordova, especifique el mandato siguiente para instalar el plug-in Push de Cordova: **cordova plugin add ibm-mfp-push**.

	En función de las plataformas añadidas, verá algo similar a lo siguiente:

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. Desde *your-app-root-folder*, verifique que los plug-ins Core y Push de Cordova se hayan instalado correctamente, mediante el siguiente mandato: **cordova plugin list**.

	En función de las plataformas añadidas, verá algo similar a lo siguiente:

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (Solo iOS): Configure su entorno de desarrollo de iOS.
	a. Abra el archivo your-app-name.xcodeproj en el directorio *your-app-name***/platforms/ios** con Xcode.

	b. Añada la cabecera de puente. Vaya a **Crear configuración > Compilador de Swift - Generación de códigos > Cabecera puente de Objective-C** y añada la vía de acceso siguiente: *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. Añada el parámetro Frameworks. Vaya a **Crear configuración > Enlaces > Runpath Search Paths** y añada el parámetro siguiente:
	```
	@executable_path/Frameworks
	```
	d. Elimine la marca de comentario de las siguientes sentencias de importación de Push en la cabecera de enlace por puente. Vaya a *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Cree y ejecute la aplicación con Xcode.
1. (Solo Android): Cree su proyecto de Android utilizando el mandato siguiente:
**cordova build android**.

	**Nota**: Antes de abrir el proyecto en Android Studio, primero debe crear la aplicación de Cordova mediante la CLI de Cordova. De lo contrario, se encontrará con errores de creación.


## Inicialización del plug-in de Cordova
{: #cordova_initialize}

Para poder utilizar el plug-in de Cordova del Servicio de notificaciones Push, debe inicializarlo
pasando la ruta de la aplicación y el GUID de aplicaciones. Tras inicializar el plug-in, puede conectarse a la aplicación del servidor que ha creado en el panel de control de Bluemix. El plug-in de Cordova es el continente para los
SDK de cliente de iOS y Android para habilitar a una aplicación de Cordova a comunicarse con los servicios de Bluemix.

1. Inicialice el BMSClient copiando y pegando el siguiente fragmento de código en el archivo JavaScript principal (normalmente ubicado en el directorio **www/js**).

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. Modifique el fragmento de código para que utilice los parámetros Ruta y appGUID de Bluemix. Pulse el enlace **Opciones móviles** en el Panel de control de aplicaciones de Bluemix para obtener la ruta de la aplicación y la GUID de la app. Utilice los valores de Ruta y GUID de la app como parámetros en el fragmento de código ```BMSClient.initialize```.

	**Nota**: Si ha creado una app de Cordova utilizando el CLI de Cordova, por ejemplo, el mandato Cordova create app-name, coloque este código Javascript en el archivo **index.js**, después de que la función ```app.receivedEvent``` dentro de la función o```nDeviceReady: function()`` inicialice el cliente BMS.

```
onDeviceReady: function() {
    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
```

## Registro de dispositivos
{: #cordova_register}

Para registrar un dispositivo con el Servicio de notificaciones Push, invoque el método de registro.

Copie y pegue el siguiente fragmento de código en la aplicación de Cordova para
                    registrar un dispositivo.

```
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	MFPPush.registerDevice({}, success, failure);
```

### Android
{: #cordova_register_android}
Android no utiliza el parámetro settings. Si solo está creando una aplicación Android, pase un objeto vacío; por ejemplo:

```
	MFPPush.registerDevice({}, success, failure);
	MFPPush.unregisterDevice(success, failure);
```

### iOS
{: #cordova_register_ios}
Si desea personalizar la alerta, el identificador y las propiedades de
                    sonido, añada el siguiente fragmento de código de JavaScript a la parte web de la
                    aplicación de Cordova.

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



### JavaScript
{: #cordova_register_js}

```
MFPPush.registerDevice({}, success, failure);
```

Puede acceder al contenido del parámetro de respuesta de éxito en Javascript utilizando JSON.parse:
**var token = JSON.parse(response).token**


Las claves disponibles son las siguientes: ```token```, ```userId`` y ```deviceId``.

El siguiente fragmento de código JavaScript muestra cómo inicializar el SDK del cliente de Bluemix Mobile Services, cómo registrar un dispositivo con el servicio de notificaciones Push y cómo escuchar las notificaciones push. Coloque este código en el archivo Javascript.



```
//Register device token with Bluemix Push Notification Service
funcapplication(application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
  CDVMFPPush.sharedInstance().didRegisterForRemoteNotifications(deviceToken)
}
```

```
//Handle error when failed to register device token with APNs
funcapplication(application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer){
CDVMFPPush.sharedInstance().didFailToRegisterForRemoteNotifications(error)
}
```

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

### Objective-C
{: #cordova_register_objective}
Añada el siguiente fragmento de código Objective-C a la clase de delegado de la aplicación

```
	// Register the device token with Bluemix Push Notification Service
	- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
	  [[CDVMFPPush sharedInstance] didRegisterForRemoteNotifications:deviceToken];
	}
	// Handle error when failed to register device token with APNs
	- (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error {
	   [[CDVMFPPush sharedInstance] didFailToRegisterForRemoteNotificationsWithError:error];
	}
```

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

##Siguientes pasos

{: #cordova_register_next}

Cree el proyecto y, a continuación, ejecute el proyecto utilizando los mandatos siguientes:

	* Android: **cordova build android** y, a continuación, **cordova run android**

	* iOS: **cordova build ios** y, a continuación, **cordova run ios**



## Recepción de notificaciones push en dispositivos
{: #cordova_receive}

Copie y pegue los siguientes fragmentos de código para recibir notificaciones push en
                    dispositivos.

###JavaScript

Añada el siguiente fragmento de código JavaScript a la parte web de la aplicación de
                        Cordova.


```
var notification = function(notification){
    // notification es un objeto JSON.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

###Propiedades de notificación de Android

En la sección siguiente se listan las propiedades de notificación de Android:

* message - mensaje de notificación de Push
* payload - objeto JSON que contiene una carga útil de notificación


###Propiedades de notificación de iOS

En la sección siguiente se listan las propiedades de notificación de iOS:

* message - mensaje de notificación de Push
* payload - objeto de JSON que contiene una action-loc-key de carga útil de notificación - La serie se utiliza como una clave para obtener una serie localizada en la localización actual para que la utilice el título del botón derecho en lugar de “Vista".
* badge - El número que se mostrará como el identificador del icono de app. Si falta esta propiedad, el
                            identificador no se modificará. Para eliminar el identificador, establezca el valor de esta
                            propiedad en 0.
* sound - El nombre de un archivo de sonido del paquete de la app de la carpeta
                            Biblioteca/Sonidos del contenedor de datos de la aplicación.

###Objective-C

Añada los siguientes fragmentos de código de Objective-C en la clase de delegado de la aplicación.

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

###Swift

Añada los siguientes fragmentos de código de Swift a la clase de delegado de la aplicación.

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```


{: #push-send-notifications}
## Envío de notificaciones push básicas


Una vez que haya desarrollado sus aplicaciones, puede enviar notificaciones push básicas (sin
  utilizar etiquetas, identificadores, cargas útiles adicionales o archivos de sonido).


Enviar notificaciones push básicas.

1. En **Elegir la audiencia**, seleccione una de las siguientes audiencias:
      **Todos los dispositivos**, o por plataforma: **Sólo dispositivos iOS** o
      **Sólo dispositivos Android**. 

	**Nota**: Cuando seleccione la opción **Todos los dispositivos**, todos los dispositivos que se han suscrito a las notificaciones push recibirán la notificación.

	![pantalla Notificaciones](images/tag_notification.jpg)

2. En **Crear la notificación**, especifique el mensaje y, a continuación, pulse **Enviar**.
3. Verifique que los dispositivos hayan recibido la notificación.

	La captura de pantalla siguiente muestra un recuadro de alerta que maneja una notificación push
en el primer plano en un dispositivo Android e iOS.

	![Notificación push en primer plano en Android](images/Android_Screenshot.jpg)

	![Notificación push en primer plano en iOS](images/iOS_Screenshot.jpg)

	La captura de pantalla siguiente muestra una notificación push en segundo plano para Android.
	![Notificación push en el fondo en Android](images/background.jpg)



## Siguientes pasos
{: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede configurar
        las notificaciones basadas en código y las opciones avanzadas.

Añada estas características de Servicio de notificaciones push a la aplicación.
Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html).
Para utilizar opciones de notificaciones avanzadas, consulte [Notificaciones push avanzadas](t_advance_notifications.html).
