---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 외부 서비스 통합
{: #ref-index}

외부 서비스 통합을 사용하면 {{site.data.keyword.iot_full}} 조직에 있는 써드파티 또는 외부 서비스의 오퍼레이션과 데이터에 액세스할 수 있습니다.

## Jasper
{: #jasper}

Jasper는 SIM 디바이스의 관리 플랫폼입니다. Jasper는 {{site.data.keyword.iot_short_notm}} 대시보드에 통합되므로 {{site.data.keyword.iot_short_notm}} 조직 대시보드를 통해 Jasper 디바이스를 관리할 수 있습니다.

### Jasper에 지원되는 오퍼레이션

IBM 플랫폼을 통해 제공되는 기본 제공 Jasper 통합에서는 다음과 같은 Jasper 오퍼레이션을 지원합니다.

- 전체 Jasper 데이터 보기
  - 상태, 요금제, 월별 데이터 사용, 월별 SMS 사용, 월별 음성 사용, 초과 한도, 추가된 날짜 및 수정한 날짜를 표시합니다.
- SIM 활성화 상태 변경
  - 인벤토리, 활성화 준비, 활성화됨, 비활성화됨 및 폐기됨 중에 선택하십시오.
- SIM 사용 보기
  - 주기 시작 날짜, 청구 가능 및 총 데이터, 청구 가능 및 총 SMS, 청구 가능 및 총 음성을 표시합니다.
  - 주기 시작 날짜는 YYYY-MM-DD 형식을 사용하여 설정할 수 있습니다.
- SIM에 SMS 전송
- 요금제 변경

다음 구성 단계가 완료된 후 Jasper에 연결된 디바이스의 디바이스 드릴 다운에서 지원되는 오퍼레이션에 액세스할 수 있습니다.

### Jasper용 REST API
Jasper용 REST API에 액세스하려면 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Jasper_Extension){: new_window} 문서에서 Jasper 확장기능 섹션을 참조하십시오. 

### Jasper 구성

{{site.data.keyword.iot_short_notm}} 조직에 Jasper 서비스를 연결하려면 먼저 두 단계의 구성을 수행해야 합니다. 먼저 {{site.data.keyword.iot_short_notm}}을 Jasper 서비스에 연결한 다음 {{site.data.keyword.iot_short_notm}} 디바이스를 구성해야 합니다.


1. Jasper 확장기능을 사용하십시오. {{site.data.keyword.iot_short_notm}} 조직과 Jasper를 통합할 수 있으려면 다음 단계를 완료하십시오.
  1. {{site.data.keyword.iot_short_notm}} 대시보드에서 **확장기능**을 선택하십시오.
  2. **확장기능** 페이지에서 **확장기능 추가**를 클릭하십시오.
  3. Jasper 옆의 **추가**를 클릭하십시오.
  4. Jasper 사용자 이름, 비밀번호, 액세스 키 및 도메인 ID를 입력하십시오.
  5. **완료**를 클릭하십시오.

2. 디바이스를 구성하십시오.
{{site.data.keyword.iot_short_notm}} 대시보드에서 Jasper의 데이터를 표시하도록 {{site.data.keyword.iot_short_notm}} 조직과 Jasper 계정에 모두 연결된 디바이스를 구성할 수 있습니다.  
**중요:** Jasper 구성은 디바이스 추가 프로세스의 일부로 적용할 수 없습니다. 이전에 연결된 디바이스만 Jasper로 구성할 수 있습니다.  
Jasper 연결 디바이스를 구성하려면 다음 단계를 완료하십시오.
 1. {{site.data.keyword.iot_short_notm}} 대시보드의 디바이스 탭에서 구성할 Jasper 연결 디바이스를 찾으십시오.
 2. *디바이스 드릴 다운* 보기를 열 디바이스를 선택하십시오.
 3. *확장기능 구성*까지 아래로 화면이동하십시오.
 4. 다음 JSON 형식을 사용하여 확장기능 구성을 입력한 다음 **변경 확인**을 클릭하여 구성을 저장하십시오.  

```json  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

조직이 정상적으로 구성되면 *확장기능* 섹션이 *디바이스 드릴 다운* 보기의 *확장기능 구성* 섹션에 표시됩니다.

## AT&T
{: #att}

### AT&T에 지원되는 오퍼레이션

AT&T 확장기능을 사용하면 다음 AT&T 오퍼레이션을 수행할 수 있습니다.

- 전체 AT&T 데이터 보기
  - 상태, 요금제, 월별 데이터 사용, 월별 SMS 사용, 월별 음성 사용, 초과 한도, 추가된 날짜 및 수정한 날짜를 표시합니다.
- SIM 활성화 상태 변경
  - 인벤토리, 활성화 준비, 활성화됨, 비활성화됨 및 폐기됨 중에 선택하십시오.
- SIM 사용 보기
  - 주기 시작 날짜, 청구 가능 및 총 데이터, 청구 가능 및 총 SMS, 청구 가능 및 총 음성을 표시합니다.
  - 주기 시작 날짜는 YYYY-MM-DD 형식을 사용하여 설정할 수 있습니다.
- SIM에 SMS 전송
- 요금제 변경

### AT&T용 REST API
AT&T용 REST API에 액세스하려면 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/AT&T_Extension){: new_window} 문서에서 AT&T 확장 섹션을 참조하십시오. 

### AT&T의 구성

{{site.data.keyword.iot_short_notm}} 조직을 AT&T에 연결하려면 조직 구성 및 디바이스 구성을 완료해야 합니다.

{{site.data.keyword.iot_short_notm}} 플랫폼을 구성하려면 다음 단계를 완료하십시오.

1. AT&T 확장 기능을 사용하십시오. AT&T와 {{site.data.keyword.iot_short_notm}} 조직을 통합할 수 있으려면 다음 단계를 완료하십시오.
  1. {{site.data.keyword.iot_short_notm}} 대시보드에서 **확장기능**을 선택하십시오.
  2. **확장기능** 페이지에서 **확장기능 추가**를 클릭하십시오.
  3. AT&T 옆의 **추가**를 클릭하십시오.
  4. AT&T 사용자 이름, 비밀번호, 액세스 키 및 도메인 ID를 입력하십시오.
  5. **완료**를 클릭하십시오.

{{site.data.keyword.iot_short_notm}} 조직을 AT&T 계정과 연결하려면 먼저 두 단계의 구성을 수행해야 합니다. 조직 구성을 완료한 다음 디바이스를 구성하십시오.


2. 디바이스를 구성하십시오.
{{site.data.keyword.iot_short_notm}} 대시보드에서 AT&T의 데이터를 표시하도록 {{site.data.keyword.iot_short_notm}} 조직과 AT&T 계정에 모두 연결된 디바이스를 구성할 수 있습니다.  
**중요:** AT&T 구성은 디바이스 추가 프로세스의 일부로 적용할 수 없습니다. 이전에 연결된 디바이스만 AT&T로 구성할 수 있습니다.  
AT&T 연결 디바이스를 구성하려면 다음 단계를 완료하십시오.
 1. {{site.data.keyword.iot_short_notm}} 대시보드의 디바이스 탭에서 구성할 AT&T 연결 디바이스를 찾으십시오.
 2. *디바이스 드릴 다운* 보기를 열 디바이스를 선택하십시오.
 3. *확장기능 구성*까지 아래로 화면이동하십시오.
 4. 다음 JSON 형식을 사용하여 확장기능 구성을 입력한 다음 **변경 확인**을 클릭하여 구성을 저장하십시오.  

```json  
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

조직이 정상적으로 구성되면 *확장기능* 섹션이 *디바이스 드릴 다운* 보기의 *확장기능 구성* 섹션에 표시됩니다.

## ARM mbed 커넥터
{: #arm}

ARM mbed 커넥터를 사용하면 {{site.data.keyword.iot_short_notm}}에 ARM mbed 디바이스를 연결할 수 있습니다. ARM mbed 확장기능에서는 ARM mbed 포털이 허용되며 {{site.data.keyword.iot_short_notm}}이 ARM mbed 포털에서 데이터를 송수신할 수 있습니다.

### 구성 설정


1. ARM mbed 커넥터 확장기능을 사용하십시오. ARM mbed 커넥터 확장기능을 사용으로 설정하려면 다음 단계를 완료하십시오.
  1. {{site.data.keyword.iot_short_notm}} 대시보드에서 **설정**을 선택하고 **확장기능**으로 이동하십시오.
  2. **확장기능** 메뉴에서 **확장기능 추가**를 클릭하십시오.
  3. ARM mbed 커넥터 확장기능 옆의 **추가**를 클릭하십시오.
  4. ARM mbed 액세스 키 및 도메인 ID를 입력하십시오. 이 키와 ID는 https://connector.mbed.com에서 ARM mbed 포털을 사용하여 찾을 수 있습니다.
  5. **연결 확인** 단추를 클릭하여 신임 정보가 올바른지 확인하십시오.
  6. **완료**를 클릭하십시오.

### 페이로드 형식

ARM mbed 플랫폼, 알림 및 비동기 응답에서 수신되는 두 가지 유형의 메시지가 있습니다. {{site.data.keyword.iot_short_notm}}은 ARM mbed 플랫폼에 연결된 디바이스로 명령을 보낼 수 있습니다.

#### 알림

디바이스 또는 센서 데이터의 변경사항에 의해 알림이 생성됩니다. {{site.data.keyword.iot_short_notm}}은 메시지를 처리한 후 {{site.data.keyword.iot_short_notm}}에 디바이스를 직접 연결한 것과 같은 방식으로 디바이스 이벤트 주제에 공개합니다. ARM mbed 플랫폼에 연결된 디바이스에서 시작된 알림에 사용되는 이벤트 유형은 `notify`입니다.

다음 코드 샘플은 ARM mbed 플랫폼 API에서 보낸 알림에 대한 페이로드 형식을 표시합니다.

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### 비동기 응답

{{site.data.keyword.iot_short_notm}}이 ARM mbed 플랫폼에 연결된 디바이스로 명령을 보내면 디바이스가 {{site.data.keyword.iot_short_notm}}으로 다시 확인 메시지를 보냅니다. 이 확인 메시지는 *비동기 응답*이라고 하며 이벤트 유형 `asyncResponse`를 사용합니다.

다음 코드 샘플은 ARM mbed 클라우드 서비스에서 보낸 비동기 응답에 대한 페이로드 형식을 표시합니다.

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### ARM mbed 플랫폼으로 명령 보내기

{{site.data.keyword.iot_short_notm}}은 ARM mbed 플랫폼에 연결된 디바이스로 명령을 보낼 수 있습니다. ARM mbed 플랫폼으로 보낸 명령은 다음 JSON 형식을 사용해야 합니다.

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```
선택한 메소드는 대소문자를 구분합니다. 리소스 경로의 처음 '/'는 건너뛰어야 합니다.


다음 주제에 페이로드를 공개해야 합니다.

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```


## Orange
{: #orange}

Orange 확장기능을 사용하면 {{site.data.keyword.iot_short_notm}}에 연결되었으며 Orange SIM 카드가 설치된 디바이스에서 SIM 카드 데이터를 볼 수 있습니다.

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Orange에 지원되는 오퍼레이션

{{site.data.keyword.iot_short_notm}} 서비스에 연결되어 있고 Orange SIM 카드가 있는 디바이스가 있으면 Orange 확장기능을 사용하여 다음 SIM 카드 데이터를 볼 수 있습니다.

- SIM 일련 번호
- 활성화 상태
- 마지막 상태 변경
- 마지막 상태 새로 고치기
- 위치 상태

### Orange용 REST API
Orange용 REST API에 액세스하려면 [{{site.data.keyword.iot_short_notm}} HTTP REST API ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Orange_Extension){: new_window} 문서에서 Orange 확장기능 섹션을 참조하십시오. 

### Orange 구성

Orange 확장기능을 사용하려면 다음을 수행하십시오.

1. {{site.data.keyword.iot_short_notm}} 대시보드에서 **확장기능**을 선택하십시오.
2. **확장기능** 페이지에서 **확장기능 추가**를 클릭하십시오.
3. Orange 확장기능 옆의 **추가**를 클릭하십시오.
4. Orange 사용자 이름과 비밀번호를 입력하십시오.
6. **완료**를 클릭하십시오.

Orange 확장기능을 사용으로 설정하고 나면 Orange SIM 데이터를 표시하도록 Orange SIM 카드가 있는 각 디바이스를 구성해야 합니다.

1. {{site.data.keyword.iot_short_notm}} 대시보드의 디바이스 탭에서 구성할 Orange SIM 디바이스를 찾으십시오.
2. 디바이스를 선택하고 *확장기능 구성*까지 아래로 화면이동하십시오.
3. 다음 JSON 형식을 사용하여 확장기능 구성을 입력한 다음 **변경 확인**을 클릭하여 구성을 저장하십시오.

```  
    {
        "orange": {
            "serialnumber": "<serial number of Orange SIM>"
        }
    }

```
조직이 정상적으로 구성되면 *확장기능* 섹션이 *디바이스 드릴 다운* 보기의 *확장기능 구성* 섹션에 표시됩니다.

## 히스토리 데이터 스토리지
{: #historical_data}

히스토리 데이터 스토리지 확장기능을 사용하면 IoT 데이터에 대해 호환 가능한 메시지 스토리지 서비스(예: [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) 또는 [{{site.data.keyword.messagehub_full}}](../../message_hub.html))를 찾아 구성할 수 있습니다.

## 사용자 정의 디바이스 관리 패키지
{: #device_mgmt}

디바이스 관리는 {{site.data.keyword.iot_short_notm}}의 코어 기능이지만 추가 기능을 개발하기 위해 확장할 수 있습니다. 사용자 정의 디바이스 관리 패키지는 올바른 JSON으로 구성되어야 하며 최소한 하나의 사용자 정의 디바이스 관리 조치를 정의해야 합니다. 

필수 JSON 형식의 예제를 포함하여 사용자 정의 디바이스 관리 기능에 대한 자세한 정보는 [디바이스 관리 사용자 정의 확장기능](../../devices/device_mgmt/custom_actions.html){: new_window}을 참조하십시오. 

### 사용자 정의 디바이스 관리 패키지 추가

{{site.data.keyword.iot_short_notm}} 대시보드를 사용하거나 API를 사용하여 사용자 정의 디바이스 관리 패키지를 추가할 수 있습니다. 

{{site.data.keyword.iot_short_notm}} 대시보드를 사용하여 사용자 정의 디바이스 관리 패키지를 추가하려면 다음을 수행하십시오. 

1. {{site.data.keyword.iot_short_notm}} 대시보드의 탐색줄에서 **설정**을 클릭하십시오. 
2. **사용자 정의 디바이스 관리 패키지**를 클릭하십시오. 
3. **패키지 추가** 단추를 클릭하십시오. 
4. 패키지 파일을 선택하고 **열기**를 클릭하십시오. 

API를 사용하여 사용자 정의 디바이스 관리 패키지를 추가하려면 [{{site.data.keyword.iot_short_notm}} API 문서 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}를 참조하십시오. 

## 블록체인(Blockchain)
{: #blockchain}

블록체인이 포함된 {{site.data.keyword.iot_short_notm}}을 사용하면 IoT 디바이스에서 블록체인 트랜잭션에 데이터를 제공할 수 있으므로, 블록체인의 불변 원장에 데이터를 저장하고 스마트 계약 비즈니스 규칙에서 사용할 수 있습니다. {{site.data.keyword.iot_short_notm}}에서 블록체인의 스마트 계약에 필요한 데이터 형식에 디바이스 데이터를 맵핑한 다음 블록체인 원장에 저장하도록 블록체인 패브릭에 전달합니다.

### 블록체인에 지원되는 오퍼레이션
- 스마트 계약을 디바이스 이벤트로 업데이트하도록 트리거합니다.
- 스마트 계약 비즈니스 로직을 실행하여 원장 상태를 디바이스 이벤트 데이터로 업데이트합니다.
- 모니터링 UI로 블록체인, 트랜잭션 및 원장 상태를 모니터합니다.

### 블록체인 구성

{{site.data.keyword.iot_short_notm}} 블록체인 통합은 {{site.data.keyword.iot_short_notm}}에서 기본적으로 활성화되지 않는 서비스 오퍼링입니다. 조직에서 기능을 활성화하려면 다음 단계를 완료하십시오. 
 1. {{site.data.keyword.iot_short_notm}} 대시보드에서 **확장기능**을 선택하십시오.
 2. **확장기능** 페이지에서 **확장기능 추가**를 클릭하십시오.
 3. 블록체인 확장기능 옆의 **추가**를 클릭하십시오. 
 4. 블록체인 타일에서 **설정**을 클릭하십시오. 
 3. **블록체인 활성화** 섹션에서 **자세히 보기** 링크를 클릭하여 [IoT 블록체인 서비스 오퍼링 페이지 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.ibm.com/internet-of-things/iot-news/announcements/private-blockchain/){: new_window}로 이동하십시오. 
 4. **블록체인 프로젝트 시작**을 클릭하여 *IoT 및 블록체인의 가능성 탐색* 양식을 채우고 제출하십시오.   
 5. 요청이 승인되면 사용자 조직의 블록체인 통합을 사용할 수 있도록 IBM이 사용자에게 연락합니다. 
 6. 조직의 {{site.data.keyword.iot_short_notm}} 대시보드로 돌아와서 [{{site.data.keyword.iot_short_notm}} 블록체인 통합](../../bl_blockchain_integration.html)의 단계에 따라 설정을 완료하십시오. 

<!-- ## The Weather Company
{: #weathercompany}

The Weather Company extension combines weather data with your existing {{site.data.keyword.iot_short_notm}} devices. Weather data from The Weather Company appears in the device details view if an update location request has been made by using the API, or if the device has already set its location by using a device management message.

**Note:** Only managed devices can set their own locations. All unmanaged devices must have their locations set manually by using the API. For more information on setting a device location, see [Update Location requests](../../devices/device_mgmt/index.html#update-location).

### REST APIs for The Weather Company
To access the REST API for The Weather Company, see the
Device Location Weather section in the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} documentation.

### Weather Data

To view the weather data retrieved for a device location, find the device in the **Devices** pane and click it. In the detailed device view scroll down to the **Extensions** section. The following weather data is listed:

- Current weather.
- Current temperature.
- Predicted maximum and minimum temperature.
- Relative humidity.
- Pressure.
- Visibility.
- Wind speed.
- Wind direction.
- Latitude.
- Longitude.
-->

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->

## 이메일
{: #email}

이메일 초대를 사용하여 사용자를 {{site.data.keyword.iot_short_notm}}에 추가할 수 있습니다. 자세한 정보는 [사용자 액세스 관리](../../add_users.html)를 참조하십시오. 

이메일 초대 기능을 사용하려면, 이메일 확장기능이 SendGrid 온라인 서비스 또는 SMTP(Simple Mail Transfer Protocol) 서비스를 사용하도록 구성되어 있어야 합니다. 이메일 확장기능은 SendGrid {{site.data.keyword.Bluemix_notm}} 애플리케이션을 사용할 수도 있습니다. 

### SendGrid 온라인 서비스

SendGrid 온라인 서비스와 함께 사용하도록 이메일 확장기능을 구성하려면 다음 단계를 따르십시오. 

1. SendGrid 온라인 계정에서 인증 API 키를 검색하십시오. 
2. {{site.data.keyword.iot_short_notm}} 대시보드의 탐색줄에서 **확장기능**을 클릭하십시오. 
3. **이메일** 섹션에서 **설정**을 클릭하십시오. 
4. **API 키가 있는 SendGrid**를 선택하십시오. 
5. 사이트 관리자의 이름과 이메일 주소 및 인증 API 키를 입력하십시오. 

### SMTP 서비스

SMTP 서비스와 함께 사용하도록 이메일 확장기능을 구성하려면 다음 단계를 따르십시오. 

1. {{site.data.keyword.iot_short_notm}} 대시보드의 탐색줄에서 **확장기능**을 클릭하십시오. 
2. **이메일** 섹션에서 **설정**을 클릭하십시오. 
3. **SMTP**를 선택하십시오. 
4. SMTP 서비스의 구성 세부사항을 입력하십시오. 

### SendGrid {{site.data.keyword.Bluemix_notm}} 애플리케이션

SendGrid {{site.data.keyword.Bluemix_notm}} 애플리케이션과 함께 사용하도록 이메일 확장기능을 구성하려면 다음 단계를 따르십시오. 

1. 더미 애플리케이션을 작성하고 SendGrid 서비스를 바인드하십시오.   
구성 신임 정보를 검색하기 위해 더미 앱에 SendGrid 서비스를 추가하고 바인드하십시오. 

 1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 **서비스 작성**을 클릭하십시오. 
 2. 카탈로그에서 SendGrid 서비스를 선택하고 **작성**을 클릭하십시오. 
 3. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.sdk4nodefull}} 애플리케이션을 추가하십시오.
 4. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.sdk4nodefull}} 애플리케이션을 클릭하고 **서비스 또는 API 바인드**를 클릭하십시오.
 5. SendGrid 서비스를 선택하고 **추가**를 클릭하십시오. 
 6. 이제 {{site.data.keyword.sdk4nodefull}} 애플리케이션을 다시 스테이징해야 합니다.
2. {{site.data.keyword.iot_short_notm}} 서비스 구성을 준비하십시오.   
{{site.data.keyword.iot_short_notm}} 대시보드를 사용하거나 {{site.data.keyword.iot_short_notm}} API를 사용하여 {{site.data.keyword.iot_short_notm}}을 구성할 수 있습니다.   
 1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.sdk4nodefull}} 애플리케이션을 클릭하십시오.
 2. 탐색줄에서 **환경 변수**를 클릭하십시오.
 3. 임시 텍스트 파일에 표시된 JSON을 복사하십시오.   
 JSON은 다음 형식이어야 합니다. 
```
{
  "name": "SendGridServiceName",
  "label": "user-provided",
  "credentials": {
    "password": "xxx",
    "hostname": "smtp.sendgrid.net",
    "username": "username"
  }
}
```
3. 구성 데이터를 {{site.data.keyword.iot_short_notm}} 조직에 추가하십시오. 
 1. {{site.data.keyword.iot_short_notm}} 대시보드를 여십시오.
 2. 탐색줄에서 **확장기능**을 클릭하십시오.
 3. **이메일** 아이콘 아래의 **설정**을 클릭하십시오. 
 4. **사용자 이름이 있는 SendGrid**를 선택하십시오. 
 5. 임시 텍스트 파일의 구성 데이터를 입력하십시오. 
 6. **완료**를 클릭하십시오.
