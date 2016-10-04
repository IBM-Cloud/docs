
---

copyright:
years: 2015, 2016

---

{:new_window: target="_blank"}
# Configuring credentials for Google cloud messaging (GCM)
{: #create-push-enable-gcm}
Last updated: 26 September 2016
{: .last-updated}

Google Cloud Messaging (GCM) is the gateway used to deliver push notifications to Android devices, Google Chrome and Mozilla web browsers. Get your Google Cloud Messaging (GCM) credentials, and then set up the {{site.data.keyword.mobilepushshort}} service on the dashboard.

##Getting Your Sender ID and API key
{: #android-senderid-apikey}

The API key is stored securely and used by the {{site.data.keyword.mobilepushshort}} service to connect to the GCM server and the sender ID (project number) is used by the Android SDK and the JS SDK for  Google Chrome and Mozilla Firefox on the client side. For more information about  Sender ID, see [Google Cloud Message](https://developers.google.com/cloud-messaging/gcm#arch).

1. Get a Google Development account at [Google Dev Console](https://console.developers.google.com/start){: new_window}. For more information about Google Cloud Messaging (GCM), see [Creating a Google API Project](https://developers.google.com/console/help/new/){: new_window}.
2. To create a Google project, follow the [Google documentation](https://developers.google.com/cloud-messaging/android/start#create-an-api-project).
3. Get the GCM API key and Sender ID from the Google app settings.


##Setting up {{site.data.keyword.mobilepushshort}} service for Android
{: #setup-push-android}

**Note:** You will need your GCM API Key and Sender ID (project number).

1. Open your Bluemix dashboard and then click the {{site.data.keyword.mobilepushfull}} service instance you have created, to open the dashboard. The Push dashboard is displayed. To set up an unbound {{site.data.keyword.mobilepushshort}} service for Android, select the Unbound {{site.data.keyword.mobilepushshort}} service icon to open the {{site.data.keyword.mobilepushshort}} service dashboard. 
 ![Push dashboard](images/push_unbound.jpg)

2. Click the **Setup Push** button, to configure the GCM credentials.
3. On the **Configuration** tab, go to the **Google Cloud Messaging** section and configure the Sender ID (GCM project number) and API Key.
4. Click **Save**.
5. Next steps. [Enabling notifications for Android](c_enable_push.html).

###Configuring for Google Chrome and Mozilla Firefox web push (using GCM)
{: #config-gcm-mozilla}

1. On the Push Dashboard navigation pane, select **Configure**.
2. Select the Web tab.
	![WebPush Configurations](images/webpush_configure.jpg)
3. Configure the GCM API key and the URL of your website that will be registering for Push Notifications.
4. Click **Save**.
5. Next steps. [Enabling notifications for Google Chrome and Mozilla Firefox browsers](c_enable_push.html).
