---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot4auto_short}} verwalten
{: #1stanchor}
Letzte Aktualisierung: 29. Juli 2016
{: .last-updated}

Sie können Ihre Instanz des Service {{site.data.keyword.iot4auto_full}} mithilfe der Administrationskonsole im {{site.data.keyword.Bluemix_notm}}-Dashboard verwalten. In der Administrationskonsole können Sie Parameter für {{site.data.keyword.iot4auto_short}} konfigurieren und die Daten verwalten, die im Service gespeichert werden. Sie können außerdem die Tenantinformationen anzeigen und das Tenantkennwort zurücksetzen.

{:shortdesc}

## Administrationskonsole starten
{: #start_admin_console}

Gehen Sie wie folgt vor, um auf die Administrationskonsole für den Service {{site.data.keyword.iot4auto_short}} zuzugreifen:

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Kachel für den Service {{site.data.keyword.iot4auto_short}}.
2. Wählen Sie die Ansicht **Verwalten** der Serviceinstanz aus.
Notieren Sie sich die Benutzernamens- und Kennwortberechtigungsnachweise, da Sie diese zu einem späteren Zeitpunkt benötigen. Für den Zugriff auf die Administrationskonsole ist Ihre IBM ID erforderlich; diese ist möglicherweise nicht mit Ihren {{site.data.keyword.Bluemix_notm}}-Berechtigungsnachweisen identisch.
3. Klicken Sie auf **Starten** und geben Sie Ihre IBM ID-Berechtigungsnachweise ein, wenn Sie dazu aufgefordert werden.
4. Klicken Sie auf **ANMELDEN**. Daraufhin wird das Fenster mit der **Administrationskonsole** geöffnet.

## Tenantinformationen verwalten
{: #view_tenant_info}

Klicken Sie auf **Tenantinformationen**, um die Tenantinformationen anzuzeigen.

### Tenantkennwort zurücksetzen
{: #reset_tenant_password}

Gehen Sie wie folgt vor, um das Tenantkennwort zurückzusetzen:

1. Klicken Sie im Fenster **Tenantinformationen** auf **ZURÜCKSETZEN**.
2. Klicken Sie in dem Dialogfeld auf **OK**.
Es wird ein neues Kennwort generiert und in der Ansicht **Tenantinformationen** angezeigt.
**Wichtig:** Stellen Sie sicher, dass Sie das Kennwort in allen Ihren Anwendungen aktualisieren, die auf die {{site.data.keyword.iot4auto_short}}-API zugreifen.

## Serviceparameter konfigurieren
{: #configure_parameters}

Mit Serviceparametern wird gesteuert, wie die Reisedaten analysiert werden. Gehen Sie wie folgt vor, um die Serviceparameter zu ändern:

1. Öffnen Sie die Ansicht **Parameter** und passen Sie die folgenden Serviceparameter an:
  - Klicken Sie auf die Registerkarte **Verhalten** und aktualisieren Sie die [Parameter für das Fahrverhalten](#behavior_parameters) so, dass sie Ihren Anforderungen entsprechen.
  - Klicken Sie auf die Registerkarte **Verhalten** und aktualisieren Sie die [Parameter für die Kontextzuordnung](#context_parameters) so, dass sie Ihren Anforderungen entsprechen.
2. Klicken Sie auf **Speichern**.
3. Klicken Sie auf **OK**.

Die aktualisierten Parameterwerte werden auf den nächsten eingereichten Job angewendet.

### Parameter für das Fahrverhalten
{: #behavior_parameters}


In der folgenden Tabelle werden die Parameter für das Fahrverhalten für die von Ihnen auf der Registerkarte **Verhalten** konfigurierten Kategorien beschrieben.

#### Einstellungen für Geschwindigkeitsbegrenzung

Sie können die Geschwindigkeitsbegrenzung für jeden Straßentyp in km/h angeben. Wenn die Geschwindigkeit den von Ihnen für den Straßentyp angegebenen Grenzwert für die Geschwindigkeit überschreitet, wird eine Geschwindigkeitsübertretung festgestellt.

|Parametername|Beschreibung|Standardwert (km/h)|
|:--------|:--------|:-------|
|Autobahn|Geschwindigkeitsbegrenzung für den Straßentyp 'Autobahn'|120|
|Stadtautobahn|Geschwindigkeitsbegrenzung für den Straßentyp 'Stadtautobahn'|90|
|Schnellstraße|Geschwindigkeitsbegrenzung für den Straßentyp 'Schnellstraße'|60|
|Hauptstraße|Geschwindigkeitsbegrenzung für den Straßentyp 'Hauptstraße'|40|
|Andere|Geschwindigkeitsbegrenzung für andere Straßentypen|30|
|Unbekannt|Geschwindigkeitsbegrenzung für unbekannte Straßentypen|120|
*Tabelle 1. Konfigurationsparameter für die Geschwindigkeitsbegrenzung*

#### Einstellungen für Wendeaktionen

|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Winkelgeschwindigkeit (Min \- Max, Grad/s)|Normale Winkelgeschwindigkeit bei einem Wendevorgang. Der Mindestwert wird als Grenzwert für die Erkennung eines Wendesegments verwendet. Der Maximalwert wird für die Erkennung einer scharfen Wende verwendet.|10 \- 25|
|Durchschnittsgeschwindigkeit (km/h)|Normale Geschwindigkeit beim Wenden. Dieser Wert wird zur Ermittlung von Verhalten in einem Wendesegment mit Werten für die Winkelgeschwindigkeit verwendet.|60|
*Tabelle 2. Konfigurationsparameter für das Wenden eines Fahrzeugs*

#### Einstellungen für das Fahrverhalten unter Müdigkeitserscheinungen

|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Zeitdauer kontinuierlichen Fahrens (s)|Die maximale Dauer für kontinuierliches Fahren, die zulässig ist.|10800|
*Tabelle 3. Konfigurationsparameter für die Feststellung des Fahrverhaltens unter Müdigkeitserscheinungen*

### Parameter für die Kontextzuordnung
{: #context_parameters}

In der folgenden Tabelle werden die Parameter für die Kontextzuordnung für die von Ihnen auf der Registerkarte **Kontext** konfigurierten Kategorien beschrieben.

#### Einstellungen für Zeitzone und Zeitraum

Geben Sie für jeden Zeitraum die Zeitzone und die Stunden an.

|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Analysezeitzone|Für die Analyse angewendete Zeitzone. |+00:00|
|Tageszeit|Zeitraum der Tageszeit.|1030 \- 1730|
|Nachtzeit|Zeitraum der Nachtzeit.|2030 \- 0700|
|Morgendliche Stoßzeit|Zeitraum der morgendlichen Stoßzeit.|0700 \- 1030|
|Abendliche Stoßzeit|Zeitraum der abendlichen Stoßzeit.|1730 \- 2030|
*Tabelle 4. Konfigurationsparameter für Zeitzone und Zeitraum*

#### Straßentypen

Die Straßentypparameter werden für die Zuordnung der Straßentypwerte aus Ihren Eingabedaten zu den {{site.data.keyword.iot4auto_short}}-Straßentypklassifikationen verwendet. Wenn Sie nicht über einen Wert für den Straßentyp verfügen, können Sie den Wert für den Straßentyp abrufen, indem Sie den REST-API-Befehl `getLinkInformation` verwenden, der vom Service {{site.data.keyword.iotmapinsights_short}} bereitgestellt wird.

Der Straßentypparameter wird im Abschnitt für die Eigenschaften der JSON-Antwort vom Typ `getLinkInformation` zurückgegeben und gespeichert und als `type` definiert; Informationen hierzu finden Sie im Abschnitt [Beispiel für eine JSON-Antwort für `getLinkInformation`](#sampleJson).


|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Autobahn|Der Wert für den Straßentyp, der 'Autobahn' zugeordnet ist.|1|
|Stadtautobahn|Der Wert für den Straßentyp, der 'Stadtautobahn' zugeordnet ist.|2|
|Schnellstraße|Der Wert für den Straßentyp, der 'Schnellstraße' zugeordnet ist.|3|
|Hauptstraße|Der Wert für den Straßentyp, der 'Hauptstraße' zugeordnet ist.|4|
|Andere|Der Wert für den Straßentyp, der 'Andere' zugeordnet ist.|5|
*Tabelle 5. Konfigurationsparameter für den Straßentyp*

#### Schwellenwert für Geschwindigkeit

Die Schwellenwertparameter für die Geschwindigkeit definieren den mittleren Geschwindigkeitsbereich für jeden Straßentyp in km/h. Der mittlere Geschwindigkeitsbereich ist ein Bereich zwischen den niedrigsten und den höchsten angegebenen Werten.

|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Autobahn|Mittlerer Geschwindigkeitsbereich für den Straßentyp 'Autobahn'.|55 \- 85|
|Stadtautobahn|Mittlerer Geschwindigkeitsbereich für den Straßentyp 'Stadtautobahn'.|35 \- 65|
|Schnellstraße|Mittlerer Geschwindigkeitsbereich für den Straßentyp 'Schnellstraße'.|20 \- 40|
|Hauptstraße|Mittlerer Geschwindigkeitsbereich für den Straßentyp 'Hauptstraße'.|15 \- 35|
|Andere|Mittlerer Geschwindigkeitsbereich für den Straßentyp 'Andere'.|10 \- 20|
|Unbekannt|Mittlerer Geschwindigkeitsbereich für den Straßentyp 'Unbekannt'.|20 \- 60|
*Tabelle 6. Konfigurationsparameter für den Geschwindigkeitsschwellenwert*


### Beispiel für eine JSON-Antwort für `getLinkInformation`
{: #sampleJson}

Bei dem folgenden Codebeispiel handelt es sich um ein Beispiel für eine JSON-Antwort für den REST-API-Befehl `getLinkInformation`:

```
{
	"links": [{
		"internal_link_id": "32088220365736308",
		"external_link_id": "3846419005",
		...
		"properties": {
			"type": "5",
			...
		},
		...
	}]
}
```
{: screen}

## Im Service gespeicherte Daten löschen
{: #managedata}

Die Autotestdaten, die Kontextdaten und die Analyseergebnisse werden so lange im Service gespeichert, bis sie gelöscht werden.

Gehen Sie wie folgt vor, um die im Service gespeicherten Daten zu löschen:

1. Klicken Sie auf **Datenmanagement**, um die Daten zum Autotest sowie zum Analyseergebnis anzuzeigen.
2. Wählen Sie einen Datensatz aus und klicken Sie anschließend auf **LÖSCHEN**.
