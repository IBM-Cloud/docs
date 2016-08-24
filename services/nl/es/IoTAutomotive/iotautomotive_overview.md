---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Acerca de {{site.data.keyword.iot4auto_short}} (Beta)
{: #iotautomotive_overview}

Última actualización: 29 de julio de 2016
{: .last-updated}

{{site.data.keyword.iot4auto_full}} es un servicio de {{site.data.keyword.Bluemix_notm}} para visualizar y analizar Big Data de vehículos.

Al utilizar el servicio {{site.data.keyword.iot4auto_short}}, se pueden recopilar y procesar grandes volúmenes de datos procedentes de los vehículos. La analítica de {{site.data.keyword.iot4auto_short}} aporta información accionable y muy valiosa sobre el comportamiento del conductor, la ubicación del vehículo, así como otras actividades relacionadas con la automoción y otros sucesos de interés.
{:shortdesc}

## Arquitectura
{: #architecture}
{{site.data.keyword.iot4auto_short}} es una plataforma de infraestructura en tiempo real para aplicaciones de automoción y dispositivos de vehículo conectados. El servicio también se ha diseñado para dar soporte a las prestaciones emergentes de conducción autónoma del futuro. 

![Arquitectura de {{site.data.keyword.iot4auto_full}}](images/architecture_iotautomotive.png "{{site.data.keyword.iot4auto_full}} architecture")

El servicio {{site.data.keyword.iot4auto_short}} incluye los siguientes servicios de {{site.data.keyword.Bluemix_notm}}, que también están disponibles de forma independiente en el catálogo de {{site.data.keyword.Bluemix_notm}}:

|Servicio|Descripción|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html)| Un servicio que puede analizar el comportamiento del conductor e identificar patrones de trayectoria de un viaje a partir de los datos de contexto y sondeo de coche recuperados del vehículo conectado.
|[Context Mapping](../IotMapInsights/index.html)| Un servicio que proporciona funciones geoespaciales, como la coincidencia de mapa y la búsqueda de la ruta más corta para redes viales.
*Tabla 1. Servicios de {{site.data.keyword.iot4auto_short}}*

## Características
{: #features}

{{site.data.keyword.iot4auto_short}} da soporte a las siguientes características y funciones de las soluciones que proporcionan los datos de sondeo de coche de los dispositivos de vehículo conectados:

### Recuperación de datos de los dispositivos {{site.data.keyword.iot4auto_short}}

- Admite los siguientes protocolos y modelos de datos:
   - TPEG
   - ITS
   - Estándares ISO de automoción
- Admite otros sensores y dispositivos que no sean vehículos

### Normalización de datos y almacenamiento

- Identifica y filtra datos de anomalías
- Correlaciona, convierte y formatea datos al modelo de datos estándar para su análisis
- Coloca los datos en uno de los siguientes almacenes de datos según el volumen, la latencia y el uso de la aplicación o servicio:
   -  Almacén de datos de Hadoop para el análisis de Big Data
   -  Almacén de datos del agente para el análisis en tiempo real

### Servicio basado en la correlación geoespacial

- Coincidencia de mapa en tiempo real
- Servicio de sucesos
- Inyección dinámica de sucesos desde vehículos y orígenes externos
- Búsqueda según topología basada en nodos o enlaces
- Soporte a mapas contextuales que integran datos meteorológicos

### Plataforma de análisis en tiempo real de baja latencia y altamente escalable

- Tecnología basada en agentes
- Análisis personalizado
- Análisis flexible basado en reglas

### Análisis de correlación de objetos en movimiento (MOMA)

- Análisis por lotes (Big Data) a partir de datos del vehículo
- Análisis del comportamiento del conductor
- Creación de perfiles de conductor
- Análisis de patrones de trayectoria

### Servicio de proveedor de datos

- API para servicios y aplicaciones de terceros

### Integración la gestión de activos

- Sistema de gestión de activos de vehículos

## API REST
{: #api}

La [API de {{site.data.keyword.iot4auto_short}}](http://ibm.biz/IoT4Automotive_APIdoc) proporciona mandatos que le ayudarán a desarrollar {{site.data.keyword.iot4auto_short}} para satisfacer sus requisitos. 

Al utilizar los mandatos de API REST disponibles, puede personalizar la instancia de servicio de {{site.data.keyword.iot4auto_short}}. 

- Inyectar sucesos específicos en el sistema
- Almacenar datos normalizados de sondeo de coche de un vehículo en el almacén de datos analíticos preferido
- Recuperar sucesos de interés en tiempo real junto con la ubicación geográfica del vehículo

### Mandatos de API REST

|Objetivo |Mandato de API |Descripción |
|:---|:---|:---|
|Inyectar suceso|`sendEvent`|Envía sucesos de tráfico y otros sucesos a la plataforma.|
|Enviar datos de sondeo de coche|`sendCarProbe`|Envía datos de sensor según la posición del vehículo y recupera los sucesos que afectan al vehículo según el resultado del análisis en tiempo real. |
|Crear datos de vehículo|`createVehicle`|Crea un registro del vehículo como un activo. Esta información se utiliza para la autenticación, el inventario y otros usos. |
|Correlacionar las API|No es aplicable|Para obtener más información, consulte [API del servicio Contextual Map](http://ibm.biz/IoTContextMapping_APIdoc).|
|API de análisis|No es aplicable|Para obtener más información, consulte [API del servicio Driver Behavior]( http://ibm.biz/IoTDriverBehavior_APIdoc).|
|Obtener datos de sondeo de coche|`getCarProbe`|Permite obtener los datos de sondeo del vehículo más recientes que se hayan enviado con el mandato de API `sendCarProbe`.|
|Obtener sucesos de mapa|`getEvent` |Permite obtener los sucesos en el mapa que se hayan enviado con el mandato de API `sendEvent`.|
|Obtener datos de activos de vehículo|`getVehicle`| Permite obtener datos de vehículo como un activo desde el mandato de API `createVehicle`.|
*Tabla 2. Mandatos de API REST de {{site.data.keyword.iot4auto_short}}*
