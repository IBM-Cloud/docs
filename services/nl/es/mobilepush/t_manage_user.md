---

copyright:
 years: 2015, 2016

---


# Dispositivo de registro con UserId
{: #register_device_with_userId}
*Última actualización: 20 de julio de 2016*
{: .last-updated}

Para registrarse para la notificación basada en el ID de usuario, complete los pasos siguientes:

## Android
 
Inicialice la clase IMFPush con la clave `pushTenantId` y `clientSecret` del servicio Notificación push.

```
// Inicialice el MFPPush
push = MFPPush.getInstance();
push.initializeBluemixPushWithClientSecret(getApplicationContext(),"clientSecret");
```

**clientSecret** 

Esta es la clave clientSecret del servicio de Notificaciones push.


Utilice la API de **registerWithUserId** para registrar el dispositivo para notificaciones push.

```
// Registre el dispositivo para enviar por push el servicio de notificaciones.
push.registerWithUserId("userId",new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
        updateTextView("Device is registered with Push Service.");
        displayTags();
    }

    @Override
    public void onFailure(MFPPushException ex) {
        updateTextView("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
    }
});
```

**userId** 

Pase el valor ID de usuario exclusivo para registrarse para notificaciones push.

>**Nota:** Para habilitar las notificaciones push objetivo de UserId, asegúrese de que registra el dispositivo con un UserId y que también pasa el 'clientSecret' que está asignado cuando se suministran los servicios Notificaciones push. Si no pasa un clientSecret válido, fallará el registro del dispositivo.


## Cordova

Copie el siguiente fragmento de código a la aplicación móvil para registrarse para notificaciones basadas en el ID de usuario.

Inicialice `MFPPush` con `clientsecret`. 

```
MFPPush.initializeBluemixPushWithClientSecret("clientSecret");
```

**clientSecret** 

Esta es la clave clientSecret del servicio de Notificaciones push.

```
//Regístrese para la Notificación push con userId
var userId = "userId";
MFPPush.registerWithUserId(userId,success,failure);
```
**userId** 

Pase el valor ID de usuario exclusivo para registrarse para el servicio de Notificación push.


## Objective-C


Utilice las siguientes API para registrarse para las notificaciones push basadas en el ID de usuario.


```
// Inicialice el MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeBluemixPushWithClientSecret:@"clientSecret"];
```

**clientSecret** 

Esta es la clave clientSecret del servicio de Notificaciones push.


Utilice la API de **registerWithUserId** para registrar el dispositivo para notificaciones push.


```
// Registre el dispositivo para enviar por push el servicio de notificaciones.
[push registerDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
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


**userId** 

Pase el valor ID de usuario exclusivo para registrarse para notificaciones push.

## Swift

```
// Inicialice el BMSPushCliet
let push =  BMSPushClient.sharedInstance
push.initializeBluemixPushWithClientSecret("clientSecret")
```

**clientSecret** 

Esta es la clave clientSecret del servicio de Notificaciones push.

Utilice la API de **registerWithUserId** para registrar el dispositivo para notificaciones push.

```
// Registre el dispositivo al servicio de Notificaciones push.
push.registerDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    } else {

        print( "Error during device registration \(error) ")
    }
}
```

**userId** 

Pase el valor ID de usuario exclusivo para registrarse para notificaciones push.


# Uso de notificaciones basadas en el ID de usuario
{: #using_userid}


Las notificaciones basadas en el ID de usuario son mensajes de notificación que están pensados para un usuario específico. Muchos dispositivos pueden registrarse con un usuario. Los pasos siguientes describen cómo enviar notificaciones basadas en el ID de usuario. 

1. Desde el panel de control de **Notificación Push**, pulse el separador
      **Notificaciones**.
1. Seleccione la opción **UserId** para enviar notificaciones basadas en userId.
1. En el campo **Búsqueda** de UserId, busque el userid que desee utilizar y, a continuación, pulse el botón **+Añadir**.![Pantalla de notificaciones](images/tag_notification.jpg)
1. En el campo **Texto del mensaje**, especifique texto que desee enviar en la notificación.
1. Pulse el botón **Enviar**.
