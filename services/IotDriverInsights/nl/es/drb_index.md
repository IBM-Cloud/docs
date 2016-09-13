---

copyright:
  año: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a Driving Behavior Analysis
{: #drb_index}
Última actualización: 16 de junio de 2016
{: .last-updated}

Driving Behavior Analysis es un servicio dentro del servicio {{site.data.keyword.iotdriverinsights_full}} de {{site.data.keyword.Bluemix_notm}}   que puede utilizar para recopilar y analizar el comportamiento de conductor a partir de los datos contextuales y de sondeo de coche. Además, puede utilizar la API de  {{site.data.keyword.iotdriverinsights_short}} para integrar los datos de comportamiento de conductor analizados en otras aplicaciones de {{site.data.keyword.Bluemix_notm}}.

{:shortdesc}

En el siguiente diagrama se muestra un esquema de una secuencia típica de llamadas de API en el servicio Driving Behavior Analysis: 

![Secuencia de análisis típica](images/sequence_diagram.png "Secuencia de análisis típica")

Después de crear y desplegar {{site.data.keyword.iotdriverinsights_short}} como una instancia de servicio desenlazado, lleve a cabo las siguientes tareas para integrar las aplicaciones con la API de {{site.data.keyword.iotdriverinsights_short}}.

También puede utilizar la guía de aprendizaje de [{{site.data.keyword.iotmapinsights_short}}y {{site.data.keyword.iotdriverinsights_short}}](https://github.com/IBM-Bluemix/car-data-management){:new_window} para ayudarle a crear una aplicación de ejemplo con datos de sondeo de coche de ejemplo. 


## Antes de empezar
{: #drb_byb}

- Revise el tema [Acerca de Driving Behavior Analysis](drb_iotdriverinsights_overview.html) para familiarizarse con los comportamientos y contextos analizables.

- Obtenga los valores *ID de arrendatario*, *Nombre de usuario* y *Contraseña*, que son necesarios para acceder a la API de {{site.data.keyword.iotdriverinsights_short}}.

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el mosaico del  servicio {{site.data.keyword.iotdriverinsights_short}}.
2. Seleccione la vista **Gestionar** de la instancia de servicio.
3. Anote los valores *ID de arrendatario*, *Nombre de usuario* y *Contraseña* que se visualizan.

- Opcional: si desea utilizar funciones geoespaciales con los datos de conductor, despliegue el servicio {{site.data.keyword.iotmapinsights_short}} {{site.data.keyword.Bluemix_notm}} en la organización.


## Tarea 1: Carga de datos de vehículo y contexto
{: #drb_task1}
Cargue uno o más conjuntos de datos de trayecto de conductor en el arrendatario de {{site.data.keyword.iotdriverinsights_short}} para que los datos del conductor estén disponibles para analizarlos. 

1. Opcional: si ha desplegado el servicio {{site.data.keyword.iotmapinsights_short}}, correlacione los datos de conductor con datos geoespaciales. Antes de que la aplicación envíe datos de sondeo a la [API de {{site.data.keyword.iotdriverinsights_short}} ](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}, puede correlacionarla con datos geoespaciales utilizando la [API de {{site.data.keyword.iotmapinsights_short}}](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}. Los datos geoespaciales mejoran la calidad de los resultados de comportamiento de conductor analizados.

     1. Obtenga datos de sondeo de coche coincidentes con la correlación utilizando la API `mapMatching`.
     La coincidencia de correlaciones correlaciona los datos de conducción de los datos de sondeo de coche con los datos de carretera geoespacial. 
        - Solicitud: Datos de sondeo de coche
        - Respuesta: Datos de sondeo de coche coincidentes con la correlación
     2. Obtenga datos de tipo de carretera con la API `getLinkInformation`.  
        - Solicitud: ID de enlace de carretera
        - Respuesta: Tipo de carretera
2. Envíe datos de sondeo de coche al almacén para analizarlos con la API `sendCarProbeData`.
Cargue sus datos de sondeo de coche sin procesar y datos geoespaciales coincidentes opcionales en {{site.data.keyword.iotdriverinsights_short}}.
   - Solicitud: Correlacione datos de sondeo de coche y tipo de carretera coincidentes

## Tarea 2: Proceso de datos de vehículo y contexto  
{: #drb_task2}
Procese los datos de vehículo y contexto comparándolos con los parámetros de análisis configurables. Para obtener información sobre cómo configurar los parámetros del análisis, consulte el tema [Configuración de parámetros para el servicio](drb_iotdriverinsights_admin.html#configureparameters).

1. Envíe una solicitud para analizar datos de sondeo de coche en un determinado periodo de tiempo con la API de `sendJobRequest`.
   - Solicitud: Fecha de y a
   - Respuesta: ID de trabajo
2. Compruebe el estado del trabajo con la API de `getJobInfo`.
El proceso de datos de comportamiento de conductor se ha completado cuando el estado de trabajo ha devuelto estados 'SUCCEEDED'. Ahora puede solicitar datos de comportamiento de conductor. 
   - Solicitud: ID de trabajo
   - Respuesta: Estado de trabajo

## Tarea 3: Analizar trayectos
{: #drb_task3}
Analice trayectos de un rango de fechas específico para comprender cómo ajustarse a los parámetros de umbral de análisis. 

1. Obtenga la lista de resumen de trayectos analizados con la API de `getAnalyzedTripSummaryList`.
Esta lista de resumen de trayectos incluye información de resumen de trayectos analizados según los parámetros de entrada.
   - Solicitud: ID de trabajo
   - Respuesta: Lista de resumen de trayectos analizados
2. Obtenga la información detallada de los trayectos analizados con la API de `getAnalyzedTripInfo`.
Por último, obtenga la información detallada de comportamiento de conductor para un trayecto analizado específico.
   - Solicitud: UUID del trayecto
   - Respuesta: Detalles del trayecto analizado

## Siguientes pasos
{: #drb_post}
Cuando haya completado los pasos, se genera un conjunto de datos de comportamiento de conductor en la organización. Utilice las aplicaciones o el software de análisis preferido para procesar la información más detalladamente en más datos empresariales significativos. 

# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Guía de aprendizaje - Parte 1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Guía de aprendizaje - Parte 2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [Aplicación de inicio de IoT for Automotive](https://iot-automotive-starter.mybluemix.net){:new_window}


## Referencia de API
{: #api}

* [Documentos de API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}

## Otros recursos
{: #general}

* [Iniciación a {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [Iniciación a {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Respuestas dW en IBM developerWorks](https://developer.ibm.com/answers/topics/iot-driver-behavior){:new_window}
* [Desbordamiento de pila](http://stackoverflow.com/questions/tagged/iot-driver-behavior){:new_window}
* [Novedades de los servicios Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
