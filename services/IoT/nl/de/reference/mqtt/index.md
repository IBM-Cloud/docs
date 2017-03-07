---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# MQTT-Messaging
{: #ref-mqtt}

MQTT ist das primäre Protokoll, das Geräte und Anwendungen für die Kommunikation mit {{site.data.keyword.iot_full}} verwenden. MQTT ist ein Messaging-Übertragungsprotokoll, das für den effizienten Austausch von Echtzeitdaten zwischen Sensoren und mobilen Geräten entworfen wurde.
{:shortdesc}

MQTT wird über TCP/IP ausgeführt; während es möglich ist, Code direkt an TCP/IP zu richten, können Sie auch eine Bibliothek verwenden, die die Details des MQTT-Protokolls für Sie handhabt. Es steht eine breite Auswahl an MQTT-Clientbibliotheken zur Verfügung. IBM trägt zur Entwicklung und Unterstützung mehrere Clientbibliotheken bei, einschließlich solcher, die auf den folgenden Sites zur Verfügung stehen:

- [Community-Wiki für MQTT](https://github.com/mqtt/mqtt.github.io/wiki)
- [Eclipse Paho-Projekt](http://eclipse.org/paho/)

## Versionsunterstützung
{: #version-support}
Informationen zu den Versionen von MQTT, die von {{site.data.keyword.iot_short_notm}} unterstützt werden, finden Sie im Abschnitt zu den [Standards und Anforderungen](../standards_and_requirements.html#mqtt).

## Clients für Anwendungen, Geräte und Gateways
{: #device-app-clients}

In {{site.data.keyword.iot_short_notm}} sind die primären Klassen von Dingen (Things) Geräte und Anwendungen. Ein Gateway ist eine Unterklasse eines Geräts.

Ihr MQTT-Client identifiziert sich beim {{site.data.keyword.iot_short_notm}}-Service als eine Klasse der Dinge. Die Klasse der Dinge legt die Funktionalität eines verbundenen Clients fest. Die Klasse der Dinge bestimmt auch den Mechanismus für die Clientauthentifizierung.

Anwendungen und Geräte arbeiten mit unterschiedlichen Bereichen für MQTT-Topics.  Geräte arbeiten innerhalb eines für das Gerät festgelegten Topic-Bereichs, während Anwendungen vollständigen Zugriff auf den Topic-Bereich einer ganzen Organisation haben. Weitere Informationen finden Sie in den folgenden Abschnitten:

- [MQTT-Messaging für Geräte](../../devices/mqtt.html)
- [MQTT-Messaging für Anwendungen](../../applications/mqtt.html)
- [MQTT-Messaging für Gateways](../../gateways/mqtt.html)

### Aufbewahrte Nachrichten
{{site.data.keyword.iot_short_notm}} bietet eingeschränkte Unterstützung für die Funktion für aufbewahrte Nachrichten im MQTT-Messaging. Wenn das Flag für aufbewahrte Nachricht in einer MQTT-Nachricht, die von einem Gerät, Gateway oder von einer Anwendung an {{site.data.keyword.iot_short_notm}} gesendet wird, auf den Wert 'true' gesetzt ist, wird die Nachricht als nicht aufbewahrte Nachricht behandelt. {{site.data.keyword.iot_short_notm}}-Organisationen sind nicht dazu berechtigt, aufbewahrte Nachrichten zu publizieren. Der {{site.data.keyword.iot_short_notm}}-Service überschreibt das Flag für aufbewahrte Nachricht, sofern es auf den Wert 'true' gesetzt ist, und verarbeitet die Nachricht so, als wäre das Flag auf 'false' gesetzt.

## Servicequalitätsstufen
{: #qos-levels}

Das MQTT-Protokoll bietet für das Übergeben von Nachrichten zwischen Clients und Servern drei Servicequalitäten: 'höchstens einmal', 'mindestens einmal' und 'genau einmal'.
Zwar können Sie Ereignisse und Befehle mit jeder beliebigen Servicequalität senden, Sie sollten jedoch sorgfältig überlegen, welche Servicequalität für Ihre Bedürfnisse die richtige ist. Servicequalitätsstufe '2' ist nicht immer die bessere Option als Stufe '0'.

### Höchstens einmal (QoS0)

Die Servicequalitätsstufe 'höchstens einmal' ist der schnellste Übertragungsmodus und wird manchmal als 'Fire-and-Forget-Modus' bezeichnet. Die Nachricht wird höchstens einmal übermittelt oder sie wird möglicherweise überhaupt nicht übermittelt. Die Übermittlung über das Netz wird nicht bestätigt und die Nachricht wird nicht gespeichert. Die Nachricht geht möglicherweise verloren, wenn die Verbindung zum Client getrennt ist oder wenn der Server fehlschlägt.

Das MQTT-Protokoll erfordert keine Server, um Publizierungen mit Servicequalitätsstufe '0' an einen Client zu übermitteln. Wenn die Verbindung zum Client zum Zeitpunkt, an dem der Server die Publizierung empfängt, unterbrochen ist, wird die Publizierung in Abhängigkeit von der Serverimplementierung möglicherweise verworfen.

**Tipp:** Versenden Sie die Servicequalitätsstufe null, wenn Sie Echtzeitdaten in einem Intervall senden. Wenn eine einzelne Nachricht verloren geht, ist dies eher unerheblich, da kurz danach eine weitere Nachricht mit neueren Daten gesendet wird. In diesem Szenario führen die zusätzlichen Kosten einer höheren Servicequalität nicht zu einem materiellen Vorteil.

### Mindestens einmal (QoS1)

Mit der Servicequalitätsstufe 1 (QoS1) wird die Nachricht stets mindestens einmal übermittelt. Wenn vor dem Erhalt der Bestätigung durch den Absender ein Fehler auftritt, kann eine Nachricht mehrere Male übermittelt werden. Die Nachricht muss lokal beim Absender gespeichert werden, bis der Absender die Bestätigung erhält, dass die Nachricht vom Empfänger publiziert wurde. Die Nachricht wird für den Fall gespeichert, dass sie erneut gesendet werden muss.

### Genau einmal (QoS2)

Die Servicequalität 'Genau einmal' der Stufe 2 (QoS2) ist der sicherste, aber auch der langsamste Übertragungsmodus. Die Nachricht wird stets genau einmal übermittelt und muss ebenfalls lokal beim Absender gespeichert werden, bis der Absender die Bestätigung erhält, dass die Nachricht vom Empfänger publiziert wurde. Die Nachricht wird für den Fall gespeichert, dass sie erneut gesendet werden muss. Mit der Servicequalitätsstufe 2 wird für Handshaking und Bestätigung eine ausgereiftere Sequenz als bei Stufe 1 verwendet, um sicherzustellen, dass Nachrichten nicht dupliziert werden.

**Tipp:** Wenn Sie beim Senden von Befehlen die Bestätigung wünschen, dass nur der angegebene Befehl ausgeführt wird und dass er nur einmal ausgeführt wird, verwenden Sie die Servicequalitätsstufe 2. Dies ist ein Beispiel dafür, in welchem Fall der zusätzliche Aufwand für Stufe 2 gegenüber den übrigen Stufen einen Vorteil bietet.

## Subskriptionspuffer und bereinigte Sitzung
{: #subscription-buffers-and-clean-session}

Jeder Subskription eines Geräts oder einer Anwendung ist ein Puffer von 5000 Nachrichten zugeordnet.  Der Puffer ermöglicht jeder Anwendung oder jedem Gerät, mit den zu verarbeitenden Livedaten im Rückstand zu sein sowie für jede vorhandene Subskription einen Rückstand von bis zu 5000 anstehenden Nachrichten aufzubauen. Wenn der Puffer voll ist, wird bei Empfang einer neuen Nachricht jeweils die älteste Nachricht gelöscht.

Verwenden Sie die MQTT-Option für bereinigte Sitzungen, um auf den Subskriptionspuffer zuzugreifen. Wenn für die bereinigte Sitzung 'false' eingestellt ist, empfängt der Subskribent Nachrichten aus dem Puffer. Wenn für die bereinigte Sitzung 'true' eingestellt ist, wird der Puffer zurückgesetzt.

**Hinweis:** Der Grenzwert für den Subskriptionspuffer gilt unabhängig von der verwendeten Einstellung für die Servicequalität. Es ist möglich, dass eine Nachricht, die mit Stufe 1 oder 2 gesendet wurde, nicht an eine Anwendung übermittelt wird, die mit der Nachrichtenrate für die vorhandenen Subskriptionen nicht Schritt halten kann.

## Einschränkungen für Nachrichtennutzdaten
{: #message-payload}

{{site.data.keyword.iot_short_notm}} unterstützt das Senden und Empfangen von Nachrichten in einem beliebigen für den MQTT-Standard zulässigen Format. MQTT ist datenagnostisch, sodass es möglich ist, Bilder zu senden, Text in beliebiger Codierung, verschlüsselte Daten und sozusagen jede Art von Daten im Binärformat. Für bestimmte Anwendungsfälle bestehen jedoch Einschränkungen.   

Es bestehen auch Größenbegrenzungen für die Nachrichtennutzdaten in {{site.data.keyword.iot_short_notm}}.

### Formateinschränkungen für Nachrichtennutzdaten

Die Nachrichtennutzdaten können beliebige gültige Zeichenfolgen enthalten, das JSON-Fornat ('json'), das Textformat ('text') und das Binärformat ('bin') werden jedoch häufiger als andere Formattypen verwendet.

In der folgenden Tabellen werden die Einschränkungen für Nachrichtennutzdaten für verschiedene Formattypen beschrieben:

Nutzdatenformat  | Richtlinien für bestimmte Anwendungsfälle
--------- | ----------  
JSON | JSON ist das Standardformat für {{site.data.keyword.iot_short_notm}}. Wenn Sie planen, die integrierten Dashboards, Boards, Karten und die Analyse von {{site.data.keyword.iot_short_notm}} zu verwenden, müssen Sie sicherstellen, dass das Format der Nachrichtennutzdaten einem korrekt formatierten JSON-Text entspricht.
Text | Verwenden Sie die gültige UTF-8-Zeichencodierung.
Binary | Keine Einschränkungen.


### Maximale Größe für Nachrichtennutzdaten

**Wichtig:** Die maximale Größe für Nutzdaten in {{site.data.keyword.iot_short_notm}} beträgt 131072 Byte. Nachrichten mit Nutzdaten, die größer sind als dieser Grenzwert, werden abgelehnt. Die Verbindung zu dem Client, der die Verbindung herstellt, wird darüber hinaus getrennt und im Diagnoseprotokoll wird eine Nachricht angezeigt, die dem folgenden Beispiel für Gerätenachrichten ähnlich ist:

`Verbindung zu x.x.x.x wurde geschlossen. Die Nachrichtengröße ist für diesen Endpunkt zu hoch.`

## MQTT-Keepalive-Intervall
{: #mqtt-keep-alive}

Das MQTT-Keepalive-Intervall, das in Sekunden gemessen wird, definiert die maximale Zeit, die ohne eine Kommunikation zwischen dem Client und dem Broker vergehen kann. Der MQTT-Client muss sicherstellen, dass bei zusätzlich fehlender Kommunikation ein PINGREQ-Paket gesendet wird. Durch das Keepalive-Intervall können der Client und der Broker erkennen, dass das Netz fehlgeschlagen ist und somit die Verbindung unterbrochen wird, ohne dass das TCP/IP-Zeitlimit erreicht wird.

Wenn die {{site.data.keyword.iot_short_notm}}-MQTT-Clients gemeinsam genutzte Subskriptionen verwenden, darf der Wert für das Keepalive-Intervall nur zwischen 1 und 3600 Sekunden liegen. Wenn der Wert '0' oder ein Wert höher als '3600' angefordert wird, legt der {{site.data.keyword.iot_short_notm}}-Broker das Keepalive-Intervall auf 3600 Sekunden fest.
