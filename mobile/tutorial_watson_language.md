---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Tutorial - Watson Language Code Starter
{: #tutorial_watson_language}

The {{site.data.keyword.Bluemix}} Mobile Code Starter for Watson Language showcases the Text To Speech and Language Translation services from Watson and gives you integration points for each of the {{site.data.keyword.Bluemix_notm}} Mobile services.


## Requirements
{: #tutorial_requirements}

* A [Bluemix ![External link icon](../icons/launch-glyph.svg "External link icon")](http://bluemix.net) Account
* [Language Translator ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/language-translator/) and [Text to Speech ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/text-to-speech/) service instances obtained from the [Bluemix Catalog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/)


## Getting Started
{: #tutorial_gs}

To get up and running quickly with the Watson Language Code Starter, follow these steps:

1. Create a Mobile dashboard project in {{site.data.keyword.Bluemix_notm}}.

   1. From the **Getting Started** page in the Mobile dashboard, click **Create Project**.

      You can alternatively click **Create Project** from the **Projects** page.

   2. Click **Code Starters**.

   3. Select **Watson Language** and click **Create Project**.

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

5. Download your project.

   1. Click **Code** and select your preferred language.

   2. Click **Download Code**.

6. Extract the archive and view the `README.md` file in a Markdown viewer to complete the setup.


## What to do next
{: #tutorial_next}

[Try it out! ![External link icon](../icons/launch-glyph.svg "External link icon")](http://console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375){: new_window}



### UI Starter tutorials
{: #tutorials_UI}

* [Tutorial - Store Catalog](tutorial_store_catalog.html)


### Code Starter tutorials
{: #tutorials_Code}

* [Tutorial - Basic](tutorial.html)
* [Tutorial - Cloudant Sync](tutorial_cloudant_synd.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutorial - Weather](tutorial_weather.html)

