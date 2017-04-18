---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Iniciación a {{site.data.keyword.iotmapinsights_short}}
{: #iotdriverinsights_index}
Última actualización: 22 de junio de 2016
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} es un servicio de {{site.data.keyword.Bluemix}} que permite habilitar funciones geoespaciales, como la coincidencia de mapa y la búsqueda de la ruta más corta para redes viales de todo el mundo, en las aplicaciones.   
{:shortdesc}

Las características siguientes están disponibles mediante la API REST de {{site.data.keyword.iotmapinsights_short}}:

|Característica|Se utiliza para...|
|:---|:---|
|Coincidencia de mapas muy precisa|Hacer coincidir su ubicación de GPS con la red vial correlacionada|
|Recuperación de datos de geometría vial|Recuperar la red vial correlacionada para dibujar formas viales en un mapa|
|Búsqueda dinámica de la ruta más corta|Buscar la ruta más corta que incorpore sucesos en tiempo real como el tráfico|
|Manipulación de sucesos de tráfico en tiempo real|Añadir sucesos de coincidencia de mapa en tiempo real; por ejemplo, condiciones de tráfico para mejorar los resultados de la planificación de ruta|

## Antes de empezar
{: #byb}

1. Cuando añada una instancia del servicio desde el [catálogo de {{site.data.keyword.Bluemix_notm}}](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}, asegúrese de que no esté vinculada a una aplicación y anote los valores de ID de arrendamiento, nombre de usuario y contraseña generados automáticamente. Necesitará estos valores más adelante para acceder al servicio a través de la API de {{site.data.keyword.iotmapinsights_short}}.

2. Familiarícese con [OpenStreetMap](http://www.openstreetmap.org/){: new_window}.  

 El servicio {{site.data.keyword.iotmapinsights_short}} utiliza datos de redes viales, en coordenadas WGS84, que se extraen de [OpenStreetMap](http://www.openstreetmap.org/){: new_window}. Solo se utilizan las carreteras en las que puede circular un vehículo.  

 Se admiten las siguientes regiones de mapa:

|Región|ID de mapa|
|:---|:---|
|Europa|map_id=1|
|África|map_id=2|
|Asia|map_id=3|
|Australia y Oceanía|map_id=4|
|América del Norte|map_id=5|
|América Central|map_id=6|
|América del Sur|map_id=7|

## Coincidencia de mapa
{: #map_matching}
Para correlacionar coordenadas GPS en bruto con coordenadas de coincidencia de mapa, efectúe los pasos siguientes:

1. Prepare un conjunto de coordenadas GPS en bruto que se analizarán.
2. Envíe las coordenadas GPS en bruto con el mandato de API `mapMatching`. Opcionalmente, configure un ángulo de cabecera de cada posición en grados para especificar la dirección del viaje.
 - Solicitud: datos GPS en bruto
 - Respuesta: datos GPS de coincidencia de mapa, ID de enlace
3. Opcional: obtenga los datos de tipo de carretera con el mandato de API `getLinkInformation`. Puede recuperar los datos de forma de carretera coincidentes como una serie de coordenadas con la API REST `getLinkInformation`. 
 - Solicitud: ID de enlace
 - Respuesta: tipo de carretera

## Búsqueda de rutas
{: #route_searching}

Encuentre la información de ruta más corta entre las coordenadas de origen y destino especificadas con los pasos siguientes:

1. Determine una posición inicial y final para obtener la ruta más corta. 
2. Envíe las coordenadas iniciales y finales con la API REST `routeSearch`.
Opcionalmente, configure un ángulo de cabecera de cada posición, en grados, para especificar la dirección del viaje. 
 - Solicitud: coordenadas de origen y destino
 - Respuesta: ruta más corta de coincidencia de mapa

Utilice los datos de forma del enlace devuelto para dibujar la forma de la ruta encontrada en un mapa.

## Adición de sucesos de tráfico
{: #traffic_events}

Para añadir información de sucesos de tráfico al servicio {{site.data.keyword.iotmapinsights_short}}, efectúe los pasos siguientes:

1. Elija el tipo y la posición del suceso de tráfico que desee crear.
2. Inyecte el suceso utilizando el mandato de API `createEvent`.
Envíe la información de sucesos de tráfico al servicio {{site.data.keyword.iotmapinsights_short}}.
 - Solicitud: información de suceso
 - Respuesta: ID de suceso
3. Encuentre sucesos utilizando el mandato de API REST `queryEvent`.
Busque los sucesos de tráfico dentro de un área rectangular específica y, opcionalmente, un tipo de suceso de tráfico específico. 
 - Solicitud: información de área
 - Respuesta: información de sucesos  
4. Opcional: elimine un suceso de tráfico que ya no sea válido utilizando el mandato de API `deleteEvent`.
5. Opcional: recupere un área de la carretera que esté afectada por un suceso de tráfico mediante el mandato de API `getAffectedLinksInformation`. 

# Enlaces relacionados
{: #rellinks}

## Tutoriales y ejemplos
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Tutorial Part1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Tutorial Part2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [Aplicación de inicio de IoT for Automotive](https://iot-automotive-starter.mybluemix.net){:new_window}

## Referencia de la API
{: #api}

* [Documentos de API](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## Enlaces relacionados
{: #general}

* [Iniciación a {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Iniciación a {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Respuestas dW en IBM developerWorks](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Desbordamiento de la pila](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [Novedades en Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}
* [&copy;Contribuidores de OpenStreetMap](http://www.openstreetmap.org/copyright){:new_window}
* [Licencia abierta de base de datos (ODbL) de Open Data Commons](http://opendatacommons.org/licenses/odbl/){:new_window}
