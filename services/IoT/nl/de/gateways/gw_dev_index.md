---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

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
Gateways stellen über das MQTT-Nachrichtenprotokoll eine Verbindung zu {{site.data.keyword.iot_short_notm}} her. Das Verbinden von Gateways mit {{site.data.keyword.iot_short_notm}} mithilfe von HTTP-Messaging wird nicht unterstützt. Diese Art der Verbindung ist nur für Geräte möglich.

## Clientbibliotheken
Clientbibliotheken für die Entwicklung von Gateways, die eine Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen können, sind in den folgenden Sprachen verfügbar:

|Clientbibliothek |Link zu Bibliothek und weiterer Dokumentation
|:---|:---
|C++|[https://github.com/ibm-watson-iot/iot-cpp ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-cpp){: new_window}
|C#|[https://github.com/ibm-watson-iot/iot-csharp ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-csharp){: new_window}
|Embedded C| [https://github.com/ibm-watson-iot/iot-embeddedc ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-embeddedc){: new_window}
|Java™|[https://github.com/ibm-watson-iot/iot-java ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-java){: new_window}
|mBed C++|[https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/ ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window}
|Node.js|[https://github.com/ibm-watson-iot/iot-nodejs ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window}
|Node-RED|[https://github.com/ibm-watson-iot/iot-nodered ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-nodered){: new_window}
|Python|[https://github.com/ibm-watson-iot/iot-python ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/ibm-watson-iot/iot-python){: new_window}

Weitere Informationen und Links zu den Clientbibliotheken, die zur Verfügung stehen, finden Sie auch in [Clientbibliotheken für die {{site.data.keyword.iot_short_notm}}-Entwicklung](../iot_platform_client_lib.html).

## Edge Analytics
{: #eaa_community}

Mit dem {{site.data.keyword.iot_short_notm}} Edge Analytics-Feature können Sie {{site.data.keyword.iot_short_notm}} Analytics auf einem Gateway-Gerät ausführen. Mit Edge Analytics werden Analysen analysiert und wird auf Daten geantwortet, die in der Netzperipherie erfasst werden. Sie können außerdem für weitere Analyseverarbeitung, Dashboardvisualisierung, als Eingabe für andere Analysen oder zum Speichern in einem cloudbasierten Protokollrepository Gerätedaten an {{site.data.keyword.iot_short_notm}} senden.

Sie können das Edge Analytics SDK von der [IBM Edge Analytics-Community-Seite ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){: new_window} herunterladen. Das SDK umfasst die SDK-JAR-Datei, Javadoc, Beispielcode, Links zu Anleitungen und Readme-Dateien. In der Community können Sie außerdem Videos zur Einführung in Edge Analytics ansehen; im Communityforum können Sie Fragen stellen.
