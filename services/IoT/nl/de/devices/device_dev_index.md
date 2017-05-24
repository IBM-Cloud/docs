---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# In {{site.data.keyword.iot_short_notm}} Geräte entwickeln
{: #device_dev_index}

Ein Gerät ist alles, was eine Verbindung zum Internet hat und Daten in die Cloud sendet oder aus der Cloud empfängt. Sie können Geräte verwenden, um Ereignisinformationen wie Sensormesswerte in die Cloud zu senden und Befehle von Anwendungen in der Cloud entgegenzunehmen.

Geräte publizieren Daten mithilfe von Ereignissen an {{site.data.keyword.iot_short_notm}}. Dabei steuert das Gerät den Inhalt des Ereignisses und ordnet jedem gesendeten Ereignis einen Namen zu. Wenn {{site.data.keyword.iot_short_notm}} ein Ereignis von einem Gerät empfängt, wird anhand der Berechtigungsnachweise für die Verbindung, über die das Ereignis empfangen wurde, ermittelt, von welchem Gerät das Ereignis gesendet wurde. Durch diese Architektur wird verhindert, dass ein Gerät die Identität eines anderen Geräts annimmt.

Weitere Informationen zu wichtigen Konzepten, einschließlich Geräten, finden Sie in [Informationen zu Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts).


## Gerät mit {{site.data.keyword.iot_short_notm}} verbinden
{: #device_connect}
Sie können Ihr Gerät unter Verwendung von HTTP- oder MQTT-Protokollen mit {{site.data.keyword.iot_short_notm}} verbinden. Verwenden Sie das HTTP-Protokoll, wenn Sie ein Anforderung/Antwort-Szenario konfigurieren möchten (z. B. wenn ein Kunde einen Kauf tätigt und eine Bestätigung erhält). Verwenden Sie das MQTT-Protokoll, wenn Sie ein Ereignisszenario konfigurieren möchten (z. B. wenn jemand an einer Tür klingelt und damit einen Alert auf einem mobilen Gerät auslöst).

Das betreffende Gerät muss bei einer Organisation registriert sein, damit es eine Verbindung zu {{site.data.keyword.iot_full}} herstellen kann. Zum Herstellen eine sicheren Verbindung zu {{site.data.keyword.iot_short_notm}} müssen Sie sich für ein Bluemix-Konto registrieren und eine eigene {{site.data.keyword.iot_short_notm}}-Organisation erstellen. Anschließend können Sie Ihr Gerät unter dieser Organisations-ID registrieren. Registrierte Geräte identifizieren sich selbst mit einer eindeutigen Geräte-ID (z. B. mit der MAC-Adresse) und mit einem Authentifizierungstoken, das ausschließlich für dieses Geräte akzeptiert wird, bei {{site.data.keyword.iot_short_notm}}. Nachdem Sie eine sichere Verbindung hergestellt haben, können Sie mit Bluemix eigene Anwendungen erstellen. Bei Bedarf können Sie Node-RED verwenden, um Ihre Anwendungen miteinander zu verbinden.

Wenn Sie Ihr Gerät verbinden möchten, ohne es zu registrieren (z. B. um einen Machbarkeitsnachweis zu erstellen), können Sie die spezielle Organisations-ID `QuickStart` verwenden. `QuickStart` ist eine allgemein zugängliche Sandbox-Instanz von {{site.data.keyword.iot_short_notm}}, die in der Cloud ausgeführt wird. Wenn keine sicher Verbindung erforderlich ist, können Sie mit `QuickStart` die Konnektivität Ihres Geräts testen und mit {{site.data.keyword.iot_short_notm}} experimentieren. Verbinden Sie nach dem Experimentieren Ihr Gerät erneut mit TLS und mit Ihrem Authentifizierungstoken über eine sicher Verbindung mit Ihrer eigenen Organisations-ID-Instanz.

Weitere Informationen zum Verbinden Ihres Geräts mit {{site.data.keyword.iot_short_notm}} unter Verwendung des HTTP-Protokolls finden Sie in [HTTP-REST-API für Geräte](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html).
Weitere Informationen zum Verbinden Ihres Geräts mit {{site.data.keyword.iot_short_notm}} unter Verwendung des MQTT-Protokolls finden Sie in [MQTT-Konnektivität für Geräte](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html).

## Einführung in die Entwicklung von Geräten
{: #get_started}
Wenn Sie über ein Gerät verfügen, das bereits für {{site.data.keyword.iot_short_notm}} aktiviert ist, können Sie das Gerät sofort verwenden.

Wenn das Gerät noch nicht aktiviert ist, lesen Sie die verfügbaren Anleitungen in [developerWorks](https://developer.ibm.com/recipes/). Suchen Sie in den vorhandenen Anleitungen nach einer Anleitung für Ihr Gerät und verwenden Sie diese Anleitung, um mit der Entwicklung zu beginnen. Sie können auch eigene Anleitungen veröffentlichen.

Falls keine Anleitung für Ihr spezielles Gerät vorhanden ist, stellt IBM verschiedene Programmierungshandbücher und APIs bereit, die Sie als Einstieg verwenden können. Diese Handbücher enthalten Clientbibliotheken, Beispiele und Informationen als Hilfe zum Erstellen und Entwickeln von Code für die Integration und das Verbinden Ihrer Geräte und Anwendungen in {{site.data.keyword.iot_short_notm}}. Momentan sind die folgenden Programmierungshandbücher verfügbar:

- Java
- Node.js
- Embedded C
- ARM mBed C++
- Python
- C#
- Node-RED

Weitere Informationen und Links zu den verfügbaren Programmierungshandbüchern finden Sie in [Clientbibliotheken für die {{site.data.keyword.iot_short_notm}}-Entwicklung](../iot_platform_client_lib.html).

Wenn Sie kein geeignetes Programmierungshandbuch für {{site.data.keyword.iot_short_notm}} finden, können Sie ein eigenes Programm schreiben und das MQTT- oder HTTP-Protokoll verwenden, um Ihr Gerät mit {{site.data.keyword.iot_short_notm}} zu verbinden.

MQTT ist ein offener Standard, der von der Standardisierungsorganisation OASIS verwaltet wird und durch ISO international anerkannt ist. Weitere Informationen finden Sie in [OASIS Message Queuing Telemetry Transport ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt){: new_window}.

Eine Vielzahl von MQTT-Clientbibliotheken für viele verschiedene Systeme steht zur Verfügung. Dazu gehören die folgenden Umgebungen:
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

Weitere Informationen zu MQTT finden Sie in [MQTT-Messaging](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3).
