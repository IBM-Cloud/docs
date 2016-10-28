---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 延伸裝置管理
{: #custom_actions}
前次更新：2016 年 7 月 11 日
{: .last-updated}

您可以使用 REST API 或 {{site.data.keyword.Bluemix_notm}} 中提供的儀表板，透過新增裝置管理延伸規格，以在 {{site.data.keyword.iot_full}} 中延伸裝置管理功能來符合需求。

{{site.data.keyword.iot_short_notm}} 預設會提供及支援下列裝置管理動作：
- 裝置重新開機
- 重設為原廠設定
- 韌體下載
- 韌體更新

如果 {{site.data.keyword.iot_short_notm}} 所提供的預設裝置動作無法滿足您的裝置及應用程式，您可以實作裝置管理延伸規格套件來開發其他裝置管理功能。

## 裝置管理延伸規格套件
{: #device_management_ext}

裝置管理延伸規格套件是定義一組裝置管理動作的 JSON 文件。可以在支援動作的一個以上裝置上起始動作。使用 {{site.data.keyword.iot_short_notm}} 儀表板或裝置管理 REST API 指令，即可起始動作。

下列程式碼範例顯示裝置管理延伸規格套件的一般格式：

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

### 延伸規格套件內容

裝置管理延伸規格套件包含下列內容：

|內容|說明|必要
|:---|:---|:---|
|`bundleId`|裝置管理延伸規格的唯一 ID。|是|
|`version`|裝置管理延伸規格的版本字串。|否|
|`provider`|裝置管理延伸規格的提供者字串，限制為 1024 個字元。|否|
|`displayName`|{{site.data.keyword.iot_short_notm}} 儀表板中顯示的 `locale`: `String` 鍵值組對映。您必須至少指定一個項目。|是|
|`description`|用於在 {{site.data.keyword.iot_short_notm}} 儀表板中顯示的 `locale`: `String` 鍵值組對映。定義時，您必須至少指定一個項目。|否|
|`actions`| 定義裝置管理延伸規格中所含動作的 `actionId`: `<action>` 鍵值組對映。您必須至少指定一個項目。|是|

### 每一個動作的內容：

|內容|說明|必要
|:---|:---|
|`actionDisplayName`|{{site.data.keyword.iot_short_notm}} 儀表板中顯示的 `locale`: `String` 鍵值組對映。您必須至少指定一個項目。|是|
|`description`|用於在 {{site.data.keyword.iot_short_notm}} 儀表板中顯示的 `locale`: `String` 鍵值組對映。選用。您必須至少指定一個項目。|否|
|`parameters`|特定動作容許的參數陣列。定義時，您必須至少指定一個項目。|否|

### 每一個動作參數的內容：

|內容|說明|必要
|:---|:---|
|`name`|動作中參數的唯一 ID|是|
|`value`|起始要求時用來驗證參數值的正規表示式。如果未指定，就不會執行驗證。|否|
|`required`|決定是否需要參數的布林值。值預設為 false。 |否|
|`defaultValue`|起始要求時，在未提供參數時要使用的值|否|

**附註：**`bundleId`、`version`、`actionId` 及 `parameterId` 值限制為只能包含 255 個字元，而且只能包含英數字元（a-z、A-Z、0-9）以及下列特殊字元：
 - 橫線 (-)
 - 底線 (_)
 - 點 (.)

## REST API
{: #rest_api}

使用下列 {{site.data.keyword.iot_short_notm}} REST API 指令，以管理延伸規格套件：

- 若要取得所有裝置管理延伸規格套件清單，請執行下列指令：
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- 若要建立新的裝置管理延伸規格套件，請執行下列指令：
  `POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- 若要取得特定裝置管理延伸規格套件，請執行下列指令：
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- 若要更新裝置管理延伸規格套件，請執行下列指令：
  `PUT https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- 若要刪除裝置管理延伸規格套件，請執行下列指令：
  `DELETE https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

如需裝置管理延伸規格套件之 REST API 的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} API 第 2 版](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}文件。


##支援自訂裝置管理動作
{: #supporting_custom_device_management_actions}

只有支援延伸規格套件中所定義之裝置管理動作的裝置，才能起始那些動作。裝置將管理要求發佈至 {{site.data.keyword.iot_short_notm}} 時，裝置會指定可支援的動作類型。

若要接收延伸規格套件的自訂動作，裝置必須在要求的 supports 物件中指定延伸規格套件的軟體組 ID，如下列範例所示：

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

如需裝置管理要求的相關資訊，請參閱[裝置管理通訊協定](index.html){: new_window}。

## 起始自訂裝置管理動作
{: #initiating_custom_dm_actions}

若要起始自訂裝置管理動作，請使用下列 REST API 指令（即用於起始裝置管理動作的預設指令）：

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

當您起始要求時，必須提供下列資訊：

- 動作 `<bundleId>/<actionId>`
- 要在其上起始動作的裝置清單，最多 5000 個裝置
- 參數清單，定義於自訂動作定義中

用於起始要求的有效負載的格式如下：

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


## 處理自訂裝置管理動作
{: #handling_custom_dm_actions}

在裝置上起始自訂動作時，會將 MQTT 訊息發佈至裝置。MQTT 訊息包含已指定為要求一部分的任何參數。裝置接收到 MQTT 訊息時，會執行動作或回應錯誤碼，該錯誤指出目前無法完成動作的原因。

順利完成裝置動作時，裝置會發佈 `rc` 值設為 `200` 的回應。

下列摘錄提供伺服器與裝置之間的交換範例。

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

## 範例
{: #example}

下列範例示範如何定義新的裝置管理延伸規格，以及執行該延伸規格中定義的動作。

有些公司會製造 `exampleDeviceType` 裝置。您可以安裝及管理要在 `exampleDeviceType` 裝置上執行的外掛程式。為了協助遠端管理 `exampleDeviceType` 裝置上的外掛程式，製造商一般會提供可匯入至 {{site.data.keyword.iot_short_notm}} 組織的裝置管理延伸規格。

下列是此範例中所使用的延伸 JSON 文件：

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
在此裝置管理延伸規格套件中，定義下列動作：

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

若要新增延伸規格，請使用下列 REST API 指令：

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

向組織 `<orgID>` 登錄的裝置發佈管理要求時，可以指定其支援 `exampleDeviceType-actions-v1` 動作，如下列範例所示：

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
裝置接收到來自 {{site.data.keyword.iot_short_notm}} 的下列回應：

```
	Incoming message from server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
此時，您可以起始 `exampleIoT-exampleDeviceType-v1` 延伸規格中定義的裝置動作。

下列有效負載用來起始 `installPlugin` 動作：

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
使用下列 REST API 指令，以起始要求：

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

提交指令時，類型 `exampleDeviceType` 的裝置 `device0` 及 `device1` 會接收到下列 MQTT 訊息：

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

每一個裝置都會對訊息採取動作，以及安裝指定的外掛程式。安裝完成時，裝置會提交訊息，以指出動作已順利完成。

```
	Outgoing message from device:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

此時，`installPlugin` 裝置管理動作已完成。

## API 範例
{: #api_examples}

使用下列 API 要求，以管理裝置：

- 若要建立新的裝置管理延伸規格，請執行下列指令：

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- 若要列出裝置管理延伸規格，請執行下列指令：

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- 若要起始裝置管理要求，請執行下列指令：

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- 若要列出進行中或已完成的裝置管理要求，請執行下列指令：

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- 若要檢視特定裝置管理要求的狀態，請執行下列指令：

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`
