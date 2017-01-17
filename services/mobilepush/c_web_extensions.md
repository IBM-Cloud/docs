---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Enabling Chrome Apps and Extensions to receive {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Last updated: 16 January 2017
{: .last-updated}

You can now enable Google Chrome Apps and Extensions to receive  {{site.data.keyword.mobilepushshort}}.

## Installing client SDK for {{site.data.keyword.mobilepushshort}}
{: #web_install}

This topic describes how to install and use the client JavaScript Push SDK to further develop your Chrome Apps and Extensions.

### Initializing in Google Chrome Apps and Extensions

For installing the Javascript SDK in Chrome Apps and Extensions, complete the steps:

Download the `BMSPushSDK.js` and `manifest_Chrome_Ext.json` (For chrome Extensions) or `manifest_Chrome_App.json` (for Chrome Apps) from the [Bluemix Web push SDK ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}.



- For Chrome Apps, configure the manifest file:
 1. In the `manifest_Chrome_App.json` file, provide the name, description, and icons.
 2. Add the `BMSPushSDK.js` in the `app.background.scripts`.
 3. Change the `manifest_Chrome_App.json` to `manifest.json`.

- For Chrome Extensions, configure the manifest file:
 1. In the `manifest_Chrome_Ext.json` file provide name, description, and icons.
 2. Add the `BMSPushSDK.js` in the `background.scripts`.
 3. Change the `manifest_Chrome_Ext.json` to `manifest.json`.

In the `background.js` file add the following to receive push notifications 
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked); 
```
	{: codeblock}



## Initializing the Push SDK 
{: #web_initialize}

Initialse the push SDK with Bluemix {{site.data.keyword.mobilepushshort}} service `app GUID` and `app Region`.  

To get your app GUID, select the **Configuration** option in the navigation pane for your initialized push services and click **Mobile Options**. Modify the code snippet to use your Bluemix push notifications service appGUID parameter.

The `App Region` specifies the location where the {{site.data.keyword.mobilepushshort}} service is hosted. You can use one of the three values:

 - For US Dallas:	 `.ng.bluemix.net`
 - For UK:			 `.eu-gb.bluemix.net`
 - For Sydney:		 `.au-syd.bluemix.net`

```
 var bmsPush = new BMSPush();
 function callback(response) {
 alert(response.response)
 }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Registering the Chrome Apps and Extensions
{: #web_register}

Use the `register()` API to register the device with {{site.data.keyword.mobilepushshort}} service. For registering from Google Chrome, add the Firebase Cloud Messaging (FCM) or Google Cloud Messaging (GCM) API Key and Web Site URL in the Bluemix {{site.data.keyword.mobilepushshort}} service web configuration dashboard. For more information, see [Configuring credentials for Google Cloud Messaging](t_push_provider_android.html) under Chrome setup.

For registering from Mozilla Firefox, add website URL in the Bluemix {{site.data.keyword.mobilepushshort}} service web configuration dashboard under Firefox setup.

Use the following code snippet to register in Bluemix {{site.data.keyword.mobilepushshort}} service.
```
var bmsPush = new BMSPush();
function callback(response) {
     alert(response.response)
  }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  }
  bmsPush.initialize(params, callback)
  bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}




