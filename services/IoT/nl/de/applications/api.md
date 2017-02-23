---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-12-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP-REST-API für Anwendungen
{: #api}

Verwenden Sie die {{site.data.keyword.iot_full}}-HTTP-REST-API, um Anwendungen zu erstellen und anzupassen, die mit Ihrer in {{site.data.keyword.iot_short_notm}} vorhandenen Organisation interagieren.
{:shortdesc}

## Funktionalität
{: #capabilities}

Die {{site.data.keyword.iot_short_notm}}-HTTP-REST-API unterstützt folgende Funktionalität sowie Funktionen für Anwendungen:

- Abrufen von Organisationsinformationen
- Massenoperationen für Geräte (auflisten, hinzufügen und entfernen)
- Operationen mit Gerätetypen (auflisten, erstellen, löschen, Details anzeigen und aktualisieren)
- Geräteoperationen (auflisten, hinzufügen, entfernen, Details anzeigen, aktualisieren, Position anzeigen und Managementinformationen anzeigen)
- Operationen zur Gerätediagnose (Protokolle löschen, Protokolle abrufen, Protokollinformationen hinzufügen, Protokolle löschen, bestimmte Protokolle abrufen, Fehlercodes löschen, Gerätefehlercodes abrufen und Fehlercodes hinzufügen)
- Problembestimmung bei Verbindungsproblemen (Protokollereignisse für Geräteverbindung auflisten)
- Cache für zuletzt gemeldete Ereignisse (letztes Ereignis für ein bestimmtes Gerät anzeigen)
- Anforderungsoperationen für Gerätemanagement (Gerätemanagementanforderungen auflisten, Anforderungen initiieren, Anforderungsstatus löschen, Anforderungsdetails abrufen, alle Anforderungsstatusarten nach Gerät auflisten, Geräteanforderungsstatus für ein bestimmtes Gerät abrufen)
- Operationen der Nutzungsverwaltung (gesamten belegten Speicherplatz abrufen)
- Publizieren von Geräteereignissen (Beta)
- Abfragen des Servicestatus (Servicestatusangaben nach Organisation abrufen)

## Zugriff auf die Dokumentation der HTTP-REST-API
{: #api_link}

Für den Zugriff auf die Dokumentation der {{site.data.keyword.iot_short_notm}}-HTTP-REST-API und zum Abrufen weiterer Informationen zur Vorgehensweise beim Erstellen und Anpassen Ihrer Anwendungen rufen Sie die Webadresse https://docs.internetofthings.ibmcloud.com/swagger/v0002.html auf.

Nur Version 2 der {{site.data.keyword.iot_short_notm}}-HTTP-REST-API ist unterstützt. Stellen Sie sicher, dass Ihre {{site.data.keyword.iot_short_notm}}-Lösungen Version 2 verwenden.



# HTTP-REST-Messaging-API für Anwendungen
{: #rest_messaging_api}

## Ereignisse und Befehle publizieren
{: #event_command_publication}

Zusätzlich zur Verwendung des MQTT-Nachrichtenprotokolls können Sie Ihre Anwendungen auch so konfigurieren, dass Ereignisse und Befehle in {{site.data.keyword.iot_short_notm}} über HTTP mithilfe eines der folgenden HTTP-REST-API-Befehle publiziert werden:

### Nicht sichere POST-Anforderung für Ereignisse
<pre class="pre">http://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

### Sichere POST-Anforderung für Ereignisse
<pre class="pre">https://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

**Hinweis:** Port 443, der SSL-Standardport, kann auch für sichere HTTP-API-Aufrufe angegeben werden.

### Nicht sichere POST-Anforderung für Befehle
<pre class="pre">http://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/commands/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

### Sichere POST-Anforderung für Befehle
<pre class="pre">https://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">Typ-Id</var>/devices/<var class="keyword varname">Geräte-ID</var>/commands/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

Wenn Sie eine Verbindung zwischen einem Gerät oder einer Anwendung und dem Quickstart-Service herstellen wollen, ersetzen Sie **Organisations-ID** durch die Zeichenfolge 'quickstart'.

**Hinweise:** 
- Zwar können Anwendungen eine HTTP-Verbindung wiederverwenden, um Ereignisse oder Befehle an andere Geräte zu posten, der HTTP-Header für die Berechtigung kann jedoch nicht geändert werden. 
- Port 443, der SSL-Standardport, kann auch für sichere HTTP-API-Aufrufe angegeben werden.

### Authentifizierung

Alle Anforderungen müssen einen Berechtigungsheader enthalten. Die Basisauthentifizierung ist die einzige Methode, die unterstützt ist. Anwendungen werden mithilfe von API-Schlüsseln authentifiziert. Wenn eine Anwendung über die {{site.data.keyword.iot_short_notm}}-HTTP-REST-API eine Anforderung ausgibt, sind folgende Berechtigungsnachweise erforderlich:

```
username = API-Schlüssel (Beispiel: a-Organisations-ID-a84ps90Ajs)
password = Authentifizierungstoken
```

### Anforderungsheader des Typs 'Content-Type'

Zusammen mit der Anforderung muss ein Anforderungsheader des Typs `Content-Type` ('Inhaltstyp') angegeben werden. Die folgende Tabelle zeigt die Zuordnung der unterstützten Typen zu den internen {{site.data.keyword.iot_short_notm}}-Formaten.

|Content-Type-Header|Format in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### Servicequalität

Ähnlich der Servicestufe 0 der MQTT-Servicequalität (Zustellung höchstens einmal) bietet das HTTP-REST-Messaging eine Zustellung nicht persistenter Nachrichten, prüft aber, ob die Anforderung richtig ist und an den Server gesendet werden kann, bevor es die HTTP-Antwort sendet. Durch eine Antwort, die den HTTP-Statuscode 200 enthält, wird bestätigt, dass die Nachricht an den Server übermittelt wurde. Wenn Sie entweder die MQTT-Servicequalitätsstufe 'höchstens einmal' oder das HTTP-Äquivalent zum Zustellen von Ereignisnachrichten verwenden, muss das Gerät oder die Anwendung Wiederholungslogik implementieren, damit die Zustellung garantiert ist.


Weitere Informationen zum MQTT-Protokoll und zu den Servicequalitätsstufen für {{site.data.keyword.iot_short_notm}} finden Sie in [MQTT-Messaging](../reference/mqtt/index.html).
