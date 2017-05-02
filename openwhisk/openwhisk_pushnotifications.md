---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Using the Push Notifications package
{: #openwhisk_catalog_pushnotifications}

The `/whisk.system/pushnotifications` package enables you to work with a push service.

The package includes the following action and feed:

| Entity | Type | Parameters | Description |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | package | appId, appSecret  | Work with the Push Service |
| `/whisk.system/pushnotifications/sendMessage` | action | text, url, deviceIds, platforms, userIds, tagNames, gcmCollapseKey, gcmCategory, gcmIcon, gcmDelayWhileIdle, gcmSync, gcmVisibility, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive, gcmStyleType, gcmStyleTitle, gcmStyleUrl, gcmStyleText, gcmStyleLines, gcmLightsLedArgb, gcmLightsLedOnMs, gcmLightsLedOffMs, apnsBadge, apnsCategory, apnsIosActionKey, apnsPayload, apnsType, apnsSound, apnsTitleLocKey, apnsLocKey, apnsLaunchImage, apnsTitleLocArgs, apnsLocArgs, apnstitle, apnsSubtitle, apnsAttachmentUrl, fireFoxTitle, fireFoxIconUrl, fireFoxTimeToLive, fireFoxPayload, safariTitle, safariUrlArgs, safariAction, chromeTitle, chromeIconUrl, chromeTimeToLive, chromePayload, chromeAppExtTitle, chromeAppExtCollapseKey, chromeAppExtDelayWhileIdle, chromeAppExtIconUrl, chromeAppExtTimeToLive, chromeAppExtPayload | Send push notification to one or more specified devices |
| `/whisk.system/pushnotifications/webhook` | feed | events | Fire trigger events on device activities (device registration, unregistration, subscription, or unsubscription) on the Push service |
Creating a package binding with the `appId` and `appSecret` values is suggested. This way, you don't need to specify these credentials every time you invoke the actions in the package.

## Creating a Push package binding
{: #openwhisk_catalog_pushnotifications_create}

While creating a Push Notifications package binding, you must specify the following parameters,

-  `appId`: The Bluemix app GUID.
-  `appSecret`: The Bluemix push notification service appSecret.

The following is an example of creating a package binding.

1. Create a Bluemix application in [Bluemix Dashboard](http://console.ng.bluemix.net).

2. Initialize the Push Notification Service and bind the service to the Bluemix application

3. Configure the [Push Notification application](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Be sure to remember the `App GUID` and the `App Secret` of the Bluemix app you created.

4. Create a package binding with the `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}
  
5. Verify that the package binding exists.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myPush private binding
  ```


## Sending push notifications
{: #openwhisk_catalog_pushnotifications_send}

The `/whisk.system/pushnotifications/sendMessage` action sends push notifications to registered devices. The parameters are as follows:

- `text`: The notification message to be shown to the user. For example: `-p text "Hi ,OpenWhisk send a notification"`.
- `url`: An optional URL that can be sent along with the alert. For example: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds` The list of specified devices. For example: `-p deviceIds ["deviceID1"]`.
- `platforms` Send notification to the devices of the specified platforms. 'A' for apple (iOS) devices and 'G' for google (Android) devices. For example `-p platforms ["A"]`.
- `userIds` - Send notification to the devices of the specified users. For example: `-p userIds "[\"testUser\"]"`
- `tagNames` Send notification to the devices that have subscribed to any of these tags. For example `-p tagNames "[\"tag1\"]" `.

- `gcmCollapseKey`: This parameter identifies a group of messages
- `gcmCategory` - The category identifier to be used for the interactive push notifications.
- `gcmIcon` - Specify the name of the icon to be displayed for the notification. Make sure the icon is already packaged with the client application.
- `gcmDelayWhileIdle`: When this parameter is set to true, it indicates that the message will not be sent until the device becomes active.
- `gcmSync`: Device group messaging makes it possible for every app instance in a group to reflect the latest messaging state.
- `gcmVisibility`: private/public - Visibility of this notification, which affects how and when the notifications are revealed on a secure locked screen.
- `gcmPayload`: Custom JSON payload that will be sent as part of the notification message. For example: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmPriority`: Sets the priority of the message.
- `gcmSound`: The sound file (on device) that will be attempted to play when the notification arrives on the device.
- `gcmTimeToLive`: This parameter specifies how long (in seconds) the message will be kept in GCM storage if the device is offline.
- `gcmStyleType`: Specifies the type of expandable notifications. The possible values are `bigtext_notification`, `picture_notification`, `inbox_notification`.
- `gcmStyleTitle`: Specifies the title of the notification. The title is displayed when the notification is expanded. Title must be specified for all three expandable notification.
- `gcmStyleUrl`: An URL from which the picture has to be obtained for the notification. Must be specified for `picture_notification`.
- `gcmStyleText`: The big text that needs to be displayed on expanding a `bigtext_notification`. Must be specified for `bigtext_notification`.
- `gcmStyleLines`: An array of strings that is to be displayed in inbox style for `inbox_notification`. Must be specified for `inbox_notification`.
- `gcmLightsLedArgb` - The color of the led. The hardware will do its best approximation.
- `gcmLightsLedOnMs` - The number of milliseconds for the LED to be on while it's flashing. The hardware will do its best approximation.
- `gcmLightsLedOffMs` - The number of milliseconds for the LED to be off while it's flashing. The hardware will do its best approximation.

- `apnsBadge`: The number to display as the badge of the application icon.
- `apnsCategory`: The category identifier to be used for the interactive push notifications.
- `apnsIosActionKey`: The title for the Action key .
- `apnsPayload`: Custom JSON payload that will be sent as part of the notification message.
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: The name of the sound file in the application bundle. The sound of this file is played as an alert.
- `apnsTitleLocKey` - The key to a title string in the Localizable.strings file for the current localization. The key string can be formatted with %@ and %n$@ specifiers to take the variables specified in the `titleLocArgs` array.
- `apnsLocKey` - A key to an alert-message string in a Localizable.strings file for the current localization (which is set by the user’s language preference). The key string can be formatted with %@ and %n$@ specifiers to take the variables specified in the locArgs array.
- `apnsLaunchImage` - The filename of an image file in the app bundle, with or without the filename extension. The image is used as the launch image when users tap the action button or move the action slider.
- `pnsTitleLocArgs` - Variable string values to appear in place of the format specifiers in `title-loc-key`.
- `apnsLocArgs` - Variable string values to appear in place of the format specifiers in `locKey`.
- `apnstitle` - The title of Rich Push notifications (Supported only on iOS 10 and above).
- `apnsSubtitle` - The subtitle of the Rich Notifications. (Supported only on iOS 10 and above).
- `apnsAttachmentUrl` - The link to the iOS notifications media (video, audio, GIF, images - Supported only on iOS 10 and above).

- `fireFoxTitle`: Specifies the title to be set for the WebPush Notification.
- `fireFoxIconUrl`: The URL of the icon to be set for the WebPush Notification.
- `fireFoxTimeToLive`: This parameter specifies how long (in seconds) the message should be kept in GCM storage if the device is offline.
- `fireFoxPayload`: Custom JSON payload that will be sent as part of the notification message.

- `chromeTitle`: Specifies the title to be set for the WebPush Notification.
- `chromeIconUrl`: The URL of the icon to be set for the WebPush Notification.
- `chromeTimeToLive`: This parameter specifies how long (in seconds) the message should be kept in GCM storage if the device is offline.
- `chromePayload`: Custom JSON payload that will be sent as part of the notification message.

- `safariTitle` - Specifies the title to be set for the Safari Push Notifications.
- `safariUrlArgs` - The URL arguments that need to be used with this notification. This has to provided in the form of a JSON Array.
- `safariAction` - The label of the action button.

- `chromeAppExtTitle`: Specifies the title to be set for the WebPush Notification.
- `chromeAppExtCollapseKey`: This parameter identifies a group of messages.
- `chromeAppExtDelayWhileIdle`: When this parameter is set to true, it indicates that the message should not be sent until the device becomes active.
- `chromeAppExtIconUrl`: The URL of the icon to be set for the WebPush Notification.
- `chromeAppExtTimeToLive`: This parameter specifies how long (in seconds) the message should be kept in GCM storage if the device is offline.
- `chromeAppExtPayload`: Custom JSON payload that will be sent as part of the notification message.

Here is an example of sending push notification from the *pushnotification* package.

- Send a push notification by using the `sendMessage` action in the package binding that you created previously. Be sure to replace `/myNamespace/myPush` with your package name.

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


## Firing a trigger event on Push Notifications service activity
{: #openwhisk_catalog_pushnotifications_fire}

The `/whisk.system/pushnotifications/webhook` configures the Push service to fire a trigger when there is a device activity such as device registration / unregistration or subscription / unsubscription in a specified application

The parameters are as follows:

- `appId:` The Bluemix app GUID.
- `appSecret:` The Bluemix push notification service appSecret.
- `events:` Supported events are `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`, `onUnsubscribe`.To get notified for all events use the wildcard character `*`.

The following is an example of creating a trigger that will be fired each time there is a new device registered with the Push Notifications service application.

1. Create a package binding configured for your Push Notifications service with your appId and appSecret.

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. Create a trigger for the Push Notifications service `onDeviceRegister` event type using your `myPush/webhook` feed.

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}

3. You could create a rule that sends a message every time a new device gets register. Create a new rule using the previous action and trigger.

  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}

  Check the results in the `wsk activation poll`.

  Register a device in your Bluemix application , you can see the `rule`,`trigger` and  `action` getting executed in the openWhisk [dashboard] (https://console.{Domain}/openwhisk/dashboard).

  The action will send a push notification.

