---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}  
{:codeblock: .codeblock}
{:pre: .pre}


# 디바이스 관리 요청
{: #requests}


{{site.data.keyword.iot_full}}은 하나 이상의 디바이스에 시작할 수 있는 조치를 제공합니다. 이러한 조치는 대시보드 또는 REST API를 사용하여 시작될 수 있습니다. 사용할 수 있는 조치의 유형은 **디바이스 조치** 및 **펌웨어 조치**입니다. 

## 대시보드를 사용하여 디바이스 관리 요청 시작
{: #initiating-dm-dashboard}

대시보드를 통해 요청을 시작할 수 있습니다. 디바이스 페이지의 **조치** 탭을 사용하십시오. **조치 시작**을 클릭하여 조치를 선택하고, 디바이스를 선택하고, 선택한 조치에서 지원하는 추가 매개변수를 지정하십시오. 

## REST API를 사용하여 디바이스 관리 요청 시작
{: #initiating-dm-api}

요청은 다음 REST API 샘플을 사용하여 시작될 수 있습니다.   

`POST https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

디바이스 관리 요청의 본문에 대한 자세한 정보는 [API 문서 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}를 참조하십시오. 

## 디바이스 조치
{: #device-actions}

디바이스는 관리 요청을 공개할 때 디바이스 조치를 지원함을 지정할 수 있습니다. 디바이스 조치 요청은 디바이스가 디바이스 재부팅 및 디바이스 재설정 조치에 응답할 수 있음을 {{site.data.keyword.iot_short_notm}}에 표시합니다. 


## 디바이스 조치 - 재부팅
{: #device-actions-reboot}

{{site.data.keyword.iot_short_notm}} 대시보드를 사용하거나 REST API를 사용하여 디바이스 재부팅 조치를 시작할 수 있습니다. 

REST API를 사용하여 디바이스 재부팅을 시작하려면 다음에 POST 요청을 발행하십시오. 

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

다음 정보를 제공하십시오. 

- 조치 `device/reboot`
- 재부팅할 디바이스의 목록(최대 5000개 디바이스)

예제 디바이스 재부팅 요청:

```
{
    "action": "device/reboot",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

요청이 시작되면 MQTT 메시지가 재부팅 요청의 본문에 지정된 모든 디바이스에 공개됩니다. 각 디바이스마다, 재부팅 조치가 시작될 수 있는지 여부를 표시하기 위해 응답을 돌려보내야 합니다. 이 오퍼레이션을 즉시 시작할 수 있으면 `rc` 매개변수를 `202`로 설정하십시오. 재부팅 시도에 실패하는 경우에는 `rc` 매개변수를 `500`으로 설정하고 `message` 매개변수를 이에 맞게 설정하십시오. 재부팅이 지원되지 않는 경우에는 `rc` 매개변수를 `501`로 설정하고 선택사항으로 `message` 매개변수를 이에 맞게 설정하십시오. 

재부팅 조치는 재부팅 이후 디바이스가 디바이스 관리 요청을 전송할 때 완료됩니다. 

### 디바이스 재부팅 요청의 주제

서버는 다음 주제에서 디바이스에 대해 재부팅 요청을 공개합니다. 

```
iotdm-1/mgmt/initiate/device/reboot
```

### 디바이스 재부팅 요청의 메시지 형식


요청 형식:

```
Incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

응답 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## 디바이스 조치 - 팩토리 재설정
{: #device-actions-factory-reset}

{{site.data.keyword.iot_short_notm}} 대시보드를 사용하거나 REST API를 사용하여 팩토리 재설정 조치를 시작할 수 있습니다. 

REST API를 사용하여 디바이스 팩토리 재설정을 시작하려면 다음에 POST 요청을 발행하십시오. 

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

다음 정보가 제공됩니다. 

- 조치 `device/factoryReset`
- 재설정할 디바이스의 목록(최대 5000개 디바이스)

다음 샘플은 예제 디바이스 재설정 요청을 제공합니다. 

```
{
    "action": "device/factoryReset",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

디바이스 재설정 요청이 시작되면 MQTT 메시지가 요청의 본문에 지정된 모든 디바이스에 공개됩니다. 각 디바이스마다, 팩토리 재설정 조치가 시작될 수 있는지 여부를 표시하기 위해 응답을 리턴해야 합니다. 이 조치를 즉시 시작할 수 있으면 응답 코드가 `202`로 설정됩니다. 팩토리 재설정 시도에 실패하는 경우에는 `rc` 매개변수를 `500`으로 설정하고 `message` 매개변수를 이에 맞게 설정하십시오. 팩토리 재설정 조치가 지원되지 않는 경우에는 `rc` 매개변수를 `501`로 설정하고 선택사항으로 `message` 매개변수를 이에 맞게 설정하십시오. 

팩토리 재설정 조치는 팩토리 재설정 이후 디바이스가 디바이스 관리 요청을 전송할 때 완료됩니다. 

### 팩토리 재설정 요청의 주제

서버는 디바이스에 대해 다음 요청을 공개합니다. 

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### 팩토리 재설정 요청의 메시지 형식


요청 형식:

```
The following topic shows the incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

응답 형식:

```
The following topic shows an outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## 펌웨어 조치
{: #firmware-actions}

디바이스에 있다고 알려진 펌웨어 레벨이 `deviceInfo.fwVersion` 속성에 저장되어 있습니다. `mgmt.firmware` 속성은 펌웨어 업데이트를 수행하고 해당 상태를 관찰하는 데 사용됩니다. 

**중요:** 관리 디바이스는 펌웨어 조치를 지원하기 위해 `mgmt.firmware` 속성의 관찰을 지원해야 합니다. 

펌웨어 업데이트 프로세스는 개별 조치로 분리됩니다. 
- 펌웨어 다운로드
- 펌웨어 업데이트

각 펌웨어 조치의 상태는 디바이스의 개별 속성에 저장되어 있습니다. `mgmt.firmware.state` 속성은 펌웨어 다운로드의 상태를 설명합니다. 다음 표에는 `mgmt.firmware.state` 속성에 대해 설정될 수 있는 가능한 값이 설명되어 있습니다. 

 |값 |상태  | 의미 |
 |:---|:---|:---|
 |0  | 유휴        | 디바이스가 펌웨어를 다운로드하고 있지 않습니다.  |  
 |1  | 다운로드 중 | 디바이스가 펌웨어를 다운로드 중입니다.  |
 |2  | 다운로드됨  | 디바이스가 펌웨어 업데이트를 성공적으로 다운로드했으며 이를 설치할 준비가 되었습니다.  |


`mgmt.firmware.updateStatus` 속성은 펌웨어 업데이트의 상태를 설명합니다. `mgmt.firmware.updateStatus` 속성의 가능한 값은 다음과 같습니다. 

|값 |상태 | 의미 |  
|:---|:---|:---|
|0 | 완료 | 펌웨어가 성공적으로 업데이트되었습니다.  |
|1 | 진행 중 | 펌웨어 업데이트가 시작되었지만 아직 완료되지 않았습니다. |
|2 | 메모리 부족 | 오퍼레이션 중에 메모리 부족 상태가 발견되었습니다. |
|3 | 연결 끊김     | 펌웨어 다운로드 중에 연결이 끊겼습니다.  |
|4 | 검증 실패 | 펌웨어 검증에 실패했습니다.  |
|5 | 지원되지 않는 이미지   | 다운로드된 펌웨어 이미지를 디바이스에서 지원하지 않습니다.  |
|6 | 올바르지 않은 URI         | 디바이스가 제공된 URI에서 펌웨어를 다운로드할 수 없습니다.  |

## 펌웨어 조치 - 다운로드
{: #firmware-actions-download}

{{site.data.keyword.iot_short_notm}} 대시보드를 사용하거나 REST API를 사용하여 펌웨어 다운로드 조치를 시작할 수 있습니다. 

REST API를 사용하여 펌웨어 다운로드를 시작하려면 다음에 POST 요청을 발행하십시오. 

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

다음 정보가 제공됩니다. 

- 조치 `firmware/download`
- 이미지를 수신할 디바이스의 목록(최대 5000개 디바이스)
- 펌웨어 이미지에 대한 URI(선택사항)
- 이미지를 유효성 검증하기 위한 검증 문자열(선택사항)
- 펌웨어 이름(선택사항)
- 펌웨어 버전(선택사항)

다음 샘플은 모든 다음 예제 메시지의 기반이 되는 펌웨어 다운로드 요청을 표시합니다. 

```
{
   "action" : "firmware/download",
   "parameters" : [{
         "name" : "uri",
         "value" : "some uri for firmware location"
      }, {
         "name" : "name",
         "value" : "some firmware name"
      }, {
         "name" : "verifier",
         "value" : "some validation code"
      }, {
         "name" : "version",
         "value" : "some firmware version"
      }
   ],
   "devices" : [{
         "typeId" : "someType",
         "deviceId" : "someId"
      }
   ]
}
```

선택 매개변수가 지정되지 않은 경우 다음 프로세스의 첫 번째 단계는 건너뜁니다. 

{{site.data.keyword.iot_short_notm}}의 디바이스 관리 서버는 디바이스 관리 프로토콜을 사용하여 디바이스에 요청을 전송하며, 디바이스는 펌웨어 다운로드를 시작합니다. 다운로드 프로세스는 다음 단계로 구성됩니다. 

1. 펌웨어 세부사항 업데이트 요청은 `iotdm-1/device/update` 주제에서 전송됩니다. 업데이트 요청은 요청된 펌웨어가 현재 설치된 펌웨어와 다른지 여부를 디바이스가 유효성 검증할 수 있도록 합니다. 차이가 있으면 `rc` 매개변수를 `204`로 설정하십시오. 이는 `Changed` 상태로 변환됩니다.
  
다음 예에서는 이전에 전송된 예제 펌웨어 다운로드 요청에 대해 예상되는 메시지와 차이점이 발견되는 경우 어떤 응답이 전송되는지 표시합니다. 
```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/device/update
   Message:
   {
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194",
      "d" : {
         "fields" : [{
               "field" : "mgmt.firmware",
               "value" : {
                  "version" : "some firmware version",
                  "name" : "some firmware name",
                  "uri" : "some uri for firmware location",
                  "verifier" : "some validation code",
                  "state" : 0,
                  "updateStatus" : 0,
                  "updatedDateTime" : ""
               }
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
이 응답은 다음 요청을 트리거합니다.
2. 펌웨어 다운로드 상태 `iotdm-1/observe`에 대한 관찰 요청이 전송됩니다.
관찰 요청은 디바이스가 펌웨어 다운로드를 시작할 준비가 되었는지 여부를 확인합니다. 다운로드를 즉시 시작할 수 있으면 `rc` 매개변수를 `200`(`Ok`)으로 설정하고 `mgmt.firmware.state` 속성을 `0`(`Idle`)으로 설정하며 `mgmt.firmware.updateStatus` 속성을 `0`(`Idle`)으로 설정하십시오. 다음 코드는 {{site.data.keyword.iot_short_notm}} 및 디바이스 간의 예제 교환입니다. 
   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/observe
   Message:
   {
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
         "fields" : [ {
            "field" : "mgmt.firmware"
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
이 교환은 마지막 단계를 트리거합니다.   

3. 다운로드 요청은 `iotdm-1/mgmt/initiate/firmware/download` 주제에서 전송됩니다. 

   다운로드 요청은 펌웨어 다운로드를 시작하도록 디바이스에 알립니다. 조치를 즉시 시작할 수 있으면 `rc` 매개변수를 `202`로 설정하십시오. 다음 코드는 다운로드 요청을 시작하는 예제를 제공합니다. 

   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/mgmt/initiate/firmware/download
   Message:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

펌웨어 다운로드가 이 방법으로 시작된 이후, 디바이스는 다운로드의 상태를 {{site.data.keyword.iot_short_notm}}에 보고해야 합니다. 디바이스는 `iotdevice-1/notify`-topic에 대해 메시지를 공개하여 상태를 보고하며, 여기서 `mgmt.firmware.state` 속성은 `1`(`Downloading`) 또는 `2`(`Downloaded`)로 설정됩니다.
다음 샘플은 펌웨어 다운로드를 시작하는 예제를 표시합니다. 

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "123456789",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 1
             }
      } ]
   }
}


Wait some time...


Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "1234567890",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 2
             }
      } ]
   }
}
```



`mgmt.firmware.state` 속성이 `2`로 설정되어 알림이 공개된 후에는 요청이 `iotdm-1/cancel`-topic에서 트리거됩니다. 이 요청은 `mgmt.firmware` 속성의 관찰을 취소합니다.
`rc` 매개변수가 `200`으로 설정된 응답이 전송된 후에는 펌웨어 다운로드가 완료됩니다. 다음 코드는 예제를 제공합니다. 

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

다음 정보가 오류 처리에 유용합니다. 

- `mgmt.firmware.state` 속성이 `0`("유휴")이 아니면 응답 코드 `400`이 있는 오류와 선택적 메시지 텍스트를 전송하십시오. 
- `mgmt.firmware.uri` 속성이 설정되지 않았거나 올바른 URI가 아니면 `rc` 매개변수를 `400`으로 설정하십시오. 
- 펌웨어 다운로드 시도에 실패하면 `rc` 매개변수를 `500`으로 설정하고 선택사항으로 `message` 매개변수를 이에 맞게 설정하십시오. 
- 펌웨어 다운로드가 지원되지 않으면 `rc` 매개변수를 `500`으로 설정하고 선택사항으로 `message` 매개변수를 이에 맞게 설정하십시오. 
- 디바이스가 실행 요청을 수신하면 `mgmt.firmware.state` 속성을 `0`(유휴)에서 `1`(다운로드 중)로 변경하십시오. 
- 다운로드가 완료되면 `mgmt.firmware.state` 속성을 `2`(다운로드됨)로 설정하십시오. 
- 다운로드 중에 오류가 발생하면 `mgmt.firmware.state` 속성을 `0`(유휴)으로 설정하고 `mgmt.firmware.updateStatus` 속성을 다음 오류 상태 값 중 하나로 설정하십시오. 
  - 2(메모리 부족)
  - 3(연결 끊김)
  - 6(올바르지 않은 URI)
- 펌웨어 검사기가 설정된 경우, 디바이스는 펌웨어 이미지를 검증하려고 시도합니다. 이미지 검증에 실패하면 `mgmt.firmware.state` 속성을 `0`(유휴)로 설정하고 `mgmt.firmware.updateStatus` 속성을 오류 상태 값 `4`(검증 실패)로 설정하십시오. 

## 펌웨어 조치 - 업데이트
{: #firmware-actions-update}

다운로드된 펌웨어의 설치는 POST 요청을 다음에 발행하여 REST API를 사용하여 시작됩니다. 

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

다음 정보가 제공됩니다. 

- 조치 `firmware/update`
- 이미지를 수신하기 위한 디바이스의 목록(모두 동일한 디바이스 유형임). 
- 펌웨어 이미지에 대한 URI(선택사항)
- 이미지를 유효성 검증하기 위한 검증 문자열(선택사항)
- 펌웨어 이름(선택사항)
- 펌웨어 버전(선택사항)

다음 코드는 예제 요청입니다. 

```
   {
      "action" : "firmware/update",
      "devices" : [{
            "typeId" : "someType",
            "deviceId" : "someId"
         }
      ]
   }

```

선택 매개변수가 지정되어 있는 경우 디바이스에서 수신하는 첫 번째 메시지는 디바이스 업데이트 요청입니다. 이 디바이스 업데이트 요청은 펌웨어 다운로드 요청의 첫 번째 메시지와 유사합니다. 

펌웨어 업데이트의 상태를 모니터하기 위해 {{site.data.keyword.iot_short_notm}}은 우선 `iotdm-1/observe` 주제에서 관찰자 요청을 트리거합니다. 디바이스가 업데이트 프로세스를 시작할 준비가 된 경우, 이는 `rc` 매개변수가 `200`으로 설정되고 `mgmt.firmware.state` 속성이 `0`으로 설정되며 `mgmt.firmware.updateStatus` 속성이 `0`으로 설정된 응답을 전송합니다. 

다음 코드는 예제를 제공합니다. 

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/observe
Message:
{
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [
         {
            "field": "mgmt.firmware"
         }
      ]
   }
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```



펌웨어 업데이트가 성공적으로 다운로드된 후에, {{site.data.keyword.iot_short_notm}}의 디바이스 관리 서버는 디바이스 관리 프로토콜을 사용하여 지정된 디바이스가 `iotdm-1/mgmt/initiate/firmware/update` 주제를 사용하여 펌웨어 설치를 시작하도록 요청합니다.
이 오퍼레이션을 즉시 시작할 수 있으면 `rc` 매개변수를 `202`로 설정하십시오.
펌웨어의 다운로드가 이전에 실패했으면 `rc` 매개변수를 `400`으로 설정하십시오. 

다음 코드는 예제를 표시합니다. 

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/mgmt/initiate/firmware/update
Message:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

펌웨어 업데이트 요청을 완료하기 위해, 디바이스는 해당 `iotdevice-1/notify`-topic에서 공개된 상태 메시지를 사용하여 해당 업데이트 상태를 {{site.data.keyword.iot_short_notm}}에 보고합니다.
펌웨어 업데이트가 완료되면 `mgmt.firmware.updateStatus` 속성이 `0`(성공)으로 설정되며 `mgmt.firmware.state` 속성이 `0`(유휴)으로 설정됩니다. 그리고 다운로드된 펌웨어 이미지를 디바이스에서 삭제할 수 있으며 `deviceInfo.fwVersion` 속성이 `mgmt.firmware.version` 속성 값으로 설정됩니다. 

다음 코드는 알림 메시지의 예제를 제공합니다. 

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "d" : {
      "fields": [
         {
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```

{{site.data.keyword.iot_short_notm}}이 완료된 펌웨어 업데이트의 알림을 수신하는 경우, 이는 `mgmt.firmware` 속성의 관찰을 취소할 수 있도록 `iotdm-1/cancel`-topic에서 마지막 요청을 트리거합니다. 


다음 예제에서 표시된 대로, `rc` 매개변수가 `200`으로 설정된 응답이 전송되면 펌웨어 업데이트 요청이 완료됩니다. 

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [
         {
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

다음 목록에서는 오류 및 프로세스 처리의 일부 유용한 정보를 제공합니다. 

- 펌웨어 업데이트 시도에 실패하면 `rc` 매개변수를 `500`으로 설정하고, 선택사항으로 관련 정보를 포함하도록 `message` 매개변수를 설정하십시오. 
- 펌웨어 업데이트가 지원되지 않으면 `rc` 매개변수를 `501`로 설정하고, 선택사항으로 관련 정보를 포함하도록 `message` 매개변수를 설정하십시오. 
- `mgmt.firmware.state` 속성이 `2`(다운로드됨)가 아니면 `rc` 매개변수가 `400`으로 설정된 오류와 선택적 메시지 텍스트를 전송하십시오. 
- 그렇지 않으면, `mgmt.firmware.updateStatus` 속성을 `1`(진행 중)로 설정하십시오. 일반적으로 펌웨어 설치가 시작됩니다. 
- 펌웨어 설치에 실패하면 `mgmt.firmware.updateStatus` 속성을 다음 값 중 하나로 설정하십시오. 
  - `2`(메모리 부족)
  - `5`(지원되지 않는 이미지)


**중요:** `mgmt.firmware`에 대한 현재 관찰이 존재할 때 단일 알림 메시지만 전송될 수 있도록 `mgmt.firmware` 속성의 일부로서 나열된 모든 매개변수를 동시에 설정해야 합니다. 

## 디바이스 조치 및 펌웨어 조치에 대한 레시피

다음 레시피는 디바이스 및 펌웨어 조치를 수행하는 데 필요한 전체 플로우를 예시합니다. 

- [WIoT Platform에서 디바이스 관리 – 롤백 및 팩토리 재설정 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}

- [디바이스 시작 펌웨어 업데이트 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/){: new_window}

- [플랫폼 시작 펌웨어 업데이트 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [백그라운드 실행의 플랫폼 시작 펌웨어 업데이트 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [펌웨어 롤백 및 팩토리 재설정 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}
