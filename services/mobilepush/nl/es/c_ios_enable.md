---

copyright:
 years: 2015, 2016

---

# Habilitación de aplicaciones iOS para recibir notificaciones push
{: #enable-push-ios-notifications}
Última actualización: 16 de agosto de 2016
{: .last-updated}

Puede habilitar aplicaciones iOS para recibir y enviar notificaciones push a sus dispositivos.


##Instalación de CocoaPods
{: #enable-push-ios-notifications-install}

Para un proyecto Xcode existente, puede configurar el SDK del cliente de Bluemix Mobile Services mediante la herramienta de gestión de dependencias de CocoaPods. Una alternativa es instalar el SDK manualmente.

**Nota**: Para ver el archivo readme push de Swift, vaya a https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master.



1. Instale CocoaPods utilizando el siguiente mandato en su terminal Mac.
```
$ sudo gem install cocoapods
```
2. Especifique el mandato siguiente en el terminal para inicializar CocoaPods. Asegúrese de ejecutar el mandato desde el directorio en el que se encuentra el proyecto Xcode. El mandato `pod init` creará un título de archivo.  
```
$ pod init
```
3. En el Podfile generado, añada las dependencias de SDK necesarias. Copie cualquiera de los siguientes Podfile, según sus preferencias.

###Objective-C
   {: objc-sdkdependencies}

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

####Swift
   {: swift-sdkdependencies}

	```
	source 'https://github.com/CocoaPods/Specs.git'
	# Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
3. Desde el terminal, vaya a la carpeta del proyecto e instale las dependencias con el mandato siguiente:

```
$ pod update
```
Este mandato instala las dependencias y crea un nuevo espacio de trabajo Xcode.  **Nota**: Asegúrese de abrir siempre el nuevo espacio de trabajo de Xcode, en lugar del archivo de proyecto Xcode original:

	```
	$ open App.xcworkspace
	```
El espacio de trabajo contiene el proyecto original y el proyecto Pods que contiene las dependencias. Si desea modificar una carpeta fuente de Bluemix Mobile Services, puede encontrarla en el proyecto Pods, en `Pods/yourImportedSourceFolder`, por ejemplo: `Pods/IMFGoogleAuthentication`.

##Carthage
{: #carthage}

Añada infraestructuras al proyecto utilizando [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos). (https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos%29.)

1. Añada infraestructuras `BMSPush` a Cartfile:
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
2. Ejecute el mandato `carthage update`. Cuando la compilación finalice, arrastre `BMSPush.framework`, `BMSCore.framework` y `BMSAnalyticsAPI.framework` al proyecto Xcode.
3. Siga las instrucciones del sitio [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) para completar la integración.

##Utilización de infraestructuras importadas y carpetas fuente
{: using-imported-frameworks}

Haga referencia al SDK del código.


####Objective-C
{: objc-import-directives}

Escriba directivas #import para las cabeceras relevantes, por
ejemplo:

```
 //Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Nota**: La actualización del proyecto Pods utilizando los mandatos CocoaPods `pod install` o `pod update` puede alterar temporalmente las carpetas fuente de Bluemix Mobile Services. Si desea conservar las versiones personalizadas
de los archivos originales, asegúrese de que se les ha hecho la copia de seguridad antes de emitir uno de estos
mandatos.

####Swift
{: swift-import-directives}

####Requisitos previos
{: prerequisites}

- iOS 8.0 o superior
- Xcode 7


Escriba directivas #import para las cabeceras relevantes, por
ejemplo:

```
//swift
import BMSCore
import BMSPush
```
**Atención**: para ver el archivo readme Push de Swift, vaya a [Readme](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master)

##Crear configuración
{: build-settings}

Vaya a **Xcode > Crear configuración > Opciones de creación y Establecer la habilitación de Bitcode** en **No**.

**Atención**: A partir de iOS 9, los cambios a la característica de App Transport Security (ATS) pueden afectar a la forma de manejar el proceso de autenticación. Las siguientes publicaciones de blog describen más información sobre los cambios:[ATS y Bitcode en iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) y [Conecte la app de iOS 9 a Bluemix ahora mismo](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)




## Inicialización de SDK Push para aplicaciones iOS
{: #enable-push-ios-notifications-initialize}

Un lugar común para colocar el código de inicialización se encuentra en el delegado de aplicación para la aplicación
     iOS. Pulse el enlace **Opciones móviles** en el panel de control Push para obtener la ruta y el GUID de la aplicación.

###Inicialización del SDK principal
{: Initializing-the-core-sdk}

####Objective-C
{: objc-initialize-core-sdk}

```
// Inicialice el SDK for Object-C con la GUID y la ruta de IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

####Swift
{: swift-initialize-core-sdk}

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```

### Ruta, GUID, y región Bluemix
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

Especifica la ruta que se asigna a la aplicación de servidor que ha creado en Bluemix.

####GUID
{: ios-guid}

Especifica la clave exclusiva asignada a la aplicación que ha creado en Bluemix. Este valor distingue
                entre mayúsculas y minúsculas.

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

Especifica la ubicación en la que se aloja la aplicación. El parámetro `bluemixRegion` especifica qué despliegue de Bluemix está utilizando. Puede establecer este valor con una propiedad estática `BMSClient.REGION` y utilizar uno de estos tres valores:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

####AppGUID
{: ios-AppGUID}

Especifica la clave AppGUID exclusiva asignada al servicio Notificación push que ha creado en Bluemix. 

###Inicialización del SDK Push del cliente
{: initializing-the-client-Push-SDK}

####Objective-C
{: objc-initialize-push-sdk}

```
//Initialize client Push SDK for Objective-C
IMFPushClient *push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID"];

```

####Swift
{: swift-initialize-push-sdk}

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID")

```



## Registro de dispositivos y aplicaciones iOS
{: #enable-push-ios-notifications-register}


Se debe registrar una aplicación en APNs para recibir notificaciones remotas, después de instalarse en un dispositivo. Después de que la aplicación reciba la señal de dispositivo que ha generado APNs, debe volver a pasarse al servicio {{site.data.keyword.mobilepushshort}}.

Para registrar las aplicaciones y los dispositivos de iOS:

1. Cree una aplicación de fondo
2. Pase la señal a {{site.data.keyword.mobilepushshort}}


###Cree una aplicación de fondo
{: create-a-backend-app}

Cree una aplicación de fondo en el catálogo Bluemix® de la sección de Contenedores modelo, que enlaza automáticamente el servicio {{site.data.keyword.mobilepushshort}} a esta aplicación. Si ya ha creado una aplicación de fondo, asegúrese de enlazarla al servicio {{site.data.keyword.mobilepushshort}}. 

####Objective-C
{: objc-backendapp-code}

```
	//Para Objective-C
	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0){
	    [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];
	    [[UIApplication sharedApplication] registerForRemoteNotifications];
	    }
	    else{
	    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
	    (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
	    }
	    return YES;
	}
```

####Swift
{: swift-backendapp-code}

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
		let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: nil) UIApplication.sharedApplication().registerUserNotificationSettings(settings) UIApplication.sharedApplication().registerForRemoteNotifications()
	}
```

###Cómo pasar señales a {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

Una vez que APNs haya enviado la señal, pásela a {{site.data.keyword.mobilepushshort}} como parte del método `registerWithDeviceToken`.

####Objective-C
{: objc-token}

```
//Para Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];

 [client initializeWithBackendRoute:@"your-backend-route-here" backendGUID:@"Your-backend-GUID-here"];


 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID"];
[push registerWithDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if (error){
     NSLog(@"%@",error.description);
  }  else {
    NSLog(@"%@",response.responseJson.description);
}
}];
```

####Swift
{: swift-token}

Después de recibir la señal desde las APNS, pase la señal a Notificaciones Push como parte del método `didRegisterForRemoteNotificationsWithDeviceToken`.

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
  push.initializeWithAppGUID("appGUID")
  push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
  push.initializeWithPushAppGUID("pushAppGUID")
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
        if error.isEmpty {
            print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
        else{
            print( "Error during device registration \(error) ")
            print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }

}
```



## Recepción de notificaciones push en dispositivos iOS
{: #enable-push-ios-notifications-receiving}

Recibir notificaciones push en dispositivos iOS.

####Objective-C
{: objc-receive-push-notifications}

Para recibir notificaciones push en dispositivos iOS, añada el método Objective-C siguiente en la aplicación delegada de la aplicación.

```
// Para Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//El diccionario userInfo contendrá datos que ha enviado el servidor.
}
```

####Swift
{: swift-receive-push-notifications}
Para recibir notificaciones push en dispositivos iOS, añada el método Swift siguiente a la aplicación delegada de la aplicación.

```
 // Para Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //El diccionario UserInfo contendrá datos que ha enviado el servidor
   }

