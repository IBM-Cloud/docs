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


# 디바이스 개발자용 Node.js
{: #nodejs}

Node.js의 클라이언트 라이브러리와 샘플을 조정하여 {{site.data.keyword.iot_full}}에서 조직과 상호작용하는 디바이스 코드를 빌드하고 개발할 수 있습니다.
{:shortdesc}

Node.js를 사용하여 디바이스 디버깅을 시작하도록 제공된 예와 정보를 사용하십시오.

## Node.js 클라이언트 및 리소스 다운로드
{: #node.js_client_downloads}

{{site.data.keyword.iot_short_notm}}에 대한 Node.js 클라이언트 라이브러리 및 기타 사용 가능한 리소스에 액세스하려면 GitHub의 [iot-nodejs ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} 저장소로 이동하여 설치 지시사항을 완료하십시오. 


자세한 정보는 다음 리소스를 참조하십시오.

- GitHub의 [디바이스용 샘플 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window}
- NPM의 [ibmiotf ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.npmjs.com/package/ibmiotf){: new_window} 저장소. 

## 생성자
{: #constructor}

생성자는 디바이스 클라이언트 인스턴스를 빌드합니다. 다음 정의를 포함하는 구성 JSON을 승인합니다.

|정의 |설명  |
|:---|:---|
|`org` |조직 ID입니다. |
|`type`  |디바이스 유형입니다. 일반적으로, deviceType은 특정 태스크를 수행하는 디바이스의 그룹화입니다(예: "weatherballoon"). |
|`id`  |디바이스 ID입니다. 일반적으로, 제공된 디바이스 유형의 경우 deviceId는 해당 디바이스의 고유 ID입니다(예: 일련 번호 또는 MAC 주소). |
|`auth-method`   |사용할 인증 메소드입니다. 현재 지원되는 값은 `token`입니다.|
|`auth-token`   |디바이스를 Watson IoT Platform에 안전하게 연결하기 위한 인증 토큰입니다. 이 필드는 `auth-method`가 `token`인 경우 필수입니다.|

**참고:** Quickstart 서비스를 사용하려는 경우 처음 세 개의 특성만 제출하면 됩니다.

```
    var iotf = require("ibmiotf");
    var config = {
		"org" : "organization",
		"id" : "deviceId",
		"type" : "deviceType",
		"auth-method" : "token",
		"auth-token" : "authToken"
    };


    var deviceClient = new iotf.IotfDevice(config);
```

### 구성 파일 사용

다음 예에 표시된 대로 구성을 직접 전달하지 않고 JSON 구성 파일을 사용하여 필수 구성 특성을 제공할 수 있습니다.


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
`device.json` 구성 파일의 형식은 다음과 같아야 합니다.

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## {{site.data.keyword.iot_short_notm}}에 연결
{: #connecting_to_iotp}

`connect` 함수를 호출하여 {{site.data.keyword.iot_short_notm}}에 연결할 수 있습니다.

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

	deviceClient.connect();

	deviceClient.on('connect', function(){
		var i=0;
		console.log("connected");
		setInterval(function function_name () {
			i++;
			deviceClient.publish('myevt', 'json', '{"value":'+i+'}', 2);
		},2000);
	});

```

{{site.data.keyword.iot_short_notm}} 서비스에 정상적으로 연결하고 나면 디바이스 클라이언트에서 `connect` 이벤트를 보냅니다. 이 프로세스는 모든 디바이스 로직을 이 콜백 함수 내에서 구현할 수 있다는 의미입니다.

디바이스 클라이언트에서 연결을 유실하면 자동으로 다시 연결하려 합니다. 다시 연결에 성공하면 클라이언트가 `reconnect` 이벤트를 전송합니다. 

## 로깅
{: #logging}

기본적으로 *경고* 유형의 모든 로그 이벤트가 기록됩니다. 로깅 레벨를 늘리거나 줄이려면 log.setLevel 함수를 사용하십시오. 지원되는 로그 레벨은 다음과 같습니다.
- 추적
- 디버그
- 정보
- 경고
- 오류

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

```


## 이벤트 공개
{: #publishing_events}

이벤트는 디바이스가 {{site.data.keyword.iot_short_notm}}에 데이터를 공개하는 데 사용하는 메커니즘입니다. 디바이스에서 이벤트의 컨텐츠를 제어하고 전송하는 각 이벤트의 이름을 지정합니다.

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신할 때 수신된 이벤트의 신임 정보는 전송 중인 디바이스를 식별하며, 이는 디바이스가 다른 디바이스로 위장할 수 없음을 의미합니다. 

공개되는 이벤트의 서비스 품질(QoS) 레벨을 늘릴 수 있습니다. QoS 레벨이 `0`보다 큰 이벤트는 추가 확인 수신 정보가 포함되어 있으므로 공개하는 데 시간이 오래 걸립니다.

**참고:** Quickstart 플로우 모드에서는 QoS 레벨 `0`만 지원합니다.


다음 특성을 사용하여 이벤트를 공개할 수 있습니다.

|특성 |설명 |
|:---|:---|
|`eventType`  | 공개할 이벤트 유형(예: 상태 또는 GPS)입니다. |  
|`eventFormat`  |이벤트 형식(예: JSON)입니다. |
|`data`  | 버퍼 문자열이어야 하는 이벤트의 페이로드입니다. |
|`QoS`  | 공개 이벤트의 MQTT 서비스 품질입니다. 지원되는 값은 0, 1 및 2입니다.|


```
    var deviceClient = new Client.IotfDevice(config);

    deviceClient.connect();

    deviceClient.on("connect", function () {
       //publish an event at the default quality of service
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

       //publish an event at the user-defined quality of service
       var myQosLevel=2
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);
  });

```

## 명령 처리
{: #handling_commands}

디바이스 클라이언트가 연결되면 이 디바이스에 대한 명령을 자동으로 구독합니다. 특정 명령을 처리하려면 명령 콜백 함수를 등록해야 합니다. 명령을 수신하면 디바이스 클라이언트에서 명령 콜백 함수를 호출합니다. 콜백 함수의 특성은 다음과 같습니다. 

|특성 |설명 |
|:---|:---|
|`commandName`  | 호출된 명령의 이름을 지정하는 문자열입니다. |  
|`format`  | 이벤트 형식을 지정하는 문자열입니다(예: JSON). |
|`payload`  | 명령 페이로드의 데이터를 지정하는 문자열입니다.  |
|`topic`  | 디바이스로 공개할 때 주제 문자열에는 디바이스 유형이나 디바이스 ID가 포함되지 않습니다. 이러한 정보는 클라이언트 ID에서 가져옵니다. 예를 들어 `iot-2/evt/event_id/fmt/format_string`입니다. 디바이스 대신에 애플리케이션 또는 게이트웨이로서 공개 중인 경우, 주제에는 디바이스 유형 및 디바이스 ID가 포함되어야 합니다. 예를 들어 `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`입니다.|


```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("command", function (commandName,format,payload,topic) {
		if(commandName === "blink") {
			console.log(blink);
			//function to be performed for this command
			blink(payload);
		} else {
			console.log("Command not supported.. " + commandName);
		}
	});

```

## 오류 처리
{: #handling_errors}

디바이스 클라이언트에 오류가 발생하면 *오류* 이벤트를 보냅니다.

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("error", function (err) {
		console.log("Error : "+err);
	});
	....

```

## 클라이언트 연결 끊기
{: #disconnecting_client}

다음 샘플에서는 클라이언트의 연결을 끊고 연결을 해제하는 방법을 보여줍니다.

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	client.on("connect", function () {
		//publish an event at the default quality of service
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

		//publishing event at the user-defined quality of service
		var myQosLevel=2
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);

		//disconnect the client
		client.disconnect();
	});

	....
```
