---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Push Notifications 패키지 사용
{: #openwhisk_catalog_pushnotifications}

`/whisk.system/pushnotifications` 패키지를 사용하면 푸시 서비스로 작업할 수 있습니다.

패키지에는 다음 조치와 피드가 포함됩니다. 

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | 패키지 | appId, appSecret  | 푸시 서비스에 대한 작업 |
| `/whisk.system/pushnotifications/sendMessage` | 조치 | text, url, deviceIds, platforms, tagNames, gcmPayload, gcmSound, gcmCollapseKey, gcmDelayWhileIdle, gcmPriority, gcmTimeToLive, gcmSync, gcmVisibility, gcmStyleType, gcmStyleTitle, gcmStyleUrl, gcmStyleText, gcmStyleLines, apnsBadge, apnsCategory, apnsIosActionKey, apnsPayload, apnsType, apnsSound, fireFoxTitle, fireFoxIconUrl, fireFoxTimeToLive, fireFoxPayload, chromeTitle, chromeIconUrl, chromeTimeToLive, chromePayload, chromeAppExtTitle, chromeAppExtCollapseKey, chromeAppExtDelayWhileIdle, chromeAppExtIconUrl, chromeAppExtTimeToLive, chromeAppExtPayload | 하나 이상의 지정된 디바이스에 푸시 알림 전송 |
| `/whisk.system/pushnotifications/webhook` | 피드 | events | 푸시 서비스에서 디바이스 활동(디바이스 등록, 등록 해제, 구독 또는 구독 해제)에 대한 트리거 이벤트 실행 |
`appId` 값과 `appSecret` 값을 사용하여 패키지 바인딩을 작성하도록 권장합니다. 이 방법을 사용하면 패키지에서 조치를 호출할 때마다 신임 정보를 지정할 필요가 없습니다.

## 푸시 패키지 바인딩 작성
{: #openwhisk_catalog_pushnotifications_create}

Push Notifications 패키지 바인딩을 작성하는 동안 다음 매개변수를 지정해야 합니다. 

-  `appId`: Bluemix 앱 GUID입니다.
-  `appSecret`: Bluemix 푸시 알림 서비스 appSecret입니다.

다음은 패키지 바인딩을 작성하는 예제입니다.

1. [Bluemix 대시보드](http://console.ng.bluemix.net)에서 Bluemix 애플리케이션을 작성하십시오.

2. Push Notifications 서비스를 초기화하고 서비스를 Bluemix 애플리케이션에 바인드하십시오.

3. [Push Notifications 애플리케이션](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)을 구성하십시오. 
  
  작성한 Bluemix 앱의 `App GUID` 및 `App Secret`을 기억해야 합니다.
  
4. `/whisk.system/pushnotifications`로 패키지 바인딩을 작성하십시오.
  
  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}
  
5. 패키지 바인딩이 있는지 확인하십시오.
  
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myPush private binding
  ```
  

## 푸시 알림 전송
{: #openwhisk_catalog_pushnotifications_send}

`/whisk.system/pushnotifications/sendMessage` 조치는 등록된 디바이스에 푸시 알림을 발송합니다. 매개변수는 다음과 같습니다.
- `text`: 사용자에게 표시할 알림 메시지입니다. 예: `-p text "Hi ,OpenWhisk send a notification"`.
- `url`: 경보와 함께 전송할 수 있는 선택적 URL입니다. 예: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds` 지정된 디바이스의 목록입니다. 예: `-p deviceIds ["deviceID1"]`.
- `platforms` 지정된 플랫폼의 디바이스에 알림을 전송합니다. Apple(iOS)의 'A' 디바이스 및 Google(Android)의 'G' 디바이스가 해당됩니다. 예: `-p platforms ["A"]`.
- `tagNames` 이 태그 중 하나로 등록한 디바이스에 알림을 전송합니다. 예: `-p tagNames "[\"tag1\"]" `.
- `gcmPayload`: 알림 메시지의 일부로 전송할 사용자 정의 JSON 페이로드입니다. 예: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: 알림이 디바이스에 도달하면 재생될 사운드 파일(디바이스에서 재생)입니다. 
- `gcmCollapseKey`: 이 매개변수는 메시지의 그룹을 식별합니다. 
- `gcmDelayWhileIdle`: 이 매개변수가 true로 설정된 경우 이는 디바이스가 활성이 될 때까\지 메시지를 보내지 않음을 표시합니다. 
- `gcmPriority`: 메시지의 우선순위를 설정합니다. 
- `gcmTimeToLive`: 이 매개변수는 디바이스가 오프라인인 경우 메시지가 GCM 스토리지에 보관되는 기간(초)을 지정합니다. 
- `gcmSync`: 디바이스 그룹 메시징을 통해 그룹의 모든 앱 인스턴스가 최신 메시징 상태를 반영할 수 있습니다.
- `gcmVisibility`: 개인용/공용 - 알림의 가시성이며, 보안 잠금 화면에 알림을 표시하는 방법과 시기에 영향을 줍니다.
- `gcmStyleType`: 펼칠 수 있는 알림 유형을 지정합니다. 가능한 값은 `bigtext_notification`, `picture_notification`, `inbox_notification`입니다.
- `gcmStyleTitle`: 알림 제목을 지정합니다. 알림을 펼치면 제목이 표시됩니다. 펼칠 수 있는 세 가지 알림 모두에 제목을 지정해야 합니다.
- `gcmStyleUrl`: 알림에 대한 그림을 확보해야 하는 URL입니다. picture_notification에 지정해야 합니다.
- `gcmStyleText`: bigtext_notification을 펼칠 때 표시해야 하는 큰 텍스트입니다. bigtext_notification에 지정해야 합니다.
- `gcmStyleLines`: inbox_notification을 위해 받은 편지함 스타일로 표시할 문자열 배열입니다. inbox_notification에 지정해야 합니다.
- `apnsBadge`: 애플리케이션 아이콘의 배지로 표시할 숫자입니다. 
- `apnsCategory`: 대화식 푸시 알림에 사용할 카테고리 ID입니다. 
- `apnsIosActionKey`: 조치 키의 제목입니다. 
- `apnsPayload`: 알림 메시지의 일부로 전송할 사용자 정의 JSON 페이로드입니다. 
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: 애플리케이션 번들에 있는 사운드 파일의 이름입니다. 이 파일의 소리가 경보로 재생됩니다.
- `fireFoxTitle`: WebPush 알림에 설정할 제목을 지정합니다.
- `fireFoxIconUrl`: WebPush 알림에 설정할 아이콘의 URL입니다.
- `fireFoxTimeToLive`: 이 매개변수는 디바이스가 오프라인인 경우 메시지를 GCM 스토리지에 보관해야 하는 시간(초)을 지정합니다.
- `fireFoxPayload`: 알림 메시지의 일부로 보낼 사용자 정의 JSON 페이로드입니다.
- `chromeTitle`: WebPush 알림에 설정할 제목을 지정합니다.
- `chromeIconUrl`: WebPush 알림에 설정할 아이콘의 URL입니다.
- `chromeTimeToLive`: 이 매개변수는 디바이스가 오프라인인 경우 메시지를 GCM 스토리지에 보관해야 하는 시간(초)을 지정합니다.
- `chromePayload`: 알림 메시지의 일부로 보낼 사용자 정의 JSON 페이로드입니다.
- `chromeAppExtTitle`: WebPush 알림에 설정할 제목을 지정합니다.
- `chromeAppExtCollapseKey`: 이 매개변수는 메시지 그룹을 식별합니다.
- `chromeAppExtDelayWhileIdle`: 이 매개변수가 true로 설정되면 디바이스가 활성화될 때까지 메시지가 전송되지 않음을 표시합니다.
- `chromeAppExtIconUrl`: WebPush 알림에 설정할 아이콘의 URL입니다.
- `chromeAppExtTimeToLive`: 이 매개변수는 디바이스가 오프라인인 경우 메시지를 GCM 스토리지에 보관해야 하는 시간(초)을 지정합니다.
- `chromeAppExtPayload`: 알림 메시지의 일부로 보낼 사용자 정의 JSON 페이로드입니다.

다음은 *pushnotification* 패키지의 푸시 알림을 보내는 예입니다.

- 이전에 작성한 패키지 바인딩에서 `sendMessage` 조치를 사용하여 푸시 알림을 보내십시오. `/myNamespace/myPush`를 패키지 이름으로 바꿔야 합니다.
  
  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}
  ```json
  {
    "result": {
  "pushResponse": 
      {
        "messageId":"11111H",
        "message":{
          "alert":"this is my message",
          "url":""
        },
        "settings":{
          "apns":{
            "sound":"default"
          },
          "gcm":{
            "sound":"default"
            },
          "target":{
            "deviceIds":["T1","T2"]
          }
        }
      }
    },
  "status": "success",
  "success": true
  }
  ```
  

## Push Notifications 서비스 활동에서 트리거 이벤트 실행
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook`에서는 지정된 애플리케이션에서 디바이스 등록/등록 해제 또는 구독/구독 해제와 같은 디바이스 활동이 있는 경우 트리거를 실행하도록 푸시 서비스를 구성합니다. 

매개변수는 다음과 같습니다.

- `appId:` Bluemix 앱 GUID입니다. 
- `appSecret:` Bluemix 푸시 알림 서비스 appSecret입니다. 
- `events:` 지원되는 이벤트는 `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`, `onUnsubscribe`입니다. 모든 이벤트에 대해 알림을 받으려면 와일드카드 문자 `*`를 사용하십시오.

다음은 Push Notifications 서비스 애플리케이션에 새 디바이스가 등록될 때마다 실행할 트리거를 작성하는 예입니다. 

1. appId와 appSecret을 사용하여 Push Notifications 서비스에 사용하도록 구성된 패키지 바인딩을 작성하십시오. 
  
  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}
  
2. `myPush/webhook` 피드를 사용하여 Push Notifications 서비스 `onDeviceRegister` 이벤트 유형의 트리거를 작성하십시오. 
  
  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}  
  
3. 새 디바이스를 등록할 때마다 메시지를 보내는 규칙을 작성해야 합니다. 이전 조치 및 트리거를 사용하여 새 규칙을 작성하십시오.
  
  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}
  
  `wsk activation poll`에서 결과를 확인하십시오.

  Bluemix 애플리케이션에 디바이스를 등록하십시오. 그러면 openWhisk [대시보드] (https://console.{Domain}/openwhisk/dashboard)에서 실행되는 `규칙`, `트리거` 및 `조치`를 볼 수 있습니다.

  조치가 푸시 알림을 보냅니다.
  
