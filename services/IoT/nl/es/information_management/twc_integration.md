---

copyright:
years: 2016, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilice los datos de The Weather Company con los dispositivos
{: #weathercompany}

La integración de Weather Company le permite combinar los datos meteorológicos con los dispositivos existentes de {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

La información meteorológica de The Weather Company aparece en la vista de detalles del dispositivo si se ha realizado una solicitud Update Location mediante la API, o si el dispositivo ya ha establecido su ubicación mediante un mensaje de gestión de dispositivos.

**Importante:** Sólo los dispositivos gestionados pueden definir sus propias ubicaciones. Todos los dispositivos no gestionados deben tener sus ubicaciones establecidas manualmente mediante la API. Para obtener más información sobre cómo configurar una ubicación de dispositivo, consulte [Solicitudes Update Location](../../devices/device_mgmt/index.html#update-location).

## API REST para The Weather Company
Para acceder a la API REST para The Weather Company, consulte la sección sobre la extensión sobre Device Location Weather en la documentación de [{{site.data.keyword.iot_short_notm}} API REST HTTP ![icono de enlace externo](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window}.

## Visualización de datos meteorológicos

Para ver los datos meteorológicos recuperados para una ubicación de dispositivo:
1. Pulse sobre el dispositivo en el panel **Dispositivos**.
2. En la vista de dispositivos detallada, desplácese hacia abajo hasta la sección **Extensiones**.  
Se enumerarán los siguientes datos meteorológicos:
 - Información meteorológica actual.
 - Temperatura actual.
 - Temperatura máxima y mínima prevista.
 - Humedad relativa.
 - Presión.
 - Visibilidad.
 - Velocidad del viento.
 - Dirección del viento.
 - Latitud.
 - Longitud.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
