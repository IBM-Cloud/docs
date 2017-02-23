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
# Standards und Anforderungen
{: #standards_and_requirements}

{{site.data.keyword.iot_full}} unterstützt eine Reihe von Standards und Anforderungen für das Messaging und die allgemeine Entwicklung von Geräten und Anwendungen.
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

{{site.data.keyword.iot_short_notm}} unterstützt folgende Versionen des MQTT-Nachrichtenprotokolls:

MQTT-Version | Hinweise
--- | --- | ---
[3.1.1](https://www.oasis-open.org/standards#mqttv3.1.1) (empfohlen)  | <ul><li>OASIS-Standard.<li>ISO-Standard (ISO/IEC PRF 20922) <li>Verbesserte Interoperabilität zwischen verschiedenen Clients und Servern aufgrund einer präziseren Definition des Protokolls im Vergleich zu Version 3.1.<li>Die maximale Länge der MQTT-Client-ID (ClientId) wurde von der in Version 3.1 geltenden Begrenzung von 23 Zeichen auf 256 Zeichen erhöht. </br>Für den {{site.data.keyword.iot_short_notm}}-Service sind häufig längere Client-IDs erforderlich. </br>Lange Client-IDs werden ohne Berücksichtigung der Version des MQTT-Protokolls unterstützt. Einige Clientbibliotheken der Version 3.1 überprüfen jedoch die Länge des Werts für 'ClientId' und erzwingen die Begrenzung auf 23 Zeichen.</ul>
3.1 | MQTT Version 3.1 ist die heute am häufigsten verwendete Protokollversion.

{{site.data.keyword.iot_short_notm}} unterstützt alle Inhalte, die im Rahmen des MQTT-Standards zulässig sind. MQTT ist datenagnostisch, sodass es möglich ist, Bilder zu senden, Text in beliebiger Codierung, verschlüsselte Daten und sozusagen jede Art von Daten im Binärformat. Weitere Informationen zum MQTT-Standard finden Sie in den folgenden Ressourcen:
- [MQTT.org](http://mqtt.org/)
- [HiveMQ: Introducing MQTT](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)

Informationen zur Größenbegrenzung für Nachrichtennutzdaten und Formateinschränkungen für bestimmte Anwendungsfälle für {{site.data.keyword.iot_short_notm}} finden Sie in [MQTT-Messaging](mqtt/index.html).
