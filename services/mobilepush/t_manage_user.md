---

copyright:
 years: 2015, 2016

---


# Register device with User ID
{: #register_device_with_userId}
Last updated: 20 July 2016
{: .last-updated}

To register for User ID-based notification, complete the following steps:

## Android
{: android-register}
 
Initialize the IMFPush class with the `AppGUID` and `clientSecret` key of Push Notification service.

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```

####AppGUID
{: push-app-guid}

This is the AppGUID key of the Push Notifications service.

####clientSecret
{: android-client-secret}

This is the clientSecret key of the Push Notifications service.

Use the **registerDeviceWithUserId** API to register the device for push notifications.

```
// Register the device to Push Notifications service.
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

Pass the unique User ID value for registering for push notifications.

**Note:** To enable push notifications targeted by UserId, ensure that you register the device with a UserId and also pass the 'clientSecret' that is allocated when the Push Notifications services are provisioned. If you do not pass a valid clientSecret, the device registration will fail.


## Cordova
{: cordova-register}

Copy the following code snippet to your mobile application to register for userId based notifications.

Initialize `MFPPush` with `clientsecret`. 

```
MFPPush.initialize("appGUID", "clientSecret");
```

###appGUID 
{: cordova-pushappguid}

This is the AppGUID key of the Push Notifications service. 

####clientSecret 
{: cordova-client-secret}

This is the clientSecret key of the Push Notifications service.

```
//Register for Push notification with userId
var userId = "userId";
MFPPush.registerDevice({},success,failure,userId); 
```
####userId
{: cordova-user-id}

Pass the unique User ID value for registering for Push Notification service.


## Objective-C
{: objc-register}

Use the following APIs to register for UserId based push notifications.

```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"]; 
```
###AppGUID 
{: objc-pushappguid}

This is the AppGUID key of the Push Notifications service.

####clientSecret
{: objc-client-secret}

This is the clientSecret key of the Push Notifications service.

Use the **registerWithUserId** API to register the device for push notifications.

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

Pass the unique User ID value for registering for push notifications.

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```

####AppGUID 
{: swift-pushappguid}
This is the AppGUID key of the Push Notifications service.

####clientSecret
{: swift-client-secret} 

This is the clientSecret key of the Push Notifications service.

Use the **registerWithUserId** API to register the device for push notifications.

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

Pass the unique User ID value for registering for push notifications.


# Using User ID-based notifications
{: #using_userid}


User ID-based notifications are notification messages that are targeted to a specific user. Many devices can be registered with one user. The following steps  describes how to send user ID-based notifications. 

1. From the **Push Notification** dashboard, click the **Notifications** tab.
1. Select the **UserId** option to send userId-based notifications.
1. In the **Search** UserId field, search for the userid that you want to use and then click the **+Add** button.![Notifications Screen](images/user_notification.jpg)
1. In the **Message Text** field, enter text that want to send in your notification.
1. Click the **Send** button.
