---

copyright:
  año: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Acerca de Trajectory Pattern Analysis
{: #tp_iotdriverinsights_overview}
Última actualización: 16 de junio de 2016
{: .last-updated}

La API de Trajectory Pattern Analysis es un servicio proporcionado por {{site.data.keyword.iotdriverinsights_full}} que se puede utilizar para analizar los patrones de rutas y de Origen/Destino (O/D) de trayectos de conducción a partir de datos de sondeo de coche.

{:shortdesc}

## Análisis de patrones de trayectorias de rutas
{: #tpa}

Puede identificar y analizar patrones de rutas y de O/D de varias trayectorias
El siguiente diagrama muestra un ejemplo simple de patrones de rutas y de O/D de un vehículo (vehículo-1) obtenidos de varios trayectos. En este ejemplo, Trajectory Pattern Analysis identifica dos patrones de O/D: 
- Un patrón de O/D desde la casa (Origen1) a la oficina (Destino1) que tiene dos patrones de ruta
- Un patrón de O/D desde la casa (Origen1) a la tienda (Destino2) que tiene un patrón de ruta. 

![Ejemplo de ruta de O/D](images/tp_odroute_example.png "Ejemplo de patrón de O/D y ruta")

Trajectory Pattern Analysis también calcula algunas métricas de diversidad de conducción para cada vehículo tal como se listan en la siguiente tabla. Puede utilizar estas métricas para juzgar las características de conducción de un conductor.

|Nombre de métrica|Descripción|
|:---|:---|
|Proporción de O/D inusual|La proporción del número de trayectos que no están cubiertos por patrones de O/D y el número total de trayectorias de entrada. |
|Proporción de kilometraje inusual|La proporción del kilometraje que no está cubierta por patrones de rutas y el kilometraje total de trayectorias de entrada. |
|Proporción de trayectorias inusuales|La proporción del número de trayectorias que no están cubiertas por patrones de rutas y el número total de trayectorias de entrada.|


## API de REST
{: #rest_api}

La API REST de Trajectory Pattern Analysis proporciona solicitudes que se pueden utilizar para personalizar y compilar las aplicaciones de {{site.data.keyword.Bluemix_notm}}:

 1. Mandatos de datos de coche:
   - `sendCarProbeData` envía los datos de sondeo del coche que deben analizarse
   - `getCarProbeDataListAsDate` devuelve la lista de datos de sondeo del coche por fecha
   - `deleteCarProbeDataListByDate` elimina los datos de sondeo del coche
 2. Mandatos de trabajo de análisis:
   - `sendJobRequest` envía la solicitud de trabajo de análisis de patrones de trayectorias
   - `getJobInfo` devuelve la información del trabajo especificado
   - `getJobInfoList` devuelve la lista de información de trabajo
 3. Mandatos de resultados del análisis:
   - `getResultSummary` devuelve la información de resumen analizada del análisis de patrones de trayectorias
   - `getAnalyzedODDetail` devuelve información detallada del patrón de O/D analizados especificado
   - `getRouteGPSList` devuelve la lista de información GPS del patrón de rutasanalizas especificado
   - `getODList` devuelve la lista de información de patrón de O/D de los argumentos especificados
   - `deleteJobResult` suprime todos los resultados analizados relacionados con un trabajo

Para obtener más información, consulte la documentación de la [API de {{site.data.keyword.iotdriverinsights_short}}](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}.
