---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 扩展设备管理
{: #custom_actions}
上次更新时间：2016 年 7 月 11 日
{: .last-updated}

您可以通过使用 REST API 或 {{site.data.keyword.Bluemix_notm}} 中提供的仪表板，添加设备管理扩展来扩展 {{site.data.keyword.iot_full}} 中的设备管理功能，以满足您的需求。

缺省情况下，{{site.data.keyword.iot_short_notm}} 提供并支持以下设备管理操作：
- 设备重新引导
- 恢复工厂设置
- 固件下载
- 固件更新

如果 {{site.data.keyword.iot_short_notm}} 提供的缺省设备操作不足以满足您对设备和应用程序的操作需求，那么可以通过实现设备管理扩展包来开发更多设备管理功能。

## 设备管理扩展程序包
{: #device_management_ext}

设备管理扩展包是一种 JSON 文档，用于定义一组设备管理操作。这些操作可以在支持这些操作的一个或多个设备上启动。操作可使用 {{site.data.keyword.iot_short_notm}} 仪表板或设备管理 REST API 命令启动。

以下代码样本显示设备管理扩展包的典型格式：

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

### 扩展包属性

设备管理扩展包中包含以下属性：

|属性|描述|必需
|:---|:---|:---|
|`bundleId`|设备管理扩展的唯一标识。|是|
|`version`|设备管理扩展的版本字符串。|否|
|`provider`|设备管理扩展的提供者字符串，限制为 1024 个字符。|否|
|`displayName`|`locale` 的映射：在 {{site.data.keyword.iot_short_notm}} 仪表板中显示的 `String` 键/值对。必须至少指定一个条目。|是|
|`描述`|`locale` 的映射：用于在 {{site.data.keyword.iot_short_notm}} 仪表板中显示的 `String` 键/值对。如果定义，必须至少指定一个条目。|否|
|`actions`| `actionId` 的映射：`<action>` 键/值对，用于定义设备管理扩展中包含的操作。必须至少指定一个条目。|是|

### 每个操作的属性：

|属性|描述|必需
|:---|:---|
|`actionDisplayName`|`locale` 的映射：在 {{site.data.keyword.iot_short_notm}} 仪表板中显示的 `String` 键/值对。必须至少指定一个条目。|是|
|`描述`|`locale` 的映射：用于在 {{site.data.keyword.iot_short_notm}} 仪表板中显示的 `String` 键/值对。可选。必须至少指定一个条目。|否|
|`parameters`|允许用于特定操作的参数的数组。如果定义，必须至少指定一个条目。|否|

### 每个操作参数的属性：

|属性|描述|必需
|:---|:---|
|`name`|操作中参数的唯一标识|是|
|`value`|正则表达式，用于在启动请求时验证参数值。如果未指定，那么不会执行验证。|否|
|`required`|布尔值，用于确定是否参数是必需的。缺省情况下，此值设置为 false。 |否|
|`defaultValue`|如果未提供参数，当启动请求时要使用的值|否|

**注：**`bundleId`、`version`、`actionId` 和 `parameterId` 值可以包含的字符数限制为 255 个，并且只能由字母数字字符（a-z、A-Z 和 0-9）和以下特殊字符组成：
 - 短划线 (-)
 - 下划线 (_)
 - 点 (.)

## REST API
{: #rest_api}

使用以下 {{site.data.keyword.iot_short_notm}} REST API 命令来管理扩展包：

- 获取所有设备管理扩展包的列表：
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- 创建新的设备管理扩展包：
  `POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- 获取特定设备管理扩展包：
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- 更新设备管理扩展包：
  `PUT https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- 删除设备管理扩展包：
  `DELETE https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

有关设备管理扩展包的 REST API 的更多信息，请参阅 [{{site.data.keyword.iot_short_notm}} API V2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} 文档。


##支持定制设备管理操作
{: #supporting_custom_device_management_actions}

扩展包中定义的设备管理操作只能由支持这些操作的设备启动。设备将管理请求发布到 {{site.data.keyword.iot_short_notm}} 时，设备会指定其可以支持的操作的类型。

要接收来自扩展包的定制操作，设备必须在请求的 supports 对象中指定扩展包的捆绑标识，如以下示例中所示：

```
	来自设备的出局消息：

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

	来自服务器的入局响应：

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

有关设备管理请求的更多信息，请参阅[设备管理协议](index.html){: new_window}。

## 启动定制设备管理操作
{: #initiating_custom_dm_actions}

要启动定制设备管理操作，请使用以下 REST API 命令，这是用于启动设备管理操作的缺省命令：

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

启动请求时，必须提供以下信息：

- 操作 `<bundleId>/<actionId>`
- 要在其上启动操作的设备列表，最多包含 5000 台设备
- 在定制操作定义中定义的参数列表

用于启动请求的有效内容的格式如下：

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


## 处理定制设备管理操作
{: #handling_custom_dm_actions}

在设备上启动定制操作时，将向该设备发布一条 MQTT 消息。该 MQTT 消息包含指定作为请求一部分的任何参数。设备收到该 MQTT 消息时，或者运行操作，或者使用错误代码进行响应，以指示为什么当前无法完成该操作。

设备操作成功完成时，设备会发布响应，其中 `rc` 值会设置为 `200`。

以下摘录是服务器与设备之间发生的交换的示例。

```
	来自服务器的入局消息：

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

	来自设备的外发消息：

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

## 示例
{: #example}

以下示例演示了可以如何定义新的设备管理扩展，并执行该扩展中定义的操作。

某些公司会制造 `exampleDeviceType` 设备。您可以安装并管理要在 `exampleDeviceType` 设备上运行的插件。为了方便远程管理 `exampleDeviceType` 设备上的插件，制造商通常会提供设备管理扩展，您可以将其导入到您的 {{site.data.keyword.iot_short_notm}} 组织。

此示例中使用了以下扩展 JSON 文档：

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
在此设备管理扩展包中，定义了以下操作：

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

要添加扩展，请使用以下 REST API 命令：

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

注册到组织 `<orgID>` 的设备可以在发布管理请求时，指定其支持 `exampleDeviceType-actions-v1` 操作，如以下示例中所示：

```
	来自设备的出局消息：

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
设备收到来自 {{site.data.keyword.iot_short_notm}} 的以下响应：

```
	来自服务器的入局消息：

 Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
此时，可以启动在 `exampleIoT-exampleDeviceType-v1` 扩展中定义的设备操作。

以下有效内容用于启动 `installPlugin` 操作：

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
使用以下 REST API 命令启动请求：

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

提交此命令时，类型为 `exampleDeviceType` 的设备 `device0` 和 `device1` 会收到以下 MQTT 消息：

```
	来自服务器的入局消息：

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

每个设备都会执行消息上的操作，并安装指定的插件。安装完成后，设备会提交一条消息，以指示操作成功完成。

```
	来自设备的出局消息：

 Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

此时，`installPlugin` 设备管理操作完成。

## API 示例
{: #api_examples}

使用以下 API 请求来管理设备：

- 创建新的设备管理扩展：

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- 列出设备管理扩展：

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- 启动设备管理请求：

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- 列出进行中或已完成的设备管理请求：

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- 查看特定设备管理请求的状态：

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`
