---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 互動式通知
{: #interactive-notifications}
前次更新：2017 年 1 月 23 日
{: .last-updated}

互動式通知可讓使用者在不開啟應用程式的情況下，就可以回應通知。當互動式通知到達時，裝置會顯示動作按鈕以及通知訊息。第 8 版或更新版本的 iOS 裝置上都支援互動式通知。若將互動式通知傳送至第 8 版之前的 iOS 裝置，則不會顯示通知動作。

##傳送互動式 {{site.data.keyword.mobilepushshort}}


您可以使用 Push 儀表板或使用 [REST API 文件](t_restapi.html)來傳送互動式通知。

從 {{site.data.keyword.mobilepushshort}} 主控台，請執行下列動作： 

1. 在 Push 儀表板的通知標籤上，按一下**傳送通知**。 
2. 選擇您的通知收件者，然後按**下一步**。 
3. 在「編寫通知」頁面中，將「類型」設為「預設值」或「混合」，並在「進階選項」標籤下指定「種類」值，即可傳送互動式推送。若要配置用戶端上的種類值，請檢查**處理原生 iOS 應用程式中的互動式 {{site.data.keyword.mobilepushshort}}** 區段。

## 處理 iOS 應用程式中的互動式 {{site.data.keyword.mobilepushshort}}


### Swift

請完成下列步驟，以接收互動式通知：

1. 啟用應用程式功能，以執行背景作業來接收遠端通知。 
1. 起始設定 `BMSPush` SDK 及您的動作種類。
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

1. 在 AppDelegate 上實作新的回呼方法：
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
5. 當使用者按一下動作按鈕時，即會呼叫這個新的回呼方法。實作此方法必須執行與指定 ID 相關聯的作業，並執行 `completionHandler` 參數中的區塊。


### Cordova

若要在 Cordova iOS 應用程式中取得可採取動作的通知，請完成下列步驟：

1. 在 `BMSPush.initialize` 方法內新增種類欄位。
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. 在 AppDelegate 上實作新的回呼方法。
3. 當使用者按一下動作按鈕時，即會呼叫這個新的回呼方法。實作此方法必須執行與指定 ID 相關聯的作業，並執行 completionHandler 參數中的區塊。
