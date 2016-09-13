---

copyright:
  año: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Acerca de Driving Behavior Analysis
{: #iotdriverinsights_overview}
Última actualización: 16 de junio de 2016
{: .last-updated}


Driving Behavior Analysis es un servicio que se puede utilizar para analizar el comportamiento de un conductor a partir de datos de sondeo de coche y contextuales.

{:shortdesc}


## Arquitectura
{: #drb}

Puede identificar y analizar varios tipos de comportamiento de conducción relacionados con la velocidad, los giros y otras categorías. Por ejemplo, puede determinar instancias de aceleración brusca, exceso de velocidad, giros bruscos, frenada frecuente o brusca, y otros tipos de comportamiento de conductor.

## Configuración de análisis
{: #configurability}  

Los parámetros de umbral de análisis determinan cómo se detectan y analizan los distintos tipos de comportamiento de conductor a partir de los datos de sondeo de coche y contextuales que se introducen en el sistema. Puede configurar algunos de los parámetros de umbral para el análisis del comportamiento de conducción desde la consola de administración de servicio {{site.data.keyword.iotdriverinsights_short}}. Por ejemplo, puede configurar el intervalo de velocidad por tipo de carretera y el intervalo de ángulo de giro. 

Para obtener más información sobre cómo configurar los parámetro de umbral para el análisis de Driving Behavior Analysis, consulte [Configuración de parámetros para el servicio](drb_iotdriverinsights_admin.html#configureparameters).

### Categorías y actividades de comportamiento de conducción

Las siguientes tablas listan los tipos de comportamientos de conducción por categoría que puede detectar y analizar el servicio: 

#### Tabla 1: Tipos de comportamiento de conducción relacionados con la velocidad

|Nombre de comportamiento|ID de comportamiento|Descripción|
|--------|:-------:|------|
|Aceleración brusca|1|El valor de umbral de aceleración brusca de acuerdo con la velocidad se establece internamente. La aceleración brusca se reconoce como tal si los datos de aceleración superan el valor de umbral. |
|Frenada brusca|2|El valor de umbral de frenada brusca de acuerdo con la velocidad se establece internamente. La frenada brusca se reconoce como tal si los datos de frenado de un trayecto supera el valor de umbral. |
|Exceso de velocidad|3|El valor de umbral de exceso de velocidad por tipo de carretera está establecido. El exceso de velocidad se reconoce como tal si los datos de velocidad para el trayecto superan el valor de umbral. Puede configurar el umbral para el exceso de velocidad. |
|Detención frecuente|4|Una detención se detecta cuando el valor de velocidad es cero. Las detenciones frecuentes se reconocen como tales si hay muchas instancias de detención dentro de un determinado intervalo de tiempo en un trayecto. |
|Aceleración frecuente|5|El valor de umbral de aceleración de acuerdo con la velocidad se establece internamente. La aceleración frecuente se detecta como tal si el conductor supera con frecuencia el valor de umbral dentro de un determinado intervalo de tiempo durante el trayecto. |
|Frenada frecuente|6|El valor de umbral de frenada de acuerdo con la velocidad se establece internamente. La frenada frecuente se reconoce como tal si el conductor supera el valor de umbral con frecuencia dentro de un determinado intervalo de tiempo durante el trayecto. |

#### Tabla 2: Comportamiento de conducción relacionado con los giros

|Nombre de comportamiento|ID de comportamiento|Descripción|
|-------|:--------:|-------|
|Giro brusco (giro a alta velocidad)|7|El valor de umbral de velocidad en el giro está establecido. Un giro brusco se reconoce como tal si el conductor supera el valor de umbral. Puede configurar el umbral de giro brusco.
|Aceleración antes de giro|8|El valor de umbral de aceleración de acuerdo con la velocidad se establece internamente. La aceleración antes de giro se reconoce como tal si el conductor supera el valor de umbral. |Frenada excesiva antes de salir de una curva|9|El valor de umbral de frenada de acuerdo con la velocidad se establece internamente. La frenada excesiva antes de salir de una curvase reconoce como tal si el conductor supera el valor de umbral.
#### Tabla 3: Otros tipos de comportamiento de conducción

|Nombre de comportamiento|ID de comportamiento|Descripción|
|-------|:--------:|-------|
|Conducción con fatiga|10|El valor de umbral de frenada de acuerdo con la velocidad se establece internamente. La fatiga en un conductor se reconoce como tal si la velocidad supera el valor de umbral. |


### Contexto de conducción
|Contexto<br/>categoría|Contexto<br/>ID de categoría|Nombre de contexto|ID de contexto|
|-------|:-----:|--------|:-------:|
|**Intervalo de tiempo**|**4**|\-|\-|
|Intervalo de tiempo|4|Día|1|
|Intervalo de tiempo|4|Noche|2|
|Intervalo de tiempo|4|Horas pico de la mañana|3|
|Intervalo de tiempo|4|Horas pico de la noche|4|
|**Tipo de carretera**|**3**|\-|\-|
|Tipo de carretera|3|Autopista|1|
|Tipo de carretera|3|Autovía urbana|2|
|Tipo de carretera|3|Vía urbana principal|3|
|Tipo de carretera|3|Carretera urbana|4|
|Tipo de carretera|3|Otros|5|
|**Patrón de velocidad**|**0**|\-|\-|
|Patrón de velocidad|0|Flujo libre|0|
|Patrón de velocidad|0|Flujo constante|1|
|Patrón de velocidad|0|Fuerte congestión|2|
|Patrón de velocidad|0|Congestión|3|
|Patrón de velocidad|0|Condiciones combinadas|4|


## API de REST
{: #rest_api}

La API REST de {{site.data.keyword.iotdriverinsights_short}} proporciona solicitudes que se pueden utilizar para personalizar y compilar las aplicaciones de {{site.data.keyword.Bluemix_notm}}:

 1. Mandatos de datos de coche:
   - `sendCarProbeData` envía los datos de sondeo del coche que deben analizarse
   - `getCarProbeDataListAsDate` devuelve la lista de datos de sondeo del coche por fecha
   - `deleteCarProbeDataListByDate` elimina los datos de sondeo del coche
 2. Mandatos de trabajo de análisis:
   - `sendJobRequest` envía la solicitud de trabajo de análisis de comportamiento de conducción
   - `getJobInfo` devuelve la información del trabajo especificado
   - `getJobInfoList` devuelve la lista de información de trabajo
 3. Mandatos de resultados del análisis:
   - `getAnalyzedTripSummaryList` devuelve la lista de información de resumen de la trayectoria analizada
   - `getAnalyzedTripInfo` devuelve la información de la trayectoria analizada especificada
   - `deleteJobResult` suprime todos los resultados analizados relacionados con un trabajo

Para obtener más información, consulte la documentación de la [API de {{site.data.keyword.iotdriverinsights_short}}](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}.

## Infraestructura del análisis de Big Data
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} utiliza Hadoop como infraestructura de fondo. Hadoop proporciona escalabilidad elevada para que el servicio {{site.data.keyword.iotdriverinsights_short}} pueda recuperar y analizar grandes volúmenes de datos de sondeo de prueba y contextuales. 
