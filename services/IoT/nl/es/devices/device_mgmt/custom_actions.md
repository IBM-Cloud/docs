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

# Ampliación de la gestión de dispositivos
{: #custom_actions}

Puede ampliar las funciones de gestión de dispositivos en {{site.data.keyword.iot_full}} para que cumplan sus requisitos añadiendo extensiones de gestión de dispositivos. Las extensiones de gestión de dispositivos se pueden añadir mediante la API REST o el panel de control de {{site.data.keyword.iot_short_notm}}.

De forma predeterminada, las siguientes acciones de gestión de dispositivos reciben soporte de {{site.data.keyword.iot_short_notm}}:
- Rearranque de dispositivo
- Restablecimiento de fábrica
- Descarga de firmware
- Actualización de firmware

## Paquetes de ampliación de gestión de dispositivos
{: #device_management_ext}

Un paquete de ampliación de gestión de dispositivos es un documento JSON que define al menos una acción de gestión de dispositivos. Puede iniciar las acciones cualquier dispositivo que dé soporte a las acciones mediante el panel de control de {{site.data.keyword.iot_short_notm}} o la API REST.

El ejemplo de código siguiente muestra el formato típico de un paquete de ampliación de gestión de dispositivos:

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

### Adición de un paquete de gestión de dispositivos personalizados

Los paquetes de gestión de dispositivos personalizados se pueden añadir mediante el panel de control de {{site.data.keyword.iot_short_notm}} o mediante la API.

Para añadir un paquete de gestión de dispositivos personalizados mediante el panel de control de {{site.data.keyword.iot_short_notm}}:

1. En el panel de control de {{site.data.keyword.iot_short_notm}}, pulse **Valores** en la barra de navegación.
2. Pulse **Paquetes de gestión de dispositivos personalizados**.
3. Pulse el botón **Añadir paquete**.
4. Seleccione el archivo de paquete y pulse **Abrir**.

Para añadir un paquete de gestión de dispositivos personalizados mediante la API, consulte la documentación de la API de [{{site.data.keyword.iot_short_notm}} ![icono de enlace externo](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

### Propiedades del paquete de ampliación

Un paquete de ampliación de gestión de dispositivos contiene las siguientes propiedades:

|Propiedad|Descripción|Obligatorio
|:---|:---|:---|
|`bundleId`|Identificador exclusivo para una ampliación de gestión de dispositivos.|Yes|
|`version`|Cadena de la versión para una ampliación de gestión de dispositivos.|No|
|`provider`|Cadena del proveedor para una extensión de gestión de dispositivos, limitada a 1024 caracteres.|No|
|`displayName`|Correlación de `locale`: Pares key-value de `Serie` que se muestran en el panel de instrumentos de {{site.data.keyword.iot_short_notm}}. Debe especificar al menos una entrada.|Yes|
|`description`|Correlación de `locale`: Pares key-value de `Serie` que se utilizan para visualizarse en el panel de instrumentos de {{site.data.keyword.iot_short_notm}}. Si se define, debe especificar al menos una entrada.|No|
|`actions`| Correlación de `actionId`: Los pares key-value de `<action>` que definen las acciones contenidas en una ampliación de gestión de dispositivos. Debe especificar al menos una entrada.|Yes|

### Propiedades para cada acción:

|Propiedad|Descripción|Obligatorio
|:---|:---|
|`actionDisplayName`|Correlación de `locale`: Pares key-value de `Serie` que se muestran en el panel de instrumentos de {{site.data.keyword.iot_short_notm}}. Debe especificar al menos una entrada.|Yes|
|`description`|Correlación de `locale`: Pares key-value de `Serie` que se utilizan para visualizarse en el panel de instrumentos de {{site.data.keyword.iot_short_notm}}. Opcional. Debe especificar al menos una entrada.|No|
|`parameters`|Matriz de parámetros que se permiten para una acción determinada. Si se define, debe especificar al menos una entrada.|No|

### Propiedades para cada parámetro de acción:

|Propiedad|Descripción|Obligatorio
|:---|:---|
|`name`|Identificador exclusivo para un parámetro en una acción|Yes|
|`value`|Expresión regular que se utiliza para validar valores de parámetro cuando se inicia una solicitud. Si no se especifica, no se produce la validación.|No|
|`required`|Valor booleano que determina si el parámetro es necesario. El valor se establece de forma predeterminada en false. |No|
|`defaultValue`|Valor que se utilizará si no se proporciona el parámetro al iniciar una solicitud|No|

**Nota:** Los valores `bundleId`, `version`, `actionId` y `parameterId` están limitados a 255 caracteres y pueden constar de sólo caracteres alfanuméricos (a-z, A-Z, 0-9) y de los siguientes caracteres especiales:
 - guión (-)
 - signo de subrayado (_)
 - punto (.)

## API REST
{: #rest_api}

Utilice los siguientes mandatos de la API REST de {{site.data.keyword.iot_short_notm}} para gestionar los paquetes de ampliación:

- Para obtener una lista de todos los paquetes de ampliación de gestión de dispositivos:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Para crear un nuevo paquete de ampliación de gestión de dispositivos:
  `POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Para obtener un paquete de ampliación de gestión de dispositivos específico:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Para actualizar un paquete de ampliación de gestión de dispositivos:
  `PUT https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Para suprimir un paquete de ampliación de gestión de dispositivos:
  `DELETE https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

Para obtener más información sobre las API REST para los paquetes de ampliación de gestión de dispositivos, consulte la documentación de [{{site.data.keyword.iot_short_notm}} API V2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


## Soporte de acciones de gestión de dispositivos personalizada
{: #supporting_custom_device_management_actions}

Las acciones de gestión de dispositivos definidas en los paquetes de ampliación las pueden iniciar únicamente los dispositivos que dan soporte a dichas acciones. Cuando un dispositivo publica una solicitud de gestión en el {{site.data.keyword.iot_short_notm}}, el dispositivo especifica los tipos de acciones a las que puede dar soporte.

Para especificar acciones personalizadas desde un paquete de ampliación, el dispositivo debe especificar el identificador de paquetes para el paquete de ampliación en el objeto supports de la solicitud, tal como se muestra en el ejemplo siguiente:

```
	Mensaje saliente del dispositivo:

	Tema: iotdevice-1/mgmt/manage
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

	Respuesta entrante del servidor:

	Tema: iotdm-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

Para obtener más información sobre las solicitudes de gestión de dispositivos, consulte [Protocolo de gestión de dispositivos](index.html){: new_window}.

## Inicio de acciones de gestión de dispositivos personalizada
{: #initiating_custom_dm_actions}

Para iniciar acciones de gestión de dispositivos personalizadas, utilice el siguiente mandato de API REST, que es el mandato predeterminado para iniciar acciones de gestión de dispositivos:

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Debe proporcionar la información siguiente al iniciar una solicitud:

- La acción `<bundleId>/<actionId>`
- Una lista de dispositivos en la que iniciar la acción, hasta un máximo de 5000 dispositivos
- Una lista de parámetros, definidos en la definición de acciones personalizada

La carga útil para iniciar una solicitud se encuentra en el siguiente formato:

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


## Manejo de acciones de gestión de dispositivos personalizada
{: #handling_custom_dm_actions}

Cuando se inicia una acción personalizada en un dispositivo, se publicará un mensaje MQTT en el dispositivo. El mensaje MQTT contiene los parámetros especificados como parte de la solicitud. Cuando el dispositivo recibe el mensaje MQTT, éste ejecuta la acción o responde con un código de error que indica el motivo por el que no puede completar la acción en este momento.

Cuando se completa correctamente una acción de dispositivo, el dispositivo publica una respuesta en la que el valor `rc` se establece en `200`.

El siguiente extracto proporciona un ejemplo del intercambio que se produce entre un servidor y un dispositivo.

```
	Mensaje entrante del servidor:

	Tema: iotdm-1/mgmt/custom/<bundleId>/<actionId>
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

	Mensaje saliente del dispositivo:

	Tema: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

## Ejemplo
{: #example}

El siguiente ejemplo demuestra cómo puede definir una nueva ampliación de gestión de dispositivos y ejecutar una acción definida en dicha ampliación.

Algunas empresas fabrican dispositivos `exampleDeviceType`. Puede instalar y gestionar plug-ins para que se ejecuten en dispositivos `exampleDeviceType`. Para facilitar la gestión remota de plug-ins en dispositivos `exampleDeviceType`, el fabricante normalmente proporciona una ampliación de gestión de dispositivos que puede importar en la organización de {{site.data.keyword.iot_short_notm}}.

Se utiliza el siguiente documento JSON de ampliación en este ejemplo:

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
En este paquete de ampliación de gestión de dispositivos, se definen las siguientes acciones:

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

Para añadir la ampliación, utilice el siguiente mandato API REST:

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

Los dispositivos registrados en la organización `<orgID>` pueden especificar que dan soporte a acciones `exampleDeviceType-actions-v1` cuando publican una solicitud de gestión, que se muestra en el ejemplo siguiente:

```
	Mensaje saliente del dispositivo:

	Tema: iotdevice-1/mgmt/manage
	{
		"d": {
			"supports": {
				"exampleDeviceType-actions-v1": true
			}
		},
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
El dispositivo recibe la respuesta siguiente desde el {{site.data.keyword.iot_short_notm}}:

```
	Mensaje entrante del servidor:

	Tema: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
En este punto, puede iniciar las acciones de dispositivos definidas en la ampliación `exampleIoT-exampleDeviceType-v1`.

La siguiente carga útil se utiliza para iniciar una acción `installPlugin`:

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
Inicie la solicitud utilizando el siguiente mandato API REST:

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Cuando se envía el mandato, los dispositivos `device0` y `device1` de tipo `exampleDeviceType` reciben el siguiente mensaje MQTT:

```
	Mensaje entrante del servidor:

	Tema: iotdm-1/mgmt/custom/exampleDeviceType-actions-v1/installPlugin
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

Cada dispositivo toma una acción en el mensaje e instala los plug-in especificados. Cuando la instalación finaliza, los dispositivos envían un mensaje para indicar que la acción se ha completado satisfactoriamente.

```
	Mensaje saliente del dispositivo:

	Tema: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

En este punto, se completa la acción de gestión de dispositivos `installPlugin`.

## Ejemplos de la API
{: #api_examples}

Utilice las siguientes solicitudes API para gestionar los dispositivos:

- Para crear una nueva ampliación de gestión de dispositivos:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Para listar extensiones de gestión de dispositivos:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Para iniciar una solicitud de gestión de dispositivos:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Para listar las solicitudes de gestión de dispositivos que están en curso o que se han completado:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Para ver el estado de una determinada solicitud de gestión de dispositivos:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`

## Recetas sobre las extensiones de gestión de dispositivos

En las siguientes recetas se muestra el flujo necesario para manejar las extensiones de gestión de dispositivos:

- La receta [Paquetes de extensiones de gestión de dispositivos en WIoT Platform ![icono de enlace externo](../../../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/device-management-extension-packages-in-wiot-platform/){: new_window} contiene instrucciones para registrar un dispositivo gestionado con {{site.data.keyword.iot_short}} de modo que el dispositivo pueda recibir y manejar acciones de extensión de gestión de dispositivos. Los ejemplos de código de la receta están escritos utilizando la biblioteca de cliente Python.
