---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerätemanagement erweitern
{: #custom_actions}
Letzte Aktualisierung: 11. Juli 2016
{: .last-updated}

Sie können die Gerätemanagementfunktionen in {{site.data.keyword.iot_full}} erweitern, damit sie Ihren Anforderungen entsprechen, indem Sie entweder mithilfe der REST-API oder des in {{site.data.keyword.Bluemix_notm}} bereitgestellten Dashboards Erweiterungen für das Gerätemanagement hinzufügen.

Folgende Aktionen für das Gerätemanagement werden standardmäßig von {{site.data.keyword.iot_short_notm}} bereitgestellt und unterstützt:
- Neustart für Geräte
- Zurücksetzen auf Werkseinstellungen
- Firmware-Download
- Firmware-Update

Wenn die von {{site.data.keyword.iot_short_notm}} standardmäßig bereitgestellten Geräteaktionen für Ihre Geräte und Anwendungen nicht ausreichend sind, können Sie durch Implementieren eines Erweiterungspackages für das Gerätemanagement zusätzliche Gerätemanagementfunktionen entwickeln.

## Erweiterungspackages für das Gerätemanagement
{: #device_management_ext}

Ein Erweiterungspackage für das Gerätemanagement ist ein JSON-Dokument, das eine Gruppe von Gerätemanagementaktionen definiert. Die Aktionen können auf mindestens einem Gerät, das die Aktionen unterstützt, initiiert werden. Die Aktionen werden entweder mithilfe des {{site.data.keyword.iot_short_notm}}-Dashboards oder der REST-API-Befehle für das Gerätemanagement initiiert.

Das folgende Codebeispiel zeigt das typische Format eines Erweiterungspackages für das Gerätemanagement:

```

	{
		"bundleId": "<eindeutige ID>",
		"displayName": {
			"<Ländereinstellung 0>": "<lokalisierter Anzeigename 0>"
		},
		"description": {
			"<Ländereinstellung 0>": "<lokalisierte Beschreibung 0>"
		},
		"version": "<Bundleversion>",
		"provider": "<Bundle-Provider>",
		"actions": {
			"<Aktions-ID 0>": {
				"actionDisplayName": {
					"<Ländereinstellung 0>": "<lokalisierter Anzeigename der Aktion 0>"
				},
				"description": {
					"<Ländereinstellung 0>": "<lokalisierte Beschreibung>"
				},
				"parameters": [
					{
						"name": "<Parameter-ID>",
						"value": "<Muster für einen regulären Ausdruck zum Überprüfen von Werten>",
						"required": false,
						"defaultValue": "<Standardwert>"
					}
				]
			}
		}
	}

```

### Eigenschaften des Erweiterungspackages

Ein Erweiterungspackage für das Gerätemanagement enthält folgende Eigenschaften:

|Eigenschaft|Beschreibung|Erforderlich
|:---|:---|:---|
|`bundleId`|Eindeutige Kennung für eine Erweiterung für das Gerätemanagement.|Ja|
|`version`|Versionszeichenfolge für eine Erweiterung für das Gerätemanagement.|Nein|
|`provider`|Versionszeichenfolge für eine Erweiterung für das Gerätemanagement, die auf 1024 Zeichen begrenzt ist.|Nein|
|`displayName`|Zuordnung von Schlüssel-Wert-Paaren des Typs `locale`: `String`, die im {{site.data.keyword.iot_short_notm}}-Dashboard angezeigt werden. Sie müssen mindestens einen Eintrag angeben.|Ja|
|`description`|Zuordnung von Schlüssel-Wert-Paaren des Typs `locale`: `String`, die für die Anzeige im {{site.data.keyword.iot_short_notm}}-Dashboard verwendet werden. Falls dies definiert ist, müssen Sie mindestens einen Eintrag angeben.|Nein|
|`actions`| Zuordnung von Schlüssel-Wert-Paaren des Typs `actionId`: `<Aktion>`, die die in einer Gerätemanagementerweiterung enthaltenen Aktionen definieren. Sie müssen mindestens einen Eintrag angeben.|Ja|

### Eigenschaften für jede Aktion:

|Eigenschaft|Beschreibung|Erforderlich
|:---|:---|
|`actionDisplayName`|Zuordnung von Schlüssel-Wert-Paaren des Typs `locale`: `String`, die im {{site.data.keyword.iot_short_notm}}-Dashboard angezeigt werden. Sie müssen mindestens einen Eintrag angeben.|Ja|
|`description`|Zuordnung von Schlüssel-Wert-Paaren des Typs `locale`: `String`, die für die Anzeige im {{site.data.keyword.iot_short_notm}}-Dashboard verwendet werden. Optional. Sie müssen mindestens einen Eintrag angeben.|Nein|
|`parameters`|Array der für eine bestimmte Aktion zulässigen Parameter. Falls dies definiert ist, müssen Sie mindestens einen Eintrag angeben.|Nein|

### Eigenschaften für jeden Aktionsparameter:

|Eigenschaft|Beschreibung|Erforderlich
|:---|:---|
|`name`|Eindeutige Kennung für einen Parameter in einer Aktion|Ja|
|`value`|Regulärer Ausdruck, der zum Validieren von Parameterwerten verwendet wird, wenn eine Anforderung initiiert wird. Falls dies nicht angegeben wird, tritt keine Validierung auf.|Nein|
|`required`|Boolescher Wert, mit dem festgelegt wird, ob der Parameter erforderlich ist. Der Wert wird standardmäßig auf 'false' gesetzt. |Nein|
|`defaultValue`|Wert, der verwendet werden soll, wenn der Parameter beim Initiieren einer Anforderung nicht angegeben wird.|Nein|

**Hinweis:** Die Werte für `bundleId`, `version`, `actionId` und `parameterId` sind auf 255 Zeichen beschränkt und müssen ausschließlich aus alphanumerischen Zeichen (a-z, A-Z, 0-9) sowie den folgenden Sonderzeichen bestehen:
 - Gedankenstrich (-)
 - Unterstreichungszeichen (_)
 - Punkt (.)

## REST-APIs
{: #rest_api}

Verwenden Sie zum Verwalten Ihrer Erweiterungspackages folgende {{site.data.keyword.iot_short_notm}}-REST-API-Befehle:

- Gehen Sie wie folgt vor, um eine Liste aller Erweiterungspackages für das Gerätemanagement abzurufen:
  `GET https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Gehen Sie wie folgt vor, um ein neues Erweiterungspackage für das Gerätemanagement zu erstellen:
  `POST https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Gehen Sie wie folgt vor, um ein bestimmtes Erweiterungspackage für das Gerätemanagement abzurufen:
  `GET https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Gehen Sie wie folgt vor, um ein Erweiterungspackage für das Gerätemanagement zu aktualisieren:
  `PUT https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Gehen Sie wie folgt vor, um ein Erweiterungspackage für das Gerätemanagement zu löschen:
  `DELETE https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

Weitere Informationen zu den REST-APIs für Erweiterungspackages für das Gerätemanagement finden Sie in der Dokumentation zur [{{site.data.keyword.iot_short_notm}}-API Version 2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


##Unterstützung für angepasste Gerätemanagementaktionen bereitstellen
{: #supporting_custom_device_management_actions}

Gerätemanagementaktionen, die in Ihren Erweiterungspackages definiert sind, können nur von Geräten initiiert werden, die diese Aktionen unterstützen. Wenn ein Gerät eine Managementanforderung an {{site.data.keyword.iot_short_notm}} publiziert, gibt das Gerät die Aktionstypen an, die von ihm unterstützt werden können.

Um angepasste Aktionen aus einem Erweiterungspackage zu erhalten, muss das Gerät die Bundle-ID für das Erweiterungspackage wie im folgenden Beispiel gezeigt im Objekt 'supports' der Anforderung angeben:

```
	Ausgehende Nachricht vom Gerät:

	Topic: iotdevice-1/mgmt/manage
	{
		"d": {
			"supports": {
				"deviceActions": false,
				"firmwareActions": false,
				"<Bundle-ID>": true
			}
		},
		"reqId": "<Anforderungs-ID>"
	}

	Eingehende Nachricht vom Server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "<Anforderungs-ID>"
	}

```

Weitere Informationen zu Managementanforderungen von Geräten finden Sie im [Gerätemanagementprotokoll](index.html){: new_window}.

## Angepasste Gerätemanagementaktionen initiieren
{: #initiating_custom_dm_actions}

Verwenden Sie zum Initiieren von angepassten Gerätemanagementaktionen den folgenden REST-API-Befehl, bei dem es sich um den Standardbefehl zum Initiieren von Gerätemanagementaktionen handelt:

`POST https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Beim Initiieren einer Anforderung müssen Sie folgende Informationen angeben:

- Die `<Bundle-ID>/<Aktions-ID>` der Aktion.
- Eine Liste der Geräte, auf denen die Aktion initiiert werden soll, maximal 5000 Geräte.
- Eine Liste der Parameter, die in der angepassten Aktionsdefinition definiert sind.

Die Nutzlast zum Initiieren einer Anforderung weist das folgende Format auf:

```
	{
		"action": "<Bundle-ID>/<Aktions-ID>",
		"devices": [
			{
				"typeId": "<Gerätetyp 0>",
				"deviceId": "<Geräte-ID 0>"
			}
		],
		"parameters": [
			{
				"name": "<Parameter0>",
				"value": "<Wert für Parameter0>"
			}
		]
	}

```


## Angepasste Gerätemanagementaktionen bearbeiten
{: #handling_custom_dm_actions}

Wenn auf einem Gerät eine angepasste Aktion initiiert wird, wird eine MQTT-Nachricht auf dem Gerät publiziert. Die MQTT-Nachricht enthält alle Parameter, die als Bestandteil der Anforderung angegeben wurden. Wenn das Gerät die MQTT-Nachricht empfängt, führt es entweder die Aktion aus oder es antwortet mit einem Fehlercode, mit dem angegeben wird, warum die Aktion zurzeit nicht ausgeführt werden kann.

Wenn eine Geräteaktion erfolgreich ausgeführt wird, publiziert das Gerät eine Antwort, in der für `rc` der Wert `200` eingestellt ist.

Der folgende Auszug zeigt ein Beispiel für den Austausch, der zwischen einem Server und einem Gerät stattfindet:

```
	Eingehende Nachricht vom Server:

	Topic: iotdm-1/mgmt/custom/<Bundle-ID>/<Aktions-ID>
	{
		"d": {
			"fields": [
				{
					"field": "<Parameter0>",
					"value": "<Wert für Parameter0>"
				}
			]
		},
		"reqId": "<Anforderungs-ID>"
	}

	... Gerät führt angeforderte Aktion aus ...

	Ausgehende Nachricht vom Gerät:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "<Anforderungs-ID>"
	}

```

## Beispiel
{: #example}

Das folgende Beispiel zeigt, wie Sie eine neue Gerätemanagementerweiterung definieren und eine Aktion ausführen können, die in dieser Erweiterung definiert ist.

Einige Unternehmen stellen `exampleDeviceType`-Geräte her. Sie können Plug-ins installieren und sie so verwalten, dass sie auf `exampleDeviceType`-Geräten ausgeführt werden können. Um die ferne Verwaltung von Plug-ins auf `exampleDeviceType`-Geräten zu ermöglichen, stellt der Hersteller in der Regel eine Gerätemanagementerweiterung bereit, die Sie in Ihre {{site.data.keyword.iot_short_notm}}-Organisation importieren können.

In diesem Beispiel wird das folgende Erweiterungs-JSON-Dokument verwendet:

```
	{
		"bundleId": "exampleDeviceType-actions-v1",
		"displayName": {
			"en_US": "exampleDeviceType Actions v1"
		},
		"description": {
			"en_US": "Device management actions for exampleDeviceType devices"
		},
		"version": "1.0",
		"provider": "some company",
		"actions": {
			"installPlugin": {
				"actionDisplayName": {
					"en_US": "Install Plug-in"
				},
				"description": {
					"en_US": "Install a new plug-in on the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					},
					{
						"name": "pluginURI",
						"value": "((http:\\/\\/|https:\\/\\/)(.*)+)",
						"required": true
					}
				]
			},
			"enablePlugin": {
				"actionDisplayName": {
					"en_US": "Enable Plug-in"
				},
				"description": {
					"en_US": "Enables a plug-in on the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					}
				]
			},
			"disablePlugin": {
				"actionDisplayName": {
					"en_US": "Disable Plug-in"
				},
				"description": {
					"en_US": "Disables a plug-in on the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					}
				]
			},
			"uninstallPlugin": {
				"actionDisplayName": {
					"en_US": "Uninstall Plug-in"
				},
				"description": {
					"en_US": "Uninstall a plug-in from the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					}
				]
			}
		}
	}

```
In diesem Erweiterungspackage für das Gerätemanagement sind folgende Aktionen definiert:

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

Verwenden Sie folgenden REST-API-Befehl, um die Erweiterung hinzuzufügen:

`POST https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

Geräte, die für die `<Organisations-ID>` der Organisation registriert wurden, können angeben, dass sie `exampleDeviceType-actions-v1`-Aktionen unterstützen, wenn sie eine Managementanforderung publizieren; dies wird im folgenden Beispiel gezeigt:

```
	Ausgehende Nachricht vom Gerät:

	Topic: iotdevice-1/mgmt/manage
	{
		"d": {
			"supports": {
				"exampleDeviceType-actions-v1": true
			}
		},
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
Das Gerät empfängt von {{site.data.keyword.iot_short_notm}} folgende Antwort:

```
	Eingehende Nachricht vom Server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
Zu diesem Zeitpunkt können Sie die in der Erweiterung `exampleIoT-exampleDeviceType-v1` definierten Geräteaktionen initiieren.

Zum Initiieren der Aktion `installPlugin` werden folgende Nutzdaten verwendet:

```
	{
		"action": "exampleDeviceType-actions-v1/installPlugin",
		"devices": [
			{
				"typeId": "exampleDeviceType",
				"deviceId": "device0"
			},
			{
				"typeId": "exampleDeviceType",
				"deviceId": "device1"
			}
		],
		"parameters": [
			{
				"name": "pluginId",
				"value": "testPluginA"
			},
			{
				"name": "pluginURI",
				"value": "http://www.example.com/testPluginA.zip"
			}
		]
	}

```
Verwenden Sie den folgenden REST-API-Befehl, um die Anforderung zu initiieren:

`POST https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Wenn der Befehl übergeben wurde, empfangen die Geräte `device0` und `device1` des Typs `exampleDeviceType` folgende MQTT-Nachricht:

```
	Eingehende Nachricht vom Server:

	Topic: iotdm-1/mgmt/custom/exampleDeviceType-actions-v1/installPlugin
	{
		"d": {
			"fields": [
				{
					"field": "pluginId",
					"value": "testPluginA"
				},
				{
					"field": "pluginURI",
					"value": "http://www.exampleiot.com/testPluginA.zip"
				}
			]
		},
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

Jedes Gerät nimmt aufgrund der Nachricht eine Aktion vor und installiert das angegebene Plug-in. Wenn die Installation abgeschlossen ist, übergeben die Geräte eine Nachricht, um anzugeben, dass die Aktion erfolgreich abgeschlossen wurde.

```
	Ausgehende Nachricht vom Gerät:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

An diesem Zeitpunkt ist die Gerätemanagementaktion `installPlugin` abgeschlossen.

## API-Beispiele
{: #api_examples}

Verwenden Sie zum Verwalten Ihrer Geräte folgende API-Anforderungen:

- Gehen Sie wie folgt vor, um eine neue Gerätemanagementerweiterung zu erstellen:

`curl -XPOST -d '<hier Nutzdaten einfügen>' -H "Content-Type: application/json" -u "<API-Schlüssel>:<API-Token>" https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Gehen Sie wie folgt vor, um Gerätemanagementerweiterungen aufzulisten:

`curl -XGET -H "Content-Type: application/json" -u "<API-Schlüssel>:<API-Token>" https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Gehen Sie wie folgt vor, um eine Gerätemanagementanforderung zu initiieren:

`curl -XPOST -d '<hier Nutzdaten einfügen>' -H "Content-Type: application/json" -u "<API-Schlüssel>:<API-Token>" https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Gehen Sie wie folgt vor, um Gerätemanagementanforderungen aufzulisten, die sich noch in der Verarbeitung befinden oder die abgeschlossen sind:

`curl -XGET -H "Content-Type: application/json" -u "<API-Schlüssel>:<API-Token>" https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Gehen Sie wie folgt vor, um den Status einer bestimmten Gerätemanagementanforderung anzuzeigen:

`curl -XGET -H "Content-Type: application/json" -u "<API-Schlüssel>:<API-Token>" https://<Organisations-ID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<Anforderungs-ID>`
