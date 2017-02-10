---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Habilitación de notificaciones para dispositivos móviles
{: #c_enable_push-notifications}
Última actualización: 18 de enero de 2017
{: .last-updated}

Asegúrese de haber [configurado credenciales para un proveedor de notificaciones](t__main_push_config_provider.html).

Esta sección describe cómo habilitar las aplicaciones cliente (aplicaciones móviles y de navegador web y también aplicaciones y extensiones de Chrome) para recibir notificaciones push, cómo crear notificaciones básicas, cómo obtener e inicializar el SDK o el plug-in, y cómo registrar el dispositivo o navegador para recibir notificaciones push. También puede habilitar las aplicaciones móviles y de navegador web para recibir notificaciones push utilizando la [API REST](t_restapi.html).

**Nota**: Para los registros de extensiones y aplicaciones de navegador o dispositivo Chrome, el servicio {{site.data.keyword.mobilepushshort}} mantiene una referencia única a las señales emitidas a partir de proveedores de notificaciones -
APN para Apple o FCM para Google. Las señales las puede invalidar el proveedor de notificación del servicio {{site.data.keyword.mobilepushshort}} por diversos motivos. 

Por ejemplo, durante la desinstalación de una app en el dispositivo. En tal caso, cuando se intenta entregar una notificación en función de la respuesta de los proveedores que ha invalidado el dispositivo, el servicio {{site.data.keyword.mobilepushshort}} eliminará los registros de dispositivos o navegadores web. Esto a su vez podría restringir los intentos consecuentes al enviar notificación a los dispositivos invalidados.
