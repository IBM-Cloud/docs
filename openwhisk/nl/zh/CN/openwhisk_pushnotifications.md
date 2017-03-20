---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Push Notifications 包
{: #openwhisk_catalog_pushnotifications}

`/whisk.system/pushnotifications` 包允许您使用推送服务。

此包中包含以下操作和订阅源：

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | 包 | appId、appSecret  | 使用推送服务 |
| `/whisk.system/pushnotifications/sendMessage` | 操作 | text、url、deviceIds、platforms、tagNames、gcmPayload、gcmSound、gcmCollapseKey、gcmDelayWhileIdle、gcmPriority、gcmTimeToLive、gcmSync、gcmVisibility、gcmStyleType、gcmStyleTitle、gcmStyleUrl、gcmStyleText、gcmStyleLines、apnsBadge、apnsCategory、apnsIosActionKey、apnsPayload、apnsType、apnsSound、fireFoxTitle、fireFoxIconUrl、fireFoxTimeToLive、fireFoxPayload、chromeTitle、chromeIconUrl、chromeTimeToLive、chromePayload、chromeAppExtTitle、chromeAppExtCollapseKey、chromeAppExtDelayWhileIdle、chromeAppExtIconUrl、chromeAppExtTimeToLive、chromeAppExtPayload | 将推送通知发送到一个或多个指定设备 |
| `/whisk.system/pushnotifications/webhook` | 订阅源 | 事件 | 在推送服务的设备活动（设备注册、取消注册、预订或取消预订）上触发触发器事件 |
建议使用 `appId` 和 `appSecret` 值创建包绑定。这样就无需在每次调用包中的操作时指定这些凭证。

## 创建 Push 包绑定
{: #openwhisk_catalog_pushnotifications_create}

创建 Push Notification 包绑定时，必须指定以下参数：

-  `appId`：Bluemix 应用程序 GUID。
-  `appSecret`：Bluemix 推送通知服务 appSecret。

下面是创建包绑定的示例。

1. 在 [Bluemix 仪表板](http://console.ng.bluemix.net)中创建 Bluemix 应用程序。

2. 初始化推送通知服务，并将该服务绑定到 Bluemix 应用程序

3. 配置 [Push Notification 应用程序](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)。
  
  确保记住您所创建的 Bluemix 应用程序的 `App GUID` 和 `App Secret`。
  
4. 创建与 `/whisk.system/pushnotifications` 的包绑定。
  
  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}
  
5. 验证包绑定是否存在。
  
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myPush private binding
  ```
  

## 发送推送通知
{: #openwhisk_catalog_pushnotifications_send}

`/whisk.system/pushnotifications/sendMessage` 操作会将推送通知发送到已注册的设备。参数如下所示：
- `text`：要向用户显示的通知消息。例如：`-p text "Hi ,OpenWhisk send a notification"`。
- `url`：可与警报一起发送的可选 URL。例如：`-p url "https:\\www.w3.ibm.com"`。
- `deviceIds`：指定设备的列表。例如：`-p deviceIds ["deviceID1"]`。
- `platforms`：向指定平台的设备发送通知。“A”表示 apple (iOS) 设备，“G”表示 google (Android) 设备。例如，`-p platforms ["A"]`。
- `tagNames`：向已预订其中任何标记的设备发送通知。例如，`-p tagNames "[\"tag1\"]"`。
- `gcmPayload`：作为通知消息一部分发送的定制 JSON 有效内容。例如：`-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`：通知到达设备时，要尝试播放的声音文件（在设备上）。
- `gcmCollapseKey`：此参数可识别一组消息
- `gcmDelayWhileIdle`：当此参数设置为 true 时，表示在设备变为活动之前，不会发送消息。
- `gcmPriority`：设置消息的优先级。
- `gcmTimeToLive`：此参数指定当设备脱机时，会在 GCM 存储器中保留消息的时间长度（秒）。
- `gcmSync`：设备组消息传递使得组中每一个应用程序实例都可反映出最新的消息传递状态。
- `gcmVisibility`：private/public - 此通知的可视性，这将影响在安全锁定屏幕上如何以及何时显示通知。
- `gcmStyleType`：指定可展开通知的类型。可能的值为 `bigtext_notification`、`picture_notification` 和 `inbox_notification`。
- `gcmStyleTitle`：指定通知的标题。标题在展开通知时显示。必须为所有三个可展开通知指定标题。
- `gcmStyleUrl`：必须从中获取通知图片的 URL。必须为 picture_notification 指定。
- `gcmStyleText`：需要在展开 bigtext_notification 时显示的大文本。必须为 bigtext_notification 指定。
- `gcmStyleLines`：要在 inbox_notification 的收件箱样式中显示的一组字符串。必须为 inbox_notification 指定。
- `apnsBadge`：显示为应用程序图标的角标的数字。
- `apnsCategory`：要用于交互式推送通知的类别标识。
- `apnsIosActionKey`：Action 键的标题。
- `apnsPayload`：作为通知消息一部分发送的定制 JSON 有效内容。
- `apnsType`：[“DEFAULT”、“MIXED”、“SILENT”]。
- `apnsSound`：应用程序捆绑软件中声音文件的名称。此文件的声音播放为警报。
- `fireFoxTitle`：指定要为 WebPush Notification 设置的标题。
- `fireFoxIconUrl`：要为 WebPush Notification 设置的图标的 URL。
- `fireFoxTimeToLive`：此参数指定当设备脱机时，应该在 GCM 存储器中保留消息的时间长度（秒）。
- `fireFoxPayload`：将作为通知消息的一部分发送的定制 JSON 有效内容。
- `chromeTitle`：指定要为 WebPush Notification 设置的标题。
- `chromeIconUrl`：要为 WebPush Notification 设置的图标的 URL。
- `chromeTimeToLive`：此参数指定当设备脱机时，应该在 GCM 存储器中保留消息的时间长度（秒）。
- `chromePayload`：将作为通知消息的一部分发送的定制 JSON 有效内容。
- `chromeAppExtTitle`：指定要为 WebPush Notification 设置的标题。
- `chromeAppExtCollapseKey`：此参数用于识别一组消息。
- `chromeAppExtDelayWhileIdle`：当此参数设置为 true 时，表示在设备变为活动之前，不应发送消息。
- `chromeAppExtIconUrl`：要为 WebPush Notification 设置的图标的 URL。
- `chromeAppExtTimeToLive`：此参数指定当设备脱机时，应该在 GCM 存储器中保留消息的时间长度（秒）。
- `chromeAppExtPayload`：将作为通知消息的一部分发送的定制 JSON 有效内容。

下面是 *pushnotification* 包中发送推送通知的示例。

- 使用先前创建的包绑定中的 `sendMessage` 操作来发送推送通知。确保将 `/myNamespace/myPush` 替换为您的包名。
  
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
  

## 在 Push Notifications 服务活动上触发触发器事件
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` 可配置 Push 服务，当在指定的应用程序中存在设备活动（如设备注册/取消注册或预订/取消预订）时，触发触发器。

参数如下所示：

- `appId：`Bluemix 应用程序 GUID。
- `appSecret：`Bluemix 推送通知服务 appSecret。
- `events：`受支持的事件为 `onDeviceRegister`、`onDeviceUnregister`、`onDeviceUpdate`、`onSubscribe`、`onUnsubscribe`。要在发生所有事件时都获得通知，请使用通配符 `*`。

以下是创建触发器的示例，此触发器将在每次向 Push Notifications 服务应用程序注册新设备时触发。

1. 使用 appId 和 appSecret，创建针对 Push Notifications 服务配置的包绑定。
  
  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}
  
2. 使用 `myPush/webhook` 订阅源为 Push Notifications 服务 `onDeviceRegister` 事件类型创建触发器。
  
  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}  
  
3. 可以创建规则，用于在每次新设备注册时发送消息。使用先前的操作和触发器创建新规则。
  
  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}
  
  检查 `wsk activation poll` 中的结果。

  在 Bluemix 应用程序中注册设备，您可以看到 `rule`、`trigger` 和 `action` 会在 openWhisk [仪表板]
(https://console.{Domain}/openwhisk/dashboard) 中执行。

  该操作将发送推送通知。
  
