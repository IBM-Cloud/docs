---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Extending device management
{: #custom_actions}

**Important:** This feature is currently available as part of a limited beta program only. Future updates might include changes that are  incompatible with the current version of this feature. Try it out and [let us know what you think](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).


The {{site.data.keyword.iot_full}} provides the ability to extend the device management capabilities. This is done by adding device management extensions by using either the REST APIs or the {{site.data.keyword.iot_short_notm}} dashboard.

Devices that connect to the {{site.data.keyword.iot_short_notm}} can have a wide range of capabilities. The device management actions that are supported by default in the {{site.data.keyword.iot_short_notm}} (*device reboot*, *factory reset*, *firmware download* and *firmware update*) might not be sufficient to manage everything that a device can do.


## Device management extension packages
{: #device_management_ext}

An extension package is a JSON document that defines a set of device management actions. The actions can be initiated against one or more devices which support those actions. The actions are initiated in the same way as the default device management actions by using either the {{site.data.keyword.iot_short_notm}} dashboard or the device management REST APIs.

Device management extension packages have the following format:

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

### Extension package properties:

- ``bundleId``: Unique identifier for a device management extension. Required.
- ``version``: Version string for a device management extension. Optional.
- ``provider``: Provider string for a device management extension. Maximum length of 1024 characters. Optional.
- ``displayName``: Map of ``locale``: ``String`` key-value pairs used for display in the{{site.data.keyword.iot_short_notm}} dashboard. Required. Must contain at least one entry.
- ``description``: Map of ``locale``: ``String`` key-value pairs used for display in the {{site.data.keyword.iot_short_notm}} dashboard. Optional. If specified, must contain at least one entry.
- ``actions``: Map of ``actionId``: ``<action>`` key-value pairs which defines the actions contained within a device management extension. Required. Must contain at least one entry.

### Properties per action:

- ``actionDisplayName``: Map of ``locale``: ``String`` key-value pairs used for display in the {{site.data.keyword.iot_short_notm}} dashboard. Required. Must contain at least one entry.
- ``description``:  Map of ``locale``: ``String`` key-value pairs used for display in the {{site.data.keyword.iot_short_notm}} dashboard. Optional. If specified, must contain at least one entry.
- ``parameters``: Array of parameters allowed for a particular action. Optional. If specified, must contain at least one entry.

### Properties per action parameter:

- ``name``: Unique identifier for a parameter within an action. Required.
- ``value``: Regular expression used for validating parameter values when a request is initiated. Optional. If not specified, value will not be validated.
- ``required``: Boolean value specifying whether the parameter is required. Optional. Default: False
- ``defaultValue``: Value to be used if the parameter is not provided when a request is initiated. Optional.

**Note:** The following restrictions apply to the  ``bundleId``, ``version``, ``actionId`` and ``parameterId`` values:  
- Maximum length of 255 characters
- Must comprise only alpha-numeric characters (a-z, A-Z, 0-9) and the following special characters:
 - dash -
 - underscore _
 - dot .

## REST APIs
{: #rest_api}

Extension packages are managed in the {{site.data.keyword.iot_short_notm}} by using the following REST APIs.

List all device management extension packages:

`GET https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

Create a new device management extension package:

`POST https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

Get a specific device management extension package:

`GET https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

Update a device management extension package:

`PUT https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

Delete a device management extension package:

`DELETE https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

For more information on the REST APIs for device management extension packages, see the [{{site.data.keyword.iot_short_notm}} API V2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) documentation.


## Supporting custom device management actions
{: #supporting_custom_device_management_actions}

Device management actions defined in an extension package may only be initiated against devices which support those actions. A device specifies what types of actions it supports when it publishes a manage request to the {{site.data.keyword.iot_short_notm}}.
In order to allow a device to receive custom actions defined in a particular extension package, the device must specify that extension's bundle identifier in the supports object when publishing a manage request.

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

For additional information about device manage requests, see [Device Management Protocol](index.html).


## Initiating custom device management actions
{: #initiating_custom_dm_actions}

Custom device management actions are initiated by using the same REST API as the default device management actions:

`POST https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

The following information must be provided when you initiate a request:

- The action ``<bundleId>/<actionId>``
- A list of devices to initiate the action against, with a maximum of 5000 devices
- A list of parameters as defined in the custom action definition

The payload for initiating a request is in the following format:

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


## Handling custom device management actions
{: #handling_custom_dm_actions}

When a custom action is initiated against a device, an MQTT message is published to the device. The message contains any parameters that were specified as part of the request. When the device
receives this message, it is expected to either execute the action or respond with an error code indicating that it cannot complete the action at this time.

To indicate that the action was completed successfully, a device should publish a response with ``rc`` set to ``200``.

Below is an example exchange between the server and a device.

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

## Example
{: #example}


The following example demonstrates how you can define a new device management extension and execute an action defined within that extension.

Some companies manufacture ``exampleDeviceType`` devices. Users of these devices have the ability to manage plug-ins, which run on the devices. To facilitate remote management of plug-ins on ``exampleDeviceType`` devices, the manufacturer provides a device management extension which users can import into their {{site.data.keyword.iot_short_notm}} organization.

The following extension JSON document is used in this example:

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
In this device management extension package, the following actions are defined:

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

The extension is added using the following REST API command:

`POST https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

Devices registered in organization ``<orgId>`` can specify that they support ``exampleDeviceType-actions-v1`` actions when publishing a manage request.

In this example, the manage request sent by a device would look like the following:

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
The device should then receive the following response from the {{site.data.keyword.iot_short_notm}}:

```
	Incoming message from server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
At this point, an action defined in the ``exampleIoT-exampleDeviceType-v1`` extension can be initiated against some devices.

The payload for initiating an ``installPlugin`` action will look like the following:

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
The request is initiated using the REST API:

`POST https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Devices ``device0`` and ``device1`` of type ``exampleDeviceType`` will then receive the following MQTT message:

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

Each device takes an action on the message, installing the new plug-in. Once installation is complete, the devices respond with the following message to indicate that the action completed successfully:

```
	Outgoing message from device:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```
At this point, the ``installPlugin`` action is now complete.


## API examples
{: #api_examples}

Use the following API requests to manage your devices:

Create a new device management extension:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

List device management extensions:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

Initiate a device management request:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

List device management requests that are in progress or completed:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

View status of a particular device management request:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgId>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`
