
---

copyright:
years: 2015, 2016

---

{:new_window: target="_blank"}
# Configuring credentials for FCM
{: #create-push-enable-gcm}
Last updated: 14 October 2016
{: .last-updated}

Firebase Cloud Messaging (FCM) is the gateway used to deliver push notifications to Android devices, Google Chrome and Mozilla web browsers. FCM has replaced Google Cloud Messaging (GCM). You need to get your FCM credentials, and then set up the {{site.data.keyword.mobilepushshort}} service on the dashboard. Ensure that you use FCM configurations for new apps. Existing apps can continue to function with the GCM configurations.

##Getting Your Sender ID and API key
{: #android-senderid-apikey}

The API key is stored securely and used by the {{site.data.keyword.mobilepushshort}} service to connect to the FCM server and the sender ID (project number) is used by the Android SDK and the JS SDK for  Google Chrome and Mozilla Firefox on the client side. 

To setup the FCM, generate the API key and Sender ID, complete the steps:

1. Visit the [Firebase Console](https://console.firebase.google.com/?pli=1).
2. Select **Create new project**. 
3. In the Create a project window, provide a project name, choose a country/region and click **Create project**.
3. In the navigation pane, click the Settings icon and select **Project settings**.
4. Choose the Cloud Messaging tab to generate a Server API Key and a Sender ID.

##Setting up {{site.data.keyword.mobilepushshort}} service for Android
{: #setup-push-android}

**Note:** You will need your FCM/GCM API Key and Sender ID (project number).

1. Open your Bluemix dashboard and then click the {{site.data.keyword.mobilepushfull}} service instance you have created, to open the dashboard. The Push dashboard is displayed. To set up an unbound {{site.data.keyword.mobilepushshort}} service for Android, select the Unbound {{site.data.keyword.mobilepushshort}} service icon to open the {{site.data.keyword.mobilepushshort}} service dashboard. 

![Push dashboard](images/push_unbound.jpg)

2. Click the **Setup Push** button, to configure the FCM/GCM credentials.
3. On the **Configuration** tab, go to the **Google Cloud Messaging** section and configure the Sender ID (FCM/GCM project number) and API Key.
4. Click **Save**.
5. Next steps. [Enabling notifications for Android](c_enable_push.html).

###Configuring for Google Chrome and Mozilla Firefox web push (using FCM/GCM)
{: #config-gcm-mozilla}

1. On the Push Dashboard navigation pane, select **Configure**.
2. Select the Web tab.
	![WebPush Configurations](images/webpush_configure.jpg)
3. Configure the FCM/GCM API key and the URL of your website that will be registered to receive push notifications.
4. Click **Save**.
5. Next steps. [Enabling notifications for Google Chrome and Mozilla Firefox browsers](c_enable_push.html).
