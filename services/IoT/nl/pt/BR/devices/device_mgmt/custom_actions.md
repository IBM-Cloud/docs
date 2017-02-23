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

# Ampliando o gerenciamento de dispositivo
{: #custom_actions}

É possível estender os recursos de gerenciamento de dispositivo no {{site.data.keyword.iot_full}} para atender seus requisitos incluindo extensões de gerenciamento de dispositivo. As extensões de gerenciamento de dispositivo podem ser incluídas usando a API de REST ou o painel {{site.data.keyword.iot_short_notm}}.

Por padrão, as ações de gerenciamento de dispositivo a seguir são suportadas pelo {{site.data.keyword.iot_short_notm}}:
- Reinicialização do dispositivo
- Reconfiguração de fábrica
- Download de firmware
- Atualização de Firmware

## Pacotes de extensão de gerenciamento de dispositivo
{: #device_management_ext}

Um pacote de extensão de gerenciamento de dispositivo é um documento JSON que define pelo menos uma ação de gerenciamento de dispositivo. As ações podem ser iniciadas em quaisquer dispositivos que suportem as ações usando o painel {{site.data.keyword.iot_short_notm}} ou a API de REST.

A amostra de código a seguir mostra o formato típico de um pacote de extensão de gerenciamento de dispositivo:

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

### Incluindo um pacote de gerenciamento de dispositivo customizado

Os pacotes de gerenciamento de dispositivo customizado podem ser incluídos usando o painel do {{site.data.keyword.iot_short_notm}} ou usando a API.

Para incluir um pacote de gerenciamento de dispositivo customizado usando o painel do {{site.data.keyword.iot_short_notm}}:

1. No painel do {{site.data.keyword.iot_short_notm}}, clique em **Configurações** na barra de navegação.
2. Clique em **Pacotes de gerenciamento de dispositivo customizado**.
3. Clique no botão **Incluir pacote**.
4. Selecione seu arquivo de pacote e clique em **Abrir**.

Para incluir um pacote de gerenciamento de dispositivo customizado usando a API, veja a [documentação da API do {{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

### Propriedades do pacote de extensão

Um pacote de extensão de gerenciamento de dispositivo contém as propriedades a seguir:

|Propriedade|Descrição|Necessárias
|:---|:---|:---|
|`bundleId`|Identificador exclusivo para uma extensão de gerenciamento de dispositivo.|Sim|
|`version`|Sequência de versões para uma extensão de gerenciamento de dispositivo.|no|
|`provider`|Sequência do provedor para uma extensão de gerenciamento de dispositivo, limitada a 1024 caracteres.|no|
|`displayName`|Mapa de pares de chave-valor `locale`: `String` mostrados no painel do {{site.data.keyword.iot_short_notm}}. Deve-se especificar pelo menos uma entrada.|Sim|
|`description`|Mapa de pares de chave-valor `locale`: `String` usados para exibição no painel do {{site.data.keyword.iot_short_notm}}. Se definido, deve-se especificar pelo menos uma entrada.|no|
|`actions`| Mapa de pares chave-valor `actionId`: `<action>` que definem as ações que estão contidas em uma extensão de gerenciamento de dispositivo. Deve-se especificar pelo menos uma entrada.|Sim|

### Propriedades para cada ação:

|Propriedade|Descrição|Necessárias
|:---|:---|
|`actionDisplayName`|Mapa de pares de chave-valor `locale`: `String` mostrados no painel do {{site.data.keyword.iot_short_notm}}. Deve-se especificar pelo menos uma entrada.|Sim|
|`description`|Mapa de pares de chave-valor `locale`: `String` usados para exibição no painel do {{site.data.keyword.iot_short_notm}}. Opcional. Deve-se especificar pelo menos uma entrada.|no|
|`parameters`|Matriz de parâmetros que são permitidos para uma ação específica. Se definido, deve-se especificar pelo menos uma entrada.|no|

### Propriedades para cada parâmetro de ação:

|Propriedade|Descrição|Necessárias
|:---|:---|
|`name`|Identificador exclusivo para um parâmetro em uma ação|Sim|
|`value`|Expressão regular usada para validar valores de parâmetros quando uma solicitação é iniciada. Se não for especificada, a validação não ocorre.|no|
|`required`|O valor booleano que determina se o parâmetro é necessário. O valor está configurado por padrão como false. |no|
|`defaultValue`|Valor a ser usado se o parâmetro não for fornecido quando uma solicitação for iniciada|no|

**Nota:** os valores de `bundleId`, `version`, `actionId` e `parameterId` são limitados a 255 caracteres e podem consistir somente em caracteres alfanuméricos (a-z, A-Z, 0-9) e os caracteres especiais a seguir:
 - travessão (-)
 - sublinhado (\_)
 - ponto (.)

## APIs REST
{: #rest_api}

Use os comandos da API (interface de programação de aplicativos) REST do {{site.data.keyword.iot_short_notm}} para gerenciar seus pacotes de extensão:

- Para obter uma lista de todos os pacotes de extensão de gerenciamento de dispositivo:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Para criar um novo pacote de extensão de gerenciamento de dispositivo:
  `POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- Para obter um pacote de extensão de gerenciamento de dispositivo:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Para atualizar um pacote de extensão de gerenciamento de dispositivo:
  `PUT https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- Para excluir um pacote de extensão de gerenciamento de dispositivo:
  `DELETE https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

Para obter mais informações sobre as APIs (interfaces de programação de aplicativos) REST para os pacotes de extensão de gerenciamento de dispositivo, consulte a documentação do [{{site.data.keyword.iot_short_notm}} API V2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


## Suportando ações de gerenciamento de dispositivo customizadas
{: #supporting_custom_device_management_actions}

As ações de gerenciamento de dispositivo definidas em seus pacotes de extensão podem ser iniciadas somente por dispositivos que suportam essas ações. Quando um dispositivo publica uma solicitação de gerenciamento no {{site.data.keyword.iot_short_notm}}, o dispositivo especifica os tipos de ações que ele pode suportar.

Para especificar ações customizadas de um pacote de extensão, o dispositivo deve especificar o identificador de pacote configurável para o pacote de extensão no objeto de suporte da solicitação, conforme mostrado no exemplo a seguir:

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

Para obter mais informações sobre solicitações de gerenciamento de dispositivo, consulte [Protocolo de gerenciamento de dispositivo](index.html){: new_window}.

## Iniciando ações de gerenciamento de dispositivo customizadas
{: #initiating_custom_dm_actions}

Para iniciar ações customizadas de gerenciamento de dispositivo, use o comando da API (interface de programação de aplicativos) REST a seguir, que é o comando padrão para iniciar ações de gerenciamento de dispositivo:

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Deve-se fornecer as informações a seguir ao iniciar uma solicitação:

- A ação `<bundleId>/<actionId>`
- Uma lista de dispositivos nos quais iniciar a ação, até no máximo 5000 dispositivos
- Uma lista de parâmetros que estão definidos na definição da ação customizada

A carga útil para iniciar uma solicitação tem o formato a seguir:

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


## Manipulando ações de gerenciamento de dispositivo customizadas
{: #handling_custom_dm_actions}

Quando uma ação customizada é iniciada em um dispositivo, uma mensagem MQTT é publicada no dispositivo. A mensagem MQTT contém quaisquer parâmetros que foram especificados como parte da solicitação. Quando o dispositivo recebe a mensagem MQTT, ele executa a ação ou responde com um código de erro que indica por que ele não pode concluir a ação no momento.

Quando uma ação de dispositivo é concluída com sucesso, o dispositivo publica uma resposta na qual o valor de `rc` está configurado para `200`.

A extração a seguir fornece um exemplo da troca que ocorre entre um servidor e um dispositivo.

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

## Exemplo
{: #example}

O exemplo a seguir demonstra como é possível definir uma nova extensão de gerenciamento de dispositivo e executar uma ação que está definida nessa extensão.

Algumas empresas fabricam dispositivos `exampleDeviceType`. É possível instalar e gerenciar plug-ins para execução em dispositivos `exampleDeviceType`. Para facilitar o gerenciamento remoto de plug-ins em dispositivos `exampleDeviceType`, o fabricante geralmente fornece uma extensão de gerenciamento de dispositivo que é possível importar para sua organização do {{site.data.keyword.iot_short_notm}}.

O documento JSON de extensão a seguir é usado neste exemplo:

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
Nesse pacote de extensão de gerenciamento de dispositivo, estão definidas as ações a seguir:

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

Para incluir a extensão, use o comando da API (interface de programação de aplicativos) REST a seguir:

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

Os dispositivos registrados na organização `<orgID>` podem especificar que eles suportam ações `exampleDeviceType-actions-v1` ao publicarem uma solicitação de gerenciamento, o que é mostrado no exemplo a seguir:

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
O dispositivo recebe a resposta a seguir do {{site.data.keyword.iot_short_notm}}:

```
	Incoming message from server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
Neste ponto, é possível iniciar as ações do dispositivo definidas na extensão `exampleIoT-exampleDeviceType-v1`.

A carga útil a seguir é usada para iniciar uma ação `installPlugin`:

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
Inicie a solicitação usando o comando da API (interface de programação de aplicativos) REST a seguir:

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

Quando o comando for enviado, os dispositivos `device0` e `device1` do tipo `exampleDeviceType` recebem a mensagem MQTT a seguir:

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

Cada dispositivo toma uma ação na mensagem e instala o plug-in especificado. Quando a instalação for concluída, os dispositivos enviam uma mensagem para indicar que a ação foi concluída com sucesso.

```
	Outgoing message from device:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

Neste momento, a ação de gerenciamento de dispositivo `installPlugin` é concluída.

## Exemplos de API
{: #api_examples}

Use as solicitações da API (interface de programação de aplicativos) a seguir para gerenciar seus dispositivos:

- Para criar uma nova extensão de gerenciamento de dispositivo:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Para listar as extensões de gerenciamento de dispositivo:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- Para iniciar uma solicitação de gerenciamento de dispositivo:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Para listar solicitações de gerenciamento de dispositivo que estão em andamento ou concluídas:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- Para visualizar o status de uma solicitação gerenciamento de dispositivo específica:

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`

## Orientações sobre Extensões de gerenciamento de dispositivo

As orientações a seguir demonstram o fluxo que é necessário para manipular Extensões de gerenciamento de dispositivo:

- A orientação [Pacotes de Extensão de gerenciamento de dispositivo no WIoT Platform ![Ícone de link externo](../../../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/device-management-extension-packages-in-wiot-platform/){: new_window} fornece instruções para registrar um dispositivo gerenciado com o {{site.data.keyword.iot_short}} para que o dispositivo possa receber e manipular ações de Extensão de gerenciamento de dispositivo. As amostras de código na orientação são gravadas usando a Biblioteca do Cliente Python.
