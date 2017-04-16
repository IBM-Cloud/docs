---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuring credentials for FCM
{: #create-push-enable-gcm}
Last updated: 16 January 2017
{: .last-updated}

Firebase Cloud Messaging (FCM) is the gateway used to deliver push notifications to Android devices and Google Chrome. FCM is the new version of Google Cloud Messaging (GCM). To set up the {{site.data.keyword.mobilepushshort}} service on the dashboard, you need to get your FCM credentials. Ensure that you use FCM configurations for new apps. Existing apps would continue to function with GCM configurations.

## Getting Your Sender ID and API key
{: #android-senderid-apikey}

The API key is stored securely and used by the {{site.data.keyword.mobilepushshort}} service to connect to the FCM server and the sender ID (project number) is used by the Android SDK and the JS SDK for  Google Chrome and Mozilla Firefox on the client side. 

To setup the FCM, generate the API key and Sender ID, complete the steps:

1. Visit the [Firebase Console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.firebase.google.com/?pli=1){: new_window}.
2. Select **Create new project**. 
3. In the Create a project window, provide a project name, choose a country/region and click **Create project**.
3. In the navigation pane, click the Settings icon and select **Project settings**.
4. Choose the Cloud Messaging tab to generate a Server API Key and a Sender ID.

## Setting up {{site.data.keyword.mobilepushshort}} service for Android and Chrome Apps and Extensions
{: #setup-push-android}

**Note:** You will need your FCM/GCM API Key and Sender ID (project number).

1. Open your Bluemix dashboard and then click the {{site.data.keyword.mobilepushfull}} service instance you have created, to open the dashboard. The Push dashboard is displayed. To set up an unbound {{site.data.keyword.mobilepushshort}} service for Android, select the Unbound {{site.data.keyword.mobilepushshort}} service icon to open the {{site.data.keyword.mobilepushshort}} service dashboard. 

![Push dashboard](images/push_unbound.jpg)

2. Click the **Setup Push** button, to configure the FCM/GCM credentials for Android applications and Google Chrome Apps and Extensions.
3. On the **Configuration** page, for Android, go to the **Mobile** tab and configure the Sender ID (GCM project number) and API Key. For Google Chrome Apps and Extensions, go to the **Web** tab and configure the Sender ID (FCM/GCM project number) and API Key appropriately.
4. Click **Save**.
5. Next steps. [Enabling notifications for Android](c_enable_push.html) or [Enabling notifications for Google Chrome Apps & Extensions](c_enable_push.html).


