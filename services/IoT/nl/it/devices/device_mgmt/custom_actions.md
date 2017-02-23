---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Estensione della gestione del dispositivo
{: #custom_actions}

Puoi estendere le funzionalità di gestione del dispositivo in {{site.data.keyword.iot_full}} per soddisfare i tuoi requisiti aggiungendo le estensioni di gestione del dispositivo. Le estensioni di gestione del dispositivo possono essere aggiunte utilizzando l'API REST o il dashboard {{site.data.keyword.iot_short_notm}}.

Per impostazione predefinita, le seguenti azioni di gestione del dispositivo vengono supportate da {{site.data.keyword.iot_short_notm}}:
- Riavvio dispositivo
- Reimpostazione fabric
- Scaricamento firmware
- Aggiornamento firmware

## Pacchetti di estensione della gestione del dispositivo
{: #device_management_ext}

Un pacchetto di estensione di gestione del dispositivo è un documento JSON che definisce almeno una azione di gestione del dispositivo. Le azioni possono inizializzare qualsiasi dispositivo che le supporta utilizzando il dashboard {{site.data.keyword.iot_short_notm}} o l'API REST.

Il seguente esempio di codice mostra il formato tipico di un pacchetto di estensione di gestione del dispositivo:

```

	{
		"bundleId": "<unique identifier>",
		"displayName": {
			"<locale 0>": "<localized display name 0>"
		},
		"description": {
			"<locale 0>": "<localized description 0>"
		},
		"version": "<bundle version>",
		"provider": "<bundle provider>",
		"actions": {
			"<actionId 0>": {
				"actionDisplayName": {
					"<locale 0>": "<localized action display name 0>"
				},
				"description": {
					"<locale 0>": "<localized description>"
				},
				"parameters": [
					{
						"name": "<parameterId>",
						"value": "<regex pattern for value checking>",
						"required": false,
						"defaultValue": "<default>"
					}
				]
			}
		}
	}

```

### Aggiunta di un pacchetto di gestione del dispositivo personalizzato 

I pacchetti di gestione del dispositivo personalizzati possono essere aggiunti utilizzando il dashboard {{site.data.keyword.iot_short_notm}} o l'API.

Per aggiungere un pacchetto di gestione personalizzato utilizzando il dashboard {{site.data.keyword.iot_short_notm}}:

1. Dal tuo dashboard {{site.data.keyword.iot_short_notm}}, fai clic su **Impostazioni** dalla barra di navigazione.
2. Fai clic su **Pacchetti di gestione del dispositivo personalizzati**.
3. Fai clic sul pulsante **Aggiungi pacchetto**.
4. Selezione il tuo file pacchetto e fai clic su **Apri**.

Per aggiungere un pacchetto di gestione personalizzato utilizzando l'API, consulta la [Documentazione API {{site.data.keyword.iot_short_notm}}![icona link esterno](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

### Estensione delle proprietà del pacchetto

Un pacchetto di estensione di gestione del dispositivo contiene le seguenti proprietà:

|Proprietà|Descrizione|Obbligatorio
|:---|:---|:---|
|`bundleId`|Identificativo univoco per un estensione di gestione del dispositivo.|Sì|
|`version`|Stringa della versione per un estensione di gestione del dispositivo.|No|
|`provider`|Stringa del provider per un estensione di gestione del dispositivo, limitata a 1024 caratteri.|No|
|`displayName`|Associazione di coppie valore-chiave `locale`: `String` visualizzate nel dashboard {{site.data.keyword.iot_short_notm}}. Devi specificare almeno una voce.|Sì|
|`description`|Associazione di coppie valore-chiave `locale`: `String` utilizzate per la visualizzazione nel dashboard {{site.data.keyword.iot_short_notm}}. Se definito, devi specificare almeno una voce.|No|
|`actions`| Associazione di coppie valore-chiave `actionId`: `<action>` che definiscono le azioni contenute in un'estensione di gestione del dispositivo. Devi specificare almeno una voce.|Sì|

### Proprietà per ogni azione:

|Proprietà|Descrizione|Obbligatorio
|:---|:---|
|`actionDisplayName`|Associazione di coppie valore-chiave `locale`: `String` visualizzate nel dashboard {{site.data.keyword.iot_short_notm}}. Devi specificare almeno una voce.|Sì|
|`description`|Associazione di coppie valore-chiave `locale`: `String` utilizzate per la visualizzazione nel dashboard {{site.data.keyword.iot_short_notm}}. Facoltativo. Devi specificare almeno una voce.|No|
|`parameters`|Array di parametri consentiti per un'azione in particolare. Se definito, devi specificare almeno una voce.|No|

### Proprietà per ogni parametro dell'azione:

|Proprietà|Descrizione|Obbligatorio
|:---|:---|
|`name`|Identificativo univoco per un parametro in un'azione|Sì|
|`value`|Espressione regolare utilizzata per convalidare i valori del parametro quando viene avviata una richiesta. Se non specificato, la convalida non viene effettuata.|No|
|`required`|Il valore booleano che determina se il parametro è obbligatorio. Il valore è impostato per impostazione predefinita su false. |No|
|`defaultValue`|Il valore da utilizzare se il parametro non viene fornito quando una richiesta viene avviata|No|

**Nota:** i valori `bundleId`, `version`, `actionId` e `parameterId` possono contenere un massimo di 255 caratteri e possono essere formati da solo caratteri alfanumerici (a-z, A-Z, 0-9) e dai seguenti caratteri speciali:
 - trattino (-)
 - segno di sottolineatura (\_)
 - punto (.)

## API REST
{: #rest_api}

Utilizza i seguenti comandi API REST {{site.data.keyword.iot_short_notm}} per gestire i tuoi pacchetti dell'estensione:

- Per ottenere un elenco di tutti i pacchetti di estensione di gestione del dispositivo:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Per creare un nuovo pacchetto di estensione di gestione del dispositivo:
  `POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Per ottenere uno specifico pacchetto di estensione di gestione del dispositivo:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Per aggiornare un pacchetto di estensione di gestione del dispositivo:
  `PUT https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Per eliminare un pacchetto di estensione di gestione del dispositivo:
  `DELETE https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

Per ulteriori informazioni sulle API REST per i pacchetti di estensione di gestione del dispositivo, consulta la documentazione [{{site.data.keyword.iot_short_notm}} API V2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


## Supporto di azioni di gestione del dispositivo personalizzate
{: #supporting_custom_device_management_actions}

Le azioni di gestione del dispositivo definite nei tuoi pacchetti di estensione possono essere avviate solo dai dispositivi che supportano tali azioni. Quando un dispositivo pubblica una richiesta di gestione in {{site.data.keyword.iot_short_notm}}, il dispositivo specifica il tipo di azioni che può supportare.

Per specificare le azioni personalizzate dal pacchetto di estensione, il dispositivo deve specificare l'identificativo bundle per il pacchetto di estensione nell'oggetto supports della richiesta, come mostrato nel seguente esempio:

```
	Outgoing message from device:

	Topic: iotdevice-1/mgmt/manage
	{
		"d": {
			"supports": {
				"deviceActions": false,
				"firmwareActions": false,
				"<bundleId>": true
			}
		},
		"reqId": "<request id>"
	}

	Incoming response from server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

Per ulteriori informazioni sulle richieste di gestione del dispositivo, consulta [Protocollo di gestione del dispositivo](index.html){: new_window}.

## Inizializzazione delle azioni di gestione del dispositivo personalizzate
{: #initiating_custom_dm_actions}

Per avviare le azioni di gestione del dispositivo personalizzate, utilizza il seguente comando API REST, che è il comando predefinito per avviare le azioni di gestione del dispositivo:

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Devi fornire le seguenti informazioni quando avvii una richiesta:

- L'azione `<bundleId>/<actionId>`
- Un elenco di dispositivi su cui avviare l'azione, al massimo 5000 dispositivi
- Un elenco di parametri, definito nella definizione dell'azione personalizzata

Il payload per avviare una richiesta è nel seguente formato:

```
	{
		"action": "<bundleId>/<actionId>",
		"devices": [
			{
				"typeId": "<deviceType 0>",
				"deviceId": "<deviceId 0>"
			}
		],
		"parameters": [
			{
				"name": "<parameter0>",
				"value": "<parameter0 value>"
			}
		]
	}

```


## Gestione delle azioni di gestione del dispositivo personalizzate
{: #handling_custom_dm_actions}

Quando viene avviata un'azione personalizzata su un dispositivo, viene pubblicato un messaggio MQTT nel dispositivo. Il messaggio MQTT contiene tutti i parametri specificati come parte della richiesta. Quando il dispositivo riceve il messaggio MQTT, esegue l'azione o risponde con un codice di errore che indica il motivo per cui non può al momento completare l'azione.

Quando un'azione del dispositivo viene completata correttamente, il dispositivo pubblica una risposta nella quale il valore `rc` viene impostato su `200`.

Il seguente estratto fornisce un esempio dello scambio che si verifica tra un server e un dispositivo.

```
	Incoming message from the server:

	Topic: iotdm-1/mgmt/custom/<bundleId>/<actionId>
	{
		"d": {
			"fields": [
				{
					"field": "<parameter0>",
					"value": "<parameter0 value>"
				}
			]
		},
		"reqId": "<request id>"
	}

	... device carries out the requested action ...

	Outgoing message from the device:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

## Esempio
{: #example}

Il seguente esempio dimostra come puoi definire una nuova estensione di gestione del dispositivo ed eseguire un'azione definita in tale estensione.

Alcuni dispositivi `exampleDeviceType` di produzione aziendale. Puoi installare e gestire i plug-in per essere eseguiti sui dispositivi `exampleDeviceType`. Per facilitare la gestione remota dei plug-in nei dispositivi `exampleDeviceType`, i produttori normalmente forniscono un'estensione di gestione del dispositivo che puoi importare nella tua organizzazione {{site.data.keyword.iot_short_notm}}.

Il seguente documento di estensione JSON viene utilizzato nell'esempio:

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
In questo pacchetto di estensione di gestione del dispositivo, sono definite le seguenti azioni:

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

Per aggiungere l'estensione, utilizza il seguente comando API REST:

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

I dispositivi registrati nell'organizzazione `<orgID>` possono specificare di supportare le azioni `exampleDeviceType-actions-v1` quando pubblicano una richiesta di gestione, come mostrato nel seguente esempio:

```
	Outgoing message from device:

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
Il dispositivo riceve la seguente risposta da {{site.data.keyword.iot_short_notm}}:

```
	Incoming message from server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
A questo punto, puoi avviare le azioni del dispositivo definite nell'estensione `exampleIoT-exampleDeviceType-v1`.

Il seguente payload viene utilizzato per avviare un'azione `installPlugin`:

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
Avvia la richiesta utilizzando il seguente comando API REST:

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Quando viene immesso il comando, i dispositivi `device0` e `device1` del tipo `exampleDeviceType` ricevono il seguente messaggio MQTT:

```
	Incoming message from server:

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

Ogni dispositivo esegue un'azione nel messaggio e installa il plug-in specificato. Quando l'installazione viene terminata, il dispositivo invia un messaggio che indica che l'azione è stata completata correttamente.

```
	Outgoing message from device:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

A questo punto, l'azione di gestione del dispositivo `installPlugin` viene completata.

## Esempi API
{: #api_examples}

Utilizza le seguenti richieste API per gestire i tuoi dispositivi:

- Per creare una nuova estensione di gestione del dispositivo:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Per elencare le estensioni di gestione del dispositivo:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Per avviare una richiesta di gestione del dispositivo:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Per elencare le richieste di gestione del dispositivo in corso o completate:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Per visualizzare lo stato di una richiesta di gestione del dispositivo in particolare:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`

## Ricette sulle estensioni di gestione dispositivo

Le seguenti ricette mostrano il flusso necessario per gestire le estensioni di gestione dispositivo:

- [La ricetta Device Management Extension Packages in WIoT Platform ![icona link esterno](../../../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/device-management-extension-packages-in-wiot-platform/){: new_window} fornisce le istruzioni per registrare un dispositivo gestito con {{site.data.keyword.iot_short}} in modo che possa ricevere e gestire le azioni delle estensioni di gestione del dispositivo. Gli esempi di codice nella ricetta sono scritti utilizzando la libreria client Python.
