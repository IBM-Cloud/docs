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


# 디바이스 관리 프로토콜
{: #index}

## 소개
{: #introduction}

{{site.data.keyword.iot_full}}은 두 개의 디바이스 클래스(**관리 디바이스** 및 **비관리 디바이스**)를 인식합니다. 

**관리 디바이스**는 디바이스 관리 에이전트가 포함된 디바이스로 정의됩니다. 디바이스 관리 에이전트는 디바이스가 디바이스 관리 프로토콜을 사용하여 {{site.data.keyword.iot_short_notm}} 디바이스 관리 서비스와 상호작용할 수 있도록 허용하는 로직 세트입니다. 관리 디바이스는 위치 업데이트, 펌웨어 다운로드 및 업데이트, 재부팅 및 팩토리 재설정이 포함된 디바이스 관리 오퍼레이션을 수행할 수 있습니다. 

디바이스 관리 프로토콜은 지원되는 오퍼레이션의 세트를 정의합니다. 디바이스 관리 에이전트는 오퍼레이션의 서브세트를 지원할 수 있지만, **관리** 및 **비관리** 오퍼레이션은 지원되어야 합니다. 펌웨어 조치 오퍼레이션을 지원하는 디바이스는 관찰도 지원해야 합니다. 

디바이스 관리 프로토콜은 MQTT 메시징 프로토콜 위에서 빌드됩니다. 디바이스 관리 프로토콜이 MQTT와 상호작용하는 방법에 대한 자세한 정보는 [디바이스에 대한 MQTT 연결](../mqtt.html)을 참조하십시오. 


### 디바이스 관리 라이프사이클

1. 디바이스 및 이와 연관된 디바이스 유형은 대시보드 또는 REST API를 사용하여 {{site.data.keyword.iot_short_notm}}에서 작성됩니다. 
2. 디바이스는 {{site.data.keyword.iot_short_notm}}에 연결되며 **관리 디바이스** 오퍼레이션을 사용하여 관리 디바이스가 됩니다. 
3. 디바이스 오퍼레이션을 사용하여 디바이스의 메타데이터를 보고 조작할 수 있습니다. 이러한 오퍼레이션(예: 펌웨어 업데이트 및 디바이스 재시작 오퍼레이션)은 "디바이스 모델" 문서에서 간략하게 설명되어 있습니다. 디바이스 모델에 대한 자세한 정보는 [디바이스 모델](https://console.ng.bluemix.net/docs/services/IoT/reference/device_model.html)을 참조하십시오. 
4. 디바이스는 디바이스 관리 프로토콜을 사용하여 오류 코드 및 진단 정보, 해당 위치에 대한 업데이트를 전달할 수 있습니다. 
5. 대형 디바이스 군집의 작동되지 않는 디바이스를 처리하기 위해 **관리 디바이스** 오퍼레이션 요청에는 선택적 수명 매개변수가 포함되어 있습니다. 수명 매개변수는 휴면으로 분류되어 비관리 디바이스가 되지 않도록 디바이스가 또 다른 **관리 디바이스** 요청을 작성해야 하는 시간(초)입니다. 
6. 디바이스가 더 이상 사용되지 않는 경우에는 대시보드 또는 REST API를 사용하여 {{site.data.keyword.iot_short_notm}}에서 이를 제거할 수 있습니다. 

[IBM Watson IoT Platform에 관리 디바이스로 Raspberry Pi 연결 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/){: new_window} 레시피를 참조하십시오. 

### 리턴 코드 요약


다음 표에는 디바이스 관리 라이프사이클 중에 다양한 단계에서 생성되는 리턴 코드가 표시되어 있습니다. 

|리턴 코드 |메시지 |
|:---|:---|
|200   |오퍼레이션에 성공함|
|202   |허용됨(명령 시작의 경우)|
|204   |변경됨(속성 업데이트의 경우)|
|400   |잘못된 요청(디바이스의 상태가 이 명령에 대해 적합하지 않은 경우)|
|404   |속성을 찾을 수 없음(오퍼레이션이 올바르지 않은 주제에 공개된 경우에도 사용됨)|
|409   |충돌 때문에 리소스를 업데이트할 수 없음(예: 두 개의 동시 요청으로 리소스를 업데이트 중이므로 나중에 업데이트를 재시도할 수 있음)|
|500   |예상치 못한 디바이스 오류|
|501   |오퍼레이션이 구현되지 않음|


## 디바이스 관리 요청
{: #manage_device_request}

디바이스는 디바이스 관리 요청을 사용하여 관리 디바이스가 됩니다. 디바이스 관리 요청은 {{site.data.keyword.iot_short_notm}}에 연결한 후에 디바이스가 전송하는 첫 번째 디바이스 관리 요청이어야 합니다. 디바이스 관리 에이전트는 일반적으로 시작되거나 다시 시작될 때마다 이러한 유형의 요청을 전송합니다. 

**중요:** 이 오퍼레이션에 대한 지원은 관리 디바이스에 필수입니다. 


### 디바이스 관리 요청의 주제

디바이스는 다음 주제에 대해 디바이스 관리 요청을 공개합니다. 

```
iotdevice-1/mgmt/manage
```

서버는 다음 주제에서 디바이스 관리 요청에 응답합니다. 

```
iotdm-1/response
```




### 디바이스 관리 요청의 메시지 형식


디바이스 관리 요청에서 `d` 필드와 이의 모든 하위 필드는 선택사항입니다. `metadata` 및 `deviceInfo` 필드 값은 전송된 경우 전송 중인 디바이스의 대응되는 속성을 대체합니다. 

선택사항인 `lifetime` 필드는 휴면으로 분류되어 비관리 디바이스가 되지 않도록 디바이스가 또 다른 관리 디바이스 요청을 전송해야 하는 기간(초)입니다. `lifetime` 필드가 생략되거나 `0`으로 설정된 경우, 관리 디바이스는 휴면 상태가 되지 않습니다. `lifetime` 필드의 최소 지원 설정은 `3600`초(1시간)입니다. 

선택사항인 `supports.deviceActions` 및 `supports.firmwareActions` 필드는 디바이스 관리 에이전트의 기능을 표시합니다. `supports.deviceActions`가 설정된 경우, 에이전트는 재시작 및 팩토리 재설정 조치를 모두 지원합니다. 재시작 및 팩토리 재설정 간에 구분하지 않는 디바이스의 경우에는 두 조치에 대해 동일한 작동을 사용할 수 있습니다. `supports.firmwareActions`이 설정된 경우, 에이전트는 펌웨어 다운로드 및 펌웨어 업데이트 조치를 둘 다 지원합니다. 

다음 샘플은 요청 형식을 표시합니다. 

```
Outgoing message from the device:

Topic: iotdevice-1/mgmt/manage
{
    "d": {
        "metadata":{},
        "lifetime": number,
        "supports": {
            "deviceActions": boolean,
            "firmwareActions": boolean
        },
        "deviceInfo": {
            "serialNumber": "string",
            "manufacturer": "string",
            "model": "string",
            "deviceClass": "string",
            "description" :"string",
            "fwVersion": "string",
            "hwVersion": "string",
            "descriptiveLocation": "string"
        }
    },
    "reqId": "string"
}
```

다음 샘플은 응답 형식을 표시합니다. 

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### 디바이스 관리 요청의 응답 코드

|응답 코드 |메시지 |
|:---|:---|
|200   |오퍼레이션에 성공했습니다. |
|400   |입력 메시지가 예상된 형식과 일치하지 않거나, 값 중 하나가 유효한 범위를 벗어납니다. |
|404   |주제 이름이 올바르지 않거나, 디바이스가 데이터베이스에 없습니다. |
|409   |디바이스 데이터베이스 업데이트 중에 충돌이 발생했습니다. 이 충돌을 해결하려면 필요 시에 오퍼레이션을 단순화하십시오. |


## 디바이스 비관리 요청
{: #manage-unmanage}


더 이상 관리될 필요가 없을 때 디바이스는 디바이스 비관리 요청을 사용합니다. 비관리 디바이스가 되는 경우, {{site.data.keyword.iot_short_notm}}에서는 더 이상 디바이스에 새 디바이스 관리 요청을 전송하지 않습니다. 비관리 디바이스는 계속해서 오류 코드, 로그 메시지 및 위치 메시지를 공개합니다.
**중요:** 이 오퍼레이션에 대한 지원은 관리 디바이스에 필수입니다. 

### 디바이스 비관리 요청의 주제


디바이스는 다음 주제에 대해 디바이스 비관리 요청을 공개합니다. 

```
iotdevice-1/mgmt/unmanage
```

서버는 다음 주제에서 디바이스 비관리 요청에 응답합니다. 

```
iotdm-1/response
```

### 디바이스 비관리 요청의 메시지 형식

요청 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/mgmt/unmanage
{
    "reqId": "string"
}
```

응답 형식:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 디바이스 비관리 요청의 응답 코드

|응답 코드 |메시지 |
|:---|:---|
|200   |오퍼레이션에 성공했습니다. |
|400   |입력 메시지가 예상된 형식과 일치하지 않거나, 값 중 하나가 유효한 범위를 벗어납니다. |
|404   |주제 이름이 올바르지 않거나, 디바이스가 데이터베이스에 없습니다. |
|409   |디바이스 데이터베이스 업데이트 중에 충돌이 발생했습니다. 이 충돌을 해결하려면 필요 시에 오퍼레이션을 단순화하십시오. |


## 위치 업데이트 요청
{: #update-location}

디바이스는 위치 업데이트 요청을 사용하여 디바이스의 위치 데이터를 관리합니다. 디바이스의 위치 메타데이터는 다음과 같은 방법으로 {{site.data.keyword.iot_short_notm}}에서 업데이트될 수 있습니다. 

#### 자동 디바이스 위치 업데이트
- 디바이스가 위치 업데이트에 대해 {{site.data.keyword.iot_short_notm}}에 알립니다. 디바이스는 GPS 수신기에서 해당 위치를 검색하고 디바이스 관리 메시지를 {{site.data.keyword.iot_short_notm}} 인스턴스에 전송하여 해당 위치를 업데이트합니다. 시간소인은 GPS 수신기에서 위치가 검색된 시간을 캡처합니다. 위치 업데이트 메시지를 보내는 중에 지연이 있어도 시간소인은 유효합니다. 디바이스 관리 메시지에서 시간소인이 생략된 경우에는 메시지 수신의 날짜 및 시간을 사용하여 위치 메타데이터를 업데이트합니다. 

#### REST API를 사용하여 수동 디바이스 위치 업데이트
- 디바이스가 등록될 때 {{site.data.keyword.iot_short_notm}} REST API를 사용하여 정적 디바이스의 위치 메타데이터를 수동으로 설정할 수 있습니다. 또한 나중에 위치를 수정할 수도 있습니다. 시간소인 설정은 선택사항이지만, 이를 생략하면 현재 날짜 및 시간이 디바이스의 위치 메타데이터에 설정됩니다. 

### 디바이스가 트리거하는 위치 업데이트

해당 위치를 판별할 수 있는 디바이스는 위치 변경에 대해 {{site.data.keyword.iot_short_notm}} 디바이스 관리 서버에 알리도록 선택할 수 있습니다. 

### 디바이스가 트리거하는 위치 업데이트 요청의 주제:


디바이스가 다음 주제에 대해 위치 업데이트 요청을 공개함: 

```
iotdevice-1/device/update/location
```

서버가 다음 주제에서 위치 업데이트 요청에 응답함: 

```
iotdm-1/response
```

### 사용자 또는 앱이 트리거하는 위치 업데이트


사용자 또는 애플리케이션이 활성 관리 디바이스의 위치를 업데이트하는 경우, 디바이스는 업데이트 메시지를 검색합니다. 




### 사용자 또는 앱이 트리거하는 위치 업데이트 요청의 주제


서버가 다음 주제에 대해 위치 업데이트 요청을 공개함: 

```
iotdm-1/device/update
```

### 위치 업데이트 요청의 메시지 형식


`measuredDateTime` 필드는 위치 측정 날짜입니다. `updatedDateTime` 필드는 디바이스 정보에 대한 업데이트 날짜입니다. 효율성을 위해 {{site.data.keyword.iot_short_notm}}은 종종 위치 정보에 대한 업데이트를 일괄처리하며, 따라서 업데이트가 약간 지연됩니다. 위도 및 경도는 WGS84(World Geodetic System 1984)를 사용하여 DD(Decimal degrees) 방식으로 지정되어야 합니다. 

위치가 업데이트될 때마다 경도, 위도, 고도 및 불확실성에 대해 제공된 값은 하나의 다중 값 업데이트로 간주됩니다. 위도 및 경도는 필수이며 둘 다 각 업데이트에서 제공되어야 합니다. 고도 및 불확실성은 선택사항이며 생략될 수 있습니다. 

선택적 값이 업데이트에서 제공된 후에 후속 업데이트에서 생략되면, 이전 값이 후속 값에 의해 삭제됩니다. 각각의 업데이트는 전체 다중 값 세트로 간주됩니다. 

### 디바이스가 트리거하는 위치 업데이트


요청 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/device/update/location
{
    "d": {
        "longitude": number,
        "latitude": number,

        "elevation": number,
        "measuredDateTime": "string in ISO8601 format",
        "updatedDateTime": "string in ISO8601 format",
        "accuracy": number
    },
    "reqId": "string"
}
```

응답 형식:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 위치 업데이트 요청의 응답 코드

|응답 코드 |메시지 |
|:---|:---|
|200   |오퍼레이션에 성공했습니다. |
|400   |입력 메시지가 예상된 형식과 일치하지 않거나, 값 중 하나가 유효한 범위를 벗어납니다. |
|404   |주제 이름이 올바르지 않거나, 디바이스가 데이터베이스에 없습니다. |
|409   |디바이스 데이터베이스 업데이트 중에 충돌이 발생했습니다. 이 충돌을 해결하려면 필요 시에 오퍼레이션을 단순화하십시오. |


### 사용자 또는 앱이 트리거하는 위치 업데이트


다음 샘플은 페이로드 형식을 개략적으로 보여줍니다. 

```
Incoming message from the server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": {
                    "latitude": number,
                    "longitude": number,
                    "elevation": number,
                    "accuracy": number,
                    "measuredDateTime": "string in ISO8601 format"
                }
            }
        ]
    }
}
```

**참고:** 디바이스가 응답할 필요가 없으므로 `reqID` 매개변수는 사용되지 않습니다. 

## 디바이스 속성 업데이트 요청
{: #update-attributes}

REST API를 사용하여 {{site.data.keyword.iot_short_notm}}은 다음 디바이스 속성 중 하나 이상의 값을 업데이트하기 위해 디바이스에 요청을 전송할 수 있습니다. 


|속성 | 자세한 정보|
|:---|:---|
|location  | [위치 업데이트](index.html#update-location) 참조|
|metadata  | 선택사항|
|deviceInfo | 선택사항|
|mgmt.firmware | [펌웨어 업데이트 프로세스](requests.html#firmware-actions-update) 참조|

### 디바이스 속성 업데이트 요청의 주제


서버는 다음 주제에 대해 디바이스 업데이트 요청을 공개합니다. 

```
iotdm-1/device/update
```


### 디바이스 속성 업데이트 요청의 메시지 형식


다음 샘플은 요청의 페이로드 형식을 개략적으로 보여줍니다. 

```
Incoming message from the server:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": ""
            }
        ]
    }
}
```


## 오류 코드 추가 요청
{: #diag-add-error-code}

디바이스는 오류 코드 추가 요청 유형을 사용하여 해당 오류 상태의 변경에 대해 {{site.data.keyword.iot_short_notm}} 디바이스 관리 서버에 알리도록 선택할 수 있습니다. 

### 오류 코드 추가 요청의 주제


디바이스가 다음 주제에 대해 오류 코드 추가 요청을 공개함: 

```
iotdevice-1/add/diag/errorCodes
```

### 오류 코드 추가 요청의 메시지 형식


`errorCode`와 연관된 값은 현재 디바이스 오류 코드이며 {{site.data.keyword.iot_short_notm}}에 추가되어야 합니다. 

요청 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/add/diag/errorCodes
{
    "d": {
        "errorCode": number
    },
    "reqId": "string"
}
```

응답 형식:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 오류 코드 추가 요청의 응답 코드

|응답 코드 |메시지 |
|:---|:---|
|200   |오퍼레이션에 성공했습니다. |
|400   |입력 메시지가 예상된 형식과 일치하지 않거나, 값 중 하나가 유효한 범위를 벗어납니다. |
|404   |주제 이름이 올바르지 않거나, 디바이스가 데이터베이스에 없습니다. |
|409   |디바이스 데이터베이스 업데이트 중에 충돌이 발생했습니다. 이 충돌을 해결하려면 필요 시에 오퍼레이션을 단순화하십시오. |


## 오류 코드 지우기 요청
{: #diag-clear-error-codes}

디바이스는 {{site.data.keyword.iot_short_notm}}이 오류 코드 지우기 요청 유형을 사용하여 디바이스의 모든 오류 코드를 지우도록 요청할 수 있습니다. 

### 오류 코드 지우기 요청의 주제


디바이스가 다음 주제에 대해 이 요청을 공개함: 

```
iotdevice-1/clear/diag/errorCodes
```

### 오류 코드 지우기 요청의 메시지 형식


요청 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/clear/diag/errorCodes
{
    "reqId": "string"
}
```

응답 형식:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 오류 코드 지우기 요청의 응답 코드

|응답 코드 |메시지 |
|:---|:---|
|200   |오퍼레이션에 성공했습니다. |
|400   |입력 메시지가 예상된 형식과 일치하지 않거나, 값 중 하나가 유효한 범위를 벗어납니다. |
|404   |주제 이름이 올바르지 않거나, 디바이스가 데이터베이스에 없습니다. |
|409   |디바이스 데이터베이스 업데이트 중에 충돌이 발생했습니다. 이 충돌을 해결하려면 필요 시에 오퍼레이션을 단순화하십시오. |


## 로그 추가 요청
{: #diag-add-log}

디바이스는 새 로그 항목을 추가하여 변경사항에 대해 {{site.data.keyword.iot_short_notm}} 디바이스 관리 지원에 알리는지 여부를 선택할 수 있습니다. 로그 항목에는 로그 메시지, 시간소인, 심각도 및 선택적 base64 인코딩 2진 진단 데이터가 포함되어 있습니다. 

### 로그 추가 요청의 주제
디바이스가 다음 주제에 대해 이 요청을 공개함: 

```
iotdevice-1/add/diag/log
```


### 로그 추가 요청의 메시지 형식

다음 표에는 출력 메시지 속성의 형식이 설명되어 있습니다. 

|속성 |설명 |
|:---|:---|
|`message`|{{site.data.keyword.iot_short_notm}}에 추가되어야 하는 진단 메시지를 지정합니다. |
|`timestamp`|ISO8601 형식으로 로그 항목의 날짜 및 시간을 지정합니다.  |
|`data`|선택적 base64 인코딩 진단 데이터를 지정합니다. |
|`severity`|메시지의 심각도를 지정합니다(0: 정보, 1: 경고, 2: 오류). |


요청 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/add/diag/log
{
    "d": {
        "message": string,
        "timestamp": string,
        "data": string,
        "severity": number
    },
    "reqId": "string"
}
```

응답 형식:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### 로그 추가 요청의 응답 코드

|응답 코드 |메시지 |
|:---|:---|
|200   |오퍼레이션에 성공했습니다. |
|400   |입력 메시지가 예상된 형식과 일치하지 않거나, 값 중 하나가 유효한 범위를 벗어납니다. |
|404   |주제 이름이 올바르지 않거나, 디바이스가 데이터베이스에 없습니다. |
|409   |디바이스 데이터베이스 업데이트 중에 충돌이 발생했습니다. 이 충돌을 해결하려면 필요 시에 오퍼레이션을 단순화하십시오. |

## 로그 지우기 요청
{: #diag-clear-logs}

디바이스는 {{site.data.keyword.iot_short_notm}}이 로그 지우기 요청 유형을 사용하여 디바이스의 모든 로그 항목을 지우도록 요청할 수 있습니다. 

### 로그 지우기 요청의 주제


디바이스가 다음 주제에 대해 로그 지우기 요청을 공개함: 

```
iotdevice-1/clear/diag/log
```

### 로그 지우기 요청의 메시지 형식


요청 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/clear/diag/log
{
    "reqId": "string"
}
```

응답 형식:

```
Incoming message from the device:

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### 로그 지우기 요청의 응답 코드

|응답 코드 |메시지 |
|:---|:---|
|200   |오퍼레이션에 성공했습니다. |
|400   |입력 메시지가 예상된 형식과 일치하지 않거나, 값 중 하나가 유효한 범위를 벗어납니다. |
|404   |주제 이름이 올바르지 않거나, 디바이스가 데이터베이스에 없습니다. |
|409   |디바이스 데이터베이스 업데이트 중에 충돌이 발생했습니다. 이 충돌을 해결하려면 필요 시에 오퍼레이션을 단순화하십시오. |

## 속성 변경사항 관찰 요청
{: #observations-observe}

{{site.data.keyword.iot_short_notm}}은 속성 변경사항 관찰 요청 유형을 사용하여 하나 이상의 디바이스 속성에 대한 변경사항을 관찰하도록 디바이스에 속성 변경사항 관찰 요청을 전송할 수 있습니다. 디바이스가 요청을 수신하는 경우, 이는 관찰된 속성의 값이 변경될 때마다 알림 요청을 {{site.data.keyword.iot_short_notm}}에 전송해야 합니다. 

**중요:** [펌웨어 조치 - 업데이트](requests.html#firmware-actions-update) 요청 유형을 지원하려면 디바이스가 관찰, 알림 및 취소 오퍼레이션을 구현해야 합니다. 

### 속성 변경사항 관찰 요청의 주제


서버가 다음 주제에 대해 속성 변경사항 관찰 요청을 공개함: 

```
iotdm-1/observe
```

### 속성 변경사항 관찰 요청의 메시지 형식


`fields` 배열은 디바이스 모델에서 디바이스 속성의 배열입니다. 복합 필드(예: `mgmt.firmware`)가 지정된 경우에는 하나의 알림 메시지만 생성되도록 해당 기본 필드가 동시에 업데이트된다고 예상됩니다. 

응답에서 사용되는 `message` 매개변수는 `rc` 매개변수의 값이 `200`이 아닌 경우에 지정될 수 있습니다. 지정된 매개변수값을 검색할 수 없는 경우, `rc` 매개변수의 값은 `404`(디바이스를 찾을 수 없는 경우) 또는 `500`(기타 이유인 경우)으로 설정되어야 합니다. 매개변수의 값을 찾을 수 없는 경우, `fields` 배열에는 읽을 수 없는 각 매개변수의 이름으로 `field`가 설정된 요소가 포함되어야 합니다. `value` 매개변수는 생략되어야 합니다. 응답 코드 매개변수가 `200`으로 설정되려면 `field` 및 `value`를 둘 다 지정해야 합니다. 여기서 `value`은 `field` 매개변수의 값으로 식별된 속성의 현재 값입니다. 

요청 형식:

```
Incoming message from the server:

Topic: iotdm-1/observe
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

응답 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "d": {
        "fields": [
            {
                "field": "field_name",
                "value": "field_value"
            }
        ]
    },
    "reqId": "string"
}
```


## 속성 관찰 취소 요청
{: #observations-cancel}

{{site.data.keyword.iot_short_notm}}은 속성 관찰 취소 요청 유형을 사용하여 하나 이상의 디바이스 속성의 현재 관찰을 취소하도록 디바이스에 요청을 전송할 수 있습니다. 요청의 `fields` 파트는 디바이스 모델에서 디바이스 속성 이름의 배열입니다(예: `location`, `mgmt.firmware` 또는 `mgmt.firmware.state` 매개변수). 

`rc` 매개변수의 값이 `200`이 아니면 `message` 매개변수를 지정해야 합니다. 

**중요:** [펌웨어 조치 - 업데이트](requests.html#firmware-actions-update) 요청 유형을 지원하려면 디바이스가 관찰, 알림 및 취소 오퍼레이션을 구현해야 합니다. 

### 속성 관찰 취소 요청의 주제


서버가 다음 주제에 대해 속성 관찰 취소 요청을 공개함: 

```
iotdm-1/cancel
```


### 속성 관찰 취소 요청의 메시지 형식


요청 형식:

```
Incoming message from the server:

Topic: iotdm-1/cancel
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

응답 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "reqId": "string"
}
```



## 속성 변경사항 알림 요청
{: #observations-notify}

{{site.data.keyword.iot_short_notm}}은 속성 변경사항 알림 요청 유형을 사용하여 특정 속성 또는 값 세트의 관찰 요청을 작성할 수 있습니다. 속성 값이 변경되는 경우, 디바이스는 최신 값이 포함된 알림을 전송해야 합니다. 

`field_name` 매개변수의 값은 변경된 속성의 이름이며, `field_value`는 속성의 현재 값입니다. 속성은 복합 필드일 수 있습니다. 복합 필드의 다중 값은 단일 오퍼레이션의 결과로서 업데이트되며, 하나의 알림 메시지만 전송됩니다. 

알림 요청이 성공적으로 처리되면 `rc` 매개변수의 값이 `200`으로 설정됩니다. 요청이 올바르지 않으면 `rc` 매개변수의 값이 `400`으로 설정됩니다. 알림 요청에 지정된 매개변수가 관찰되지 않으면 `rc` 매개변수의 값이 `404`로 설정됩니다. 

**중요:** [펌웨어 조치 - 업데이트](requests.html#firmware-actions-update) 요청 유형을 지원하려면 디바이스가 관찰, 알림 및 취소 오퍼레이션을 구현해야 합니다. 


### 속성 변경사항 알림 요청의 주제


디바이스가 다음 주제에 대해 속성 변경사항 알림 요청을 공개함: 

```
iotdevice-1/notify
```


### 속성 변경사항 알림 요청의 메시지 형식


요청 형식:

```
Outgoing message from the device:

Topic: iotdevice-1/notify
{
    "d": {
        "field": "field_name",
        "value": "field_value"
    }
    "reqId": "string"
}
```

응답 형식:

```
Incoming message from the server:

Topic: iotdm-1/response
{
    "rc": number,
    "reqId": "string"
}
```

### 속성 변경사항 알림 요청의 응답 코드

|응답 코드 |메시지 |
|:---|:---|
|200   |오퍼레이션에 성공했습니다. |
|400   |입력 메시지가 예상된 형식과 일치하지 않거나, 값 중 하나가 유효한 범위를 벗어납니다. |
|404   |주제 이름이 올바르지 않거나, 디바이스가 데이터베이스에 없습니다. 또는 보고된 필드에 대한 관찰이 없습니다. |
|409   |디바이스 데이터베이스 업데이트 중에 충돌이 발생했습니다. 이 충돌을 해결하려면 필요 시에 오퍼레이션을 단순화하십시오. |
|500   |내부 오류가 발생했습니다.|
