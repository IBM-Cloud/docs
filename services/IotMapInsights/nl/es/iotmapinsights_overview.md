---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Acerca de {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}
Última actualización: 20 de julio de 2016
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} es un servicio de {{site.data.keyword.Bluemix_notm}} que permite obtener acceso rápido a datos estáticos de redes viales y a datos de sucesos dinámicos. {{site.data.keyword.iotmapinsights_short}} además proporciona herramientas geoespaciales para las redes viales, que se pueden utilizar para integrar prestaciones geoespaciales en las aplicaciones.
{:shortdesc}

El servicio {{site.data.keyword.iotmapinsights_short}} proporciona las siguientes características:

- Datos de mapas estáticos
- Datos de sucesos dinámicos
- Herramientas geoespaciales

El servicio {{site.data.keyword.iotmapinsights_short}} recopila y utiliza datos de redes viales de [OpenStreetMap](http://www.openstreetmap.org/){: new_window} almacenados en la memoria caché del servicio para su procesamiento. 

Los datos de OpenStreetMap son disponibles de acuerdo con la licencia abierta de base de datos (ODbL) de Open Data Common de OpenStreetMap Foundation (OSMF). Para obtener más información, consulte [Derechos de autor y licencia de OpenStreetMap](http://www.openstreetmap.org/copyright){: new_window}.

## Datos de mapas estáticos
{: #static_map_data_query}

Una de las características clave del producto es la capacidad para recuperar información vial detallada para su uso en aplicaciones. Utilice la interfaz de API REST de Link Query para consultar datos estáticos de atributos viales de mapas mediante el ID de enlace. Utilice la función de [coincidencia de mapa](#map_matching) de {{site.data.keyword.iotmapinsights_short}} para identificar el parámetro de ID de enlace  necesario.

Los datos devueltos incluyen la información siguiente sobre el ID de enlace solicitado:

- Tipo de carretera
- Longitud de carretera
- Una matriz de puntos de forma detallada
- Información sobre enlaces y nodos adyacentes

Al consultar la información detallada de enlace vial, la aplicación puede atravesar una red de enlaces viales utilizando la información de enlace adyacente que se devuelve.

## Datos de sucesos dinámicos
{: #dynamic_event_data}

Además de los datos de mapas estáticos, la condición real de las carreteras incluye necesariamente sucesos dinámicos, como los atascos y las obras. Utilice {{site.data.keyword.iotmapinsights_short}} para crear, gestionar e incorporar sucesos de tráfico con [búsquedas de enlaces afectados](#link_search) para la planificación de rutas.

### Inyección y supresión de sucesos
{: #inject_event}

Utilice la API REST de inyección de sucesos de servicio {{site.data.keyword.iotmapinsights_short}} para inyectar y eliminar de forma dinámica sucesos de tráfico en forma de modelos de objeto de mapa que se colocan en enlaces viales específicos. Cada suceso incluye atributos básicos como las coordenadas GPS, la hora de inicio, el tipo de suceso, la duración del suceso y la longitud de carretera afectada. 

Utilice la interfaz de API REST de supresión de sucesos para eliminar sucesos del mapa cuando estén obsoletos. 

### Consulta de sucesos
{: #query_event}

Utilice la API REST de consulta de sucesos para obtener información detallada sobre todos los sucesos dinámicos en un área geográfica concreta. Puede consultar por área con un rango de longitud y latitud, así como incluir atributos de suceso para reducir el número de sucesos de destino que se devuelven. 

## Herramientas geoespaciales
{: #geospatial_tools}

Amplíe la aplicación con las funciones de búsqueda de rutas y coincidencia de mapa que proporcionan las herramientas geoespaciales de {{site.data.keyword.iotmapinsights_short}}.

### Coincidencia de mapa
{: #map_matching}

Utilice la interfaz de API REST de coincidencia de mapa con la aplicación para correlacionar coordenadas GPS reales del dispositivo con los datos de redes viales de [OpenStreetMap](http://www.openstreetmap.org/){: new_window} para aumentar la precisión de la ubicación en el caso de datos de GPS poco precisos. También puede recibir información sobre atributos viales según la ubicación. La API REST de coincidencia de mapa permite a la aplicación ajustar el punto de datos GPS en bruto a un punto coincidente en el enlace vial. 

La interfaz de la API REST de coincidencia de mapa recibirá un punto de datos de coordenadas GPS de longitud y latitud y devolverá un punto de coincidencia de mapa. El punto de coincidencia de mapa se analizará teniendo en cuenta los datos históricos de cada vehículo dentro del periodo de tiempo específico para encontrar el punto más probable en tiempo real. Para puntos que no tienen datos de ubicación históricos, la interfaz de coincidencia de mapa devuelve el punto más cercano en el enlace vial del punto GPS solicitado.

### Búsqueda de ruta
{: #route_search}

Una de las características básicas de una aplicación con funciones geoespaciales es la capacidad para encontrar la ruta más corta entre dos puntos.   

La interfaz de la API REST de búsqueda de ruta del servicio {{site.data.keyword.iotmapinsights_short}} calcula la ruta más corta entre las coordenadas GPS de punto inicial y final. Las coordenadas recibidas se hacen coincidir con el enlace más próximo del mapa utilizando la función de coincidencia de mapa, y se calculará la ruta más corta entre estos puntos de coincidencia de mapa.

### Búsqueda de enlaces afectada
{: #link_search}

Cuando se dé un suceso en una carretera, puede afectar a varios enlaces viales. Puede utilizar las API REST para buscar enlaces afectados y también para buscar enlaces viales donde los vehículos puedan llegar al suceso. La búsqueda tiene en cuenta la topología de la red de enlace vial, no solo la distancia de los vehículos al suceso.
