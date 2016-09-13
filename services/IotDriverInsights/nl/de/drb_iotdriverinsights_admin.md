---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Analyse des Fahrverhaltens verwalten
{: #1stanchor}
Letzte Aktualisierung: 19. Juni 2016
{: .last-updated}

Verwenden Sie zur Verwaltung Ihrer {{site.data.keyword.iotdriverinsights_full}}-Serviceinstanz die Administrationskonsole im {{site.data.keyword.Bluemix_notm}}-Dashboard. Über die Administrationskonsole können Sie Parameter für {{site.data.keyword.iotdriverinsights_short}} konfigurieren und die im Service gespeicherten Daten verwalten. Außerdem können Sie die Tenantinformationen anzeigen und das Tenantkennwort zurücksetzen. 

{:shortdesc}

## Administrationskonsole starten
{: #start-admin-console}

Gehen Sie wie folgt vor, um auf die Administrationskonsole des {{site.data.keyword.iotdriverinsights_short}}-Service zuzugreifen: 

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Kachel für den {{site.data.keyword.iotdriverinsights_short}}-Service. 
2. Wählen Sie die Ansicht **Verwalten** Ihrer Serviceinstanz aus. Notieren Sie die Berechtigungsnachweise *Benutzername* und *Kennwort*. Für den Zugriff auf die Administrationskonsole benötigen Sie Ihre IBM ID, die unter Umständen nicht mit den Berechtigungsnachweisen für {{site.data.keyword.Bluemix_notm}} identisch ist. 
3. Klicken Sie auf **Starten** und geben Sie bei der entsprechenden Eingabeaufforderung die Berechtigungsnachweise für Ihre IBM ID ein. 
4. Klicken Sie auf **Anmelden**. Die **Administrationskonsole** wird in einem neuen Fenster geöffnet. 

## Tenantinformationen verwalten
{: #viewtenantinfo}

Klicken Sie zum Anzeigen der Tenantinformationen auf **Tenantinformationen**. 

### Tenantkennwort zurücksetzen
{: #resettenantpassword}

Gehen Sie wie folgt vor, um das Tenantkennwort zurückzusetzen: 

1. Klicken Sie im Fenster **Tenantinformationen** auf **Zurücksetzen**.
2. Klicken Sie im Bestätigungsdialogfenster auf **OK**. Ein neues Kennwort wird generiert und in der Ansicht **Tenantinformationen** angezeigt.
**Wichtig:** Stellen Sie sicher, dass Sie das Kennwort in allen Anwendungen aktualisieren, die auf die {{site.data.keyword.iotdriverinsights_short}}-API zugreifen. 

## Serviceparameter konfigurieren
{: #configureparameters}

Serviceparameter steuern, wie die Fahrtdaten analysiert werden. Gehen Sie wie folgt vor, um die Serviceparameter zu ändern: 

1. Öffnen Sie die Ansicht **Parameter** und passen Sie die folgenden Serviceparameter nach Bedarf an: 
  - Klicken Sie auf die Registerkarte **Verhalten** und aktualisieren Sie die [Parameter für das Fahrverhalten](#behavior_parameters), sodass sie Ihren Anforderungen entsprechen. 
  - Klicken Sie auf die Registerkarte **Kontext** und aktualisieren Sie die [Parameter für die Kontextzuordnung](#context_parameters), sodass sie Ihren Anforderungen entsprechen. 
2. Klicken Sie auf **Speichern**.
3. Klicken Sie auf **OK**. 

Die aktualisierten Parameterwerte werden auf den nächsten Job angewendet, der übergeben wird. 

### Parameter für das Fahrverhalten
{: #behavior_parameters}

In den folgenden Tabellen werden die Parameter für das Fahrverhalten der Kategorien erläutert, die Sie auf der Registerkarte **Verhalten** konfigurieren können. 

#### Geschwindigkeitsbegrenzung - Einstellungen

Sie können die Geschwindigkeitsbegrenzung in km/h für jede Straßenkategorie angeben. Wenn die Geschwindigkeit den von Ihnen für die Straßenkategorie angegebenen Wert für die Geschwindigkeitsbegrenzung überschreitet, wird eine Geschwindigkeitsüberschreitung festgestellt. 

|Parametername|Beschreibung|Standardwert (km/h)|
|:--------|:--------|:-------|
|Autobahn|Geschwindigkeitsbegrenzung für die Straßenkategorie 'Autobahn'.|120|
|Stadtautobahn|Geschwindigkeitsbegrenzung für die Straßenkategorie 'Stadtautobahn'.|90|
|Schnellstraße|Geschwindigkeitsbegrenzung für die Straßenkategorie 'Schnellstraße'.|60|
|Hauptstraße|Geschwindigkeitsbegrenzung für die Straßenkategorie 'Hauptstraße'.|50|
|Nebenstraßen|Geschwindigkeitsbegrenzung für die Straßenkategorie 'Nebenstraße'.|30|
|Unbekannt|Geschwindigkeitsbegrenzung für die Straßenkategorie 'Unbekannt'.|120|

#### Wenden - Einstellungen

|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Winkelgeschwindigkeit (Min \- Max, Grad/s)|Normale Winkelgeschwindigkeit beim Wenden. Der Mindestwert wird als Grenzwert für die Erkennung eines Winkelsegments verwendet. Der Maximalwert wird für die Erkennung einer scharfen Wende verwendet. |10 \- 25|
|Durchschnittsgeschwindigkeit (km/h)|Normale Geschwindigkeit beim Wenden. Dieser Wert wird verwendet, um die Verhaltensweisen in einem Winkelsegment zu erkennen, das Werte für die Winkelgeschwindigkeit enthält. |60|

#### Ermüdendes Fahren - Einstellungen

|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Zeitdauer kontinuierlichen Fahrens (s)|Die maximal zulässige Zeitdauer für kontinuierliches Fahren. |10800|


### Parameter für die Kontextzuordnung
{: #context_parameters}

In den folgenden Tabellen werden die Parameter für die Kontextzuordnung der Kategorien erläutert, die Sie auf der Registerkarte **Kontext** konfigurieren können. 

#### Zeitzone und Zeitbereich - Einstellungen

Geben Sie die Zeitzone und die Stunden für jeden Zeitraum an. 

|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Analysezeitzone|Für die Analyse verwendete Zeitzone. |+00:00|
|Tageszeit|Zeitbereich der Tageszeit.|1030 \- 1730|
|Nachtzeit|Zeitbereich der Nachtzeit.|2030 \- 0700|
|Morgendliche Spitze|Zeitbereich der morgendlichen Spitzenzeit.|0700 \- 1030|
|Nachmittägliche Spitze|Zeitbereich der nachmittäglichen Spitzenzeit.|1730 \- 2030|

#### Straßenkategorien

Mithilfe der Parameter für die Straßenkategorie werden die Straßenkategoriewerte Ihrer Eingabedaten den Klassifizierungen für die Straßenkategorien von {{site.data.keyword.iot4auto_short}} zugeordnet. Wenn kein Straßenkategoriewert angegeben ist, können Sie diesen über die REST-API "getLinkInformation" abrufen, die von {{site.data.keyword.iotmapinsights_short}} bereitgestellt wird. 

 Der Wert für die Straßenkategorie wird in der Antwort in "properties > type" gespeichert. Ein Beispiel, aus dem die Position von "type" in der Antwort ersichtlich ist, finden Sie im Abschnitt [Beispiel für eine JSON-Antwort der REST-API "`getLinkInformation`"](#sampleJson). 

 |Parametername|Beschreibung|Standardwert|
 |:--------|:--------|:-------|
|Autobahn|Straßenkategoriewert, der 'Autobahn' zugeordnet ist.|1|
|Stadtautobahn|Straßenkategoriewert, der 'Stadtautobahn' zugeordnet ist.|2|
|Schnellstraße|Straßenkategoriewert, der 'Schnellstraße' zugeordnet ist.|3|
|Hauptstraße|Straßenkategoriewert, der 'Hauptstraße' zugeordnet ist.|4|
|Nebenstraßen|Straßenkategoriewert, der 'Nebenstraßen' zugeordnet ist.|5|

#### Geschwindigkeitsgrenze

Mit den Parametern für die Geschwindigkeitsgrenze wird der mittlere Geschwindigkeitsbereich für jede Straßenkategorie in km/h definiert. Der mittlere Geschwindigkeitsbereich ist der Bereich zwischen dem angegebenen niedrigsten und höchsten Wert. 

|Parametername|Beschreibung|Standardwert|
|:--------|:--------|:-------|
|Autobahn|Mittlerer Geschwindigkeitsbereich für die Straßenkategorie 'Autobahn'.|55 \- 85|
|Stadtautobahn|Mittlerer Geschwindigkeitsbereich für die Straßenkategorie 'Stadtautobahn'.|35 \- 65|
|Schnellstraße|Mittlerer Geschwindigkeitsbereich für die Straßenkategorie 'Schnellstraße'.|20 \- 40|
|Hauptstraße|Mittlerer Geschwindigkeitsbereich für die Straßenkategorie 'Hauptstraße'.|15 \- 35|
|Nebenstraßen|Mittlerer Geschwindigkeitsbereich für die Straßenkategorie 'Nebenstraßen'.|10 \- 20|
|Unbekannt|Mittlerer Geschwindigkeitsbereich für die Straßenkategorie 'Unbekannt'.|20 \- 60|

### Beispiel für eine JSON-Antwort der REST-API "getLinkInformation"
{: #sampleJson}

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


## Im Service gespeicherte Daten verwalten
{: #managedata}

Die Fahrzeugtestdaten, die Kontextdaten und die Analyseergebnisse bleiben im Service gespeichert bis sie gelöscht werden. 

Gehen Sie wie folgt vor, um Daten zu löschen, die im Service gespeichert sind:

1. Klicken Sie auf **Data Management**, um die Fahrzeugtest- und Analyseergebnisdaten anzuzeigen. 
2. Wählen Sie einen Datensatz aus und klicken Sie anschließend in dem Datensatz auf **Löschen**.
