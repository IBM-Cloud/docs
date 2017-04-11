---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-28"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# Estándares y requisitos
{: #standards_and_requirements}

{{site.data.keyword.iot_full}} da soporte a diversos estándares y requisitos para mensajería y desarrollo general de aplicaciones y dispositivos.
{:shortdesc}


<!-- ## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} supports the following versions of the Hyperledger fabric:
- 0.5

## Python
{: #python}

Support for MQTT over SSL requires at least Python v2.7.9 or v3.4, and OpenSSL v1.0.1.
-->

## MQTT
{: #mqtt}

{{site.data.keyword.iot_short_notm}} da soporte a las versiones siguientes del protocolo de mensajería MQTT:

Versión de MQTT | Notas
--- | --- | ---
[3.1.1](https://www.oasis-open.org/standards#mqttv3.1.1) (recomendado)  | <ul><li>Estándar OASIS.<li>Estándar ISO (ISO/IEC PRF 20922) <li>Interoperatividad mejorada entre varios clientes y servidores gracias a una definición más precisa del protocolo comparado con V3.1.   <li>La longitud máxima del identificador de cliente de MQTT (ClientId) se ha aumentado a 256 desde el límite de 23 caracteres que ha impuesto V3.1. </br>El servicio de {{site.data.keyword.iot_short_notm}} normalmente requiere ID de cliente más grandes. </br>Los ID de cliente grandes están soportados independientemente de la versión del protocolo MQTT. Sin embargo, algunas bibliotecas de clientes de V3.1 comprueban la longitud del valor ClientId y aplican el límite de 23 caracteres.</ul>
3.1 | MQTT V3.1 es la versión del protocolo más en uso hoy día.

{{site.data.keyword.iot_short_notm}} da soporte a cualquier contenido permitido por el estándar MQTT. MQTT es neutro desde el punto de vista de los datos, por lo que es posible enviar imágenes, textos en cualquier codificación, datos cifrados, y prácticamente cualquier tipo de datos en formato binario. Para obtener más información sobre el estándar MQTT, consulte los siguientes recursos:
- [MQTT.org](http://mqtt.org/)
- [HiveMQ: Introducción a MQTT](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)

Para obtener más información sobre los límites de tamaño de carga útil de mensajes y restricciones de formato para casos de uso específicos de {{site.data.keyword.iot_short_notm}}, consulte [Mensajería de MQTT](mqtt/index.html).
