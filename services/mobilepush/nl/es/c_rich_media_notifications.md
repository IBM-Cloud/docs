---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Habilitación de notificaciones Rich Media
{: #interactive-notifications}
Última actualización: 11 de enero de 2017
{: .last-updated}


Puede habilitar Rich Media {{site.data.keyword.mobilepushshort}} en iOS 10 y posteriores. Las notificaciones push se pueden enviar con audio, vídeo, GIF e imágenes. 

Para configurar la aplicación de modo que reciba push completo en iOS 10, siga estos pasos:  

1. En Xcode, seleccione **File** > **Nuevo** > **Destino** > **Extensión de servicio de notificación**.
2. En el método `didReceive()` de `UNNotificationServiceExtension`, añada el siguiente código.
```
BMSPushRichPushNotificationOptions.didReceive(request, withContentHandler: contentHandler)
```
	
Para enviar Rich Media {{site.data.keyword.mobilepushshort}} desde el panel de control de Push, asegúrese de especificar los campos de mensaje, título, subtítulo y attachmentURL.
