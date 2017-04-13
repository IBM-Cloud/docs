---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"
---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Important: The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.**

# Setting up the Android SDK
{: #getting-started-android}

Instrument your Android application with the {{site.data.keyword.amafull}} client SDK, initialize the SDK, and make requests to protected and unprotected resources.
{: shortdesc}

## Before you begin
{: #before-you-begin}

You must have:

* An instance of a  {{site.data.keyword.Bluemix_notm}} application.
* An instance of a {{site.data.keyword.amafull}} service.
* Your **TenantID**. Open your service in the  {{site.data.keyword.amafull}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  values are displayed in the  **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Your **Application Route**. This is the URL of your back-end application. You need this value for for sending requests to its protected endpoints.
* Your {{site.data.keyword.Bluemix_notm}} **Region**.  You can find your current {{site.data.keyword.Bluemix_notm}} region in the header, next to the **Avatar** icon ![Avatar icon](images/face.jpg "Avatar icon"). The region value that appears should be one of the following: `US South`,  `Sydney`, or  `United Kingdom`, and correspond to the SDK values required in the code: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY`, or `BMSClient.REGION_UK`. You will need this value for initializing the {{site.data.keyword.amashort}} client.
* An Android Studio project, set up to work with Gradle. For more information about how to set up your Android development environment, see [Google Developer Tools  ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/sdk/index.html){: new_window}.

## Installing the {{site.data.keyword.amashort}} client SDK
{: #install-mca-sdk}

The {{site.data.keyword.amashort}} client SDK is distributed with Gradle, a dependency manager for Android projects. Gradle automatically downloads artifacts from repositories, and makes them available to your Android application.

1. Create an Android Studio project, or open an existing project.

1. Open the `build.gradle` file for your application (**not** the project `build.gradle` file).

1. Find the **dependencies** section of the `build.gradle` file.  Add a compile dependency for the {{site.data.keyword.amashort}} client SDK:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
		name:'core',
		version: '2.+',
		ext: 'aar',
		transitive: true
		// other dependencies  
	}
	```
	{: codeblock}

1. Synchronize your project with Gradle. Click **Tools &gt; Android &gt; Sync Project with Gradle Files**.

1. Open the `AndroidManifest.xml` file for your Android project. Add internet access permission under the `<manifest>` element:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

## Initializing the {{site.data.keyword.amashort}} client SDK
{: #initalize-mca-sdk}

Initialize the client SDK  by passing the **context** and **region** parameters to the `initialize` method. A common, though not mandatory, place to put the initialization code is in the `onCreate` method of the main activity in your Android application.

```Java
BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

BMSClient.getInstance().setAuthorizationManager(
	MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));
```
{: codeblock}

* Replace `<applicationBluemixRegion>` with the region where your {{site.data.keyword.Bluemix_notm}} service is hosted.
* Replace `<MCAServiceTenantId>` with the **tenantId**

For more information on these values, see [Before you begin](#before-you-begin).

## Making a request to your mobile back-end application
{: #request}

After the {{site.data.keyword.amashort}} client SDK is initialized, you can start making requests to your mobile back-end application.

1. Try to send a request to a protected endpoint of your mobile back-end application. In your browser, open the following URL: `{applicationRoute}/protected` (for example `http://my-mobile-backend.mybluemix.net/protected`).   

	The `/protected` endpoint of a mobile back-end application that was created with MobileFirst Services Starter boilerplate is protected with {{site.data.keyword.amashort}}. An `Unauthorized` message is returned in your browser, because this endpoint can only be accessed by mobile applications that are instrumented with the {{site.data.keyword.amashort}} client SDK.

1. Use your Android application to make a request to the same endpoint. Add the following code after you initialize `BMSClient`:

	```Java
	Request request = new Request("http://my-mobile-backend.mybluemix.net/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```
	{: codeblock}

1. When your request succeeds, you will see the following output in the LogCat utility:

	![image](images/getting-started-android-success.png)

## Next steps
{: #next-steps}

When you connected to the protected endpoint, no credentials were required. To require your users to log in to your application, you must configure Facebook, Google, or custom authentication.

* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Custom](custom-auth-android.html)
