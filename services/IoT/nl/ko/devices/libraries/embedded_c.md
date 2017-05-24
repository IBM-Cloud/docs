---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 디바이스 개발자용 Embedded C
{: #embedded_c}

Embedded C를 사용하여 {{site.data.keyword.iot_full}}에서 조직과 상호작용하는 디바이스를 빌드하고 사용자 정의할 수 있습니다. 제공된 정보와 예제를 사용하면 Embedded C를 사용한 디바이스 개발을 시작할 수 있습니다.
{:shortdesc}

## Embedded C 클라이언트 및 리소스 다운로드
{: #embeddedc_client_download}

{{site.data.keyword.iot_short_notm}}에 대한 임베디드 C  클라이언트 라이브러리 및 샘플에 액세스하려면, GitHub의 [iotf-embeddedc ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-messaging/iotf-embeddedc){: new_window} 저장소로 이동하여 설치 지시사항을 완료하십시오. 


## 종속 항목
{: #dependencies}

|종속 항목 |설명|
|:---|:---|
|[Eclipse Paho 임베디드 C 라이브러리 ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git){: new_window} |MQTT C 클라이언트 라이브러리를 제공합니다. 자세한 정보는 [MQTT 클라이언트 패키지 -  임베디드 디바이스용 C ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}을 참조하십시오. |


## 설치
{: #installation}

Embedded C의 {{site.data.keyword.iot_short_notm}} 클라이언트 라이브러리를 설치하려면 다음 지시사항을 완료하십시오. 

1. 라이브러리의 최신 버전을 설치하려면 명령행에서 다음 코드를 입력하십시오. 
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. Paho 라이브러리 .tar 파일을 *lib* 디렉토리에 복사하십시오. 
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. 라이브러리 파일 추출
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
다운로드된 클라이언트의 파일 구조는 다음과 같습니다.

```
 |-lib - contains all the dependent files
 |-samples - contains the helloWorld and sampleDevice samples
   |-sampleDevice.c - sample device implementation
   |-helloworld.c - quickstart application
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c - Main client file
 |-iotfclient.h - Header file for the client
```

## 클라이언트 라이브러리 초기화
{: #initialize_client_library}

클라이언트 라이브러리가 다운로드된 후에는 이를 초기화하고 {{site.data.keyword.iot_short_notm}}에 연결해야 합니다. 매개변수를 전달하거나 구성 파일을 사용하여 Embedded C의 {{site.data.keyword.iot_short_notm}} 클라이언트 라이브러리를 초기화할 수 있습니다. 

### 매개변수 전달

`initialize` 함수는 다음 매개변수를 사용하여 {{site.data.keyword.iot_short_notm}} 서비스에 연결합니다. 

|정의 |설명 |
|:---|:---|
|`client`|*iotfclient*에 대한 포인터입니다. |
|`org`|조직 ID입니다. |
|`type` |디바이스 유형입니다. |
|`id` |디바이스 ID입니다. |
|`auth-method` |사용할 인증 메소드입니다. 현재 지원되는 값은 `token`입니다. |
|`auth-token`|디바이스를 Watson IoT Platform에 안전하게 연결하기 위한 인증 토큰입니다. |


```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	//quickstart
	rc = initialize(&client,"quickstart","iotsample","001122334455",NULL,NULL);
	//registered
	rc = initialize(&client,"org","type","id","auth-method","auth-token");
	....
```

### 구성 파일 사용

구성 파일을 사용하여 Embedded C 클라이언트 라이브러리를 초기화할 수도 있습니다. `initialize_configfile` 함수는 구성 파일 경로를 매개변수로서 취합니다. 

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

구성 파일은 다음 형식을 사용해야 합니다. 

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## 서비스에 연결
{: #connecting_service}

{{site.data.keyword.iot_short_notm}} Embedded C 클라이언트 라이브러리가 초기화되면 `connectiotf` 함수를 호출하여 {{site.data.keyword.iot_short_notm}}에 연결할 수 있습니다. 

```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	char *configFilePath = "./device.cfg";

	rc = initialize_configfile(&client, configFilePath);

	if(rc != SUCCESS){
		printf("initialize failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}

	rc = connectiotf(&client);

	if(rc != SUCCESS){
		printf("Connection failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}
	....
```

## 명령 처리
{: #handling_commands}

디바이스 클라이언트가 연결되면 이 디바이스에 대한 명령을 자동으로 구독합니다. 특정 명령을 처리하려면 `setCommandHandler` 함수를 호출하여 명령 콜백 함수를 등록해야 합니다. 콜백 함수의 특성은 다음과 같습니다. 

|특성 |설명|
|:---|:---|
|`commandName`  |호출된 명령의 이름입니다.  |  
|`format`  |이벤트의 형식입니다. 형식은 임의의 문자열일 수 있습니다(예: JSON). |
|`payload`  |명령 페이로드의 데이터입니다. 최대 길이는 131072바이트입니다.  |


```
	#include "iotfclient.h"

	void myCallback (char* commandName, char* format, void* payload)
	{
	printf("The command received :: %s\n", commandName);
	printf("format : %s\n", format);
	printf("Payload is : %s\n", (char *)payload);
	}
	...
	...
	char *filePath = "./device.cfg";
	rc = connectiotfConfig(filePath);
	setCommandHandler(myCallback);

	yield(1000);
	....

```
**참고:** `yield()` 함수는 디바이스가 Watson IoT Platform에서 명령을 수신하고 연결을 활성으로 유지할 수 있도록 합니다. keepAlive 간격으로 지정된 시간 범위 내에 `yield()` 함수가 호출되지 않으면 플랫폼에서 전송된 명령을 디바이스가 수신하지 않습니다. `yield()` 함수에 지정된 값은 제어가 애플리케이션으로 리턴되기 전에 소켓에서 데이터를 읽을 수 있는 기간(밀리초)을 지정합니다.

## 이벤트 공개
{: #publishing_events}

다음 특성을 사용하여 이벤트를 공개할 수 있습니다.

|특성 |설명|
|:---|:---|
|eventType  |공개되는 이벤트의 유형입니다(예: 상태 또는 gps). |  
|eventFormat  |형식은 임의의 문자열일 수 있습니다(예: `json`).  |
|data  |페이로드의 데이터입니다. 최대 길이는 131072바이트입니다.  |
|QoS  |공개 이벤트의 서비스 품질(QoS) 레벨입니다. 지원되는 값은 `0`, `1`, `2`입니다. |


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## 클라이언트 연결 끊기
{: #disconnect_client}

클라이언트의 연결을 끊고 연결을 해제하려면 다음 코드 스니펫을 실행하십시오. 

```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", payload , QOS0);
	...
	rc = disconnect();
	....
```

## 샘플
{: #samples}

샘플 디바이스 및 애플리케이션 코드는 [GitHub ![외부 링크 아이콘](../../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples){: new_window}에 제공됩니다. 
