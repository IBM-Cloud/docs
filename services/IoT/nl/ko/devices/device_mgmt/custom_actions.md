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

# 디바이스 관리 확장
{: #custom_actions}

디바이스 관리 확장기능을 추가하여 요구사항을 충족하도록 {{site.data.keyword.iot_full}}의 디바이스 관리 기능을 확장할 수 있습니다. REST API 또는 {{site.data.keyword.iot_short_notm}} 대시보드를 사용하여 디바이스 관리 확장기능을 추가할 수 있습니다. 

{{site.data.keyword.iot_short_notm}}에서는 기본적으로 다음과 같은 디바이스 관리 조치를 지원합니다. 
- 디바이스 재부팅
- 팩토리 재설정
- 펌웨어 다운로드
- 펌웨어 업데이트

## 디바이스 관리 확장 패키지
{: #device_management_ext}

디바이스 관리 확장 패키지는 하나 이상의 디바이스 관리 조치를 정의하는 JSON 문서입니다. {{site.data.keyword.iot_short_notm}} 대시보드 또는 REST API를 사용하여 조치를 지원하는 디바이스에서 조치를 시작할 수 있습니다. 

다음 코드 샘플은 디바이스 관리 확장 패키지의 일반 형식을 표시합니다. 

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

### 사용자 정의 디바이스 관리 패키지 추가

{{site.data.keyword.iot_short_notm}} 대시보드를 사용하거나 API를 사용하여 사용자 정의 디바이스 관리 패키지를 추가할 수 있습니다. 

{{site.data.keyword.iot_short_notm}} 대시보드를 사용하여 사용자 정의 디바이스 관리 패키지를 추가하려면 다음을 수행하십시오. 

1. {{site.data.keyword.iot_short_notm}} 대시보드의 탐색줄에서 **설정**을 클릭하십시오. 
2. **사용자 정의 디바이스 관리 패키지**를 클릭하십시오. 
3. **패키지 추가** 단추를 클릭하십시오. 
4. 패키지 파일을 선택하고 **열기**를 클릭하십시오. 

API를 사용하여 사용자 정의 디바이스 관리 패키지를 추가하려면 [{{site.data.keyword.iot_short_notm}} API 문서 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}를 참조하십시오. 

### 확장 패키지 특성

디바이스 관리 확장 패키지에는 다음 특성이 포함되어 있습니다. 

|특성|설명|필수
|:---|:---|:---|
|`bundleId`|디바이스 관리 확장의 고유 ID입니다. |예|
|`version`|디바이스 관리 확장의 버전 문자열입니다. |아니오|
|`provider`|디바이스 관리 확장의 제공자 문자열이며, 길이는 1024자로 제한됩니다. |아니오|
|`displayName`|{{site.data.keyword.iot_short_notm}} 대시보드에 표시되는 `locale`: `String` 키-값 쌍의 맵입니다. 최소한 하나의 항목을 지정해야 합니다. |예|
|`description`|{{site.data.keyword.iot_short_notm}} 대시보드에 표시하기 위해 사용되는 `locale`: `String` 키-값 쌍의 맵입니다. 정의된 경우, 최소한 하나의 항목을 지정해야 합니다. |아니오|
|`actions`| 디바이스 관리 확장에 포함된 조치를 정의하는 `actionId`: `<action>` 키-값 쌍의 맵입니다. 최소한 하나의 항목을 지정해야 합니다. |예|

### 각 조치의 특성:

|특성|설명|필수
|:---|:---|
|`actionDisplayName`|{{site.data.keyword.iot_short_notm}} 대시보드에 표시되는 `locale`: `String` 키-값 쌍의 맵입니다. 최소한 하나의 항목을 지정해야 합니다. |예|
|`description`|{{site.data.keyword.iot_short_notm}} 대시보드에 표시하기 위해 사용되는 `locale`: `String` 키-값 쌍의 맵입니다. 선택사항입니다. 최소한 하나의 항목을 지정해야 합니다. |아니오|
|`parameters`|특정 조치에 대해 허용되는 매개변수의 배열입니다. 정의된 경우, 최소한 하나의 항목을 지정해야 합니다. |아니오|

### 각 조치 매개변수의 특성:

|특성|설명|필수
|:---|:---|
|`name`|조치의 매개변수에 대한 고유 ID입니다. |예|
|`value`|요청이 시작될 때 매개변수값을 유효성 검증하는 데 사용되는 정규식입니다. 지정되지 않은 경우, 유효성 검증이 발생하지 않습니다. |아니오|
|`required`|매개변수가 필수인지 여부를 판별하는 부울 값입니다. 값은 기본적으로 false로 설정됩니다.  |아니오|
|`defaultValue`|요청이 시작될 때 매개변수가 제공되지 않는 경우에 사용되는 값입니다. |아니오|

**참고:** `bundleId`, `version`, `actionId` 및 `parameterId` 값에는 최대 255자까지 포함될 수 있으며, 영숫자 문자(a-z, A-Z, 0-9) 및 다음의 특수 문자로만 구성될 수 있습니다. 
 - 대시(-)
 - 밑줄(\_)
 - 점(.)

## REST API
{: #rest_api}

다음과 같은 {{site.data.keyword.iot_short_notm}} REST API 명령을 사용하여 확장 패키지를 관리할 수 있습니다. 

- 모든 디바이스 관리 확장 패키지의 목록 가져오기:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- 새 디바이스 관리 확장 패키지 작성:
  `POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- 특정 디바이스 관리 확장 패키지 가져오기:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- 디바이스 관리 확장 패키지 업데이트:
  `PUT https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- 디바이스 관리 확장 패키지 삭제:
  `DELETE https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

디바이스 관리 확장 패키지의 REST API에 대한 자세한 정보는 [{{site.data.keyword.iot_short_notm}} API V2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} 문서를 참조하십시오. 


## 사용자 정의 디바이스 관리 조치 지원
{: #supporting_custom_device_management_actions}

확장 패키지에 정의된 디바이스 관리 조치는 해당 조치를 지원하는 디바이스에 의해서만 시작될 수 있습니다. 디바이스는 {{site.data.keyword.iot_short_notm}}에 관리 요청을 공개할 때 지원 가능한 조치 유형을 지정합니다. 

확장 패키지의 사용자 정의 조치를 지정하려면 다음 예제에 표시된 대로 디바이스가 요청의 supports 오브젝트에 확장 패키지의 번들 ID를 지정해야 합니다. 

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

디바이스 관리 요청에 대한 자세한 정보는 [디바이스 관리 프로토콜](index.html){: new_window}을 참조하십시오. 

## 사용자 정의 디바이스 관리 조치 시작
{: #initiating_custom_dm_actions}

사용자 정의 디바이스 관리 조치를 시작하려면, 디바이스 관리 조치를 시작하기 위한 기본 명령인 다음 REST API 명령을 사용하십시오. 

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

요청을 시작할 때는 다음 정보를 제공해야 합니다. 

- 조치 `<bundleId>/<actionId>`
- 조치가 시작되는 디바이스의 목록(최대 5000개 디바이스)
- 사용자 정의 조치 정의에 정의된 매개변수의 목록

요청을 시작하기 위한 페이로드의 형식은 다음과 같습니다. 

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


## 사용자 정의 디바이스 관리 조치 처리
{: #handling_custom_dm_actions}

사용자 정의 조치가 디바이스에서 시작되면 MQTT 메시지가 디바이스에 공개됩니다. MQTT 메시지에는 요청의 일부로서 지정된 매개변수가 포함되어 있습니다. 디바이스가 MQTT 메시지를 수신하는 경우, 이는 조치를 실행하거나 조치를 현재 완료할 수 없는 이유를 표시하는 오류 코드로 응답합니다. 

디바이스 조치가 성공적으로 완료된 경우, 디바이스는 `rc` 값이 `200`으로 설정된 응답을 공개합니다. 

다음 추출은 서버 및 디바이스 간에 발생하는 교환의 예제를 제공합니다. 

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

## 예제
{: #example}

다음 예제는 새 디바이스 관리 확장을 정의하고 해당 확장에 정의된 조치를 실행하는 방법을 예시합니다. 

일부 회사는 `exampleDeviceType` 디바이스를 제조합니다. `exampleDeviceType` 디바이스에서 실행할 수 있도록 플러그인을 설치하고 관리할 수 있습니다. `exampleDeviceType` 디바이스에서 플러그인의 원격 관리가 용이하도록, 제조업체는 일반적으로 {{site.data.keyword.iot_short_notm}} 조직으로 가져올 수 있는 디바이스 관리 확장을 제공합니다. 

다음의 확장 JSON 문서가 이 예제에서 사용됩니다. 

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
이 디바이스 관리 확장 패키지에는 다음 조치가 정의되어 있습니다.

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

확장을 추가하려면 다음 REST API 명령을 사용하십시오. 

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

`<orgID>` 조직에 등록된 디바이스는 관리 요청을 공개할 때 `exampleDeviceType-actions-v1` 조치를 지원함을 지정할 수 있으며, 이는 다음 예제에 표시되어 있습니다. 

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
디바이스는 {{site.data.keyword.iot_short_notm}}에서 다음 응답을 수신합니다.

```
	Incoming message from server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
이 시점에서 `exampleIoT-exampleDeviceType-v1` 확장에 정의된 디바이스 조치를 시작할 수 있습니다.

다음 페이로드가 `installPlugin` 조치를 시작하는 데 사용됩니다. 

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
다음 REST API 명령을 사용하여 요청을 시작하십시오.

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

명령이 제출되면 `exampleDeviceType` 유형의 `device0` 및 `device1` 디바이스에서 다음 MQTT 메시지를 수신합니다. 

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

각 디바이스는 메시지에 대해 조치를 취하고 지정된 플러그인을 설치합니다. 설치기 완료되면 디바이스는 조치가 성공적으로 완료되었음을 표시하는 메시지를 제출합니다. 

```
	Outgoing message from device:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

이 시점에 `installPlugin` 디바이스 관리 조치가 완료됩니다. 

## API 예제
{: #api_examples}

다음 API 요청을 사용하여 디바이스를 관리할 수 있습니다. 

- 새 디바이스 관리 확장 작성: 

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- 디바이스 관리 확장 나열: 

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- 디바이스 관리 요청 시작: 

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- 진행 중이거나 완료된 디바이스 관리 요청 나열: 

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- 특정 디바이스 관리 요청의 상태 보기: 

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`

## 디바이스 관리 확장에 대한 레시피

다음 레시피는 디바이스 관리 확장을 처리하는 데 필요한 플로우를 예시합니다. 

- [WIoT Platform의 디바이스 관리 확장 패키지 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/device-management-extension-packages-in-wiot-platform/){: new_window} 레시피는 디바이스가 디바이스 관리 확장 조치를 수신하고 처리할 수 있도록 {{site.data.keyword.iot_short}}에서 관리 디바이스를 등록하는 지시사항을 제공합니다. 레시피의 코드 샘플은 Python 클라이언트 라이브러리를 사용하여 작성되어 있습니다. 
