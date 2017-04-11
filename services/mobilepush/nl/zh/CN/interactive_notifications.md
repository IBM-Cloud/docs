---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 交互式通知
{: #interactive-notifications}
上次更新时间：2017 年 1 月 23 日
{: .last-updated}

使用交互式通知，用户可以在不打开应用程序的情况下响应通知。当交互式通知到达时，设备会显示通知消息及相应的操作按钮。V8 或更高版本的 iOS 设备上支持交互式通知。对于向版本低于 V8 的 iOS 设备发送的交互式通知，不会显示通知操作。

##发送交互式 {{site.data.keyword.mobilepushshort}}


使用“推送”仪表板或使用 [REST API 文档](t_restapi.html)可发送交互式通知。

从 {{site.data.keyword.mobilepushshort}} 控制台： 

1. 在“推送”仪表板中的“通知”选项卡上，单击**发送通知**。 
2. 选择通知收件人，并单击**下一步**。 
3. 在编写通知页面上，可以通过将“类型”设置为“缺省值”或“混合”并在“高级选项”选项卡下指定“类别”值来发送交互式推送。要在客户机上配置类别值，请查看“在本机 iOS 应用程序中**处理交互式 {{site.data.keyword.mobilepushshort}}**”一节。

## 在 iOS 应用程序中处理交互式 {{site.data.keyword.mobilepushshort}}


### Swift

完成以下步骤以接收交互式通知：

1. 为应用程序启用在后台执行接收远程通知任务的功能。 
1. 使用您的操作类别，初始化`BMSPush` SDK。
	```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: BMSClient.Region.usSouth)
	let push =  BMSPushClient.sharedInstance
    let actionOne = BMSPushNotificationAction(identifierName: "FIRST", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let actionTwo = BMSPushNotificationAction(identifierName: "SECOND", buttonTitle: "Reject", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
   	let notifOptions = BMSPushClientOptions(categoryName: [category])
	push.initializeWithAppGUID(appGUID: "YOUR_APP_GUID", clientSecret:"YOUR_APP_CLIENT_SECRET", options: notifOptions)
	```
		{: codeblock}

1. 在 AppDelegate 上实施新回调方法：
	```
	 func userNotificationCenter(_ center: UNUserNotificationCenter,
       didReceive response: UNNotificationResponse,
       withCompletionHandler completionHandler: @escaping () -> Void) {
            switch response.actionIdentifier {
		    case "FIRST":
		      print("FIRST")
		    case "SECOND":
		      print("SECOND")  
		    default:
		      print("Unknown action")
		    }
		completionHandler
	}
	```
	{: codeblock} 
5. 用户单击操作按钮时，将调用此新回调方法。要实施此方法，必须执行与指定标识关联的任务，并执行 `completionHandler` 参数中的块。


### Cordova

要在 Cordova iOS 应用程序中获取可操作通知，请完成以下步骤：

1. 在 `BMSPush.initialize` 方法内添加类别字段。
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. 在 AppDelegate 上实施新回调方法。
3. 用户单击操作按钮时，将调用此新回调方法。要实施此方法，必须执行与指定标识关联的任务，并执行 completionHandler 参数中的块。
