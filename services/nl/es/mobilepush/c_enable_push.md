---

copyright:
 years: 2015, 2016

---

# Habilitación de notificaciones
{: #c_enable_push-notifications}
*Última actualización: 14 de junio de 2016*
{: .last-updated}

Puede habilitar aplicaciones para recibir y enviar notificaciones push a sus dispositivos.

Esta sección describe cómo habilitar las aplicaciones móviles para recibir notificaciones push, cómo crear notificaciones básicas, cómo obtener e inicializar el SDK o el plug-in, y cómo registrar el dispositivo para recibir notificaciones push. También puede habilitar las aplicaciones móviles para recibir notificaciones push utilizando la [API REST](t_restapi.html).

Nota: Para los registros de dispositivos con push, el servicio de Notificaciones push mantiene una referencia exclusiva para las señales emitidas a partir de proveedores de notificaciones -
APNS for Apple o GCM for Google. Las señales las puede invalidar el proveedor de notificación de servicios Notificaciones push por diversos motivos. 

Por ejemplo, durante la desinstalación de la app en el dispositivo. En tal caso, cuando se intenta entregar una notificación en función de la respuesta de los proveedores que ha invalidado el dispositivo, el servicio de Notificaciones push eliminará los registros de dispositivos. Esto a su vez podría restringir los intentos consecuentes al enviar notificación a los dispositivos invalidados.
