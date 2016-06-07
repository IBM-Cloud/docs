---

copyright:
  año: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a {{site.data.keyword.iotdriverinsights_short}}
{: #gettingstartedtemplate}
*Última actualización: 13 de mayo de 2016*

Con {{site.data.keyword.iotdriverinsights_full}}, puede ejecutar un análisis del comportamiento de los conductores utilizando la API {{site.data.keyword.iotdriverinsights_short}} para recopilar y analizar datos de sondeo y datos contextuales del coche.
{:shortdesc}

Siga estos pasos para integrar la aplicación con la API {{site.data.keyword.iotdriverinsights_short}} después de crear y despegar una instancia de servicio de anulación de enlace.  

1. (Opcional) Antes de enviar los datos de sondeo del coche a la API {{site.data.keyword.iotdriverinsights_short}}, puede añadir datos adicionales mediante la API {{site.data.keyword.iotmapinsights_short}}.
     - Obtenga datos de sondeo de coche coincidentes con la correlación utilizando la API `mapMatching`. 
        - [Solicitud] Datos de sondeo de coche
        - [Respuesta] Datos de sondeo de coche coincidentes con la correlación
     - Obtenga el tipo de carretera utilizando la API `getLinkInformation`.
        - [Solicitud] ID de enlace de carretera
        - [Respuesta] Tipo de carretera
2. Envíe datos de sondeo de coche para almacenarlos y analizarlos mediante la API `sendCarProbe`. 
   - [Solicitud] Correlacione datos de sondeo de coche y tipo de carretera coincidentes
3. Envíe una solicitud de trabajo para analizar datos de sondeo de coche utilizando la API `sendJobRequest`. 
   - [Solicitud] Fecha de y a
   - [Respuesta] ID del trabajo
4. Compruebe el estado del trabajo utilizando la API `getJobInfo`.
   - [Solicitud] ID del trabajo
   - [Respuesta] Estado del trabajo
5. Obtenga la listad e resumen de viaje analizado utilizando la API `getAnalyzedTripSummaryList`. 
   - [Solicitud] ID del trabajo
   - [Respuesta] Lista de resumen del viaje analizado
6. Obtenga información detallada del análisis del viaje utilizando la API `getAnalyzedTripInfo`. 
   - [Solicitud] UUID del viaje
   - [Respuesta] Detalles del viaje analizado 

El siguiente diagrama de secuencia muestra la secuencia de pasos. 

![Secuencia de análisis típica](images/sequence_diagram.png "Secuencia de análisis típica")

Consulte el tema [Acerca de {{site.data.keyword.iotdriverinsights_short}}](iotdriverinsights_overview.html) para obtener información detallada sobre los comportamientos y contextos analizables.
Utilice [{{site.data.keyword.iotmapinsights_short}} / Guía de aprendizaje - Parte 1 de {{site.data.keyword.iotdriverinsights_short}}](https://github.com/IBM-Bluemix/car-data-management){:new_window} para probar una aplicación de ejemplo con datos de sondeo de coche de ejemplo. 


# Enlaces relacionados
{: #rellinks}
## Guías de aprendizaje y ejemplos
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Guía de aprendizaje - Parte 1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Guía de aprendizaje - Parte 2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

## Referencia de la API
{: #api}

* [Documentos de API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}

## Enlaces relacionados
{: #general}

* [Iniciación a {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [Iniciación a {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Respuestas dW en IBM developerWorks](https://developer.ibm.com/answers/topics/iot-driver-behavior){:new_window}
* [Desbordamiento de pila](http://stackoverflow.com/questions/tagged/iot-driver-behavior){:new_window}
* [Novedades de los servicios Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}

