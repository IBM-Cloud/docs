---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java를 사용하여 관리 게이트웨이 개발
{: #java_cli_managed_gw}

게이트웨이는 이에 연결된 디바이스의 관리에 중요한 역할을 수행합니다. 많은 디바이스가 아주 기본적이며 디바이스 관리 기능을 보유하지 않으므로, 게이트웨이에서 이러한 기본 디바이스의 관리가 필요합니다. {{site.data.keyword.iot_full}}에서 관리 게이트웨이는 이에 연결된 디바이스를 관리하며 디바이스 관리 기능(예: 펌웨어, 위치 및 진단 업데이트)을 제공할 수 있는 게이트웨이입니다.
{:shortdesc}

{{site.data.keyword.iot_short}} Java™ 클라이언트 라이브러리 및 제공된 정보를 사용하여 사용자는 게이트웨이를 관리 게이트웨이로 전환하기 위한 Java 코드를 개발할 수 있습니다. 또한 디바이스 관리 서비스에 게이트웨이를 연결하고 디바이스 관리 오퍼레이션을 실행하기 위한 Java 코드를 개발하는 데 도움이 되도록 샘플이 제공됩니다. 

## 디바이스 관리 서비스
{: #dm_service}

{{site.data.keyword.iot_short}} DM(Device Management) 서비스는 게이트웨이가 이에 연결된 디바이스를 관리할 수 있도록 디바이스 관리 기능을 제공합니다. 

관리 게이트웨이는 게이트웨이를 통해 {{site.data.keyword.iot_short}}에 연결된 모든 디바이스에 대한 프록시로서 실행되는 디바이스 관리 에이전트를 실행합니다. 

### 디바이스 관리 에이전트

게이트웨이 디바이스에서 지원하는 경우, 게이트웨이를 통해 간접적으로 {{site.data.keyword.iot_short}}에 연결된 디바이스는 다양한 연결 프로토콜을 사용할 수 있습니다. 

`ManagedGateway` 인스턴스는 하나 이상의 디바이스 관리 조치(예: 디바이스 관리 활동에 참여, 오류 코드, 로그, 위치 및 펌웨어 또는 디바이스 업데이트 조치)를 수행하기 위한 메소드의 목록을 제공하는 디바이스 관리 에이전트입니다. 

게이트웨이의 디바이스 관리 에이전트는 연결 중인 디바이스의 연결 프로토콜을 변환하고 처리하며, 이는 디바이스가 {{site.data.keyword.iot_short}}에 의해 관리될 수 있도록 보장합니다. 디바이스 관리 에이전트를 통해 게이트웨이는 연결된 디바이스 및 {{site.data.keyword.iot_short}} 간의 투명한 터널 이상이 됩니다. 예를 들어, 게이트웨이에 연결된 디바이스가 펌웨어를 다운로드할 수 없으면 게이트웨이의 디바이스 관리 에이전트가 다음 조치를 수행할 수 있습니다. 
- 펌웨어 다운로드를 위한 디바이스의 요청 인터셉트
- 디바이스에 대한 펌웨어 다운로드
- 게이트웨이에서 디바이스 펌웨어 저장

나중 시점에 디바이스가 업그레이드 수행 지시를 받을 때 게이트웨이의 디바이스 관리 에이전트는 펌웨어를 디바이스에 푸시하고 이를 업데이트할 수 있습니다. 

## 디바이스 모델 작성
{: #create_device_model}

{{site.data.keyword.iot_short}}에서 디바이스 모델은 디바이스와 게이트웨이의 메타데이터 및 관리 특성을 기술합니다. 디바이스 데이터베이스는 디바이스 또는 게이트웨이 정보의 마스터 소스입니다. 애플리케이션 및 관리 디바이스는 위치 업데이트, 펌웨어 업그레이드 진행 업데이트와 기타 유형의 업데이트를 전송할 수 있습니다. {{site.data.keyword.iot_short}}에 의해 업데이트가 수신되면, 연결 중인 애플리케이션이 해당 정보를 사용할 수 있도록 디바이스 데이터베이스가 업데이트됩니다. 

{{site.data.keyword.iot_short}} Java 클라이언트 라이브러리에서 디바이스 모델은 `DeviceData` Java 클래스로 표시됩니다. 

`DeviceData` 클래스를 작성하려면 다음 오브젝트를 작성하십시오. 

- `DeviceInfo`(선택사항)
- `DeviceLocation`(선택사항, 디바이스가 {{site.data.keyword.iot_short}} API를 통해 애플리케이션이 설정한 위치에 대해 알림을 받고자 하는 경우에만 필요함)
- `DeviceFirmware`(선택사항)
- `DeviceMetadata`(선택사항)

자세한 정보는 [디바이스 모델](../../reference/device_model.html)을 참조하십시오. 

### DeviceInfo

샘플 데이터가 포함된 다음 코드 스니펫은 `DeviceInfo` 및 `DeviceMetadata` 오브젝트를 작성하는 방법을 표시합니다. 

```java
DeviceInfo deviceInfo = new DeviceInfo.Builder().
                           serialNumber("10087").
                           manufacturer("IBM").
                           model("7865").
                           deviceClass("A").
                           description("My RasPi Device").
                           fwVersion("1.0.0").
                           hwVersion("1.0").
                           descriptiveLocation("EGL C").
                           build();

/**
  * Create a DeviceMetadata object
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);

```

다음 코드 스니펫은 이전 샘플에서 작성된 `DeviceInfo` 및 `DeviceMetadata` 오브젝트를 사용하여 `DeviceData` 클래스를 작성하는 방법을 간략하게 설명합니다. 

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();
```

모든 게이트웨이와 연결된 모든 디바이스에는 {{site.data.keyword.iot_short}}에서 자신을 표시하기 위한 자체 `DeviceData` 클래스 정의가 있어야 합니다. 게이트웨이의 경우, `DeviceData` 클래스는 `ManagedGateway` 인스턴스 생성의 일부로서 라이브러리에 전달됩니다. 연결된 디바이스의 경우, `DeviceData` 클래스는 `sendDeviceManageRequest()` 오브젝트의 일부로서 라이브러리에 전달됩니다. 

## 관리 게이트웨이 생성자
{: #construct_managed_gateway}

`ManagedGateway`는 독자적으로 또는 연결된 디바이스에 대해 최소한 하나의 디바이스 관리 오퍼레이션을 수행할 수 있는 관리 게이트웨이로서 {{site.data.keyword.iot_short}}에 게이트웨이를 연결하는 Java 클래스입니다. 또한 `ManagedGateway` 인스턴스를 사용하여 일반 게이트웨이 오퍼레이션(예: 게이트웨이 이벤트 공개, 디바이스 이벤트 연결 및 애플리케이션의 명령 청취)을 수행할 수도 있습니다. `ManagedGateway` 인스턴스는 디바이스 관리 에이전트입니다. 

`ManagedGateway` 클래스에서 두 개의 상이한 생성자(생성자 1과 생성자 2)는 상이한 패턴을 지원합니다. 

### 생성자 1

생성자 1은 다음의 모든 특성이 포함된 `DeviceData` 클래스를 허용하여 `ManagedGateway` 인스턴스를 생성합니다. 

| 특성     |설명      |
|----------------|----------------|
|`Organization-ID` |조직 ID입니다. |
|`Gateway-Type` |게이트웨이 디바이스의 유형입니다.|
|`Gateway-ID` |게이트웨이 디바이스의 ID입니다. |
|`Authentication-Method`|인증 메소드입니다. 지원되는 유일한 메소드는 "token"입니다. |
|`Authentication-Token`|API 키 토큰입니다. |
|`auth-key`   |auth-method의 값을 `apikey`로 설정할 때 지정해야 하는 선택적 API 키입니다.|
|`auth-token`   |auth-method의 값을 `apikey`로 설정할 때 필수인 API 키 토큰입니다. |
|`clean-session`|지속 가능한 구독 모드로 게이트웨이 연결을 원하는 경우에만 필요한 true 또는 false 값입니다. 기본적으로 `clean-session`은 `true`로 설정됩니다. |
|`Port`|연결할 포트 번호입니다. 8883 또는 443을 지정하십시오. 포트 번호를 지정하지 않으면 기본적으로 클라이언트가 포트 번호 8883의 {{site.data.keyword.iot_short_notm}}에 연결됩니다.|
|`WebSocket`|WebSocket을 사용한 게이트웨이 연결을 원하는 경우에만 필요한 true 또는 false 값입니다. |
|`MaxInflightMessages`  |연결을 위한 인플라이트 메시지의 최대 수를 설정합니다. 기본값은 100입니다.|
|`Automatic-Reconnect`  |연결이 끊긴 상태일 때 {{site.data.keyword.iot_short_notm}}에 디바이스를 자동으로 다시 연결하려는 경우에 필요한 true 또는 false 값입니다. 기본값은 false입니다.|
|`Disconnected-Buffer-Size`|클라이언트가 연결이 끊겼을 때 메모리에 저장할 수 있는 최대 메시지 수입니다. 기본값은 5000입니다.|

**참고:** 지속 가능한 구독 모드로 게이트웨이를 연결하려면 `clean-session`을 `false`로 설정하십시오. `clean-session` 특성에 대한 자세한 정보는 [MQTT 문서](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)의 '구독 버퍼 및 정리 세션' 절을 참조하십시오. 

다음 코드는 `ManagedGateway` 인스턴스를 작성하는 방법을 간략하게 설명합니다. 

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### 생성자 2

생성자 2는 `DeviceData` 오브젝트 및 MQTT 클라이언트 인스턴스를 허용하여 `ManagedGateway` 인스턴스를 생성합니다. 또한 생성자 2에서는 다음 코드 샘플에서 간략하게 설명한 대로 인스턴스의 `DeviceData` 오브젝트에 디바이스 유형 및 디바이스 ID가 포함되도록 요구합니다. 

```java
// Code that constructs either a synchronous or asynchronous MQTT client instance of mqttClient.
.....

// Code that constructs the DeviceData object
DeviceData deviceData = new DeviceData.Builder().
                         typeId("Gateway-Type").
                         deviceId("Gateway-ID").
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();

....
ManagedGateway ManagedGateway = new ManagedGateway(mqttClient, deviceData);

```

**참고:** 사용자가 디바이스 관리 오퍼레이션의 레버리지를 활용할 수 있도록 이 생성자가 기존의 연결된 MQTT 클라이언트 인스턴스를 사용하여 관리 게이트웨이 인스턴스를 작성하므로, 사용자 정의 디바이스용으로 개발 중인 경우에는 생성자 2를 사용하십시오. 모든 디바이스 함수에 대해 Java 클라이언트 라이브러리를 사용하십시오. 

## 게이트웨이의 디바이스 관리 요청
{: #dm_requests}

### 게이트웨이의 관리 요청 전송

디바이스 관리 활동에 참여하도록 게이트웨이에 지시하려면, 다음 코드 샘플에서 간략하게 설명된 `sendGatewayManageRequest()` 메소드를 호출하십시오. 

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
디바이스가 아직 {{site.data.keyword.iot_short}}에 연결되지 않은 경우, 관리 요청은 연결 요청을 내부적으로 시작합니다.

`sendGatewayManageRequest()` 메소드는 다음 매개변수를 허용합니다. 

| 매개변수     |설명      |
|----------------|----------------|
|`lifetime`|휴면 상태로 분류되어 비관리 디바이스가 되지 않도록 게이트웨이가 다른 관리 디바이스 유형 요청을 전송해야 하는 시간의 길이(초)입니다. `lifetime` 필드가 생략되거나 0으로 으로 설정된 경우에는 관리 게이트웨이가 휴면 상태가 되지 않습니다. `lifetime` 필드의 최소 지원 설정은 3600초(1시간)입니다. |
|`supportFirmwareActions`|게이트웨이가 펌웨어 조치를 지원하는지 여부를 판별하는 true 또는 false 값입니다. 게이트웨이는 또한 펌웨어 요청을 처리하기 위한 펌웨어 핸들러를 추가해야 합니다. |
|`supportDeviceActions`|게이트웨이가 디바이스 조치를 지원하는지 여부를 판별하는 true 또는 false 값입니다. 게이트웨이는 또한 재부팅 및 팩토리 재설정 요청을 처리하기 위한 디바이스 조치 핸들러를 추가해야 합니다. |


`ManagedGateway` 인스턴스는 하나 이상의 디바이스 관리 조치(예: 디바이스 관리 활동에 참여, 오류 코드, 로그, 위치 및 펌웨어 또는 디바이스 업데이트 조치)를 수행하기 위한 메소드의 목록을 제공하는 디바이스 관리 에이전트입니다. 

### 연결된 디바이스의 관리 요청 전송

게이트웨이 뒤에서 연결된 디바이스가 게이트웨이의 디바이스 관리 활동에 참여할 수 있도록 허용하려면 `sendDeviceManageRequest()` 메소드를 호출하십시오. 

`sendDeviceManageRequest()` 메소드는 `lifetime`, `supportFirmwareActions` 및 `supportDeviceActions` 매개변수와 연결된 디바이스의 세부사항을 받습니다. 게이트웨이는 또한 오버로드된 `sendDeviceManageRequest()` 메소드를 사용하여 연결된 디바이스에 대한 `DeviceData` 오브젝트를 정의할 수 있습니다. 

#### 연결된 디바이스의 관리 요청을 전송하는 예제

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### 게이트웨이의 비관리 요청 전송

게이트웨이를 더 이상 관리할 필요가 없을 때 게이트웨이에서 디바이스 관리 활동을 중지하려면 `sendGatewayUnmanageRequet()` 메소드를 호출하십시오. `sendGatewayUnmanageRequet()`를 호출하면 {{site.data.keyword.iot_short}}이 더 이상 게이트웨이에 대한 새 디바이스 관리 요청을 전송하지 않으며 **관리** 요청을 제외한 게이트웨이의 모든 디바이스 관리 요청이 거부됩니다. 게이트웨이 뒤에 있는 디바이스의 요청은 거부되지 않습니다. 

#### 게이트웨이의 비관리 요청을 전송하는 예제

```java
managedGateway.sendGatewayUnmanageRequet();
```

### 연결된 디바이스의 비관리 요청 전송

게이트웨이 뒤에 있는 디바이스를 더 이상 관리할 필요가 없을 때 연결된 디바이스를 관리 상태에서 비관리 상태로 이동하기 위해 게이트웨이는 `sendDeviceUnmanageRequet()` 메소드를 호출할 수 있습니다. `sendDeviceUnmanageRequet()`를 호출하면 {{site.data.keyword.iot_short}}이 더 이상 디바이스에 대한 새 디바이스 관리 요청을 전송하지 않으며 **Manage** 요청을 제외한 연결된 디바이스용인 게이트웨이의 모든 디바이스 관리 요청이 거부됩니다. 

#### 연결된 디바이스의 비관리 요청을 전송하는 예제

```java
managedGateway.sendDeviceUnmanageRequet();
```

## 위치 업데이트
{: #location_updates}

### 게이트웨이 위치 업데이트 전송

자신의 위치를 판별할 수 있는 게이트웨이는 위치 변경사항에 대해 {{site.data.keyword.iot_short}}에 알리도록 선택할 수 있습니다. 게이트웨이는 오버로드된 `updateLocation()` 메소드 중 하나를 호출하여 디바이스의 위치를 업데이트할 수 있습니다. 

```java
    // update the location with latitude, longitude, and elevation.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### 연결된 디바이스 위치 업데이트 전송

게이트웨이는 대응되는 `updateDeviceLocation()` 디바이스 메소드를 호출하여 연결된 디바이스의 위치를 업데이트할 수 있습니다. 오버로드된 메소드는 `measuredDateTime` 메소드를 지정하는 데 사용될 수 있습니다.   

```java
// update the location of the attached device with latitude, longitude, and elevation
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
위치 업데이트에 대한 자세한 정보는 [디바이스 관리 요청](../../devices/device_mgmt/index.html#/update-location#update-location)을 참조하십시오.

## 오류 코드 처리
{: #errors}

### 게이트웨이 오류 코드 작성 및 삭제

게이트웨이는 자체 오류 상태에 대한 변경사항을 {{site.data.keyword.iot_short}}에 알리도록 선택할 수 있습니다. 게이트웨이는 `addErrorCode()` 메소드를 호출하여 현재 오류 코드를 {{site.data.keyword.iot_short}}에 추가할 수 있습니다. 

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

게이트웨이에 대한 오류 코드는 아래에 표시된 대로 `clearErrorCodes()` 메소드를 호출하여 {{site.data.keyword.iot_short}}에서 지워질 수 있습니다. 

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### 연결된 디바이스에 대한 오류 코드 작성 및 삭제

게이트웨이는 또한 대응되는 디바이스 메소드를 호출하여 연결된 디바이스에 대한 오류 코드를 추가하거나 지울 수 있습니다. 

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### 게이트웨이 로그 메시지 작성 및 삭제

게이트웨이는 새 로그 항목을 추가하여 변경사항에 대해 {{site.data.keyword.iot_short}}에 알리도록 선택할 수 있습니다. 로그 항목에는 다음 항목이 포함되어 있습니다.

- 메시지 문자열
- 시간소인
- 심각도
- base64 인코딩된 2진 진단 데이터(선택사항)

게이트웨이는 `addGatewayLog()` 메소드를 호출하여 로그 메시지를 전송할 수 있으며, 이는 다음 샘플에서 간략하게 설명되어 있습니다. 

```java
// An example Log event
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

`clearLogs()` 메소드를 호출하여 {{site.data.keyword.iot_short}}에서 로그 메시지를 지울 수 있습니다. 

```java
rc = managedGateway.clearGatewayLogs();
```

### 연결된 디바이스에 대한 로그 작성 및 삭제

유사하게, 게이트웨이는 대응되는 디바이스 메소드를 호출하여 연결된 디바이스에 대한 로그를 작성하거나 지울 수 있으며, 이는 다음 샘플에서 간략하게 설명되어 있습니다. 

```java

// An example log event:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

연결된 디바이스의 로그를 지우려면 연결된 디바이스의 세부사항을 지정하여 `clearDeviceLogs()` 메소드를 호출하십시오. 이는 다음 코드 샘플에서 간략하게 설명되어 있습니다. 

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

디바이스 진단 오퍼레이션의 용도는 게이트웨이 또는 디바이스 오류에 대한 정보를 제공하는 것입니다. 이는 {{site.data.keyword.iot_short}}에 디바이스 연결에 대한 진단 정보는 제공하지 않습니다. 

진단 오퍼레이션에 대한 자세한 정보는 [디바이스 관리 요청](../../devices/device_mgmt/index.html#/update-location#update-location)을 참조하십시오. 

## 펌웨어 업데이트 및 조치
{: #firmware}

펌웨어 업데이트 프로세스는 두 개의 개별 조치로 구분됩니다. 

- 펌웨어 다운로드
- 펌웨어 업데이트

게이트웨이는 독자적으로 및 자체 연결된 디바이스에 대해 펌웨어 조치를 지원하기 위해 다음 활동을 수행해야 합니다. 

1. 선택사항: `DeviceFirmware` 오브젝트를 생성합니다. 
2. 펌웨어 조치 지원에 대해 서버에 알립니다. 
3. 펌웨어 조치 핸들러를 작성합니다. 
4. `ManagedGateway`에 핸들러를 추가합니다. 

### 1단계: `DeviceFirmware` 오브젝트 생성

펌웨어 조치를 수행하기 위해 게이트웨이는 독자적으로 및 자체 연결된 디바이스에 대해 `DeviceFirmware` 오브젝트를 선택적으로 생성한 후에 이를 `DeviceData` 오브젝트에 추가할 수 있습니다. 이는 다음 샘플에서 간략하게 설명되어 있습니다. 

```java
DeviceFirmware firmware = new DeviceFirmware.Builder().
			version("Firmware.version").
			name("Firmware.name").
			url("Firmware.url").
			verifier("Firmware.verifier").
			state(FirmwareState.IDLE).				
			build();

DeviceData deviceData = new DeviceData.Builder().
			deviceInfo(deviceInfo).
			deviceFirmware(firmware).
			metadata(metadata).
			build();

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
managedGateway.connect();
```

연결된 디바이스의 경우, 생성된 `DeviceData` 오브젝트는 다음 코드 샘플에서 간략하게 설명된 대로 관리 요청을 전송하는 동안 라이브러리에 전달될 수 있습니다. 

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

`DeviceFirmware` 오브젝트는 게이트웨이 또는 연결된 디바이스의 현재 펌웨어를 표시하며, {{site.data.keyword.iot_short}}에 펌웨어 다운로드와 펌웨어 업데이트 조치의 상태를 보고하는 데 사용됩니다. `DeviceFirmware` 오브젝트가 게이트웨이에 의해 생성되지 않은 경우, 라이브러리는 비어 있는 오브젝트를 작성하며 상태를 {{site.data.keyword.iot_short}}에 보고합니다. 

### 2단계: 펌웨어 조치 지원에 대해 서버에 알림

게이트웨이 또는 연결된 디바이스는 서버가 펌웨어 요청을 시작할 수 있도록 펌웨어 조치 플래그를 true로 설정해야 합니다. 이러한 변경은 관리 요청에서 `supportFirmwareActions` 매개변수에 대해 true 값을 전달하여 이루어질 수 있습니다. 

게이트웨이는 다음 메소드를 호출하여 자체 펌웨어 지원에 대해 서버에 알릴 수 있습니다. 
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

유사하게, 게이트웨이는 대응되는 디바이스 메소드를 호출하여 연결된 디바이스의 펌웨어 지원을 알릴 수 있습니다. 

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

지원을 디바이스 관리 서버에 알린 경우, 서버는 게이트웨이 자체 또는 그 뒤의 디바이스에 대해 게이트웨이에 펌웨어 조치를 전달합니다. 

### 3단계: 펌웨어 조치 핸들러 작성

펌웨어 조치를 지원하기 위해 게이트웨이는 핸들러를 작성하고 이를 `managedGateway`에 추가해야 합니다. 핸들러에서 `DeviceFirmwareHandler` 클래스를 확장하고 다음 메소드를 구현해야 합니다.

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**참고**: 펌웨어 다운로드 또는 업데이트 요청이 경로 재지정된 게이트웨이 및 연결된 디바이스 모두에 대해 라이브러리에 오직 하나의 핸들러만 추가되어야 합니다. 구현에서는 동시에 여러 펌웨어 요청을 처리하기 위해 스레드 또는 스레드 풀을 작성해야 합니다. 

[게이트웨이 샘플 GutHub 저장소 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}에서 스레드 풀 핸들러의 샘플 구현을 찾을 수 있습니다. 

### `downloadFirmware`의 샘플 구현

구현에서는 `DeviceFirmware` 오브젝트를 사용하여 펌웨어를 다운로드하고 다운로드 상태를 보고하는 로직을 추가해야 합니다. 펌웨어 다운로드 오퍼레이션에 성공하는 경우, 펌웨어의 상태는 'DOWNLOADED'로 설정되어야 하며 `UpdateStatus` 특성은 'SUCCESS'로 설정되어야 합니다. 

펌웨어 다운로드 중에 오류가 발생하는 경우에는 상태가 'IDLE'로 설정되어야 하며 `updateStatus` 특성이 다음 오류 상태 값 중 하나로 설정되어야 합니다. 

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

샘플 펌웨어 다운로드 구현은 다음 코드 샘플에 표시되어 있습니다. 

**중요:** 제공된 코드 샘플에는 스레드 풀 섹션이 포함되지 않습니다. 펌웨어 핸들러의 전체 구현의 경우 샘플은 [IBM Java 게이트웨이 샘플 GitHub 저장소 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}에서 사용 가능합니다. 

```java
public void downloadFirmware(DeviceFirmware deviceFirmware) {
	boolean success = false;
	URL firmwareURL = null;
	URLConnection urlConnection = null;

	try {
		firmwareURL = new URL(deviceFirmware.getUrl());
		urlConnection = firmwareURL.openConnection();
		if(deviceFirmware.getName() != null) {
			downloadedFirmwareName = deviceFirmware.getName();
		} else {
			// use the time stamp as the name
			downloadedFirmwareName = "firmware_" +new Date().getTime()+".deb";
		}

		File file = new File(downloadedFirmwareName);
		BufferedInputStream bis = new BufferedInputStream(urlConnection.getInputStream());
		BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(file.getName()));

		int data = bis.read();
		if(data != -1) {
			bos.write(data);
			byte[] block = new byte[1024];
			while (true) {
				int len = bis.read(block, 0, block.length);
				if(len != -1) {
					bos.write(block, 0, len);
				} else {
					break;
				}
			}
			bos.close();
			bis.close();
			success = true;
		} else {
			//There is no data to read, so set an error
			deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
		}
	} catch(MalformedURLException me) {
		// Invalid URL, so set the status to reflect the same,
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
	} catch (IOException e) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.CONNECTION_LOST);
	} catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
	}

		if(success == true) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
		deviceFirmware.setState(FirmwareState.DOWNLOADED);
	} else {
		deviceFirmware.setState(FirmwareState.IDLE);
	}
}
```

관리 게이트웨이는 검사기를 사용하여 다운로드된 펌웨어 이미지의 무결성을 확인한 후에 상태를 다시 {{site.data.keyword.iot_short}}에 보고할 수 있습니다. 검사기는 다음 단계 중에 게이트웨이에 의해 설정될 수 있습니다. 

- 'DeviceFirmware' 오브젝트가 작성될 때 스타트업 중에
- 애플리케이션이 'downloadFirmware' 요청을 제출할 때

#### 예제

```java
private boolean verifyFirmware(File file, String verifier) throws IOException {
	FileInputStream fis = null;
	String md5 = null;
	try {
		fis = new FileInputStream(file);
		md5 = org.apache.commons.codec.digest.DigestUtils.md5Hex(fis);
		System.out.println("Downloaded Firmware MD5 sum:: "+ md5);
	} catch (FileNotFoundException e) {
		e.printStackTrace();
	} catch (IOException e) {
		e.printStackTrace();
	} finally {
		fis.close();
	}
	if(verifier.equals(md5)) {
		System.out.println("Firmware verification successful");
		return true;
	}
	System.out.println("Download firmware checksum verification failed."
			+ "Expected "+verifier + " found "+md5);
	return false;
}
```

전체 코드는 게이트웨이 관리 샘플 [GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java)에서 찾을 수 있습니다. 

### `updateFirmware`의 샘플 구현

구현에서는 별도의 스레드를 작성하고 `DeviceFirmware` 오브젝트를 사용하여 다운로드된 펌웨어를 설치하고 업데이트 상태를 보고하는 로직을 추가해야 합니다. 펌웨어 업데이트 오퍼레이션에 성공하는 경우, 펌웨어의 상태는 'IDLE'로 설정되어야 하며 `updateStatus` 값은 'SUCCESS'로 설정되어야 합니다. 

펌웨어 업데이트 중에 오류가 발생하면 `updateStatus` 값이 다음 오류 상태 값 중 하나로 설정되어야 합니다. 

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

다음 코드 샘플은 Raspberry Pi 디바이스에 대한 펌웨어 업데이트를 구현할 수 있는 방법을 간략하게 설명합니다. 

```java
public void updateFirmware(DeviceFirmware deviceFirmware) {
	try {
		ProcessBuilder pkgInstaller = null;
		Process p = null;
		pkgInstaller = new ProcessBuilder("sudo", "dpkg", "-i", downloadedFirmwareName);
		boolean success = false;
		try {
			p = pkgInstaller.start();
			boolean status = waitForCompletion(p, 5);
			if(status == false) {
				p.destroy();
				deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
				return;
			}
			System.out.println("Firmware Update command "+status);
			deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
			deviceFirmware.setState(FirmwareState.IDLE);
		} catch (IOException e) {
			e.printStackTrace();
			deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
		} catch (InterruptedException e) {
			e.printStackTrace();
			deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
		}
	} catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
	}
}
```

전체 코드는 [게이트웨이 샘플 GitHub 저장소 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}에 있는 `GatewayFirmwareHandlerSample` 샘플에서 찾을 수 있습니다. 

### 4단계: `ManagedGateway`에 핸들러 추가

핸들러가 작성되는 경우, 이는 {{site.data.keyword.iot_short}}에서 펌웨어 조치 요청이 있을 때 Java 클라이언트 라이브러리가 대응되는 메소드를 호출하도록 `ManagedGateway` 인스턴스에 추가되어야 합니다. 

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

펌웨어 조치에 대한 자세한 정보는 [디바이스 관리 요청 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions){: new_window}을 참조하십시오. 

## 디바이스 조치
{: #dev_actions}

{{site.data.keyword.iot_short}}에서는 다음 디바이스 조치를 지원합니다. 

- 재부팅
- 팩토리 재설정

게이트웨이는 독자적으로 또한 그 뒤에 있는 디바이스에 대해 디바이스 조치를 지원할 수 있도록 다음 활동을 수행해야 합니다. 

1. 디바이스 조치 지원에 대해 서버에 알립니다. 
2. 디바이스 조치 핸들러를 작성합니다. 
3. `ManagedGateway`에 핸들러를 추가합니다. 

### 1단계: 디바이스 조치 지원에 대해 서버에 알림

게이트웨이 및 연결된 디바이스에 대해 재부팅 또는 팩토리 재설정 조치를 수행하려면, 우선 게이트웨이가 지원에 대해 {{site.data.keyword.iot_short}}에 알려야 합니다. 이 조치는 **관리** 요청을 전송할 때 `supportDeviceActions` 매개변수에 대해 true 값을 전달하여 수행될 수 있습니다. 

게이트웨이는 다음 메소드를 호출하여 자체 디바이스 조치 지원에 대해 서버에 알릴 수 있습니다. 

```java
// Last parameter represents the device action support
managedGateway.sendGatewayManageRequest(3600, true, true);
```

게이트웨이는 대응되는 디바이스 메소드를 호출하여 연결된 디바이스의 디바이스 조치 지원을 알릴 수 있습니다. 

```java
// Last parameter represents the device action support
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

