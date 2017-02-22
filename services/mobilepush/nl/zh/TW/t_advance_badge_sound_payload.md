---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#啟用進階推送通知
前次更新：2017 年 1 月 11 日
{: .last-updated}

配置 iOS 徽章、音效、其他 JSON 有效負載、可採取動作的通知，以及保存通知。

## 配置音效、有效負載以及 iOS 徽章
{: #badge-sound-payload}

配置 iOS 徽章、音效及其他 JSON 有效負載。

1. 在 {{site.data.keyword.mobilepushshort}} 儀表板上，移至**通知**標籤。
2. 移至**選用欄位**區段，以配置 {{site.data.keyword.mobilepushshort}} 特性。 
	- **音效檔** - 輸入指向行動應用程式中音效檔的字串。在有效負載中，指定要使用之音效檔的字串名稱。
	- **iOS 徽章** - 對於 iOS 裝置，這是要顯示為應用程式圖示徽章的號碼。如果沒有此內容，則不會變更徽章。若要移除徽章，請將此內容的值設為 0。
	
###Android

在 Android 應用程式的 `res/raw` 目錄中，新增您的音效檔。傳送通知時，在 {{site.data.keyword.mobilepushshort}} 的音效欄位中新增音效檔名稱。

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
		
**其他有效負載** - 此有效負載可以是任意鍵值組，而且必須是您要與 {{site.data.keyword.mobilepushshort}} 一起傳送的 JSON 物件。



```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## 保存 Android 通知 
{: #hold-notifications-android}

在應用程式進入背景時，您可能會想要 {{site.data.keyword.mobilepushshort}} 保留傳送給應用程式的通知。若要保留通知，請在處理 {{site.data.keyword.mobilepushshort}} 之活動的 onPause() 方法中呼叫 hold() 方法。

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
## 啟用可採取動作的 iOS 通知  
{: #enable-actionable-notifications-ios}

與傳統 {{site.data.keyword.mobilepushshort}} 不同，可採取動作的通知會提示使用者在接收通知警示時做出選擇，而不必開啟應用程式。 

請完成這些步驟，以在應用程式中啟用可採取動作的 {{site.data.keyword.mobilepushshort}}。

1. 建立使用者回應動作。
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

2. 建立通知種類並設定動作。**UIUserNotificationActionContextDefault** 或 **UIUserNotificationActionContextMinimal** 是有效的環境定義。
```
// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
```
	{: codeblock}

1. 建立通知設定，並指派先前步驟的種類。
```
// For Swift
	let categories = NSSet(array:[pushCategory]);
```
	{: codeblock}

1. 建立本端或遠端通知，並為其指派種類身分。
```
//For Swift
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications()
```
	{: codeblock}
	
## 處理可採取動作的 iOS 通知  
{: #actionable-notifications}

接收到可採取動作的通知時，會根據所選擇的 ID，將控制權傳遞給下列方法。

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
	{: codeblock}
    
