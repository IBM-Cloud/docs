---

copyright:
 years: 2015, 2016

---


# Dispositivo de registro con ID de usuario
{: #register_device_with_userId}
Última actualización: 16 de agosto de 2016
{: .last-updated}

Para registrarse para la notificación basada en el ID de usuario, complete los pasos siguientes:

## Android
{: android-register}
 
Inicialice la clase MFPPush con las claves `AppGUID` y `clientSecret` del servicio {{site.data.keyword.mobilepushshort}}.

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```

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

####userId
{: android-user-id}

Pase el valor ID de usuario exclusivo para registrarse para {{site.data.keyword.mobilepushshort}}.

**Nota:** Para habilitar las {{site.data.keyword.mobilepushshort}} objetivo de UserId, asegúrese de que registra el dispositivo con un UserId y que también pasa el 'clientSecret' que está asignado cuando se suministran los servicios {{site.data.keyword.mobilepushshort}}. Si no pasa un clientSecret válido, fallará el registro del dispositivo.


## Cordova
{: cordova-register}

Copie el siguiente fragmento de código en la aplicación móvil para registrarse para notificaciones basadas en userId.

Inicialice `MFPPush` con `clientsecret`. 

```
MFPPush.initialize("appGUID", "clientSecret");
```

###appGUID 
{: cordova-pushappguid}

Esta es la clave AppGUID del servicio {{site.data.keyword.mobilepushshort}}. 

####clientSecret 
{: cordova-client-secret}

Esta es la clave clientSecret del servicio {{site.data.keyword.mobilepushshort}}.

```
//Register for {{site.data.keyword.mobilepushshort}} with userId
var userId = "userId";
MFPPush.registerDevice({},success,failure,userId); 
```
####userId
{: cordova-user-id}

Pase el valor ID de usuario exclusivo para registrarse para el servicio {{site.data.keyword.mobilepushshort}}.


## Objective-C
{: objc-register}

Utilice las siguientes API para registrarse para las {{site.data.keyword.mobilepushshort}} basadas en UserId.

```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"]; 
```
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


####userId 
{: objc-user-id}

Pase el valor ID de usuario exclusivo para registrarse para {{site.data.keyword.mobilepushshort}}.

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```

####AppGUID 
{: swift-pushappguid}
Esta es la clave AppGUID del servicio {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: swift-client-secret} 

Esta es la clave clientSecret del servicio {{site.data.keyword.mobilepushshort}}.

Utilice la API **registerWithUserId** para registrar el dispositivo para {{site.data.keyword.mobilepushshort}}.

```
// Registre el dispositivo al servicio de Notificaciones push.
push.registerWithDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    } else {

        print( "Error during device registration \(error) ")
    }
}
```

####userId 
{: swift-user-id}

Pase el valor ID de usuario exclusivo para registrarse para {{site.data.keyword.mobilepushshort}}.


# Uso de notificaciones basadas en el ID de usuario
{: #using_userid}


Las notificaciones basadas en el ID de usuario son mensajes de notificación que están pensados para un usuario específico. Muchos dispositivos pueden registrarse con un usuario. Los pasos siguientes describen cómo enviar notificaciones basadas en el ID de usuario. 

1. Desde el panel de control de **Notificación Push**, pulse el separador
      **Notificaciones**.
1. Seleccione la opción **UserId** para enviar notificaciones basadas en userId.
1. En el campo **Búsqueda** de UserId, busque el userid que desee utilizar y, a continuación, pulse el botón **+Añadir**.![Pantalla de notificaciones](images/user_notification.jpg)
1. En el campo **Texto del mensaje**, especifique texto que desee enviar en la notificación.
1. Pulse el botón **Enviar**.
