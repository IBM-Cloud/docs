---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Habilitación de aplicaciones web para recibir notificaciones push
{: #web_notifications}
Última actualización: 12 de abril de 2017
{: .last-updated}

Puede habilitar las aplicaciones web Google Chrome, Mozilla Firefox y Safari para recibir {{site.data.keyword.mobilepushshort}}. Asegúrese de haber [configurado credenciales para un proveedor de notificaciones](t__main_push_config_provider.html) antes de continuar con estos pasos.

## Instalación del SDK del cliente de navegador web para {{site.data.keyword.mobilepushshort}}
{: #web_install}

En este tema se describe cómo instalar y utilizar el SDK Push de JavaScript del cliente para seguir desarrollando aplicaciones web.

### Inicialización en la aplicación web
{: #web_initialise_web_app}

Para instalar el SDK de Javascript en la aplicación web de Google Chrome, siga estos pasos:

Descargue los archivos `BMSPushSDK.js`, `BMSPushServiceWorker.js` y `manifest_Website.json` desde el [SDK Push Web de Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}.

1. Edite el archivo `manifest_Website.json`.
	- Para el navegador Google Chrome, cambie `name` por el nombre de su sitio. Por ejemplo, `www.dailynewsupdates.com`. Cambie `gcm_sender_id` por su sender_ID de Firebase Cloud Messaging (FCM) o Google Cloud Messaging (GCM). Para obtener más información, consulte [Configuración de credenciales para un proveedor de notificaciones](t__main_push_config_provider.html).El valor de gcm_sender_id solo contiene números.

		```
			{
	"name": "YOUR_WEBSITE_NAME",
  			"gcm_sender_id": "GCM_Sender_Id"
			 }
		```
    		{: codeblock}
 
	- Para el navegador Mozilla Firefox, añada los valores siguientes al archivo `manifest_Website.json`. Especifique el valor adecuado para `name`. Debe ser el nombre del sitio web.

		```
			{ 
	"name": "YOUR_WEBSITE_NAME"
			 }
		```
    		{: codeblock}

2. Cambie el nombre del archivo `manifest_Website.json` a `manifest.json`.
3. Añada `BMSPushSDK.js`, `BMSPushServiceWorker.js` y `manifest.json` al directorio raíz del sitio web.
3. Incluya `manifest.json` en la etiqueta `<head>` del archivo html.
	```
		<link rel="manifest" href="manifest.json">
	```
    	{: codeblock}
4. Incluya el SDK de envío web de Bluemix en la aplicación web.
	```
		<script src="BMSPushSDK.js" async></script>
	```
    	{: codeblock}

**Nota**: Asegúrese de que el código esté desplegado y de que se pueda acceder al enlace de muestra mediante `https`, y no `http`. 

## Inicialización del SDK Push Web 
{: #web_initialize}

Inicialice el SDK Push con `app GUID` y `app Region` del servicio {{site.data.keyword.mobilepushshort}} de Bluemix.  

Para obtener el GUID de la app, seleccione la opción **Configuración** en el panel de navegación de los servicios push inicializados y haga clic en **Opciones móviles**. Modifique el fragmento de código para que utilice el parámetro appGUID del servicio de notificaciones push de Bluemix.

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
  "appRegion":"Región donde se aloja el servicio",
   "clientSecret":"clientSecret del servicio push"
   "websitePushIDSafari": "Parámetro opcional sólo para Notificaciones Push de Safari. El valor debe coincidir con el ID Push del sitio web proporcionado durante la configuración del lado del servidor".
    }
  	bmsPush.initialize(initParams, callback)
```
	{: codeblock}

**Nota**: Si se modifican las credenciales de FCM para el SDK Push Web, es posible que falle la entrega de mensajes para el navegador Chrome. Asegúrese de que invoca `bmsPush.unRegisterDevice` para evitar anomalías.

Es posible que vea errores relacionados con la configuración su especifica un parámetro erróneo. Para obtener más información, consulte [Resolución de problemas](troubleshooting.html).

## Registro de la aplicación web
{: #web_register}

Utilice la API **register()** para registrar el dispositivo con el servicio {{site.data.keyword.mobilepushshort}}. Utilice una de las siguientes opciones, según el navegador.

- Para efectuar el registro desde Google Chrome, añada el URL del sitio web y la clave de API de Firebase Cloud Messaging (FCM) o Google Cloud Messaging (GCM) en el panel de control de configuración web del servicio {{site.data.keyword.mobilepushshort}} de Bluemix. Para obtener más información, consulte [Configuración de credenciales para un proveedor de notificaciones](t__main_push_config_provider.html) en la configuración de Chrome.

- Para efectuar el registro desde Mozilla Firefox, añada el URL del sitio web en el panel de control de configuración web del servicio {{site.data.keyword.mobilepushshort}} de Bluemix.

Utilice el siguiente fragmento de código para realizar el registro en el servicio {{site.data.keyword.mobilepushshort}} de Bluemix.

```
	var bmsPush = new BMSPush();
    function callback(response) {
     alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Región donde se aloja el servicio",
   "clientSecret":"clientSecret del servicio push"
   "websitePushIDSafari": "Parámetro opcional sólo para Notificaciones Push de Safari. El valor debe coincidir con el ID Push del sitio web proporcionado durante la configuración del lado del servidor".
    }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}


## Envío de notificaciones básicas a navegadores web
{: #web_browsers}

Una vez que haya desarrollado sus aplicaciones, puede enviar una notificación push. 

1. Seleccione **Enviar notificaciones** y para redactar un mensaje seleccione **Notificaciones web** como opción **Enviar a**. 
2. Escriba el mensaje en el campo **Mensaje**.
3. Puede elegir que se proporcionen valores opcionales:
  - **Título de notificación**: es el texto que se visualizará como mensaje en la cabecera de la alerta de mensaje.
  - **URL de icono de notificación**: si el mensaje debe entregarse con un icono de notificación de la app, indique el enlace al icono en este campo.
  - **Tiempo de duración**: notifica al servidor sobre la validez de los mensajes.
4. Para notificaciones web enviadas al navegador Safari, hay alguna información adicional necesaria:
  - **Acción**: esta es la etiqueta del botón de acción.
  - **Argumentos URL**: los argumentos URL que necesitan utilizarse con esta notificación. Asegúrese de que se proporciona en la forma de una matriz JSON. 
 
En la imagen siguiente se muestra la opción de notificaciones web en el panel de control.

  ![pantalla Notificaciones](images/DashboardWebpush.jpg)


### Pasos siguientes
{: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede optar por configurar las notificaciones basadas en código y las opciones avanzadas.

Añada estas características del servicio {{site.data.keyword.mobilepushshort}} a su app.
Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html). Para utilizar opciones de notificaciones avanzadas, consulte [Notificaciones avanzadas](t_advance_badge_sound_payload.html).