```



## Envío de notificaciones push básicas
{: #send}

Una vez que haya desarrollado sus aplicaciones, puede enviar notificaciones push básicas (sin
  utilizar etiquetas, identificadores, cargas útiles adicionales o archivos de sonido).


1. En **Elegir la audiencia**, seleccione una de las siguientes audiencias:
      **Todos los dispositivos**, o por plataforma: **Sólo dispositivos iOS** o
      **Sólo dispositivos Android**. 

	**Nota**: Cuando seleccione la opción **Todos los dispositivos**, todos los dispositivos que se han suscrito a las notificaciones push recibirán la notificación.

![pantalla Notificaciones](images/tag_notification.jpg)

2. En **Crear la notificación**, especifique el mensaje y, a continuación, pulse **Enviar**.
3. Verifique que los dispositivos hayan recibido la notificación. En la captura de pantalla siguiente se muestra un recuadro de alerta en el que se maneja una {{site.data.keyword.mobilepushshort}} en el primer plano y segundo plano de un dispositivo iOS.


	![Notificación push en primer plano en Android](images/iOS_Foreground.jpg)

![Notificación push en primer plano en iOS](images/iOS_Screenshot.jpg)




## Siguientes pasos
{: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede configurar
        las notificaciones basadas en código y las opciones avanzadas.

Añada estas características de Servicio de notificaciones push a la aplicación.
Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html).
Para utilizar opciones de notificaciones avanzadas, consulte [Notificaciones push avanzadas](t_advance_notifications.html).
