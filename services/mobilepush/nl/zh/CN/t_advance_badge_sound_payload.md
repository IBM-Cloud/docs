---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#启用高级推送通知
上次更新时间：2017 年 1 月 11 日
{: .last-updated}

配置 iOS 角标、声音、其他 JSON 有效内容、可操作通知和暂停通知。

## 配置声音、有效内容和 iOS 角标
{: #badge-sound-payload}

配置 iOS 角标、声音和其他 JSON 有效内容。

1. 在 {{site.data.keyword.mobilepushshort}} 仪表板上，转至**通知**选项卡。
2. 转至**可选字段**部分，以配置 {{site.data.keyword.mobilepushshort}} 功能。 
	- **声音文件** - 输入字符串，以指向移动应用程序中的声音文件。在有效内容中，指定要使用的声音文件的字符串名称。
	- **iOS 角标** - 对于 iOS 设备，要显示为应用程序图标角标的数字。如果缺少此属性，那么角标不会改变。要除去角标，请将此属性的值设置为 0。
	
###Android

将声音文件添加到 Android 应用程序的 `res/raw` 目录中。发送通知时，在 {{site.data.keyword.mobilepushshort}} 的声音字段中添加声音文件名。

```
"settings":{
     "gcm":{
	     "sound":"tt.wav",
	  }
	 }  
```
    {: codeblock}	
	
###iOS

```
"settings": {
     "apns" : {
	      "badge": 10,
	      "sound": "tt.wav",
	  }
	}
``` 
	{: codeblock}
		
**其他有效内容** - 此有效内容可以是任何键/值对，但必须为要与 {{site.data.keyword.mobilepushshort}} 一起发送的 JSON 对象。


```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## 暂停 Android 通知 
{: #hold-notifications-android}

应用程序转入后台运行时，您可能希望 {{site.data.keyword.mobilepushshort}} 暂停发送给应用程序的通知。要暂停通知，请调用处理 {{site.data.keyword.mobilepushshort}} 的活动的 onPause() 方法中的 hold() 方法。

```
@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}
## 启用 iOS 可操作通知  
{: #enable-actionable-notifications-ios}

与传统 {{site.data.keyword.mobilepushshort}} 不同，可操作通知会提示用户在收到通知警报时进行相应的选择，而无需打开应用程序。 

请完成以下步骤，以在应用程序中启用可操作的 {{site.data.keyword.mobilepushshort}}。

1. 创建用户响应操作。
```
//For Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground
	```
	{: codeblock}
```
//For Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
	```
	{: codeblock}

2. 创建通知类别并设置操作。**UIUserNotificationActionContextDefault** 或 **UIUserNotificationActionContextMinimal** 是有效的上下文。
```
// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
	```
	{: codeblock}

1. 创建通知设置并分配前一步中的类别。
```
// For Swift
	let categories = NSSet(array:[pushCategory]);
	```
	{: codeblock}

1. 创建本地或远程通知，并为其分配类别的标识。
```
//For Swift
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications() 
	```
	{: codeblock}
	
## 处理可操作的 iOS 通知  
{: #actionable-notifications}

收到可操作通知时，会根据所选择的标识将控制权传递到以下方法上。

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
//must call completion handler when finished
      completionHandler()
  }
```    
	{: codeblock}
    
