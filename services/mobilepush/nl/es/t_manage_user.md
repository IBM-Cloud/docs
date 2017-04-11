---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Registro de un dispositivo con userId
{: #register_device_with_userId}
Última actualización: 06 de febrero de 2017
{: .last-updated}

Para registrarse para la notificación basada en userID, complete los pasos siguientes:

## Android
{: android-register}

Inicialice la clase MFPPush con las claves `AppGUID` y `clientSecret` del servicio {{site.data.keyword.mobilepushshort}}.
```
// Inicialice el servicio de Notificaciones Push
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```
	{: codeblock}


- **AppGUID**: Esta es la clave AppGUID del servicio {{site.data.keyword.mobilepushshort}}.
- **clientSecret**: Esta es la clave clientSecret del servicio {{site.data.keyword.mobilepushshort}}.

  Utilice la API **registerDeviceWithUserId** para registrar el dispositivo para {{site.data.keyword.mobilepushshort}}.

```
// Registre el dispositivo en Notificaciones Push
push.registerDeviceWithUserId("userId",new MFPPushResponseListener<String>() {
		@Override
		public void onSuccess(String response) {
		Log.d("Device is registered with Push Service.");}
		@Override
    public void onFailure(MFPPushException ex) {
		  Log.d("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
		}
		});
```
	{: codeblock}

- **userId**: Pase el valor de userId exclusivo para registrarse para {{site.data.keyword.mobilepushshort}}.

**Nota:** para habilitar las {{site.data.keyword.mobilepushshort}} de destino según UserId, asegúrese de que registra el dispositivo con un userId y que también pasa el 'clientSecret' que está asignado cuando se suministran los servicios {{site.data.keyword.mobilepushshort}}. El registro del dispositivo no funcionará si no se proporciona un clientSecret válido.

## Cordova
{: cordova}

Utilice las siguientes API para registrarse para las {{site.data.keyword.mobilepushshort}} basadas en UserId.

```
// Registre el dispositivo para la Notificación Push con UserId
var options = {"userId": "Your User Id value"};
BMSPush.registerDevice(options,success, failure);
```
	{: codeblock}


- **userId**: Pase el valor de userId exclusivo para registrarse para {{site.data.keyword.mobilepushshort}}.


## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


- **AppGUID**: Esta es la clave AppGUID del servicio {{site.data.keyword.mobilepushshort}}.
- **clientSecret**: Esta es la clave clientSecret del servicio {{site.data.keyword.mobilepushshort}}.

Utilice la API **registerWithUserId** para registrar el dispositivo para {{site.data.keyword.mobilepushshort}}.

```
// Registre el dispositivo en el servicio de Notificaciones Push
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

- **userId**: Pase el valor de userId exclusivo para registrarse para {{site.data.keyword.mobilepushshort}}.

## Google Chrome, Safari y Mozilla Firefox
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
  
Tras la correcta inicialización, debe registrar la aplicación web con el userId.

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