지원을 디바이스 관리 서버에 알리는 경우, 서버는 디바이스 조치 요청을 디바이스에 전달합니다. 

### 2단계: 디바이스 조치 핸들러 작성

디바이스 조치를 지원하기 위해 게이트웨이는 핸들러를 작성하고 이를 `managedGateway` 인스턴스에 추가해야 합니다. 핸들러는 `DeviceActionHandler` 클래스를 확장하고 다음 메소드에 대한 구현을 제공해야 합니다. 

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**참고:** 디바이스 조치 요청이 경로 재지정된 게이트웨이 및 연결된 디바이스 모두에 대해 라이브러리에 오직 하나의 핸들러만 추가되어야 합니다. 구현에서는 동시에 여러 디바이스 조치 요청을 처리하기 위해 스레드 또는 스레드 풀을 작성해야 합니다. 스레드 풀을 사용하는 샘플러 핸들러 구현은 [iot-gateway-samples GitHub 저장소 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window}에 표시됩니다. 

### `handleReboot`의 샘플 구현

구현에서는 별도의 스레드를 작성하고 `DeviceAction` 오브젝트를 사용하여 게이트웨이 및 연결된 디바이스를 재부팅하고 재부팅 상태를 보고하는 로직을 추가해야 합니다. 요청을 수신한 후에 게이트웨이는 실제 재부팅을 진행하기 전에 지원 또는 실패에 대해 우선 서버에 알려야 합니다. 샘플이 디바이스를 재부팅할 수 없거나 재부팅 중에 기타 오류가 발생하는 경우, 게이트웨이는 선택적 메시지의 상태를 업데이트할 수 있습니다. Raspberry Pi 디바이스에 대한 샘플 재부팅 구현은 다음 코드 샘플에서 제공됩니다. 

