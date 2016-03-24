---

copyright:
 years: 2015, 2016

---

# Initializing Push SDK for iOS apps
{: #enable-push-ios-notifications-initialize}

A common place to put the initialization code is in the application delegate for the iOS application.
Click the **Mobile Options** link in your Bluemix Application Dashboard to get the application route and GUID.

##Initializing the Core SDK

###Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

###Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```

##Initializing the client Push SDK

###Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

###Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

## Route, GUID, and Bluemix region

**appRoute**

Specifies the route that is assigned to the server application that you created on Bluemix.

**GUID**

Specifies the unique key that is assigned to the application that you created on Bluemix. This value is case-sensitive.

**bluemixRegionSuffix**

Specifies the location where the app is hosted. The ```bluemixRegion``` parameter specifies which Bluemix deployment you are using. You can set this value with a ```BMSClient.REGION``` static property and use one of three values:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY
