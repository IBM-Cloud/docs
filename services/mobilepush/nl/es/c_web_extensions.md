---

copyright:
years: 2015 2016

---


# Habilitación de aplicaciones y extensiones de Chrome para recibir {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Última actualización: 17 de octubre de 2016
{: .last-updated}

Ya puede habilitar las aplicaciones y extensiones de Google Chrome para recibir {{site.data.keyword.mobilepushshort}}.

## Instalación del SDK del cliente para {{site.data.keyword.mobilepushshort}}
{: #web_install}

En este tema se describe cómo instalar y utilizar el SDK Push de JavaScript del cliente para seguir desarrollando aplicaciones y extensiones de Chrome.

### Inicialización en aplicaciones y extensiones de Google Chrome

Para la instalación del SDK de Javascript en las aplicaciones y extensiones de Chrome, realice estos pasos:

Descargue el `BMSPushSDK.js` y `manifest_Chrome_Ext.json` (para extensiones de Chrome) o `manifest_Chrome_App.json` (para aplicaciones de Chrome) desde el [SDK Push Web de Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master).



- Para aplicaciones de Chrome, configure el archivo de manifiesto:
 1. En el archivo `manifest_Chrome_App.json`, proporcione el nombre, la descripción y los iconos.
 2. Añada el `BMSPushSDK.js` en el `app.background.scripts`.
 3. Cambie el `manifest_Chrome_App.json` a `manifest.json`.

- Para las extensiones de Chrome, configure el archivo de manifiesto:
 1. En el archivo `manifest_Chrome_Ext.json`, proporcione el nombre, la descripción y los iconos.
 2. Añada el `BMSPushSDK.js` en el `background.scripts`.
 3. Cambie el `manifest_Chrome_Ext.json` a `manifest.json`.

En el archivo `background.js`, añada lo siguiente para recibir notificaciones push 
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked); 
```
	{: codeblock}



## Inicialización del SDK Push 
{: #web_initialize}

Inicialice el SDK Push con `app GUID` y `app Region` del servicio {{site.data.keyword.mobilepushshort}} de Bluemix.  

Para obtener el GUID de la aplicación, seleccione la opción **Configuración** en el panel de navegación de los servicios push inicializados y haga clic en **Opciones móviles**. Modifique el fragmento de código para que utilice el parámetro appGUID del servicio de notificaciones push de Bluemix.

`App Region` especifica la ubicación en la que se aloja el servicio {{site.data.keyword.mobilepushshort}}. Puede utilizar uno de estos tres valores:

 - Para Dallas, EE.UU.:	 `.ng.bluemix.net`
 - Para RU:			 `.eu-gb.bluemix.net`
 - Para Sídney:		 `.au-syd.bluemix.net`

```
 var bmsPush = new BMSPush();
    function callback(response) {
 alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Registro de las aplicaciones y extensiones de Chrome
{: #web_register}

Utilice la API `register()` para registrar el dispositivo con el servicio {{site.data.keyword.mobilepushshort}}. Para efectuar el registro desde Google Chrome, añada el URL del sitio web y la clave de API de Firebase Cloud Messaging (FCM) o Google Cloud Messaging (GCM) en el panel de control de configuración web del servicio {{site.data.keyword.mobilepushshort}} de Bluemix. Para obtener más información, consulte [Configuración de credenciales para Google Cloud Messaging](t_push_provider_android.html) en la configuración de Chrome.

Para efectuar el registro desde Mozilla Firefox, añada el URL del sitio web en el panel de control de configuración web del servicio {{site.data.keyword.mobilepushshort}} de Bluemix.

Utilice el siguiente fragmento de código para realizar el registro en el servicio {{site.data.keyword.mobilepushshort}} de Bluemix.
```
var bmsPush = new BMSPush();
    function callback(response) {
     alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}

## Envío de {{site.data.keyword.mobilepushshort}} básicas
  {: #send}

Una vez que haya desarrollado sus aplicaciones, puede enviar una notificación push. 

1. Seleccione **Enviar notificaciones** y para redactar un mensaje seleccione **Notificaciones web** como opción **Enviar a**. 
2. Escriba el mensaje en el campo **Mensaje**.
3. Puede elegir que se proporcionen valores opcionales:
  - **Título de notificación**: es el texto que se visualizará como mensaje en la cabecera de la alerta de mensaje.
  - **URL de icono de notificación**: si el mensaje debe entregarse con un icono de notificación de la aplicación, indique el enlace al icono en este campo.
  - **Contraer clave**: las claves contraídas se adjuntan a las notificaciones. Si llegan varias notificaciones de forma secuencias con la misma clave contraída cuando el dispositivo está desconectado, estas se contraerán. Cuando el dispositivo vuelva a conectarse, recibirá las notificaciones del servidor FCM/GCM y mostrará solo la última notificación transportada con la misma clave contraída. Si no se establece esta clave contraída, se almacenarán los mensajes nuevos y antiguos para entregarlos más adelante.
  - **Tiempo de duración**: este valor se establece en segundos. Si no se especifica este parámetro, el servidor FCM/GCM almacenará el mensaje cuatro semanas e intentará entregarlo. La validez caduca transcurridas cuatro semanas. El intervalo de valores posible es de 0 a 2.419.200 segundos.
  - **Retrasar cuando esté desocupado**: si se define como `true`, el servidor FCM/GCM no entregará la notificación cuando el dispositivo esté desocupado. Establezca este valor en `false` para garantizar que se entregan notificaciones aunque el dispositivo esté desocupado.
  - **Carga útil adicional**: permite especificar valores personalizados de carga útil para las notificaciones.

En la imagen siguiente se muestra la opción de notificaciones web en el panel de control.

  ![pantalla Notificaciones](images/push_chrome_extns.jpg)
  
## Pasos siguientes
  {: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede configurar las notificaciones basadas en código y las opciones avanzadas.

Añada estas características del servicio {{site.data.keyword.mobilepushshort}} a la aplicación. Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html). Para utilizar opciones de notificaciones avanzadas, consulte [Notificaciones avanzadas](t_advance_badge_sound_payload.html).



