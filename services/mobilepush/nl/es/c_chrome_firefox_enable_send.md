---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Envío de notificaciones básicas a navegadores web
{: #web_notifications}
Última actualización: 11 de enero de 2017
{: .last-updated}

Una vez que haya desarrollado sus aplicaciones, puede enviar una notificación push. 

1. Seleccione **Enviar notificaciones** y para redactar un mensaje seleccione **Notificaciones web** como opción **Enviar a**. 
2. Escriba el mensaje en el campo **Mensaje**.
3. Puede elegir que se proporcionen valores opcionales:
  - **Título de notificación**: es el texto que se visualizará como mensaje en la cabecera de la alerta de mensaje.
  - **URL de icono de notificación**: si el mensaje debe entregarse con un icono de notificación de la aplicación, indique el enlace al icono en este campo.
  - **Tiempo de duración**: Notifica al servidor sobre la validez de los mensajes.
4. Para notificaciones web enviadas al navegador Safari, hay alguna información adicional necesaria:
  - **Acción**: Esta es la etiqueta del botón de acción.
  - **Argumentos URL**: Los argumentos URL que necesitan utilizarse con esta notificación. Asegúrese de que se proporciona en la forma de una matriz JSON. 
 
En la imagen siguiente se muestra la opción de notificaciones web en el panel de control.

  ![pantalla Notificaciones](images/DashboardWebpush.jpg)


## Pasos siguientes
  {: #next_steps_tags}

Una vez que haya configurado correctamente las notificaciones básicas, puede optar por configurar las notificaciones basadas en código y las opciones avanzadas.

Añada las características de servicio de {{site.data.keyword.mobilepushshort}} a la app. Para utilizar notificaciones basadas en código, consulte [Notificaciones basadas en código](c_tag_basednotifications.html). Para utilizar opciones de notificaciones avanzadas, consulte [Notificaciones avanzadas](t_advance_badge_sound_payload.html).



