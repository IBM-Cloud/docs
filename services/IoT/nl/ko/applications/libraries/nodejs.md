---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-07-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# 애플리케이션 개발자용 Node.js
{: #nodejs}

마지막 업데이트 날짜: 2016년 7월 29일
{: .last-updated}

Node.js의 클라이언트 라이브러리 및 샘플을 조정하여 {{site.data.keyword.iot_full}}에서 조직과 상호작용하는 애플리케이션을 빌드하고 사용자 정의할 수 있습니다.
{:shortdesc}

제공된 정보와 예제를 사용하면 Node.js를 사용한 애플리케이션 개발을 시작할 수 있습니다. 

## Node.js 클라이언트 및 자원 다운로드
{: #nodejs_client_download}

{{site.data.keyword.iot_short_notm}}의 Node.js 클라이언트 라이브러리 및 기타 사용 가능한 자원에 액세스하려면 GitHub의 [iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs) 저장소로 이동하여 설치 지시사항을 완료하십시오. 


자세한 정보는 다음 자원을 참조하십시오. 
- GitHub의 [애플리케이션 샘플](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples). 
- NPM의 [ibmiotf](https://www.npmjs.com/package/ibmiotf). 
- 이 문서의 [참조](#reference_nodejs) 섹션. 


## 생성자
{: #constructor}

생성자는 애플리케이션 클라이언트 인스턴스를 빌드하며 다음 특성이 포함된 JSON 구성 파일을 허용합니다. 

| 특성     |설명     |
|----------------|----------------|
|`org` |조직 ID입니다. 이는 필수 값입니다. |
|`id`  |조직 내에서 애플리케이션의 고유 ID입니다. |
|`auth-key`   |애플리케이션을 Watson IoT Platform에 안전하게 연결하기 위한 API 키입니다. |
|`auth-token`   |디바이스를 Watson IoT Platform에 안전하게 연결하기 위한 API 키 토큰입니다. |
|`type`  |구독의 유형입니다. 공유 구독을 사용하려면 `shared`를 지정하십시오. |


Quickstart를 사용하려면 처음 두 특성만 필요합니다. 

```
  var Client = require("ibmiotf");
	var appClientConfig = {
		"org" : orgId,
		"id" : appId,
		"auth-key" : apiKey,
		"auth-token" : apiToken
	}

	var appClient = new Client.IotfApplication(appClientConfig);
```


### 구성 파일 사용


JSON 특성을 직접 전달하는 대신, 다음 코드 샘플에서 개략적으로 설명한 구성 파일을 사용할 수도 있습니다. 

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

JSON 구성 파일의 형식이 다음과 같은지 확인하십시오. 

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## {{site.data.keyword.iot_short_notm}}에 연결
{: #connecting_to_iotp}

{{site.data.keyword.iot_short_notm}}에 연결하려면 다음과 같이 *연결* 요청을 제출하십시오. 

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Add your code here
	});
```

{{site.data.keyword.iot_short_notm}} 서비스에 연결이 성공한 이후, 애플리케이션 클라이언트는 이 콜백 함수 내에서 로직이 구현될 수 있도록 `connect` 이벤트를 전송합니다. 



연결이 끊어지면 애플리케이션 클라이언트가 자동으로 다시 연결을 시도합니다. 다시 연결에 성공하면 클라이언트가 `reconnect` 이벤트를 전송합니다. 



## 로깅
{: #logging}

기본적으로 `warn` 유형의 로그 이벤트만 기록됩니다. 로깅 레벨을 올리거나 내리려면 `log.setLevel` 함수를 사용하십시오. 지원되는 로그 레벨은 다음과 같습니다. 
- 추적
- 디버그
- 정보
- 경고
- 오류

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## 공유 구독
{: #shared_subscriptions}

공유 구독 기능을 사용하여 애플리케이션의 여러 인스턴스 간에 메시지를 로드 밸런싱하는 확장 가능한 애플리케이션을 빌드할 수 있습니다. 로드 밸런싱을 사용하려면 다음 예제에 표시된 대로 `type` 필드를 `shared`로 설정하십시오. 

```

	var appClientConfig = {
	  org: 'xxxxx',
	  id: 'myapp',
	  "auth-key": 'a-xxxxxx-xxxxxxxxx',
	  "auth-token": 'xxxxx!xxxxxxxx',
	  "type" : "shared" // make this connection as shared subscription
	};
	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## 오류 처리
{: #handling_errors}

애플리케이션 클라이언트에서 오류가 발생하면 `error` 이벤트가 생성됩니다. 

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
	appClient.on("error", function (err) {
		console.log("Error : "+err);
	});
```

## 디바이스 이벤트 구독
{: #subscribing_device_events}

이벤트는 디바이스가 {{site.data.keyword.iot_short_notm}} 인스턴스에 데이터를 공개하는 메커니즘입니다. 디바이스에서 이벤트의 컨텐츠를 제어하고 전송하는 각 이벤트의 이름을 지정합니다. 

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신할 때 수신된 이벤트의 신임 정보는 전송 중인 디바이스를 식별하며, 이는 디바이스가 다른 디바이스로 위장할 수 없음을 의미합니다. 


기본적으로, 애플리케이션은 연결된 모든 디바이스의 모든 이벤트를 구독합니다. 디바이스 유형, 디바이스 ID, 이벤트 및 메시지 형식 매개변수를 사용하면 구독의 범위를 제어할 수 있습니다. 다음 코드 샘플은 이러한 매개변수를 사용하여 구독의 범위를 정의할 수 있는 방법을 표시합니다. 

### 모든 디바이스의 모든 이벤트 구독


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### 특정 유형인 모든 디바이스의 모든 이벤트 구독

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### 모든 디바이스의 특정 이벤트 구독


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### 둘 이상의 서로 다른 디바이스의 특정 이벤트 구독

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### JSON 형식으로 공개된 모든 이벤트 구독


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**참고**: 하나의 클라이언트는 여러 구독을 지원할 수 있습니다. 

### 디바이스에서 이벤트 처리


구독으로 수신된 이벤트를 처리하려면 디바이스 이벤트 콜백 메소드를 구현하십시오. {{site.data.keyword.iot_short_notm}} 애플리케이션 클라이언트는 `deviceEvent` 이벤트를 전송합니다. 이 함수의 특성은 다음과 같습니다. 

- deviceType
- deviceId
- eventType
- format
- payload
- topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
	appClient.on("deviceEvent", function (deviceType, deviceId, eventType, format, payload) {

		console.log("Device Event from :: "+deviceType+" : "+deviceId+" of event "+eventType+" with payload : "+payload);

	});
```


## 디바이스 상태 구독
{: #subscribing_device_status}

기본적으로, 디바이스 상태를 구독하면 연결된 모든 디바이스에 대해 상태 업데이트가 수신됩니다. 유형 및 ID 매개변수를 사용하면 구독의 범위를 제어할 수 있습니다. 하나의 클라이언트는 여러 구독을 지원할 수 있습니다. 

### 모든 디바이스의 상태 업데이트 구독

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### 특정 유형인 모든 디바이스의 상태 업데이트 구독


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### 두 개의 서로 다른 디바이스의 상태 업데이트 구독

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### 디바이스에서 상태 업데이트 처리

구독으로 수신된 상태 업데이트를 처리하려면 디바이스 상태 콜백 메소드를 구현하십시오. {{site.data.keyword.iot_short_notm}} 애플리케이션 클라이언트는 `deviceStatus` 이벤트를 전송합니다. 이 함수의 특성은 다음과 같습니다. 

-   deviceType
-   deviceId
-   payload
-   topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
	appClient.on("deviceStatus", function (deviceType, deviceId, payload, topic) {

		console.log("Device status from :: "+deviceType+" : "+deviceId+" with payload : "+payload);

	});
```


## 디바이스에서 이벤트 공개
{: #publishing_device_events}


애플리케이션은 디바이스에서 가져온 것처럼 이벤트를 공개할 수 있습니다. 이 함수에서는 다음 특성이 필요합니다. 

-   deviceType
-   deviceId
-   eventType
-   format
-   data


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50};
		myData = JSON.stringify(myData);
		appClient.publishDeviceEvent("myDeviceType","device01", "myEvent", "json", myData);

	});
```


## 디바이스에 명령 공개
{: #publishing_commands_devices}

애플리케이션은 연결된 디바이스에 대한 명령을 공개할 수 있습니다.이 함수에서는 다음 특성이 필요합니다. 

-   deviceType
-   deviceId
-   eventType
-   format
-   data

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10};
		myData = JSON.stringify(myData);
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

	});
```


## 클라이언트 연결 끊기
{: #disconnect_client}

다음 샘플은 클라이언트와의 연결을 끊으며 연결도 역시 해제합니다. 

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## 참조
{: #reference_nodejs}

다음 표에는 이 Node.js 문서에서 설명한 함수에서 사용되는 매개변수가 설명되어 있습니다. 

|매개변수|데이터 유형|설명|
|:---|:---|
|`deviceType`|문자열|디바이스 유형입니다. 일반적으로, deviceType은 특정 태스크를 수행하는 디바이스의 그룹화입니다(예: "weatherballoon"). |
|`deviceId`|문자열|디바이스의 ID입니다. 일반적으로, 제공된 디바이스 유형의 경우 deviceId는 해당 디바이스의 고유 ID입니다(예: 일련 번호 또는 MAC 주소). |
|`eventType`|문자열|특정 이벤트의 그룹입니다(예: "상태", "경고" 및 "데이터"). |
|`format`|문자열|형식은 임의의 문자열일 수 있습니다(예: JSON).   |
|`data`|사전|메시지 페이로드의 데이터입니다. 최대 길이는 131072바이트입니다. |
|`payload`|문자열|메시지 페이로드의 데이터입니다. 최대 길이는 131072바이트입니다. |
|`topic`|문자열|디바이스로 공개할 때 주제 문자열에는 디바이스 유형이나 디바이스 ID가 포함되지 않습니다. 이러한 정보는 클라이언트 ID에서 가져옵니다. 예를 들어 `iot-2/evt/event_id/fmt/format_string`입니다.  디바이스 대신에 애플리케이션 또는 게이트웨이로서 공개 중인 경우, 주제에는 디바이스 유형 및 디바이스 ID가 포함되어야 합니다. 예를 들어 `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`입니다.|
