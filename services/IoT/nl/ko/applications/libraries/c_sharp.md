---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-07-28"

---

  {:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 애플리케이션 개발자용 C#
{: #c_sharp}


C#을 사용하여 {{site.data.keyword.iot_full}}에서 조직과 상호작용하는 애플리케이션을 빌드하고 사용자 정의할 수 있습니다. 제공된 정보와 예제를 사용하면 C#을 사용한 애플리케이션 개발을 시작할 수 있습니다.
{:shortdesc}

## C# 클라이언트 및 자원 다운로드
{: #csharp_client_download}

{{site.data.keyword.iot_short_notm}}의 C# 클라이언트 라이브러리와 샘플에 액세스하려면 GitHub의 [iot-csharp](https://github.com/ibm-watson-iot/iot-csharp) 저장소로 이동하여 설치 지시사항을 완료하십시오. 


## 생성자
{: #constructor}

생성자는 클라이언트 인스턴스를 빌드하며 다음 정의가 포함된 인수를 허용합니다. 

|정의 |설명 |
|:---|:---|
|`orgId`   |조직 ID입니다. |
|`appId`   |조직에서 애플리케이션의 고유 ID입니다. |
|`auth-key`   |애플리케이션을 Watson IoT Platform에 안전하게 연결하기 위한 API 키입니다. |
|`auth-token`   |애플리케이션을 Watson IoT Platform에 안전하게 연결하기 위한 API 키 토큰입니다. |

`appId`가 유일하게 제공되는 인수인 경우, 클라이언트는 {{site.data.keyword.iot_short_notm}} Quickstart 서비스에 미등록 디바이스로 연결합니다. 인수 목록은 클라이언트가 {{site.data.keyword.iot_short_notm}} 모듈에 연결하는 방법을 정의합니다. 

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```


## 디바이스 이벤트 구독
{: #subscribe_device_events}

디바이스는 이벤트를 사용하여 데이터를 {{site.data.keyword.iot_short_notm}} 인스턴스에 공개합니다. 디바이스는 이벤트의 컨텐츠를 제어하며 전송 중인 각 이벤트에 대해 이름을 지정합니다. 

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신할 때 수신된 이벤트의 신임 정보는 전송 중인 디바이스를 식별하며, 이는 디바이스가 다른 디바이스로 위장할 수 없음을 의미합니다. 

기본적으로, 애플리케이션은 연결된 모든 디바이스의 모든 이벤트를 구독합니다. 디바이스 유형, 디바이스 ID, 이벤트 및 메시지 형식 매개변수를 사용하면 구독의 범위를 제어할 수 있습니다. 다음 코드 샘플은 이러한 매개변수를 사용하여 구독의 범위를 정의할 수 있는 방법을 표시합니다. 

### 모든 디바이스의 모든 이벤트 구독

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### 특정 유형인 모든 디바이스의 모든 이벤트 구독

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### 모든 디바이스의 특정 이벤트 구독

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  둘 이상의 서로 다른 디바이스의 특정 이벤트 구독:

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### JSON 형식으로 공개된 모든 이벤트 구독

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**참고**: 하나의 클라이언트 인스턴스는 여러 구독을 지원할 수 있습니다. 

### 디바이스에서 이벤트 처리

구독으로 수신된 이벤트를 처리하려면 다음 예제에서 표시된 대로 이벤트 콜백 메소드를 등록하십시오. 

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Do something
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
다음 표에는 이벤트 콜백 메소드의 매개변수가 설명되어 있습니다.

|매개변수|데이터 유형|설명|
|:---|:---|
|`eventName`|문자열|이벤트를 식별합니다.  |
|`eventFormat`|문자열| 형식은 임의의 문자열일 수 있습니다(예: JSON). |
|`eventData`|사전| 메시지 페이로드의 데이터입니다. 최대 길이는 131072바이트입니다. |


## 디바이스 상태 구독
{: #subscribe_device_status}

기본적으로, 구독은 연결된 모든 디바이스의 상태 업데이트를 수신하도록 설정되어 있습니다. 디바이스 유형 및 디바이스 ID 매개변수를 사용하면 구독의 범위를 제어할 수 있습니다. 다음 코드 샘플은 이러한 매개변수를 사용하여 구독의 범위를 정의할 수 있는 방법을 표시합니다. 

### 모든 디바이스의 상태 업데이트 구독

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### 두 개의 서로 다른 디바이스의 상태 업데이트 구독

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**참고**: 하나의 클라이언트 인스턴스는 여러 구독을 지원할 수 있습니다. 

### 디바이스에서 상태 업데이트 처리

구독으로 수신된 상태 업데이트를 처리하려면 다음 예제에서 표시된 대로 이벤트 콜백 메소드를 등록하십시오. 

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## 디바이스에서 이벤트 공개
{: #publish_events_devices}

애플리케이션은 디바이스에서 가져온 것처럼 이벤트를 공개할 수 있습니다. 

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

다음 표에는 `publishEvent()` 메소드에 지정된 매개변수가 설명되어 있습니다. 

|매개변수|데이터 유형|설명|
|:---|:---|
|`deviceType`|문자열| 디바이스 유형입니다. 일반적으로, deviceType은 특정 태스크를 수행하는 디바이스의 그룹화입니다(예: "weatherballoon"). |
|`deviceId`|문자열| 디바이스의 ID입니다. 일반적으로, 제공된 디바이스 유형의 경우 deviceId는 해당 디바이스의 고유 ID입니다(예: 일련 번호 또는 MAC 주소). |
|`evt`|문자열| 이벤트의 이름입니다. |
|`format`|문자열| 형식은 임의의 문자열일 수 있습니다(예: JSON). |
|`data`|사전| 메시지 페이로드의 데이터입니다. 최대 길이는 131072바이트입니다. |
|`QoS`|정수| 서비스 품질(QoS)입니다. 올바른 값은 `0`, `1`, `2`입니다.  |


## 디바이스에 명령 공개
{: #publish_commands_devices}

애플리케이션은 연결된 디바이스에 대한 명령을 공개할 수 있습니다.

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
다음 표에는 `publishCommand()` 메소드에 지정된 매개변수가 설명되어 있습니다.

|매개변수|데이터 유형|설명|
|:---|:---|
|`deviceType`|문자열| 디바이스 유형입니다. 일반적으로, deviceType은 특정 태스크를 수행하는 디바이스의 그룹화입니다(예: "weatherballoon"). |
|`deviceId`|문자열| 디바이스의 ID입니다. 일반적으로, 제공된 디바이스 유형의 경우 deviceId는 해당 디바이스의 고유 ID입니다(예: 일련 번호 또는 MAC 주소). |
|`command`|문자열| 명령의 이름입니다. |
|`format`|문자열| 형식은 임의의 문자열일 수 있습니다(예: JSON). |
|`data`|사전| 메시지 페이로드의 데이터입니다. 최대 길이는 131072바이트입니다. |
|`QoS`|정수| 서비스 품질(QoS)입니다. 올바른 값은 `0`, `1`, `2`입니다.  |
