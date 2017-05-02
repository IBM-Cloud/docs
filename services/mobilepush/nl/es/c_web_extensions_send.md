---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Envío de notificaciones básicas a apps y extensiones de Chrome 
{: #web_extensions_notifications}
Última actualización: 11 de enero de 2017
{: .last-updated}

Una vez que haya desarrollado sus aplicaciones, puede enviar una notificación push. 

1. Seleccione **Enviar notificaciones** y para redactar un mensaje seleccione **Notificaciones web** como opción **Enviar a**. 
2. Escriba el mensaje en el campo **Mensaje**.
3. Puede elegir que se proporcionen valores opcionales:
  - **Título de notificación**: es el texto que se visualizará como mensaje en la cabecera de la alerta de mensaje.
  - **URL de icono de notificación**: si el mensaje debe entregarse con un icono de notificación de la app, indique el enlace al icono en este campo.
  - **Contraer clave**: las claves contraídas se adjuntan a las notificaciones. Si llegan varias notificaciones de forma secuencias con la misma clave contraída cuando el dispositivo está desconectado, estas se contraerán. Cuando el dispositivo vuelva a conectarse, recibirá las notificaciones del servidor FCM/GCM y mostrará solo la última notificación transportada con la misma clave contraída. Si no se establece esta clave contraída, se almacenarán los mensajes nuevos y antiguos para entregarlos más adelante.
  - **Tiempo de duración**: este valor se establece en segundos. Si no se especifica este parámetro, el servidor FCM/GCM almacenará el mensaje cuatro semanas e intentará entregarlo. La validez caduca transcurridas cuatro semanas. El intervalo de valores posible es de 0 a 2.419.200 segundos.
  - **Retrasar cuando esté desocupado**: si se define como `true`, el servidor FCM/GCM no entregará la notificación cuando el dispositivo esté desocupado. Establezca este valor en `false` para garantizar que se entregan notificaciones aunque el dispositivo esté desocupado.
  - **Carga útil adicional**: permite especificar valores personalizados de carga útil para las notificaciones.

En la imagen siguiente se muestra la opción de notificaciones de apps y extensiones Chrome en el panel de control.

  ![pantalla Notificaciones](images/push_chrome_extns.jpg)
  
## Pasos siguientes
  {: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede optar por configurar las notificaciones basadas en código y las opciones avanzadas.

Añada estas características del servicio {{site.data.keyword.mobilepushshort}} a su app.
Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html). Para utilizar opciones de notificaciones avanzadas, consulte [Notificaciones avanzadas](t_advance_badge_sound_payload.html).