```java
public void handleReboot(DeviceAction action) {
	ProcessBuilder processBuilder = null;
	Process p = null;
	processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
	boolean status = false;
	try {
		p = processBuilder.start();
		// wait for say 2 minutes before giving it up
		status = waitForCompletion(p, 2);
	} catch (IOException e) {
		action.setMessage(e.getMessage());
	} catch (InterruptedException e) {
		action.setMessage(e.getMessage());
	}
	if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
	}
}
```

스레드 풀을 사용하는 전체 샘플러 핸들러 구현은 [iot-gateway-samples GitHub 저장소 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window}에 표시됩니다. 


### `handleFactoryReset`의 샘플 구현

구현에서는 별도의 스레드를 작성하고 DeviceAction 오브젝트를 사용하여 게이트웨이 및 연결된 디바이스를 팩토리 설정으로 재설정하고 재설정 상태를 보고하는 로직을 추가해야 합니다. 요청이 수신되면 게이트웨이는 실제 재설정을 진행하기 전에 지원 또는 실패에 대해 우선 서버에 알려야 합니다. 팩토리 재설정 구현의 기본 아웃라인은 다음 코드 샘플에 표시되어 있습니다. 

```java
public void handleFactoryReset(DeviceAction action) {
	try {
		// code to perform Factory reset
	} catch (IOException e) {
		action.setMessage(e.getMessage());
	}
	if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
	}
}
```

