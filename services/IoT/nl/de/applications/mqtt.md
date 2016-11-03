---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# MQTT-Konnektivität für Anwendungen
{: #mqtt}
Letzte Aktualisierung: 31. August 2016
{: .last-updated}

MQTT ist das primäre Protokoll, das Geräte und Anwendungen für die Kommunikation mit {{site.data.keyword.iot_full}} verwenden. Es werden Clientbibliotheken, Informationen und Beispiele bereitgestellt, die Sie verwenden können, um für Ihre {{site.data.keyword.iot_short_notm}}-Anwendungen Verbindungen herzustellen und sie zu integrieren.
{:shortdesc}

## Clientverbindungen
{: #client_connections}

Informationen zur Clientsicherheit und zur Vorgehensweise beim Herstellen von Verbindungen zwischen MQTT-Clients und Anwendungen in {{site.data.keyword.iot_short_notm}} finden Sie in [Anwendungen, Geräte und Gateways mit {{site.data.keyword.iot_short_notm}} verbinden](../reference/security/connect_devices_apps_gw.html).

## MQTT-Authentifizierung
{: #mqtt_authentication}

Damit {{site.data.keyword.iot_short_notm}}-Anwendungen eine Verbindung zu einer Organisation herstellen können, ist ein API-Schlüssel erforderlich. Nach der Registrierung eines API-Schlüssels wird ein Authentifizierungstoken generiert, das zusammen mit diesem API-Schlüssel verwendet werden muss.

Das folgende Beispiel zeigt einen typischen API-Schlüssel:

<pre class="pre">a-<var class="keyword varname">Organisations-ID</var>-a84ps90Ajs</pre>
{: codeblock}


Das folgende Beispiel zeigt ein typisches Authentifizierungstoken: 

```
MP$08VKz!8rXwnR-Q*
```

Wenn Sie mithilfe eines API-Schlüssels eine MQTT-Verbindung herstellen, müssen Sie sicherstellen, dass folgende Richtlinien angewendet werden:

- Die MQTT-Client-ID hat das folgende Format: a:*Organisations-ID*:*Anwendungs-ID*
- Der MQTT-Benutzername ist der API-Schlüssel (Beispiel: a-*Organisations-ID*-a84ps90Ajs)
- Das MQTT-Kennwort ist das Authentifizierungstoken (Beispiel: MP$08VKz!8rXwnR-Q*)


## Geräteereignisse publizieren
{: #publishing_device_events}

Eine Anwendung kann Ereignisse so publizieren, als stammten diese von einem beliebigen registrierten Gerät, zum Beispiel:

-  Publish to topic iot-2/type/*Gerätetyp*/id/*Geräte-ID*/evt/*Ereignis-ID*/fmt/*Format_Zeichenfolge*

Um vorhandene Daten von einem Gerät an {{site.data.keyword.iot_short_notm}} zu übertragen, können Sie eine Anwendung erstellen, mit der die Daten verarbeitet und in {{site.data.keyword.iot_short_notm}} publiziert werden.

**Wichtig:** Der Umfang der Nachrichtennutzdaten ist auf maximal 131072 Byte begrenzt. Nachrichten, die den Grenzwert überschreiten, werden abgelehnt.

## Gerätebefehle publizieren
{: #publishing_device_commands}

Eine Anwendung kann einen Befehl in einem beliebigen registrierten Gerät publizieren, zum Beispiel:

-  Publish to topic iot-2/type/*Gerätetyp*/id/*Geräte-ID*/cmd/*Befehls-ID*/fmt/*Format_Zeichenfolge*

## Geräteereignisse subskribieren
{: #subscribe_device_events}

Eine Anwendung kann Ereignisse von mindestens einem Gerät subskribieren, zum Beispiel:

-  Subscribe to topic iot-2/type/*Gerätetyp*/id/*Geräte-ID*/evt/*Ereignis-ID*/fmt/*Format_Zeichenfolge*

**Hinweis:** Um mehr als einen Ereignistyp oder um Ereignisse von mehr als einem Gerät zu subskribieren, verwenden Sie für jede der folgenden Komponenten das MQTT-Platzhalterzeichen für 'beliebig' (+):

- Gerätetyp
- Geräte-ID
- Ereignis-ID
- Format_Zeichenfolge

## Gerätebefehle subskribieren
{: #subscribe_device_commands}

Eine Anwendung kann Befehle subskribieren, die an mindestens ein Gerät gesendet werden, zum Beispiel:

-  Subscribe to topic iot-2/type/*Gerätetyp*/id/*Geräte-ID*/cmd/*Befehls-ID*/fmt/*Format_Zeichenfolge*

**Hinweis:** Um mehr als einen Ereignistyp oder um Ereignisse von mehr als einem Gerät zu subskribieren, verwenden Sie für jede der folgenden Komponenten das MQTT-Platzhalterzeichen für 'beliebig' (+):

-  Gerätetyp
-  Geräte-ID
-  Befehls-ID
-  Format_Zeichenfolge

## Gerätestatusnachrichten subskribieren
{: #subscribe_device_status}

Eine Anwendung kann den Überwachungsstatus mindestens eines Geräts subskribieren, zum Beispiel:

-  Subscribe to topic iot-2/type/*Gerätetyp*/id/*Geräte-ID*/mon

**Hinweis:** Um Aktualisierungen von mehr als einem Gerät zu subskribieren, verwenden Sie für jede der folgenden Komponenten das MQTT-Platzhalterzeichen für 'beliebig' (+):

- Gerätetyp
- Geräte-ID

## Anwendungsstatusnachrichten subskribieren
{: #subscribe_app_status}

Eine Anwendung kann den Überwachungsstatus mindestens einer Anwendung subskribieren, zum Beispiel:

- Subscribe to topic iot-2/app/*Anwendungs-ID*/mon

**Hinweis:** Um Aktualisierungen für alle Anwendungen zu subskribieren, verwenden Sie für die Komponente *Anwendungs-ID* das MQTT-Platzhalterzeichen für 'beliebig' (+):


## Quickstart-Einschränkungen
{: #quickstart_restrictions}
Wenn Sie planen, Anwendungscode zur Verwendung mit dem Quickstart-Service zu erstellen, werden folgende Funktionen in Quickstart nicht unterstützt:

- Befehle publizieren
- Befehle subskribieren
- Verwendung des MQTT-Platzhalterzeichens für 'beliebig' (+) in den Komponenten **Gerätetyp** oder **Anwendungs-ID**
- MQTT-Verbindung über Transport Layer Security (TLS)
- Skalierbare Anwendungen

## Skalierbare Anwendungen
{: #scalable_apps}

Durch Anpassen der Art und Weise, wie Ihre Anwendungen Verbindungen herstellen, können Sie Ihre {{site.data.keyword.iot_short_notm}}-Anwendungen skalierbarer machen. Teilen Sie dazu die Verarbeitung der Ereignisnachrichtenlast auf mehrere Instanzen einer Anwendung auf.

Die Anzahl der Clients, die für einen optimalen Lastausgleich und eine optimale Skalierbarkeit erforderlich sind, ist je nach Bereitstellung unterschiedlich. Um die optimale Anzahl von Clients zu ermitteln, müssen Sie für Ihr System einen Stresstest ausführen.

Stellen Sie zum Aktivieren der Lastverteilung sicher, dass die Anwendungssubskription nicht permanent ist und dass die Client-ID in der Subskription mit dem folgenden Format übereinstimmt:

<pre class="pre">A:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Anwendungs-ID</var></pre>
{: codeblock}

Dabei gilt: 
-  Das Zeichen **A** gibt an, dass es sich bei dem Client um eine skalierbare Anwendung handelt.
-  *Organisations-ID* ist die aus sechs Zeichen bestehende eindeutige Organisations-ID, die generiert wurde, als Sie die beim ersten Registrieren des Service zugeordnete alphanumerische Zeichenfolge des Service registriert haben. 
-  *Anwendungs-ID* ist eine benutzerdefinierte eindeutige Zeichenfolge-ID für den Client. Die Zeichenfolge kann nur alphanumerische Zeichen (a-z, A-Z, 0-9) und als Sonderzeichen den Gedankenstrich (-), das Unterstreichungszeichen (_) und den Punkt (.) enthalten. 

**Wichtig:**
- Für skalierbare Anwendungen werden nur Subskriptionen unterstützt, die nicht permanent sind.
- Die Client-ID muss mit dem Zeichen **A** in Großschreibung beginnen, um von {{site.data.keyword.iot_short_notm}} ordnungsgemäß als skalierbare Anwendung bezeichnet zu werden.
- Andere Clients, die Teil der skalierbaren Anwendung sind, müssen dieselbe Client-ID verwenden.


### Funktionsweise

Der {{site.data.keyword.iot_short_notm}}-Service erweitert die Spezifikation des Nachrichtenprotokolls von MQTT Version 3.1.1, um gemeinsam genutzte Subskriptionen zu unterstützen. Gemeinsam genutzte Subskriptionen stellen für Anwendungen Funktionen für den Lastausgleich zur Verfügung. Eine gemeinsam genutzte Subskription ist möglicherweise erforderlich, wenn eine Back-End-Unternehmensanwendung den Umfang der Nachrichten, die in einem bestimmten Topic-Bereich publiziert werden sollen, nicht verarbeiten kann. Wenn beispielsweise viele Geräte Nachrichten publizieren, die von einer einzigen Anwendung verarbeitet werden, ist es möglicherweise erforderlich, die Lastausgleichsfunktion einer gemeinsam genutzten Subskription zu verwenden. Die {{site.data.keyword.iot_short_notm}}-Unterstützung gemeinsam genutzter Subskriptionen ist auf nicht permanente Subskriptionen eingeschränkt.


**Beispiel**

Das folgende Szenario ist ein Beispiel dafür, wie eine skalierbare Anwendung in {{site.data.keyword.iot_short_notm}} funktioniert:

- Der erste Client stellt als **A:abc123:myApplication** eine Verbindung her und subskribiert alle Geräteereignisse; dies bedeutet, dass der erste Client 100 % der publizierten Geräteereignisse empfängt.
- Der zweite Client stellt als **A:abc123:myApplication** eine Verbindung her und subskribiert ebenfalls alle Geräteereignisse; dies bedeutet, dass der erste und der zweite Client alle publizierten Ereignisse gemeinsam nutzen. Die Systembelastung wird zwischen dem ersten und dem zweiten Client aufgeteilt.
- Der dritte Client stellt als **A:abc123:myApplication** eine Verbindung her und subskribiert ebenfalls alle Geräteereignisse; dies bedeutet, dass der erste, der zweite und der dritte Client die aufgrund der Ereignisse vorhandene Systembelastung teilen.
- Der zweite und der dritte Client beenden anschließend die Subskription der Geräteereignisse; dies bedeutet, dass nur der erste Client alle publizierten Geräteereignisse empfängt. Während die Verbindung des zweiten und des dritten Clients zum Service weiterhin besteht, empfängt der erste Client 100 % der publizierten Geräteereignisse.
- Wenn zwei oder mehr Anwendungen eine Subskription gemeinsam nutzen, treffen Nachrichten möglicherweise nicht in derselben Reihenfolge ein, in der sie gesendet wurden. Beispielsweise kann Nachricht B beim ersten Client eintreffen, bevor Nachricht A beim zweiten Client eintrifft, obwohl Nachricht A zuerst gesendet wurde.
