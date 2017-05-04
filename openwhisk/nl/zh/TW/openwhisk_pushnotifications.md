---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Push Notifications 套件
{: #openwhisk_catalog_pushnotifications}

`/whisk.system/pushnotifications` 套件可讓您使用 Push 服務。

該套件包含下列動作及資訊來源：

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | 套件 | appId、appSecret  | 使用 Push 服務 |
| `/whisk.system/pushnotifications/sendMessage` | 動作 | text、url、deviceIds、platforms、tagNames、gcmPayload、gcmSound、gcmCollapseKey、gcmDelayWhileIdle、gcmPriority、gcmTimeToLive、gcmSync、gcmVisibility、gcmStyleType、gcmStyleTitle、gcmStyleUrl、gcmStyleText、gcmStyleLines、apnsBadge、apnsCategory、apnsIosActionKey、apnsPayload、apnsType、apnsSound、fireFoxTitle、fireFoxIconUrl、fireFoxTimeToLive、fireFoxPayload、chromeTitle、chromeIconUrl、chromeTimeToLive、chromePayload、chromeAppExtTitle、chromeAppExtCollapseKey、chromeAppExtDelayWhileIdle、chromeAppExtIconUrl、chromeAppExtTimeToLive、chromeAppExtPayload | 將推送通知傳送至一個以上的指定裝置 |
| `/whisk.system/pushnotifications/webhook` | 資訊來源 | 事件 | 在 Push 服務上產生裝置活動（裝置登錄、取消註冊、訂閱或取消訂閱）時發動觸發程式事件 |
建議使用 `appId` 及 `appSecret` 值來建立套件連結。如此，您就不需要每次在呼叫套件中的動作時都指定這些認證。

## 建立 Push 套件連結
{: #openwhisk_catalog_pushnotifications_create}

建立 Push Notifications 套件連結時，您必須指定下列參數：

-  `appId`：Bluemix 應用程式 GUID。
-  `appSecret`：Bluemix 推送通知服務 appSecret。

下列範例說明如何建立套件連結。

1. 在 [Bluemix 儀表板](http://console.ng.bluemix.net)中建立 Bluemix 應用程式。

2. 起始設定「推送通知服務」，並將該服務連結至 Bluemix 應用程式。

3. 配置 [Push Notification 應用程式](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)。
  
  請務必記住您建立之 Bluemix 應用程式的 `App GUID` 和 `App Secret`。
  
4. 建立與 `/whisk.system/pushnotifications` 連結的套件。
  
  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}
  
5. 驗證套件連結已存在。
  
  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myPush private binding
  ```
  

## 傳送推送通知
{: #openwhisk_catalog_pushnotifications_send}

`/whisk.system/pushnotifications/sendMessage` 動作會將推送通知傳送至已登錄的裝置。參數如下所示：
- `text`：要對使用者顯示的通知訊息。例如：`-p text "Hi ,OpenWhisk send a notification"`。
- `url` - 可隨著警示一起傳送的選用性 URL。例如：`-p url "https:\\www.w3.ibm.com"`。
- `deviceIds` 所指定裝置的清單。例如：`-p deviceIds ["deviceID1"]`。
- `platforms` 將通知傳送至指定平台的裝置。'A' 表示 Apple (iOS) 裝置，而 'G' 表示 google (Android) 裝置。例如 `-p platforms ["A"]`。
- `tagNames` 將通知傳送至已訂閱其中任何標籤的裝置。例如 `-p tagNames "[\"tag1\"]" `。
- `gcmPayload`：會放在通知訊息中一起傳送的自訂 JSON 有效負載。例如：`-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`：當通知到達裝置時，將會嘗試播放的音效檔（在裝置上）。
- `gcmCollapseKey`：此參數可識別訊息的群組。
- `gcmDelayWhileIdle`：當此參數設為 true 時，表示要等到裝置變成作用中時才會傳送訊息。
- `gcmPriority`：設定訊息的優先順序。
- `gcmTimeToLive`：此參數指定當裝置離線時，訊息保留在 GCM 儲存空間中多久（以秒為單位）。
- `gcmSync`：裝置群組傳訊可讓群組中的每個應用程式實例反映最新傳訊狀態。
- `gcmVisibility`：private/public - 此通知的可見性，其影響在安全鎖定的畫面上顯示通知的時間和方式。
- `gcmStyleType`：指定可擴充通知的類型。可能值為 `bigtext_notification`、`picture_notification` 或 `inbox_notification`。
- `gcmStyleTitle`：指定通知的標題。擴充通知時，會顯示標題。必須指定所有三個可擴充通知的標題。
- `gcmStyleUrl`：必須從中取得通知圖片的 URL。必須針對 picture_notification 指定。
- `gcmStyleText`：需要在擴充 bigtext_notification 時顯示的大型文字。必須針對 bigtext_notification 指定。
- `gcmStyleLines`：要顯示在 inbox_notification 的收件匣樣式中的字串陣列。必須針對 inbox_notification 指定。
- `apnsBadge`：要顯示成應用程式圖示徽章的數字。
- `apnsCategory`：要用於互動式推送通知的種類 ID。
- `apnsIosActionKey`：動作鍵的標題。
- `apnsPayload`：會放在通知訊息中一起傳送的自訂 JSON 有效負載。
- `apnsType`：['DEFAULT'、'MIXED'、'SILENT']。
- `apnsSound`：應用程式組合中的音效檔名稱。將會播放此檔案的音效作為警示。
- `fireFoxTitle`：指定要針對「WebPush 通知」設定的標題。
- `fireFoxIconUrl`：要針對「WebPush 通知」設定的圖示的 URL。
- `fireFoxTimeToLive`：此參數指定當裝置離線時，訊息應該保留在 GCM 儲存空間中多久（以秒為單位）。
- `fireFoxPayload`：會放在通知訊息中一起傳送的自訂 JSON 有效負載。
- `chromeTitle`：指定要針對「WebPush 通知」設定的標題。
- `chromeIconUrl`：要針對「WebPush 通知」設定的圖示的 URL。
- `chromeTimeToLive`：此參數指定當裝置離線時，訊息應該保留在 GCM 儲存空間中多久（以秒為單位）。
- `chromePayload`：會放在通知訊息中一起傳送的自訂 JSON 有效負載。
- `chromeAppExtTitle`：指定要針對「WebPush 通知」設定的標題。
- `chromeAppExtCollapseKey`：此參數可識別一組訊息。
- `chromeAppExtDelayWhileIdle`：當此參數設為 true 時，表示要等到裝置變成作用中時才會傳送訊息。
- `chromeAppExtIconUrl`：要針對「WebPush 通知」設定的圖示的 URL。
- `chromeAppExtTimeToLive`：此參數指定當裝置離線時，訊息應該保留在 GCM 儲存空間中多久（以秒為單位）。
- `chromeAppExtPayload`：會放在通知訊息中一起傳送的自訂 JSON 有效負載。

以下是從 *pushnotification* 套件傳送推送通知的範例。

- 使用您先前建立之套件連結中的 `sendMessage` 動作來傳送推送通知。請務必將 `/myNamespace/myPush` 取代成您的套件名稱。
  
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
  

## 發動 Push Notifications 服務活動的觸發程式事件
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` 將 Push 服務配置成：當指定的應用程式中有裝置活動（例如裝置登錄/取消登錄或訂閱/取消訂閱）時，即發動觸發程式

參數如下所示：

- `appId`：Bluemix 應用程式 GUID。
- `appSecret`：Bluemix 推送通知服務 appSecret。
- `events`：支援的事件為 `onDeviceRegister`、`onDeviceUnregister`、`onDeviceUpdate`、`onSubscribe`、`onUnsubscribe`。如果所有事件都要通知，請使用萬用字元 `*`。

下列範例說明如何建立在每次有新裝置向 Push Notifications 服務應用程式登錄時即發動的觸發程式。

1. 使用 appId 和 appSecret 來建立為 Push Notifications 服務所配置的套件連結。
  
  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}
  
2. 使用 `myPush/webhook` 資訊來源，為 Push Notifications 服務的 `onDeviceRegister` 事件類型建立觸發程式。
  
  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}  
  
3. 您可以建立一個每次登錄新裝置時即傳送訊息的規則。請使用前一個動作及觸發程式來建立新規則。
  
  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}
  
  檢查 `wsk activation poll` 中的結果。

  在 Bluemix 應用程式中登錄裝置，您可以看到已在 openWhisk [儀表板] (https://console.{Domain}/openwhisk/dashboard) 中執行 `rule`、`trigger` 及 `action`。

  動作將會傳送推送通知。
  
