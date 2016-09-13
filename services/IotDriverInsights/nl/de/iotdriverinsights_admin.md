---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iotdriverinsights_short}} verwalten
{: #1stanchor}
*Letzte Aktualisierung: 6 Mai 2016*


Die Verwaltung von {{site.data.keyword.iotdriverinsights_full}} umfasst die Anzeige von Tenantinformationen und das Zurücksetzen des Tenantkennworts, die Konfiguration von Parametern für den Service sowie die Verwaltung von Daten, die im Service gespeichert sind.
{:shortdesc}

Sie können die Administrationsaufgaben mithilfe der Administrationskonsole von {{site.data.keyword.iotdriverinsights_full}} durchführen. 

Gehen Sie wie folgt vor, um auf die Administratorkonsole zuzugreifen: 

1. Wechseln Sie zur Ansicht **Verwalten** Ihrer Serviceinstanz. 
2. Klicken Sie auf **Starten**. Die **Administratorkonsole** wird als neues Fenster geöffnet. 
3. Geben Sie den *Benutzernamen* und das *Kennwort* wie in der Ansicht **Verwalten** dargestellt ein und klicken Sie auf **Anmeldung**.

## Tenantinformationen anzeigen
{: #viewtenantinfo}

Nach der Anmeldung bei der **Administratorkonsole** können Sie die Ansicht **Tenantinformationen** mit den zugehörigen Daten anzeigen. 

## Tenantkennwort zurücksetzen
{: #resettenantpassword}

Führen Sie in der Ansicht **Tenantinformationen** folgende Aktionen aus:  

1. Klicken Sie auf **Zurücksetzen**.
2. Klicken Sie im Bestätigungsdialog auf **OK**.
Anschließend wird das neue Kennwort in der Ansicht **Tenantinformationen** angezeigt.

## Parameter für den Service konfigurieren
{: #configureparameters}

Klicken Sie im Navigationsbereich auf **Parameter**. Die Ansicht **Parameter** wird mit den Parametern angezeigt.

Sie können Parameter bearbeiten, um die Analyseergebnisse zu ändern. 

Die folgende Tabelle beschreibt die Verhaltensparameter:

|Kategorie|Parametername|Beschreibung|Standardwert|
|:-------:|:--------:|:--------|:-------:|
|Geschwindigkeitsbegrenzung (km/h)|\-|Geschwindigkeitsbegrenzung für jede Straßenkategorie. Falls die Geschwindigkeit des Fahrzeugs den Wert für die Straßenkategorie übersteigt, erkennt der Service dies als Geschwindigkeitsüberschreitung. |\-|
|Geschwindigkeitsbegrenzung (km/h)|Autobahn|Geschwindigkeitsbegrenzung für Autobahnen|120|
|Geschwindigkeitsbegrenzung (km/h)|Stadtautobahn|Geschwindigkeitsbegrenzung für Stadtautobahnen|90|
|Geschwindigkeitsbegrenzung (km/h)|Schnellstraße|Geschwindigkeitsbegrenzung für Schnellstraßen|60|
|Geschwindigkeitsbegrenzung (km/h)|Hauptstraße|Geschwindigkeitsbegrenzung für Hauptstraßen|50|
|Geschwindigkeitsbegrenzung (km/h)|Nebenstraßen|Geschwindigkeitsbegrenzung für Nebenstraßen|30|
|Geschwindigkeitsbegrenzung (km/h)|Unbekannt|Geschwindigkeitsbegrenzung für 'Unbekannt'|120|
|Wenden|Winkelgeschwindigkeit (Min \- Max, Grad/s)|Normale Winkelgeschwindigkeit beim Wenden. Der Mindestwert wird als Grenzwert für die Erkennung eines Winkelsegments verwendet. Der Maximalwert wird für die Erkennung einer scharfen Wende verwendet. |10 \- 25|
|Wenden|Durchschnittsgeschwindigkeit (km/h)|Normale Geschwindigkeit beim Wenden. Dieser Wert wird zusammen mit den Werten für die Winkelgeschwindigkeit verwendet, um die Verhaltensweisen in Winkelsegmenten beim Wenden zu erkennen. |60|
|Ermüdendes Fahren|Zeitdauer kontinuierlichen Fahrens (s)|Falls ein Fahrzeug kontinuierlich für eine längere Zeitdauer als in diesem Wert angegeben gefahren wird, erkennt der Service dies als "Ermüdendes Fahren".|10800|

Die folgende Tabelle beschreibt die Kontextparameter: 

|Kategorie|Parametername|Beschreibung|Standardwert|
|:-------:|:--------:|:--------|:-------:|
|Analysezeitzone|\-|Angewendete Zeitzone für die Analyse |+00:00|
|Zeitbereich|\-|Dieser Wert definiert den Typ des Zeitraums.|\-|
|Zeitbereich|Tageszeit|Zeitbereich der Tageszeit|1030 \- 1730|
|Zeitbereich|Nachtzeit|Zeitbereich der Nachtzeit|2030 \- 0700|
|Zeitbereich|Morgendliche Spitze|Zeitbereich der morgendlichen Spitzenzeit|0700 \- 1030|
|Zeitbereich|Nachmittägliche Spitze|Zeitbereich der nachmittäglichen Spitze|1730 \- 2030|
|Straßenkategorie|\-|Diese Werte werden verwendet, um den Wert für die Straßenkategorie des Benutzers in den Eingabedaten mit der für {{site.data.keyword.iotdriverinsights_short}} eindeutigen Klassifizierung der Straßenkategorien abzugleichen. Wenn Sie nicht über einen Wert für die Straßenkategorie verfügen, können Sie den Wert für die Straßenkategorie abrufen, indem Sie die REST-API `getLinkInformation` verwenden, die von **{{site.data.keyword.iotmapinsights_short}}** zur Verfügung gestellt wird. Der Wert für die Straßenkategorie wird in der Antwort in **properties > type** gespeichert. Das Beispiel für JSON ([Sample JSON](#sampleJson)) stellt die Position von `type` in der Antwort dar. |\-|
|Straßenkategorie|Autobahn|Wert für Straßenkategorie zu Autobahn zuordnen|1|
|Straßenkategorie|Stadtautobahn|Wert für Straßenkategorie zu Stadtautobahn zuordnen|2|
|Straßenkategorie|Schnellstraße|Wert für Straßenkategorie zu Schnellstraße zuordnen|3|
|Straßenkategorie|Hauptstraße|Wert für Straßenkategorie zu Hauptstraße zuordnen|4|
|Straßenkategorie|Nebenstraßen|Wert für Straßenkategorie zu Nebenstraßen zuordnen|5|
|Geschwindigkeitsgrenze (Niedrig \- Hoch, km/h)|\-|Dieser Wert definiert den mittleren Geschwindigkeitsbereich für die einzelnen Straßenkategorien. |\-|
|Geschwindigkeitsgrenze (Niedrig \- Hoch, km/h)|Autobahn|Mittlerer Geschwindigkeitsbereich für Autobahn|55 \- 85|
|Geschwindigkeitsgrenze (Niedrig \- Hoch, km/h)|Stadtautobahn|Mittlerer Geschwindigkeitsbereich für Stadtautobahn|35 \- 65|
|Geschwindigkeitsgrenze (Niedrig \- Hoch, km/h)|Schnellstraße|Mittlerer Geschwindigkeitsbereich für Schnellstraße|20 \- 40|
|Geschwindigkeitsgrenze (Niedrig \- Hoch, km/h)|Hauptstraße|Mittlerer Geschwindigkeitsbereich für Hauptstraße|15 \- 35|
|Geschwindigkeitsgrenze (Niedrig \- Hoch, km/h)|Nebenstraßen|Mittlerer Geschwindigkeitsbereich für Nebenstraßen|10 \- 20|
|Geschwindigkeitsgrenze (Niedrig \- Hoch, km/h)|Unbekannt|Mittlerer Geschwindigkeitsbereich für 'Unbekannt'|20 \- 60|


Gehen Sie wie folgt vor, um die Änderungen auf die Parameter anzuwenden:

1. Klicken Sie auf **Speichern**. 
2. Klicken Sie im Bestätigungsdialog auf **OK**.

Anschließend werden neue Parameter angewendet und werden für den nächsten übergebenen Job wirksam. 

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

- Klicken Sie im Navigationsbereich auf **Data Management**. Sie können die Ansicht **Data Management** mit den Daten zum Fahrzeugtest und Analyseergebnis anzeigen. 
- Sie können Daten löschen, indem Sie in einem Datensatz auf **Löschen** klicken. 
