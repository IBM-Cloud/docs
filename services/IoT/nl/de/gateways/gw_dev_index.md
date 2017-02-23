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

# In {{site.data.keyword.iot_short_notm}} Gateways entwickeln
{: #gw_dev_index}

Wenn von Ihren Geräten keine direkte Verbindung zum Internet hergestellt werden kann, können Sie ein Gateway-Gerät erstellen, mit dem Daten abgerufen und an Anwendungen in Ihrer {{site.data.keyword.iot_full}}-Organisation gesendet werden können. Es werden Clientbibliotheken, Beispiele und Informationen bereitgestellt, die Sie beim Verbinden von Geräte-Gateways mit Ihrer {{site.data.keyword.iot_short_notm}}-Organisation und Ihren Anwendungen unterstützen.
{:shortdesc}

## Verbindungsprotokolle
Gateways stellen über das MQTT-Nachrichtenprotokoll eine Verbindung zu {{site.data.keyword.iot_short_notm}} her. Das Verbinden von Gateways mit {{site.data.keyword.iot_short_notm}} mithilfe der HTTP-Nachrichtenübertragung wird nicht unterstützt. Diese Art der Verbindung ist nur für Geräte möglich.

## Clientbibliotheken
Clientbibliotheken für die Entwicklung von Gateways, die eine Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen können, sind in den folgenden Sprachen verfügbar:

|Clientbibliothek |Link zu Bibliothek und weiterer Dokumentation
|:---|:---
|C++| https://github.com/ibm-watson-iot/iot-cpp
|C#| https://github.com/ibm-watson-iot/iot-csharp
|Embedded C| https://github.com/ibm-watson-iot/iot-embeddedc
|Java™|https://github.com/ibm-watson-iot/iot-java
|mBed C++|https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/
|Node.js|https://github.com/ibm-watson-iot/iot-nodejs
|Node-RED|https://github.com/ibm-watson-iot/iot-nodered
|Python|https://github.com/ibm-watson-iot/iot-python

Weitere Informationen und Links zu den Clientbibliotheken, die zur Verfügung stehen, finden Sie auch in [Clientbibliotheken für die {{site.data.keyword.iot_short_notm}}-Entwicklung](../iot_platform_client_lib.html).
