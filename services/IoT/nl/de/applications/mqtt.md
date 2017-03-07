---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# MQTT-Konnektivität für Anwendungen
{: #mqtt}

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

Um vorhandene Daten von einem Gerät an {{site.data.keyword.iot_short_notm}} zu senden, können Sie eine Anwendung erstellen, mit der die Daten verarbeitet und in {{site.data.keyword.iot_short_notm}} publiziert werden.

**Wichtig:** Der Umfang der Nachrichtennutzdaten ist auf maximal 131072 Byte begrenzt.  Nachrichten, die den Grenzwert überschreiten, werden abgelehnt.

### Aufbewahrte Nachrichten
{{site.data.keyword.iot_short_notm}}-Organisationen sind nicht dazu berechtigt, aufbewahrte MQTT-Nachrichten zu publizieren. Wenn eine Anwendung, ein Gateway oder ein Gerät eine aufbewahrte Nachricht sendet, überschreibt der {{site.data.keyword.iot_short_notm}}-Service das Flag für aufbewahrte Nachricht, sofern es auf den Wert 'true' gesetzt ist, und verarbeitet die Nachricht so, als wäre das Flag auf 'false' gesetzt.

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

Skalierbare Anwendungen werden als nicht permanente Subskriptionen definiert oder als gemeinsam genutzte Subskriptionen mit variabler Permanenz (Beta).

### Nicht permanente Subskriptionen
{: #shared_sub_non_durable}

Stellen Sie zum Aktivieren der Lastverteilung sicher, dass die Anwendungssubskription nicht permanent ist und dass die Client-ID in der Subskription mit dem folgenden Format übereinstimmt:

<pre class="pre">A:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Anwendungs-ID</var></pre>
{: codeblock}

Dabei gilt:
-  Das Zeichen **A** gibt an, dass es sich bei dem Client um eine skalierbare Anwendung handelt.
-  *Organisations-ID* ist die aus sechs Zeichen bestehende eindeutige Organisations-ID, die beim Registrieren des Service generiert wurde.
-  *Anwendungs-ID* ist eine benutzerdefinierte eindeutige Zeichenfolge-ID für den Client. Die Zeichenfolge kann nur alphanumerische Zeichen (a-z, A-Z, 0-9) und als Sonderzeichen den Gedankenstrich (-), das Unterstreichungszeichen (_) und den Punkt (.) enthalten.


**Wichtig:**
- Die Client-ID muss mit dem Zeichen **A** in Großschreibung beginnen, um von {{site.data.keyword.iot_short_notm}} ordnungsgemäß als skalierbare Anwendung bezeichnet zu werden.
- Andere Clients, die Teil der skalierbaren Anwendung sind, müssen dieselbe Client-ID verwenden.
- Der Sitzungsbereinigungswert für nicht permanente Subskriptionen muss auf 'false' (0) festgelegt werden.

### Gemeinsam genutzte Subskriptionen mit variabler Permanenz (Beta)
{: #shared_sub_mixed}

Der {{site.data.keyword.iot_short_notm}}-Service erweitert die Spezifikation des Nachrichtenprotokolls von MQTT V3.1.1, um einen Beta-Test für gemeinsam genutzte Subskriptionen mit variabler Permanenz zu unterstützen. Gemeinsam genutzte Subskriptionen stellen für Anwendungen Funktionen für den Lastausgleich zur Verfügung. Eine gemeinsam genutzte Subskription ist möglicherweise erforderlich, wenn eine Back-End-Unternehmensanwendung den Umfang der Nachrichten, die in einem bestimmten Topic-Bereich publiziert werden sollen, nicht verarbeiten kann. Wenn beispielsweise viele Geräte Nachrichten publizieren, die von einer einzigen Anwendung verarbeitet werden, ist es möglicherweise erforderlich, die Lastausgleichsfunktion einer gemeinsam genutzten Subskription zu verwenden.

Stellen Sie bei gemeinsam genutzten Subskriptionen mit variabler Permanenz sicher, dass die Client-ID in der Subskription mit dem folgenden Format übereinstimmt:

<pre class="pre">A:<var class="keyword varname">Organisations-ID</var>:<var class="keyword varname">Anwendungs-ID</var>:<var class="keyword varname">Instanz-ID</var></pre>
{: codeblock}

Dabei gilt:
- Die Zeichen für **A**, *Organisations-ID* und *Anwendungs-ID* in der Client-ID werden auf die gleiche Weise definiert wie bei [nicht permanenten Subskriptionen](#shared_sub_non_durable).
- Die Zeichenfolge für *Instanz-ID* darf maximal 36 Zeichen umfassen und nur die folgenden Zeichen enthalten:
   - Alphanumerische Zeichen (a-z, A-Z, 0-9)
   - Gedankenstriche (-)
   - Unterstreichungszeichen (_)
   - Punkte (.)

**Wichtig:**
- Unterstützung für gemeinsam genutzte Subskriptionen mit variabler Permanenz wird nur als Betafunktion bereitgestellt. Implementieren Sie Betafunktionen nicht in Produktionsanwendungen.
- Der Wert für bereinigte Sitzung kann in gemeinsam genutzten Subskriptionen mit variabler Permanenz auf 'true' (1) oder 'false' (0) gesetzt werden.
- Clients, die Verbindungen mit der Instanz-ID herstellen, verwenden andere Subskriptionen als Clients, die Verbindungen ohne die Instanz-ID herstellen. Wenn mehrere Clients Verbindungen in einer gemeinsam genutzten Subskription mit variabler Permanenz herstellen sollen, müssen Sie daher die Instanz-ID in allen Subskriptionen angeben.

**Beispielszenario**

Das folgende Szenario ist ein Beispiel dafür, wie eine nicht permanente skalierbare Anwendung in {{site.data.keyword.iot_short_notm}} funktioniert:

- Der erste Client stellt als **A:abc123:myApplication** eine Verbindung her und subskribiert alle Geräteereignisse; dies bedeutet, dass der erste Client 100 % der publizierten Geräteereignisse empfängt.
- Client 2 stellt als **A:abc123:myApplication** eine Verbindung her und subskribiert außerdem alle Geräteereignisse. Dies bedeutet, dass Client 1 und Client 2 alle publizierten Ereignisse gemeinsam nutzen. Die Systembelastung wird zwischen dem ersten und dem zweiten Client aufgeteilt.
- Client 3 stellt als **A:abc123:myApplication** eine Verbindung her und subskribiert ebenfalls alle Geräteereignisse. Dies bedeutet, dass Client 1, Client 2 und Client 3 den Verarbeitungsaufwand für Ereignisse miteinander teilen.
- Der zweite und der dritte Client beenden anschließend die Subskription der Geräteereignisse; dies bedeutet, dass nur der erste Client alle publizierten Geräteereignisse empfängt. Während die Verbindung des zweiten und des dritten Clients zum Service weiterhin besteht, empfängt der erste Client 100 % der publizierten Geräteereignisse.
- Wenn zwei oder mehr Anwendungen eine Subskription gemeinsam nutzen, treffen Nachrichten möglicherweise nicht in derselben Reihenfolge ein, in der sie gesendet wurden. Beispielsweise kann Nachricht B beim ersten Client eintreffen, bevor Nachricht A beim zweiten Client eintrifft, obwohl Nachricht A zuerst gesendet wurde.
