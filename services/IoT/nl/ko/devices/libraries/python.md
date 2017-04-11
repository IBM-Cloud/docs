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


# 디바이스 개발자용 Python
{: #python}

{{site.data.keyword.iot_full}}에서 조직과 상호작용하는 디바이스 코드를 빌드하고 개발하는 데 Python을 사용할 수 있습니다. {{site.data.keyword.iot_short_notm}}용 Python 클라이언트는 기본 프로토콜(예: MQTT 및 HTTP)을 추상화하여 {{site.data.keyword.iot_short_notm}} 기능과의 단순 상호작용을 용이하게 하는 API를 제공합니다.
{:shortdesc}

Python를 사용하여 디바이스 디버깅을 시작하도록 제공된 예와 정보를 사용하십시오.

## Python 클라이언트 및 리소스 다운로드
{: #python_client_download}

{{site.data.keyword.iot_short_notm}}에 대한 Python 클라이언트 및 기타 사용 가능한 리소스에 액세스하려면 GitHub의 [iot-python ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-python){: new_window} 저장소로 이동하여 설치 지시사항을 완료하십시오. 

## 생성자
{: #constructor}

옵션 사전이 {{site.data.keyword.iot_short_notm}} 모듈과 상호작용하는 데 사용하는 정의를 작성합니다. 생성자가 클라이언트 인스턴스를 빌드하고 다음 정의가 포함된 옵션 사전을 승인합니다.

|정의|설명  |
|:---|:---|
|`orgId`|조직 ID입니다. |
|`type`|디바이스의 유형입니다. 디바이스 유형은 특정 태스크를 수행하는 디바이스를 그룹화한 것입니다(예: "weatherballoon").|
|`id`|디바이스를 식별하는 고유 ID입니다. 일반적으로, 특정 디바이스 유형이 지정된 경우 디바이스 ID는 해당 디바이스의 고유 ID입니다(예: 일련 번호 또는 MAC 주소).|
|`auth-method`|인증 메소드입니다. 지원되는 유일한 메소드는 `apikey`입니다.|
|`auth-token`|auth-method의 값을 `apikey`로 설정할 때 필수인 API 키 토큰입니다.|
|`clean-session`|지속 가능한 구독 모드로 애플리케이션에 연결을 원하는 경우에만 필요한 true 또는 false 값입니다. 기본적으로 `clean-session`은 true로 설정됩니다.|

옵션 사전이 제공되지 않은 경우, 클라이언트는 미등록 디바이스로서 {{site.data.keyword.iot_short_notm}} Quickstart 서비스에 연결됩니다. 

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### 구성 파일 사용

다음 코드 샘플에 간략하게 설명된 대로, 옵션 사전을 직접 정의하지 않고 구성 파일에서 옵션 사전을 개별적으로 정의할 수도 있습니다.

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

옵션 사전을 포함하는 구성 파일의 형식은 다음과 같아야 합니다.

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token
clean-session=true/false
```

## 이벤트 공개
{: #publishing_events}

이벤트는 디바이스가 {{site.data.keyword.iot_short_notm}}에 데이터를 공개하는 데 사용하는 메커니즘입니다. 디바이스에서 이벤트의 컨텐츠를 제어하고 전송하는 각 이벤트의 이름을 지정합니다.

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신할 때 수신된 이벤트의 신임 정보는 전송 중인 디바이스를 식별하며, 이는 디바이스가 다른 디바이스로 위장할 수 없음을 의미합니다. 

이벤트는 MQTT 프로토콜을 통해 정의한 세 개의 서비스 품질(QoS) 레벨로 공개할 수 있습니다. 기본적으로 이벤트는 QoS 레벨 `0`으로 공개됩니다.

### 기본 서비스 품질(QoS)을 사용하여 이벤트 공개

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### 이벤트의 QoS 레벨 증가

공개되는 이벤트의 [서비스 품질(QoS) 레벨](../../reference/mqtt/index.html#qos-levels)을 늘릴 수 있습니다. 포함된 추가 확인 수신 정보로 인해 QoS 레벨이 `0`보다 큰 이벤트는 공개하는 데 더 오래 걸릴 수 있습니다.

**참고:** Quickstart 플로우 모드에서는 QoS 레벨 `0`만 지원합니다.

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## 명령 처리
{: #handling_commands}

디바이스 클라이언트가 연결되면 이 디바이스에 지정된 명령을 자동으로 구독합니다. 특정 명령을 처리하려면 명령 콜백 메소드를 등록해야 합니다.
메시지는 명령 클래스의 인스턴스로 리턴되며, 다음과 같은 특성이 있습니다.

|특성|데이터 유형|설명 |
|:---|:---|
|`command`|문자열|명령을 식별합니다.|
|`format`|문자열|형식은 임의의 문자열일 수 있습니다(예: JSON). |
|`data`|사전|페이로드의 데이터입니다. 최대 길이는 131072바이트입니다.|
|`timestamp`|날짜 및 시간|이벤트의 날짜 및 시간입니다.|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## 사용자 정의 메시지 형식 지원
{: #custom_message_format}

기본적으로 메시지 형식은 `json`으로 설정되며, 라이브러리에서 JSON 형식의 Python 사전 오브젝트를 인코딩하고 디코딩하도록 지원합니다. 메시지 형식이 `json-iotf`로 설정되면 {{site.data.keyword.iot_short_notm}} JSON 페이로드 스펙에 따라 메시지가 인코딩됩니다. 고유 사용자 정의 메시지 형식에 대한 지원을 추가하려면 GitHub의 [사용자 정의 메시지 형식 샘플 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat){: new_window}을 참조하십시오. 

다음 예에 간략하게 설명된 대로 사용자 정의 인코더 모듈을 작성하면 디바이스 클라이언트에 등록해야 합니다.

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
이벤트를 알 수 없는 형식으로 전송하거나 디바이스에서 형식을 인식하지 못하는 경우 디바이스 라이브러리에서 `MissingMessageDecoderException` 조건을 리턴합니다.
