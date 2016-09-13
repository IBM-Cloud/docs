---

copyright:
  año: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Acerca de {{site.data.keyword.iotdriverinsights_short}}
{: #iotdriverinsights_overview}

Puede utilizar {{site.data.keyword.iotdriverinsights_full}} para analizar el comportamiento del conductor a partir de los datos de sondeo del coche y los datos contextuales.
{:shortdesc}

## Análisis del comportamiento del conductor
{: #driver_behavior_analysis}
Puede analizar el comportamiento del conductor, como una aceleración o frenada brusca, frenadas frecuentes, exceso de velocidad, giros bruscos y otras acciones de los datos de sondeo y datos contextuales del coche. 

Se incluyen las siguientes actividades y contextos: 
 - Comportamientos de conducción 
    - Relacionados con la velocidad
       - Aceleración brusca
       - Frenada brusca
       - Exceso de velocidad
       - Paradas frecuentes
       - Aceleración frecuente
       - Frenada frecuente
    - Relacionados con los giros
       - Giro brusco (guro a alta velocidad)
       - Aceleración antes de giro
       - Frenada excesiva en una curva
    - Otros
       - Conducción con fatiga
 - Contexto de conducción
    - Intervalo de tiempo
       - Horas pico de la mañana
       - Horas pico de la noche
       - Día
       - Noche
    - Tipo de carretera
       - Autopista
       - Autovía urbana
       - Vía urbana principal
       - Carretera urbana
       - Otros
    - Patrón de velocidad basado en el tipo de carretera
       - Flujo libre
       - Flujo constante
       - Congestión
       - Fuerte congestión
       - Condiciones combinadas

## Infraestructura del análisis de Big Data
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} utiliza Hadoop como infraestructura de fondo. Hadoop permite a {{site.data.keyword.iotdriverinsights_short}} realizar una escalabilidad elevada para analizar Big Data de datos de sondeo y datos contextuales del coche. 

## API de REST
{: #rest_api}
Los desarrolladores pueden recuperar los resultados del análisis mediante la API de REST y utilizarlos en la aplicación {{site.data.keyword.Bluemix_notm}}. 
 1. Datos del vehículo
   - `sendCarProbeData` envía los datos de sondeo del coche que deben analizarse. 
   - `getCarProbeDataListAsDate` devuelve la lista de datos de sondeo del coche por fecha. 
   - `deleteCarProbeDataListByDate` elimina los datos de sondeo del coche. 
 2. Trabajo de análisis
   - `sendJobRequest` envía la solicitud de trabajo de análisis del comportamiento de conducción. 
   - `getJobInfo` devuelve la información del trabajo especificado. 
   - `getJobInfoList` devuelve la lista de información de trabajo. 
 3. Resultado del análisis 
   - `getAnalyzedTripSummaryList` devuelve la lista de información de resumen de la trayectoria analizada. 
   - `getAnalyzedTripInfo` devuelve la información de la trayectoria analizada especificada. 
   - `deleteJobResult` elimina todos los resultados analizados relacionados con un trabajo. 

## Posibilidades de configuración
{: #configurability}
Algunos parámetros de límite del análisis (como intervalo de velocidad por tipo de carretera, intervalo de ángulo de giro, etc) pueden configurarse desde la interfaz de usuario (UI). 
