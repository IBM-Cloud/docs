---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-08-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 디바이스 개발자용 C#
{: #c_sharp}

C#을 사용하여 {{site.data.keyword.iot_full}}에서 조직과 상호작용하는 디바이스를 빌드하고 사용자 정의할 수 있습니다. 제공된 정보와 예제를 사용하면 C#을 사용한 디바이스 개발을 시작할 수 있습니다.
{:shortdesc}

## C# 클라이언트 및 자원 다운로드
{: #csharp_client_download}

{{site.data.keyword.iot_short_notm}}의 C# 클라이언트 및 자원에 액세스하려면 GitHub의 [iot-csharp](https://github.com/ibm-watson-iot/iot-csharp) 저장소로 이동하여 설치 지시사항을 완료하십시오. 


## 생성자
{: #constructor}

생성자는 클라이언트 인스턴스를 빌드하며 다음 정의가 포함된 인수를 허용합니다. 

|정의 |설명 |
|:---|:---|
|`orgId`|조직 ID입니다. |
|`deviceType`|디바이스 유형입니다. |
|`deviceId` |디바이스 ID입니다. |
|`auth-method`   |사용할 인증 메소드입니다. 현재 지원되는 값은 `token`입니다. |
|`auth-token`   |디바이스를 Watson IoT Platform에 안전하게 연결하기 위한 인증 토큰입니다. |


`deviceId` 및 `deviceType`이 유일하게 제공되는 인수인 경우, 클라이언트는 {{site.data.keyword.iot_short_notm}} Quickstart 서비스에 미등록 디바이스로 연결합니다. 인수 목록은 클라이언트가 {{site.data.keyword.iot_short_notm}} 모듈에 연결하는 방법을 정의합니다. 


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## 이벤트 공개
{: #publishing-events}

디바이스는 이벤트를 사용하여 데이터를 {{site.data.keyword.iot_short_notm}} 인스턴스에 공개합니다. 디바이스는 이벤트의 컨텐츠를 제어하며 전송 중인 각 이벤트에 대해 이름을 지정합니다. 

{{site.data.keyword.iot_short_notm}} 인스턴스에서 이벤트를 수신할 때 수신 중인 이벤트의 신임 정보는 전송 중인 디바이스를 식별하며, 이는 디바이스가 다른 디바이스로 위장할 수 없음을 의미합니다. 

이벤트는 MQTT 프로토콜에서 정의하는 세 [서비스 품질(QoS) 레벨](../mqtt.html#managed-devices) 중 임의의 레벨에서 공개될 수 있습니다. 기본적으로, 이벤트는 QoS 0에서 공개됩니다. 


## 기본 서비스 품질(QoS) 레벨을 사용하여 이벤트 공개
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## 사용자 정의된 서비스 품질(QoS) 레벨을 사용하여 이벤트 공개
{: #publish_event_user_qos}

`0`보다 큰 MQTT QoS 레벨에서 공개된 이벤트에는 추가 수신 확인 정보가 포함되며, QoS 레벨이 `0`인 이벤트보다 공개하는 데 더 오랜 시간이 걸릴 수 있습니다. 


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## 명령 처리
{: #handling_commands}

디바이스 클라이언트가 연결된 경우, 이는 이 디바이스에 대한 명령을 자동으로 구독합니다. 특정 명령을 처리하려면 다음 예제에서 표시된 대로 명령 콜백 메소드를 등록해야 합니다. 

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
다음 표에는 commandCallback 메소드의 매개변수가 설명되어 있습니다.

|매개변수|데이터 유형|설명|
|:---|:---|
|`cmdName`|문자열|명령을 식별합니다.  |
|`cmdFormat`|문자열|형식은 임의의 문자열일 수 있습니다(예: JSON). |
|`cmdData`|사전|페이로드의 데이터입니다. 최대 길이는 131072바이트입니다. |
