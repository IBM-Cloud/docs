---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Extension de la gestion des terminaux
{: #custom_actions}

Vous pouvez étendre les fonctions de gestion des terminaux dans {{site.data.keyword.iot_full}} en fonction de vos besoins en ajoutant des extensions de gestion des terminaux. Les extensions de gestion des terminaux peuvent être ajoutées à l'aide de l'API REST ou du tableau de bord {{site.data.keyword.iot_short_notm}}.

Par défaut, les actions de gestion des terminaux suivantes sont prises en charge par {{site.data.keyword.iot_short_notm}} :
- Réamorçage de terminal
- Réinitialisation avec les paramètres d'usine
- Téléchargement de microprogramme
- Mise à jour de microprogramme

## Packages d'extension de gestion des terminaux
{: #device_management_ext}

Un package d'extension de gestion des terminaux est un document JSON qui définit au moins une action de gestion des terminaux. Les actions peuvent être lancées sur tous les terminaux prenant en charge les actions en utilisant le tableau de bord {{site.data.keyword.iot_short_notm}} ou l'API REST.

L'exemple de code suivant présente le format standard d'un package d'extension de gestion des terminaux :

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

### Ajout d'un package de gestion des terminaux personnalisé

Vous pouvez ajouter un package de gestion des terminaux personnalisé à l'aide du tableau de nord {{site.data.keyword.iot_short_notm}} ou de l'API.

Pour ajouter un package de gestion des terminaux personnalisé à l'aide du tableau de bord {{site.data.keyword.iot_short_notm}} :

1. Depuis votre tableau de bord {{site.data.keyword.iot_short_notm}}, cliquez sur **Paramètres** dans la barre de navigation.
2. Cliquez sur **Packages de gestion des terminaux personnalisés**.
3. Cliquez sur le bouton **Ajouter un package**.
4. Sélectionnez votre fichier de package et cliquez sur **Ouvrir**.

Pour ajouter un package de gestion des terminaux personnalisé à l'aide de l'API, voir la [documentation de l'API {{site.data.keyword.iot_short_notm}} ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

### Propriétés de package d'extension

Un package d'extension de gestion des terminaux contient les propriétés suivantes :

|Propriété|Description|Obligatoire
|:---|:---|:---|
|`bundleId`|Identificateur unique d'une extension de gestion des terminaux.|Oui|
|`version`|Chaîne de version d'une extension de gestion des terminaux.|Non|
|`provider`|Chaîne de fournisseur d'une extension de gestion des terminaux, limitée à 1024 caractères.|Non|
|`displayName`|Mappe de paires valeur-clé `locale`:`String` affichées dans le tableau de bord {{site.data.keyword.iot_short_notm}}. Vous devez spécifier au moins une entrée.|Oui|
|`description`|Mappe de paires clé-valeur `locale`:`String` utilisées à des fins d'affichage dans le tableau de bord {{site.data.keyword.iot_short_notm}}. Si cette propriété est définie, vous devez spécifier au moins une entrée.|Non|
|`actions`| Mappe de paires clé-valeur `actionId`:`<action>` qui définissent les actions contenues dans une extension de gestion des terminaux. Vous devez spécifier au moins une entrée.|Oui|

### Propriétés de chaque action :

|Propriété|Description|Obligatoire
|:---|:---|
|`actionDisplayName`|Mappe de paires valeur-clé `locale`:`String` affichées dans le tableau de bord {{site.data.keyword.iot_short_notm}}. Vous devez spécifier au moins une entrée.|Oui|
|`description`|Mappe de paires clé-valeur `locale`:`String` utilisées à des fins d'affichage dans le tableau de bord {{site.data.keyword.iot_short_notm}}. Facultatif. Vous devez spécifier au moins une entrée.|Non|
|`parameters`|Tableau de paramètres autorisés pour une action donnée. Si cette propriété est définie, vous devez spécifier au moins une entrée.|Non|

### Propriétés de chaque paramètre d'action :

|Propriété|Description|Obligatoire
|:---|:---|
|`name`|Identificateur unique d'un paramètre dans une action|Oui|
|`value`|Expression régulière utilisée pour valider des valeurs de paramètre lorsqu'une demande est lancée. Si la propriété n'est pas spécifiée, la validation n'a pas lieu.|Non|
|`required`|Valeur booléenne qui détermine si le paramètre est obligatoire. La valeur par défaut est false. |Non|
|`defaultValue`|Valeur à utiliser si le paramètre n'est pas fourni lorsqu'une demande est lancée.|Non|

**Remarque :** Les valeurs `bundleId`, `version`, `actionId` et `parameterId` sont limitées à 255 caractères et ne peuvent comporter que des caractères alphanumériques (a-z, A-Z, 0-9), ainsi que les caractères spéciaux suivants :
 - Le trait d'union (-)
 - Le trait de soulignement (_)
 - Le point (.)

## API REST
{: #rest_api}

Utilisez les commandes d'API REST {{site.data.keyword.iot_short_notm}} suivantes pour gérer vos packages d'extension :

- Pour obtenir la liste de tous les packages d'extension de gestion des terminaux :
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Pour créer un nouveau package d'extension de gestion des terminaux :
  `POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Pour obtenir un package d'extension de gestion des terminaux spécifique :
`GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Pour mettre à jour un package d'extension de gestion des terminaux :
  `PUT https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Pour supprimer un package d'extension de gestion des terminaux :
  `DELETE https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

Pour plus d'informations sur les API REST pour les packages d'extension de gestion des terminaux, voir la documentation de l'[API V2 {{site.data.keyword.iot_short_notm}} ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}. 


## Prise en charge des actions de gestion des terminaux personnalisées
{: #supporting_custom_device_management_actions}

Les actions de gestion des terminaux qui sont définies dans vos packages d'extension ne peuvent être lancées que par des terminaux qui prennent en charge ces actions. Lorsqu'un terminal publie une demande de gestion sur {{site.data.keyword.iot_short_notm}}, le terminal spécifie les types d'action qu'il peut prendre en charge.

Pour indiquer des actions personnalisées d'un package d'extension, le terminal doit spécifier l'identificateur de bundle du package d'extension dans l'objet supports de la demande, comme illustré dans l'exemple suivant :

```
	Message sortant depuis le terminal :

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

	Réponse entrante depuis le serveur :

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

Pour plus d'informations sur les demandes de gestion des terminaux, voir [Protocole de gestion des terminaux](index.html).

## Lancement des actions de gestion des terminaux personnalisées
{: #initiating_custom_dm_actions}

Pour lancer des actions de gestion des terminaux personnalisées, utilisez la commande d'API REST suivante (commande par défaut pour le lancement des actions de gestion des commandes) :

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Vous devez indiquer les informations suivantes lorsque vous lancez une demande :

- L'action `<bundleId>/<actionId>`
- Une liste de terminaux sur lesquels lancer l'action (5 000 terminaux au maximum)
- Une liste de paramètres, qui sont définis dans la définition de l'action personnalisée

Le contenu pour le lancement d'une demande est au format suivant :

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


## Traitement des actions de gestion des terminaux personnalisées
{: #handling_custom_dm_actions}

Lorsqu'une action personnalisée est lancée sur un terminal, un message MQTT est publié sur le terminal. Le message MQTT contient des paramètres qui ont été spécifiés dans le cadre de la demande. Lorsque le terminal reçoit le message MQTT, il exécute l'action ou il répond avec un code d'erreur indiquant la raison pour laquelle l'action ne peut pas être exécutée pour le moment.

Lorsqu'une action de terminal aboutit, le terminal publie une réponse dans laquelle la valeur `rc` prend la valeur `200`.

L'extrait suivant fournit un exemple de l'échange qui a lieu entre un serveur et un terminal.

```
	Message entrant depuis le serveur :

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

## Exemple
{: #example}

L'exemple suivant vous montre comment définir une nouvelle extension de gestion des terminaux et comment exécuter une action qui est définie dans cette extension.

Certaines sociétés fabriquent des terminaux `exampleDeviceType`. Vous pouvez installer et gérer des plug-ins pour qu'ils s'exécutent sur des terminaux `exampleDeviceType`. Pour faciliter la gestion à distance de plug-ins sur les terminaux `exampleDeviceType`, le fabricant fournit généralement une extension de gestion des terminaux que vous pouvez importer dans votre organisation {{site.data.keyword.iot_short_notm}}.

Le document JSON d'extension suivant est utilisé dans cet exemple :

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
Dans ce package d'extension de gestion des terminaux, les actions suivantes sont définies :

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

Pour ajouter l'extension, utilisez la commande d'API REST suivante :

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

Les terminaux qui sont enregistrés sur l'organisation `<orgID>` peuvent spécifier qu'ils prennent en charge des actions `exampleDeviceType-actions-v1` lorsqu'ils publient une demande de gestion, illustrée dans l'exemple suivant :

```
	Message sortant depuis le terminal :

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
Le terminal reçoit la réponse suivante depuis {{site.data.keyword.iot_short_notm}} :

```
	Message entrant depuis le serveur :

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
A ce stade, vous pouvez lancer les actions sur les terminaux que vous avez définies dans l'extension `exampleIoT-exampleDeviceType-v1`.

Le contenu suivant est utilisé pour lancer une action `installPlugin` :

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
Lancez la demande à l'aide de la commande d'API REST suivante :

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Lorsque la commande est soumise, les terminaux `device0` et `device1` de type `exampleDeviceType` reçoivent le message MQTT suivant :

```
	Message entrant depuis le serveur :

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

Chaque terminal exécute une action sur le message et installe le plug-in spécifié. Lorsque l'installation est terminée, les terminaux soumettent un message pour indiquer que l'action a abouti.

```
	Message sortant depuis le terminal :

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

A ce stade, l'action de gestion des terminaux `installPlugin` est terminée.

## Exemples d'API
{: #api_examples}

Utilisez les demandes d'API suivantes pour gérer vos terminaux :

- Pour créer une nouvelle extension de gestion des terminaux :

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Pour répertorier les extensions de gestion des terminaux :

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Pour lancer une demande de gestion des terminaux :

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Pour répertorier les demandes de gestion des terminaux en cours ou terminées :

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Pour afficher le statut d'une demande de gestion des terminaux spécifique :

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`

## Recettes relatives aux extensions de gestion des terminaux

Les recettes suivantes décrivent le flux requis pour gérer les extensions de gestion des terminaux :

- La recette [Device Management Extension Packages in WIoT Platform ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-extension-packages-in-wiot-platform/){: new_window} explique comment enregistrer un terminal géré auprès de {{site.data.keyword.iot_short}} afin qu'il puisse recevoir et traiter des actions d'extension de gestion des terminaux. Les exemples de code décrits dans la recette sont écrits à l'aide de la bibliothèque client Python.
