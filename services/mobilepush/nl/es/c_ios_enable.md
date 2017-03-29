---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Habilitación de aplicaciones iOS para enviar {{site.data.keyword.mobilepushshort}}
{: #enable-push-ios-notifications}
Última actualización: 14 de febrero de 2017
{: .last-updated}

Puede habilitar aplicaciones iOS para enviar {{site.data.keyword.mobilepushshort}} a sus dispositivos.


##Instalación de CocoaPods
{: #enable-push-ios-notifications-install}

Para un proyecto Xcode existente, puede configurar el SDK del cliente de Bluemix Mobile Services mediante la herramienta de gestión de dependencias de CocoaPods. Una alternativa es instalar el SDK manualmente.

Para ver el archivo readme de Push de Swift, vaya a [Readme ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.



1. Instale CocoaPods utilizando el siguiente mandato en su terminal Mac.
```$ sudo gem install cocoapods
```
	{: codeblock}
2. Especifique el mandato `pod init` en el terminal para inicializar CocoaPods. Asegúrese de ejecutar el mandato desde el directorio en el que se encuentra el proyecto Xcode. El mandato `pod init` crea un Podfile.  
3. En el Podfile generado, añada las dependencias de SDK necesarias. Copie el siguiente Podfile.
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
		use_frameworks!
		target 'MyApp' do
	    platform :ios, '8.0'
		pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. Desde el terminal, vaya a la carpeta del proyecto e instale las dependencias con el mandato `pod update`.

El mandato instala las dependencias y crea un nuevo espacio de trabajo Xcode.  
**Nota**: Asegúrese de abrir siempre el nuevo espacio de trabajo de Xcode, en lugar del archivo de proyecto Xcode original:
```
  $ open App.xcworkspace
```
	{: codeblock}

El espacio de trabajo contiene el proyecto original y el proyecto Pods que contiene las dependencias. Para modificar una carpeta fuente de Bluemix mobile services, puede encontrarla en el proyecto Pods, en `Pods/yourImportedSourceFolder`, por ejemplo: `Pods/BMSPush`.

##Adición de infraestructuras mediante Carthage
{: #carthage}

Añada infraestructuras al proyecto utilizando [Carthage ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}. Tenga en cuenta que Carthage en Xcode8 no está soportado.

1. Añada infraestructuras `BMSPush` a Cartfile:
```
  github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. Ejecute el mandato `carthage update`. Cuando la compilación finalice, arrastre `BMSPush.framework`, `BMSCore.framework` y `BMSAnalyticsAPI.framework` al proyecto Xcode.
3. Siga las instrucciones del sitio de [Carthage ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} para llevar a cabo la integración.

##Configuración del SDK de iOS
{: ios-sdk}

Configure el SDK de iOS, añada el código siguiente al archivo **AppDelegate.swift** de su aplicación. Tenga en cuenta que también se registra con APNs.  
```
  func application(_ application: UIApplication,
  didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool
   {
   BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

##Utilización de infraestructuras importadas y carpetas fuente
{: using-imported-frameworks}

Haga referencia al SDK del código. Asegúrese de que se cumplen los requisitos previos siguientes.

- iOS 8.0 o superior	
- Xcode 7

Escriba directivas `#import` para las cabeceras relevantes, por
ejemplo:
```
//swift
import BMSCore
import BMSPush
```
		{: codeblock}

Para leer el archivo readme de Push de Swift, consulte [Readme ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}.

**Nota**: La actualización del proyecto Pods utilizando los mandatos CocoaPods `pod install` o `pod update` puede alterar temporalmente las carpetas fuente de Bluemix Mobile services. Si desea conservar las versiones personalizadas
de los archivos originales, asegúrese de que se les ha hecho la copia de seguridad antes de emitir uno de estos
mandatos.


##Crear configuración
{: build-settings}

Vaya a **Xcode > Crear configuración > Opciones de creación y Establecer la habilitación de Bitcode** en **No**.

**Atención**: A partir de iOS 9, los cambios a la característica de App Transport Security (ATS) pueden afectar a la forma de manejar el proceso de autenticación. En las siguientes publicaciones del blog se ofrece más información sobre los cambios: [ATS y Bitcode en iOS 9 ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} y [Conecte su app iOS 9 a Bluemix hoy mismo ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

## Inicialización de SDK Push para aplicaciones iOS
{: #enable-push-ios-notifications-initialize}

Un lugar común para colocar el código de inicialización se encuentra en el delegado de aplicación para la aplicación iOS. Pulse el enlace **Opciones móviles** en el panel de control Push para obtener la ruta y el GUID de la aplicación.

###Inicialización del SDK principal
{: Initializing-the-core-sdk}


```
// Inicialice el SDK principal para Swift con la GUID, la ruta y la región de IBM Bluemix
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

### Ruta, GUID, y región Bluemix
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

Especifica la ruta que se asigna a la aplicación de servidor que ha creado en Bluemix.

####GUID
{: ios-guid}

Especifica la clave exclusiva asignada a la aplicación que ha creado en Bluemix. Este valor distingue entre mayúsculas y minúsculas.

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

Especifica la ubicación en la que se aloja la aplicación. El parámetro `bluemixRegion` especifica qué despliegue de Bluemix está utilizando. Puede establecer este valor con una propiedad estática `BMSClient.REGION` y utilizar uno de estos tres valores:

- BMSClient.Region.usSouth 
- BMSClient.Region.unitedKingdom
- BMSClient.Region.sydney

####AppGUID
{: ios-AppGUID}

Especifica la clave AppGUID exclusiva asignada al servicio {{site.data.keyword.mobilepushshort}} que ha creado en Bluemix.

###Inicialización del SDK Push del cliente
{: initializing-the-client-Push-SDK}

```
	//Inicializar el SDK Push del cliente para Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


## Registro de dispositivos y aplicaciones iOS
{: #enable-push-ios-notifications-register}


Se debe registrar una aplicación en APNs para recibir notificaciones remotas, después de instalarse en un dispositivo. Después de que la aplicación reciba la señal de dispositivo que APNs ha generado, debe volver a pasarse al servicio {{site.data.keyword.mobilepushshort}}.

Para registrar las aplicaciones y los dispositivos de iOS, tiene que:

1. Crear una aplicación de fondo.
2. Pasar la señal a {{site.data.keyword.mobilepushshort}}.


###Crear una aplicación de fondo
{: create-a-backend-app}

Cree una aplicación de fondo en el catálogo Bluemix® de la sección de Contenedores modelo, que enlaza automáticamente el servicio {{site.data.keyword.mobilepushshort}} a esta aplicación. Si ya ha creado una aplicación de fondo, asegúrese de enlazarla al servicio {{site.data.keyword.mobilepushshort}}.


###Cómo pasar señales a {{site.data.keyword.mobilepushshort}}
{: pass-token-push-notifications}

Una vez que APNs haya enviado la señal, pásela a {{site.data.keyword.mobilepushshort}} como parte del método `registerWithDeviceToken`.

Después de recibir la señal desde APNs, pase la señal a Notificaciones Push como parte del método `didRegisterForRemoteNotificationsWithDeviceToken`.

```
  func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
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
	{: codeblock}


## Recepción de notificaciones push en dispositivos iOS
{: #enable-push-ios-notifications-receiving}


Para recibir notificaciones push en dispositivos iOS, añada el método Swift siguiente a la aplicación delegada de la aplicación.

```
  // Para Swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //El diccionario UserInfo contendrá datos que ha enviado el servidor }
```
	{: codeblock}

## Supervisión de notificaciones push en dispositivos iOS
{: ios-monitoring}

Para supervisar el estado actual de la notificación, añada el método Swift siguiente a la aplicación delegada de la aplicación.

```
	// Enviar estado de notificación cuando se abre la app pulsando las notificaciones
	func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
 	let push =  BMSPushClient.sharedInstance
 	let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 	let data = respJson.data(using: String.Encoding.utf8)
 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 	let messageId:String = jsonResponse.value(forKey: "nid") as! String
    push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
      print("Send message status to the Push server")
     }
}
```
	{: codeblock}

```
	// Enviar estado de notificación cuando la app esté en modalidad de fondo.
	func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 	let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
 	self.showAlert(title: "Recieved Push notifications", message: payLoad)
 	let push =  BMSPushClient.sharedInstance
 	let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 	let data = respJson.data(using: String.Encoding.utf8)
 	let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 	let messageId:String = jsonResponse.value(forKey: "nid") as! String
 	push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
   }
}
```
	{: codeblock}


## Envío de notificaciones push básicas
{: #send}

Una vez que haya desarrollado sus aplicaciones, puede enviar notificaciones push básicas.

Para ello, realice estos pasos:

1. Seleccione **Enviar notificaciones** y para redactar un mensaje seleccione la opción **Enviar a**. Las opciones admitidas son **Dispositivo por etiqueta**, **ID de dispositivo**, **ID de usuario**, **Dispositivos Android**, **Dispositivos iOS**, **Notificaciones web** y **Todos los dispositivos**.  
**Nota**: Cuando seleccione la opción **Todos los dispositivos**, todos los dispositivos suscritos a {{site.data.keyword.mobilepushshort}} recibirán notificaciones.
![pantalla Notificaciones](images/tag_notification.jpg)

2. En el campo **Mensaje**, redacte el mensaje. Elija configurar los valores opcionales según sea necesario.
3. Pulse **Enviar**.
3. Verifique que los dispositivos hayan recibido la notificación.

En la captura de pantalla siguiente se muestra un recuadro de alerta en el que se maneja una {{site.data.keyword.mobilepushshort}} en un dispositivo iOS.

![Notificación push en primer plano en iOS](images/iOS_Screenshot.jpg) 

### Valores opcionales para el envío de notificaciones
{: #send_ios_otpional_setting}

Puede personalizar aún más los valores de {{site.data.keyword.mobilepushshort}} para el envío de notificaciones a dispositivos iOS. Se admiten las siguientes opciones de personalización.

- **Identificador**: Indica el número que se muestra en el identificador de la aplicación. El valor predeterminado es cero (0), que no mostraría un identificador. 
- **Sonido**: indica un fragmento de sonido que se reproducirá al recibir una notificación. Da soporte a la opción predeterminada o al nombre de un recurso de sonido incorporado en la aplicación.
- **Carga útil adicional**: permite especificar valores personalizados de carga útil para las notificaciones.

##Habilitación de notificaciones interactivas

Ahora puede enriquecer sus notificaciones de iOS con más detalles como la adición de una imagen, mapa o un botón de respuesta mediante la habilitación de notificaciones interactivas. Ello proporciona más contexto a los clientes, junto con la capacidad para realizar una acción inmediata sin abandonar el contexto actual.  

Para habilitar las notificaciones interactivas, utilice el código siguiente:

```
	// Esto define la acción del botón.
	let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
```
	{: codeblock}
```
	// Esto define la categoría para los botones
let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
```
	{: codeblock}
```
	// Esto actualiza el registro para que incluya la categoría definida de buttonsPass en iOS BMSPushClientOptions
let notificationOptions = BMSPushClientOptions(categoryName: [category])
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
```
	{: codeblock}

Para enviar una notificación interactiva, realice estos pasos:

1. En la sección Componer, para la lista desplegable Enviar a, seleccione **Dispositivos iOS**.
2. Introduzca el mensaje de notificación que puede desear enviar.
3. En la sección Valores opcionales, seleccione **Móvil** y pulse **iOS**.
4. En la lista desplegable Tipo, seleccione **Mixto**.
5. En el campo Categoría, especifique el tipo de notificación que ha definido en la app. 

![Notificación interactiva para iOS](images/push_ios_notification_interactive.jpg) 

## Pasos siguientes
{: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede configurar las notificaciones basadas en código y las opciones avanzadas.

Añada estas características de servicio de notificaciones push a la app. Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html).
Para utilizar opciones de notificaciones avanzadas, consulte [Habilitación de notificaciones push avanzadas](t_advance_badge_sound_payload.html).
