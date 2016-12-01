---

copyright:
years: 2015 2016

---


# Habilitación de aplicaciones web para recibir {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Última actualización: 15 de noviembre de 2016
{: .last-updated}

Ya puede habilitar las aplicaciones web Google Chrome y Mozilla Firefox para recibir {{site.data.keyword.mobilepushshort}}.

## Instalación del SDK del cliente de navegador web para {{site.data.keyword.mobilepushshort}}
{: #web_install}

En este tema se describe cómo instalar y utilizar el SDK Push de JavaScript del cliente para seguir desarrollando aplicaciones web.

### Inicialización en la aplicación web

Para instalar el SDK de Javascript en la aplicación web de Google Chrome, siga estos pasos:

Descargue `BMSPushSDK.js`, `BMSPushServiceWorker.js` y `manifest_Website.json` desde el [SDK Push Web de Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master).

1. Edite el archivo `manifest_Website.json`.

Para el navegador Google Chrome, cambie `name` por el nombre de su sitio. Por ejemplo, `www.dailynewsupdates.com`. Cambie `gcm_sender_id` por su sender_ID de Firebase Cloud Messaging (FCM) o Google Cloud Messaging (GCM). Para obtener más información, consulte [Cómo obtener el ID de remitente y la clave de la API](t_push_provider_android.html). El valor de gcm_sender_id solo contiene números.

```
 {
  "name": "YOUR_WEBSITE_NAME",
      "gcm_sender_id": "GCM_Sender_Id"
 }
```
    {: codeblock}
 
En el navegador Mozilla Firefox, añada los valores siguientes al archivo `manifest.json`.     Especifique el valor adecuado para `name`. Debe ser el nombre del sitio web. 

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

## Inicialización del SDK Push Web 
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
  bmsPush.initialize(initParams, callback)
```
	{: codeblock}

## Registro de la aplicación web
{: #web_register}

Utilice la API `register()` para registrar el dispositivo con el servicio {{site.data.keyword.mobilepushshort}}. Utilice una de las siguientes opciones, según el navegador. 

- Para efectuar el registro desde Google Chrome, añada el URL del sitio web y la clave de API de Firebase Cloud Messaging (FCM) o Google Cloud Messaging (GCM) en el panel de control de configuración web del servicio {{site.data.keyword.mobilepushshort}} de Bluemix. Para obtener más información, consulte [Configuración de credenciales para Google Cloud Messaging](t_push_provider_android.html) en la configuración de Chrome.



- Para efectuar el registro desde Mozilla Firefox, añada el URL del sitio web en el panel de control de configuración web del servicio {{site.data.keyword.mobilepushshort}} de Bluemix.

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






