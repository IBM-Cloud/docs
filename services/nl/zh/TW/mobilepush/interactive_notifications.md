---

copyright:
 years: 2015, 2016

---

# 互動式通知
{: #interactive-notifications}

互動式通知容許使用者在通知到達時能夠作用，而無需開啟應用程式。當互動式通知到達時，裝置會顯示動作按鈕以及通知訊息。第 8 版以及更新版本的 iOS 裝置上支援互動式通知。如果互動式通知傳送至低於第 8 版的 iOS 裝置，則不會顯示通知動作。

##傳送互動式推送通知


您可以使用 Push 儀表板或使用 REST API 來傳送互動式通知（請參閱 REST API documentationREST API 文件）。

從 Push 主控台： 

在 Push 儀表板的通知標籤下，按一下「傳送通知」。選擇您的通知收件者，然後按「下一步」。在「編寫通知」頁面中，將「類型」設為「預設值」或「混合」，並且指定「進階選項」標籤下的「種類」值，即可傳送互動式推送。若要配置用戶端上的種類值，請檢查「處理原生 iOS 應用程式中的互動式推送通知」區段。

## 處理 iOS 應用程式中的互動式推送通知

您必須遵循下列這些步驟，才能接收互動式通知：

1. 啟用應用程式功能，以執行背景作業來接收遠端通知。如果部分動作是在背景啟用，則這是必要步驟。
1. 在 `AppDelegate (application: didRegisterForRemoteNotificationsWithDeviceTokenapplication:)` 中，請先設定種類，然後再設定 `WLPush Object` 上的 `deviceToken`。

```
	if([application respondsToSelector:@selector(registerUserNotificationSettings:)]){
	 UIUserNotificationType userNotificationTypes = UIUserNotificationTypeNone | UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge;
	      
	 UIMutableUserNotificationAction *acceptAction = [[UIMutableUserNotificationAction alloc] init];
	 acceptAction.identifier = @"OK";
	 acceptAction.title = @"OK";
	      
	 UIMutableUserNotificationAction *rejetAction = [[UIMutableUserNotificationAction alloc] init];
	 rejetAction.identifier = @"NOK";
	 rejetAction.title = @"NOK";
	      
	 UIMutableUserNotificationCategory *cateogory = [[UIMutableUserNotificationCategory alloc] init];
	 cateogory.identifier = @"poll";
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextDefault];
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextMinimal];
	      
	 NSSet *catgories = [NSSet setWithObject:cateogory];
	 [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:userNotificationTypes categories:catgories]];
}
```

1. 在 AppDelegate 上實作新的回呼方法：

```
	-(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
``` 

5. 當使用者按一下動作按鈕時，即會呼叫這個新的回呼方法。實作此方法必須執行與指定 ID 相關聯的 do，並執行 `completionHandler` 參數中的 block。