### 3단계: `ManagedGateway`에 핸들러 추가

핸들러가 작성되는 경우, 이는 게이트웨이 또는 연결된 디바이스에 대해 {{site.data.keyword.iot_short}}에서 디바이스 조치 요청이 있을 때 Java 클라이언트 라이브러리가 대응되는 메소드를 호출하도록 `ManagedGateway` 인스턴스에 추가되어야 합니다. 

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

디바이스 조치에 대한 자세한 정보는 [디바이스 관리 요청 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot){: new_window}을 참조하십시오. 

## 디바이스 속성 변경사항 청취
{: #listen_device_attributes}

Java 클라이언트 라이브러리는 {{site.data.keyword.iot_short}}에서 업데이트 요청이 있을 때마다 대응되는 오브젝트를 업데이트합니다. 이러한 업데이트 요청은 {{site.data.keyword.iot_short}} REST API를 사용하여 펌웨어 업데이트를 통해 직간접적으로 애플리케이션에 의해 시작됩니다. 이러한 속성의 업데이트 외에도 라이브러리는 디바이스 속성이 업데이트될 때마다 게이트웨이에 알릴 수 있는 메커니즘을 제공합니다. 

이 오퍼레이션 유형으로 업데이트될 수 있는 속성은 게이트웨이 또는 연결된 디바이스의 위치, 메타데이터, 디바이스 정보 및 펌웨어입니다. 

속성 변경사항에 대해 알림을 받으려면 게이트웨이가 관심 있는 오브젝트에 특성 변경 리스너를 추가해야 하며, 이는 다음 코드 샘플에서 간략하게 설명되어 있습니다. 

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

게이트웨이는 또한 알림을 수신하는 `propertyChange()` 메소드를 구현해야 하며, 이는 다음 샘플 구현에서 간략하게 설명되어 있습니다. 

```java
public void propertyChange(PropertyChangeEvent evt) {
	if(evt.getNewValue() == null) {
		return;
	}
	Object value = (Object) evt.getNewValue();
		switch(evt.getPropertyName()) {
		case "metadata":
			DeviceMetadata metadata = (DeviceMetadata) value;
			System.out.println("Received an updated metadata -- "+ metadata);
			break;

			case "location":
			DeviceLocation location = (DeviceLocation) value;
			System.out.println("Received an updated location -- "+ location);
			break;

			case "deviceInfo":
			DeviceInfo info = (DeviceInfo) value;
			System.out.println("Received an updated device info -- "+ info);
			break;

			case "mgmt.firmware":
			DeviceFirmware firmware = (DeviceFirmware) value;
			System.out.println("Received an updated device firmware -- "+ firmware);
			break;		
	}
}
```

디바이스 속성 업데이트에 대한 자세한 정보는 [디바이스 관리 요청 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes){: new_window}을 참조하십시오. 

## 샘플
{: #samples}

게이트웨이 및 게이트웨이 뒤에 있는 디바이스를 {{site.data.keyword.iot_short_notm}} 인스턴스에 연결하는 데 도움이 되도록 여러 샘플이 사용 가능합니다. 샘플은 {{site.data.keyword.iot_short_notm}} Java 클라이언트 라이브러리를 사용하며 [게이트웨이 샘플 GitHub 저장소 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window}에 있습니다. 

## 레시피
{: #recipes}

관리 게이트웨이로 Rasberry Pi 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결하고 연결된 디바이스를 관리하는 방법을 보여주는 레시피는 [{{site.data.keyword.iot_short_notm}}에서 관리 게이트웨이 역할의 Raspberry Pi ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}를 참조하십시오. 

이 레시피는 {{site.data.keyword.iot_short_notm}}의 디바이스 관리 프로토콜을 사용하여 게이트웨이 역할을 하는 Raspberry Pi 디바이스에서 Arduino Uno 디바이스를 관리하고 디바이스 관리 오퍼레이션(예: 디바이스 재부팅 또는 스케치 프로그램 추가)을 수행할 수 있는 방법을 설명합니다. 
