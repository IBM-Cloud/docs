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

El servicio de {{site.data.keyword.iotmapinsights_short}} se basa en datos de red vial almacenados en la memoria caché. El servicio proporciona acceso de alta velocidad a datos de red vial estáticos, datos de sucesos dinámicos y herramientas geoespaciales basadas en la red vial, lo que permite a su aplicación integrar prestaciones geoespaciales.
{:shortdesc}

## Consulta de datos de mapas estáticos
{: #static_map_data_query}

Para acceder a los datos de atributos de enlaces viales, el servicio de {{site.data.keyword.iotmapinsights_short}} proporciona una interfaz de API REST de Link Query. La interfaz recibe un ID de enlace como un parámetro que se puede identificar mediante una función de coincidencia de mapas, y devuelve información detallada para el enlace solicitado, como por ejemplo el tipo de carretera, la longitud, la matriz de puntos de forma de detalle, los nodos adyacentes y los enlaces adyacentes. Al utilizar la información de enlace de detalles consultados, la aplicación puede atravesar una red de enlace de carreteras observando la información de enlace adyacente.

## Datos de sucesos dinámicos
{: #dynamic_event_data}

Un suceso del servicio de {{site.data.keyword.iotmapinsights_short}} es un modelo de objetos para un suceso de tráfico que se coloca de forma dinámica en un enlace a carretera específico. El suceso tiene atributos básicos de un suceso de tráfico, como por ejemplo coordenadas GPS, la hora, el tipo, la duración del suceso y la longitud afectada. Puede inyectar y suprimir sucesos de forma dinámica.

## Inyección y supresión de sucesos
{: #inject_event}

Con la interfaz de API REST de inyección de sucesos, puede almacenar un suceso en un mapa. Para inyectar un suceso, puede publicar la información de sucesos en la interfaz con un tipo de sucesos definido para clasificar sucesos y sus atributos según el uso que se pretende de la aplicación. Con la interfaz de la API REST de la supresión de sucesos, puede eliminar sucesos del mapa para que se puedan gestionar los sucesos obsoletos.

## Consulta de sucesos
{: #query_event}

Con la interfaz de la API REST de la consulta de sucesos, puede consultar sucesos en condiciones específicas que se establecen como parámetros de consulta. Para una condición de consulta, puede establecer el área con un rango de longitud y de latitud, y los atributos de sucesos para reducir los sucesos de destino devueltos como respuesta de la solicitud.

## Herramientas geoespaciales
{: #geospatial_tools}

Para las herramientas geoespaciales, el servicio de {{site.data.keyword.iotmapinsights_short}} proporciona una interfaz de API REST para las funciones de coincidencia de mapa y de búsqueda de ruta.

## Coincidencia de mapa
{: #map_matching}

Si los datos GPS de los dispositivos no son lo suficientemente precisos como para utilizar el análisis o la visualización, o si los atributos de la red de enlace vial son obligatorios para la aplicación, puede utilizar la interfaz de la API REST de coincidencia de mapa. La API REST de coincidencia de mapa permite a la app ajustar el punto de datos GPS en bruto a un punto coincidente en el enlace vial. La interfaz de la API REST de coincidencia de mapa recibirá un punto de datos de coordenadas GPS de longitud y latitud y devolverá un punto de coincidencia de mapa. Este punto se analizará teniendo en cuenta los datos históricos para cada vehículo dentro del periodo de tiempo específico para encontrar el punto más probable en tiempo real. Para el punto que no tiene datos de ubicación históricos, la interfaz de coincidencia de mapa devuelve el punto más cercano en el enlace vial del punto GPS solicitado.

## Búsqueda de ruta
{: #route_search}

Si necesita implementar una aplicación con funciones geoespaciales, necesitará buscar la ruta más corta entre dos puntos. La interfaz de la API REST de la búsqueda de ruta del servicio de {{site.data.keyword.iotmapinsights_short}} calcula la ruta más corta entre las coordenadas GPS de punto de inicio y punto final. Las coordenadas recibidas se hacen coincidir con el enlace más próximo del mapa utilizando la función de coincidencia de mapa, y se calculará la ruta más corta entre estos puntos de coincidencia de mapa.

## Búsqueda de enlaces afectada
{: #link_search}

Cuando se dé un suceso en una carretera, puede afectar a varios enlaces viales. Puede utilizar API REST para buscar enlaces afectados y para buscar enlaces viales donde los vehículos puedan llegar al suceso. La búsqueda tiene en cuenta la topología de la red de enlace vial, no solo la distancia de los vehículos al suceso.

