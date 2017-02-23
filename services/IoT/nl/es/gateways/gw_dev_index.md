---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

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
|C++| https://github.com/ibm-watson-iot/iot-cpp
|C#| https://github.com/ibm-watson-iot/iot-csharp
|Embedded C| https://github.com/ibm-watson-iot/iot-embeddedc
|Java™|https://github.com/ibm-watson-iot/iot-java
|mBed C++|https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/
|Node.js|https://github.com/ibm-watson-iot/iot-nodejs
|Node-RED|https://github.com/ibm-watson-iot/iot-nodered
|Python|https://github.com/ibm-watson-iot/iot-python

Para obtener más información y ver enlaces con las bibliotecas de cliente disponibles, consulte también [Bibliotecas de cliente para el desarrollo de {{site.data.keyword.iot_short_notm}}](../iot_platform_client_lib.html).
