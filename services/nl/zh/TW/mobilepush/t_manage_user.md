---

copyright:
 years: 2015, 2016

---


# 向使用者 ID 登錄裝置
{: #register_device_with_userId}
*前次更新：2016 年 7 月 20 日*
{: .last-updated}

若要登錄「使用者 ID 型」通知，請完成下列步驟：

## Android
 
利用 Push Notification Service 的 `pushTenantId` 及 `clientSecret` 金鑰，起始設定 IMFPush 類別。

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initializeBluemixPushWithClientSecret(getApplicationContext(),"clientSecret");
```

**clientSecret** 

這是 Push Notification Service 的 clientSecret 金鑰。


使用 **registerWithUserId** API 登錄裝置，以取得推送通知。

```
// Register the device to push notifications service.
push.registerWithUserId("userId",new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
	           updateTextView("Device is registered with Push Service.");
        displayTags();
    }

    @Override
  public void onFailure(MFPPushException ex) {
    updateTextView("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
    }
});
```

**userId** 

傳遞唯一「使用者 ID」值，以登錄推送通知。

>**附註：**若要啟用使用者 ID 設為目標的推送通知，請確定您向使用者 ID 登錄裝置，同時也傳遞當佈建 Push Notification Service 時所配置的 'clientSecret'。如果未傳遞有效的 clientSecret，裝置登錄將失敗。

## Cordova

將下列程式碼 Snippet 複製至行動應用程式，來登錄使用者 ID 型通知。

利用 `clientsecret` 起始設定 `MFPPush`。 

```
MFPPush.initializeBluemixPushWithClientSecret("clientSecret");
```

**clientSecret** 

這是 Push Notification Service 的 clientSecret 金鑰。

```
//Register for Push notification with userId
var userId = "userId";
MFPPush.registerWithUserId(userId,success,failure);
```
**userId** 

傳遞唯一「使用者 ID」值，以登錄 Push Notification Service。


## Objective-C


使用下列 API 來登錄「使用者 ID 型」推送通知。


```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeBluemixPushWithClientSecret:@"clientSecret"];
```

**clientSecret** 

這是 Push Notification Service 的 clientSecret 金鑰。


使用 **registerWithUserId** API 登錄裝置，以取得推送通知。


```
// Register the device to push notifications service.
[push registerDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
    NSString *message=@"";
    
	if (error){
        message = [NSString stringWithFormat:@"Error registering for push notifications: %@", error.description];
        NSLog(@"%@",message);
    } else {
        message=@"Successfully registered for push notifications";
        NSLog(@"%@",message);
    }
}];
```


**userId** 

傳遞唯一「使用者 ID」值，以登錄推送通知。

## Swift

```
// Initialize the BMSPushCliet
let push =  BMSPushClient.sharedInstance
push.initializeBluemixPushWithClientSecret("clientSecret")
```

**clientSecret** 

這是 Push Notification Service 的 clientSecret 金鑰。

使用 **registerWithUserId** API 登錄裝置，以取得推送通知。

```
// Register the device to Push Notifications service.
push.registerDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    } else {
print( "Error during device registration \(error) ")
    }
}
```

**userId** 

傳遞唯一「使用者 ID」值，以登錄推送通知。


# 使用「使用者 ID 型」通知
{: #using_userid}


使用者 ID 型通知是以特定使用者為目標的通知訊息。可向一個使用者登錄多個裝置。下列步驟說明如何傳送使用者 ID 型通知。 

1. 從**推送通知**儀表板中，按一下**通知**標籤。
1. 選取**使用者 ID** 選項，以傳送使用者 ID 型通知。
1. 在**搜尋使用者 ID** 欄位中，搜尋您要使用的使用者 ID，然後按一下 **+ 新增**按鈕。![通知畫面](images/tag_notification.jpg)
1. 在**訊息文字**欄位中，輸入要在通知中傳送的文字。
1. 按一下**傳送**按鈕。
