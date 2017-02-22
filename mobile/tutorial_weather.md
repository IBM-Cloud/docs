---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-31"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Tutorial - Weather Code Starter
{: #tutorial_weather}

The {{site.data.keyword.Bluemix}} Mobile Code Starter for Weather showcases a scaffold project to begin working with Weather, using Swift and includes Push and Analytics integration points.


## Requirements
{: #tutorial_requirements notoc}

* A [Bluemix ![External link icon](../icons/launch-glyph.svg "External link icon")](http://bluemix.net) Account
* A [Weather Company Data ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/weather-company-data/) service instance obtained from the [Bluemix Catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/)


## Getting Started
{: #tutorial_gs notoc}

To get up and running quickly with the Weather Code Starter, follow these steps:

1. Create a Mobile dashboard project in {{site.data.keyword.Bluemix_notm}}.

   1. From the **Getting Started** page in the Mobile dashboard, click **Create Project**.

      You can alternatively click **New Project** from the **Projects** page.

   2. Click **Code Starters**.

   3. Select **Weather** and click **Create Project**.

   4. Enter your project name and click **Create**.

2. Optional: Add the {{site.data.keyword.mobilepushshort}} capability.

   1. Click **Add** for **{{site.data.keyword.mobilepushshort}}** in the **Project Overview** page.

      You can alternatively click **Create** from the **{{site.data.keyword.mobilepushshort}}** page.

   2. Enter your service name and click **Create**.

   3. For iOS, [configure Apple Push Notification Service ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. For Android, [configure Google Cloud Messaging ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
3. Optional: Add the Analytics capability.

   1. Click **Add** for **Analytics** in the **Project Overview** page.

      You can alternatively click **Create** from the **Analytics** page.

   2. Enter your service name and click **Create**.
   
   3. Toggle off **Demo Mode** to see your analytics data after you run your app.

   4. See [Getting started with {{site.data.keyword.mobileanalytics_short}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobileanalytics/index.html){: new_window} for more information about configuring Analytics.

4. Optional: Add the Authentication capability.

   1. Click **Add** for **Authentication** on the **Project Overview** page.

      You can alternatively select **Create** on the **Authentication** page.

   2. Enter your service name and click **Create**.
   
   3. Toggle on **Authentication**.
   
   4. Select your identity provider and enter the required information to configure it. You can enable only one identity provider.

   5. See [Getting started with Mobile Client Access ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobileaccess/index.html){: new_window} for more information about configuring authentication.

5. Optional: Add the Data capability.

   1. Click **View** for **Data** on the **Project Overview** page.

      You can alternatively select **Create** on the **Data** page.
      
   2. Choose **{{site.data.keyword.cloudant_short_notm}}** or **{{site.data.keyword.objectstorageshort}}**.

   3. Enter your service name and click **Create**.

   4. See [Getting started with {{site.data.keyword.cloudant_short_notm}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/Cloudant/index.html){: new_window} for more information about configuring {{site.data.keyword.cloudant_short_notm}}.

   5. [Getting started with {{site.data.keyword.objectstorageshort}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/ObjectStorage/index.html){: new_window} for more information about configuring {{site.data.keyword.objectstorageshort}}.

6. Download your project.

   1. Click **Code** and select your preferred language.

   2. Click **Download Code**.

7. Extract the archive and follow the instructions in the `README.md` file.


## What to do next
{: #tutorial_next notoc}

View other tutorials.


### Code Starter tutorials
{: #tutorials_Code notoc}

* [Tutorial - Basic](tutorial.html)
* [Tutorial - Cloudant Sync](tutorial_cloudant_sync.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutorial - Watson {{site.data.keyword.conversationshort}}](tutorial_conversation.html)
* [Tutorial - Watson Language](tutorial_watson_language.html)
