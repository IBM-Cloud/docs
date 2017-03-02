---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Panel de control de administración de servicios
{: #service-dashboard}


Puede ver el estado de la instancia del servicio {{site.data.keyword.geospatialshort_Geospatial}} y detenerla o reiniciarla desde el panel de control de administración de servicios. Para acceder al panel de control de administración de servicios, pulse el mosaico {{site.data.keyword.geospatialshort_Geospatial}} en el panel de control de {{site.data.keyword.geospatialshort_Geospatial}}. Si utiliza la aplicación de ejemplo y la instancia de servicio alcanza el límite de sucesos y se detiene, puede reiniciar el servicio. Al detener el servicio se elimina el límite de sucesos. Continúa recibiendo sucesos hasta que detenga el servicio. El panel de control de administración de servicios también muestra el estado y estadísticas de la instancia de servicio.{:shortdesc}

##Comprobaciones de región de {{site.data.keyword.geospatialshort_Geospatial}}

{{site.data.keyword.geospatialshort_Geospatial}} supervisa los dispositivos móviles desde el Internet de las cosas. Cada dispositivo supervisado envía mensajes de dispositivo que contienen un identificador único junto con su posición actual, que comprende latitud y longitud. La posición del dispositivo se contrasta con las coordenadas de cada región geográfica definida. A continuación, el servicio genera sucesos cuando los dispositivos entran, salen o están "bloqueados" en una región específica.

Una Comprobación de región se utiliza como unidad para medir el uso del servicio de {{site.data.keyword.geospatialfull}}. Para cada mensaje de dispositivo, se realiza una comprobación de región si se ha especificado la detección de entrada, salida o ambas para la región. Para cada mensaje de dispositivo, se realiza una comprobación de región si se ha especificado la detección de bloqueo para la región.
Si no se ha definido ninguna región, una comprobación de región se cuenta como si hubiera 1 región. Esto significa que si tiene 100 regiones definidas para la comprobación de entrada, salida y bloqueo, un solo mensaje de dispositivo produciría 200 comprobaciones de región.
