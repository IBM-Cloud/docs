---

copyright:
years: 2015 2016

---


# Habilitación de aplicaciones web para recibir {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Última actualización: 17 de octubre de 2016
{: .last-updated}

Ya puede habilitar las aplicaciones web Google Chrome y Mozilla Firefox para recibir {{site.data.keyword.mobilepushshort}}.

## Instalación del SDK del cliente de navegador web para {{site.data.keyword.mobilepushshort}}
{: #web_install}

En este tema se describe cómo instalar y utilizar el SDK Push de JavaScript del cliente para seguir desarrollando aplicaciones web.

### Inicialización en la aplicación web Google Chrome

Para la instalación del SDK de Javascript en la aplicación web de Chrome, realice estos pasos:

Descargue `BMSPushSDK.js`, `BMSPushServiceWorker.js` y `manifest_Website.json` desde el [SDK Push Web de Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master).

1. Edite el archivo `manifest_Website.json`.

Para el navegador Google Chrome, cambie `name` por el nombre de su sitio. Cambie `gcm_sender_id` a su sender_ID de Firebase Cloud Messaging (FCM) o Google Cloud Messaging (GCM). Para obtener más información, consulte [Documentación de Google](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/#make_a_project_on_the_google_developer_console). El valor de gcm_sender_id solo contiene números.

```
 {
  "name": "YOUR_WEBSITE_NAME",
      "gcm_sender_id": "GCM_Sender_Id"
 }
```
    {: codeblock}
 
En el navegador Mozilla Firefox, añada los valores siguientes al archivo `manifest.json`.     Cambie `name` por el nombre de su sitio.

```
{
  "name": "YOUR_WEBSITE_NAME"
 }
```
    {: codeblock}

2. Cambie el nombre del archivo `manifest_Website.json` a `manifest.json`.
3. Añada `BMSPushSDK.js`, `BMSPushServiceWorker.js` y `manifest.json` al directorio raíz.
3. Incluya `manifest.json` en la etiqueta `<head>` del archivo html.
```
 <link rel="manifest" href="manifest.json">
```
    {: codeblock}
4. Incluya el SDK Push Web de Bluemix a la aplicación web desde GitHub.
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
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Registro de la aplicación web
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
  - **Carga útil adicional**: permite especificar valores personalizados de carga útil para las notificaciones.

En la imagen siguiente se muestra la opción de notificaciones web en el panel de control.

  ![pantalla Notificaciones](images/DashboardWebpush.jpg)
  
## Pasos siguientes
  {: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede configurar las notificaciones basadas en código y las opciones avanzadas.

Añada estas características del servicio {{site.data.keyword.mobilepushshort}} a la aplicación. Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html). Para utilizar opciones de notificaciones avanzadas, consulte [Notificaciones avanzadas](t_advance_badge_sound_payload.html).



