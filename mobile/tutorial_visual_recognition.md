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

# End-to-end tutorial of the {{site.data.keyword.visualrecognitionshort}} Code Starter
{: #tutorial_vr}

The following end-to-end tutorial walks through the steps to create a project from the {{site.data.keyword.visualrecognitionshort}} Code Starter, including the tools that you must have installed, and subsequently, the steps to run the starter in Xcode and Android Studio.


## Installing developer tools
{: #dev_tools notoc}

Ensure that you have installed the [prerequisite developer tools ![External link icon](../icons/launch-glyph.svg "External link icon")](get_code.html#prereq-dev-tools){: new_window}.


## Creating a project from the {{site.data.keyword.visualrecognitionshort}} Code Starter
{: #create_project notoc}

1. Create a Mobile dashboard project in {{site.data.keyword.Bluemix}}.

   1. From the **Getting Started** page in the Mobile dashboard, click **Create Project**.

      You can alternatively click **Create Project** from the **Projects** page.

   2. Click **Code Starters**.

   3. Select **Visual Recognition** and click **Create Project**.

   4. Enter your project name. For this tutorial, use `VisualRecognitionProject`.
   
   5. Click **Create**.

2. Optional: Add the {{site.data.keyword.mobilepushshort}} capability.

   1. Click **Add** for **{{site.data.keyword.mobilepushshort}}** in the **Project Overview** page.

      You can alternatively click **Create** from the **{{site.data.keyword.mobilepushshort}}** page.

   2. Enter your service name and click **Create**.

   3. For iOS, [configure Apple Push Notification Service ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. For Android, [configure Firebase Cloud Messaging ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
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

   5. See [Getting started with {{site.data.keyword.amashort}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobileaccess/index.html){: new_window} for more information about configuring Authentication.

5. Optional: Add the Data capability.

   1. Click **View** for **Data** on the **Project Overview** page.

      You can alternatively select **Create** on the **Data** page.
      
   2. Choose **{{site.data.keyword.cloudant_short_notm}}** or **{{site.data.keyword.objectstorageshort}}**.

   3. Enter your service name and click **Create**.

   4. See [Getting started with {{site.data.keyword.cloudant_short_notm}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/Cloudant/index.html){: new_window} for more information about configuring {{site.data.keyword.cloudant_short_notm}}.

   5. [Getting started with {{site.data.keyword.objectstorageshort}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/ObjectStorage/index.html){: new_window} for more information about configuring {{site.data.keyword.objectstorageshort}}.

6. Generate your project code.

   1. Click **Get Code** on the **Project Overview** page to select your platform and language.
   
      You can alternatively click on the **Code** page.
      
   2. For iOS, click **iOS Swift**.
   
   3. For Android, click **Android**.
   
   4. When the project code is finished generating, click **Download Code** to download your project archive.


## Running your project in Xcode
{: #run_xcode notoc}

1. Extract the `VisualRecognitionProject-Swift.zip` file.

2. Open the `README.md` file in a Markdown viewer to review the steps to configure your project.

   1. Create your [{{site.data.keyword.visualrecognitionshort}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window} service instance.
   
   2. Open your Terminal and navigate to your project folder.
   
      1. Run `pod setup` if you need to set up your CocoaPods repository.
      
      2. Run `pod update` if you need to update you update your existing pods.
      
      3. Run `pod install` to install the pods that are required for your project.
      
      4. Run `carthage update --platform iOS` to build the dependencies and frameworks to use the {{site.data.keyword.ibmwatson}} Developer Cloud iOS SDK.
      
   3. Open your `VisualRecognitionProject.xcworkspace` Xcode workspace.
   
   4. Add your {{site.data.keyword.visualrecognitionshort}} service credentials.
   
      1. Copy your `api_key` from  your {{site.data.keyword.visualrecognition}} service credentials.
      
      2. Paste your `api_key` into the `VisualRecognitionAPIKey` key into the `WatsonCredentials.plist` file.
      
3. Run your app.


## Running your project in Android Studio
{: #run_studio notoc}

1. Extract the `VisualRecognitionProject-Android.zip` file.

2. Open the `README.md` file in a Markdown viewer to configure your project.

   1. Create your [{{site.data.keyword.visualrecognitionshort}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window} service instance.
   
      Skip this step if you already have a {{site.data.keyword.visualrecognitionshort}} service instance.
   
   2. Open your `VisualRecognitionProject-Android` project in Android Studio.
   
   4. Add your {{site.data.keyword.visualrecognitionshort}} service credentials.
   
      1. Copy your `api_key` from  your {{site.data.keyword.visualrecognitionshort}} service credentials.
      
      2. Paste your `api_key` into the `watson_visual_recognition_api_key` key into the `res/values/watson_credentials.xml` file.
      
3. Run your app.


## What to do next
{: #what_next notoc}

View other tutorials.


### Code Starter tutorials
{: #tutorials_Code notoc}

* [Tutorial - Basic](tutorial.html)
* [Tutorial - Cloudant Sync](tutorial_cloudant_sync.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - Watson {{site.data.keyword.conversationshort}}](tutorial_conversation.html)
* [Tutorial - Watson Language](tutorial_watson_language.html)
* [Tutorial - Weather](tutorial_weather.html)

