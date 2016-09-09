---

copyright:
 years: 2015, 2016

---


# 使用用户标识注册设备
{: #register_device_with_userId}
上次更新时间：2016 年 8 月 16 日
{: .last-updated}

要注册基于用户标识的通知，请完成以下步骤：

## Android
{: android-register}
 
使用 {{site.data.keyword.mobilepushshort}} 服务的 `AppGUID` 和 `clientSecret` 键来初始化 MFPPush 类。

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```

####AppGUID
{: push-app-guid}

此为 {{site.data.keyword.mobilepushshort}} 服务的 AppGUID 键。

####clientSecret
{: android-client-secret}

此为 {{site.data.keyword.mobilepushshort}} 服务的 clientSecret 键。

使用 **registerDeviceWithUserId** API 为设备注册 {{site.data.keyword.mobilepushshort}}。

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

传递用于注册 {{site.data.keyword.mobilepushshort}} 的唯一用户标识值。

**注：**要启用用户标识所针对的 {{site.data.keyword.mobilepushshort}}，请确保您是使用用户标识注册设备的，并且还需要传递在供应 {{site.data.keyword.mobilepushshort}} 服务时分配的“clientSecret”。如果未传递有效的 clientSecret，设备注册将会失败。





## Cordova
{: cordova-register}

将以下代码片段复制到您的移动应用程序中，以注册基于 userId 的通知。

使用 `clientSecret` 初始化 `MFPPush`。 

```
MFPPush.initialize("appGUID", "clientSecret");
```

###appGUID 
{: cordova-pushappguid}

此为 {{site.data.keyword.mobilepushshort}} 服务的 AppGUID 键。 

####clientSecret 
{: cordova-client-secret}

此为 {{site.data.keyword.mobilepushshort}} 服务的 clientSecret 键。

```
//Register for {{site.data.keyword.mobilepushshort}} with userId
var userId = "userId";
MFPPush.registerDevice({},success,failure,userId); 
```
####userId
{: cordova-user-id}

传递用于注册 {{site.data.keyword.mobilepushshort}} 服务的唯一用户标识值。


## Objective-C
{: objc-register}

使用以下 API 来注册基于 UserId 的 {{site.data.keyword.mobilepushshort}}。

```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"]; 
```
###AppGUID 
{: objc-pushappguid}

此为 {{site.data.keyword.mobilepushshort}} 服务的 AppGUID 键。

####clientSecret
{: objc-client-secret}

此为 {{site.data.keyword.mobilepushshort}} 服务的 clientSecret 键。

使用 **registerWithUserId** API 为设备注册 {{site.data.keyword.mobilepushshort}}。

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

传递用于注册 {{site.data.keyword.mobilepushshort}} 的唯一用户标识值。

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```

####AppGUID 
{: swift-pushappguid}
此为 {{site.data.keyword.mobilepushshort}} 服务的 AppGUID 键。

####clientSecret
{: swift-client-secret} 

此为 {{site.data.keyword.mobilepushshort}} 服务的 clientSecret 键。

使用 **registerWithUserId** API 为设备注册 {{site.data.keyword.mobilepushshort}}。

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

传递用于注册 {{site.data.keyword.mobilepushshort}} 的唯一用户标识值。


# 使用基于用户标识的通知
{: #using_userid}


基于用户标识的通知是针对特定用户的通知消息。一个用户可注册多个设备。以下步骤描述了如何发送基于用户标识的通知。 

1. 在**推送通知**仪表板中，单击**通知**选项卡。
1. 选择**用户标识**选项，以发送基于用户标识的通知。
1. 在**搜索用户标识**字段中，搜索要使用的用户标识，然后单击 **+添加**按钮。![通知屏幕](images/user_notification.jpg)
1. 在**消息文本**字段中，输入要在通知中发送的文本。
1. 单击**发送**按钮。
