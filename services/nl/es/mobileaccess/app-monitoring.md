---

copyright:
  años: 2015, 2016
  
---

# Supervisión de la aplicación
{: #app-monitoring}

Además de las características de seguridad, {{site.data.keyword.amafull}} también ofrece capacidades de supervisión y análisis para aplicaciones móviles. Puede grabar registros de clientes y supervisar datos con el SDK del cliente de {{site.data.keyword.amashort}}. Los desarrolladores pueden controlar cuándo se envían estos datos al servicio de {{site.data.keyword.amashort}}. Todos los sucesos de seguridad, como un error de autenticación o una autenticación correcta, que se produce en el servicio de {{site.data.keyword.amashort}} se registran automáticamente.

Cuando se entregan los datos a {{site.data.keyword.amashort}}, puede utilizar el panel de control de supervisión de {{site.data.keyword.amashort}} para obtener información de analíticas sobre aplicaciones móviles, dispositivos y registros de clientes. La información sobre las solicitudes que efectúa la aplicación en los recursos protegidos por {{site.data.keyword.amashort}} queda registrada de forma predeterminada.

Los datos registrados automáticamente incluyen información como el número de autenticaciones, los dispositivos nuevos y los usuarios nuevos. Además puede configurar el SDK del cliente de {{site.data.keyword.amashort}} para que notifica la información siguiente:

### Estadísticas de uso de las aplicaciones móviles
{: #usage-stats}

Puede configurar las aplicaciones móviles para que registren sucesos del ciclo de vida de la aplicación y para que envíen estos datos al servicio de {{site.data.keyword.amashort}} con unas sencillas llamadas de API. Puede registrar el número de apps abiertas, notificaciones push recibidas, etc.

### Capturas de registros del lado de cliente
{: #client-side-logcapture}

Las aplicaciones en capo pueden, de manera ocasional, experimentar problemas que necesiten la atención de un desarrollador para ser solucionados. No obstante, muchas veces es difícil reproducir esos problemas. <!--in R&D.--> Los desarrolladores que trabajaron en el código pueden carecer del entorno del dispositivo exacto para realizar las pruebas. En estas situaciones, es útil poder recuperar los registros de depuración de los dispositivos cliente en el entorno en el que ocurren los problemas.

## Conservación de los datos capturados
{: #preserve-captureddata}

No es posible garantizar la conservación de todos los datos capturados en el lado del cliente. Es posible que los usuarios estén ejecutando la aplicación móvil fuera de línea y que, a la vez, estén acumulando datos de análisis y de registro capturados. Como el cliente está fuera de línea con un espacio de sistema de archivos limitado, se conservarán los sucesos de anotaciones más recientes en detrimento de los más antiguos. El desarrollador debe decidir cuándo se envían los datos capturados al servicio de {{site.data.keyword.amashort}} utilizando las API proporcionadas.

## Utilización del panel de control de supervisión de {{site.data.keyword.amashort}}
{: #monitoring-dashboard}

1. Abra el panel de control de {{site.data.keyword.Bluemix}} y pulse la aplicación de {{site.data.keyword.Bluemix_notm}}.

2. Cuando se abra el panel de control de la aplicación de {{site.data.keyword.Bluemix_notm}}, pulse en un mosaico de {{site.data.keyword.amashort}}.

3. En el panel de control de {{site.data.keyword.amashort}},haga clic en el enlace `Supervisión` del menú de la izquierda.

## Próximos pasos
{: #next-steps}
* [Habilitación, configuración y uso del registrador](app-monitoring-logger.html)
* [Recopilación de analíticas de uso](app-monitoring-gathering-analytics.html)
