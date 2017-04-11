---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Desarrollo de pasarelas en {{site.data.keyword.iot_short_notm}}
{: #gw_dev_index}

Si los dispositivos no se pueden conectar directamente a Internet, puede crear un dispositivo de pasarela para recuperar y enviar datos a las aplicaciones de la organización de {{site.data.keyword.iot_full}}. Se proporcionan bibliotecas de cliente, ejemplos e información para ayudarle a conectar pasarelas de dispositivo a la organización y aplicaciones de {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Protocolos de conexión
Las pasarelas se conectan a {{site.data.keyword.iot_short_notm}} utilizando el protocolo de mensajería MQTT. No se admite la conexión de pasarelas a {{site.data.keyword.iot_short_notm}} mediante mensajería HTTP. Solo los dispositivos se pueden conectar mediante mensajería HTTP.

## Bibliotecas de clientes
Las bibliotecas de cliente para desarrollar pasarelas que se conectan a {{site.data.keyword.iot_short_notm}} están disponibles en los siguientes lenguajes:

|Biblioteca cliente |Enlace a biblioteca y más documentación
|:---|:---
|C++|[https://github.com/ibm-watson-iot/iot-cpp](https://github.com/ibm-watson-iot/iot-cpp)
|C#|[https://github.com/ibm-watson-iot/iot-csharp](https://github.com/ibm-watson-iot/iot-csharp)
|Embedded C| [https://github.com/ibm-watson-iot/iot-embeddedc](https://github.com/ibm-watson-iot/iot-embeddedc)
|Java™|[https://github.com/ibm-watson-iot/iot-java](https://github.com/ibm-watson-iot/iot-java)
|mBed C++|[https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/)
|Node.js|[https://github.com/ibm-watson-iot/iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs)
|Node-RED|[https://github.com/ibm-watson-iot/iot-nodered](https://github.com/ibm-watson-iot/iot-nodered)
|Python|[https://github.com/ibm-watson-iot/iot-python

](https://github.com/ibm-watson-iot/iot-python)

Para obtener más información y ver enlaces con las bibliotecas de cliente disponibles, consulte también [Bibliotecas de cliente para el desarrollo de {{site.data.keyword.iot_short_notm}}](../iot_platform_client_lib.html).

## Edge Analytics
{: #eaa_community}

La característica {{site.data.keyword.iot_short_notm}} Edge Analytics le permite ejecutar {{site.data.keyword.iot_short_notm}} Analytics en un dispositivo de pasarela. Utilice Edge Analytics para que el análisis analice y responda a datos recopilados en el extremo de la red. También puede enviar datos de dispositivo a {{site.data.keyword.iot_short_notm}} para el proceso adicional de análisis, la visualización del panel de control, como entrada a otros análisis o para que se almacene en un repositorio histórico basado en la nube. 

Puede descargar el SDK de Edge Analytics desde la [página de comunidad de IBM Edge Analytics](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true). El SDK incluye el archivo JAR de SDK, javadoc, código de ejemplo, enlaces de recetas y archivos README. En la comunidad, también puede ver vídeos para ponerse en marcha con Edge Analytics y puede utilizar el foro de la comunidad para hacer preguntas. 
