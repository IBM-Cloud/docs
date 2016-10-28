---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}
Última actualización: 26 de agosto de 2016
{: .last-updated}

{{site.data.keyword.iot_full}} para {{site.data.keyword.Bluemix_notm}} le ofrece un kit de utilidades versátiles que incluye dispositivos de pasarela, gestión de dispositivos y acceso de aplicaciones potente. Al utilizar {{site.data.keyword.iot_short_notm}}, puede recopilar datos de dispositivo conectados y realizar las analíticas en datos en tiempo real desde la organización.
{:shortdesc}

## Antes de empezar
{: #byb}

Antes de conectar dispositivos y de utilizar datos, debe existir una instancia del servicio de {{site.data.keyword.iot_short_notm}} en la organización de {{site.data.keyword.Bluemix_notm}}. Puede crearla directamente desde la página de [{{site.data.keyword.iot_short_notm}} en el Catálogo de servicios de Bluemix](https://console.{DomainName}/catalog/services/internet-of-things-platform/).  

## Paso 1: Conectar los dispositivos
{: #up_and_running}

Para ejecutar el servicio, explore las opciones siguientes en función de su situación:

   |   El servicio se despliega | El servicio no se despliega
  ------------- | -------------
  **Tengo un dispositivo para conectar** | [Conecte el dispositivo a {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task).| Explore la conexión del dispositivo en la [Demostración de la organización Play](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}.
  **No tengo un dispositivo para conectar** | [Cree y conecte un simulador de dispositivos Node-RED](nodereddevice_sample.html){:new_window}. | Iníciese a [Watson IoT Platform Starter](https://new-console.stage1.ng.bluemix.net/docs/starters/IoT/iot500.html){:new_window}.
Para obtener más información sobre cómo conectarse a tipos de dispositivos específicos a {{site.data.keyword.iot_short_notm}}, consulte [Recetas de developerWorks](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}.  

Para la documentación de desarrollador de conexiones de dispositivos, consulte:
- [Conectividad de MQTT para dispositivos](devices/mqtt.html).
- [Conectividad de MQTT para pasarelas](gateways/mqtt.html).

## Paso 2: Analizar los datos de dispositivo
{: #analyzing_data}

Empiece a explorar los datos en tiempo real que los dispositivos están enviando a {{site.data.keyword.iot_short_notm}}.

{{site.data.keyword.iot_short_notm}} incluye las siguientes herramientas de analíticas:  
- [Paneles y tarjetas](data_visualization.html) para visualizar los datos de dispositivos en tiempo real.
- [Reglas y acciones](analytics.html) que desencadenan datos de dispositivos en tiempo real.

Para ver un ejemplo rápido de como empezar, consulte la receta de developerWorks [Uso de reglas y acciones con IBM Watson IoT Platform Cloud Analytics](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window}.

## Paso 3: Crear las aplicaciones que van a consumir los datos de dispositivo
{: #develop_applications}

Amplíe las características de análisis de datos de {{site.data.keyword.iot_short_notm}} creando y conectando sus propias aplicaciones para consumir datos de dispositivos históricos y en tiempo real.

Para obtener más información consulte los siguientes temas:   
- Explore la [documentación de desarrollador de aplicaciones](applications/api.html) y la [Documentación de la API de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}.
- Explore las [bibliotecas de cliente de {{site.data.keyword.iot_short_notm}}](iot_platform_client_lib.html) que proporcionan herramientas y archivos para crear y desarrollar código para integrar y conectar los dispositivos y aplicaciones.
- [Conecte un servicio de {{site.data.keyword.cloudantfull}}](cloudant_connector.html) a su {{site.data.keyword.iot_short_notm}} para almacenar datos de dispositivos históricos.




# Enlaces afines
{: #rellinks}
## Guías de aprendizaje y ejemplos
{: #samples}
* [Recetas para conectar los dispositivos](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [Organización Play de {{site.data.keyword.iot_short_notm}}](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Conexión de un Intel Galileo al {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [Conexión de un kit de iniciador de ARM® mbed™ IoT](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Conexión de un Raspberry Pi a {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## Referencia de API
{: #api}
* [Documentación de la API de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}
* [Documentación del desarrollador](developer_doc_overview.html)
