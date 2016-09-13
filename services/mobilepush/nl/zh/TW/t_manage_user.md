---

copyright:
 years: 2015, 2016

---


# 向使用者 ID 登錄裝置
{: #register_device_with_userId}
前次更新：2016 年 8 月 16 日
{: .last-updated}

若要登錄「使用者 ID 型」通知，請完成下列步驟：

## Android
{: android-register}
 
使用 {{site.data.keyword.mobilepushshort}} Service 的 `AppGUID` 及 `clientSecret` 金鑰，來起始設定 MFPPush 類別。

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```

####AppGUID
{: push-app-guid}

這是 {{site.data.keyword.mobilepushshort}} Service 的 AppGUID 金鑰。

####clientSecret
{: android-client-secret}

這是 {{site.data.keyword.mobilepushshort}} Service 的 clientSecret 金鑰。

使用 **registerDeviceWithUserId** API 登錄裝置，以取得 {{site.data.keyword.mobilepushshort}}。

```
// Register the device to {{site.data.keyword.mobilepushshort}}.
push.registerDeviceWithUserId("userId",new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
	           Log.d("Device is registered with Push Service.");
    }

    @Override
  public void onFailure(MFPPushException ex) {
    Log.d("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
    }
});
```

####userId
{: android-user-id}

傳遞唯一「使用者 ID」值，以登錄 {{site.data.keyword.mobilepushshort}}。

**附註：**若要啟用以「使用者 ID」為目標的 {{site.data.keyword.mobilepushshort}}，請確定您向「使用者 ID」登錄裝置，同時也傳遞佈建 {{site.data.keyword.mobilepushshort}} Services 時所配置的 'clientSecret'。如果未傳遞有效的 clientSecret，裝置登錄將失敗。




## Cordova
{: cordova-register}

將下列程式碼 Snippet 複製到行動應用程式，以登錄使用者 ID 型通知。

利用 `clientsecret` 起始設定 `MFPPush`。 

```
MFPPush.initialize("appGUID", "clientSecret");
```

###appGUID 
{: cordova-pushappguid}

這是 {{site.data.keyword.mobilepushshort}} Service 的 AppGUID 金鑰。 

####clientSecret 
{: cordova-client-secret}

這是 {{site.data.keyword.mobilepushshort}} Service 的 clientSecret 金鑰。

```
//Register for {{site.data.keyword.mobilepushshort}} with userId
var userId = "userId";
MFPPush.registerDevice({},success,failure,userId); 
```
####userId
{: cordova-user-id}

傳遞唯一「使用者 ID」值，以登錄 {{site.data.keyword.mobilepushshort}} Service。


## Objective-C
{: objc-register}

使用下列 API 來登錄使用者 ID 型 {{site.data.keyword.mobilepushshort}}。

```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"]; 
```
###AppGUID 
{: objc-pushappguid}

這是 {{site.data.keyword.mobilepushshort}} Service 的 AppGUID 金鑰。

####clientSecret
{: objc-client-secret}

這是 {{site.data.keyword.mobilepushshort}} Service 的 clientSecret 金鑰。

使用 **registerWithUserId** API 登錄裝置，以取得 {{site.data.keyword.mobilepushshort}}。

```
// Register the device to push notifications service.
[push registerWithDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
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


####userId 
{: objc-user-id}

傳遞唯一「使用者 ID」值，以登錄 {{site.data.keyword.mobilepushshort}}。

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```

####AppGUID 
{: swift-pushappguid}
這是 {{site.data.keyword.mobilepushshort}} Service 的 AppGUID 金鑰。

####clientSecret
{: swift-client-secret} 

這是 {{site.data.keyword.mobilepushshort}} Service 的 clientSecret 金鑰。

使用 **registerWithUserId** API 登錄裝置，以取得 {{site.data.keyword.mobilepushshort}}。

```
// Register the device to Push Notifications service.
push.registerWithDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    } else {
print( "Error during device registration \(error) ")
    }
}
```

####userId 
{: swift-user-id}

傳遞唯一「使用者 ID」值，以登錄 {{site.data.keyword.mobilepushshort}}。


# 使用「使用者 ID 型」通知
{: #using_userid}


使用者 ID 型通知是以特定使用者為目標的通知訊息。可向一個使用者登錄多個裝置。下列步驟說明如何傳送使用者 ID 型通知。 

1. 從**推送通知**儀表板中，按一下**通知**標籤。
1. 選取**使用者 ID** 選項，以傳送使用者 ID 型通知。
1. 在**搜尋使用者 ID** 欄位中，搜尋您要使用的使用者 ID，然後按一下 **+ 新增**按鈕。![通知畫面](images/user_notification.jpg)
1. 在**訊息文字**欄位中，輸入要在通知中傳送的文字。
1. 按一下**傳送**按鈕。
