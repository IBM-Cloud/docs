---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a {{site.data.keyword.iot4auto_short}} (Beta)
{: #getting_started_iotautomotive}

Última actualización: 29 de julio de 2016
{: .last-updated}

{{site.data.keyword.iot4auto_full}} es un servicio de {{site.data.keyword.Bluemix_notm}} para recuperar, gestionar y analizar Big Data de vehículos conectados. La analítica de {{site.data.keyword.iot4auto_short}} aporta información accionable y muy valiosa sobre el comportamiento en la conducción, la ubicación del vehículo, así como otras actividades relacionadas con la automoción y otros sucesos de interés.


{:shortdesc}

Al utilizar {{site.data.keyword.iot4auto_short}}, puede realizar las tareas siguientes:

- Enviar datos de sondeo de coche y datos normalizados al almacén de datos para su análisis
- Inyectar sucesos a la correlación de contexto y recuperar los sucesos que afectan a vehículos específicos
- Identificar nuevos sucesos a partir de los datos de sondeo de coche
- Recuperar información sobre vehículos conectados
- Gestionar datos de activos para conductores, vehículos, reglas de sucesos, tipos de sucesos y proveedores


El servicio {{site.data.keyword.iot4auto_short}} incluye los siguientes servicios de {{site.data.keyword.Bluemix_notm}}, que también están disponibles de forma independiente en el catálogo de {{site.data.keyword.Bluemix_notm}}:

|Servicio|Descripción|
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html){:new_window}| Un servicio que puede analizar el comportamiento del conductor e identificar patrones de trayectoria de un viaje a partir de los datos de contexto y sondeo de coche recuperados del vehículo conectado.
|[Context Mapping](../IotMapInsights/index.html){:new_window}| Un servicio que proporciona funciones geoespaciales, como la coincidencia de mapa y la búsqueda de la ruta más corta para redes viales.
*Tabla 1. Servicios de {{site.data.keyword.iot4auto_short}}*

Antes de empezar a integrar aplicaciones y dispositivos de automoción en el servicio, asegúrese de realizar los pasos siguientes:

1. Revise el tema [Acerca de {{site.data.keyword.iot4auto_short}}](iotautomotive_overview.html) para conocer las características y los análisis disponibles y admitidos en el servicio. 
2. Cuando añada una instancia del servicio desde el [catálogo de {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/catalog/labs/){:new_window}, asegúrese de que el servicio esté vinculado a una aplicación y anote los valores de ID de arrendatario, nombre de usuario y contraseña generados automáticamente. Necesitará estos valores más adelante para acceder al servicio a través de la API de {{site.data.keyword.iot4auto_short}}.
3. Con la consola del panel de control, puede configurar los puertos, los nombres de host de destino y otros valores de {{site.data.keyword.iot4auto_short}}. Para obtener más información, consulte [Administración](iotautomotive_admin.html).

Puede integrar aplicaciones y dispositivos de automoción con este servicio utilizando los mandatos de API REST de {{site.data.keyword.iot4auto_short}}.

Para empezar rápidamente, efectúe los pasos siguientes:

1. Inyecte sucesos con el mandato de solicitud de API `sendEvent` para que se envíen los sucesos a analizar.
  - Solicitud: datos de suceso con la posición
2. Confirme que los datos del suceso se almacenan con Map Matching utilizando el mandato de solicitud de API `getEvent` para recuperar el suceso. 
  - Solicitud: datos de área (longitud y latitud de los puntos inicial y final)
  - Respuesta: datos del suceso con el ID de enlace vial
3.  Envíe datos de sondeo de coche para su análisis utilizando el mandato de solicitud de API `sendCarProbe`.
  - Solicitud: datos de sondeo de coche con la posición
4. Confirme que los datos de sondeo de coche se almacenan con Map Matching utilizando el mandato de solicitud de API `getCarProbe` para recuperar los datos.
  - Solicitud: datos de área (longitud y latitud de los puntos inicial y final)
  - Respuesta: datos del sondeo de coche con el ID de enlace vial
5. Analice los datos del conductor. Para obtener más información, consulte [Driver Behavior](../IotDriverInsights/index.html){:new_window}.

# Enlaces relacionados
{: #rellinks}

## Referencia de la API
{: #api}
* [Documentos de la API de {{site.data.keyword.iot4auto_short}}](http://ibm.biz/IoT4Automotive_APIdoc){:new_window}
* [API del servicio Contextual Map](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}
* [API del servicio Driver Behavior]( http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}


## Enlaces relacionados
{: #general}
* [Iniciación a {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Iniciación a {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [Iniciación a {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Novedades en Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [Respuestas dW en IBM developerWorks](https://developer.ibm.com/answers/topics/iot-for-automotive){:new_window}
* [Desbordamiento de la pila](http://stackoverflow.com/questions/tagged/iot-for-automotive){:new_window}
