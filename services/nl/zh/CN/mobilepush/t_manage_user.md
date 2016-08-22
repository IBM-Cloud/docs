---

copyright:
 years: 2015, 2016

---


# 使用用户标识注册设备
{: #register_device_with_userId}
*上次更新时间：2016 年 7 月 20 日*
{: .last-updated}

要注册基于用户标识的通知，请完成以下步骤：

## Android
 
使用 Push Notifications 服务的 `pushTenantId` 和 `clientSecret` 键来初始化 IMFPush 类。

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initializeBluemixPushWithClientSecret(getApplicationContext(),"clientSecret");
```

**clientSecret** 

此为 Push Notifications 服务的 clientSecret 键。


使用 **registerWithUserId** API 为设备注册推送通知。

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

传递用于注册推送通知的唯一用户标识值。

>**注：**要按用户标识向目标推送通知，请确保您是使用用户标识注册设备的，并且还需要传递在供应 Push Notifications 服务时分配的“clientSecret”。如果未传递有效的 clientSecret，设备注册将会失败。


## Cordova

将以下代码片段复制到您的移动应用程序中，以注册基于用户标识的通知。

使用 `clientSecret` 初始化 `MFPPush`。 

```
MFPPush.initializeBluemixPushWithClientSecret("clientSecret");
```

**clientSecret** 

此为 Push Notifications 服务的 clientSecret 键。

```
//Register for Push notification with userId
var userId = "userId";
MFPPush.registerWithUserId(userId,success,failure);
```
**userId** 

传递用于注册 Push Notifications 服务的唯一用户标识值。


## Objective-C


使用以下 API 来注册基于用户标识的推送通知。


```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeBluemixPushWithClientSecret:@"clientSecret"];
```

**clientSecret** 

此为 Push Notifications 服务的 clientSecret 键。


使用 **registerWithUserId** API 为设备注册推送通知。


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

传递用于注册推送通知的唯一用户标识值。

## Swift

```
// Initialize the BMSPushCliet
let push =  BMSPushClient.sharedInstance
push.initializeBluemixPushWithClientSecret("clientSecret")
```

**clientSecret** 

此为 Push Notifications 服务的 clientSecret 键。

使用 **registerWithUserId** API 为设备注册推送通知。

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

传递用于注册推送通知的唯一用户标识值。


# 使用基于用户标识的通知
{: #using_userid}


基于用户标识的通知是针对特定用户的通知消息。一个用户可注册多个设备。以下步骤描述了如何发送基于用户标识的通知。 

1. 在**推送通知**仪表板中，单击**通知**选项卡。
1. 选择**用户标识**选项，以发送基于用户标识的通知。
1. 在**搜索用户标识**字段中，搜索要使用的用户标识，然后单击 **+添加**按钮。![通知屏幕](images/tag_notification.jpg)
1. 在**消息文本**字段中，输入要在通知中发送的文本。
1. 单击**发送**按钮。
