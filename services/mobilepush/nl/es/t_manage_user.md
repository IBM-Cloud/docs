---

copyright:
 years: 2015, 2016

---


# Registro de un dispositivo con userId
{: #register_device_with_userId}
Última actualización: 17 de octubre de 2016
{: .last-updated}

Para registrarse para la notificación basada en userID, complete los pasos siguientes:

## Android
{: android-register}

Inicialice la clase MFPPush con las claves `AppGUID` y `clientSecret` del servicio {{site.data.keyword.mobilepushshort}}.
```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```
	{: codeblock}

####AppGUID
{: push-app-guid}

Esta es la clave AppGUID del servicio {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: android-client-secret}

Esta es la clave clientSecret del servicio {{site.data.keyword.mobilepushshort}}.

Utilice la API **registerDeviceWithUserId** para registrar el dispositivo para {{site.data.keyword.mobilepushshort}}.
```
// Register the device to {{site.data.keyword.mobilepushshort}}.
push.registerDeviceWithUserId("userId",new MFPPushResponseListener<String>() {
  @Override
	    public void onSuccess(String deviceId) {
    Log.d("Device is registered with Push Service.");
  }
  @Override
    public void onFailure(MFPPushException ex) {
      Log.d("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
  }
});
```
	{: codeblock}

####userId
{: android-user-id}

Pase el valor de userID exclusivo para registrarse para {{site.data.keyword.mobilepushshort}}.

**Nota:** para habilitar las {{site.data.keyword.mobilepushshort}} de destino según UserId, asegúrese de que registra el dispositivo con un userId y que también pasa el 'clientSecret' que está asignado cuando se suministran los servicios {{site.data.keyword.mobilepushshort}}. El registro del dispositivo no funcionará si no se proporciona un clientSecret válido.


## Objective-C
{: objc-register}

Utilice las siguientes API para registrarse para las {{site.data.keyword.mobilepushshort}} basadas en UserId.
```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"];
```
	{: codeblock}

###AppGUID
{: objc-pushappguid}

Esta es la clave AppGUID del servicio {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: objc-client-secret}

Esta es la clave clientSecret del servicio {{site.data.keyword.mobilepushshort}}.

Utilice la API **registerWithUserId** para registrar el dispositivo para {{site.data.keyword.mobilepushshort}}.
```
// Registre el dispositivo para enviar por push el servicio de notificaciones.
[push registerWithDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
  NSString *message=@"";
	if (error){
        message = [NSString stringWithFormat:@"Error registering for push notifications: %@", error.description];
        NSLog(@"%@",message);
    } else {
     message=@"Successfully registered for push notifications";
        NSLog(@"%@",message);
    }
}];
```
	{: codeblock}

####userId
{: objc-user-id}

Pase el valor de userID exclusivo para registrarse para {{site.data.keyword.mobilepushshort}}.

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}

####AppGUID
{: swift-pushappguid}
Esta es la clave AppGUID del servicio {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: swift-client-secret}

Esta es la clave clientSecret del servicio {{site.data.keyword.mobilepushshort}}.

Utilice la API **registerWithUserId** para registrar el dispositivo para {{site.data.keyword.mobilepushshort}}.

```
// Registre el dispositivo para enviar por push el servicio de notificaciones.
push.registerWithDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {
  print( "Response during device registration : \(response)")
        print( "status code during device registration : \(statusCode)")
    } else {
  print( "Error during device registration \(error) ")
    }
  }
```
	{: codeblock}

####userId
{: swift-user-id}

Pase el valor de userID exclusivo para registrarse para {{site.data.keyword.mobilepushshort}}.

## Google Chrome y Mozilla Firefox
{: web-register}

Utilice las API siguientes para registrarse para las notificaciones basadas en userID. Inicialice el SDK con `app GUID`, `app Region` y `Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
    })
```
	{: codeblock}
  
Una vez inicializado correctamente, registre la aplicación web con userID.

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

## Aplicaciones y extensiones de Google Chrome
{: web-register-new}

Utilice las API siguientes para registrarse para las notificaciones basadas en userID. Inicialice el SDK con `app GUID`, `app Region` y `Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
    })
```
	{: codeblock}
  
Una vez inicializado correctamente, registre la aplicación web con userID.

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

# Uso de notificaciones basadas en userId
{: #using_userid}


Las notificaciones basadas en userID son mensajes de notificación que están pensados para un usuario específico. Muchos dispositivos pueden registrarse con un usuario. Los pasos siguientes describen cómo enviar notificaciones basadas en el ID de usuario.

1. Desde el panel de control **Notificación Push**, seleccione la opción **Enviar notificaciones**.
1. Seleccione **UserId** en la lista de opciones **Enviar a**.
1. En el campo **ID de usuario**, busque el ID del usuario que desea utilizar y, a continuación, pulse **+Añadir**.![Pantalla de notificaciones](images/user_notification.jpg)
1. En el campo **Mensaje**, escriba el texto que desea enviar en la notificación.
1. Pulse **Enviar**.
