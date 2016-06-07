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
{: #gettingstartedtemplate}
*Última actualización: 13 de mayo de 2016*

{{site.data.keyword.iotmapinsights_full}} facilita a los desarrolladores habilitar sus aplicaciones para utilizar funciones geoespaciales como la búsqueda de coincidencia de mapas y la ruta más corta en función de las redes viales de todo el mundo.
{:shortdesc}

Puede utilizar las siguientes funciones mediante la API REST de {{site.data.keyword.iotmapinsights_short}}:

- Coincidencia de mapas muy precisa que utiliza la geometría de la red vial.
- Manipulación de sucesos en tiempo real en un mapa, como el tráfico.
- Búsqueda de ruta más corta dinámica (búsqueda de rutas) teniendo en cuenta sucesos en tiempo real, como el tráfico.
- Recuperación de los datos de geometría vial que se pueden utilizar para dibujar formas viales en un mapa.

El servicio de {{site.data.keyword.iotmapinsights_short}} utiliza los datos de la red vial, en coordenadas WGS84, que se extraen desde OpenStreetMap. Solo se utilizan las carreteras en las que puede viajar un vehículo para el análisis.

Las regiones de mapa soportadas son:

- Europa (map_id=1)
- África (map_id=2)
- Asia (map_id=3)
- Australia y Oceanía (map_id=4)
- América del Norte (map_id=5)
- América Central (map_id=6)
- América del Sur (map_id=7)


Siga estos pasos para utilizar las funciones de análisis del servicio de {{site.data.keyword.iotmapinsights_short}}.

## Uso de {{site.data.keyword.iotmapinsights_short}} para la coincidencia de mapas

1. Prepare un conjunto de datos de coordenadas GPS en bruto que se analizarán.
2. Envíe los datos de coordenadas GPS en bruto en orden de serie temporal al servicio de {{site.data.keyword.iotmapinsights_short}} utilizando la API REST de `mapMatching`. Opcionalmente, configure un ángulo de cabecera de cada posición en grados (el Norte es 0, en ángulo en sentido de las agujas del reloj) para especificar la dirección del viaje.
3. Reciba la información de coordenadas de coincidencia de mapas y de enlace de carreteras en respuesta a la invocación de la API REST `mapMatching`.
4. Opcionalmente, recupere los datos de forma de la carretera del enlace de la carretera coincidente de mapas utilizando la API REST `getLinkInformation`. Invoque a la API REST `getLinkInformation` con un ID de enlace para obtener una serie de coordenadas que constan de una forma de carretera.

## Uso de {{site.data.keyword.iotmapinsights_short}} para la búsqueda de rutas

1. Determine una posición de inicio y de fin para la que desea obtener un ruta más corta.
2. Envíe las coordenadas de inicio y de fin al servicio de {{site.data.keyword.iotmapinsights_short}} mediante la API REST `routeSearch`. Opcionalmente, configure un ángulo de cabecera de cada posición en grados (el Norte es 0, en ángulo en sentido de las agujas del reloj) para especificar la dirección del viaje.
3. Reciba una lista de enlaces viales en respuesta a la invocación de la API REST de `routeSearch`. Puede dibujar la forma de la ruta encontrada en un mapa mediante los datos de forma incluidos en los datos de resultado.

## Uso de {{site.data.keyword.iotmapinsights_short}} para la manipulación de sucesos de tráfico

1. Determine un tipo y una posición de un suceso de tráfico que desea crear.
2. Envíe la información de sucesos de tráfico al servicio de {{site.data.keyword.iotmapinsights_short}} mediante la API REST `createEvent`.
3. Reciba un ID de suceso del suceso de tráfico creado en respuesta a la invocación de la API REST `createEvent`.
4. Busque los sucesos de tráfico dentro de un área rectangular específica y, opcionalmente, con un tipo de suceso de tráfico específico, mediante la API REST `queryEvent`.

- Opcionalmente, elimine un suceso de tráfico que ya no sea válido mediante la API REST `deleteEvent`.
- Opcionalmente, recupere un área en la carretera que esté afectada por un suceso de tráfico mediante la API REST `getAffectedLinksInformation`.


# Enlaces relacionados
{: #rellinks}
## Tutoriales y ejemplos
{: #samples}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Tutorial Part1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Tutorial Part2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

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

