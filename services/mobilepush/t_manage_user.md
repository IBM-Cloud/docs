---

copyright:
 years: 2015, 2016

---


# Registering a device with userId
{: #register_device_with_userId}
<<<<<<< HEAD
Last updated: 23 August 2016
=======
Last updated: 16 August 2016
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f
{: .last-updated}

To register for userId-based notification, complete the following steps:

## Android
{: android-register}
<<<<<<< HEAD

Initialize the MFPPush class with the `AppGUID` and `clientSecret` key of {{site.data.keyword.mobilepushshort}} service.

=======
 
Initialize the MFPPush class with the `AppGUID` and `clientSecret` key of {{site.data.keyword.mobilepushshort}} service.

>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f
	```
	// Initialize the MFPPush
	push = MFPPush.getInstance();
	push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
	```
	{: codeblock}

####AppGUID
{: push-app-guid}

This is the AppGUID key of the {{site.data.keyword.mobilepushshort}} service.

####clientSecret
{: android-client-secret}

This is the clientSecret key of the {{site.data.keyword.mobilepushshort}} service.

Use the **registerDeviceWithUserId** API to register the device for {{site.data.keyword.mobilepushshort}}.

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
	{: codeblock}

####userId
{: android-user-id}

<<<<<<< HEAD
Pass the unique userId value for registering for {{site.data.keyword.mobilepushshort}}.

**Note:** To enable {{site.data.keyword.mobilepushshort}} targeted by UserId, ensure that you register the device with a userId and also pass the 'clientSecret' that is allocated when the {{site.data.keyword.mobilepushshort}} services are provisioned. Device registration will fail without a valid clientSecret.
=======
Pass the unique User ID value for registering for {{site.data.keyword.mobilepushshort}}.

**Note:** To enable {{site.data.keyword.mobilepushshort}} targeted by UserId, ensure that you register the device with a UserId and also pass the 'clientSecret' that is allocated when the {{site.data.keyword.mobilepushshort}} services are provisioned. If you do not pass a valid clientSecret, the device registration will fail.
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f


## Cordova
{: cordova-register}

Copy the following code snippet to your mobile application to register for userId -based notifications.

Initialize `MFPPush` with `clientsecret`.

	```
	MFPPush.initialize("appGUID", "clientSecret");
	```
	{: codeblock}

###appGUID
{: cordova-pushappguid}

<<<<<<< HEAD
This is the AppGUID key of the {{site.data.keyword.mobilepushshort}} service.
=======
This is the AppGUID key of the {{site.data.keyword.mobilepushshort}} service. 
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f

####clientSecret
{: cordova-client-secret}

This is the clientSecret key of the {{site.data.keyword.mobilepushshort}} service.

	```
	//Register for {{site.data.keyword.mobilepushshort}} with userId
	var userId = "userId";
<<<<<<< HEAD
	MFPPush.registerDevice({},success,failure,userId);
=======
	MFPPush.registerDevice({},success,failure,userId); 
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f
	```
	{: codeblock}

####userId
{: cordova-user-id}

Pass the unique userId value for registering for {{site.data.keyword.mobilepushshort}} service.


## Objective-C
{: objc-register}

Use the following APIs to register for UserId based {{site.data.keyword.mobilepushshort}}.
<<<<<<< HEAD

	```
	// Initialize the MFPPush
	IMFPushClient* push = [IMFPushClient sharedInstance];
	[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"];
	```
	{: codeblock}

###AppGUID
=======

	```
	// Initialize the MFPPush
	IMFPushClient* push = [IMFPushClient sharedInstance];
	[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"]; 
	```
	{: codeblock}

###AppGUID 
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f
{: objc-pushappguid}

This is the AppGUID key of the {{site.data.keyword.mobilepushshort}} service.

####clientSecret
{: objc-client-secret}

This is the clientSecret key of the {{site.data.keyword.mobilepushshort}} service.

Use the **registerWithUserId** API to register the device for {{site.data.keyword.mobilepushshort}}.

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
	{: codeblock}

####userId
{: objc-user-id}

<<<<<<< HEAD
Pass the unique userId value for registering for {{site.data.keyword.mobilepushshort}}.
=======
Pass the unique User ID value for registering for {{site.data.keyword.mobilepushshort}}.
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f

## Swift
{: swift-register}

	```
	// Initialize the BMSPushClient
	let push =  BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
	```
	{: codeblock}

####AppGUID
{: swift-pushappguid}
This is the AppGUID key of the {{site.data.keyword.mobilepushshort}} service.

####clientSecret
{: swift-client-secret}

This is the clientSecret key of the {{site.data.keyword.mobilepushshort}} service.

Use the **registerWithUserId** API to register the device for {{site.data.keyword.mobilepushshort}}.

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
	{: codeblock}

####userId
{: swift-user-id}

<<<<<<< HEAD
Pass the unique userId value for registering for {{site.data.keyword.mobilepushshort}}.

## Google Chrome and Mozilla Firefox
{: web-register}

Use the following APIs to register for userId based notifications. Initialize the SDK with `app GUID`, `app Region` and `Client Secret`.

  ```
    var bmsPush = new bmsPush();
    var params = {
        "appGUID":"push app GUID",
        "appRegion":"App Region"
        "clientSecret":"Push Client Secret" (optional)
      }
      bmsPush.initialize(params, function(response){
          alert(response.response)
      })
  ```
	{: codeblock}
  
After successfully initialized register the web application with userId.

  ```
    bmsPush.registerWithUserId("UserId", function(response) {
      alert(response.response)
    })
  ```
	{: codeblock}

# Using userId-based notifications
=======
Pass the unique User ID value for registering for {{site.data.keyword.mobilepushshort}}.


# Using User ID-based notifications
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f
{: #using_userid}


The userId-based notifications are notification messages that are targeted to a specific user. Many devices can be registered with one user. The following steps  describes how to send user ID-based notifications.

1. From the **Push Notification** dashboard, click the **Notifications** tab.
1. Select the **UserId** option to send userId-based notifications.
1. In the **Search** UserId field, search for the userid that you want to use and then click the **+Add** button.![Notifications Screen](images/user_notification.jpg)
1. In the **Message Text** field, enter text that want to send in your notification.
1. Click the **Send** button.
