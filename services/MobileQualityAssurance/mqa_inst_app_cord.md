---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Instrumenting MQA with a Cordova app (Deprecated)
{: #instrumentcord}

To use {{site.data.keyword.mqafull}} with your Cordova app, you must download the SDK and instrument it by making some changes using the command-line interface.
{: shortdesc}

Before you can instrument an app with {{site.data.keyword.mqa}}, you must have a {{site.data.keyword.Bluemix}} account and the correctly installed version of the development environment for the platforms of the app you that are instrumenting.

To instrument {{site.data.keyword.mqa}} to work with your Cordova app, complete the following tasks:

1. Add the required permissions and downloaded SDK to your Cordova project.

	1. Open a command prompt and navigate to the directory that contains your project files.
	
	2. Add the {{site.data.keyword.mqa}} plug-in to your Cordova project by completing the following steps, depending on your environment:
		
		**Important**: If you are using Xcode 7.x on iOS 9, you must set the Enable Bitcode setting to No in the Xcode Build Settings. You can change this setting by opening Xcode using the Cordova project file .xcodeproj, which is located in the platform\iPhone folder.

		* IBM MobileFirst™ Platform Foundation Version 7.1:
			
			1. Enter the following command to install the {{site.data.keyword.mqa}} plugin:

				```
				mfp cordova plugin add plugin_location
				```
				{: codeblock}

			Where *plugin_location* is the path to the directory of the extracted {{site.data.keyword.mqa}} plug-in that you downloaded.
        
			2. If your app runs on Android, rename the ```project_name/app_name/platforms/android/custom_rules.xml``` file to ```custom_rules.xml.bak```.
		
		* Apache Cordova earlier than version 4.0:
			1. Enter the following command to install the {{site.data.keyword.mqa}} plugin:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Where *plugin_location* is the path to the directory of the extracted {{site.data.keyword.mqa}} plug-in that you downloaded.
        
			2. Enter the following command to add an additional required plugin:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. If your app runs on Android, rename the ```project_name/app_name/platforms/android/custom_rules.xml``` file to ```custom_rules_bak.xml```.

		* Apache Cordova version 4.0, or later:

			1. Enter the following command:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Where *plugin_location* is the path to the directory of the extracted {{site.data.keyword.mqa}} Cordova plug-in that you downloaded.
    
			2. Enter the following command to add an additional required plugin:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. Start a new session of {{site.data.keyword.mqa}} with each log in.

	1. Open the ```index.js``` file that is in the following directory: ```your_project_name\www\js```.
	
	2. Add the following function and parameters inside the ```onDeviceReady()``` function that is in the ```index.js``` file. Place the function before the end brace of the function.
	
	Restriction: For an app that is already instrumented for Mobile Quality Assurance using an older version of the plug-in for Cordova to use the features that are included in the Mobile Quality Assurance plug-in for Cordova version 3.0.18, and later, you must regenerate and replace your app key. For more information about how to regenerate your app key, see Managing app settings. App keys that were generated earlier than February 2016 continue to work with the older plug-in, but no longer work after you upgrade your plug-in to version 3.0.18, or later.
	
		```
		MQA.startNewSession(
			{
				mode: "QA",
				// or mode: "MARKET" for production mode.
			android: {
				appKey: "your_MQA_Android_appKey" ,
				notificationsEnabled: true},
			ios: {
				appKey: "your_MQA_iOS_appKey" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session 
			   Started successfully");},
			error: function (string) { console.log("Session 
			   error" + string);}
			}
			); 
		```
		{: codeblock}
	
	3. Continue with the steps in [Getting started with {{site.data.keyword.mqa}}](index.html).
	
		

# Related Links
{: #rellinks notoc}

## Related Links
{: #general notoc}
* [Getting started with {{site.data.keyword.mqa}}](index.html){:new_window}
