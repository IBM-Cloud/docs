---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Registering a device with userId
{: #register_device_with_userId}
Last updated: 06 February 2017
{: .last-updated}

To register for userId-based notification, complete the following steps:

## Android
{: android-register}

Initialize the MFPPush class with the `AppGUID` and `clientSecret` key of {{site.data.keyword.mobilepushshort}} service.
```
// Initialize the Push Notifications service
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```
	{: codeblock}


- **AppGUID**: This is the AppGUID key of the {{site.data.keyword.mobilepushshort}} service.
- **clientSecret**: This is the clientSecret key of the {{site.data.keyword.mobilepushshort}} service.

  Use the **registerDeviceWithUserId** API to register the device for {{site.data.keyword.mobilepushshort}}.

```
// Register the device to Push Notifications
push.registerDeviceWithUserId("userId",new MFPPushResponseListener<String>() {
		@Override
		public void onSuccess(String response) {
		Log.d("Device is registered with Push Service.");}
		@Override
		public void onFailure(MFPPushException ex) {
		  Log.d("Error registering with Push Service...\n"
   		  + "Push notifications will not be received.");
		}
		});
```
	{: codeblock}

- **userId**: Pass the unique userId value for registering for {{site.data.keyword.mobilepushshort}}.

**Note:** To enable {{site.data.keyword.mobilepushshort}} targeted by UserId, ensure that you register the device with a userId and also pass the 'clientSecret' that is allocated when the {{site.data.keyword.mobilepushshort}} services are provisioned. Device registration will fail without a valid clientSecret.

## Cordova
{: cordova}

Use the following APIs to register for UserId based {{site.data.keyword.mobilepushshort}}.

```
// Register device for Push Notification with UserId
var options = {"userId": "Your User Id value"};
BMSPush.registerDevice(options,success, failure); 
```
	{: codeblock}


- **userId**: Pass the unique userId value for registering for {{site.data.keyword.mobilepushshort}}.


## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


- **AppGUID**: This is the AppGUID key of the {{site.data.keyword.mobilepushshort}} service.
- **clientSecret**: This is the clientSecret key of the {{site.data.keyword.mobilepushshort}} service.

Use the **registerWithUserId** API to register the device for {{site.data.keyword.mobilepushshort}}.

```
// Register the device to Push Notifications service
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

- **userId**: Pass the unique userId value for registering for {{site.data.keyword.mobilepushshort}}.

## Google Chrome, Safari and Mozilla Firefox
{: web-register}

Use the following APIs to register for userId based notifications. Initialize the SDK with `app GUID`, `app Region` and `Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
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

## Google Chrome Apps and Extensions
{: web-register-new}

Use the following APIs to register for userId based notifications. Initialize the SDK with `app GUID`, `app Region` and `Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
    alert(response.response)
    })
```
	{: codeblock}
  
After the successful initialization, you need to register the web application with the userId.

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

# Using userId-based notifications
{: #using_userid}

The userId-based notifications are notification messages that are targeted to a specific user. Many devices can be registered with one user. The following steps  describes how to send user ID-based notifications.

1. From the **Push Notification** dashboard, select **Send Notifications** option.
1. Select **UserId** in the **Send to** list of options.
1. In the **User Id** field, search for the user Id that you want to use and then click the **+Add**.![Notifications Screen](images/user_notification.jpg)
1. In the **Message** field, enter text that want to send in your notification.
1. Click **Send**.
