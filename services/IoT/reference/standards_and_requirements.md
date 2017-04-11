---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# Standards and requirements
{: #standards_and_requirements}

{{site.data.keyword.iot_full}} supports a number of standards and requirements for messaging and general device and application development.
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

{{site.data.keyword.iot_short_notm}} supports the following versions of the MQTT messaging protocol:

MQTT version | Notes
--- | --- | ---
[3.1.1 ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.oasis-open.org/standards#mqttv3.1.1){: new_window} (recommended)  | <ul><li>OASIS Standard.<li>ISO standard (ISO/IEC PRF 20922) <li>Improved interoperability between various clients and servers because of a more precise definition of the protocol compared to V3.1.   <li>The maximum length of the MQTT client identifier (ClientId) is increased to 256 from the 23 character limit that is imposed by V3.1. </br>The {{site.data.keyword.iot_short_notm}} service often requires longer client IDs. </br>Long client IDs are supported regardless of the MQTT protocol version. However, some V3.1 client libraries check the length of the ClientId value and enforce the 23 character limit.</ul>
3.1 | MQTT V3.1 is the version of the protocol that is in widest use today.

{{site.data.keyword.iot_short_notm}} supports any content that is permitted by the MQTT standard. MQTT is data-agnostic, so it's possible to send images, texts that are in any encoding, encrypted data, and virtually every type of data in binary format. For more information about the MQTT standard, see the following resources:
- [MQTT.org ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://mqtt.org/){: new_window}
- [HiveMQ: Introducing MQTT ![External link icon](../../../icons/launch-glyph.svg "External link icon")](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt){: new_window}

For information about message payload size limits and format restrictions for specific use cases for {{site.data.keyword.iot_short_notm}}, see [MQTT messaging](mqtt/index.html).
