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


# 애플리케이션 개발자용 Python
{: #python}


Python을 사용하여 {{site.data.keyword.iot_full}}에서 조직과 상호작용하는 애플리케이션을 빌드하고 개발할 수 있습니다. {{site.data.keyword.iot_short_notm}}용 Python 클라이언트는 기본 프로토콜(예: MQTT 및 HTTP)을 추상화하여 {{site.data.keyword.iot_short_notm}} 기능과의 단순 상호작용을 용이하게 하는 API를 제공합니다. 

{:shortdesc}

제공된 정보와 예제를 사용하면 Python을 사용한 애플리케이션 개발을 시작할 수 있습니다. 

## Python 클라이언트 및 리소스 다운로드
{: #python_client_download}

{{site.data.keyword.iot_short_notm}}에 대한 Python 클라이언트 및 기타 사용 가능한 리소스에 액세스하려면 GitHub의 [iot-python ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-messaging/iot-python){: new_window} 저장소로 이동하여 설치 지시사항을 완료하십시오. 

## 생성자
{: #constructor}

옵션 사전은 {{site.data.keyword.iot_short_notm}} 모듈과 상호작용하는 데 사용되는 정의를 작성합니다. 생성자가 클라이언트 인스턴스를 빌드하고 다음 정의가 포함된 옵션 사전을 승인합니다. 

|정의|설명 |
|:-----|:-----|
|`orgId`|조직 ID입니다. |
|`appId`|조직에서 애플리케이션의 고유 ID입니다. |
|`auth-method`|인증 메소드입니다. 지원되는 유일한 메소드는 `apikey`입니다.|
|`auth-key`|auth-method의 값을 `apikey`로 설정할 때 지정해야 하는 선택적 API 키입니다.|
|`auth-token`|auth-method의 값을 `apikey`로 설정할 때 필수인 API 키 토큰입니다.|
|`clean-session`|지속 가능한 구독 모드로 애플리케이션에 연결을 원하는 경우에만 필요한 true 또는 false 값입니다. 기본적으로 `clean-session`은 true로 설정됩니다.|


옵션 사전이 제공되지 않은 경우, 클라이언트는 미등록 디바이스로서 {{site.data.keyword.iot_short_notm}} Quickstart 서비스에 연결됩니다. 

```python

import ibmiotf.application
try:
  options = {
    "org": organization,
    "id": appId,
    "auth-method": authMethod,
    "auth-key": authKey,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### 구성 파일 사용


옵션 사전을 사용하지 않는 경우에는 다음 코드 형식으로 옵션 사전이 포함된 구성 파일을 포함해야 합니다. 

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
애플리케이션 구성 파일은 다음 형식이어야 합니다.

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## API 호출
{: #api_calls}

API 클라이언트의 각 메소드는 다음 중 하나로 응답합니다. 

- 성공하는 경우, 유효한 JSON 또는 부울 응답
- 실패하는 경우, IoTFCReSTException 예외

API 호출이 실패한 이유에 대한 자세한 정보를 가져오거나 조치가 일부만 성공했는지 여부를 확인하기 위해, 애플리케이션은 예외 응답의 특성을 구문 분석할 수 있습니다. IoTFCReSTException 예외 응답에는 다음 특성이 포함되어 있습니다. 

|특성|설명|
|:---|:---|
|`httpcode`|HTTP 상태 코드입니다. |
|`message`|실패한 이유가 포함된 예외 메시지입니다. |
|`response`|일부 응답이 포함된 JSON 요소입니다. 아무 것도 없으면 이 값은 널로 설정됩니다. |

## 디바이스 이벤트 구독
{: #subscribe_device_events}

이벤트는 디바이스가 {{site.data.keyword.iot_short_notm}} 인스턴스에 데이터를 공개하는 메커니즘입니다. 디바이스에서 이벤트의 컨텐츠를 제어하고 전송하는 각 이벤트의 이름을 지정합니다. 

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신할 때 수신된 이벤트의 신임 정보는 전송 중인 디바이스를 식별하며, 따라서 디바이스는 다른 디바이스로 위장할 수 없습니다. 

기본적으로, 애플리케이션은 연결된 모든 디바이스의 모든 이벤트를 구독합니다. deviceType, deviceId, event 및 msgFormat 매개변수를 사용하면 구독의 범위를 제어할 수 있습니다. 하나의 클라이언트는 여러 구독을 지원할 수 있습니다. 다음 코드 샘플은 deviceType, deviceId, event 및 msgFormat 매개변수를 사용하여 구독의 범위를 정의할 수 있는 방법을 표시합니다. 


### 모든 디바이스의 모든 이벤트 구독


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### 특정 유형인 모든 디바이스의 모든 이벤트 구독


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### 모든 디바이스의 특정 이벤트 구독


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### 둘 이상의 서로 다른 디바이스의 특정 이벤트 구독

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### JSON 형식으로 공개된 모든 이벤트 구독

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## 디바이스에서 이벤트 처리
{: #handling_events_devices}

구독으로 수신된 이벤트를 처리하려면 이벤트 콜백 메소드를 등록해야 합니다. 메시지는 이벤트 클래스의 인스턴스로 리턴됩니다. 

|특성|데이터 유형|설명|
|:---|:---|
|`event.device`|문자열|조직의 모든 유형의 디바이스 간에 디바이스를 고유하게 식별합니다. |
|`event.deviceType`|문자열|디바이스 유형을 식별합니다. 일반적으로, deviceType은 특정 태스크를 수행하는 디바이스의 그룹화입니다(예: "weatherballoon"). |
|`event.deviceId`|문자열|디바이스의 ID를 표시합니다. 일반적으로, 제공된 디바이스 유형의 경우 deviceId는 해당 디바이스의 고유 ID입니다(예: 일련 번호 또는 MAC 주소). |
|`event.event`|문자열|일반적으로, 특정 이벤트를 그룹화하는 데 사용됩니다(예: "상태", "경고" 및 "데이터").
|`event.format`|문자열|형식은 임의의 문자열일 수 있습니다(예: JSON).
|`event.data`|사전|메시지 페이로드의 데이터입니다. 최대 길이는 131072바이트입니다.
|`event.timestamp`|날짜 및 시간 |이벤트의 날짜 및 시간입니다. |

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  def myEventCallback(event):
      str = "%s event '%s' received from device [%s]: %s"
      print(str % (event.format, event.event, event.device, json.dumps(event.data)))

...
client.connect()
client.deviceEventCallback = myEventCallback
client.subscribeToDeviceEvents()
```


## 디바이스 상태 구독
{: #subscribe_device_status}


기본적으로, 디바이스 상태를 구독하면 연결된 모든 디바이스에 대해 상태 업데이트가 수신됩니다. 유형 및 ID 매개변수를 사용하면 구독의 범위를 제어할 수 있습니다. 하나의 클라이언트는 여러 구독을 지원할 수 있습니다. 

### 모든 디바이스의 상태 업데이트 구독


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### 특정 유형인 모든 디바이스의 상태 업데이트 구독


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### 두 개의 서로 다른 디바이스의 상태 업데이트 구독


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## 디바이스에서 상태 업데이트 처리
{: #handling_device_updates}

상태 이벤트

구독으로 수신된 상태 업데이트를 처리하려면 이벤트 콜백 메소드를 등록해야 합니다. 메시지는 상태 클래스의 인스턴스로 리턴됩니다. 

두 가지 유형의 상태 이벤트(`Connect` 이벤트 및 `Disconnect` 이벤트)가 있습니다. 모든 상태 이벤트에는 다음 특성이 포함되어 있습니다. 

|특성|데이터 유형|
|:---|:---|
|`status.clientAddr`|문자열|
|`status.protocol`|문자열|
|`status.clientId`|문자열|
|`status.user`|문자열|
|`status.time`|날짜 및 시간 |
|`status.action`|문자열|
|`status.connectTime`|날짜 및 시간 |
|`status.port`|정수|


`status.action` 특성은 상태 이벤트가 `Connect` 또는 `Disconnect` 유형인지 여부를 판별합니다. 

`Disconnect` 상태 이벤트에는 다음의 추가 특성이 포함되어 있습니다. 

|특성|데이터 유형|
|:---|:---|
|`status.writeMsg`|정수|
|`status.readMsg`|정수|
|`status.reason`|문자열|
|`status.readBytes`|정수|
|`status.writeBytes`|정수|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

def myStatusCallback(status):

  if status.action == "Disconnect":
    str = "%s - device %s - %s (%s)"
    print(str % (status.time.isoformat(), status.device, status.action, status.reason))
    else:
      print("%s - %s - %s" % (status.time.isoformat(), status.device, status.action))
  ...
client.connect()
client.deviceStatusCallback = myStatusCallback
client.subscribeToDeviceStstus()
```


## 디바이스에서 이벤트 공개
{: #publishing_device_events}

애플리케이션은 디바이스에서 가져온 것처럼 이벤트를 공개할 수 있습니다. 

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## 디바이스에 명령 공개
{: #publishing_commands_devices}


애플리케이션은 연결된 디바이스에 대한 명령을 공개할 수 있습니다.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", commandData)
```


## 조직 세부사항
{: #org_details}

애플리케이션은 `getOrganizationDetails()` 메소드를 사용하여 조직의 구성에 대한 세부사항을 검색할 수 있습니다. 

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

요청과 응답 모델 및 HTTP 상태 코드에 대한 정보는 [{{site.data.keyword.iot_short_notm}} API ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}의 조직 구성 섹션을 참조하십시오. 


## 벌크 디바이스 오퍼레이션
{: #bulk_device_ops}

애플리케이션은 벌크 오퍼레이션을 사용하여 여러 디바이스를 동시에 가져오고 추가하거나 제거할 수 있습니다. 

조회 매개변수 목록, 요청 및 응답 모델, HTTP 상태 코드에 대한 정보는 [{{site.data.keyword.iot_short_notm}} API ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/){: new_window}의 '벌크 오퍼레이션' 섹션을 참조하십시오. 


### 디바이스 정보 검색

벌크 디바이스 정보는 `getAllDevices()` 메소드를 사용하여 검색될 수 있습니다. 이 메소드는 조직의 등록된 모든 디바이스에 대한 정보를 검색합니다. 각 요청에는 최대 512KB가 포함될 수 있습니다. 

응답에는 애플리케이션에 필요한 매개변수가 포함되어 있습니다. 응답의 사전 결과를 사용하면 리턴된 디바이스의 배열을 가져올 수 있습니다. 응답의 기타 매개변수는 추가 호출을 작성하는 데 필요합니다. 예를 들어, `_bookmark` 요소를 사용하여 결과 페이지를 넘겨볼 수 있습니다. 책갈피를 지정하지 않고 첫 번째 요청을 제출한 후에 응답에서 리턴된 책갈피를 가져와서 이를 다음 페이지에 대한 요청에서 제공하십시오. 결과 세트의 끝까지 반복하십시오. 책갈피가 없으면 끝입니다. 각 요청은 기타 매개변수에 대해 동일한 값을 사용해야 하며, 그렇지 않으면 결과가 정의되지 않습니다. 


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### 여러 디바이스 추가


`addMultipleDevices()` 메소드를 사용하여 {{site.data.keyword.iot_short_notm}} 조직에 하나 이상의 디바이스를 추가할 수 있습니다. 요청은 512KB를 초과할 수 없습니다. 응답에는 각 디바이스에 대해 생성된 인증 토큰이 포함되어 있습니다. 인증 토큰을 유실하면 이를 검색할 수 없으므로 반드시 인증 토큰의 사본을 작성하십시오. 


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
  deviceList = client.api.addMultipleDevices(listOfDevicesToAdd)
except IoTFCReSTException as e:
  print("ERROR [" + e.httpcode + "] " + e.message)
```

### 여러 디바이스 삭제


`deleteMultipleDevices()` 메소드를 사용하여 {{site.data.keyword.iot_short_notm}} 조직에서 여러 디바이스를 삭제할 수 있습니다. 요청은 512KB를 초과할 수 없습니다. 

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToDelete = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
      deviceList = client.api.deleteMultipleDevices(listOfDevicesToDelete)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## 디바이스 유형 오퍼레이션
{: #device_type_ops}

조직에서 작성하는 디바이스 유형은 디바이스 추가를 위한 템플리트를 작성하는 데 사용될 수 있습니다. {{site.data.keyword.iot_short_notm}} API 기능을 사용하면 애플리케이션이 조직의 디바이스 유형을 나열, 작성, 삭제하고 이를 보거나 업데이트할 수 있습니다. 

조회 매개변수, 요청 및 응답 모델, HTTP 상태 코드에 대한 정보는 [{{site.data.keyword.iot_short_notm}} API ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} 문서의 '디바이스 유형' 섹션을 참조하십시오. 


### 모든 디바이스 유형 검색

`getAllDeviceTypes()` 메소드를 사용하여 {{site.data.keyword.iot_short_notm}} 조직에 있는 모든 디바이스 유형을 검색할 수 있습니다.
응답의 사전 결과를 사용하면 리턴된 디바이스의 배열을 가져올 수 있습니다. 응답의 기타 매개변수는 추가 호출을 작성하는 데 필요합니다. 예를 들어, `_bookmark` 요소를 사용하여 결과 페이지를 넘겨볼 수 있습니다. 책갈피를 지정하지 않고 첫 번째 요청을 제출한 후에 응답에서 리턴된 책갈피를 가져와서 이를 다음 페이지에 대한 요청에서 제공하십시오. 결과 세트의 끝까지 이 프로세스를 반복하십시오. 책갈피가 없으면 끝입니다. 각 요청은 기타 매개변수에 대해 동일한 값을 사용해야 하며, 그렇지 않으면 결과가 정의되지 않습니다. 

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

 listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
   options = {'_limit' : 2}
   deviceTypeList = client.api.getAllDeviceTypes(options)
except IoTFCReSTException as e:
   print("ERROR [" + e.httpcode + "] " + e.message)

```

### 디바이스 유형 추가

`addDeviceType()` 메소드를 사용하여 {{site.data.keyword.iot_short_notm}} 인스턴스에 대해 디바이스 유형을 등록할 수 있습니다. 각 요청에는 우선 이 유형의 모든 디바이스에 적용할 디바이스 정보와 디바이스 메타데이터 요소를 정의해야 합니다. 디바이스 정보 요소는 여러 변수로 구성되어 있으며, 여기에는 일련 번호, 제조업체, 모델, 클래스, 설명, 펌웨어, 하드웨어 버전 및 설명적 위치 등이 포함됩니다. 메타데이터 요소는 사용자 정의 변수 및 정의로 구성되며, 이는 사용자에 의해 정의될 수 있습니다. 


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2"
  }

try:
      deviceType = client.api.addDeviceType(deviceType = "myDeviceType", description = "My first device type", deviceInfo = info, metadata = meta)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### 디바이스 유형 삭제


`deleteDeviceType()` 메소드를 사용하여 {{site.data.keyword.iot_short_notm}} 조직에서 디바이스 유형을 삭제할 수 있습니다. 

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### 특정 디바이스 유형의 정보 검색


`getDeviceType()` 메소드를 사용하여 특정 디바이스 유형에 대한 정보를 검색할 수 있습니다. 검색할 디바이스 유형의 `typeId`는 매개변수로서 지정되어야 합니다. 

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### 디바이스 유형 업데이트


`updateDeviceType()` 메소드를 사용하여 디바이스 유형의 특성을 수정할 수 있습니다. `updateDeviceType()` 메소드를 사용할 때는 우선 업데이트되는 디바이스 유형의 `typeId`를 지정한 후에 다음 요소를 지정하십시오. 

- `description`
- `deviceInfo`
- `metadata`

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2",
      "customField3": "customValue3"
  }

try:
      updatedDeviceTypeInfo = client.api.updateDeviceType("myDeviceType", "New description", deviceInfo, metadata)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## 디바이스 오퍼레이션
{: #device_ops}

API에서 사용 가능한 디바이스 오퍼레이션에는 나열, 추가, 제거, 보기, 업데이트, 위치 보기 및 {{site.data.keyword.iot_short_notm}} 조직의 디바이스에 대한 디바이스 관리 정보 보기가 포함됩니다. 

조회 매개변수, 요청 및 응답 모델, HTTP 상태 코드에 대한 정보는 [{{site.data.keyword.iot_short_notm}} API ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}의 '디바이스 섹션'을 참조하십시오. 


### 특성 디바이스 유형의 디바이스 검색

`retrieveDevices()` 메소드를 사용하여 {{site.data.keyword.iot_short_notm}} 인스턴스에서 조직의 특정 디바이스 유형인 모든 디바이스를 검색할 수 있으며, 이는 다음 예제에 표시되어 있습니다. 


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

응답의 사전 결과를 사용하면 리턴된 디바이스의 배열을 가져올 수 있습니다. 응답의 기타 매개변수는 추가 호출을 작성하는 데 필요합니다. 예를 들어, *_bookmark* 요소를 사용하여 결과 페이지를 넘겨볼 수 있습니다. 책갈피를 지정하지 않고 첫 번째 요청을 제출한 후에 응답에서 리턴된 책갈피를 가져와서 이를 다음 페이지에 대한 요청에서 제공하십시오. 결과 세트의 끝까지 반복하십시오. 책갈피가 없으면 끝입니다. 각 요청은 기타 매개변수에 대해 동일한 값을 사용해야 하며, 그렇지 않으면 결과가 정의되지 않습니다. 

*_bookmark* 또는 기타 조건을 전달하려면 오버로드된 메소드를 사용해야 합니다. 오버로드된 메소드는 다음 예제에서 표시된 대로 사전 양식의 매개변수를 취합니다. 

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

이전 코드 샘플은 디바이스 ID를 기반으로 응답을 정렬한 후에 책갈피를 사용하여 결과 페이지를 넘겨봅니다. 

### 디바이스 추가


{{site.data.keyword.iot_short_notm}} 조직에 디바이스를 추가하려면 `registerDevice()` 메소드를 사용하십시오. `registerDevice()` 메소드는 {{site.data.keyword.iot_short_notm}} 조직에 하나의 디바이스를 추가합니다. 디바이스를 추가하는 경우, 다음 매개변수를 지정할 수 있습니다. 

|매개변수|요구사항|설명
|:---|:---|
|`deviceTypeId`|선택사항|디바이스에 대해 디바이스 유형을 지정합니다. 디바이스 유형에서 정의한 변수와 `deviceInfo` 변수에서 정의한 변수 간에 충돌이 있으면 디바이스 특정 변수가 우선합니다. |
|`deviceId`|필수||
|`authToken`|선택사항|제공되지 않은 경우, 인증 토큰이 생성되며 응답에 포함됩니다. |
|`deviceInfo`|선택사항|일련 번호, 제조업체, 모델, 디바이스 클래스, 설명, 설명적 위치, 펌웨어 및 하드웨어 버전을 포함하는 여러 변수가 포함됩니다. |
|`metadata`|선택사항|[디바이스 유형 추가를 위한 샘플 코드](#sample_device_type)에서 개략적으로 설명한 사용자 정의 필드 값 문자열 쌍입니다. |
|`location`|선택사항|경도, 위도, 고도, 정확도 및 measuredDateTime 변수가 포함됩니다. |

이러한 매개변수 및 응답 형식과 코드에 대한 자세한 정보는 [API 문서 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices){: new_window}를 참조하십시오. 

`registerDevice()` 메소드를 사용할 때는 디바이스에 필요한 필수 deviceID 매개변수 및 선택적 매개변수를 정의한 후에 선택한 매개변수를 사용하여 메소드를 호출하십시오. 

### 디바이스 유형 추가를 위한 샘플 코드
{: #sample_device_type}

Python(.py) 스크립트 파일에서 생성자 코드 뒤에 다음 코드를 삽입하십시오. 샘플에서는 deviceId, authToken, metadata, deviceInfo 및 location 매개변수를 정의하여 디바이스 유형을 추가하는 메소드를 예시합니다. 

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### 디바이스 삭제

`deleteDevice()` 메소드를 사용하여 {{site.data.keyword.iot_short_notm}} 조직에서 조직의 디바이스를 제거할 수 있습니다. `deleteDevice()` 메소드를 사용하여 디바이스를 삭제할 때는 deviceTypeId 및 deviceId 매개변수를 지정해야 합니다. 

다음 코드 샘플은 이 메소드에 필요한 형식을 개략적으로 보여줍니다. 

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### 디바이스 가져오기

`getDevice()` 메소드를 사용하여 {{site.data.keyword.iot_short_notm}}에서 조직의 디바이스를 검색할 수 있습니다. `getDevice()` 메소드를 사용하여 디바이스 세부사항을 검색할 때는 deviceTypeId 및 deviceId 매개변수를 지정해야 합니다. 

다음 코드 샘플은 이 메소드에 필요한 형식을 개략적으로 보여줍니다. 

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### 모든 디바이스 검색

`getAllDevices()` 메소드를 사용하여 {{site.data.keyword.iot_short_notm}}에서 조직의 모든 디바이스를 검색할 수 있습니다. 

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### 디바이스 업데이트

하나 이상의 디바이스 특성을 수정하려면 `updateDevice()` 메소드를 사용하십시오. 

deviceInfo 또는 metadata 매개변수에서 특성을 업데이트할 수 있습니다. 디바이스 특성을 업데이트하려면 `updateDevice()` 메소드를 호출하기 전에 deviceInfo 매개변수를 정의하십시오. status 매개변수에는 `alert`: True가 포함되어야 합니다. 경보 특성은 디바이스가 {{site.data.keyword.iot_short_notm}} 사용자 인터페이스에서 오류 코드를 표시하는지 여부를 제어하며, 다음 코드 예제에서 개략적으로 설명한 대로 기본적으로 `enabled`: True로 설정되어야 합니다. 

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### deviceInfo 특성 업데이트를 위한 샘플 코드

다음 코드 샘플은 특정 디바이스를 식별한 후에 deviceInfo 매개변수의 여러 특성을 업데이트합니다. 

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### 위치 정보 검색


`getDeviceLocation()` 메소드를 사용하여 디바이스의 위치 정보를 검색할 수 있습니다. 위치 데이터의 검색에 필요한 매개변수는 deviceTypeId 및 deviceId입니다. 

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

이 메소드에 대한 응답에는 경도, 위도, 고도, 정확도, measuredTimeStamp 및 updatedTimeStamp 특성이 포함되어 있습니다. 

### 위치 정보 업데이트


`updateDeviceLocation()` 메소드를 사용하여 디바이스의 위치 정보를 수정할 수 있습니다. 디바이스 특성 업데이트에서와 마찬가지로, deviceLocation 매개변수는 적용하고자 하는 변경사항으로 정의되어야 합니다. 다음 코드 샘플에서는 특정 디바이스의 위치 데이터 변경을 예시합니다. 

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

날짜가 제공되지 않으면 현재 날짜 및 시간이 사용됩니다. 


### 관리 정보 가져오기


`getDeviceManagementInformation()` 메소드를 사용하여 디바이스의 디바이스 관리 정보를 가져올 수 있습니다. 응답에는 마지막 활성 Datetime, 디바이스의 휴면 상태(True/False), 디바이스 및 펌웨어 조치에 대한 지원, 그리고 펌웨어 데이터가 포함됩니다. 응답 컨텐츠의 전체 목록은 관련 API 문서를 참조하십시오. 

다음 코드 샘플에서는 "00aabbccde03"으로 설정된 deviceId 및 "iotsample-arduino"로 설정된 deviceTypeId의 디바이스에 대한 디바이스 관리 정보를 리턴합니다. 

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## 디바이스 진단 오퍼레이션
{: #device_diag_ops}

다음의 문제점 해결 및 로그 관리 태스크를 구현하기 위한 디바이스 진단 오퍼레이션 사용: 
- 로그 지우기
- 디바이스의 모든 또는 특정 로그 검색
- 로그 정보 추가
- 로그 삭제
- 오류 코드 지우기
- 디바이스 오류 코드 검색
- 오류 코드 추가

조회 및 응답 모델, 응답 코드 및 조회 매개변수에 대한 자세한 정보는 [API 문서 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} {{site.data.keyword.iot_short_notm}} API 문서를 참조하십시오. 

### 진단 로그 가져오기


`getAllDiagnosticLogs()` 메소드를 사용하여 특정 디바이스의 모든 진단 로그를 검색할 수 있습니다. `getAllDiagnosticLogs()` 메소드에는 deviceTypeId 및 deviceId 매개변수가 필요합니다. 

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

이 메소드의 응답 모델에는 로그 ID, 메시지, 심각도, 데이터 및 시간소인 특성이 포함되어 있습니다. 

### 디바이스의 진단 로그 지우기


`clearAllDiagnosticLogs()` 메소드를 사용하여 특정 디바이스의 모든 진단 로그를 삭제할 수 있습니다. 필수 매개변수는 deviceTypeId 및 deviceId입니다. 일단 삭제되면 복구할 수 없으므로 로그 파일을 삭제할 때는 주의하십시오. 

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### 진단 로그 추가


`addDiagnosticLog()` 메소드를 사용하여 디바이스의 진단 로그에 항목을 추가할 수 있습니다. 로그는 새 항목이 추가되면 제거될 수 있습니다. 날짜가 제공되지 않으면 현재 날짜 및 시간이 항목에 추가됩니다. 이 메소드를 사용하려면 다음 변수와 함께 'logs' 매개변수를 정의해야 합니다. 


|변수|요구사항|설명|
|:---|:---|:---|
|`message`|필수|추가할 진단 메시지가 포함되어 있습니다. |
|`severity`|선택사항|진단 로그의 심각도에 대응되며 0, 1 또는 2(이는 정보, 경고 및 오류 카테고리에 해당됨) 중 하나로 설정될 수 있습니다. |
|`data`|선택사항|진단 데이터가 포함되어 있습니다. |
|`timestamp`|선택사항|ISO8601 형식으로 로그 항목의 날짜 및 시간이 포함되지만, 이를 지정하지 않으면 현재 날짜 및 시간이 사용됩니다. |


메소드에서 필요한 기타 매개변수는 디바이스의 deviceTypeId 및 deviceId 값입니다. 

다음 코드 샘플에는 `addDiagnosticLog()` 메소드의 예제가 포함되어 있습니다. 

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### 특정 진단 로그 검색


`getDiagnosticLog()` 메소드를 사용하여 로그 ID를 기반으로 지정된 디바이스의 특정 진단 로그를 검색할 수 있습니다. 이 메소드의 필수 매개변수는 deviceTypeId, deviceId 및 logId입니다. 

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### 진단 로그 삭제


`deleteDiagnosticLog()` 메소드를 사용하여 특정 진단 로그를 삭제할 수 있습니다. 진단 로그를 지정하려면 deviceTypeId, deviceId 및 logID 매개변수를 제공해야 합니다. 

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### 디바이스 오류 코드 검색


`getAllDiagnosticErrorCodes()` 메소드를 사용하여 특정 디바이스와 연관된 모든 진단 오류 코드를 검색할 수 있습니다. 

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### 진단 오류 코드 지우기


`clearAllErrorCodes()` 메소드를 사용하여 디바이스와 연관된 오류 코드의 목록을 지울 수 있습니다. 목록이 단일 오류 코드 0으로 대체됩니다. 

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### 단일 진단 오류 코드 추가


`addErrorCode()` 메소드를 사용하여 디바이스와 연관된 오류 코드의 목록에 오류 코드를 추가할 수 있습니다. 목록은 새 항목이 추가되면 제거될 수 있습니다. 메소드에서 필요한 매개변수는 deviceTypeId, deviceId 및 errorCode입니다. errorCode 매개변수에는 다음 변수가 포함되어 있습니다. 

- errorCode: 이 변수는 필수이며 정수로 설정되어야 합니다. 이 변수는 작성된 오류 코드의 수를 설정합니다. 
- timestamp: 이 변수는 선택사항이며, ISO8601 형식으로 로그 항목의 날짜 및 시간을 포함합니다. 이 변수를 포함하지 않은 경우, 이는 현재 날짜 및 시간으로 자동 추가됩니다. 

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## 연결 문제점 판별
{: #connection_problem_determination}

`getDeviceConnectionLogs()` 메소드를 사용하여 디바이스의 연결 로그 이벤트를 나열할 수 있습니다. 연결 로그 이벤트를 사용하면 디바이스 및 {{site.data.keyword.iot_short_notm}} 서비스 간의 연결 문제점을 진단하는 데 도움이 될 수 있습니다. 항목은 연결 성공, 연결 시도 실패, 의도적 연결 끊기 및 서버가 실행한 연결 끊기 이벤트를 기록합니다. 

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

응답에는 로그 항목의 목록이 포함되며, 여기에는 로그 메시지 및 시간소인이 포함되어 있습니다. 
