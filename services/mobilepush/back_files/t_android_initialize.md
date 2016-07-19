---

copyright:
 years: 2015, 2016

---

# Initializing the Push SDK for Android apps
{: #android_initialize}

A common place to put the initialization code is in the onCreate method of the main activity in your Android application.

Click the **Mobile Options** link in your Bluemix Application Dashboard to get the application route and applicationGUID. Use these values for your route and App GUID. Modify the code snippet to use your Bluemix app appRoute and appGUID parameters.


##Initialize the Core SDK

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

Specifies the route that is assigned to the server application that you created on Bluemix.

**AppGUID**

Specifies the unique key that is assigned to the application that you created on Bluemix. This value is case-sensitive.

**bluemixRegionSuffix**

Specifies the location where the app hosted. You can use one of three values:

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

##Initialize the client Push SDK

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
