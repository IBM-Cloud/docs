---

copyright:
 years: 2015, 2016

---

# Habilitación de notificaciones
{: #c_enable_push-notifications}
Última actualización: 16 de agosto de 2016
{: .last-updated}

Puede habilitar aplicaciones para recibir y enviar notificaciones push a sus dispositivos.

Esta sección describe cómo habilitar las aplicaciones móviles para recibir notificaciones push, cómo crear notificaciones básicas, cómo obtener e inicializar el SDK o el plug-in, y cómo registrar el dispositivo para recibir notificaciones push. También puede habilitar las aplicaciones móviles para recibir notificaciones push utilizando la [API REST](t_restapi.html).

Nota: Para los registros de dispositivos con push, el servicio {{site.data.keyword.mobilepushshort}} mantiene una referencia exclusiva para las señales emitidas a partir de proveedores de notificaciones: APNs para Apple y GCM para Google. Las señales las puede invalidar el proveedor de notificación del servicio {{site.data.keyword.mobilepushshort}} por diversos motivos. 

Por ejemplo, durante la desinstalación de una aplicación en el dispositivo. En tal caso, cuando se intenta entregar una notificación en función de la respuesta de los proveedores que ha invalidado el dispositivo, el servicio {{site.data.keyword.mobilepushshort}} eliminará los registros de dispositivos. Esto a su vez podría restringir los intentos consecuentes al enviar notificación a los dispositivos invalidados.
