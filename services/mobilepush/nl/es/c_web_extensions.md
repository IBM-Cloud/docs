---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Habilitación de aplicaciones y extensiones de Chrome para recibir {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Última actualización: 18 de enero de 2017
{: .last-updated}

Puede habilitar las aplicaciones y extensiones de Google Chrome para que reciban {{site.data.keyword.mobilepushshort}}. Asegúrese de haber [configurado credenciales para un proveedor de notificaciones](t__main_push_config_provider.html) antes de continuar con estos pasos.

## Instalación del SDK del cliente para {{site.data.keyword.mobilepushshort}}
{: #web_install}

En este tema se describe cómo instalar y utilizar el SDK Push de JavaScript del cliente para seguir desarrollando aplicaciones y extensiones de Chrome.

### Inicialización en aplicaciones y extensiones de Google Chrome

Para la instalación del SDK de Javascript en las aplicaciones y extensiones de Chrome, realice estos pasos:

Descargue `BMSPushSDK.js` y `manifest_Chrome_Ext.json` (para extensiones de Chrome) o `manifest_Chrome_App.json` (para aplicaciones de Chrome) desde el [SDK de push web de Bluemix ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}.



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




